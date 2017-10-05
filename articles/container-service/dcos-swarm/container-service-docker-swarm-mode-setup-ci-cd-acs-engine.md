---
title: "Azure Container Service Engine 및 Swarm Mode를 사용한 CI/CD | Microsoft Docs"
description: "Docker Swarm Mode, Azure Container Registry Engine 및 Visual Studio Team Services와 Azure Container Service를 사용하여 다중 컨테이너 .NET Core 응용 프로그램 연속 배달"
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
ms.openlocfilehash: 2c0e5fe4f60738fcc1aa67a78674e6f3c62e5628
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="9f709-104">Visual Studio Team Services를 사용하여 ACS Engine 및 Docker Swarm Mode를 포함한 Azure Container Service에 있는 다중 컨테이너 응용 프로그램을 배포하는 전체 CI/CD 파이프라인</span><span class="sxs-lookup"><span data-stu-id="9f709-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="9f709-105">*이 문서는 [Visual Studio Team Services를 사용하여 Docker Swarm을 포함한 Azure Container Service에 있는 다중 컨테이너 응용 프로그램을 배포하는 전체 CI/CD 파이프라인](container-service-docker-swarm-setup-ci-cd.md) 설명서를 토대로 작성되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="9f709-105">*This article is based on [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="9f709-106">요즘 클라우드를 위한 최신 응용 프로그램을 개발할 때 어려운 문제 중 하나는 이러한 응용 프로그램을 지속적으로 전달할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-106">Nowadays, One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="9f709-107">이 문서에서는 다음을 사용하여 전체 CI/CD(지속적인 통합 및 배포) 파이프라인을 구현하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-107">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="9f709-108">Docker Swarm Mode의 Azure Container Service Engine</span><span class="sxs-lookup"><span data-stu-id="9f709-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="9f709-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="9f709-109">Azure Container Registry</span></span>
* <span data-ttu-id="9f709-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9f709-110">Visual Studio Team Services</span></span>

<span data-ttu-id="9f709-111">이 문서는 간단한 응용 프로그램을 기반으로 [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)에서 사용할 수 있으며 ASP.NET Core를 사용하여 전개됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="9f709-112">응용 프로그램은 세 개의 웹 API 및 하나의 웹 프론트 엔드라는 네 개의 다른 서비스로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-112">The application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="9f709-114">Visual Studio Team Services를 사용하여 Docker Swarm Mode 클러스터에서 이 응용 프로그램을 지속적으로 제공하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-114">The objective is to deliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="9f709-115">다음 그림에서는 이 연속 배달 파이프라인을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-115">The following figure details this continuous delivery pipeline:</span></span>

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="9f709-117">여기에서는 단계에 대해 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-117">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="9f709-118">코드 변경 내용을 소스 코드 리포지토리로 커밋합니다(여기에서는 GitHub).</span><span class="sxs-lookup"><span data-stu-id="9f709-118">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="9f709-119">GitHub은 Visual Studio Team Services에서 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="9f709-120">Visual Studio Team Services는 최신 버전의 원본을 가져오고 응용 프로그램을 작성하는 모든 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-120">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="9f709-121">Visual Studio Team Services는 Azure 컨테이너 레지스트리 서비스를 사용하여 만든 Docker 레지스트리에 이미지를 각각 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-121">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="9f709-122">Visual Studio Team Services는 새 릴리스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="9f709-123">릴리스는 Azure Container Service 클러스터 노드에서 SSH를 사용하는 마스터 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-123">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="9f709-124">클러스터의 Docker Swarm Mode는 이미지의 최신 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-124">Docker Swarm Mode on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="9f709-125">Docker Stack을 사용하여 새 버전의 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-125">The new version of the application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9f709-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9f709-126">Prerequisites</span></span>

