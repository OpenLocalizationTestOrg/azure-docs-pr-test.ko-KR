---
title: "Azure에서 Git 및 Visual Studio Team Services를 사용한 지속적인 업데이트 | Microsoft Docs"
description: "Git을 사용하여 자동으로 빌드되어 Azure 앱 서비스 또는 클라우드 서비스의 웹앱 기능에 배포되도록 Visual Studio Team Services 팀 프로젝트를 구성하는 방법을 알아봅니다."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="f6b26-103">Visual Studio Team Services 및 Git을 사용하여 Azure에 지속적으로 전송</span><span class="sxs-lookup"><span data-stu-id="f6b26-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="f6b26-104">Visual Studio Team Services 팀 프로젝트를 사용하여 소스 코드용 Git 리포지토리를 호스트할 수 있으며 리포지토리로 커밋을 푸시할 때마다 Azure 웹앱 또는 클라우드 서비스를 자동으로 빌드 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="f6b26-105">Visual Studio 2013 및 Azure SDK가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="f6b26-106">Visual Studio 2013을 아직 설치하지 않은 경우 **www.visualstudio.com** 에서 [무료로 시작하기](http://www.visualstudio.com)링크를 선택하여 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="f6b26-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="f6b26-107">Azure SDK의 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=239540)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="f6b26-108">이 자습서를 완료하려면 Visual Studio Team Services 계정이 있어야 합니다. [Visual Studio Team Services 계정은 무료로 개설](http://go.microsoft.com/fwlink/p/?LinkId=512979)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="f6b26-109">Visual Studio Team Services를 사용하여 Azure에 자동으로 빌드 및 배포하도록 클라우드 서비스를 설정하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f6b26-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="f6b26-110">1: Git 리포지토리 만들기</span><span class="sxs-lookup"><span data-stu-id="f6b26-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="f6b26-111">Visual Studio Team Services 계정이 없는 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=397665)에서 계정을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="f6b26-112">팀 프로젝트를 만들 때 소스 제어 시스템으로 Git을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="f6b26-113">지침을 따라 Visual Studio를 팀 프로젝트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="f6b26-114">**팀 탐색기**에서 **이 리포지토리 복제** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="f6b26-115">로컬 복사본의 위치를 지정한 다음 **복제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="f6b26-116">2: 프로젝트를 만들어 리포지토리로 푸시</span><span class="sxs-lookup"><span data-stu-id="f6b26-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="f6b26-117">**팀 편집기**의 **솔루션** 섹션에서 로컬 리포지토리에 새 프로젝트를 만들 수 있는 **새** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="f6b26-118">이 연습의 단계에 따라 웹앱 또는 클라우드 서비스(Azure 응용 프로그램)를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="f6b26-119">새 Azure 클라우드 서비스 프로젝트 또는 새 ASP.NET MVC 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="f6b26-120">프로젝트가 .NET Framework 4 또는 그 이상을 대상으로 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="f6b26-121">Visual Studio 클라우드 서비스 프로젝트를 만드는 경우 ASP.NET MVC 웹 역할과 작업자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="f6b26-122">웹앱을 만들려는 경우 **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 선택한 후 **MVC**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="f6b26-123">자세한 내용은 [Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 만들기](../app-service-web/app-service-web-get-started-dotnet.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6b26-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="f6b26-124">솔루션의 바로 가기 메뉴를 열고 **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="f6b26-125">Visual Studio Team Services에서 처음으로 Git을 사용하는 경우 Git에서 본인을 식별해 주는 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="f6b26-126">**팀 탐색기**의 **보류 중인 변경 내용** 영역에서 사용자 이름 및 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="f6b26-127">커밋에 대한 설명을 입력한 다음 **커밋** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="f6b26-128">체크 인할 때 특정 변경 내용을 포함하거나 제외하는 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="f6b26-129">원하는 변경 내용이 제외된 경우 **모두 포함**링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="f6b26-130">이제 리포지토리에 있는 로컬 복사본의 변경 내용을 커밋했습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="f6b26-131">그런 다음 **동기화** 링크를 선택하여 변경 내용을 서버와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="f6b26-132">3: Azure에 프로젝트 연결</span><span class="sxs-lookup"><span data-stu-id="f6b26-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="f6b26-133">Visual Studio Team Services에 일부 소스 코드를 포함한 Git 리포지토리가 있으므로 Azure에 Git 리포지토리를 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="f6b26-134">[Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 클라우드 서비스 또는 웹앱을 선택하거나, 왼쪽 아래에 있는 **클라우드 서비스** 또는 **웹앱**을 선택한 후 **빠른 생성**을 선택하여 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="f6b26-135">클라우드 서비스의 경우 **Visual Studio Team Services로 게시 설정** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="f6b26-136">웹앱의 경우 **소스 코드에서 배포 설정** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="f6b26-137">마법사의 텍스트 상자에 Visual Studio Team Services 계정의 이름을 입력하고 **지금 권한 부여** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="f6b26-138">로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="f6b26-139">**연결 요청** 팝업 대화 상자에서 **동의함**을 선택하여 Azure에 권한을 부여하고 Visual Studio Team Services에서 팀 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="f6b26-140">권한 부여가 완료된 후, Visual Studio Team Services 팀 프로젝트를 포함하는 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="f6b26-141">이전 단계에서 만든 팀 프로젝트 이름을 선택하고 마법사의 확인 표시 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="f6b26-142">다음에 리포지토리에 커밋을 푸시할 때 Visual Studio Team Services가 프로젝트를 빌드하여 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="f6b26-143">4: 프로젝트 다시 빌드 및 다시 배포 트리거</span><span class="sxs-lookup"><span data-stu-id="f6b26-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="f6b26-144">Visual Studio에서 파일을 열어 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="f6b26-145">예를 들어 MVC 웹 역할의 Views\\ 폴더에서 `_Layout.cshtml` 파일을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="f6b26-146">사이트에 대한 바닥글 텍스트를 편집하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="f6b26-147">**솔루션 탐색기**에서 솔루션 노드, 프로젝트 노드 또는 변경한 파일의 바로 가기 메뉴를 연 다음, **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="f6b26-148">설명을 입력하고 **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="f6b26-149">**동기화** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="f6b26-150">**푸시** 링크를 선택하여 Visual Studio Team Services의 리포지토리에 커밋을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="f6b26-151">또한 **동기화** 단추를 사용하여 리포지토리로 커밋을 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="f6b26-152">**동기화** 는 리포지토리의 최신 변경 내용을 끌어온다는 점이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="f6b26-153">**홈** 단추를 선택하여 **팀 탐색기** 홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="f6b26-154">**빌드** 링크를 선택하여 진행 중인 빌드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="f6b26-155">**팀 탐색기** 에서 빌드의 체크 인이 트리거되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="f6b26-156">빌드가 진행되는 동안 자세한 로그를 보려면 진행 중인 빌드의 이름을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="f6b26-157">빌드가 진행되는 동안 마법사를 사용하여 Azure에 연결할 때 생성된 빌드 정의를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="f6b26-158">빌드 정의의 바로 가기 메뉴를 열고 **빌드 정의 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="f6b26-159">**트리거** 탭에서 기본적으로 체크 인할 때마다 빌드 정의가 빌드되도록 설정된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="f6b26-160">클라우드 서비스의 경우 Visual Studio Team Services에서 마스터 분기를 자동으로 빌드하여 스테이징 환경에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="f6b26-161">라이브 사이트에 배포하려면 여전히 수동 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="f6b26-162">스테이징 환경이 없는 웹 사이트의 경우 마스터 분기를 라이브 사이트에 직접 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="f6b26-163">**프로세스** 탭에서 배포 환경이 사용 중인 클라우드 서비스 또는 웹앱의 이름으로 설정된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="f6b26-164">기본값 이외의 다른 값을 원하는 경우 속성 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="f6b26-165">Azure 게시의 속성은 **배포** 섹션에 있으며 MSBuild 매개 변수를 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="f6b26-166">예를 들어 클라우드 서비스 프로젝트에서 "클라우드" 외의 서비스 구성을 지정하려면 MSbuild 매개 변수를 `/p:TargetProfile=[YourProfile]`로 설정합니다. 여기서 *[YourProfile]*은 ServiceConfiguration.*YourProfile*.cscfg와 같은 이름을 갖는 서비스 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="f6b26-167">다음 테이블에서는 **배포** 섹션에서 사용할 수 있는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="f6b26-168">속성</span><span class="sxs-lookup"><span data-stu-id="f6b26-168">Property</span></span> | <span data-ttu-id="f6b26-169">기본값</span><span class="sxs-lookup"><span data-stu-id="f6b26-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f6b26-170">신뢰할 수 없는 인증서 허용</span><span class="sxs-lookup"><span data-stu-id="f6b26-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="f6b26-171">false인 경우 루트 인증 기관에서 SSL 인증서에 서명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="f6b26-172">업그레이드 허용</span><span class="sxs-lookup"><span data-stu-id="f6b26-172">Allow Upgrade</span></span> |<span data-ttu-id="f6b26-173">새로운 배포를 만들지 않고 기존 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="f6b26-174">IP 주소를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="f6b26-175">삭제 안 함</span><span class="sxs-lookup"><span data-stu-id="f6b26-175">Do Not Delete</span></span> |<span data-ttu-id="f6b26-176">true인 경우 관련 없는 기존 배포를 덮어쓰지 않습니다(업그레이드가 허용됨).</span><span class="sxs-lookup"><span data-stu-id="f6b26-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="f6b26-177">배포 설정의 경로</span><span class="sxs-lookup"><span data-stu-id="f6b26-177">Path to Deployment Settings</span></span> |<span data-ttu-id="f6b26-178">보고서의 루트 폴더를 기준으로 웹앱의 .pubxml 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="f6b26-179">클라우드 서비스의 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="f6b26-180">SharePoint 배포 환경</span><span class="sxs-lookup"><span data-stu-id="f6b26-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="f6b26-181">서비스 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-181">The same as the service name.</span></span> |
    | <span data-ttu-id="f6b26-182">Azure 배포 환경</span><span class="sxs-lookup"><span data-stu-id="f6b26-182">Azure Deployment Environment</span></span> |<span data-ttu-id="f6b26-183">웹앱 또는 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="f6b26-184">이제 빌드가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="f6b26-185">빌드 이름을 두 번 클릭하면 Visual Studio에서 연결된 단위 테스트 프로젝트의 모든 테스트 결과가 포함된 **빌드 요약**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="f6b26-186">[Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 스테이징 환경을 선택하면 **배포** 탭에서 연결된 배포를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="f6b26-187">사용 중인 사이트의 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-187">Browse to your site's URL.</span></span> <span data-ttu-id="f6b26-188">웹앱의 경우 포털에서 **찾아보기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="f6b26-189">클라우드 서비스의 경우 클라우드 서비스에 대한 스테이징 환경을 표시하는 **대시보드** 페이지의 **간략 상태** 섹션에서 URL을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="f6b26-190">클라우드 서비스의 연속 통합에서 배포는 기본적으로 스테이징 환경에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="f6b26-191">**대체 클라우드 서비스 환경** 속성을 **프로덕션**으로 설정하여 이를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="f6b26-192">다음 스크린샷은 클라우드 서비스의 대시보드 페이지에서 사이트 URL이 어느 위치에 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="f6b26-193">새 브라우저 탭이 열리며 실행 중인 사이트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="f6b26-194">프로젝트의 다른 내용을 변경하고 추가 빌드를 트리거하면 여러 배포가 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="f6b26-195">최신 배포가 활성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="f6b26-196">5: 초기 빌드 다시 배포</span><span class="sxs-lookup"><span data-stu-id="f6b26-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="f6b26-197">이 단계는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-197">This step is optional.</span></span> <span data-ttu-id="f6b26-198">Azure 클래식 포털에서 이전 배포를 선택하고 **다시 배포** 를 선택하여 사이트를 이전 체크 인으로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="f6b26-199">그러면 TFS에 새 빌드가 트리거되고 배포 기록에 새 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="f6b26-200">6: 프로덕션 배포 변경</span><span class="sxs-lookup"><span data-stu-id="f6b26-200">6: Change the Production deployment</span></span>
<span data-ttu-id="f6b26-201">준비가 되면 Azure 클래식 포털에서 **교환** 을 선택하여 스테이징 환경에서 프로덕션 환경으로 수준을 올릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="f6b26-202">새로 배포된 스테이징 환경에서 프로덕션으로 수준이 올라가며, 이전 프로덕션 환경이 있는 경우 스테이징 환경으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="f6b26-203">활성 배포는 프로덕션 환경과 스테이징 환경에서 서로 다를 수 있지만 최근 빌드의 배포 기록은 환경과 관계없이 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="f6b26-204">7: 작업 분기에서 배포</span><span class="sxs-lookup"><span data-stu-id="f6b26-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="f6b26-205">Git을 사용할 경우 보통 작업 분기에서 변경한 다음 개발이 최종 단계에 도달하면 마스터 분기로 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="f6b26-206">프로젝트의 개발 단계에서는 작업 분기를 구성하여 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="f6b26-207">**팀 탐색기**에서 **홈** 단추를 선택한 다음 **분기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="f6b26-208">**새 분기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="f6b26-209">"working"과 같은 분기의 이름을 입력하고 **분기 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="f6b26-210">그러면 새 로컬 분기가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="f6b26-211">분기를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-211">Publish the branch.</span></span> <span data-ttu-id="f6b26-212">**게시 취소된 분기**에서 분기 이름을 선택하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="f6b26-213">기본적으로 마스터 분기만 변경하면 연속 빌드가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="f6b26-214">작업 분기의 연속 빌드를 설정하려면 **팀 탐색기**에서 **빌드** 페이지를 선택하고 **빌드 정의 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="f6b26-215">**소스 설정** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="f6b26-216">**지속적인 통합 및 빌드의 모니터링된 분기**에서 **새 행을 추가하려면 여기를 클릭하세요.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="f6b26-217">생성된 분기(예: refs/heads/working)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="f6b26-218">코드를 변경하고, 변경된 파일의 바로 가기 메뉴를 연 다음, **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="f6b26-219">**동기화되지 않은 커밋** 링크를 선택한 다음 **동기화** 단추 또는 **푸시** 링크를 선택하여 Visual Studio Team Services에서 작업 분기의 복사본 변경 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="f6b26-220">**빌드** 뷰로 이동하여 작업 분기에 대해 트리거된 빌드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f6b26-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6b26-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6b26-221">Next steps</span></span>
<span data-ttu-id="f6b26-222">Visual Studio Team Services에서 Git 사용에 대해 더 많은 팁을 알아보려면 [Visual Studio를 사용하여 Git에서 코드 개발 및 공유](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017)를 참조하고, Visual Studio Team Services에서 관리하지 않는 Git 리포지토리를 사용하여 Azure에 게시하는 방법에 대한 자세한 내용은 [Azure App Service에 지속적인 배포](../app-service-web/app-service-continuous-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6b26-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f6b26-223">Visual Studio Team Services에 대한 자세한 내용은 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6b26-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
