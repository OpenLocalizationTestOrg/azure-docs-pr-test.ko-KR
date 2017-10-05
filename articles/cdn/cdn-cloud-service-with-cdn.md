---
title: "Azure CDN과 Azure 클라우드 서비스 통합 | Microsoft Docs"
description: "통합 Azure CDN 끝점에서 콘텐츠를 제공하는 클라우드 서비스의 배포 방법에 대해 알아봅니다."
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="3a442-103"><a name="intro"></a> Azure CDN과 클라우드 서비스 통합</span><span class="sxs-lookup"><span data-stu-id="3a442-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="3a442-104">클라우드 서비스는 Azure CDN과 통합되어 클라우드 서비스의 위치에 있는 모든 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="3a442-105">이 접근 방식을 통해 다음과 같은 장점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="3a442-106">클라우드 서비스 프로젝트 디렉터리의 이미지, 스크립트 및 스타일시트를 쉽게 배포 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="3a442-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="3a442-107">jQuery 또는 부트스트랩 버전과 같은 클라우드 서비스의 NuGet 패키지를 쉽게 업그레이드</span><span class="sxs-lookup"><span data-stu-id="3a442-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="3a442-108">동일한 Visual Studio 인터페이스에서 웹 응용 프로그램 및 CDN 제공 콘텐츠 모두 관리</span><span class="sxs-lookup"><span data-stu-id="3a442-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="3a442-109">웹 응용 프로그램 및 CDN 제공 콘텐츠에 대한 통합 배포 워크플로</span><span class="sxs-lookup"><span data-stu-id="3a442-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="3a442-110">ASP.NET 묶음 및 축소를 Azure CDN과 통합</span><span class="sxs-lookup"><span data-stu-id="3a442-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3a442-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="3a442-111">What you will learn</span></span>
<span data-ttu-id="3a442-112">이 자습서에서는 다음 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="3a442-113">Azure CDN 끝점을 클라우드 서비스와 통합하여 Azure CDN에서 웹 페이지의 정적 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="3a442-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="3a442-114">클라우드 서비스의 정적 콘텐츠에 대한 캐시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="3a442-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="3a442-115">Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="3a442-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="3a442-116">Visual Studio의 스크립트 디버깅 환경은 유지하면서 Azure CDN을 통해 묶이고 축소된 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="3a442-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="3a442-117">Azure CDN이 오프라인인 경우 스크립트 및 CSS 대체 구성</span><span class="sxs-lookup"><span data-stu-id="3a442-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="3a442-118">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="3a442-118">What you will build</span></span>
<span data-ttu-id="3a442-119">기본 ASP.NET MVC 템플릿을 사용하여 클라우드 서비스 웹 역할을 배포하고, 코드를 추가하여 통합 Azure CDN에서 이미지, 컨트롤러 작업 결과, 기본 JavaScript 및 CSS 파일과 같은 콘텐츠를 제공하고, 코드를 작성하여 CDN이 오프라인인 경우에 제공할 번들의 대체 메커니즘을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="3a442-120">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="3a442-120">What you will need</span></span>
<span data-ttu-id="3a442-121">이 자습서를 사용하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="3a442-122">활성 [Microsoft Azure 계정](/account/)</span><span class="sxs-lookup"><span data-stu-id="3a442-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="3a442-123">[Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="3a442-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="3a442-124">이 자습서를 완료하려면 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="3a442-125">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/) 할 수 있음 - 유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 되며 크레딧을 모두 사용한 후에도 계정을 유지하고 무료 Azure 서비스(예: 웹 서비스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="3a442-126">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음 - MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="3a442-127">클라우드 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="3a442-127">Deploy a cloud service</span></span>
<span data-ttu-id="3a442-128">이 섹션에서는 Visual Studio 2015에서 기본 ASP.NET MVC 응용 프로그램 템플릿을 클라우드 서비스 웹 역할에 배포한 후 새로운 CDN 끝점과 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="3a442-129">아래의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="3a442-130">Visual Studio 2015의 메뉴 모음에서 **파일 > 새로 만들기 > 프로젝트 > 클라우드 > Azure 클라우드 서비스**로 이동하여 새 Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="3a442-131">해당 서비스의 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="3a442-132">**ASP.NET 웹 역할**을 선택하고 **>** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="3a442-133">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="3a442-134">**MVC**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="3a442-135">이제 이 웹 역할을 Azure 클라우드 서비스에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="3a442-136">클라우드 서비스 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="3a442-137">아직 Microsoft Azure에 로그인하지 않은 경우 **계정 추가...** 드롭다운을 클릭하고 **계정 추가** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="3a442-138">로그인 페이지에서 Azure 계정을 활성화하는 데 사용한 Microsoft 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="3a442-139">로그인했으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="3a442-140">Visual Studio에서는 클라우드 서비스 또는 저장소 계정이 생성되지 않았다고 가정하고 두 계정의 생성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="3a442-141">**클라우드 서비스 및 계정 만들기** 대화 상자에서 원하는 서비스 이름을 입력하고 원하는 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="3a442-142">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="3a442-143">게시 설정 페이지에서 구성을 확인하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="3a442-144">클라우드 서비스를 게시하는 프로세스는 시간이 조금 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="3a442-145">모든 웹 역할에 대해 웹 배포 사용 옵션을 사용하면 웹 역할에 대한 신속한(하지만 임시적) 업데이트를 제공함으로써 클라우드 서비스를 훨씬 빠르게 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="3a442-146">이 옵션에 대한 자세한 내용은 [Azure Tools를 사용하여 클라우드 서비스 게시](http://msdn.microsoft.com/library/ff683672.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="3a442-147">**Microsoft Azure 활동 로그**에서 게시 상태가 **완료**로 표시된 경우 이 클라우드 서비스와 통합된 CDN 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="3a442-148">게시 후, 배포된 클라우드 서비스에서 오류 화면을 표시하는 경우 개발한 클라우드 서비스가 [.NET 4.5.2가 포함되지 않은 게스트 OS](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates)를 사용하고 있기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="3a442-149">[시작 작업으로 .NET 4.5.2를 배포](../cloud-services/cloud-services-dotnet-install-dotnet.md)하여 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="3a442-150">새 CDN 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="3a442-150">Create a new CDN profile</span></span>
<span data-ttu-id="3a442-151">CDN 프로필은 CDN 끝점의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="3a442-152">각 프로필에는 CDN 끝점이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="3a442-153">여러 프로필을 사용하여 인터넷 도메인, 웹 응용 프로그램 또는 일부 기타 조건에서 CDN 끝점을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="3a442-154">이미 이 자습서에 사용하려는 CDN 프로필이 있는 경우 [새 CDN 끝점 만들기](#create-a-new-cdn-endpoint)로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="3a442-155">새 CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="3a442-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="3a442-156">**저장소 계정에 대한 새 CDN 끝점을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="3a442-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="3a442-157">[Azure 관리 포털](https://portal.azure.com)에서 CDN 프로필로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="3a442-158">이전 단계에서 대시보드에 고정해 놓았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="3a442-159">그렇지 않은 경우 **찾아보기**, **CDN 프로필**을 차례로 클릭한 다음 끝점을 추가하려는 프로필을 클릭하면 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="3a442-160">CDN 프로필 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-160">The CDN profile blade appears.</span></span>
   
    ![CDN 프로필][cdn-profile-settings]
2. <span data-ttu-id="3a442-162">**끝점 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-162">Click the **Add Endpoint** button.</span></span>
   
    ![끝점 추가 단추][cdn-new-endpoint-button]
   
    <span data-ttu-id="3a442-164">**끝점 추가** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-164">The **Add an endpoint** blade appears.</span></span>
   
    ![끝점 추가 블레이드][cdn-add-endpoint]
3. <span data-ttu-id="3a442-166">이 CDN 끝점에 대한 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="3a442-167">이 이름은 `<EndpointName>.azureedge.net`도메인의 캐시된 리소스에 액세스하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="3a442-168">**원본 형식** 드롭다운에서 *클라우드 서비스*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="3a442-169">**원본 호스트 이름** 드롭다운에서 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="3a442-170">**원본 경로**, **원본 호스트 헤더** 및 **프로토콜/원본 포트**에 대한 기본값을 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="3a442-171">하나 이상의 프로토콜(HTTP 또는 HTTPS)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="3a442-172">**추가** 단추를 클릭하여 새 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="3a442-173">끝점이 만들어지면 프로필에 대한 끝점 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="3a442-174">목록 보기에는 캐시된 콘텐츠에 액세스하는 데 사용할 URL과 원본 도메인이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![CDN 끝점][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="3a442-176">끝점은 즉시 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="3a442-177">CDN 네트워크를 통해 등록을 전파하는 데 최대 90분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="3a442-178">사용자가 CDN 도메인 이름을 즉시 사용하려고 시도할 경우 CDN을 통해 콘텐츠를 사용할 수 있을 때까지 상태 코드 404가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="3a442-179">CDN 끝점 테스트</span><span class="sxs-lookup"><span data-stu-id="3a442-179">Test the CDN endpoint</span></span>
<span data-ttu-id="3a442-180">게시 상태가 **완료됨**인 경우 브라우저 창을 열고 **http://<cdnName>*.azureedge.net/Content/bootstrap.css**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="3a442-181">이 자습서 설정에서 이 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="3a442-182">이는 CDN 끝점의 다음 원본 URL과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="3a442-183">**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**로 이동한 경우 브라우저에 따라 게시한 웹앱에서 제공한 bootstrap.css를 다운로드하거나 열라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="3a442-184">마찬가지로 CDN 끝점에서 **http://*&lt;서비스 이름>*.cloudapp.net/**의 공개적으로 액세스 가능한 URL에 바로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="3a442-185">예:</span><span class="sxs-lookup"><span data-stu-id="3a442-185">For example:</span></span>

* <span data-ttu-id="3a442-186">/Script 경로의 .js 파일</span><span class="sxs-lookup"><span data-stu-id="3a442-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="3a442-187">/Content 경로의 모든 콘텐츠 파일</span><span class="sxs-lookup"><span data-stu-id="3a442-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="3a442-188">모든 controller/action</span><span class="sxs-lookup"><span data-stu-id="3a442-188">Any controller/action</span></span>
* <span data-ttu-id="3a442-189">CDN 끝점에서 쿼리 문자열을 사용하도록 설정한 경우 쿼리 문자열이 포함된 모든 URL</span><span class="sxs-lookup"><span data-stu-id="3a442-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="3a442-190">실제로 위의 구성을 사용하면 **http://*&lt;cdnName>*.azureedge.net/**에서 전체 클라우드 서비스를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="3a442-191">**http://camservice.azureedge.net/**으로 이동하면 Home/Index에서 작업 결과를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="3a442-192">그러나 Azure CDN을 통해 전체 클라우드 서비스를 제공하는 것이 항상 바람직하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="3a442-193">CDN이 새로운 버전의 자산을 원본 서버에서 매우 자주 풀해야 하므로 고정 배달 최적화를 포함한 CDN은 동적 자산의 배달 속도를 반드시 높이지 않으며 따라서 캐시되지 않거나 매우 자주 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="3a442-194">이 시나리오에서는 CDN 끝점에서 DSA([동적 사이트 가속](cdn-dynamic-site-acceleration.md)) 최적화를 사용할 수 있습니다. 이 기능은 캐시 불가능한 동적 자산의 배달 속도를 향상시키기 위한 다양한 기술을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="3a442-195">고정 및 동적 콘텐츠가 혼합된 사이트가 있는 경우 고정 최적화 형식(예: 일반 웹 배달)을 사용하여 CDN에서 고정 콘텐츠를 실행하고 상황에 따라 DSA 최적화를 설정하여 원본 서버에서 직접 또는 CDN 끝점을 통해 들어오는 동적 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="3a442-196">이를 위해 CDN 끝점에서 개별 콘텐츠 파일에 액세스하는 방법을 이미 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="3a442-197">Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공에서는 특정 CDN 끝점을 통해 특정 컨트롤러 작업을 제공하는 방법을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="3a442-198">대안은 클라우드 서비스의 사례별로 Azure CDN에서 제공할 콘텐츠를 판단하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="3a442-199">이를 위해 CDN 끝점에서 개별 콘텐츠 파일에 액세스하는 방법을 이미 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="3a442-200">[Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공](#controller)에서는 CDN 끝점을 통해 특정 컨트롤러 작업을 제공하는 방법을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="3a442-201">클라우드 서비스의 정적 파일에 대한 캐싱 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="3a442-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="3a442-202">클라우드 서비스의 Azure CDN 통합으로 정적 콘텐츠를 CDN 끝점에서 캐시하는 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="3a442-203">이를 수행하려면 웹 역할 프로젝트(예: WebRole1)에서 *Web.config*를 열고 `<staticContent>` 요소를 `<system.webServer>`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="3a442-204">아래 XML은 캐시가 3일 이내에 만료되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="3a442-205">이렇게 구성하면 클라우드 서비스의 모든 정적 파일이 CDN 캐시에서 동일한 규칙을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="3a442-206">캐싱 설정을 더 세밀하게 제어하려면 *Web.config* 파일을 폴더에 추가하고 이 파일에 해당 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="3a442-207">예를 들어 *Web.config* 파일을 *\Content* 폴더에 추가하고 다음 XML로 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="3a442-208">이 설정을 통해 *\Content* 폴더의 모든 정적 파일은 15일 동안 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="3a442-209">`<clientCache>` 요소를 구성하는 방법에 대한 자세한 내용은 [클라이언트 캐시 &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="3a442-210">[Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공](#controller)에서는 CDN 캐시의 컨트롤러 작업 결과에 대해 캐시 설정을 구성하는 방법에 관해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="3a442-211">Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="3a442-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="3a442-212">클라우드 서비스 웹 역할을 Azure CDN과 통합한 경우 Azure CDN을 통해 컨트롤러 작업의 콘텐츠를 비교적 쉽게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="3a442-213">[Maarten Balliauw](https://twitter.com/maartenballiauw)는 Azure CDN을 통해 직접 클라우드 서비스를 제공(위에서 설명함)하지 않고 [Azure CDN으로 웹 대기 시간 단축](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN)에서 재미있는 MemeGenerator 컨트롤러로 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="3a442-214">여기서 그 방법을 간단히 재현해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="3a442-215">클라우드 서비스에서 다음과 같은 젊은 척 노리스의 이미지( [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)제공 사진)를 기반으로 하여 밈을 생성하려고 한다고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="3a442-216">고객이 최상급 이미지를 지정한 후 작업에 게시하면 밈이 생성되는 간단한 `Index` 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="3a442-217">유명한 척 노리스이기 때문에 이 페이지가 전 세계적으로 널리 알려질 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="3a442-218">이는 Azure CDN으로 동적인 요소가 가미된 콘텐츠를 제공하는 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="3a442-219">위의 단계에 따라 이 컨트롤러 작업을 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="3a442-220">*\Controllers* 폴더에서 *MemeGeneratorController.cs*라는 새로운 .cs 파일을 만들고 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="3a442-221">또한 강조 표시된 부분은 사용 중인 CDN 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="3a442-222">기본 `Index()` 작업을 마우스 오른쪽 단추로 클릭하고 **뷰 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="3a442-223">아래의 설정을 적용하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="3a442-224">새로운 *Views\MemeGenerator\Index.cshtml* 파일을 열고 내용을 다음과 같이 최상급을 제출하는 간단한 HTML로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="3a442-225">클라우드 서비스를 다시 게시하고 브라우저에서 **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="3a442-226">양식 값을 `/MemeGenerator/Index`로 제출할 경우 `Index_Post` 동작 메서드가 각각의 입력 식별자와 함께 `Show` 동작 메서드에 대한 링크를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="3a442-227">링크를 클릭하면 다음 코드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="3a442-228">로컬 디버거가 연결되어 있다면 로컬로 리디렉션되면서 정규 디버그 환경이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="3a442-229">클라우드 서비스에서 실행 중인 경우에는 다음으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="3a442-230">이는 CDN 끝점의 다음 원본 URL과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="3a442-231">그런 다음 `Generate` 메서드의 `OutputCacheAttribute` 특성을 사용하여 작업 결과를 캐시할 방법을 지정할 수 있으며, 이렇게 지정한 설정은 Azure CDN에서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="3a442-232">다음 코드는 캐시 만료를 1시간(3,600초)으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="3a442-233">마찬가지로 클라우드 서비스에서 모든 컨트롤러 작업의 콘텐츠를 Azure CDN을 통해 원하는 캐싱 옵션으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="3a442-234">다음 섹션에서는 Azure CDN을 통해 묶이고 축소된 스크립트 및 CSS를 제공하는 방법을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="3a442-235">ASP.NET 묶음 및 축소를 Azure CDN과 통합</span><span class="sxs-lookup"><span data-stu-id="3a442-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="3a442-236">스크립트 및 CSS 스타일시트는 드물게 변경되며 Azure CDN 캐시의 주요 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="3a442-237">Azure CDN을 통해 전체 웹 역할을 제공하는 것은 묶음 및 축소를 Azure CDN에 통합하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="3a442-238">그러나 이러한 방법을 원하지 않을 수도 있으므로 다음과 같이 ASP.NET 묶음 및 축소의 바람직한 개발자 환경을 유지하면서 동시에 통합을 수행하는 방법을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="3a442-239">탁월한 디버그 모드 환경</span><span class="sxs-lookup"><span data-stu-id="3a442-239">Great debug mode experience</span></span>
* <span data-ttu-id="3a442-240">간소화된 배포</span><span class="sxs-lookup"><span data-stu-id="3a442-240">Streamlined deployment</span></span>
* <span data-ttu-id="3a442-241">스크립트/CSS 버전 업그레이드를 위한 클라이언트 즉시 업데이트</span><span class="sxs-lookup"><span data-stu-id="3a442-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="3a442-242">CDN 끝점의 오류에 대비한 대체 메커니즘</span><span class="sxs-lookup"><span data-stu-id="3a442-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="3a442-243">코드 수정의 최소화</span><span class="sxs-lookup"><span data-stu-id="3a442-243">Minimize code modification</span></span>

<span data-ttu-id="3a442-244">[Azure CDN 끝점을 Azure 웹 사이트와 통합하여 Azure CDN에서 웹 페이지에 정적 콘텐츠 제공](#deploy)에서 만든 **WebRole1** 프로젝트에서 *App_Start\BundleConfig.cs*를 열고 `bundles.Add()` 메서드 호출을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="3a442-245">첫 번째 `bundles.Add()` 문은 가상 디렉터리 `~/bundles/jquery`에 스크립트 번들을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="3a442-246">그런 다음 *Views\Shared\_Layout.cshtml* 파일을 열고 스크립트 번들 태그가 어떻게 렌더링되는지 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="3a442-247">다음과 같은 Razor 코드 줄이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="3a442-248">이 Razor 코드가 Azure 웹 역할에서 실행되는 경우 다음과 유사한 스크립트 번들의 `<script>` 태그를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="3a442-249">그러나 `F5`키를 눌러 Visual Studio에서 코드가 실행되면 다음과 같이 번들의 각 스크립트 파일을 개별적으로 렌더링합니다(위의 경우에는 하나의 스크립트 파일만 번들에 있음).</span><span class="sxs-lookup"><span data-stu-id="3a442-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="3a442-250">그러면 프로덕션 환경에서 클라이언트의 동시 연결은 줄이고(묶음) 파일 다운로드 성능은 향상시키는(축소) 동시에 개발 환경에서 JavaScript 코드를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="3a442-251">이 방법은 Azure CDN 통합을 유지하는 훌륭한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="3a442-252">또한 렌더링된 번들에는 이미 자동으로 생성된 버전 문자열이 포함되어 있기 때문에 NuGet을 통해 jQuery 버전을 업데이트할 때마다 가능한 한 빠르게 클라이언트 쪽에서 업데이트할 수 있도록 해당 기능을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="3a442-253">ASP.NET 묶음 및 축소를 CDN 끝점과 통합하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="3a442-254">*App_Start\BundleConfig.cs* 파일로 돌아가서 CDN 주소를 지정한 다른 [Bundle 생성자](http://msdn.microsoft.com/library/jj646464.aspx)를 사용하도록 `bundles.Add()` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="3a442-255">이를 수행하려면 `RegisterBundles` 메서드 정의를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="3a442-256">`<yourCDNName>` 을 사용 중인 Azure CDN 이름으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="3a442-257">쉽게 말하면 `bundles.UseCdn = true` 를 설정하고 있으며 신중하게 만든 CDN URL을 각 번들에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="3a442-258">예를 들어 코드의 첫 번째 생성자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="3a442-259">이 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="3a442-260">이 생성자에 따라 ASP.NET 묶음 및 축소가 로컬에서 디버깅될 때 개별 스크립트 파일을 렌더링하지만 지정된 CDN 주소를 사용하여 해당 스크립트에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="3a442-261">그러나 신중하게 만든 이 CDN URL의 두 가지 중요한 특징에서 다음을 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="3a442-262">이 CDN URL의 원본은 `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`이며, 실제로는 클라우드 서비스에서 스크립트 번들의 가상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="3a442-263">CDN 생성자를 사용하고 있으므로 번들의 CDN 스크립트 태그가 더 이상 렌더링된 URL에 자동으로 생성된 버전 문자열을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="3a442-264">스크립트 번들이 Azure CDN에서 캐시 누락을 강제하도록 수정될 때마다 고유한 버전 문자열을 수동으로 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="3a442-265">동시에 고유한 버전 문자열은 전 배포 수명 동안 일정하게 유지되어 번들이 배포된 이후 Azure CDN에서 캐시 적중을 극대화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="3a442-266">쿼리 문자열 v=<W.X.Y.Z>는 웹 역할 프로젝트의 *Properties\AssemblyInfo.cs*에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="3a442-267">Azure에 게시할 때마다 어셈블리 버전 증분 등의 기능을 포함하는 배포 워크플로를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="3a442-268">또는 간단히 와일드카드 문자(*)를 사용하여 빌드할 때마다 버전 문자열을 자동으로 증분하도록 프로젝트의 *Properties\AssemblyInfo.cs* 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="3a442-269">예:</span><span class="sxs-lookup"><span data-stu-id="3a442-269">For example:</span></span>
     
        <span data-ttu-id="3a442-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="3a442-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="3a442-271">배포 수명 동안의 고유한 문자열 생성을 간소화하는 다른 전략도 효과가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="3a442-272">클라우드 서비스를 다시 게시하고 홈페이지에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="3a442-273">페이지의 HTML 코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-273">View the HTML code for the page.</span></span> <span data-ttu-id="3a442-274">변경 내용을 클라우드 서비스에 다시 게시할 때마다 고유한 버전 문자열과 함께 렌더링된 CDN URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="3a442-275">예:</span><span class="sxs-lookup"><span data-stu-id="3a442-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="3a442-276">Visual Studio로 돌아가 `F5`키를 눌러 Visual Studio에서 클라우드 서비스를 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="3a442-277">페이지의 HTML 코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-277">View the HTML code for the page.</span></span> <span data-ttu-id="3a442-278">개별적으로 렌더링된 각 스크립트 파일을 살펴볼 수 있으므로 Visual Studio의 일관된 디버그 환경을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="3a442-279">CDN URL의 대체 메커니즘</span><span class="sxs-lookup"><span data-stu-id="3a442-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="3a442-280">어떤 이유로 Azure CDN 끝점에 문제가 발생한 경우 JavaScript 또는 부트스트랩을 로드하는 대체 옵션으로 원본 웹 서버에 액세스할 수 있을 정도로 지능적인 웹 페이지를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="3a442-281">CDN을 사용할 수 없어서 웹 사이트의 이미지가 손실되는 심각한 상황이 올 수도 있지만 좀 더 심각한 경우는 스크립트 및 스타일시트에서 제공하는 중요한 페이지 기능을 사용하지 못하는 게 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="3a442-282">[Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) 클래스에는 CDN 오류에 대비해 대체 메커니즘을 구성할 수 있도록 [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx)이라는 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="3a442-283">이 속성을 사용하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3a442-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="3a442-284">웹 역할 프로젝트에서 각 [Bundle 생성자](http://msdn.microsoft.com/library/jj646464.aspx)의 CDN URL을 추가한 *App_Start\BundleConfig.cs* 파일을 열고 다음과 같이 강조 표시된 내용을 변경하여 기본 번들에 대체 메커니즘을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="3a442-285">`CdnFallbackExpression` 이 null이 아니면 스크립트가 HTML에 삽입되어 번들이 제대로 로드되는지 테스트하고 제대로 로드되지 않는 경우 원본 웹 서버에서 직접 번들에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="3a442-286">이 속성은 각각의 CDN 번들이 제대로 로드되는지 테스트하는 JavaScript 식으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="3a442-287">각 번들을 테스트하는 데 필요한 식은 콘텐츠에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="3a442-288">위 기본 번들의 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="3a442-289">`window.jquery` 는 jquery-{version}.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="3a442-290">`$.validator` 는 jquery.validate.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="3a442-291">`window.Modernizr` 는 modernizer-{version}.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="3a442-292">`$.fn.modal` 은 bootstrap.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="3a442-293">여기서는 `~/Cointent/css` 번들에 대해 CdnFallbackExpression을 설정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="3a442-294">그 이유는 현재 필요한 `<link>` 태그 대신 대체 CSS의 `<script>` 태그를 삽입하는 [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104)가 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="3a442-295">그러나 [Ember 컨설팅 그룹](https://github.com/EmberConsultingGroup)에서 제공한 우수한 [스타일 번들 대체](https://github.com/EmberConsultingGroup/StyleBundleFallback)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="3a442-296">이 CSS 해결 방법을 사용하려면 *StyleBundleExtensions.cs*라고 하는 웹 역할 프로젝트의 *App_Start* 폴더에서 새로운 .cs 파일을 만들어 해당 내용을 [GitHub의 코드](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="3a442-297">*App_Start\StyleFundleExtensions.cs* 파일에서 웹 역할 이름(예: **WebRole1**)에 대한 네임스페이스의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="3a442-298">`App_Start\BundleConfig.cs` 파일로 돌아가 마지막 `bundles.Add` 문을 다음과 같은 강조 표시된 코드로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="3a442-299">이 새로운 확장 메서드는 동일한 개념을 사용하여 CSS 번들에 정의된 일치하는 클래스 이름, 규칙 이름 및 규칙 값에 대한 DOM을 확인하고 일치 항목을 찾지 못할 경우 원본 웹 서버로 대체하는 스크립트를 HTML에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="3a442-300">클라우드 서비스를 다시 게시하고 홈페이지에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="3a442-301">페이지의 HTML 코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-301">View the HTML code for the page.</span></span> <span data-ttu-id="3a442-302">다음과 비슷한 삽입 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-302">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="3a442-303">CSS 번들의 삽입 스크립트에서 다음 줄에 여전히 `CdnFallbackExpression` 속성의 나머지 잘못된 부분이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="3a442-304">그러나 || 식의 첫 부분이 항상 true를 반환하므로(바로 위의 줄에서) document.write() 함수가 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a442-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="3a442-305">추가 정보</span><span class="sxs-lookup"><span data-stu-id="3a442-305">More Information</span></span>
* [<span data-ttu-id="3a442-306">Azure CDN(콘텐츠 배달 네트워크) 개요</span><span class="sxs-lookup"><span data-stu-id="3a442-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="3a442-307">Azure CDN 사용</span><span class="sxs-lookup"><span data-stu-id="3a442-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="3a442-308">ASP.NET 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="3a442-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
