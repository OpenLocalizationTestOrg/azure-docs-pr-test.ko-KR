---
title: "Azure에서 Visual Studio Team Services를 사용한 지속적인 업데이트 | Microsoft Docs"
description: "자동으로 빌드되어 Azure 앱 서비스 또는 클라우드 서비스에서 웹앱에 배포되도록 Visual Studio Team Services 팀 프로젝트를 구성하는 방법을 알아봅니다."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="b95fd-103">Visual Studio Team Services를 사용한 지속적인 업데이트</span><span class="sxs-lookup"><span data-stu-id="b95fd-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="b95fd-104">Azure 웹앱 또는 클라우드 서비스에 자동으로 빌드 및 배포하도록 Visual Studio Team Services 팀 프로젝트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="b95fd-105">*온-프레미스* Team Foundation Server를 사용하여 연속 빌드 및 배포 시스템을 설정하는 방법에 대한 자세한 내용은 [Azure 클라우드 서비스의 지속적인 전송](cloud-services-dotnet-continuous-delivery.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="b95fd-106">이 자습서에서는 Visual Studio 2013 및 Azure SDK가 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="b95fd-107">Visual Studio 2013을 아직 설치하지 않은 경우 **www.visualstudio.com** 에서 [무료로 시작하기](http://www.visualstudio.com)링크를 선택하여 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="b95fd-108">Azure SDK의 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=239540)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="b95fd-109">이 자습서를 완료하려면 Visual Studio Team Services 계정이 있어야 합니다. [Visual Studio Team Services 계정은 무료로 개설](http://go.microsoft.com/fwlink/p/?LinkId=512979)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="b95fd-110">Visual Studio Team Services를 사용하여 Azure에 자동으로 빌드 및 배포하도록 클라우드 서비스를 설정하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="b95fd-111">1:팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b95fd-111">1: Create a team project</span></span>
<span data-ttu-id="b95fd-112">[여기](http://go.microsoft.com/fwlink/?LinkId=512980) 에 나와 있는 지침에 따라 팀 프로젝트를 만들고 Visual Studio에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="b95fd-113">이 연습에서는 TFVC(Team Foundation 버전 제어)를 소스 제어 솔루션으로 사용하고 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="b95fd-114">버전 제어를 위해 Git를 사용하려는 경우 [이 연습의 Git 버전](http://go.microsoft.com/fwlink/p/?LinkId=397358)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="b95fd-115">2: 소스 제어에 프로젝트 체크 인</span><span class="sxs-lookup"><span data-stu-id="b95fd-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="b95fd-116">Visual Studio에서 배포할 솔루션을 열거나 새 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="b95fd-117">이 연습의 단계에 따라 웹앱 또는 클라우드 서비스(Azure 응용 프로그램)를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="b95fd-118">새 솔루션을 만들려는 경우 새 Azure 클라우드 서비스 프로젝트 또는 새 ASP.NET MVC 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="b95fd-119">프로젝트의 대상을 .NET Framework 4 또는 4.5로 지정했는지 확인하고, 클라우드 서비스 프로젝트를 만드는 경우 ASP.NET MVC 웹 역할 및 작업자 역할을 추가하고 웹 역할을 위한 인터넷 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="b95fd-120">메시지가 표시되면 **인터넷 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="b95fd-121">웹앱을 만들려는 경우 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 선택한 후 MVC를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="b95fd-122">[Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 만들기](../app-service-web/app-service-web-get-started-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="b95fd-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b95fd-123">Visual Studio Team Services는 현재 Visual Studio 웹 응용 프로그램의 CI 배포만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="b95fd-124">웹 사이트 프로젝트는 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="b95fd-125">솔루션의 상황에 맞는 메뉴를 열고 **소스 제어에 솔루션 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="b95fd-126">기본값을 그대로 사용하거나 변경한 후 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="b95fd-127">프로세스가 완료되면 소스 제어 아이콘이 **솔루션 탐색기**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="b95fd-128">솔루션의 바로 가기 메뉴를 열고 **체크 인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="b95fd-129">**팀 탐색기**의 **보류 중인 변경 내용** 영역에서 체크 인에 대한 설명을 입력하고 **체크 인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="b95fd-130">체크 인할 때 특정 변경 내용을 포함하거나 제외하는 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="b95fd-131">원하는 변경 내용이 제외된 경우 **모두 포함** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="b95fd-132">3: Azure에 프로젝트 연결</span><span class="sxs-lookup"><span data-stu-id="b95fd-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="b95fd-133">일부 소스 코드를 포함한 VS Team Services 팀 프로젝트가 있으므로 Azure에 팀 프로젝트를 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="b95fd-134">[Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 클라우드 서비스 또는 웹앱을 선택하거나, 왼쪽 아래에 있는 **+** 아이콘을 선택하고 **클라우드 서비스** 또는 **웹앱**을 선택한 후 **빨리 만들기**를 선택하여 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="b95fd-135">**Visual Studio Team Services로 게시 설정** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="b95fd-136">마법사의 텍스트 상자에 Visual Studio Team Services 계정의 이름을 입력하고 **지금 권한 부여** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="b95fd-137">로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="b95fd-138">**연결 요청** 팝업 대화 상자에서 **동의함** 단추를 선택하여 Azure에 권한을 부여하고 VS Team Services에서 팀 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="b95fd-139">권한 부여가 완료되면 Visual Studio Team Services 팀 프로젝트 목록이 포함된 드롭다운이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="b95fd-140">이전 단계에서 만든 팀 프로젝트 이름을 선택하고 마법사의 확인 표시 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="b95fd-141">프로젝트가 연결되면 Visual Studio Team Services 팀 프로젝트에 대한 변경 내용을 체크 인하는 몇 가지 지침이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="b95fd-142">다음번에 체크 인할 때 Visual Studio Team Services에서 프로젝트를 Azure에 빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="b95fd-143">**Visual Studio에서 체크 인** 링크와 **Visual Studio 시작** 링크(또는 포털 화면 아래에 있는 해당 **Visual Studio** 단추)를 차례로 클릭하여 지금 이 작업을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="b95fd-144">4: 프로젝트 다시 빌드 및 다시 배포 트리거</span><span class="sxs-lookup"><span data-stu-id="b95fd-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="b95fd-145">Visual Studio의 **팀 탐색기**에서 **소스 제어 탐색기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="b95fd-146">솔루션 파일로 이동하여 해당 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="b95fd-147">**솔루션 탐색기**에서 파일을 열어 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="b95fd-148">예를 들어 MVC 웹 역할의 Views\\ 폴더에서 `_Layout.cshtml` 파일을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="b95fd-149">사이트 로고를 편집하고 **Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="b95fd-150">**팀 탐색기**에서 **보류 중인 변경 내용** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="b95fd-151">설명을 입력하고 **체크 인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="b95fd-152">**홈** 단추를 선택하여 **팀 탐색기** 홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="b95fd-153">**빌드** 링크를 선택하여 진행 중인 빌드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="b95fd-154">**팀 탐색기** 에서 빌드의 체크 인이 트리거되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="b95fd-155">진행 중인 빌드 이름을 두 번 클릭하여 빌드가 진행되는 동안 생성되는 자세한 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="b95fd-156">빌드가 진행되는 동안 마법사를 사용하여 TFS를 Azure에 연결할 때 생성된 빌드 정의를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="b95fd-157">빌드 정의의 바로 가기 메뉴를 열고 **빌드 정의 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="b95fd-158">**트리거** 탭에서 기본적으로 체크 인할 때마다 빌드 정의가 빌드되도록 설정된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="b95fd-159">**프로세스** 탭에서 배포 환경이 사용 중인 클라우드 서비스 또는 웹앱의 이름으로 설정된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="b95fd-160">웹앱에 대해 작업하고 있는 경우 표시되는 속성은 여기에서 표시된 속성과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="b95fd-161">기본값 이외의 다른 값을 원하는 경우 속성 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="b95fd-162">Azure 게시의 속성은 **배포** 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="b95fd-163">다음 테이블에서는 **배포** 섹션에서 사용할 수 있는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="b95fd-164">속성</span><span class="sxs-lookup"><span data-stu-id="b95fd-164">Property</span></span> | <span data-ttu-id="b95fd-165">기본값</span><span class="sxs-lookup"><span data-stu-id="b95fd-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="b95fd-166">신뢰할 수 없는 인증서 허용</span><span class="sxs-lookup"><span data-stu-id="b95fd-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="b95fd-167">false인 경우 루트 인증 기관에서 SSL 인증서에 서명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="b95fd-168">업그레이드 허용</span><span class="sxs-lookup"><span data-stu-id="b95fd-168">Allow Upgrade</span></span> |<span data-ttu-id="b95fd-169">새로운 배포를 만들지 않고 기존 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="b95fd-170">IP 주소를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="b95fd-171">삭제 안 함</span><span class="sxs-lookup"><span data-stu-id="b95fd-171">Do Not Delete</span></span> |<span data-ttu-id="b95fd-172">true인 경우 관련 없는 기존 배포를 덮어쓰지 않습니다(업그레이드가 허용됨).</span><span class="sxs-lookup"><span data-stu-id="b95fd-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="b95fd-173">배포 설정의 경로</span><span class="sxs-lookup"><span data-stu-id="b95fd-173">Path to Deployment Settings</span></span> |<span data-ttu-id="b95fd-174">보고서의 루트 폴더를 기준으로 웹앱의 .pubxml 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="b95fd-175">클라우드 서비스의 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="b95fd-176">SharePoint 배포 환경</span><span class="sxs-lookup"><span data-stu-id="b95fd-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="b95fd-177">서비스 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-177">The same as the service name.</span></span> |
    | <span data-ttu-id="b95fd-178">Azure 배포 환경</span><span class="sxs-lookup"><span data-stu-id="b95fd-178">Azure Deployment Environment</span></span> |<span data-ttu-id="b95fd-179">웹앱 또는 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="b95fd-180">여러 서비스 구성(.cscfg 파일)을 사용하는 경우 **빌드, 고급, MSBuild 인수** 설정에서 원하는 서비스 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="b95fd-181">예를 들어 ServiceConfiguration.Test.cscfg를 사용하려면 MSBuild 인수 줄 옵션인 `/p:TargetProfile=Test`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="b95fd-182">이제 빌드가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="b95fd-183">빌드 이름을 두 번 클릭하면 Visual Studio에서 연결된 단위 테스트 프로젝트의 모든 테스트 결과가 포함된 **빌드 요약**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="b95fd-184">[Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 스테이징 환경을 선택하면 **배포** 탭에서 연결된 배포를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="b95fd-185">사용 중인 사이트의 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-185">Browse to your site's URL.</span></span> <span data-ttu-id="b95fd-186">웹앱의 경우 명령 모음의 **찾아보기** 단추를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="b95fd-187">클라우드 서비스의 경우 클라우드 서비스에 대한 스테이징 환경을 표시하는 **대시보드** 페이지의 **간략 상태** 섹션에서 URL을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="b95fd-188">클라우드 서비스의 연속 통합에서 배포는 기본적으로 스테이징 환경에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="b95fd-189">**대체 클라우드 서비스 환경** 속성을 **프로덕션**으로 설정하여 이를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="b95fd-190">다음 스크린샷은 클라우드 서비스의 대시보드 페이지에서 사이트 URL이 어느 위치에 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="b95fd-191">새 브라우저 탭이 열리며 실행 중인 사이트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="b95fd-192">클라우드 서비스의 경우 프로젝트의 다른 내용을 변경하고 추가 빌드를 트리거하면 여러 배포가 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="b95fd-193">최신 배포가 활성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="b95fd-194">5: 초기 빌드 다시 배포</span><span class="sxs-lookup"><span data-stu-id="b95fd-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="b95fd-195">이 단계는 클라우드 서비스에 적용되며 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="b95fd-196">Azure 클래식 포털에서 이전 배포를 선택하고 **다시 배포** 단추를 선택하여 사이트를 이전 체크 인으로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="b95fd-197">그러면 TFS에 새 빌드가 트리거되고 배포 기록에 새 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="b95fd-198">6: 프로덕션 배포 변경</span><span class="sxs-lookup"><span data-stu-id="b95fd-198">6: Change the Production deployment</span></span>
<span data-ttu-id="b95fd-199">이 단계는 웹앱이 아닌 클라우드 서비스에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="b95fd-200">준비가 되면 Azure 클래식 포털에서 **교환** 단추를 선택하여 스테이징 환경에서 프로덕션 환경으로 수준을 올릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="b95fd-201">새로 배포된 스테이징 환경에서 프로덕션으로 수준이 올라가며, 이전 프로덕션 환경이 있는 경우 스테이징 환경으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="b95fd-202">활성 배포는 프로덕션 환경과 스테이징 환경에서 서로 다를 수 있지만 최근 빌드의 배포 기록은 환경과 관계없이 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="b95fd-203">7: 단위 테스트 실행</span><span class="sxs-lookup"><span data-stu-id="b95fd-203">7: Run unit tests</span></span>
<span data-ttu-id="b95fd-204">이 단계는 클라우드 서비스가 아닌 웹앱에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="b95fd-205">배포에 대한 품질 관문을 배치하기 위해 단위 테스트를 실행하고 실패할 경우 배포를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="b95fd-206">Visual Studio에서 단위 테스트 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="b95fd-207">테스트하려는 프로젝트에 프로젝트 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="b95fd-208">일부 단위 테스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-208">Add some unit tests.</span></span> <span data-ttu-id="b95fd-209">시작하려면 항상 통과하는 더미 테스트를 시도해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="b95fd-210">빌드 정의를 편집하고 **프로세스** 탭을 선택한 후 **테스트** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="b95fd-211">**테스트 실패 시 빌드 실패** 를 True로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="b95fd-212">이는 테스트를 통과하지 못하면 배포가 수행되지 않는다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="b95fd-213">새 빌드를 큐에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="b95fd-214">빌드가 처리되는 동안 진행 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="b95fd-215">빌드가 완료되면 테스트 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="b95fd-216">실패로 끝나는 테스트를 만들어 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-216">Try creating a test that will fail.</span></span> <span data-ttu-id="b95fd-217">첫 번째 테스트를 복사하고 이름을 바꾼 후 NotImplementedException는 예상되는 예외라고 설명하는 주석을 추가하여 새 테스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="b95fd-218">변경 내용을 체크 인하여 새 빌드를 큐에 대기시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="b95fd-219">테스트 결과에서 실패에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b95fd-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="b95fd-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b95fd-220">Next steps</span></span>
<span data-ttu-id="b95fd-221">Visual Studio Team Services의 단위 테스트에 대한 자세한 내용은 [빌드에서 단위 테스트 실행](http://go.microsoft.com/fwlink/p/?LinkId=510474)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="b95fd-222">Git를 사용하는 경우 [Git로 코드 공유](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) 및 [Azure App Service에 연속 배포](../app-service-web/app-service-continuous-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="b95fd-223">Visual Studio Team Services에 대한 자세한 내용은 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b95fd-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
