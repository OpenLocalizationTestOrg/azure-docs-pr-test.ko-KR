---
title: "Azure에서 클러스터를 Docker 컨테이너 aaaDeploy | Microsoft Docs"
description: "Hello Azure 포털 또는 리소스 관리자 템플릿을 사용 하 여 Azure 컨테이너 서비스의 Kubernetes, DC/OS 또는 docker는 Docker Swarm 솔루션을 배포 합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, DCOS, Swarm, Kubernetes, Azure Container Service, ACS"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="b9447-104">호스팅 솔루션 hello Azure 포털을 사용 하 여 Docker 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="b9447-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="b9447-105">Azure 컨테이너 서비스는 인기 있는 오픈 소스 컨테이너 클러스터링 및 오케스트레이션 솔루션의 신속한 배포를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="b9447-106">이 문서에서는 Azure 리소스 관리자 퀵 스타트 템플릿이나 hello Azure 포털을 사용 하 여 Azure 컨테이너 서비스 클러스터를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="b9447-107">Hello를 사용 하 여 Azure 컨테이너 서비스 클러스터를 배포할 수도 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) 또는 Azure 컨테이너 서비스 Api를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="b9447-108">배경 지식은 [Azure Container Service 소개](../container-service-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b9447-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9447-109">Prerequisites</span></span>

