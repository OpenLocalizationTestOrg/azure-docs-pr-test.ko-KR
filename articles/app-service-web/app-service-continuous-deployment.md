---
title: "앱 서비스 배포 tooAzure aaaContinuous | Microsoft Docs"
description: "자세한 내용은 방법 tooenable 연속 배포 tooAzure 앱 서비스입니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="888f2-103">연속 배포 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="888f2-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="888f2-104">이 자습서에서는 어떻게 tooconfigure 연속 배포 워크플로의 대 한 프로그램 [Azure 앱 서비스] 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="888f2-105">BitBucket, GitHub와 서비스 응용 프로그램 통합 및 [VSTS Visual Studio Team Services ()](https://www.visualstudio.com/team-services/) 연속을 사용 하면 Azure 프로젝트에서 hello 가장 최근의 업데이트를 가져와서 여기서 배포 워크플로 tooone 이러한 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="888f2-106">연속 배포는 여러 개의 빈번한 작성자가 통합되는 프로젝트에 적합한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="888f2-107">어떻게 tooconfigure 연속 배포로 나열 되지 않은 클라우드 저장소에서 수동으로 hello Azure 포털 아웃 toofind (같은 [GitLab](https://gitlab.com/)), 참조 [수동 단계를 사용 하 여 연속 배포를 설정](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="888f2-108"><a name="overview"></a>연속 배포 활성화</span><span class="sxs-lookup"><span data-stu-id="888f2-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="888f2-109">tooenable 연속 배포</span><span class="sxs-lookup"><span data-stu-id="888f2-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="888f2-110">연속 배포에 사용 될 응용 프로그램 콘텐츠 toohello 리포지토리를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="888f2-111">프로젝트 toothese 서비스 게시에 대 한 자세한 내용은 참조 하십시오. [리포지토리 (GitHub)를 만들], [리포지토리 (BitBucket) 만들기], 및 [VSTS 시작]합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="888f2-112">Hello에 응용 프로그램의 메뉴 블레이드에서 [Azure 포털], 클릭 **응용 프로그램 배포 > 배포 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="888f2-113">클릭 **소스 선택**을 선택한 후 hello 배포 원본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="888f2-114">앱 서비스 배포에 대 한 VSTS 계정을 tooconfigure 하십시오이 참조 [자습서](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="888f2-115">Hello 권한 부여 워크플로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="888f2-116">Hello에 **배포 원본** 블레이드에서 hello 프로젝트를 선택 하 고에서 toodeploy 분기 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="888f2-117">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="888f2-118">GitHub 또는 BitBucket에서 지속적으로 배포할 수 있도록 하면 공용 및 개인 프로젝트가 둘 다 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="888f2-119">Hello 선택한 저장소와의 연결을 만들고 hello 지정 된 분기에서 hello 파일에서 가져오는 앱 서비스 앱에 대 한 저장소의 복제본을 유지 관리 하는 응용 프로그램 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="888f2-120">Hello 통합 hello 앱 서비스를 사용 하 여 VSTS hello Azure 포털의에서 연속 배포를 구성할 때 [Kudu 배포 엔진](https://github.com/projectkudu/kudu/wiki)어떤, 이미 있는 빌드 및 배포 작업을 자동화 모든 `git push`합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="888f2-121">Tooseparately 불필요 VSTS에서 연속 배포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="888f2-122">이 프로세스가 완료 되 면 hello **배포 옵션** 앱 블레이드 배포를 나타내는 활성 배포 성공이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="888f2-123">tooverify hello 응용 프로그램이 성공적으로 배포 되었는지, hello 클릭 **URL** hello hello 앱 블레이드 hello Azure 포털의에서 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="888f2-124">선택한 hello 리포지토리에서 지속적인 배포 발생 하 고 있는 tooverify 변경 toohello 리포지토리를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="888f2-125">앱은 hello 푸시 toohello 리포지토리 완료 된 후에 곧 tooreflect hello 변경 사항을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="888f2-126">Hello 업데이트 hello에 가져올에 확인할 수 있습니다 **배포 옵션** 응용 프로그램의 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="888f2-127"><a name="VSsolution"></a>Visual Studio 솔루션의 연속 배포</span><span class="sxs-lookup"><span data-stu-id="888f2-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="888f2-128">Visual Studio 솔루션 tooAzure 앱 서비스를 푸시하는 간단한 index.html 파일을 푸시하는 것 처럼 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="888f2-129">앱 서비스 배포 프로세스 hello NuGet 종속성을 복원 하 고 구축 hello 응용 프로그램 이진 파일을 포함 하 여 모든 hello 세부 정보를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="888f2-130">Hello 소스 제어의 Git 리포지토리를 에서만 코드를 유지 관리 모범 사례에 따라 수 있으며 앱 서비스 배포 hello rest를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="888f2-131">hello 서비스는 Visual Studio 솔루션 tooApp에 밀어 넣는 단계 hello 동일 hello와 같이 [이전 섹션](#overview), 구성 하는 경우 솔루션 및 리포지토리 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="888f2-132">Visual Studio 소스 제어 옵션 toogenerate hello를 사용 하 여 한 `.gitignore` 아래 hello 이미지 등의 파일 또는 수동으로 추가 `.gitignore` 와 비슷한 toothis 콘텐츠 리포지토리 루트에 파일 [.gitignore 샘플](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="888f2-133">Hello.sln 파일 hello 리포지토리 루트에 있는 hello 전체 솔루션 디렉터리 트리 tooyour 리포지토리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="888f2-134">Visual Studio에서 로컬로 ASP.NET 응용 프로그램을 개발 하 고 지속적으로 코드를 하 여 배포 수, 설명 된 대로 저장소를 설정 하 고 Azure의 hello 온라인 Git 리포지토리 중 하나에서 지속적인 게시에 대 한 응용 프로그램을 구성 후 변경 내용을 tooyour 온라인 Git 리포지토리가 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="888f2-135"><a name="disableCD"></a>지속적 배포 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="888f2-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="888f2-136">toodisable 연속 배포</span><span class="sxs-lookup"><span data-stu-id="888f2-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="888f2-137">Hello에 응용 프로그램의 메뉴 블레이드에서 [Azure 포털], 클릭 **응용 프로그램 배포 > 배포 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="888f2-138">클릭 **연결 끊기** hello에 **배포 옵션** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="888f2-139">에 답변 한 후 **예** toohello 확인 메시지에서 있습니다 수 tooyour 앱 블레이드 돌아가서 **응용 프로그램 배포 > 배포 옵션** tooset 다른 원본에서 게시를 원하는 경우.</span><span class="sxs-lookup"><span data-stu-id="888f2-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="888f2-140">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="888f2-140">Additional Resources</span></span>
* [<span data-ttu-id="888f2-141">연속 배포와 tooinvestigate 공통 발급 하는 방법</span><span class="sxs-lookup"><span data-stu-id="888f2-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="888f2-142">[어떻게 toouse Azure에 대 한 PowerShell]</span><span class="sxs-lookup"><span data-stu-id="888f2-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="888f2-143">[Toouse는 Mac 및 Linux 용 Azure 명령줄 도구를 hello 하는 방법]</span><span class="sxs-lookup"><span data-stu-id="888f2-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="888f2-144">[Git 설명서]</span><span class="sxs-lookup"><span data-stu-id="888f2-144">[Git documentation]</span></span>
* [<span data-ttu-id="888f2-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="888f2-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="888f2-146">Azure를 사용 하 여 tooautomatically CI/CD 파이프라인 toodeploy ASP.NET 4 응용 프로그램 생성</span><span class="sxs-lookup"><span data-stu-id="888f2-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="888f2-147">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="888f2-148">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="888f2-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure 앱 서비스]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure 포털]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[어떻게 toouse Azure에 대 한 PowerShell]: /powershell/azureps-cmdlets-docs
[Toouse는 Mac 및 Linux 용 Azure 명령줄 도구를 hello 하는 방법]:../cli-install-nodejs.md
[Git 설명서]: http://git-scm.com/documentation

[리포지토리 (GitHub)를 만들]: https://help.github.com/articles/create-a-repo
[리포지토리 (BitBucket) 만들기]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[VSTS 시작]: https://www.visualstudio.com/docs/vsts-tfs-overview
