---
title: "Jenkins tooAzure Team Services를 통해 Vm에서에서 aaaCI/CD | Microsoft Docs"
description: "CI (연속 통합) 및 VSTS Visual Studio Team Services () 또는 Microsoft Team Foundation Server (TFS)에 Release Management에서 Jenkins tooAzure Vm을 사용 하 여 Node.js 응용 프로그램의 연속 배포 (CD) 설정"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="a5872-103">사용자 응용 프로그램 tooLinux Vm 배포 Jenkins 및 Team Services를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a5872-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="a5872-104">CI(지속적인 통합) 및 CD(지속적인 배포)는 코드를 작성, 릴리스 및 배포하는 데 사용할 수 있는 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="a5872-105">Team Services 배포 tooAzure에 대 한 완전 하 고 모든 기능을 갖춘 CI/CD 자동화 도구 집합이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="a5872-106">Jenkins는 널리 사용되고 있는 타사 CI/CD 서버 기반 도구이며, 마찬가지로 CI/CD 자동화 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="a5872-107">모두 함께 toocustomize를 사용할 수 있습니다 어떻게 클라우드 앱 이나 서비스 발휘 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="a5872-108">이 자습서를 사용 하 여 Jenkins toobuild는 **Node.js 웹 응용 프로그램**, 및 Visual Studio Team Services toodeploy 것 tooa [배포 그룹](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Linux 가상 컴퓨터를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="a5872-109">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5872-110">Jenkins에서 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="a5872-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="a5872-111">Team Services와 통합되도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="a5872-112">Azure 가상 컴퓨터 hello에 대 한 배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="a5872-113">Hello Vm을 구성 하 고 hello 앱을 배포 하는 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a5872-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a5872-114">Before you begin</span></span>

* <span data-ttu-id="a5872-115">액세스 tooa Jenkins 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="a5872-116">Jenkins 서버를 아직 만들지 않은 경우 [Jenkins 설명서](https://jenkins.io/doc/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5872-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="a5872-117">Tooyour Team Services 계정에에서 로그인 (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="a5872-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="a5872-118">[Team Services 계정은 무료](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="a5872-119">자세한 내용은 참조 [tooTeam 서비스 연결](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="a5872-120">Team Services 계정에 PAT(개인용 액세스 토큰)가 아직 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="a5872-121">Jenkins는이 정보 tooaccess Team Services 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="a5872-122">읽기 [어떻게 만드나요 개인용 액세스 토큰을 Team Services 및 TFS 용](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn 어떻게 toogenerate 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="a5872-123">Hello 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="a5872-123">Get hello sample app</span></span>

<span data-ttu-id="a5872-124">Git 리포지토리에 저장 하는 응용 프로그램 toodeploy가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="a5872-125">이 자습서에서는 [GitHub에서 제공되는 이 샘플 앱](https://github.com/azooinmyluggage/fabrikam-node)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="a5872-126">이 앱의 분기를 만들고이 자습서의 이후 단계에서 사용 하기 위해 hello 위치 (URL)을 숙지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="a5872-127">Hello 포크 확인 **공용** toosimplify tooGitHub 나중에 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="a5872-128">자세한 내용은 [Fork a repo](https://help.github.com/articles/fork-a-repo/)(리포지토리 포크) 및 [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/)(비공개 리포지토리를 공개로 설정)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5872-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="a5872-129">hello 앱을 사용 하 여 빌드된 [Yeoman](http://yeoman.io/learning/index.html); 사용 하 여 **Express**, **bower**, 및 **grunt**; 일부 있으며 **npm**종속성으로 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="a5872-130">hello 샘플 응용 프로그램 집합이 포함 되어 [Azure 리소스 관리자 템플릿을](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) 는 사용 되는 toodynamically 배포에 대 한 hello 가상 컴퓨터에서 만들 Azure입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="a5872-131">이러한 템플릿은 hello에 작업에 사용 되 [Team Services 릴리스 정의가](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="a5872-132">hello 주 템플릿은 네트워크 보안 그룹, 가상 컴퓨터 및 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="a5872-133">또한 공용 IP 주소를 할당하고 인바운드 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="a5872-134">또한 hello 배포 그룹 너무 선택 hello 컴퓨터 tooreceive hello 배포에서 사용 되는 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="a5872-135">또한 hello 샘플 Nginx를 설정 하 고 hello 앱을 배포 하는 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="a5872-136">각각의 hello 가상 컴퓨터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="a5872-137">Hello 스크립트 노드, Nginx, 및; 오후 2를 설치 하는 구체적으로, Nginx 및 오후 2; 구성합니다. hello 노드 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="a5872-138">Jenkins 플러그 인 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="a5872-139">먼저 **NodeJS**용과 **Team Services와의 통합**용 Jenkins 플러그 인을 두 개 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="a5872-140">Jenkins 계정을 열고 **Manage Jenkins**(Jenkins 관리)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="a5872-141">Hello에 **관리 Jenkins** 페이지에서 선택 **플러그 인 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="a5872-142">필터 hello 목록 toolocate hello **NodeJS** 플러그 인 및 다시 시작 하지 않아도 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Hello NodeJS 플러그 인 tooJenkins 추가](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="a5872-144">필터 hello 목록 toofind hello **Team Foundation Server** 플러그 인 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="a5872-145">이 플러그 인은 Team Foundation Server와 Team Services 둘 다에서 작동합니다. Jenkins를 다시 시작할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="a5872-146">Node.js용으로 Jenkins 빌드 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="a5872-147">Jenkins에서 새 빌드 프로젝트를 만들고 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="a5872-148">Hello에 **일반** 탭에서 빌드 프로젝트에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="a5872-149">Hello에 **소스 코드 관리** 탭에서 **Git** hello 저장소 및 응용 프로그램 코드를 포함 하는 hello 분기의 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![리포지토리 tooyour 빌드 추가](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="a5872-151">리포지토리에 public 인 경우 선택 **추가** tooconnect tooit 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="a5872-152">Hello에 **빌드 트리거** 탭에서 **폴링 SCM** hello 일정을 입력 하 고 `H/03 * * * *` toopoll hello Git 리포지토리 3 분 마다 변경에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="a5872-153">Hello에 **빌드 환경** 탭에서 **제공 노드 &amp; npm bin / 폴더 경로** 입력 `NodeJS` hello 노드 JS 설치 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="a5872-154">**npmrc file**(npmrc 파일)은 "use system default"(시스템 기본값 사용) 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="a5872-155">Hello에 **빌드** 탭을 hello 명령 입력 `npm install` tooensure 모든 종속 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="a5872-156">Team Services와 통합되도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="a5872-157">Hello에 **빌드 후 작업** 탭에 대 한 **파일 tooarchive**, 입력 `**/*` tooinclude 모든 파일.</span><span class="sxs-lookup"><span data-stu-id="a5872-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="a5872-158">에 대 한 **TFS/Team Services에서 릴리스 트리거**, 사용자의 계정 hello 전체 URL을 입력 (같은 `https://your-account-name.visualstudio.com`), 프로젝트 이름, (나중에 만들어진) hello 릴리스 정의 대 한 이름 hello 및 자격 증명 tooconnect tooyour 계정 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="a5872-159">사용자 이름 및 hello 앞에서 만든 PAT 필요.</span><span class="sxs-lookup"><span data-stu-id="a5872-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Jenkins 빌드 후 작업 구성](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="a5872-161">Hello 빌드 프로젝트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="a5872-162">Jenkins 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="a5872-163">서비스 끝점에는 Team Services tooconnect tooJenkins 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="a5872-164">열기 hello **서비스** 열기 hello Team Services의 페이지 **새 서비스 끝점** , 목록을 열고 **Jenkins**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Jenkins 끝점 추가](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="a5872-166">Toorefer toothis 연결을 사용할 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="a5872-167">Jenkins 서버 hello URL을 입력 하 고 hello 눈금 **신뢰할 수 없는 SSL 인증서를 수락** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="a5872-168">Jenkins 계정에 대 한 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="a5872-169">선택 **연결을 확인** 정보 hello toocheck 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="a5872-170">선택 **확인** toocreate hello 서비스 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="a5872-171">배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-171">Create a deployment group</span></span>

<span data-ttu-id="a5872-172">필요한는 [배포 그룹](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) 너무 hello 가상 컴퓨터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="a5872-173">열기 hello **릴리스** hello 탭 **빌드 &amp; 릴리스** 허브 다음 열기 hello **배포 그룹** 탭을 선택한 **+ 새로 만들기**.</span><span class="sxs-lookup"><span data-stu-id="a5872-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="a5872-174">Hello 배포 그룹 및 선택적 설명을 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="a5872-175">그런 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-175">Then choose **Create**.</span></span>

<span data-ttu-id="a5872-176">hello Azure 리소스 그룹 배포 작업이 만들고 hello Azure 리소스 관리자 템플릿을 사용 하 여 실행 될 때 hello Vm을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="a5872-177">Toocreate 필요 하 고 직접 hello 가상 컴퓨터를 등록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="a5872-178">릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-178">Create a release definition</span></span>

<span data-ttu-id="a5872-179">릴리스 정의 hello 프로세스 Team Services는 toodeploy hello 앱 실행을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="a5872-180">Team Services에서 toocreate hello 릴리스 정의:</span><span class="sxs-lookup"><span data-stu-id="a5872-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="a5872-181">열기 hello **릴리스** hello 탭 **빌드 &amp; 릴리스** 허브, 열기 hello  **+**  드롭 다운 릴리스 정의의 hello 목록에서 선택 하 고 hello **만들기 릴리스 정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="a5872-182">선택 hello **빈** 템플릿을 선택 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="a5872-183">Hello에 **아티팩트** 섹션에서 클릭 **아티팩트 링크** 선택 **Jenkins**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="a5872-184">Jenkins 서비스 끝점 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="a5872-185">그런 다음 hello Jenkins 소스 작업을 선택 하 고 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="a5872-186">Hello 새 릴리스 정의 선택 **작업 추가 +** 추가 **Azure 리소스 그룹 배포** 작업 toohello 기본 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="a5872-187">화살표 다음 toohello hello 드롭다운 선택 **작업 추가 +** 에 연결 하 고 배포 그룹 단계 toohello 정의 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![배포 그룹 단계 추가](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="a5872-189">Hello 작업 카탈로그에서 엽니다 hello **유틸리티** hello의 인스턴스를 추가 하 고 섹션 **셸 스크립트** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="a5872-190">hello 매개 변수 템플릿 hello Azure 리소스 그룹 배포 작업에 사용 된 hello 관리자 사용 되는 암호 tooconnect toohello Vm을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="a5872-191">Hello 변수와 함께이 암호를 제공 **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="a5872-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="a5872-192">열기 hello **변수** 탭 및 hello **변수** 섹션을 hello 이름 입력 `adminpassword`합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="a5872-193">Hello 관리자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="a5872-194">Hello "자물쇠" 아이콘 다음 toohello 값 텍스트 상자에 붙여넣습니다 tooprotect hello 암호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="a5872-195">Hello Azure 리소스 그룹 배포 태스크 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="a5872-196">hello **Azure 리소스 그룹 배포** 작업은 사용 되는 toocreate hello 배포 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="a5872-197">다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-197">Configure it as follows:</span></span>

* <span data-ttu-id="a5872-198">**Azure 구독:** hello 목록 아래에서 연결을 선택 **사용할 수 있는 Azure 서비스 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="a5872-199">연결이 없는 나타나지 **관리**선택, **새 서비스 끝점** 다음 **Azure 리소스 관리자**, hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="a5872-200">새로 고침 hello tooyour 릴리스 정의 반환 **AzureRM 구독** 목록과 만든 선택 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="a5872-201">**리소스 그룹**: 이전에 만든 hello 리소스 그룹의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="a5872-202">**위치**: hello 배포에 대 한 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-202">**Location**: Select a region for hello deployment.</span></span>

  ![새 리소스 그룹 만들기](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="a5872-204">**템플릿 위치**: `URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="a5872-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="a5872-205">**템플릿 링크**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="a5872-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="a5872-206">**템플릿 매개 변수 링크**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="a5872-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="a5872-207">**템플릿 매개 변수 재정의**: hello 목록이 재정의 값, 예: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="a5872-208">{자리 표시자} hello에 대 한 고유한 특정 값을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="a5872-209">**필수 구성 요소 사용**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="a5872-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="a5872-210">**TFS/VSTS 끝점**: 선택 **추가** hello "새 Team Foundation Server 팀/서비스 연결 추가" 대화 상자에서 선택 및 **토큰 기반 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="a5872-211">Hello 연결의 이름 및 팀 프로젝트의 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="a5872-212">그런 다음 생성 하 고 입력 한 [개인 액세스 토큰 (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello 연결 tooyour 팀 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![개인용 액세스 토큰 만들기](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="a5872-214">**팀 프로젝트**: 현재 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="a5872-215">**배포 그룹**: 입력 hello에 사용한 것과 동일한 배포 그룹 이름을 hello **리소스 그룹** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="a5872-216">hello Azure 리소스 그룹 배포 작업에 대 한 기본 설정을 hello toocreate 또는 리소스 및 toodo 하므로 증분 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="a5872-217">hello 작업 hello Vm hello 처음으로 실행 하 고 이후에 업데이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="a5872-218">Hello 셸 스크립트 태스크 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="a5872-219">hello **셸 스크립트** 작업 항목은 각 서버 tooinstall Node.js 및 시작 hello 앱에 스크립트 toorun에 사용 되는 tooprovide hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="a5872-220">다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-220">Configure it as follows:</span></span>

* <span data-ttu-id="a5872-221">**스크립트 경로**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="a5872-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="a5872-222">**작업 디렉터리 지정**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="a5872-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="a5872-223">**작업 디렉터리**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="a5872-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="a5872-224">이름을 바꾸고 hello 릴리스 정의 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="a5872-225">Hello hello 릴리스 정의 toohello 이름에 지정 된 이름을 편집 하는 **빌드 후 작업** hello Jenkins 빌드를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="a5872-226">Jenkins는 hello 소스 아티팩트를 업데이트할 때이 이름을 toobe 수 tootrigger 새 릴리스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="a5872-227">필요에 따라 hello 이름을 클릭 하 여 hello 환경의 hello 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="a5872-228">**저장**과 **확인**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="a5872-229">수동 배포 시작</span><span class="sxs-lookup"><span data-stu-id="a5872-229">Start a manual deployment</span></span>

1. <span data-ttu-id="a5872-230">**+ 릴리스**와 **릴리스 만들기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="a5872-231">Hello 빌드를 완료 하셨습니까 hello 강조 표시 된 드롭 다운 목록에서 선택 하 고 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="a5872-232">Hello 팝업 메시지의 hello 릴리스 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="a5872-233">예를 들어 "**Release-1** 릴리스를 만들었습니다."를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="a5872-234">열기 hello **로그** toowatch hello 릴리스 콘솔 출력을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="a5872-235">브라우저를 열고 hello URL tooyour 배포 그룹을 추가한 hello 서버 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="a5872-236">예를 들어 `http://{your-server-ip-address}`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="a5872-237">CI/CD 배포 시작</span><span class="sxs-lookup"><span data-stu-id="a5872-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="a5872-238">Hello에 정의 해제, hello의 선택을 취소 **Enabled** hello 확인란을 선택 **제어 옵션** hello Azure 리소스 그룹 배포 작업에 대 한 hello 설정의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="a5872-239">이후 배포 toohello 기존 배포 그룹에 대 한 불필요 toore-이 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="a5872-240">Toohello 소스 Git 리포지토리를 이동 하 고 hello의 hello 내용을 수정 **h1** hello 파일의 제목 [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="a5872-241">변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-241">Commit your change.</span></span>

1. <span data-ttu-id="a5872-242">몇 분 후 hello에서 만든 새 릴리스 나타납니다 **릴리스** Team Services 또는 TFS의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="a5872-243">Hello 릴리스 toosee hello 배포 수행을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="a5872-244">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5872-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5872-245">Next Steps</span></span>

<span data-ttu-id="a5872-246">이 자습서에서는 Jenkins 빌드 및 릴리스에 대 한 Team Services를 사용 하는 응용 프로그램 tooAzure의 hello 배포를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="a5872-247">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5872-248">Jenkins에서 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="a5872-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="a5872-249">Team Services와 통합되도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="a5872-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="a5872-250">Azure 가상 컴퓨터 hello에 대 한 배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="a5872-251">Hello Vm을 구성 하 고 hello 앱을 배포 하는 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="a5872-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="a5872-252">다음 자습서 toolearn toohello toodeploy (Linux, Apache, MySQL 및 PHP) LAMP 스택 하는 방법에 대 한 자세한 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5872-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5872-253">LAMP 스택 배포</span><span class="sxs-lookup"><span data-stu-id="a5872-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)