---
title: "Git 및 Azure에서 Visual Studio Team Services를 사용한 aaaContinuous 배달 | Microsoft Docs"
description: "어떻게 tooconfigure Visual Studio Team Services 팀 프로젝트 toouse Git tooautomatically 빌드 및 Azure 앱 서비스 또는 클라우드 서비스의 toohello 웹 응용 프로그램 기능을 배포에 대해 알아봅니다."
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
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="5a330-103">Visual Studio Team Services 및 Git를 사용 하 여 지속적인 업데이트 tooAzure</span><span class="sxs-lookup"><span data-stu-id="5a330-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="5a330-104">있습니다 수 소스 코드를 Visual Studio Team Services 팀 프로젝트 toohost Git 리포지토리를 사용 하 고 자동으로 빌드 및 tooAzure 웹 앱을 배포 또는 클라우드 서비스 커밋 toohello 리포지토리에 푸시 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="5a330-105">Visual Studio 2013 및 Azure SDK가 설치 되어 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="5a330-106">Visual Studio 2013, 아직 없는 경우 hello를 선택 하 여 다운로드 **무료로 시작** 동시 연결할 [www.visualstudio.com](http://www.visualstudio.com)합니다. 설치에서 Azure SDK hello [여기](http://go.microsoft.com/fwlink/?LinkId=239540)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="5a330-107">이 자습서는 Visual Studio Team Services 계정 toocomplete 필요한: 할 수 있습니다 [무료 Visual Studio Team Services 계정 열고](http://go.microsoft.com/fwlink/p/?LinkId=512979)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="5a330-108">클라우드 서비스 tooautomatically tooset 빌드 및 Visual Studio Team Services를 사용 하 여 tooAzure 배포, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="5a330-109">1: Git 리포지토리 만들기</span><span class="sxs-lookup"><span data-stu-id="5a330-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="5a330-110">Visual Studio Team Services 계정이 없는 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=397665)에서 계정을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="5a330-111">팀 프로젝트를 만들 때 소스 제어 시스템으로 Git을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="5a330-112">Hello 지침 tooconnect Visual Studio tooyour 팀 프로젝트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="5a330-113">**팀 탐색기**, hello 선택 **이 리포지토리를 복제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="5a330-114">Hello 로컬 복사본의 hello 위치를 지정 하 고 hello를 눌러 **복제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="5a330-115">2: 프로젝트를 만들고 toohello 저장소 커밋</span><span class="sxs-lookup"><span data-stu-id="5a330-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="5a330-116">**팀 탐색기**, hello에 **솔루션** 섹션에서 hello **새로** toocreate hello 로컬 저장소에서 새 프로젝트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="5a330-117">웹 앱을 배포할 수 또는이 연습 단계를 다음 hello 사용 하 여 클라우드 서비스 (Azure 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="5a330-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="5a330-118">새 Azure 클라우드 서비스 프로젝트 또는 새 ASP.NET MVC 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="5a330-119">Hello 프로젝트의 대상.NET Framework 4 hello 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="5a330-120">Visual Studio 클라우드 서비스 프로젝트를 만드는 경우 ASP.NET MVC 웹 역할과 작업자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="5a330-121">Toocreate 웹 응용 프로그램을 사용 하도록 하려는 경우 선택 hello **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 선택한 후 **MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="5a330-122">자세한 내용은 [Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 만들기](../app-service-web/app-service-web-get-started-dotnet.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a330-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="5a330-123">Hello 솔루션에 대 한 hello 바로 가기 메뉴를 열고 **커밋**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="5a330-124">인 경우 hello 처음으로 Visual Studio Team Services에서 Git를 사용한 해야 tooprovide 일부 정보 tooidentify 직접 Git에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="5a330-125">Hello에 **보류 중인 변경 내용** 부문의 **팀 탐색기**사용자 이름을 입력 하 고 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="5a330-126">Hello 커밋에 대 한 설명을 입력 한 다음 hello **커밋** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="5a330-127">Hello 옵션 tooinclude 또는 특정 변경 내용을 체크 인할 때 제외.</span><span class="sxs-lookup"><span data-stu-id="5a330-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="5a330-128">Hello 변경한 경우 하려는 제외 된를 **모두 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="5a330-129">했습니다. 이제 hello 저장소의 로컬 복사본으로 커밋된 hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="5a330-130">다음으로 hello를 선택 하 여 hello 서버와 해당 변경 내용을 동기화 **동기화** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="5a330-131">3: hello 프로젝트 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="5a330-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="5a330-132">준비 tooconnect는 일부 소스 코드를 Visual Studio Team Services의 Git 리포지토리를가지고 git 리포지토리 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="5a330-133">Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)클라우드 서비스나 웹 응용 프로그램을 선택 하거나 hello + 왼쪽 아래 hello 및 선택 아이콘을 선택 하 여 새로 만들 **클라우드 서비스** 또는 **웹 응용 프로그램**차례로 **빨리 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="5a330-134">클라우드 서비스에 대 한 선택 hello **Visual Studio Team Services를 통해 게시 설정** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="5a330-135">웹 앱에 대 한 선택 hello **소스 제어에서 배포 설정** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="5a330-136">Hello 마법사에서 hello 텍스트 상자에 hello Visual Studio Team Services 계정 이름을 입력 하 고 hello 선택 **이제 권한을 부여** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="5a330-137">toosign을 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="5a330-138">Hello에 **연결 요청** 팝업 대화 상자에서 선택 **Accept** tooauthorize Azure tooconfigure Visual Studio Team Services에서 팀 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="5a330-139">권한 부여가 완료된 후, Visual Studio Team Services 팀 프로젝트를 포함하는 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="5a330-140">Hello 이전 단계에서 만든 팀 프로젝트의 hello 이름 선택한 hello 마법사의 확인 표시 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="5a330-141">hello 커밋 tooyour 리포지토리를 Visual Studio Team Services 푸시 다음에 빌드하고 프로젝트 tooAzure 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="5a330-142">4: 프로젝트 다시 빌드 및 다시 배포 트리거</span><span class="sxs-lookup"><span data-stu-id="5a330-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="5a330-143">Visual Studio에서 파일을 열어 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="5a330-144">예를 들어 hello 파일을 변경 `_Layout.cshtml` hello 보기에서\\MVC 웹 역할에서 공유 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="5a330-145">Hello 사이트에 대 한 hello 바닥글 텍스트를 편집 하 고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="5a330-146">**솔루션 탐색기**를 hello 솔루션 노드, 프로젝트 노드 또는 hello 파일 변경 hello 바로 가기 메뉴를 열고 다음 선택 **커밋**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="5a330-147">설명을 입력하고 **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="5a330-148">Hello 선택 **동기화** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="5a330-149">Hello 선택 **푸시** toopush Visual Studio Team Services에서 커밋 toohello 리포지토리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="5a330-150">(Hello를 사용할 수도 있습니다 **동기화** toocopy 커밋 toohello 리포지토리에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="5a330-151">hello 차이점은 **동기화** 도 끌어오는 소스 hello hello 리포지토리에서 최근 변경 내용을.)</span><span class="sxs-lookup"><span data-stu-id="5a330-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="5a330-152">Hello 선택 **홈** 단추 tooreturn toohello **팀 탐색기** 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="5a330-153">선택 **빌드** tooview hello 빌드 진행 중에서입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="5a330-154">**팀 탐색기** 에서 빌드의 체크 인이 트리거되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="5a330-155">자세한 로그 tooview hello 빌드 진행 과정에서 이름을 두 번 클릭 hello hello 빌드가 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="5a330-156">Hello 빌드가 진행 중인 hello 마법사 toolink tooAzure를 사용할 때 생성 된 hello 빌드 정의에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="5a330-157">Hello 빌드 정의 대 한 hello 바로 가기 메뉴를 열고 **빌드 정의 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="5a330-158">Hello에 **트리거** 탭 표시 됩니다는 hello 빌드 정의 toobuild 모든 체크 인에 기본적으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="5a330-159">(클라우드 서비스에 대 한 Visual Studio Team Services 빌드 및 배포 환경을 자동으로 준비 하는 hello 마스터 분기 toohello.</span><span class="sxs-lookup"><span data-stu-id="5a330-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="5a330-160">해야 toodo 수동 단계 toodeploy toohello 라이브 사이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="5a330-161">웹 앱에는 스테이징 환경 없는 hello 마스터 분기 toohello 라이브 사이트에 직접 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="5a330-162">Hello에 **프로세스** 탭 hello 배포 환경에 클라우드 서비스 또는 웹 응용 프로그램의 toohello 이름을 설정 되어을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="5a330-163">Hello 기본값 값은 다른 hello 속성에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="5a330-164">hello Azure 게시에 대 한 속성에에서 있는 hello **배포** 섹션과 있습니다 tooset MSBuild 매개 변수 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="5a330-165">예를 들어 toospecify "클라우드" 이외의 다른 서비스 구성 클라우드 서비스 프로젝트에서 hello MSbuild 매개 변수를 너무 설정`/p:TargetProfile=[YourProfile]` 여기서 *[YourProfile]* 일치와 같은 이름 가진 서비스 구성 파일 ServiceConfiguration입니다. *YourProfile*.cscfg입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="5a330-166">hello 다음 표에 나와 hello 사용 가능한 속성 hello **배포** 섹션:</span><span class="sxs-lookup"><span data-stu-id="5a330-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="5a330-167">속성</span><span class="sxs-lookup"><span data-stu-id="5a330-167">Property</span></span> | <span data-ttu-id="5a330-168">기본값</span><span class="sxs-lookup"><span data-stu-id="5a330-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5a330-169">신뢰할 수 없는 인증서 허용</span><span class="sxs-lookup"><span data-stu-id="5a330-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="5a330-170">false인 경우 루트 인증 기관에서 SSL 인증서에 서명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="5a330-171">업그레이드 허용</span><span class="sxs-lookup"><span data-stu-id="5a330-171">Allow Upgrade</span></span> |<span data-ttu-id="5a330-172">Hello 배포 tooupdate 새로 만드는 대신 기존 배포를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="5a330-173">Hello IP 주소를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="5a330-174">삭제 안 함</span><span class="sxs-lookup"><span data-stu-id="5a330-174">Do Not Delete</span></span> |<span data-ttu-id="5a330-175">true인 경우 관련 없는 기존 배포를 덮어쓰지 않습니다(업그레이드가 허용됨).</span><span class="sxs-lookup"><span data-stu-id="5a330-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="5a330-176">경로 tooDeployment 설정</span><span class="sxs-lookup"><span data-stu-id="5a330-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="5a330-177">hello tooyour.pubxml 파일 경로 웹 앱, 상대 toohello hello 리 포 루트 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="5a330-178">클라우드 서비스의 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="5a330-179">SharePoint 배포 환경</span><span class="sxs-lookup"><span data-stu-id="5a330-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="5a330-180">hello 서비스 이름으로을 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="5a330-181">Azure 배포 환경</span><span class="sxs-lookup"><span data-stu-id="5a330-181">Azure Deployment Environment</span></span> |<span data-ttu-id="5a330-182">hello 웹 응용 프로그램 또는 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="5a330-183">이제 빌드가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="5a330-184">Hello 빌드 이름을 두 번 클릭 하면 Visual Studio는 표시는 **빌드 요약**, 연결 된 단위 테스트 프로젝트의 모든 테스트 결과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="5a330-185">Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), hello에 관련 된 hello 배포를 볼 수 있습니다 **배포** hello 스테이징 환경 선택 된 경우를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="5a330-186">찾아보기 tooyour 사이트의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="5a330-187">웹 앱에 대 한 선택 hello **찾아보기** hello 포털에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="5a330-188">클라우드 서비스에 대 한 hello에 hello URL 선택 **빠른 보기** hello 섹션 **대시보드** hello 스테이징 환경을 보여 주는 페이지.</span><span class="sxs-lookup"><span data-stu-id="5a330-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="5a330-189">클라우드 서비스에 대 한 연속 통합에서 배포는 기본적으로 게시 된 toohello 스테이징 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="5a330-190">Hello 설정 하 여 변경할 수 있습니다 **대체 클라우드 서비스 환경** 속성 너무**프로덕션**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="5a330-191">여기서 hello 사이트 URL을 hello 클라우드 서비스의 대시보드 페이지에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="5a330-192">새 브라우저 탭이 열립니다 실행 중인 사이트 tooreveal 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="5a330-193">만들면 tooyour 프로젝트 변경 된 기타, 하면 트리거 더 빌드 및 배포를 여러 개를 누적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="5a330-194">hello 최신 중 하나가 활성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="5a330-195">5: 초기 빌드 다시 배포</span><span class="sxs-lookup"><span data-stu-id="5a330-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="5a330-196">이 단계는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-196">This step is optional.</span></span> <span data-ttu-id="5a330-197">에 Azure 클래식 포털 hello 이전 배포를 선택 하 고 선택 **재배포** toorewind 사이트 tooan를 앞에서 체크 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="5a330-198">그러면 TFS에 새 빌드가 트리거되고 배포 기록에 새 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="5a330-199">6: hello 프로덕션 배포를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="5a330-200">준비 되 면 선택 하 여 hello 준비 toohello 프로덕션 환경의 승격할 수 있습니다 **교체** hello Azure 클래식 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="5a330-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="5a330-201">새로 배포 된 hello 스테이징 환경 승격된 tooProduction 이며 hello 이전 프로덕션 환경에서는 있는 경우 스테이징 환경 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="5a330-202">활성 배포 hello hello 프로덕션 및 스테이징 환경에 대해 다를 수 있습니다 하지만 최근 빌드 hello 배포 기록을 hello 동일 환경에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="5a330-203">7: 작업 분기에서 배포</span><span class="sxs-lookup"><span data-stu-id="5a330-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="5a330-204">Git를 사용 하면 일반적으로 변경 작업 분기에서 하 고 개발에는 완료 된 상태에 도달할 때 hello 마스터 분기에 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="5a330-205">프로젝트를 hello 개발 단계 동안 toobuild 원하는 고 hello 작업 분기 tooAzure를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="5a330-206">**팀 탐색기**, hello 선택 **홈** 단추를 선택한 후 hello **분기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="5a330-207">Hello 선택 **새 분기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="5a330-208">"Working"와 같은 hello 분기의 hello 이름을 입력 하 고 선택 **분기 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="5a330-209">그러면 새 로컬 분기가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="5a330-210">Hello 분기를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-210">Publish hello branch.</span></span> <span data-ttu-id="5a330-211">Hello 분기 이름에 선택 **분기 게시 되지 않은**, 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="5a330-212">기본적으로 toohello 마스터 분기는 연속 빌드 트리거를 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="5a330-213">작업 분기에 대 한 연속 빌드 설치 tooset 선택 hello **빌드** 페이지에 **팀 탐색기**, 선택 **빌드 정의 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="5a330-214">열기 hello **소스 설정** 탭 합니다. 아래 **연속 통합 및 빌드에 대 한 분기 모니터링**, 선택 **tooadd 새 행 여기를 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="5a330-215">Refs/헤드/작업 같이 사용자가 만든 hello 분기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="5a330-216">선택 hello 코드를 변경 하는 hello 파일에 대 한 바로 가기 메뉴를 열고 hello에 변경 내용을 확인 한 다음 **커밋**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="5a330-217">Hello 선택 **되지 않은 커밋** 링크를 선택한 hello **동기화** 단추나 hello **푸시** 링크 toocopy hello toohello 복사본 Visual Studio에서 hello 작업 분기의 변경 Team Services입니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="5a330-218">Toohello 이동 **빌드** 보기 및 hello 작업 분기에 대 한 hello 빌드를 방금 트리거한 (를) 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a330-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a330-219">Next steps</span></span>
<span data-ttu-id="5a330-220">toolearn Visual Studio Team Services를 통해 Git를 사용 하 여에 관한 자세한 정보 참조 [개발 하 고 Visual Studio를 사용 하 여 Git에서 코드를 공유할](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) toopublish Visual Studio Team Services에서 관리 되지 않는 한 Git 리포지토리를 사용 하 여에 대 한 정보 tooAzure, 참조 [연속 배포 tooAzure 앱 서비스](../app-service-web/app-service-continuous-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a330-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="5a330-221">Visual Studio Team Services에 대한 자세한 내용은 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a330-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
