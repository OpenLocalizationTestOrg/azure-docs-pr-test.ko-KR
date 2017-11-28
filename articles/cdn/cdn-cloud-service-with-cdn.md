---
title: "Azure 클라우드 서비스와 Azure CDN aaaIntegrate | Microsoft Docs"
description: "어떻게 toodeploy 클라우드 서비스 역할 하는 콘텐츠를 통합된 Azure CDN 끝점에 알아봅니다"
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="9e1e0-103"><a name="intro"></a> Azure CDN과 클라우드 서비스 통합</span><span class="sxs-lookup"><span data-stu-id="9e1e0-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="9e1e0-104">클라우드 서비스는 hello 클라우드 서비스의 위치에서 모든 콘텐츠를 처리 하는 Azure CDN와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="9e1e0-105">이 접근 방식에서는 장점 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="9e1e0-106">클라우드 서비스 프로젝트 디렉터리의 이미지, 스크립트 및 스타일시트를 쉽게 배포 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="9e1e0-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="9e1e0-107">클라우드 서비스, jQuery 또는 부트스트랩 버전 등의 hello NuGet 패키지를 쉽게 업그레이드합니다</span><span class="sxs-lookup"><span data-stu-id="9e1e0-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="9e1e0-108">웹 응용 프로그램을 관리 및 CDN served 콘텐츠 hello에서 모두 동일 Visual Studio 인터페이스</span><span class="sxs-lookup"><span data-stu-id="9e1e0-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="9e1e0-109">웹 응용 프로그램 및 CDN 제공 콘텐츠에 대한 통합 배포 워크플로</span><span class="sxs-lookup"><span data-stu-id="9e1e0-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="9e1e0-110">ASP.NET 묶음 및 축소를 Azure CDN과 통합</span><span class="sxs-lookup"><span data-stu-id="9e1e0-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9e1e0-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="9e1e0-111">What you will learn</span></span>
<span data-ttu-id="9e1e0-112">이 자습서에서는 다음 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="9e1e0-113">Azure CDN 끝점을 클라우드 서비스와 통합하여 Azure CDN에서 웹 페이지의 정적 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="9e1e0-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="9e1e0-114">클라우드 서비스의 정적 콘텐츠에 대한 캐시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="9e1e0-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="9e1e0-115">Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="9e1e0-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="9e1e0-116">Serve 번들로 제공 하 고 Visual Studio에서 디버깅이 hello 스크립트를 유지 하면서 Azure CDN을 통해 콘텐츠를 축소</span><span class="sxs-lookup"><span data-stu-id="9e1e0-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="9e1e0-117">Azure CDN이 오프라인인 경우 스크립트 및 CSS 대체 구성</span><span class="sxs-lookup"><span data-stu-id="9e1e0-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="9e1e0-118">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="9e1e0-118">What you will build</span></span>
<span data-ttu-id="9e1e0-119">Hello 기본 ASP.NET MVC 템플릿에서 사용 하 여 클라우드 서비스 웹 역할을 배포 하, 이미지, 컨트롤러 작업 결과 및 hello 기본 JavaScript 및 CSS 파일을 같은 통합된 된 Azure CDN에서 코드 tooserve 콘텐츠를 추가 하 고 tooconfigure hello 코드를 작성할 수도 합니다. 해당 hello CDN hello 이벤트에서 제공 하는 번들에 대 한 대체 (fallback) 메커니즘은 오프 라인 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="9e1e0-120">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="9e1e0-120">What you will need</span></span>
<span data-ttu-id="9e1e0-121">이 자습서에는 다음 필수 구성 요소는 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="9e1e0-122">활성 [Microsoft Azure 계정](/account/)</span><span class="sxs-lookup"><span data-stu-id="9e1e0-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="9e1e0-123">[Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="9e1e0-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="9e1e0-124">이 자습서는 Azure 계정 toocomplete 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="9e1e0-125">할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/) -크레딧을 얻게 유료 Azure 서비스 아웃 tootry 사용할 수 있으며 사용 후에 최대 hello 계정 등에 사용 하 여 웹 사이트와 같은 Azure 서비스를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="9e1e0-126">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음 - MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="9e1e0-127">클라우드 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="9e1e0-127">Deploy a cloud service</span></span>
<span data-ttu-id="9e1e0-128">이 섹션에서는 hello 기본 Visual Studio 2015 tooa 클라우드 서비스 웹 역할에 ASP.NET MVC 응용 프로그램 템플릿을 배포 하 고 새 CDN 끝점에 부합 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="9e1e0-129">아래 hello 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="9e1e0-130">Visual Studio 2015에서 새 Azure 클라우드 서비스는 hello 메뉴 모음에서 너무 이동 하 여 만들**파일 > 새로 만들기 > 프로젝트 > 클라우드 > Azure 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="9e1e0-131">해당 서비스의 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="9e1e0-132">선택 **ASP.NET 웹 역할** hello 클릭  **>**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="9e1e0-133">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="9e1e0-134">**MVC**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="9e1e0-135">지금이 웹 역할 tooan Azure 클라우드 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="9e1e0-136">Hello 클라우드 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="9e1e0-137">아직 Microsoft Azure에 등록 하지 않은 경우 클릭 hello **계정 추가...**  드롭다운을 클릭 하 고 hello **계정 추가** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="9e1e0-138">Hello 로그인 페이지에서 hello tooactivate Azure 계정을 사용 하는 Microsoft 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="9e1e0-139">로그인했으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="9e1e0-140">Visual Studio에서는 클라우드 서비스 또는 저장소 계정이 생성되지 않았다고 가정하고 두 계정의 생성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="9e1e0-141">Hello에 **클라우드 서비스 만들기 및 계정** 대화 상자, 형식 hello 원하는 서비스 이름과 선택 hello 원하는 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="9e1e0-142">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="9e1e0-143">Hello에서 게시 설정 페이지, hello 구성 확인 및 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="9e1e0-144">클라우드 서비스에 대 한 hello 게시 프로세스에 오랜 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="9e1e0-145">모든 역할 옵션에 대 한 웹 배포 사용 hello 빠른 (하지만 임시) 업데이트 tooyour 웹 역할을 제공 하 여 속도가 훨씬 빨라집니다 클라우드 서비스를 디버깅 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="9e1e0-146">이 옵션에 대 한 자세한 내용은 참조 하십시오. [hello Azure Tools를 사용 하 여 클라우드 서비스 게시](http://msdn.microsoft.com/library/ff683672.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="9e1e0-147">Hello 때 **Microsoft Azure 활동 로그** 게시 상태 임을 보여주고 **완료**,이 클라우드 서비스와 통합 된 CDN 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="9e1e0-148">게시 후 배포 된 hello 클라우드 서비스 오류 화면 표시 하는 경우 될 hello 클라우드 서비스가 배포 되었으며 사용 중이기 때문에 [.NET 4.5.2 포함 하지 않는 운영 체제를 게스트](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="9e1e0-149">[시작 작업으로 .NET 4.5.2를 배포](../cloud-services/cloud-services-dotnet-install-dotnet.md)하여 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="9e1e0-150">새 CDN 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="9e1e0-150">Create a new CDN profile</span></span>
<span data-ttu-id="9e1e0-151">CDN 프로필은 CDN 끝점의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="9e1e0-152">각 프로필에는 CDN 끝점이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="9e1e0-153">여러 프로필 tooorganize toouse를 지정할 수 있습니다 인터넷 도메인, 웹 응용 프로그램 또는 기타 일부 조건에 의해 CDN 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="9e1e0-154">이 자습서에 대 한 toouse 되도록 CDN 프로필을 이미 보유 하는 경우 너무 진행[새 CDN 끝점 만들기](#create-a-new-cdn-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="9e1e0-155">새 CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="9e1e0-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="9e1e0-156">**저장소 계정에 대 한 새 CDN 끝점 toocreate**</span><span class="sxs-lookup"><span data-stu-id="9e1e0-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="9e1e0-157">Hello에 [Azure 관리 포털](https://portal.azure.com), tooyour CDN 프로필을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="9e1e0-158">수 있는 고정 toohello 대시보드 hello 이전 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="9e1e0-159">경우 not, 있습니다 찾을 수 있습니다 것을 클릭 하 여 **찾아보기**, 다음 **CDN 프로필**, 인증서 및 hello 프로필 클릭 하면 tooadd를 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="9e1e0-160">CDN 프로필 블레이드 hello 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-160">hello CDN profile blade appears.</span></span>
   
    ![CDN 프로필][cdn-profile-settings]
2. <span data-ttu-id="9e1e0-162">Hello 클릭 **끝점 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-162">Click hello **Add Endpoint** button.</span></span>
   
    ![끝점 추가 단추][cdn-new-endpoint-button]
   
    <span data-ttu-id="9e1e0-164">hello **끝점 추가** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![끝점 추가 블레이드][cdn-add-endpoint]
3. <span data-ttu-id="9e1e0-166">이 CDN 끝점에 대한 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="9e1e0-167">이 이름은 hello 도메인에서 캐시 된 리소스 사용된 tooaccess 됩니다 `<EndpointName>.azureedge.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="9e1e0-168">Hello에 **원본 형식을** 드롭다운 *클라우드 서비스*합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="9e1e0-169">Hello에 **원본 호스트 이름을** 드롭다운을 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="9e1e0-170">에 대 한 hello 기본값 그대로 두고 **원래 경로**, **원본 호스트 헤더**, 및 **프로토콜/원본 포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="9e1e0-171">하나 이상의 프로토콜(HTTP 또는 HTTPS)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="9e1e0-172">Hello 클릭 **추가** 단추 toocreate hello 새 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="9e1e0-173">Hello 끝점을 만들 되 면 hello 프로필에 대 한 끝점의 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="9e1e0-174">hello 목록 보기 hello URL toouse tooaccess 캐시 hello 원본 도메인 뿐만 아니라 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![CDN 끝점][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="9e1e0-176">hello 끝점 즉시 사용할 수 있는 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="9e1e0-177">Hello CDN 네트워크를 통해 등록 toopropagate hello에 대 일 분까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="9e1e0-178">Hello 콘텐츠 hello CDN 통해 사용 가능할 때까지 사용자가 즉시 toouse hello CDN 도메인 이름을 시도 상태 코드 404을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="9e1e0-179">테스트 hello CDN 끝점</span><span class="sxs-lookup"><span data-stu-id="9e1e0-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="9e1e0-180">게시 상태 hello 다음과 같은 경우 **Completed**브라우저 창을 열고 너무 이동**http://<cdnName>*.azureedge.net/Content/bootstrap.css** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="9e1e0-181">이 자습서 설정에서 이 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="9e1e0-182">해당 하는 hello CDN 끝점에서 원본 URL을 다음 toohello:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="9e1e0-183">너무 이동할 때**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, 브라우저에 따라 됩니다 증명된 toodownload 또는 열기 hello bootstrap.css입니다 게시 된 웹 앱에서 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="9e1e0-184">마찬가지로 CDN 끝점에서 **http://*&lt;서비스 이름>*.cloudapp.net/**의 공개적으로 액세스 가능한 URL에 바로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="9e1e0-185">예:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-185">For example:</span></span>

* <span data-ttu-id="9e1e0-186">Hello /Script 경로에서.js 파일</span><span class="sxs-lookup"><span data-stu-id="9e1e0-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="9e1e0-187">/Content hello에서 모든 콘텐츠 파일 경로</span><span class="sxs-lookup"><span data-stu-id="9e1e0-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="9e1e0-188">모든 controller/action</span><span class="sxs-lookup"><span data-stu-id="9e1e0-188">Any controller/action</span></span>
* <span data-ttu-id="9e1e0-189">쿼리 문자열 hello를 모든 URL 쿼리 문자열이 포함 된 CDN 끝점에서 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9e1e0-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="9e1e0-190">실제로 구성 이상 hello,으로 호스트할 수 있습니다 hello 전체 클라우드 서비스에서  **http://*&lt;cdnName >*.azureedge.net/**합니다. 너무를 탐색 하는 경우**http://camservice.azureedge.net/ * * hello 작업 결과에서 받는 Home/Index입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="9e1e0-191">그러나이 의미는 아닙니다 좋습니다 tooserve Azure CDN을 통해 전체 클라우드 서비스는 항상 임을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="9e1e0-192">정적 배달 최적화 CDN 않습니다 하지 반드시 속도를 높이기 toobe 캐시는 사용 되지 않는 되거나 hello CDN 매우 자주 새 버전의 hello 자산 hello 원본 서버에서 끌어오도록 해야 하므로 자주 업데이트 되는 동적 자산 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="9e1e0-193">이 시나리오에서는 사용할 수 있습니다 [동적 사이트 가속](cdn-dynamic-site-acceleration.md) 다양 한 기술을 toospeed 캐시할 동적 자산 배달을 사용 하 여 CDN 끝점에서 (DSA) 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="9e1e0-194">정적 및 동적 콘텐츠가 혼합 된 사이트가 있는 경우 선택할 수 있습니다 tooserve CDN에서 정적 콘텐츠 (예: 일반 웹 배달의 경우)는 정적 최적화 형식과 및 tooserve 동적 콘텐츠 hello 원본 서버에서 직접 또는 CDN을 통해 DSA 최적화 상황별으로 설정 되어 있는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="9e1e0-195">toothat 끝 tooaccess 개별 콘텐츠 hello CDN 끝점에서 파일을 방법 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="9e1e0-196">Tooserve에 특정 CDN 끝점을 통해 특정 컨트롤러 동작을 서비스 방법을 컨트롤러 작업을 통해 Azure CDN에서 콘텐츠 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="9e1e0-197">hello는 대체 항목은 toodetermine tooserve Azure CDN에서 클라우드 서비스에서 경우-기준 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="9e1e0-198">toothat 끝 tooaccess 개별 콘텐츠 hello CDN 끝점에서 파일을 방법 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="9e1e0-199">살펴본 다음 방법을 tooserve를 통해 특정 컨트롤러 액션 hello에 CDN 끝점 [Azure CDN을 통해 컨트롤러 작업에서 콘텐츠를 제공](#controller)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="9e1e0-200">클라우드 서비스의 정적 파일에 대한 캐싱 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="9e1e0-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="9e1e0-201">클라우드 서비스에서 Azure CDN 통합을 원하는 정적 콘텐츠 toobe hello CDN 끝점에 캐시를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="9e1e0-202">toodo이,이 오픈 *Web.config* 웹 역할에서 프로젝트 (예: WebRole1) 하 고 추가 `<staticContent>` 요소 너무`<system.webServer>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="9e1e0-203">다음 XML hello 3 일에서 hello 캐시 tooexpire를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="9e1e0-204">이렇게 하면 클라우드 서비스의 모든 정적 파일은 hello CDN 캐시에서 동일한 규칙을 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="9e1e0-205">캐싱 설정을 더 세밀하게 제어하려면 *Web.config* 파일을 폴더에 추가하고 이 파일에 해당 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="9e1e0-206">예를 들어 추가 *Web.config* toohello 파일 *\Content* 폴더 및 바꾸기 hello 다음과 같은 XML로 콘텐츠를 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="9e1e0-207">이 설정을 사용 하면 hello에서 모든 정적 파일 *\Content* 폴더 toobe 15 일 동안 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="9e1e0-208">방법에 대 한 자세한 내용은 tooconfigure hello `<clientCache>` 요소 참조 [클라이언트 캐시 &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="9e1e0-209">[Azure CDN을 통해 컨트롤러 작업에서 콘텐츠를 제공](#controller), 또한 살펴본 다음 hello CDN 캐시에서에서 컨트롤러 작업 결과 대 한 캐시 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="9e1e0-210">Azure CDN을 통해 컨트롤러 작업의 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="9e1e0-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="9e1e0-211">Azure CDN을 클라우드 서비스 웹 역할을 통합 때는 hello Azure CDN을 통해 컨트롤러 작업에서 상대적으로 쉬운 tooserve 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="9e1e0-212">Azure CDN (위 예제)을 통해 직접 서비스 클라우드 경우를 제외 [Maarten Balliauw](https://twitter.com/maartenballiauw) 표시 하는 toodo 재미 있는 MemeGenerator 컨트롤러에 [hello Azure CDN을 사용 하 여 hello 웹에 대 한 대기 시간 ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="9e1e0-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="9e1e0-213">여기서 그 방법을 간단히 재현해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="9e1e0-214">클라우드 서비스에서 젊은 Chuck Norris 이미지에 따라 toogenerate memes 한다고 가정 (하 여 사진 [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="9e1e0-215">간단한 있는 `Index` toohello 작업을 게시 한 후 다음 hello 고객 toospecify hello 최상급 hello 이미지에서 허용 하는 작업 hello 캐릭터가 문화적 요소로 등장 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="9e1e0-216">Chuck Norris 이므로, 예상 페이지 toobecome이 매우 인기 있는 전역적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="9e1e0-217">이는 Azure CDN으로 동적인 요소가 가미된 콘텐츠를 제공하는 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="9e1e0-218">이 컨트롤러 동작 toosetup 위의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="9e1e0-219">Hello에 *\Controllers* 폴더를 새.cs 파일을 만들 *MemeGeneratorController.cs* 바꾸기 hello hello를 사용 하 여 콘텐츠 코드를 다음 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="9e1e0-220">CDN 이름의 있는지 tooreplace hello 강조 표시 된 부분을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. <span data-ttu-id="9e1e0-221">Hello 기본 마우스 오른쪽 단추로 클릭 `Index()` 작업을 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="9e1e0-222">아래 hello 설정을 적용 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="9e1e0-223">새 열기 hello *Views\MemeGenerator\Index.cshtml* hello 콘텐츠 hello 최상급 전송 하기 위한 간단한 HTML 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="9e1e0-224">Hello 클라우드 서비스를 다시 게시 하 고 탐색 너무**http://*&lt;serviceName >*브라우저에서.cloudapp.net/MemeGenerator/Index** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="9e1e0-225">너무 hello 폼 값을 제출할 때`/MemeGenerator/Index`, hello `Index_Post` 작업 메서드가 링크 toohello 반환 `Show` hello 각각 입력된 식별자를 가진 동작 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="9e1e0-226">Hello 링크를 클릭 하면 hello 코드 다음에 도달 하면:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="9e1e0-227">로컬 디버거를 연결 하면 뷰어에서 hello 일반 디버그 경험이 로컬 리디렉션 얻이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="9e1e0-228">Hello 클라우드 서비스에서 실행 되는 경우를 리디렉션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="9e1e0-229">CDN 끝점에 대 한 원본 URL을 다음 toohello 해당:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="9e1e0-230">Hello를 사용 하 여 있습니다 `OutputCacheAttribute` hello에 대 한 특성 `Generate` Azure CDN은 유지 하는 메서드 toospecify 어떻게 hello 작업 결과 캐시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="9e1e0-231">아래 hello 코드는 1 시간 (3, 600 초)의 캐시 만료를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="9e1e0-232">마찬가지로, 통해 hello 원하는 캐싱 옵션을 사용 하 여 Azure CDN에서 클라우드 서비스에서 컨트롤러 작업에서 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="9e1e0-233">Hello 다음 섹션에서 하겠습니다 tooserve hello 번들로 제공 하 고 스크립트와 Azure CDN을 통해 CSS 축소 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="9e1e0-234">ASP.NET 묶음 및 축소를 Azure CDN과 통합</span><span class="sxs-lookup"><span data-stu-id="9e1e0-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="9e1e0-235">스크립트 및 CSS 스타일 시트 자주 변경 되며 hello Azure CDN에 캐시에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="9e1e0-236">Azure CDN을 통해 제공 hello 전체 웹 역할은 hello 가장 쉬운 방법은 toointegrate 묶음 및 축소 Azure CDN을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="9e1e0-237">그러나 하지 못하게 하려는 toodo이, 대로 살펴본 다음 방법을 toodo hello를 유지 하면서이 필요한 ASP.NET 묶음 및 축소의 develper 경험와 같은:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="9e1e0-238">탁월한 디버그 모드 환경</span><span class="sxs-lookup"><span data-stu-id="9e1e0-238">Great debug mode experience</span></span>
* <span data-ttu-id="9e1e0-239">간소화된 배포</span><span class="sxs-lookup"><span data-stu-id="9e1e0-239">Streamlined deployment</span></span>
* <span data-ttu-id="9e1e0-240">스크립트/CSS 버전 업그레이드에 대 한 즉시 업데이트 tooclients</span><span class="sxs-lookup"><span data-stu-id="9e1e0-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="9e1e0-241">CDN 끝점의 오류에 대비한 대체 메커니즘</span><span class="sxs-lookup"><span data-stu-id="9e1e0-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="9e1e0-242">코드 수정의 최소화</span><span class="sxs-lookup"><span data-stu-id="9e1e0-242">Minimize code modification</span></span>

<span data-ttu-id="9e1e0-243">Hello에 **WebRole1** 에서 만든 프로젝트 [Azure CDN에서 정적 콘텐츠 웹 페이지에서 서비스 및 Azure 웹 사이트와 Azure CDN 끝점을 통합](#deploy)개방형 *App_Start\ BundleConfig.cs* hello 살펴보세요 및 `bundles.Add()` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="9e1e0-244">먼저 hello `bundles.Add()` hello 가상 디렉터리에 있는 스크립트 번들을 추가 하는 문을 `~/bundles/jquery`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="9e1e0-245">그런 다음을 열고 *Views\Shared\_Layout.cshtml* toosee hello 스크립트 번들 태그를 렌더링 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="9e1e0-246">다음 Razor 코드의 줄 수 toofind hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="9e1e0-247">렌더링이 Razor 코드가 hello Azure 웹 역할에서 실행 되는 경우는 `<script>` hello에 대 한 태그 스크립트 번들 비슷한 toohello 다음:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="9e1e0-248">그러나이 실행 될 때 Visual Studio에서를 입력 하 여 `F5`를 개별적으로 hello 번들에서 각 스크립트 파일을 렌더링 합니다 (위의 hello 경우에만 하나의 스크립트 파일은 hello 번들에):</span><span class="sxs-lookup"><span data-stu-id="9e1e0-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="9e1e0-249">이렇게 하면 toodebug hello JavaScript 코드 개발 환경에서 프로덕션 환경에서 동시 클라이언트 연결 (번들)을 절감 하 고 파일을 향상 다운로드 성능을 (축소) 하는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="9e1e0-250">Azure CDN 통합 훌륭한 기능 toopreserve 이며</span><span class="sxs-lookup"><span data-stu-id="9e1e0-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="9e1e0-251">또한 렌더링 hello 번들 자동으로 생성 된 버전 문자열에 이미 포함 되어 있으므로 원하는 기능 NuGet 통해 jQuery 버전을 업데이트할 때마다 하므로 hello tooreplicate hello 클라이언트 쪽에서 업데이트할 수 있으므로 즉시 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="9e1e0-252">Toointegration ASP.NET 묶음 및 축소 CDN 끝점과 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="9e1e0-253">다시 *App_Start\BundleConfig.cs*, hello 수정 `bundles.Add()` 메서드 toouse 다른 [번들 생성자](http://msdn.microsoft.com/library/jj646464.aspx), CDN 주소를 지정 하는 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="9e1e0-254">toodo이, replace hello `RegisterBundles` 코드 다음 hello로 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="9e1e0-255">수 있는지 tooreplace `<yourCDNName>` Azure CDN의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="9e1e0-256">설정 하는 일반 단어에서 `bundles.UseCdn = true` 신중 하 게 만든된 CDN URL tooeach 번들을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="9e1e0-257">예를 들어 hello 첫 번째 생성자 hello 코드에서:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="9e1e0-258">hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="9e1e0-259">이 생성자 지시 ASP.NET 묶음 및 축소 toorender 개별 스크립트 파일 디버깅할 때 로컬에 있지만 사용 하 여 hello CDN 주소 tooaccess hello 스크립트에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="9e1e0-260">그러나 신중하게 만든 이 CDN URL의 두 가지 중요한 특징에서 다음을 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="9e1e0-261">이 CDN URL에 대 한 hello 원본은 `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, 클라우드 서비스에서 hello 스크립트 번들의 가상 디렉터리 hello 실제로 변수인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="9e1e0-262">CDN 생성자를 사용 하므로 hello hello 번들에 대 한 CDN 스크립트 태그는 더 이상 URL 렌더링 hello에 자동으로 생성 하는 hello 버전 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="9e1e0-263">Hello 스크립트 번들은 Azure CDN에 캐시를 누락 하는 수정 된 tooforce 때마다 고유한 버전 문자열을 수동으로 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="9e1e0-264">At hello 동일 time, hello 번들 배포 된 후이 고유한 버전 문자열 hello 배포 toomaximize 캐시 적중 횟수 Azure CDN에서의 hello 수명 통해 일정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="9e1e0-265">쿼리 문자열 v hello < W.X.Y.Z > 끌어오는 소스에서 = *Properties\AssemblyInfo.cs* 웹 역할 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="9e1e0-266">TooAzure 게시할 때마다 hello 어셈블리 버전을 증가 포함 하는 배포 워크플로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="9e1e0-267">방금 수정할 수 있습니다 또는 *Properties\AssemblyInfo.cs* 프로젝트 tooautomatically 증가 hello 버전 문자열에서을 빌드할 때마다 사용 하 여 hello 와일드 카드 문자 ' *'입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="9e1e0-268">예:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-268">For example:</span></span>
     
        <span data-ttu-id="9e1e0-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="9e1e0-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="9e1e0-270">여기에 배포의 hello 수명에 대 한 고유 문자열을 생성 전략 toostreamline 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="9e1e0-271">Hello 클라우드 서비스 및 액세스 hello 홈 페이지를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="9e1e0-272">보기 hello hello 페이지에 대 한 HTML 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="9e1e0-273">수 toosee hello CDN URL 변경 tooyour 클라우드 서비스를 다시 게시 될 때마다 고유한 버전 문자열을 사용 하 여 렌더링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="9e1e0-274">예:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="9e1e0-275">Visual Studio에서를 입력 하 여 Visual Studio에서 클라우드 서비스의 hello 디버그 `F5`.,</span><span class="sxs-lookup"><span data-stu-id="9e1e0-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="9e1e0-276">보기 hello hello 페이지에 대 한 HTML 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="9e1e0-277">개별적으로 렌더링된 각 스크립트 파일을 살펴볼 수 있으므로 Visual Studio의 일관된 디버그 환경을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="9e1e0-278">CDN URL의 대체 메커니즘</span><span class="sxs-lookup"><span data-stu-id="9e1e0-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="9e1e0-279">Azure CDN 끝점에 어떤 이유로 든 실패 하면 웹 페이지 toobe 스마트 충분 한 tooaccess 원본 웹 서버 hello JavaScript 또는 부트스트랩 로드 하기 위한 대체 옵션으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="9e1e0-280">것 만큼 심각 toolose 이미지 tooCDN 사용 불가능 하지만 스크립트 및 스타일 시트에서 제공 하는 훨씬 더 심각한 toolose 중요 한 페이지 기능 인해 웹 사이트에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="9e1e0-281">hello [번들](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) 클래스 라는 속성이 포함 [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) 수 있게 해 주는 tooconfigure hello CDN 실패에 대 한 대체 메커니즘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="9e1e0-282">toouse이이 속성을 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="9e1e0-283">웹 역할 프로젝트를 열고 *App_Start\BundleConfig.cs*각 CDN URL을 추가한, [번들 생성자](http://msdn.microsoft.com/library/jj646464.aspx), hello 다음 강조 표시 하 고 tooadd 대체 메커니즘이 toohello 변경 기본 번들:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    <span data-ttu-id="9e1e0-284">때 `CdnFallbackExpression` 은 null이 아닌 스크립트는에 삽입할 HTML hello tootest hello 번들 성공적으로 로드 되 고 있는지 여부를 하 고 그렇지 않은 경우 hello 번들 hello 원본 웹 서버에서 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="9e1e0-285">이 속성은 toobe 집합 tooa JavaScript 식 hello 해당 CDN 번들 제대로 로드 하는지 여부를 테스트 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="9e1e0-286">hello 식 tootest 필요한 각 번들 toohello 내용에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="9e1e0-287">번들 기본 hello에 대 한:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="9e1e0-288">`window.jquery` 는 jquery-{version}.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="9e1e0-289">`$.validator` 는 jquery.validate.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="9e1e0-290">`window.Modernizr` 는 modernizer-{version}.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="9e1e0-291">`$.fn.modal` 은 bootstrap.js에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="9e1e0-292">알 수 있습니다는 설정 하지 않았는데 CdnFallbackExpression hello에 대 한 `~/Cointent/css` 번들입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="9e1e0-293">현재이 때문에 이것이 [System.Web.Optimization의 버그](https://aspnetoptimization.codeplex.com/workitem/104) 삽입 하는 `<script>` hello 대신 대체 CSS에서 예상 하는 hello에 대 한 태그 `<link>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="9e1e0-294">그러나 [Ember 컨설팅 그룹](https://github.com/EmberConsultingGroup)에서 제공한 우수한 [스타일 번들 대체](https://github.com/EmberConsultingGroup/StyleBundleFallback)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="9e1e0-295">CSS에 대 한 toouse hello 해결 웹 역할 프로젝트에 새.cs 파일을 만들 *App_Start* 라는 폴더 *StyleBundleExtensions.cs*, 및 해당 내용을 hello로 바꾸기 [에서 발생 한 코드 GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="9e1e0-296">*App_Start\StyleFundleExtensions.cs*, hello 네임 스페이스 tooyour 웹 역할의 이름을 바꿉니다 (예: **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="9e1e0-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="9e1e0-297">너무 돌아가서`App_Start\BundleConfig.cs` hello를 마지막 수정 `bundles.Add` 문을 강조 표시 된 코드를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="9e1e0-298">이 새 확장 메서드 hello를 사용 하 여 일치 하는 클래스 이름, 규칙 이름 및 hello CSS 번들 및 toofind hello 일치 실패할 경우 폭포 백 toohello 원본 웹 서버에 정의 된 규칙 값 tooinject 스크립트 hello에 대 한 HTML hello toocheck hello DOM에 동일한 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="9e1e0-299">클라우드 서비스를 다시 hello 및 액세스 hello 홈 페이지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="9e1e0-300">보기 hello hello 페이지에 대 한 HTML 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="9e1e0-301">비슷한 toohello 다음 삽입된 스크립트를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-301">You should find injected scripts similar toohello following:</span></span>    
   
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

    <span data-ttu-id="9e1e0-302">Hello CSS 번들에 대 한 삽입 된 스크립트에 여전히 hello에서 잘못 된 나머지 hello 포함 `CdnFallbackExpression` hello 줄에는 속성:</span><span class="sxs-lookup"><span data-stu-id="9e1e0-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="9e1e0-303">하지만 hello의 첫 번째 부분 hello | | 식은 항상 (바로 위에 있는 hello 줄)에서 true를 반환, hello document.write() 함수 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1e0-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="9e1e0-304">추가 정보</span><span class="sxs-lookup"><span data-stu-id="9e1e0-304">More Information</span></span>
* [<span data-ttu-id="9e1e0-305">Hello Azure 콘텐츠 배달 네트워크 (CDN)의 개요</span><span class="sxs-lookup"><span data-stu-id="9e1e0-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="9e1e0-306">Azure CDN 사용</span><span class="sxs-lookup"><span data-stu-id="9e1e0-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="9e1e0-307">ASP.NET 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="9e1e0-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
