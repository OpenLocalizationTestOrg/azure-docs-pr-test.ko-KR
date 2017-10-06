---
title: "Azure 컨테이너 서비스 엔진 및 Swarm 모드로 aaaCI/CD | Microsoft Docs"
description: "Azure 컨테이너 서비스 엔진을 사용 하 여 Docker Swarm 모드, Azure 컨테이너 레지스트리 및 Visual Studio Team Services toodeliver 지속적으로 다중 컨테이너.NET Core 응용 프로그램 사용"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, 컨테이너, 마이크로서비스, Swarm, Azure, Visual Studio Team Services, DevOps, ACS Engine"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="ddb2e-104">전체 CI/CD 파이프라인 toodeploy ACS 엔진 및 Docker Swarm 모드로 Visual Studio Team Services를 사용 하 여 Azure 컨테이너 서비스에서 여러 컨테이너 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ddb2e-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="ddb2e-105">*이 문서는 기준 [전체 CI/CD 파이프라인 toodeploy docker는 Docker Swarm Visual Studio Team Services를 사용 하 여 Azure 컨테이너 서비스에서 여러 컨테이너 응용 프로그램](container-service-docker-swarm-setup-ci-cd.md) 설명서*</span><span class="sxs-lookup"><span data-stu-id="ddb2e-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="ddb2e-106">오늘날에 중 하나 hello 난제 수 toodeliver hello 클라우드에 대 한 최신 응용 프로그램을 개발 중인 경우 이러한 응용 프로그램 지속적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="ddb2e-107">이 문서에서는 어떻게 tooimplement 전체 연속 통합 및 배포 (CI/CD) 파이프라인 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="ddb2e-108">Docker Swarm Mode의 Azure Container Service Engine</span><span class="sxs-lookup"><span data-stu-id="ddb2e-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="ddb2e-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ddb2e-109">Azure Container Registry</span></span>
* <span data-ttu-id="ddb2e-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ddb2e-110">Visual Studio Team Services</span></span>

<span data-ttu-id="ddb2e-111">이 문서는 간단한 응용 프로그램을 기반으로 [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)에서 사용할 수 있으며 ASP.NET Core를 사용하여 전개됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="ddb2e-112">네 개의 서로 다른 서비스로 구성 되어 있고 hello 응용 프로그램: 3 개 웹 Api 및 하나의 웹 프런트 엔드:</span><span class="sxs-lookup"><span data-stu-id="ddb2e-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="ddb2e-114">hello 목표는 toodeliver Visual Studio Team Services를 사용 하 여 Docker Swarm 모드 클러스터에서 지속적으로이 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="ddb2e-115">hello 다음이 지속적인 업데이트 파이프라인 세부 정보를 그림:</span><span class="sxs-lookup"><span data-stu-id="ddb2e-115">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="ddb2e-117">Hello 단계에 대 한 간략 한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="ddb2e-118">코드 변경 내용이 커밋된 toohello 소스 코드 리포지토리 (여기서 GitHub)</span><span class="sxs-lookup"><span data-stu-id="ddb2e-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="ddb2e-119">GitHub은 Visual Studio Team Services에서 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="ddb2e-120">Visual Studio Team Services hello hello 소스의 최신 버전을 가져오고 hello 응용 프로그램을 구성 하는 모든 hello 이미지 작성</span><span class="sxs-lookup"><span data-stu-id="ddb2e-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="ddb2e-121">Visual Studio Team Services 푸시 hello Azure 컨테이너 레지스트리 서비스를 사용 하 여 만든 각 이미지 tooa Docker 레지스트리</span><span class="sxs-lookup"><span data-stu-id="ddb2e-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="ddb2e-122">Visual Studio Team Services는 새 릴리스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="ddb2e-123">hello 릴리스 hello Azure 컨테이너 서비스 클러스터 노드에서 마스터 SSH를 사용 하 여 몇 가지 명령 실행</span><span class="sxs-lookup"><span data-stu-id="ddb2e-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="ddb2e-124">Hello 클러스터에서 docker Swarm 모드 hello hello 이미지의 최신 버전을 가져오고</span><span class="sxs-lookup"><span data-stu-id="ddb2e-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="ddb2e-125">Docker 스택을 사용 하 여 hello hello 응용 프로그램의 새 버전 배포</span><span class="sxs-lookup"><span data-stu-id="ddb2e-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ddb2e-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ddb2e-126">Prerequisites</span></span>

