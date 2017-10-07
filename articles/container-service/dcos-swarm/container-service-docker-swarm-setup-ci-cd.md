---
title: "Azure 컨테이너 서비스 및 웜 aaaCI/CD | Microsoft Docs"
description: "Azure 컨테이너 서비스를 사용 하 여 docker는 Docker Swarm, Azure 컨테이너 레지스트리 및 Visual Studio Team Services toodeliver 지속적으로 다중 컨테이너.NET Core 응용 프로그램 사용"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로서비스, Swarm, Azure, Visual Studio Team Services, DevOps"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="5f929-104">전체 CI/CD 파이프라인 toodeploy docker는 Docker Swarm Visual Studio Team Services를 사용 하 여 Azure 컨테이너 서비스에서 여러 컨테이너 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5f929-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="5f929-105">중 하나 hello 난제 수 toodeliver hello 클라우드에 대 한 최신 응용 프로그램을 개발 중인 경우 이러한 응용 프로그램 지속적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="5f929-106">이 문서에서는 tooimplement 전체 연속 통합 및 배포 (CI/CD) 파이프라인 Azure 컨테이너 서비스를 사용 하 여 docker는 Docker Swarm, Azure 컨테이너 레지스트리 및 Visual Studio Team Services를 구축 하는 방법에 대해 알아봅니다 및 릴리스 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="5f929-107">이 문서는 간단한 응용 프로그램을 기반으로 [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs)에서 사용할 수 있으며 ASP.NET Core를 사용하여 전개됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="5f929-108">네 개의 서로 다른 서비스로 구성 되어 있고 hello 응용 프로그램: 3 개 웹 Api 및 하나의 웹 프런트 엔드:</span><span class="sxs-lookup"><span data-stu-id="5f929-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="5f929-110">hello 목표는 toodeliver Visual Studio Team Services를 사용 하는 docker는 Docker Swarm 클러스터에서 지속적으로이 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="5f929-111">hello 다음이 지속적인 업데이트 파이프라인 세부 정보를 그림:</span><span class="sxs-lookup"><span data-stu-id="5f929-111">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="5f929-113">Hello 단계에 대 한 간략 한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="5f929-114">코드 변경 내용이 커밋된 toohello 소스 코드 리포지토리 (여기서 GitHub)</span><span class="sxs-lookup"><span data-stu-id="5f929-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="5f929-115">GitHub은 Visual Studio Team Services에서 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="5f929-116">Visual Studio Team Services hello hello 소스의 최신 버전을 가져오고 hello 응용 프로그램을 구성 하는 모든 hello 이미지 작성</span><span class="sxs-lookup"><span data-stu-id="5f929-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="5f929-117">Visual Studio Team Services 푸시 hello Azure 컨테이너 레지스트리 서비스를 사용 하 여 만든 각 이미지 tooa Docker 레지스트리</span><span class="sxs-lookup"><span data-stu-id="5f929-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="5f929-118">Visual Studio Team Services는 새 릴리스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="5f929-119">hello 릴리스 hello Azure 컨테이너 서비스 클러스터 노드에서 마스터 SSH를 사용 하 여 몇 가지 명령 실행</span><span class="sxs-lookup"><span data-stu-id="5f929-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="5f929-120">Docker 웜 hello 클러스터 끌어오는 소스 hello 최신 버전의 hello 이미지</span><span class="sxs-lookup"><span data-stu-id="5f929-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="5f929-121">Docker Compose를 사용 하 여 hello hello 응용 프로그램의 새 버전 배포</span><span class="sxs-lookup"><span data-stu-id="5f929-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5f929-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5f929-122">Prerequisites</span></span>

<span data-ttu-id="5f929-123">이 자습서를 시작 하기 전에 다음 작업 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="5f929-124">Azure 컨테이너 서비스에서 Swarm 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="5f929-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="5f929-125">컨테이너 서비스를 Azure의 hello 웜 클러스터를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="5f929-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="5f929-126">Azure 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="5f929-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="5f929-127">Visual Studio Team Services 계정 및 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5f929-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="5f929-128">포크 hello GitHub 리포지토리 tooyour GitHub 계정</span><span class="sxs-lookup"><span data-stu-id="5f929-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="5f929-129">또한 Docker를 설치한 Ubuntu 14.04 또는 16.04 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="5f929-130">이 컴퓨터를 사용 하는 hello 하는 동안 Visual Studio Team Services에서 빌드 및 릴리스 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="5f929-131">한 가지 방법은 toocreate이이 컴퓨터는 hello에서 사용할 수 있는 toouse hello 이미지 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="5f929-132">1단계: Visual Studio Team Services 계정 구성</span><span class="sxs-lookup"><span data-stu-id="5f929-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="5f929-133">이 섹션에서는 사용자의 Visual Studio Team Services 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="5f929-134">Visual Studio Team Services Linux 빌드 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="5f929-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="5f929-135">toocreate Docker 이미지와 Visual Studio Team Services에서 Azure 컨테이너 레지스트리에 이러한 이미지 빌드 푸시 tooregister Linux 에이전트를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="5f929-136">다음과 같은 설치 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-136">You have these installation options:</span></span>