* <span data-ttu-id="b9447-110">**Azure 구독**: 없는 경우 지금 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="b9447-111">대규모 클러스터의 경우, 종량제 구독이나 다른 구매 옵션을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9447-112">Azure 구독 사용 현황 및 [리소스 할당량](../../azure-subscription-service-limits.md), 코어 할당량과 같은 hello 클러스터 배포의 hello 크기를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="b9447-113">할당량 증가 열기 toorequest는 [온라인 고객 지원 요청](../../azure-supportability/how-to-create-azure-support-request.md) 비용 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="b9447-114">**SSH RSA 공개 키**: hello 포털 또는 hello Azure 빠른 시작 템플릿 중 하나를 통해 배포, 있습니다 tooprovide hello 공개 키에 대 한 필요 컨테이너 서비스를 Azure 가상 컴퓨터에 대 한 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="b9447-115">toocreate SSH (보안 셸) RSA 키 참조 hello [Osx 및 Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../../virtual-machines/linux/ssh-from-windows.md) 지침.</span><span class="sxs-lookup"><span data-stu-id="b9447-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="b9447-116">**주 클라이언트 ID와 암호를 서비스** (Kubernetes만): 자세한 정보와 지침 toocreate Azure Active Directory 서비스 사용자를 참조 하십시오. [Kubernetes 클러스터에 대 한 hello 서비스 사용자에 대 한](../kubernetes/container-service-kubernetes-service-principal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="b9447-117">Hello Azure 포털을 사용 하 여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b9447-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="b9447-118">Toohello Azure 포털에에서 로그인 선택 **새로**, 검색에 대 한 Azure 마켓플레이스 hello **Azure 컨테이너 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Marketplace의 Azure Container Service](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="b9447-120">**Azure Container Service**를 클릭하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="b9447-121">Hello에 **기본 사항** 블레이드에서 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="b9447-122">**Orchestrator**: hello 컨테이너 orchestrators toodeploy hello 클러스터 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="b9447-123">**DC/OS**: DC/OS 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="b9447-124">**Swarm**: Docker Swarm 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="b9447-125">**Kubernetes**: Kubernetes 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="b9447-126">**구독**: Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="b9447-127">**리소스 그룹**: hello 배포에 대 한 새 리소스 그룹의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="b9447-128">**위치**: hello Azure 컨테이너 서비스 배포에 대 한 Azure 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="b9447-129">가용성은 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![기본 설정](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="b9447-131">클릭 **확인** 준비 tooproceed 라인인 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="b9447-132">Hello에 **구성 마스터** 블레이드에서 hello hello Linux 마스터 노드 또는 (일부 설정은 특정 tooeach orchestrator 검색) hello 클러스터의 노드에 대 한 설정을 다음 입력:</span><span class="sxs-lookup"><span data-stu-id="b9447-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="b9447-133">**마스터 DNS 이름**: hello master에 대 한 정규화 된 도메인 이름 (FQDN) hello 사용 되는 접두사 toocreate는 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="b9447-134">hello 폼의 마스터 FQDN은 hello *접두사*관리*위치*. cloudapp.azure.com 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="b9447-135">**사용자 이름**: hello 클러스터의 hello Linux 가상 컴퓨터의 각 계정에 대 한 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="b9447-136">**SSH RSA 공개 키**: hello 공개 키 toobe hello Linux 가상 컴퓨터에 대 한 인증에 사용 되는 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="b9447-137">이 키에 줄 바꿈이 없어야 하 고 hello 포함 것이 중요 `ssh-rsa` 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="b9447-138">hello `username@domain` 접미사는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="b9447-139">hello 키 해야 hello 다음과 유사할: **ssh rsa AAAAB3Nz... <>...... UcyupgH azureuser@linuxvm** 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="b9447-140">**서비스 사용자**: hello Kubernetes orchestrator를 선택한 경우 입력 Azure Active Directory **주 클라이언트 ID를 서비스** (hello appId 라고도 함) 및 **서비스보안주체클라이언트암호** (암호)입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="b9447-141">자세한 내용은 참조 [Kubernetes 클러스터에 대 한 hello 서비스 사용자에 대 한](../kubernetes/container-service-kubernetes-service-principal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="b9447-142">**Count 마스터**: hello hello 클러스터에서 마스터의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="b9447-143">**VM 진단**: 일부 orchestrators VM 진단 hello 마스터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![마스터 구성](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="b9447-145">클릭 **확인** 준비 tooproceed 라인인 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="b9447-146">Hello에 **에이전트 구성** 블레이드에서 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="b9447-147">**에이전트 개수의**: Docker 웜 및 Kubernetes이이 값은 hello hello 에이전트 크기 집합에 에이전트의 초기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="b9447-148">DC/OS hello 개인 크기 집합에 에이전트의 초기 수는.</span><span class="sxs-lookup"><span data-stu-id="b9447-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="b9447-149">또한, 사전에 지정된 수의 에이전트를 포함하는 DC/OS에 대한 공개 규모 집합이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="b9447-150">hello 수가이 공용 크기 집합의 에이전트 결정 hello 클러스터에서 마스터의 hello 번호로: 하나의 마스터에 대해 하나의 공용 에이전트가 및 세 가지 또는 5 개인 마스터에 대 한 두 명의 공용 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="b9447-151">**에이전트가 가상 컴퓨터 크기**: hello hello 에이전트가 가상 컴퓨터의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="b9447-152">**운영 체제**:이 설정은 현재 hello Kubernetes orchestrator를 선택한 경우에 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="b9447-153">Linux 배포 또는 hello 에이전트에서 Windows Server 운영 체제 toorun 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="b9447-154">이 설정은 클러스터가 Linux 또는 Windows 컨테이너 앱을 실행할 수 있을지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="b9447-155">Windows 컨테이너 지원은 Kubernetes 클러스터에 대해 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="b9447-156">DC/OS 및 Swarm 클러스터의 경우 현재 Linux 에이전트만 Azure Container Service에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="b9447-157">**에이전트 자격 증명**: hello Windows 운영 체제를 선택한 경우 입력 관리자 **사용자 이름** 및 **암호** hello 에이전트 Vm에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![에이전트 구성](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="b9447-159">클릭 **확인** 준비 tooproceed 라인인 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="b9447-160">서비스 유효성 검사가 완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-160">After service validation finishes, click **OK**.</span></span>

    ![유효성 검사](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="b9447-162">Hello 용어를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-162">Review hello terms.</span></span> <span data-ttu-id="b9447-163">toostart hello 배포 프로세스를 클릭 하 여 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="b9447-164">Toopin hello 배포 toohello Azure 포털을 설정 했으면, hello 배포 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![배포 상태](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="b9447-166">hello 배포는 몇 분 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="b9447-167">그런 다음 hello Azure 컨테이너 서비스 클러스터 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="b9447-168">빠른 시작 템플릿을 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b9447-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="b9447-169">Azure 빠른 시작 템플릿은 Azure 컨테이너 서비스의 클러스터 toodeploy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="b9447-170">hello 제공 퀵 스타트 서식 파일 수정된 tooinclude 추가 또는 고급 Azure 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="b9447-171">Azure 빠른 시작 템플릿을 사용 하 여 Azure 컨테이너 서비스 클러스터는 toocreate Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="b9447-172">없는 경우 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="b9447-173">이러한 단계 toodeploy 템플릿을 사용 하는 클러스터를 따르고 hello Azure CLI 2.0 (참조 [설치 및 설치 지침](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="b9447-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="b9447-174">Windows 시스템을 사용 하는 경우 비슷한 단계 toodeploy을 Azure PowerShell을 사용 하 여 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="b9447-175">이 섹션의 뒷부분에 나오는 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-175">See steps later in this section.</span></span> <span data-ttu-id="b9447-176">Hello 통해 서식 파일을 배포할 수도 있습니다 [포털](../../azure-resource-manager/resource-group-template-deploy-portal.md) 또는 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="b9447-177">DC/OS, docker는 Docker Swarm 또는 Kubernetes 클러스터 toodeploy GitHub에서 hello 빠른 시작 사용 가능한 템플릿 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="b9447-178">다음은 일부 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-178">A partial list follows.</span></span> <span data-ttu-id="b9447-179">hello DC/OS 및 웜 템플릿 hello 기본 orchestrator 선택 제외 하 고 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="b9447-180">DC/OS 템플릿</span><span class="sxs-lookup"><span data-stu-id="b9447-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="b9447-181">Swarm 템플릿</span><span class="sxs-lookup"><span data-stu-id="b9447-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="b9447-182">Kubernetes 템플릿</span><span class="sxs-lookup"><span data-stu-id="b9447-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="b9447-183">Tooyour Azure 계정에에서 로그인 (`az login`), 해당 hello Azure CLI 연결된 tooyour Azure 구독 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="b9447-184">다음 명령을 hello를 사용 하 여 hello 기본 구독을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="b9447-185">둘 이상의 구독과 필요 tooset 다른 기본 구독을 보유 하는 경우 실행 `az account set --subscription` hello 구독 ID 또는 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="b9447-186">모범 사례로, hello 배포에 대 한 새 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="b9447-187">리소스 그룹 toocreate hello를 사용 하 여 `az group create` 명령은 리소스 그룹 이름 및 위치 지정:</span><span class="sxs-lookup"><span data-stu-id="b9447-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="b9447-188">JSON 파일 포함 hello 필요한 템플릿 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="b9447-189">명명 된 다운로드 hello 매개 변수 파일 `azuredeploy.parameters.json` hello Azure 컨테이너 서비스 템플릿을 함께 제공 되는 `azuredeploy.json` GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="b9447-190">클러스터에 대한 필수 매개 변수 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="b9447-191">예를 들어 toouse hello [DC/OS 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), 매개 변수 값을 제공할 `dnsNamePrefix` 및 `sshRSAPublicKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="b9447-192">참조의 hello 설명 `azuredeploy.json` 및 다른 매개 변수에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="b9447-193">다음 명령을, hello로 hello 배포 매개 변수 파일을 전달 하 여 컨테이너 서비스 클러스터를 만들 위치:</span><span class="sxs-lookup"><span data-stu-id="b9447-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="b9447-194">**RESOURCE_GROUP** hello hello 이전 단계에서 만든 hello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="b9447-195">**DEPLOYMENT_NAME** (선택 사항) 이름인 toohello 배포를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="b9447-196">**TEMPLATE_URI** 는 hello 배포 파일의 위치 hello `azuredeploy.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="b9447-197">이 URI는 포인터 toohello GitHub UI hello 원시 파일 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="b9447-198">toofind 선택 hello이이 URI `azuredeploy.json` GitHub에서 파일을 hello 클릭 **Raw** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="b9447-199">또한 hello 명령줄에서 JSON 형식 문자열 매개 변수를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="b9447-200">명령 비슷한 toohello 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="b9447-201">hello 배포는 몇 분 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="b9447-202">동일한 PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="b9447-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="b9447-203">PowerShell 사용하여 Azure Container Service 클러스터 템플릿을 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="b9447-204">이 문서는 hello 버전 1.0 기반 [Azure PowerShell 모듈](https://azure.microsoft.com/blog/azps-1-0/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="b9447-205">DC/OS, docker는 Docker Swarm 또는 Kubernetes 클러스터 toodeploy GitHub에서 hello 빠른 시작 사용 가능한 템플릿 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="b9447-206">다음은 일부 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-206">A partial list follows.</span></span> <span data-ttu-id="b9447-207">참고는 hello DC/OS 및 웜 서식 파일은 hello 동일 hello 예외 hello 기본 orchestrator 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="b9447-208">DC/OS 템플릿</span><span class="sxs-lookup"><span data-stu-id="b9447-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="b9447-209">Swarm 템플릿</span><span class="sxs-lookup"><span data-stu-id="b9447-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="b9447-210">Kubernetes 템플릿</span><span class="sxs-lookup"><span data-stu-id="b9447-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="b9447-211">Azure 구독에서 클러스터를 만들기 전에 tooAzure에서 PowerShell 세션에 서명이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="b9447-212">Hello로 이렇게 하려면 `Get-AzureRMSubscription` 명령:</span><span class="sxs-lookup"><span data-stu-id="b9447-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="b9447-213">Hello를 사용 하 여 toosign tooAzure에서 해야 할 경우 `Login-AzureRMAccount` 명령:</span><span class="sxs-lookup"><span data-stu-id="b9447-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="b9447-214">모범 사례로, hello 배포에 대 한 새 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="b9447-215">리소스 그룹 toocreate hello를 사용 하 여 `New-AzureRmResourceGroup` 명령을 실행 하 고 리소스 그룹 이름 및 대상 지역을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="b9447-216">리소스 그룹을 만든 후 다음 명령을 hello로 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="b9447-217">hello hello의 URI 템플릿이 hello로 지정 되어 필요한 `-TemplateUri` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="b9447-218">이 명령을 실행하면 PowerShell에서 배포 매개 변수 값을 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="b9447-219">템플릿 매개 변수 제공</span><span class="sxs-lookup"><span data-stu-id="b9447-219">Provide template parameters</span></span>
<span data-ttu-id="b9447-220">PowerShell에 익숙하다면 빼기 기호 (-)를 입력 하 고 다음 hello TAB 키를 눌러 cmdlet에 대 한 사용 가능한 매개 변수 hello 순환 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="b9447-221">이 기능은 템플릿에 정의하는 매개 변수에 대해서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="b9447-222">Hello 템플릿 이름을 입력 하는 즉시 hello cmdlet는 hello 서식 파일을 인출 하 hello 매개 변수를 구문 분석 하 고 hello 템플릿 매개 변수 toohello 명령을 동적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="b9447-223">이 통해 쉽게 toospecify hello 템플릿 매개 변수 값.</span><span class="sxs-lookup"><span data-stu-id="b9447-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="b9447-224">하며, 필요한 매개 변수 값을 잊은 경우 PowerShell 묻는 hello 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="b9447-225">다음은 매개 변수가 포함 되어 있는 hello 전체 명령이입니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="b9447-226">Hello 리소스의 hello 이름에 대 한 사용자 지정 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9447-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="b9447-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9447-227">Next steps</span></span>
<span data-ttu-id="b9447-228">이제 클러스터가 작동하기 시작했으니 연결 및 관리 정보는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9447-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="b9447-229">Tooan Azure 컨테이너 서비스 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b9447-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="b9447-230">Azure 컨테이너 서비스 및 DC/OS로 작업</span><span class="sxs-lookup"><span data-stu-id="b9447-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="b9447-231">Azure 컨테이너 서비스 및 Docker Swarm으로 작업</span><span class="sxs-lookup"><span data-stu-id="b9447-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="b9447-232">Azure Container Service 및 Kubernetes로 작업</span><span class="sxs-lookup"><span data-stu-id="b9447-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