<span data-ttu-id="ddb2e-127">이 자습서를 시작 하기 전에 다음 작업 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="ddb2e-128">ACS Engine을 사용하여 Azure Container Service에서 Swarm Mode 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ddb2e-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="ddb2e-129">컨테이너 서비스를 Azure의 hello 웜 클러스터를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="ddb2e-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="ddb2e-130">Azure 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="ddb2e-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="ddb2e-131">Visual Studio Team Services 계정 및 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ddb2e-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="ddb2e-132">포크 hello GitHub 리포지토리 tooyour GitHub 계정</span><span class="sxs-lookup"><span data-stu-id="ddb2e-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="ddb2e-133">컨테이너 서비스를 Azure의 hello docker는 Docker Swarm orchestrator 웜 레거시 독립 실행형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="ddb2e-134">현재 hello 통합 [웜 모드](https://docs.docker.com/engine/swarm/) (Docker 1.12 및 더 높은) Azure 컨테이너 서비스에서 지원 되는 조정 자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="ddb2e-135">이러한 이유로 사용 하 여 [ACS 엔진](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), 커뮤니티 제공 [퀵 스타트 템플릿](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), 또는 hello에 Docker 솔루션 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="ddb2e-136">1단계: Visual Studio Team Services 계정 구성</span><span class="sxs-lookup"><span data-stu-id="ddb2e-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="ddb2e-137">이 섹션에서는 사용자의 Visual Studio Team Services 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="ddb2e-138">Visual Studio Team Services 프로젝트에서 tooconfigure VSTS 서비스 끝점을 클릭 하 여 hello **설정** hello 도구 모음 및 선택 아이콘 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![서비스 끝점 열기](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="ddb2e-140">Visual Studio Team Services 및 Azure 계정 연결</span><span class="sxs-lookup"><span data-stu-id="ddb2e-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="ddb2e-141">VSTS 프로젝트와 Azure 계정 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="ddb2e-142">Hello 왼쪽에서 클릭 **새 서비스 끝점** > **Azure 리소스 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="ddb2e-143">Azure 계정과 tooauthorize VSTS toowork 선택 프로그램 **구독** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - Azure 인증](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="ddb2e-145">Visual Studio Team Services 및 GitHub 연결</span><span class="sxs-lookup"><span data-stu-id="ddb2e-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="ddb2e-146">VSTS 프로젝트와 GitHub 계정 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="ddb2e-147">Hello 왼쪽에서 클릭 **새 서비스 끝점** > **GitHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="ddb2e-148">클릭 하 여 GitHub 계정과 tooauthorize VSTS toowork **Authorize** hello 창이 열리면 hello 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - GitHub 인증](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="ddb2e-150">VSTS tooyour Azure 컨테이너 서비스 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="ddb2e-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="ddb2e-151">hello CI/CD 파이프라인에 도달 하기 전에 hello 마지막 단계 tooconfigure 외부 연결 tooyour docker는 Docker Swarm Azure 클러스터에에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="ddb2e-152">Docker는 Docker Swarm 클러스터 hello에 대 한 형식의 끝점을 추가 **SSH**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="ddb2e-153">웜 클러스터 (마스터 노드)의 hello SSH 연결 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="ddb2e-155">모든 hello 구성은 이제 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-155">All hello configuration is done now.</span></span> <span data-ttu-id="ddb2e-156">Hello 다음 단계를 빌드 및 hello 응용 프로그램 toohello docker는 Docker Swarm 클러스터를 배포 하는 hello CI/CD 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="ddb2e-157">2 단계: hello 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="ddb2e-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="ddb2e-158">이 단계에서는 VSTS 프로젝트에 대 한 빌드 정의를 설정 하 고이 컨테이너 이미지에 대 한 hello 빌드 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="ddb2e-159">초기 정의 설정</span><span class="sxs-lookup"><span data-stu-id="ddb2e-159">Initial definition setup</span></span>

1. <span data-ttu-id="ddb2e-160">빌드 정의 toocreate 연결 tooyour Visual Studio Team Services 프로젝트 마우스 클릭 **빌드 및 릴리스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="ddb2e-161">Hello에 **빌드 정의** 섹션에서 클릭 **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - 새 빌드 정의](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="ddb2e-163">선택 hello **빈 프로세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services - 새 빈 빌드 정의](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="ddb2e-165">클릭 hello **변수** 탭 및 두 개의 새로운 변수를 만듭니다: **RegistryURL** 및 **AgentURL**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="ddb2e-166">레지스트리 및 클러스터 에이전트 DNS hello 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - 빌드 변수 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="ddb2e-168">Hello에 **빌드 정의** 페이지, 열기 hello **트리거** 탭 및 hello 필수 구성 요소에서 만든 hello MyShop 프로젝트의 분기 hello와 hello 빌드 toouse 연속 통합을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="ddb2e-169">그런 다음 **일괄 처리 변경 사항**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="ddb2e-170">선택 해야 *docker linux* hello로 **사양 분기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="ddb2e-172">마지막 hello를 클릭 하 여 **옵션** 탭 하 고 hello 기본 에이전트 큐를 너무 구성**Linux 미리 보기 호스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - 호스트 에이전트 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="ddb2e-174">Hello 빌드 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-174">Define hello build workflow</span></span>
<span data-ttu-id="ddb2e-175">다음 단계 hello hello 빌드 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="ddb2e-176">먼저 hello 코드의 tooconfigure hello 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="ddb2e-177">toodo 선택 **GitHub** 하였고 **리포지토리** 및 **분기** (linux docker).</span><span class="sxs-lookup"><span data-stu-id="ddb2e-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - 코드 소스 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="ddb2e-179">Hello에 대 한 컨테이너 이미지 toobuild 다섯 가지 *MyShop* 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="ddb2e-180">각 이미지 Dockerfile hello 프로젝트 폴더에 있는 hello를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="ddb2e-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="ddb2e-181">ProductsApi</span></span>
* <span data-ttu-id="ddb2e-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="ddb2e-182">Proxy</span></span>
* <span data-ttu-id="ddb2e-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="ddb2e-183">RatingsApi</span></span>
* <span data-ttu-id="ddb2e-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="ddb2e-184">RecommandationsApi</span></span>
* <span data-ttu-id="ddb2e-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="ddb2e-185">ShopFront</span></span>

<span data-ttu-id="ddb2e-186">각 이미지에 대 한 두 Docker 단계, 한 toobuild hello 이미지 및 hello Azure 컨테이너 레지스트리에 toopush hello 이미지 하나 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="ddb2e-187">hello 빌드 워크플로에서 단계 tooadd 클릭 **+ 추가 빌드 단계** 선택 **Docker**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - 빌드 단계 추가](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="ddb2e-189">각 이미지에 대 한 hello를 사용 하 여 한 번 구성 `docker build` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker 빌드](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="ddb2e-191">Hello에 대 한 빌드 작업을 선택 하면 Azure 컨테이너 레지스트리 hello **이미지 빌드** 작업과 각 이미지를 정의 하는 Dockerfile hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="ddb2e-192">집합 hello **작업 디렉터리** hello Dockerfile 루트 디렉터리로 hello 정의 **이미지 이름**을 선택 하 고 **최신 태그 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="ddb2e-193">이미지 이름 hello이이 형식에 대 한 toobe: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="ddb2e-194">대체 **[NAME]** hello 이미지 이름의:</span><span class="sxs-lookup"><span data-stu-id="ddb2e-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="ddb2e-195">각 이미지에 대 한 hello를 사용 하는 두 번째 단계를 구성 `docker push` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker 푸시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="ddb2e-197">Hello 푸시 작업에 대 한 선택 사용자 Azure 컨테이너 레지스트리에 hello **이미지 푸시** 동작을 hello 입력 **이미지 이름** hello 이전 단계를 선택에 기본 제공 되는 **최신 태그 포함** .</span><span class="sxs-lookup"><span data-stu-id="ddb2e-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="ddb2e-198">Hello 빌드를 구성한 후 및 각 hello 5 이미지에 대 한 단계 push, hello에 3 개 더 많은 단계가 빌드 워크플로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services - 명령줄 작업 추가](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="ddb2e-200">Bash 스크립트 tooreplace hello를 사용 하는 명령줄 작업 *RegistryURL* hello RegistryURL 변수로 hello docker compose.yml 파일에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - 레지스트리 URL로 작성 파일 업데이트](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="ddb2e-202">Bash 스크립트 tooreplace hello를 사용 하는 명령줄 작업 *AgentURL* hello AgentURL 변수로 hello docker compose.yml 파일에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="ddb2e-203">Hello를 삭제 하는 작업 hello 릴리스에서 사용할 수 있도록 작성 파일 빌드 아티팩트 업데이트.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="ddb2e-204">Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services - 아티팩트 게시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - 작성 파일 게시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="ddb2e-207">클릭 **저장 후 큐** tootest 빌드 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services - 저장 및 큐에 넣기](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - 새 큐](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="ddb2e-210">경우 hello **빌드** 올바른지, toosee이이 화면이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services - 빌드 성공](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="ddb2e-212">3 단계: hello 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="ddb2e-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="ddb2e-213">Visual Studio Team Services 사용 하면 너무[릴리스를 관리 하는 환경에 걸쳐](https://www.visualstudio.com/team-services/release-management/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="ddb2e-214">연속 배포 toomake 부드러운 방식으로 하거나 다른 환경 (예: 개발, 테스트, 사전 프로덕션 및 프로덕션)에서 응용 프로그램은 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="ddb2e-215">Azure Container Service Docker Swarm Mode 클러스터를 나타내는 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services-릴리스 tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="ddb2e-217">최초 릴리스 설정</span><span class="sxs-lookup"><span data-stu-id="ddb2e-217">Initial release setup</span></span>

1. <span data-ttu-id="ddb2e-218">릴리스 정의 toocreate 클릭 **릴리스** > **릴리스 +**</span><span class="sxs-lookup"><span data-stu-id="ddb2e-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="ddb2e-219">tooconfigure hello 아티팩트 소스 클릭 **아티팩트** > **아티팩트 소스 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="ddb2e-220">여기에서 hello 이전 단계에서 정의 된이 새 릴리스 정의 toohello 빌드에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="ddb2e-221">그 후 hello docker compose.yml 파일을 hello 릴리스 프로세스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - 릴리스 아티팩트](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="ddb2e-223">tooconfigure hello 릴리스 트리거를 클릭 하 여 **트리거** 선택 **연속 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="ddb2e-224">Hello에 hello 트리거 설정 같은 아티팩트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="ddb2e-225">이 설정은 새 릴리스 hello 빌드가 성공적으로 완료 될 때 시작 됨을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services - 릴리스 트리거](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="ddb2e-227">tooconfigure hello 릴리스 변수 클릭 **변수** 선택 **변수 +** toocreate hello 레지스트리 hello 정보 인 세 개의 새로운 변수: **docker.username**, **docker.password**, 및 **docker.registry**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="ddb2e-228">레지스트리 및 클러스터 에이전트 DNS hello 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="ddb2e-230">이전 hello 화면에 표시 된 것과 같이 hello 클릭 **잠금** docker.password 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="ddb2e-231">이 설정은 중요 toorestrict hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="ddb2e-232">Hello 릴리스 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-232">Define hello release workflow</span></span>

<span data-ttu-id="ddb2e-233">hello 릴리스 워크플로 추가 하는 두 가지 작업으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="ddb2e-234">작업 toosecurely 복사 hello 구성 파일 tooa 작성 *배포* hello docker는 Docker Swarm 마스터 노드를 이전에 구성한 hello SSH 연결을 사용 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="ddb2e-235">Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="ddb2e-236">소스 폴더: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="ddb2e-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - 릴리스 SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="ddb2e-238">두 번째 작업 tooexecute bash 명령 toorun 구성 `docker` 및 `docker stack deploy` hello 마스터 노드에서 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="ddb2e-239">Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - 릴리스 Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="ddb2e-241">hello 마스터에서 실행 하는 hello 명령은 Docker CLI hello 및 작업을 수행 하는 hello Docker Compose CLI toodo hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="ddb2e-242">Azure 컨테이너 레지스트리 toohello 로그인 (hello에 정의 된 세 개의 빌드 변수를 사용 하 여 **변수** 탭)</span><span class="sxs-lookup"><span data-stu-id="ddb2e-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="ddb2e-243">Hello 정의 **DOCKER_HOST** hello 웜 끝점과 변수 toowork (: 2375)</span><span class="sxs-lookup"><span data-stu-id="ddb2e-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="ddb2e-244">Toohello 이동 *배포* hello docker compose.yml 파일을 포함 하 고 hello 안전한 복사 작업을 앞에서 만든 폴더</span><span class="sxs-lookup"><span data-stu-id="ddb2e-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="ddb2e-245">실행 `docker stack deploy` hello 컨테이너를 만들고 hello 새 이미지를 끌어오도록 하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="ddb2e-246">이전 hello 화면에 표시 된 대로 둡니다 hello **STDERR에서 실패** 확인란을 선택된 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="ddb2e-247">이 설정을 통해 인해 toocomplete hello 릴리스 프로세스 너무`docker-compose` 컨테이너 중지 또는 삭제 하는 hello 표준 오류 출력에는 같은 여러 가지 진단 메시지를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="ddb2e-248">Hello 확인란을 선택 하면 Visual Studio Team Services를 보고 hello 릴리스 하는 동안 오류가 발생 했다는 코드가 정상적으로 작동 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="ddb2e-249">새 릴리스 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="ddb2e-250">4 단계: 테스트 hello CI/CD 파이프라인</span><span class="sxs-lookup"><span data-stu-id="ddb2e-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="ddb2e-251">이제 hello 구성 했으면입니다이 새로운 시간 tootest CI/CD 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="ddb2e-252">hello 가장 쉬운 방법은 tootest tooupdate hello 소스 코드 및 커밋 hello는 GitHub 리포지토리에으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="ddb2e-253">몇 초 후 hello 코드 푸시 Visual Studio Team Services에서 실행 되는 새 빌드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="ddb2e-254">성공적으로 완료 되 면 새 릴리스 트리거되고 hello hello Azure 컨테이너 서비스 클러스터에서 hello 응용 프로그램의 새 버전을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddb2e-255">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddb2e-255">Next steps</span></span>

* <span data-ttu-id="ddb2e-256">Visual Studio Team Services를 통해 CI/CD에 대 한 자세한 내용은 참조 hello [VSTS 빌드 개요](https://www.visualstudio.com/docs/build/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="ddb2e-257">ACS 엔진에 대 한 자세한 내용은 참조 hello [ACS 엔진 GitHub 리포지토리](https://github.com/Azure/acs-engine)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="ddb2e-258">Docker는 Docker Swarm 모드에 대 한 자세한 내용은 참조 hello [모드 개요 docker는 Docker Swarm](https://docs.docker.com/engine/swarm/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb2e-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