* [<span data-ttu-id="5f929-137">Linux에서 에이전트 배포</span><span class="sxs-lookup"><span data-stu-id="5f929-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="5f929-138">Docker toorun hello VSTS 에이전트 사용</span><span class="sxs-lookup"><span data-stu-id="5f929-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="5f929-139">Hello Docker 통합 VSTS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="5f929-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="5f929-140">Microsoft는 빌드에 Docker가 있는 VSTS 확장 toowork를 제공 하 고 프로세스를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="5f929-141">이 확장은 hello에서 사용할 수 있는 [VSTS 마켓플레이스](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="5f929-142">클릭 **설치** tooadd이 확장 tooyour VSTS 계정:</span><span class="sxs-lookup"><span data-stu-id="5f929-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Hello Docker 통합 설치](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="5f929-144">Tooconnect tooyour VSTS 계정 자격 증명을 사용 하는 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="5f929-145">Visual Studio Team Services 및 GitHub 연결</span><span class="sxs-lookup"><span data-stu-id="5f929-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="5f929-146">VSTS 프로젝트와 GitHub 계정 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="5f929-147">Visual Studio Team Services 프로젝트를 클릭 hello **설정** hello 도구 모음 및 선택 아이콘 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - 외부 연결](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="5f929-149">Hello 왼쪽에서 클릭 **새 서비스 끝점** > **GitHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="5f929-151">클릭 하 여 GitHub 계정과 tooauthorize VSTS toowork **Authorize** hello 창이 열리면 hello 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - GitHub 인증](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="5f929-153">VSTS tooyour Azure 컨테이너 레지스트리 및 Azure 컨테이너 서비스 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="5f929-154">hello CI/CD 파이프라인에 도달 하기 전에 hello 마지막 단계는 tooconfigure 외부 연결 tooyour 컨테이너 레지스트리 및 Azure에서 docker는 Docker Swarm 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="5f929-155">Hello에 **서비스** 유형의 서비스 끝점을 추가 하는 Visual Studio Team Services 프로젝트의 설정을 **Docker 레지스트리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="5f929-156">열리면 hello 팝업에서 hello URL과 Azure 컨테이너 레지스트리 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker 레지스트리](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="5f929-158">Docker는 Docker Swarm 클러스터 hello에 대 한 형식의 끝점을 추가 **SSH**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="5f929-159">웜 클러스터의 hello SSH 연결 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="5f929-161">모든 hello 구성은 이제 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-161">All hello configuration is done now.</span></span> <span data-ttu-id="5f929-162">Hello 다음 단계를 빌드 및 hello 응용 프로그램 toohello docker는 Docker Swarm 클러스터를 배포 하는 hello CI/CD 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="5f929-163">2 단계: hello 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="5f929-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="5f929-164">이 단계에서는 VSTS 프로젝트 빌드 definitionfor를 설정 하 고이 컨테이너 이미지에 대 한 hello 빌드 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="5f929-165">초기 정의 설정</span><span class="sxs-lookup"><span data-stu-id="5f929-165">Initial definition setup</span></span>

1. <span data-ttu-id="5f929-166">빌드 정의 toocreate 연결 tooyour Visual Studio Team Services 프로젝트 마우스 클릭 **빌드 및 릴리스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="5f929-167">Hello에 **빌드 정의** 섹션에서 클릭 **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="5f929-168">선택 hello **빈** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services - 새 빌드 정의](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="5f929-170">GitHub 리포지토리 소스, 확인을 사용 하 여 hello 새 빌드를 구성 **연속 통합**, 및 select hello 에이전트 큐 Linux 에이전트를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="5f929-171">클릭 **만들기** toocreate hello 빌드 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services - 빌드 정의 만들기](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="5f929-173">Hello에 **빌드 정의** 페이지를 열면 hello **저장소** 탭 하 고 hello 필수 구성 요소에서 만든 hello MyShop 프로젝트의 빌드 toouse hello 포크 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="5f929-174">선택 해야 *acs docs* hello로 **기본 분기가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="5f929-176">Hello에 **트리거** 탭 hello 빌드 toobe 각 커밋 후 트리거를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="5f929-177">**연속 통합** 및 **Batch 변경 내용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - 빌드 트리거 구성](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="5f929-179">Hello 빌드 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-179">Define hello build workflow</span></span>
<span data-ttu-id="5f929-180">다음 단계 hello hello 빌드 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="5f929-181">Hello에 대 한 컨테이너 이미지 toobuild 다섯 가지 *MyShop* 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="5f929-182">각 이미지 Dockerfile hello 프로젝트 폴더에 있는 hello를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="5f929-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="5f929-183">ProductsApi</span></span>
* <span data-ttu-id="5f929-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="5f929-184">Proxy</span></span>
* <span data-ttu-id="5f929-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="5f929-185">RatingsApi</span></span>
* <span data-ttu-id="5f929-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="5f929-186">RecommandationsApi</span></span>
* <span data-ttu-id="5f929-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="5f929-187">ShopFront</span></span>

<span data-ttu-id="5f929-188">각 이미지에 대 한 두 Docker 단계 tooadd, 한 toobuild hello 이미지 및 hello Azure 컨테이너 레지스트리에 단일 toopush hello 이미지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="5f929-189">hello 빌드 워크플로에서 단계 tooadd 클릭 **+ 추가 빌드 단계** 선택 **Docker**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - 빌드 단계 추가](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="5f929-191">각 이미지에 대 한 hello를 사용 하 여 한 번 구성 `docker build` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker 빌드](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="5f929-193">Hello에 대 한 빌드 작업을 선택 하면 Azure 컨테이너 레지스트리 hello **이미지 빌드** 작업과 각 이미지를 정의 하는 Dockerfile hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="5f929-194">집합 hello **빌드 컨텍스트에서** Dockerfile hello로 루트 디렉터리를 하 고 hello 정의 **이미지 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="5f929-195">Hello 화면을 앞에 표시 된 것과 같이 hello 이미지 이름 hello Azure 컨테이너 레지스트리의 URI로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="5f929-196">(사용할 수 있습니다도이 예에서 hello 빌드 식별자와 같은 hello 이미지의 빌드 변수 tooparameterize hello 태그.)</span><span class="sxs-lookup"><span data-stu-id="5f929-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="5f929-197">각 이미지에 대 한 hello를 사용 하는 두 번째 단계를 구성 `docker push` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker 푸시](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="5f929-199">Hello 푸시 작업에 대 한 선택 사용자 Azure 컨테이너 레지스트리에 hello **이미지 푸시** 동작을 hello 입력 **이미지 이름** hello 이전 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="5f929-200">Hello 빌드를 구성한 후 및 각 hello 5 이미지에 대 한 단계 push, hello에 두 개 이상의 단계 빌드 워크플로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="5f929-201">a.</span><span class="sxs-lookup"><span data-stu-id="5f929-201">a.</span></span> <span data-ttu-id="5f929-202">Bash 스크립트 tooreplace hello를 사용 하는 명령줄 작업 *BuildNumber* 현재 hello로 hello docker compose.yml 파일에 나타나는 빌드 id입니다. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f929-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 작성 파일 업데이트](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="5f929-204">b.</span><span class="sxs-lookup"><span data-stu-id="5f929-204">b.</span></span> <span data-ttu-id="5f929-205">Hello를 삭제 하는 작업 hello 릴리스에서 사용할 수 있도록 작성 파일 빌드 아티팩트 업데이트.</span><span class="sxs-lookup"><span data-stu-id="5f929-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="5f929-206">Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f929-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 작성 파일 게시](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="5f929-208">**저장**을 클릭하여 빌드 정의의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="5f929-209">3 단계: hello 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="5f929-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="5f929-210">Visual Studio Team Services 사용 하면 너무[릴리스를 관리 하는 환경에 걸쳐](https://www.visualstudio.com/team-services/release-management/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="5f929-211">연속 배포 toomake 부드러운 방식으로 하거나 다른 환경 (예: 개발, 테스트, 사전 프로덕션 및 프로덕션)에서 응용 프로그램은 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="5f929-212">Azure Container Service Docker Swarm 클러스터를 나타내는 새 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services-릴리스 tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="5f929-214">최초 릴리스 설정</span><span class="sxs-lookup"><span data-stu-id="5f929-214">Initial release setup</span></span>

1. <span data-ttu-id="5f929-215">릴리스 정의 toocreate 클릭 **릴리스** > **릴리스 +**</span><span class="sxs-lookup"><span data-stu-id="5f929-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="5f929-216">tooconfigure hello 아티팩트 소스 클릭 **아티팩트** > **아티팩트 소스 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="5f929-217">여기에서 hello 이전 단계에서 정의 된이 새 릴리스 정의 toohello 빌드에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="5f929-218">이 작업을 수행 하 여 hello docker compose.yml 파일은 hello 릴리스 프로세스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - 릴리스 아티팩트](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="5f929-220">tooconfigure hello 릴리스 트리거를 클릭 하 여 **트리거** 선택 **연속 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="5f929-221">Hello에 hello 트리거 설정 같은 아티팩트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="5f929-222">이 설정은 새 릴리스 hello 빌드가 완료 되는 즉시 시작 되도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services - 릴리스 트리거](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="5f929-224">Hello 릴리스 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-224">Define hello release workflow</span></span>

<span data-ttu-id="5f929-225">hello 릴리스 워크플로 추가 하는 두 가지 작업으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="5f929-226">작업 toosecurely 복사 hello 구성 파일 tooa 작성 *배포* hello docker는 Docker Swarm 마스터 노드를 이전에 구성한 hello SSH 연결을 사용 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="5f929-227">Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f929-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 릴리스 SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="5f929-229">두 번째 작업 tooexecute bash 명령 toorun 구성 `docker` 및 `docker-compose` hello 마스터 노드에서 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="5f929-230">Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f929-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 릴리스 Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="5f929-232">hello 마스터 사용 하 여 hello Docker CLI 및 hello Docker Compose CLI toodo hello 작업 다음에 실행 된 hello 명령:</span><span class="sxs-lookup"><span data-stu-id="5f929-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="5f929-233">로그인 toohello Azure 컨테이너 레지스트리 (사용 하 여 hello에 정의 된 세 개의 빌드 variab'les **변수** 탭)</span><span class="sxs-lookup"><span data-stu-id="5f929-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="5f929-234">Hello 정의 **DOCKER_HOST** hello 웜 끝점과 변수 toowork (: 2375)</span><span class="sxs-lookup"><span data-stu-id="5f929-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="5f929-235">Toohello 이동 *배포* hello docker compose.yml 파일을 포함 하 고 hello 안전한 복사 작업을 앞에서 만든 폴더</span><span class="sxs-lookup"><span data-stu-id="5f929-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="5f929-236">실행 `docker-compose` hello 새로운 이미지를 끌어오는 명령 hello 서비스를 중지, hello 서비스 제거 및 hello 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="5f929-237">Hello 화면을 앞에 표시 된 대로 둡니다 hello **STDERR에서 실패** 확인란을 선택된 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="5f929-238">중요 한 설정 때문에 이것이 `docker-compose` 컨테이너 중지 또는 삭제 하는 hello 표준 오류 출력에는 같은 여러 가지 진단 메시지를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="5f929-239">Hello 확인란을 선택 하면 Visual Studio Team Services를 보고 hello 릴리스 하는 동안 오류가 발생 했다는 코드가 정상적으로 작동 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="5f929-240">새 릴리스 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="5f929-241">이 배포에는 hello 이전 서비스를 중지 하 고 새 hello를 실행 하기 때문에 일부 가동 중지 시간이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="5f929-242">것 입니까 가능한 tooavoid 청록색 배포를 수행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="5f929-243">4단계.</span><span class="sxs-lookup"><span data-stu-id="5f929-243">Step 4.</span></span> <span data-ttu-id="5f929-244">테스트 hello CI/CD 파이프라인</span><span class="sxs-lookup"><span data-stu-id="5f929-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="5f929-245">이제 hello 구성 했으면입니다이 새로운 시간 tootest CI/CD 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="5f929-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="5f929-246">hello 가장 쉬운 방법은 tootest tooupdate hello 소스 코드 및 커밋 hello는 GitHub 리포지토리에으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="5f929-247">몇 초 후 hello 코드 푸시 Visual Studio Team Services에서 실행 되는 새 빌드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="5f929-248">성공적으로 완료 되 면 새 릴리스 트리거됩니다 및 hello hello Azure 컨테이너 서비스 클러스터에서 hello 응용 프로그램의 새 버전을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f929-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f929-249">Next Steps</span></span>

* <span data-ttu-id="5f929-250">Visual Studio Team Services를 통해 CI/CD에 대 한 자세한 내용은 참조 hello [VSTS 빌드 개요](https://www.visualstudio.com/docs/build/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f929-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
