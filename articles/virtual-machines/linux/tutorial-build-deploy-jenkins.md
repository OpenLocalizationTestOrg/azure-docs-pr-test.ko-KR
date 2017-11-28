---
title: "Team Services를 사용하여 Jenkins에서 Azure VM으로의 CI/CD 설정 | Microsoft Docs"
description: "Jenkins를 사용하여 Visual Studio Team Services(VSTS) 또는 Microsoft Team Foundation Server(TFS)의 Release Management에서 Azure VM으로의 Node.js 앱 CI(지속적인 통합) 및 CD(지속적인 배포)를 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="481b4-103">Jenkins 및 Team Services를 사용하여 Linux VM에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="481b4-103">Deploy your app to Linux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="481b4-104">CI(지속적인 통합) 및 CD(지속적인 배포)는 코드를 작성, 릴리스 및 배포하는 데 사용할 수 있는 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="481b4-105">Team Services는 Azure로의 배포에 필요한 모든 기능을 갖춘 완벽한 CI/CD 자동화 도구 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment to Azure.</span></span> <span data-ttu-id="481b4-106">Jenkins는 널리 사용되고 있는 타사 CI/CD 서버 기반 도구이며, 마찬가지로 CI/CD 자동화 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="481b4-107">Team Services와 Jenkins를 함께 사용하여 클라우드 앱이나 서비스를 제공하는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-107">You can use both together to customize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="481b4-108">이 자습서에서는 Jenkins를 사용하여 **Node.js 웹앱**을 빌드하고, Visual Studio Team Services를 사용하여 이 웹앱을 Linux 가상 컴퓨터가 포함된 [배포 그룹](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-108">In this tutorial, you use Jenkins to build a **Node.js web app**, and Visual Studio Team Services to deploy it to a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="481b4-109">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="481b4-110">Jenkins에서 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="481b4-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="481b4-111">Team Services와 통합되도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="481b4-112">Azure 가상 컴퓨터용 배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-112">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="481b4-113">VM을 구성하고 앱을 배포하는 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-113">Create a release definition that configures the VMs and deploys the app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="481b4-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="481b4-114">Before you begin</span></span>

* <span data-ttu-id="481b4-115">Jenkins 계정에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-115">You need access to a Jenkins account.</span></span> <span data-ttu-id="481b4-116">Jenkins 서버를 아직 만들지 않은 경우 [Jenkins 설명서](https://jenkins.io/doc/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="481b4-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="481b4-117">Team Services 계정(`https://{youraccount}.visualstudio.com`)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-117">Sign in to your Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="481b4-118">[Team Services 계정은 무료](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="481b4-119">자세한 내용은 [Team Services에 연결](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="481b4-119">For more information, see [Connect to Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="481b4-120">Team Services 계정에 PAT(개인용 액세스 토큰)가 아직 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="481b4-121">이 정보는 Jenkins가 Team Services 계정에 액세스하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-121">Jenkins requires this information to access your Team Services account.</span></span>
  <span data-ttu-id="481b4-122">PAT를 만드는 방법을 알아보려면 [Team Services 및 TFS용으로 개인용 액세스 토큰(PAT)을 만드는 방법](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)(영문)의 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="481b4-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to learn how to generate one.</span></span>

## <a name="get-the-sample-app"></a><span data-ttu-id="481b4-123">샘플 앱 가져오기</span><span class="sxs-lookup"><span data-stu-id="481b4-123">Get the sample app</span></span>

<span data-ttu-id="481b4-124">Git 리포지토리에 저장되어 있는 앱을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-124">You need an app to deploy stored in a Git repository.</span></span>
<span data-ttu-id="481b4-125">이 자습서에서는 [GitHub에서 제공되는 이 샘플 앱](https://github.com/azooinmyluggage/fabrikam-node)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="481b4-126">이 앱의 포크를 만든 다음, 이 자습서의 이후 단계에서 사용할 수 있도록 해당 위치(URL)를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-126">Create a fork of this app and take note of the location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="481b4-127">나중에 GitHub에 쉽게 연결할 수 있도록 이 포크를 **공개**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-127">Make the fork **public** to simplify connecting to GitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="481b4-128">자세한 내용은 [Fork a repo](https://help.github.com/articles/fork-a-repo/)(리포지토리 포크) 및 [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/)(비공개 리포지토리를 공개로 설정)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="481b4-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="481b4-129">[Yeoman](http://yeoman.io/learning/index.html)을 사용하여 빌드된 이 앱은 **Express**, **bower**, **grunt**를 사용하며 몇몇 **npm** 패키지가 종속성으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-129">The app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="481b4-130">이 샘플 앱에는 Azure에 배포용으로 가상 컴퓨터를 동적으로 만들 때 사용되는 일련의 [Azure Resource Manager 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-130">The sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used to dynamically create the virtual machines for deployment on Azure.</span></span> <span data-ttu-id="481b4-131">이러한 템플릿은 [Team Services 릴리스 정의](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions)의 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-131">These templates are used by tasks in the [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="481b4-132">기본 템플릿에서는 네트워크 보안 그룹, 가상 컴퓨터 및 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-132">The main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="481b4-133">또한 공용 IP 주소를 할당하고 인바운드 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="481b4-134">그리고 배포를 받을 가상 컴퓨터를 선택하기 위해 배포 그룹에서 사용되는 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-134">It also adds a tag that is used by the deployment group to select the machines to receive the deployment.</span></span>
>
> <span data-ttu-id="481b4-135">샘플에는 Nginx를 설정하고 앱을 배포하는 스크립트도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-135">The sample also contains a script that sets up Nginx and deploys the app.</span></span> <span data-ttu-id="481b4-136">이 스크립트는 각 가상 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-136">It is executed on each of the virtual machines.</span></span> <span data-ttu-id="481b4-137">해당 스크립트 실행 시 Node, Nginx 및 PM2가 설치되고, Nginx 및 PM2가 구성된 다음, Node 앱이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-137">Specifically, the script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts the Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="481b4-138">Jenkins 플러그 인 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="481b4-139">먼저 **NodeJS**용과 **Team Services와의 통합**용 Jenkins 플러그 인을 두 개 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="481b4-140">Jenkins 계정을 열고 **Manage Jenkins**(Jenkins 관리)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="481b4-141">**Manage Jenkins**(Jenkins 관리) 페이지에서 **Manage Plugins**(플러그 인 관리)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-141">In the **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="481b4-142">목록을 필터링해 **NodeJS** 플러그 인을 찾아서 설치합니다. 이때 Jenkins를 다시 시작할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-142">Filter the list to locate the **NodeJS** plugin and install it without restart.</span></span>

   ![Jenkins에 NodeJS 플러그 인 추가](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="481b4-144">목록을 필터링해 **Team Foundation Server** 플러그 인을 찾아서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-144">Filter the list to find the **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="481b4-145">이 플러그 인은 Team Foundation Server와 Team Services 둘 다에서 작동합니다. Jenkins를 다시 시작할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="481b4-146">Node.js용으로 Jenkins 빌드 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="481b4-147">Jenkins에서 새 빌드 프로젝트를 만들고 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="481b4-148">**General**(일반) 탭에서 빌드 프로젝트의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-148">In the **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="481b4-149">**Source Code Management**(소스 코드 관리) 탭에서 **Git**를 선택하고, 앱 코드가 포함된 리포지토리 및 분기의 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-149">In the **Source Code Management** tab, select **Git** and enter the details of the repository and the branch containing your app code.</span></span>

   ![빌드에 리포지토리 추가](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="481b4-151">리포지토리가 공개 상태가 아닌 경우 **Add**(추가)를 선택하고 리포지토리 연결을 위한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-151">If your repository is not public, choose **Add** and provide credentials to connect to it.</span></span>

1. <span data-ttu-id="481b4-152">**Build Triggers**(빌드 트리거) 탭에서 **Poll SCM**(SCM 폴링)을 선택하고 일정 `H/03 * * * *`을 입력하여, 3분마다 Git 리포지토리에서 변경 내용을 폴링하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-152">In the **Build Triggers** tab, select **Poll SCM** and enter the schedule `H/03 * * * *` to poll the Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="481b4-153">**Build Environment**(빌드 환경) 탭에서 **Provide Node &amp; npm bin/ folder PATH**(노드 및 npm bin/ 폴더 경로 제공)을 선택하고 Node JS 설치 값으로 `NodeJS`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-153">In the **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for the Node JS Installation value.</span></span> <span data-ttu-id="481b4-154">**npmrc file**(npmrc 파일)은 "use system default"(시스템 기본값 사용) 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="481b4-155">**Build**(빌드) 탭에서 `npm install` 명령을 입력하여 모든 종속성이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-155">In the **Build** tab, enter the command `npm install` to ensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="481b4-156">Team Services와 통합되도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="481b4-157">**Post-build Actions**(빌드 후 작업) 탭의 **Files to archive**(보관할 파일)에 `**/*`를 입력하여 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-157">In the **Post-build Actions** tab, for **Files to archive**, enter `**/*` to include all files.</span></span>

1. <span data-ttu-id="481b4-158">**Trigger release in TFS/Team Services**(TFS/Team Services에서 릴리스 트리거)에서는 계정의 전체 URL(예:  `https://your-account-name.visualstudio.com`), 프로젝트 이름, 릴리스 정의의 이름(이후 단계에서 만듬) 및 계정에 연결하기 위한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-158">For **Trigger release in TFS/Team Services**, enter the full URL of your account (such as `https://your-account-name.visualstudio.com`), the project name, a name for the release definition (created later), and the credentials to connect to your account.</span></span>
   <span data-ttu-id="481b4-159">앞에서 만든 사용자 이름과 PAT가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-159">You need your user name and the PAT you created earlier.</span></span> 

   ![Jenkins 빌드 후 작업 구성](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="481b4-161">빌드 프로젝트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-161">Save the build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="481b4-162">Jenkins 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="481b4-163">서비스 끝점이 있으면 Team Services에서 Jenkins에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-163">A service endpoint allows Team Services to connect to Jenkins.</span></span>

1. <span data-ttu-id="481b4-164">Team Services에서 **서비스** 페이지를 열고 **새 서비스 끝점** 목록을 열어 **Jenkins**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-164">Open the **Services** page in Team Services, open the **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Jenkins 끝점 추가](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="481b4-166">이 연결을 참조하는 데 사용할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-166">Enter a name you will use to refer to this connection.</span></span>

1. <span data-ttu-id="481b4-167">Jenkins 서버의 URL을 입력하고 **신뢰할 수 없는 SSL 인증서 수락** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-167">Enter the URL of your Jenkins server, and tick the **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="481b4-168">Jenkins 계정의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-168">Enter the user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="481b4-169">**연결 확인**을 선택하여 정보가 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-169">Choose **Verify connection** to check that the information is correct.</span></span>

1. <span data-ttu-id="481b4-170">**확인**을 선택하여 서비스 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-170">Choose **OK** to create the service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="481b4-171">배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-171">Create a deployment group</span></span>

<span data-ttu-id="481b4-172">가상 컴퓨터를 포함할 [배포 그룹](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) to  contain the virtual machines.</span></span>

1. <span data-ttu-id="481b4-173">**빌드 및 릴리스** 허브의 **릴리스** 탭을 열고, **배포 그룹** 탭을 연 다음, **+ 새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-173">Open the **Releases** tab of the **Build &amp; Release** hub, then open the **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="481b4-174">배포 그룹의 이름을 입력하고 원하는 경우 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-174">Enter a name for the deployment group, and an optional description.</span></span>
   <span data-ttu-id="481b4-175">그런 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-175">Then choose **Create**.</span></span>

<span data-ttu-id="481b4-176">Azure Resource Manager 템플릿을 사용하여 Azure 리소스 그룹 배포 작업을 실행하면 VM이 생성되어 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-176">The Azure Resource Group Deployment task creates and registers the VMs when it runs using the Azure Resource Manager template.</span></span>
<span data-ttu-id="481b4-177">따라서 가상 컴퓨터를 직접 만들어서 등록할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-177">You don't need to create and register the virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="481b4-178">릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-178">Create a release definition</span></span>

<span data-ttu-id="481b4-179">릴리스 정의는 앱을 배포하기 위해 Team Services에서 실행할 프로세스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-179">A release definition specifies the process Team Services will execute to deploy the app.</span></span>
<span data-ttu-id="481b4-180">Team Services에서 릴리스 정의를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-180">To create the release definition in Team Services:</span></span>

1. <span data-ttu-id="481b4-181">**빌드 및 릴리스** 허브의 **릴리스** 탭을 열고, 릴리스 정의 목록에서 **+** 드롭다운을 연 다음, **릴리스 정의 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-181">Open the **Releases** tab of the **Build &amp; Release** hub, open the **+** drop-down in the list of release definitions, and choose the **Create release definition**.</span></span> 

1. <span data-ttu-id="481b4-182">**비어 있는** 템플릿을 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-182">Select the **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="481b4-183">**아티팩트** 섹션에서 **아티팩트 연결**을 클릭하고 **Jenkins**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-183">In the **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="481b4-184">Jenkins 서비스 끝점 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="481b4-185">그런 다음 Jenkins 소스 작업을 선택하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-185">Then select the Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="481b4-186">새 릴리스 정의에서 **+ 작업 추가**를 선택하고 **Azure 리소스 그룹 배포** 작업을 기본 환경에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-186">In the new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task to the default environment.</span></span>

1. <span data-ttu-id="481b4-187">**+ 작업 추가** 링크 옆의 드롭다운 화살표를 선택하여 배포 그룹 단계를 정의에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-187">Choose the drop down arrow next to the **+ Add tasks** link and add a deployment group phase to the definition.</span></span>

   ![배포 그룹 단계 추가](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="481b4-189">작업 카탈로그에서 **유틸리티** 섹션을 열고 **셸 스크립트** 작업의 인스턴스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-189">In the Task catalog, open the **Utility** section and add an instance of the **Shell Script** task.</span></span>

1. <span data-ttu-id="481b4-190">Azure 리소스 그룹 배포 작업에 사용되는 매개 변수 템플릿은 VM에 연결하는 데 사용되는 관리자 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-190">The parameters template used in the Azure Resource Group Deployment task sets the admin password used to connect to the VMs.</span></span>
   <span data-ttu-id="481b4-191">이 암호는 **$(adminpassword)** 변수를 사용하여 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-191">You provide this password with the variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="481b4-192">**변수** 탭을 열고 **변수** 섹션에 이름 `adminpassword`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-192">Open the **Variables** tab and, in the **Variables** section, enter the name `adminpassword`.</span></span>

   - <span data-ttu-id="481b4-193">관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-193">Enter the administrator password.</span></span>

   - <span data-ttu-id="481b4-194">암호를 보호하려면 값 텍스트 상자 옆의 "자물쇠" 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-194">Choose the "padlock" icon next to the value textbox to protect the password.</span></span> 

## <a name="configure-the-azure-resource-group-deployment-task"></a><span data-ttu-id="481b4-195">Azure 리소스 그룹 배포 작업의 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-195">Configure the Azure Resource Group Deployment task</span></span>

<span data-ttu-id="481b4-196">**Azure 리소스 그룹 배포** 작업은 배포 그룹을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-196">The **Azure Resource Group Deployment** task is used to create the deployment group.</span></span> <span data-ttu-id="481b4-197">다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-197">Configure it as follows:</span></span>

* <span data-ttu-id="481b4-198">**Azure 구독:** **사용 가능한 Azure 서비스 연결** 아래의 목록에서 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-198">**Azure Subscription:** Select a connection from the list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="481b4-199">연결이 표시되지 않으면 **관리**, **새 서비스 끝점**, **Azure Resource Manager**를 차례로 선택하고 표시되는 메시지를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow the prompts.</span></span>
  <span data-ttu-id="481b4-200">릴리스 정의로 돌아와 **AzureRM 구독** 목록을 새로 고친 다음, 작성한 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-200">Return to your release definition, refresh the **AzureRM Subscription** list, and select the connection you created.</span></span>

* <span data-ttu-id="481b4-201">**리소스 그룹**: 이전에 만든 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-201">**Resource group**: Enter a name of the resource group you created earlier.</span></span>

* <span data-ttu-id="481b4-202">**위치**: 배포의 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-202">**Location**: Select a region for the deployment.</span></span>

  ![새 리소스 그룹 만들기](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="481b4-204">**템플릿 위치**: `URL of the file`</span><span class="sxs-lookup"><span data-stu-id="481b4-204">**Template location**: `URL of the file`</span></span>

* <span data-ttu-id="481b4-205">**템플릿 링크**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="481b4-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="481b4-206">**템플릿 매개 변수 링크**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="481b4-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="481b4-207">**템플릿 매개 변수 재정의**: 재정의 값의 목록입니다. 예를 들면 다음과 같습니다. `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`</span><span class="sxs-lookup"><span data-stu-id="481b4-207">**Override template parameters**: A list of the override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="481b4-208">{자리 표시자}에는 실제로 사용할 값을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-208">Insert your own specific values for the {placeholders}.</span></span> 

* <span data-ttu-id="481b4-209">**필수 구성 요소 사용**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="481b4-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="481b4-210">**TFS/VSTS 끝점**: **추가**를 선택하고, "새 Team Foundation Server/Team Services 연결 추가" 대화 상자에서 **토큰 기반 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-210">**TFS/VSTS endpoint**: Choose **Add** and, in the "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="481b4-211">연결의 이름 및 팀 프로젝트의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-211">Enter a name of the connection and the URL of your team project.</span></span> <span data-ttu-id="481b4-212">그런 다음 팀 프로젝트에 대한 연결을 인증하기 위한 [PAT(개인용 액세스 토큰)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)를 생성하여 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to authenticate the connection to your team project.</span></span>

  ![개인용 액세스 토큰 만들기](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="481b4-214">**팀 프로젝트**: 현재 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="481b4-215">**배포 그룹**: **리소스 그룹** 매개 변수에 사용한 것과 같은 배포 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-215">**Deployment Group**: Enter the same deployment group name as you used for the **Resource group** parameter.</span></span>

<span data-ttu-id="481b4-216">Azure 리소스 그룹 배포 작업의 기본 설정에서 리소스는 단계적으로 생성되고 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-216">The default settings for the Azure Resource Group Deployment task are to create or update a resource, and to do so incrementally.</span></span> <span data-ttu-id="481b4-217">이 작업을 처음 실행하면 VM이 생성되며, 그 이후에는 단순히 VM이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-217">The task creates the VMs the first time it runs, and subsequently just update them.</span></span>

## <a name="configure-the-shell-script-task"></a><span data-ttu-id="481b4-218">셸 스크립트 작업 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-218">Configure the Shell Script task</span></span>

<span data-ttu-id="481b4-219">**셸 스크립트** 작업은 Node.js를 설치하고 앱을 시작하기 위해 각 서버에서 실행할 스크립트의 구성을 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-219">The **Shell Script** task is used to provide the configuration for a script to run on each server to install Node.js and start the app.</span></span> <span data-ttu-id="481b4-220">다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-220">Configure it as follows:</span></span>

* <span data-ttu-id="481b4-221">**스크립트 경로**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="481b4-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="481b4-222">**작업 디렉터리 지정**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="481b4-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="481b4-223">**작업 디렉터리**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="481b4-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-the-release-definition"></a><span data-ttu-id="481b4-224">릴리스 정의 이름 바꾸기 및 저장</span><span class="sxs-lookup"><span data-stu-id="481b4-224">Rename and save the release definition</span></span>

1. <span data-ttu-id="481b4-225">릴리스 정의의 이름을 Jenkins에서 빌드의 **빌드 후 작업** 탭에 지정한 이름으로 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-225">Edit the name of the release definition to the name you specified in the **Post-build Actions** tab of the build in Jenkins.</span></span> <span data-ttu-id="481b4-226">소스 아티팩트를 업데이트할 때 Jenkins가 새 릴리스를 트리거하려면 이 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-226">Jenkins requires this name to be able to trigger a new release when the source artifacts are updated.</span></span>

1. <span data-ttu-id="481b4-227">(선택 사항) 환경 이름을 변경하려면 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-227">Optionally, change the name of the environment by clicking on the name.</span></span> 

1. <span data-ttu-id="481b4-228">**저장**과 **확인**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="481b4-229">수동 배포 시작</span><span class="sxs-lookup"><span data-stu-id="481b4-229">Start a manual deployment</span></span>

1. <span data-ttu-id="481b4-230">**+ 릴리스**와 **릴리스 만들기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="481b4-231">강조 표시된 드롭다운 목록에서 완성한 빌드를 선택하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-231">Select the build you completed in the highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="481b4-232">팝업 메시지에서 릴리스 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-232">Choose the release link in the popup message.</span></span> <span data-ttu-id="481b4-233">예를 들어 "**Release-1** 릴리스를 만들었습니다."를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="481b4-234">**로그** 탭을 열어 릴리스 콘솔 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-234">Open the **Logs** tab to watch the release console output.</span></span>

1. <span data-ttu-id="481b4-235">브라우저에서 배포 그룹에 추가한 서버 중 하나의 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-235">In your browser, open the URL of one of the servers you added to your deployment group.</span></span> <span data-ttu-id="481b4-236">예를 들어 `http://{your-server-ip-address}`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="481b4-237">CI/CD 배포 시작</span><span class="sxs-lookup"><span data-stu-id="481b4-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="481b4-238">릴리스 정의에서 Azure 리소스 그룹 배포 작업에 대한 설정의 **제어 옵션** 섹션에 있는 **사용** 확인란 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-238">In the release definition, uncheck the **Enabled** checkbox in the **Control Options** section of the settings for the Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="481b4-239">기존 배포 그룹에 추가로 배포하는 경우에는 이 작업을 다시 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-239">For future deployments to the existing deployment group, you do not need to re-execute this task.</span></span>

1. <span data-ttu-id="481b4-240">소스 Git 리포지토리로 이동하여 [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade) 파일의 **h1** 제목 내용을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-240">Go to the source Git repository and modify the contents of the **h1** heading in the file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="481b4-241">변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-241">Commit your change.</span></span>

1. <span data-ttu-id="481b4-242">몇 분이 지나면 Team Services 또는 TFS의 **릴리스** 페이지에서 새 릴리스가 만들어진 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-242">After a few minutes, you will see a new release created in the **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="481b4-243">릴리스를 열어 배포가 진행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-243">Open the release to see the deployment taking place.</span></span> <span data-ttu-id="481b4-244">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="481b4-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="481b4-245">Next Steps</span></span>

<span data-ttu-id="481b4-246">이 자습서에서는 Team Services와 Jenkins 빌드를 사용하여 릴리스용 앱을 Azure에 배포하는 과정을 자동화했습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-246">In this tutorial, you automated the deployment of an app to Azure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="481b4-247">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="481b4-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="481b4-248">Jenkins에서 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="481b4-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="481b4-249">Team Services와 통합되도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="481b4-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="481b4-250">Azure 가상 컴퓨터용 배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-250">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="481b4-251">VM을 구성하고 앱을 배포하는 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="481b4-251">Create a release definition that configures the VMs and deploys the app</span></span>

<span data-ttu-id="481b4-252">LAMP(Linux, Apache, MySQL 및 PHP) 스택을 배포하는 방법에 대한 자세한 내용을 보려면 다음 자습서로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="481b4-252">Advance to the next tutorial to learn more about how to deploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="481b4-253">LAMP 스택 배포</span><span class="sxs-lookup"><span data-stu-id="481b4-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)