<span data-ttu-id="9f709-127">이 자습서를 시작하기 전에 다음 작업을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-127">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="9f709-128">ACS Engine을 사용하여 Azure Container Service에서 Swarm Mode 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9f709-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="9f709-129">Azure 컨테이너 서비스에서 Swarm 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="9f709-129">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="9f709-130">Azure 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="9f709-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="9f709-131">Visual Studio Team Services 계정 및 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9f709-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="9f709-132">GitHub 계정에 GitHub 리포지토리 포크</span><span class="sxs-lookup"><span data-stu-id="9f709-132">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="9f709-133">Azure Container Service의 Docker Swarm Orchestrator는 레거시 독립 실행형 Swarm을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-133">The Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="9f709-134">현재 통합 [Swarm 모드](https://docs.docker.com/engine/swarm/)(Docker 1.12 이상)는 Azure Container Service에서 지원되는 Orchestrator가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-134">Currently, the integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="9f709-135">이러한 이유로 [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), 커뮤니티 제공 [빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/) 또는 [Azure Marketplace](https://azuremarketplace.microsoft.com)의 Docker 솔루션을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in the [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="9f709-136">1단계: Visual Studio Team Services 계정 구성</span><span class="sxs-lookup"><span data-stu-id="9f709-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="9f709-137">이 섹션에서는 사용자의 Visual Studio Team Services 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="9f709-138">VSTS 서비스 끝점을 구성하려면 Visual Studio Team Services 프로젝트의 도구 모음에서 **설정** 아이콘을 클릭하고 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-138">To configure VSTS Services Endpoints, in your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

![서비스 끝점 열기](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="9f709-140">Visual Studio Team Services 및 Azure 계정 연결</span><span class="sxs-lookup"><span data-stu-id="9f709-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="9f709-141">VSTS 프로젝트와 Azure 계정 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="9f709-142">왼쪽에서 **새 서비스 끝점** > **Azure Resource Manager**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-142">On the left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="9f709-143">Azure 계정을 사용하도록 VSTS를 인증하려면 **구독**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-143">To authorize VSTS to work with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - Azure 인증](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="9f709-145">Visual Studio Team Services 및 GitHub 연결</span><span class="sxs-lookup"><span data-stu-id="9f709-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="9f709-146">VSTS 프로젝트와 GitHub 계정 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="9f709-147">왼쪽에서 **새 서비스 끝점** > **GitHub**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-147">On the left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="9f709-148">VSTS를 인증하여 GitHub 계정으로 작업하려면 **인증**을 클릭하고 열린 창에서 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-148">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio Team Services - GitHub 인증](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-to-your-azure-container-service-cluster"></a><span data-ttu-id="9f709-150">Azure Container Service 클러스터에 VSTS 연결</span><span class="sxs-lookup"><span data-stu-id="9f709-150">Connect VSTS to your Azure Container Service cluster</span></span>

<span data-ttu-id="9f709-151">CI/CD 파이프라인에 도달하기 전에 Azure의 Docker Swarm 클러스터에 대한 외부 연결을 구성하는 마지막 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-151">The last steps before getting into the CI/CD pipeline are to configure external connections to your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="9f709-152">Docker Swarm 클러스터의 경우 **SSH** 형식의 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-152">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="9f709-153">그런 다음 Swarm 클러스터(마스터 노드)의 SSH 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-153">Then enter the SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="9f709-155">이제 모든 구성을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-155">All the configuration is done now.</span></span> <span data-ttu-id="9f709-156">다음 단계에서는 Docker Swarm 클러스터에 응용 프로그램을 빌드하고 배포하는 CI/CD 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-156">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="9f709-157">2단계: 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="9f709-157">Step 2: Create the build definition</span></span>

<span data-ttu-id="9f709-158">이 단계에서는 VSTS 프로젝트의 빌드 정의를 설정하고 사용자 컨테이너 이미지에 대한 빌드 워크플로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-158">In this step, you set up a build definition for your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="9f709-159">초기 정의 설정</span><span class="sxs-lookup"><span data-stu-id="9f709-159">Initial definition setup</span></span>

1. <span data-ttu-id="9f709-160">빌드 정의를 만들려면 Visual Studio Team Services 프로젝트에 연결하고 **빌드 및 릴리스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-160">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="9f709-161">**빌드 정의** 섹션에서 **+ 새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-161">In the **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - 새 빌드 정의](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="9f709-163">**시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-163">Select the **Empty process**.</span></span>

    ![Visual Studio Team Services - 새 빈 빌드 정의](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="9f709-165">그런 후 **변수** 탭을 클릭하고 두 개의 새로운 변수 **RegistryURL** 및 **AgentURL**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-165">Then, click the **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="9f709-166">레지스트리 및 클러스터 에이전트 DNS 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-166">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - 빌드 변수 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="9f709-168">**빌드 정의** 페이지에서 **트리거** 탭을 열고 필수 구성 요소에서 만든 MyShop 프로젝트 포크와의 연속 통합을 사용하도록 빌드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-168">On the **Build Definitions** page, open the **Triggers** tab and configure the build to use continuous integration with the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="9f709-169">그런 다음 **일괄 처리 변경 사항**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="9f709-170">*docker-linux*를 **분기 사양**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-170">Make sure that you select *docker-linux* as the **Branch specification**.</span></span>

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="9f709-172">마지막으로 **옵션** 탭을 클릭하고 기본 에이전트 큐를 **Hosted Linux Preview**로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-172">Finally, click the **Options** tab and configure the Default agent queue to **Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - 호스트 에이전트 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="9f709-174">빌드 워크플로 정의</span><span class="sxs-lookup"><span data-stu-id="9f709-174">Define the build workflow</span></span>
<span data-ttu-id="9f709-175">다음 단계에서는 빌드 워크플로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-175">The next steps define the build workflow.</span></span> <span data-ttu-id="9f709-176">먼저 코드의 소스를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-176">First, you need to configure the source of the code.</span></span> <span data-ttu-id="9f709-177">이렇게 하려면 **GitHub**, **리포지토리** 및 **분기**(docker-linux)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-177">To do it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - 코드 소스 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="9f709-179">*MyShop* 응용 프로그램에 대해 빌드되는 5개의 컨테이너 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-179">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="9f709-180">각 이미지는 프로젝트 폴더에 있는 Dockerfile을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-180">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="9f709-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="9f709-181">ProductsApi</span></span>
* <span data-ttu-id="9f709-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="9f709-182">Proxy</span></span>
* <span data-ttu-id="9f709-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="9f709-183">RatingsApi</span></span>
* <span data-ttu-id="9f709-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="9f709-184">RecommandationsApi</span></span>
* <span data-ttu-id="9f709-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="9f709-185">ShopFront</span></span>

<span data-ttu-id="9f709-186">각 이미지에 대한 두 가지 Docker 단계가 필요합니다. 하나는 이미지를 빌드하고 다른 하나는 Azure 컨테이너 레지스트리에서 이미지를 푸시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-186">You need two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="9f709-187">빌드 워크플로에서 단계를 추가하려면 **+ 빌드 단계 추가**를 클릭하고 **Docker**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-187">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - 빌드 단계 추가](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="9f709-189">각 이미지의 경우 `docker build` 명령을 사용하는 하나의 단계를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-189">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker 빌드](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="9f709-191">빌드 작업의 경우 **이미지 빌드** 작업인 Azure Container Registry를 선택하고 각 이미지를 정의하는 Dockerfile을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-191">For the build operation, select your Azure Container Registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="9f709-192">**작업 디렉터리**를 Dockerfile 루트 디렉터리로 설정하고, **이미지 이름**을 정의한 후 **최신 태그 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-192">Set the **Working Directory** as the Dockerfile root directory, define the **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="9f709-193">이미지 이름은 ```$(RegistryURL)/[NAME]:$(Build.BuildId)``` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-193">The Image Name has to be in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="9f709-194">**[NAME]**을 이미지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-194">Replace **[NAME]** with the image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="9f709-195">각 이미지의 경우 `docker push` 명령을 사용하는 두 번째 단계를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-195">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker 푸시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="9f709-197">푸시 작업의 경우 **이미지 푸시** 작업인 Azure 컨테이너 레지스트리를 선택하고 이전 단계에서 기본 설치되어 있는 **이미지 이름**을 입력한 후 **최신 태그 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-197">For the push operation, select your Azure container registry, the **Push an image** action, enter the **Image Name** that is built in the previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="9f709-198">5개의 이미지 각각에 대한 빌드 및 푸시 단계를 구성한 후에 빌드 워크플로에서 3개의 단계를 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-198">After you configure the build and push steps for each of the five images, add three more steps in the build workflow.</span></span>

   ![Visual Studio Team Services - 명령줄 작업 추가](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="9f709-200">bash 스크립트를 사용하여 docker-compose.yml 파일에 나오는 모든 *RegistryURL*을 RegistryURL 변수로 바꾸는 명령줄 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-200">A command-line task that uses a bash script to replace the *RegistryURL* occurrence in the docker-compose.yml file with the RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - 레지스트리 URL로 작성 파일 업데이트](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="9f709-202">bash 스크립트를 사용하여 docker-compose.yml 파일에 나오는 모든 *AgentURL*을 AgentURL 변수로 바꾸는 명령줄 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-202">A command-line task that uses a bash script to replace the *AgentURL* occurrence in the docker-compose.yml file with the AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="9f709-203">릴리스에서 사용할 수 있도록 빌드 아티팩트인 업데이트된 작성 파일을 삭제하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-203">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="9f709-204">자세한 내용은 다음과 같은 화면을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f709-204">See the following screen for details.</span></span>

         ![Visual Studio Team Services - 아티팩트 게시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - 작성 파일 게시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="9f709-207">**저장 및 큐에 넣기**를 클릭하여 빌드 정의를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-207">Click **Save & queue** to test your build definition.</span></span>

   ![Visual Studio Team Services - 저장 및 큐에 넣기](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - 새 큐](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="9f709-210">**빌드**가 올바른 경우 다음 화면이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-210">If the **Build** is correct, you have to see this screen:</span></span>

  ![Visual Studio Team Services - 빌드 성공](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="9f709-212">3단계: 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="9f709-212">Step 3: Create the release definition</span></span>

<span data-ttu-id="9f709-213">Visual Studio Team Services를 사용하면 [환경에서 릴리스를 관리](https://www.visualstudio.com/team-services/release-management/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-213">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="9f709-214">연속 배포를 설정하여 사용자의 응용 프로그램이 다른 환경(예: 개발, 테스트, 프로덕션 전 및 프로덕션)에서 원활하게 배포되고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-214">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="9f709-215">Azure Container Service Docker Swarm Mode 클러스터를 나타내는 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - ACS에 대한 릴리스](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="9f709-217">최초 릴리스 설정</span><span class="sxs-lookup"><span data-stu-id="9f709-217">Initial release setup</span></span>

1. <span data-ttu-id="9f709-218">릴리스 정의를 만들려면 **릴리스** > **+ 릴리스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-218">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="9f709-219">아티팩트 원본을 구성하려면 **아티팩트** > **아티팩트 원본 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-219">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="9f709-220">여기에서는 이전 단계에서 정의한 빌드에 이 새로운 릴리스 정의를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-220">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="9f709-221">그런 후에 docker-compose.yml 파일을 릴리스 프로세스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-221">After that, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio Team Services - 릴리스 아티팩트](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="9f709-223">릴리스 트리거를 구성하려면 **트리거**를 클릭하고 **연속 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-223">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="9f709-224">동일한 아티팩트 원본에 트리거를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-224">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="9f709-225">이 설정을 통해 빌드가 성공적으로 완료되면 새 릴리스가 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-225">This setting ensures that a new release starts when the build completes successfully.</span></span>

    ![Visual Studio Team Services - 릴리스 트리거](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="9f709-227">릴리스 변수를 구성하려면 **변수**를 클릭하고 **+변수**를 선택하여 레지스트리의 정보로 3개의 변수, 즉 **docker.username**, **docker.password** 및 **docker.registry**를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-227">To configure the release variables, click **Variables** and select **+Variable** to create three new variables with the info of the registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="9f709-228">레지스트리 및 클러스터 에이전트 DNS 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-228">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="9f709-230">이전 화면에서와 같이 docker.password에서 **잠금** 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-230">As shown on the previous screen, click the **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="9f709-231">이 설정은 암호를 제한하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-231">This setting is important to restrict the password.</span></span>
    >

### <a name="define-the-release-workflow"></a><span data-ttu-id="9f709-232">릴리스 워크플로 정의</span><span class="sxs-lookup"><span data-stu-id="9f709-232">Define the release workflow</span></span>

<span data-ttu-id="9f709-233">릴리스 워크플로는 추가한 두 가지 작업으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-233">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="9f709-234">이전에 구성한 SSH 연결을 사용하여 Docker Swarm 마스터 노드의 *배포* 폴더에 작성 파일을 안전하게 복사하도록 작업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-234">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="9f709-235">자세한 내용은 다음과 같은 화면을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f709-235">See the following screen for details.</span></span>
    
    <span data-ttu-id="9f709-236">소스 폴더: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="9f709-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - 릴리스 SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="9f709-238">bash 명령을 실행하는 두 번째 작업을 구성하여 마스터 노드에서 `docker` 및 `docker stack deploy` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-238">Configure a second task to execute a bash command to run `docker` and `docker stack deploy` commands on the master node.</span></span> <span data-ttu-id="9f709-239">자세한 내용은 다음과 같은 화면을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f709-239">See the following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - 릴리스 Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="9f709-241">마스터에서 실행되는 명령은 Docker CLI 및 Docker 작성 CLI를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-241">The command executed on the master uses the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="9f709-242">Azure Container Registry에 로그인(**변수** 탭에 정의된 세 개의 빌드 변수 사용)</span><span class="sxs-lookup"><span data-stu-id="9f709-242">Log in to the Azure container registry (it uses three build variables that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="9f709-243">Swarm 끝점을 사용하는 **DOCKER_HOST** 변수 정의(:2375)</span><span class="sxs-lookup"><span data-stu-id="9f709-243">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="9f709-244">이전 안전한 복사 작업에서 만들어지고 docker-compose.yml 파일을 포함하는 *배포* 폴더 탐색</span><span class="sxs-lookup"><span data-stu-id="9f709-244">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="9f709-245">새 이미지를 가져오고 컨테이너를 만드는 `docker stack deploy` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-245">Execute `docker stack deploy` commands that pull the new images and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="9f709-246">이전 화면에 표시된 대로 **STDERR에 실패** 확인란을 취소된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-246">As shown on the previous screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="9f709-247">이 설정을 사용하면 `docker-compose`이 표준 오류 출력에서 “컨테이너가 중지 또는 삭제됩니다.”와 같은 여러 진단 메시지를 인쇄하기 때문에 릴리스 프로세스를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-247">This setting allows us to complete the release process due to `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="9f709-248">확인란을 선택하면 모든 작업이 정상적으로 작동하는 경우에도 Visual Studio Team Services는 릴리스 중에 오류가 발생했다고 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-248">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="9f709-249">새 릴리스 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-249">Save this new release definition.</span></span>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="9f709-250">4단계: CI/CD 파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="9f709-250">Step 4: Test the CI/CD pipeline</span></span>

<span data-ttu-id="9f709-251">이제 구성했으면 이 새 CI/CD 파이프라인을 테스트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-251">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="9f709-252">테스트하는 가장 쉬운 방법은 소스 코드를 업데이트하고 GitHub 리포지토리에 변경 내용을 커밋하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-252">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="9f709-253">코드를 푸시한 몇 초 후에 새 빌드가 Visual Studio Team Services에서 실행되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-253">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="9f709-254">성공적으로 완료되면 새 릴리스가 트리거되고 Azure Container Service 클러스터에서 새 버전의 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9f709-254">Once completed successfully, a new release is triggered and deployed the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f709-255">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f709-255">Next steps</span></span>

* <span data-ttu-id="9f709-256">Visual Studio Team Services를 사용하는 CI/CD에 대한 자세한 내용은 [VSTS 빌드 개요](https://www.visualstudio.com/docs/build/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f709-256">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="9f709-257">ACS Engine에 대한 자세한 내용은 [ACS Engine GitHub 리포지토리](https://github.com/Azure/acs-engine)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f709-257">For more information about ACS Engine, see the [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="9f709-258">Docker Swarm Mode에 대한 자세한 내용은 [Docker Swarm Mode 개요](https://docs.docker.com/engine/swarm/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f709-258">For more information about Docker Swarm mode, see the [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
