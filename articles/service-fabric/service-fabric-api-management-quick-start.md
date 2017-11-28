---
title: "API 관리 빠른 시작 되 면 서비스 패브릭 aaaAzure | Microsoft Docs"
description: "이 가이드에서는 Azure API 관리 및 서비스 패브릭 tooquickly 시작 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="6dd8b-103">Service Fabric 및 Azure API Management 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="6dd8b-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="6dd8b-104">이 가이드에서는 알아봅니다 tooset Azure API 관리 서비스 패브릭를 하 고 서비스 패브릭에서 첫 번째 API 작업 toosend 트래픽 tooback 간 서비스를 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="6dd8b-105">서비스 패브릭 Azure API 관리 시나리오에 대해 자세히 toolearn 참조 hello [개요](service-fabric-api-management-overview.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="6dd8b-106">API 관리 및 서비스 패브릭 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="6dd8b-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="6dd8b-107">hello 첫 번째 단계는 toodeploy API 관리 및 공유 가상 네트워크에서 서비스 패브릭 클러스터 tooAzure 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="6dd8b-108">따라서 tooany 백 엔드 서비스 서비스 패브릭에서 직접 서비스 검색과 서비스 파티션 확인 트래픽을 전달을 수행할 수 있도록 서비스 패브릭와 직접 API 관리 toocommunicate를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="6dd8b-109">토폴로지</span><span class="sxs-lookup"><span data-stu-id="6dd8b-109">Topology</span></span>

<span data-ttu-id="6dd8b-110">이 가이드는 hello 다음 배포 토폴로지 tooAzure API 관리 및 서비스 패브릭의 서브넷에는 hello 동일한 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![그림 캡션][sf-apim-topology-overview]

<span data-ttu-id="6dd8b-112">리소스 관리자 템플릿은 tooget 신속 하 게 시작 각 배포 단계에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="6dd8b-113">네트워크 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-113">Network topology:</span></span>
    - <span data-ttu-id="6dd8b-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="6dd8b-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="6dd8b-116">Service Fabric 클러스터:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="6dd8b-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="6dd8b-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="6dd8b-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-119">API Management:</span></span>
    - <span data-ttu-id="6dd8b-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="6dd8b-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="6dd8b-122">TooAzure에 로그인 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="6dd8b-123">이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="6dd8b-124">새 PowerShell 세션을 시작할 때 tooyour Azure 계정에에서 로그인 하 고 Azure 명령을 실행 하기 전에 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="6dd8b-125">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="6dd8b-126">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6dd8b-127">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6dd8b-127">Create a resource group</span></span>

<span data-ttu-id="6dd8b-128">배포에 대해 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="6dd8b-129">이름 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="6dd8b-130">Hello 네트워크 토폴로지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-130">Deploy hello network topology</span></span>

<span data-ttu-id="6dd8b-131">hello 첫 번째 단계는 hello 네트워크 토폴로지 toowhich API 관리를 tooset 및 hello 서비스 패브릭 클러스터를 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="6dd8b-132">hello [network.json] [ network-arm] 리소스 관리자 서식 파일은 구성 된 toocreate 두 서브넷과 가상 네트워크 (VNET) 및 두 개의 보안 그룹 NSG (네트워크).</span><span class="sxs-lookup"><span data-stu-id="6dd8b-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="6dd8b-133">hello [network.parameters.json] [ network-parameters-arm] 매개 변수 파일 hello 서브넷 및 API 관리 및 서비스 패브릭에 배포 될 Nsg의 hello 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="6dd8b-134">이 가이드에 대 한 hello 매개 변수 값 변경 toobe가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="6dd8b-135">이러한 값을 사용 하는 hello API 관리 및 서비스 패브릭 리소스 관리자 템플릿, 그에 따라에 다른 리소스 관리자 템플릿을 hello 여기를 수정 하는 경우 수정 해야 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="6dd8b-136">Hello 다음 리소스 관리자 템플릿 및 매개 변수 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="6dd8b-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="6dd8b-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="6dd8b-139">다음 PowerShell 명령을 toodeploy hello 리소스 관리자 템플릿 및 매개 변수 파일이 hello 네트워크 설정에 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="6dd8b-140">Hello 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="6dd8b-141">Hello 네트워크 리소스 배포를 완료 되 고 나면 hello 다음 단계 toodeploy hello 서브넷에 있는 서비스 패브릭 클러스터 toohello VNET 되며 NSG hello 서비스 패브릭 클러스터에 대 한 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="6dd8b-142">이 자습서에 대 한 hello 서비스 패브릭 리소스 관리자 템플릿은 hello VNET, 서브넷 및 hello 이전 단계에서 설정한 NSG의 미리 구성 된 toouse hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="6dd8b-143">hello 서비스 패브릭 클러스터 리소스 관리자 템플릿 구성된 toocreate 인증서 보안을 사용 하 여 보안 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="6dd8b-144">hello 인증서가 클러스터 및 toomanage 사용자 액세스 tooyour 서비스 패브릭 클러스터에 사용 되는 toosecure 노드 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="6dd8b-145">API 관리 서비스 검색에 대 한이 인증서 tooaccess hello 서비스 패브릭 명명 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="6dd8b-146">이 단계에서는 클러스터 보안을 위해 Key Vault에 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="6dd8b-147">Key Vault를 사용하여 보안 클러스터를 설정하는 작업에 대한 자세한 내용은 [Resource Manager를 사용하여 Azure에서 클러스터를 만드는 방법에 대한 가이드](service-fabric-cluster-creation-via-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="6dd8b-148">Azure Active Directory 인증 클러스터 액세스에 사용 되는 추가 toohello 인증서에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="6dd8b-149">Azure Active Directory 방식으로 toomanage 사용자 액세스 tooyour 서비스 패브릭 클러스터를 권장 하는 hello 이지만이 자습서 toocomplete 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="6dd8b-150">인증서는 클러스터 노드 간 보안에도 필요하고 Azure API Management 인증에도 필요하지만 Service Fabric 백 엔드에 대해 Azure Active Directory를 사용하는 인증은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="6dd8b-151">Hello 다음 리소스 관리자 템플릿 및 매개 변수 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="6dd8b-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="6dd8b-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="6dd8b-154">Hello hello에 빈 매개 변수를 입력 `cluster.parameters.json` hello 등 배포에 대 한 파일 [키 자격 증명 모음 정보가](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) 클러스터 인증서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="6dd8b-155">다음 PowerShell 명령을 toodeploy hello 리소스 관리자 템플릿 및 매개 변수 파일 toocreate hello 서비스 패브릭 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="6dd8b-156">API Management 배포</span><span class="sxs-lookup"><span data-stu-id="6dd8b-156">Deploy API Management</span></span>

<span data-ttu-id="6dd8b-157">API 관리 toohello VNET 서브넷 hello 및 API 관리에 대 한 지정 된 NSG에 마지막으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="6dd8b-158">않아도 toowait 서비스 패브릭 클러스터 배포 toofinish hello에 대 한 API 관리를 배포 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="6dd8b-159">이 자습서에 대 한 hello API 관리 리소스 관리자 템플릿은 hello VNET, 서브넷 및 hello 이전 단계에서 설정한 NSG의 미리 구성 된 toouse hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="6dd8b-160">Hello 다음 리소스 관리자 템플릿 및 매개 변수 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="6dd8b-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="6dd8b-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="6dd8b-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="6dd8b-163">Hello hello에 빈 매개 변수를 입력 `apim.parameters.json` 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="6dd8b-164">다음 PowerShell 명령을 toodeploy hello 리소스 관리자 템플릿 및 매개 변수 파일이 API 관리에 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="6dd8b-165">API Management 구성</span><span class="sxs-lookup"><span data-stu-id="6dd8b-165">Configure API Management</span></span>

<span data-ttu-id="6dd8b-166">API Management 및 Service Fabric 클러스터가 배포되면 API Management에서 Service Fabric 백 엔드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="6dd8b-167">이렇게 하면 toocreate 트래픽 tooyour 서비스 패브릭 클러스터를 보내는 백 엔드 서비스 정책은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="6dd8b-168">API Management 보안</span><span class="sxs-lookup"><span data-stu-id="6dd8b-168">API Management Security</span></span>

<span data-ttu-id="6dd8b-169">tooconfigure hello 서비스 패브릭 백 엔드 먼저 tooconfigure API 관리의 보안 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="6dd8b-170">tooconfigure 보안 설정을 hello Azure 포털의에서 tooyour API 관리 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="6dd8b-171">Hello API 관리 REST API를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6dd8b-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="6dd8b-172">hello API 관리 REST API는 현재 hello 유일한 방법은 tooconfigure 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="6dd8b-173">hello 첫 번째 단계는 tooenable hello API 관리 REST API 및 보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="6dd8b-174">API 관리 서비스 hello 선택 **관리 API-미리 보기** 아래 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="6dd8b-175">Hello 확인 **API 관리 REST API 사용** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="6dd8b-176">관리 API URL hello-이후 tooset hello 서비스 패브릭 백 엔드를 사용 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="6dd8b-177">생성 된 **액세스 토큰** 만료 날짜와 키를 선택 하 여 hello를 클릭 한 다음 **생성** hello 페이지의 hello 아래쪽으로 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="6dd8b-178">복사 hello **액세스 토큰** 및 저장-단계를 수행 하는 hello이 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="6dd8b-179">Note hello 기본 키와 보조 키와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="6dd8b-180">Service Fabric 클라이언트 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="6dd8b-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="6dd8b-181">API 관리 액세스 tooyour 클러스터를 포함 하는 클라이언트 인증서를 사용 하 여 서비스 검색에 대 한 서비스 패브릭 클러스터도 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="6dd8b-182">간단한 설명을 위해이 자습서에서는 클러스터에 동일한 인증서는 기본적으로 사용 되는 tooaccess 수 hello 서비스 패브릭 클러스터를 만들 때 지정한을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="6dd8b-183">API 관리 서비스 hello 선택 **클라이언트 인증서-미리 보기** 아래 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="6dd8b-184">Hello 클릭 **+ 추가** 단추</span><span class="sxs-lookup"><span data-stu-id="6dd8b-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="6dd8b-185">Hello 개인 키 (.pfx) 인증서의 파일 hello 클러스터 서비스 패브릭 클러스터를 만들 때 지정한 선택한 이름을, hello 개인 키 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="6dd8b-186">이 자습서에서는 클라이언트 인증 및 클러스터 노드를 보안에 대 한 hello 동일한 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="6dd8b-187">구성 된 하나의 tooaccess 서비스 패브릭 클러스터를 설정한 경우 별도 클라이언트 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="6dd8b-188">Hello 백 엔드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-188">Configure hello backend</span></span>

<span data-ttu-id="6dd8b-189">API 관리 보안을 구성 했으므로 hello 서비스 패브릭 백 엔드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="6dd8b-190">서비스 패브릭 백 엔드에 대 한 hello 서비스 패브릭 클러스터에는 특정 서비스 패브릭 서비스 아니라 hello 백 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="6dd8b-191">그러면 hello 클러스터를 하나의 서비스 보다 단일 정책 tooroute toomore 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="6dd8b-192">이 단계는 앞에서 생성 하는 hello 액세스 토큰이 필요 하 고 hello tooAPI 관리 hello 이전 단계에서 업로드 한 클러스터 인증서에 대 한 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="6dd8b-193">Hello 이전 단계에서 별도 클라이언트 인증서를 사용 하는 API 관리에 대 한 경우이 단계에서는 추가 toohello 클러스터 인증서 지문에 클라이언트 인증서 hello hello 지문이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="6dd8b-194">HTTP PUT 요청 toohello API 관리 API URL hello API 관리 REST API tooconfigure hello 서비스 패브릭 백 엔드 서비스를 사용 하도록 설정할 때 앞에서 기록한 다음 hello를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="6dd8b-195">표시 됩니다는 `HTTP 201 Created` hello 명령 성공할 때 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="6dd8b-196">각 필드에 대 한 자세한 내용은 참조 hello API 관리 [백 엔드 API 참조 설명서](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="6dd8b-197">HTTP 명령 및 URL:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="6dd8b-198">헤더 요청:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="6dd8b-199">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="6dd8b-200">hello **url** 여기에서 매개 변수는 모든 요청을 하는 클러스터에서 서비스의 정규화 된 서비스 이름을 라우팅할 tooby 기본 백 엔드 정책에 지정 되는 서비스 이름이 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="6dd8b-201">와 같은 가짜 서비스 이름을 사용할 수 있습니다 "fabric: / 가짜/서비스" toohave 대체 서비스 수행 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="6dd8b-202">API 관리 toohello 참조 [백 엔드 API 참조 설명서](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) 각 필드에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="6dd8b-203">예제</span><span class="sxs-lookup"><span data-stu-id="6dd8b-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="6dd8b-204">Service Fabric 백 엔드 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="6dd8b-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="6dd8b-205">서비스 패브릭 백 엔드 tooAPI 관리로 구성 하는 hello를가지고 tooyour 서비스 패브릭 서비스 트래픽을 전송 하는 Api에 대 한 백 엔드 정책을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="6dd8b-206">그러나 먼저 서비스 패브릭 tooaccept 요청에서 실행 되는 서비스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="6dd8b-207">HTTP 끝점이 있는 Service Fabric 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="6dd8b-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="6dd8b-208">이 자습서에 대 한 기본 상태 비저장 ASP.NET Core 신뢰할 수 있는 서비스 hello 기본 웹 API 프로젝트 템플릿을 사용 하 여 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="6dd8b-209">이렇게 하면 서비스의 HTTP 끝점을 Azure API Management를 통해 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="6dd8b-210">[ASP.NET Core 개발에 대한 개발 환경을 설정](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core)하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="6dd8b-211">개발 환경이 설정되면 Visual Studio를 관리자 권한으로 시작하고 ASP.NET Core 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="6dd8b-212">Visual Studio에서 파일 -> 새 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="6dd8b-213">클라우드에 hello 서비스 패브릭 응용 프로그램 템플릿을 선택 하 고 이름을 **"ApiApplication"**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="6dd8b-214">Hello ASP.NET Core 서비스 템플릿 선택한 이름 hello 프로젝트 **"WebApiService"**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="6dd8b-215">Web API ASP.NET Core 1.1 hello 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="6dd8b-216">Hello 프로젝트를 만든 후 엽니다 `PackageRoot\ServiceManifest.xml` hello를 제거 하 고 `Port` hello 끝점 리소스 구성에서 특성:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="6dd8b-217">이렇게 하면 서비스 패브릭 toospecify API 관리에서 트래픽 tooflow tooit 허용 hello 클러스터 리소스 관리자 템플릿에 hello 네트워크 보안 그룹을 통해 열에서는 있는 hello 응용 프로그램 포트 범위에서 동적으로 포트.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="6dd8b-218">Visual Studio tooverify hello web API에서에서 F5 키를 눌러를 로컬로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="6dd8b-219">서비스 패브릭 탐색기를 열고 드릴 다운 tooa 특정 인스턴스의 hello ASP.NET Core 서비스 toosee hello 기준 주소 hello 서비스에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="6dd8b-220">추가 `/api/values` toohello 기준 주소와 브라우저에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="6dd8b-221">Hello hello Web API 템플릿에 ValuesController hello에서 Get 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="6dd8b-222">두 문자열을 포함 하는 JSON 배열 hello 템플릿에서 제공 되는 hello 기본 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="6dd8b-223">Azure에서 API 관리를 통해 노출할 수 있는 hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="6dd8b-224">마지막으로, Azure의 hello 응용 프로그램 tooyour 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="6dd8b-225">[Visual Studio를 사용 하 여](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="6dd8b-226">클러스터 끝점을 제공 (예를 들어 `mycluster.westus.cloudapp.azure.com:19000`) Azure에 있는 toodeploy hello 응용 프로그램 tooyour 서비스 패브릭 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="6dd8b-227">`fabric:/ApiApplication/WebApiService`로 명명된 ASP.NET Core 상태 비저장 서비스는 이제 Azure의 Service Fabric 클러스터에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="6dd8b-228">API 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="6dd8b-228">Create an API operation</span></span>

<span data-ttu-id="6dd8b-229">이제 우리 준비 toocreate API 관리에서 작업으로 해당 외부 클라이언트가 사용 하 여 toocommunicate hello ASP.NET Core hello 서비스 패브릭 클러스터에서 실행 되는 상태 비저장 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="6dd8b-230">Azure 포털 toohello을 고 tooyour API 관리 서비스 배포를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="6dd8b-231">Hello API 관리 서비스 블레이드에서 선택 **Api-미리 보기**</span><span class="sxs-lookup"><span data-stu-id="6dd8b-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="6dd8b-232">Hello를 클릭 하 여 새로운 API 추가 **빈 API** 상자와 hello 대화 상자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="6dd8b-233">**웹 서비스 URL**: Service Fabric 백 엔드에는 이 URL 값이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="6dd8b-234">여기에 임의의 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-234">You can put any value here.</span></span> <span data-ttu-id="6dd8b-235">이 자습서에서는 `http://servicefabric`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="6dd8b-236">**이름**: API 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="6dd8b-237">이 자습서에서는 `Service Fabric App`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="6dd8b-238">**URL 구성표**: HTTP, HTTPS 또는 둘 다 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="6dd8b-239">이 자습서에서는 `both`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="6dd8b-240">**API URL 접미사**: API의 접미사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="6dd8b-241">이 자습서에서는 `myapp`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="6dd8b-242">Hello API를 만든 후 클릭 **추가 작업이 +** tooadd 프런트 엔드 API 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="6dd8b-243">Hello 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="6dd8b-244">**URL**: 선택 `GET` hello API에 대 한 URL 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="6dd8b-245">이 자습서에서는 `/api/values`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="6dd8b-246">기본적으로 hello URL 경로입니다. 여기에 지정 된 URL 경로 hello toohello 백 엔드 서비스 패브릭 서비스 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="6dd8b-247">Hello를 사용 하는 경우 동일한 URL 경로 여기에 경우 해당 서비스 사용 `/api/values`, 추가 수정 없이 hello 작업 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="6dd8b-248">이 경우는 또한 필요 toospecify 경로 다시 작성 작업이 정책에 나중에 백 엔드 서비스 패브릭 서비스에서 사용 하는 hello URL 경로와 다른 URL 경로 여기 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="6dd8b-249">**표시 이름**: hello API에 대 한 모든 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="6dd8b-250">이 자습서에서는 `Values`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="6dd8b-251">백 엔드 정책 구성</span><span class="sxs-lookup"><span data-stu-id="6dd8b-251">Configure a backend policy</span></span>

<span data-ttu-id="6dd8b-252">hello 백 엔드 정책 모든 항목이 함께 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="6dd8b-253">이 hello 백 엔드 서비스 패브릭 서비스 toowhich 요청 라우팅됩니다 구성한입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="6dd8b-254">이 정책 tooany API 작업을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="6dd8b-255">hello [서비스 패브릭 용 백 엔드 구성이](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) hello 다음 요청 라우팅 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="6dd8b-256">인스턴스 선택 하거나 하드 코드 된 서비스 패브릭 서비스 인스턴스 이름을 지정 하 여 서비스 (예를 들어 `"fabric:/myapp/myservice"`) 또는 hello HTTP 요청에서 생성 된 (예를 들어 `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="6dd8b-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="6dd8b-257">Service Fabric 분할 체계를 통해 파티션 키를 생성하여 파티션 확인</span><span class="sxs-lookup"><span data-stu-id="6dd8b-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="6dd8b-258">상태 저장 서비스 복제본 선택</span><span class="sxs-lookup"><span data-stu-id="6dd8b-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="6dd8b-259">확인 조건을 다시 서비스 위치를 확인 하 고 요청을 보내거나 toospecify hello 조건을 사용할 수 있는 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="6dd8b-260">이 자습서에 대 한 요청을 라우팅하 직접 toohello 이전에 배포한 ASP.NET Core 상태 비저장 서비스 백 엔드 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="6dd8b-261">선택 하 고 hello 편집 **정책 인바운드** hello에 대 한 `Values` hello 편집 아이콘을 클릭 하 고 다음을 선택 하 여 작업 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="6dd8b-262">Hello 정책 코드 편집기에서 추가 된 `set-backend-service` 아래에서 다음과 같이 정책 인바운드 정책과 hello 클릭 **저장** 단추:</span><span class="sxs-lookup"><span data-stu-id="6dd8b-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="6dd8b-263">모든 서비스 패브릭 백 엔드 정책 특성 집합에 대 한 참조 toohello [API 관리 백 엔드 설명서](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="6dd8b-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="6dd8b-264">Hello API tooa 제품을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="6dd8b-265">Hello API를 호출할 수 있습니다, 전에 tooa 제품 toousers 액세스 권한을 부여할 수 있는 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="6dd8b-266">API 관리 서비스 hello 선택 **제품-미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="6dd8b-267">기본적으로 API Management는 스타터와 무제한의 두 가지 제품을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="6dd8b-268">Hello 무제한 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="6dd8b-269">API를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-269">Select APIs.</span></span>
 4. <span data-ttu-id="6dd8b-270">Hello 클릭 **+ 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="6dd8b-271">선택 hello `Service Fabric App` API hello 누르고 hello 이전 단계에서 만든 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="6dd8b-272">테스트</span><span class="sxs-lookup"><span data-stu-id="6dd8b-272">Test it</span></span>

<span data-ttu-id="6dd8b-273">이제 hello Azure 포털에서 직접 요청 tooyour 백 엔드 서비스 관리 API를 통해 서비스 패브릭에서 보내는 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="6dd8b-274">API 관리 서비스 hello 선택 **API-미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="6dd8b-275">Hello에 `Service Fabric App` hello 이전 단계에서 만든 API 선택 hello **테스트** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="6dd8b-276">Hello 클릭 **보낼** 단추 toosend 테스트 요청 toohello 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dd8b-277">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6dd8b-277">Next steps</span></span>

<span data-ttu-id="6dd8b-278">이제 기본 설정의 Service Fabric 및 API Management가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="6dd8b-279">이 자습서를 신속 하 게 설정 하 여 서비스 패브릭 클러스터 tooget에 대 한 기본 인증서 기반 사용자 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="6dd8b-280">Service Fabric 클러스터에 대한 보다 고급의 사용자 인증은 [Azure Active Directory 인증](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication)과 함께 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="6dd8b-281">그런 다음, [만들고 Azure API 관리에서 고급 제품 설정을 구성](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare 현실 세계 트래픽에 대 한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8b-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
