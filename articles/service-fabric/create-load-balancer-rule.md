---
title: "클러스터에 대 한 Azure 부하 분산 장치 규칙 aaaCreate"
description: "Azure 서비스 패브릭 클러스터에 대 한 Azure 부하 분산 장치 tooopen 포트를 구성 합니다."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="5405e-103">Service Fabric 클러스터에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="5405e-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="5405e-104">hello 부하 분산 장치에 배포 된 Azure 서비스 패브릭 클러스터 노드에서 실행 되는 트래픽 tooyour 응용 프로그램을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="5405e-105">사용자 앱 toouse 다른 포트를 변경 하면 해야 해당 포트를 노출 (또는 다른 포트로 라우팅할) hello Azure 부하 분산 장치에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="5405e-106">서비스 패브릭 클러스터 tooAzure 프로그램을 배포할 때 부하 분산 장치에 자동으로 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="5405e-107">부하 분산 장치가 없는 경우 [인터넷 연결 부하 분산 장치 구성](..\load-balancer\load-balancer-get-started-internet-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5405e-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="5405e-108">Service Fabric 구성</span><span class="sxs-lookup"><span data-stu-id="5405e-108">Configure service fabric</span></span>

<span data-ttu-id="5405e-109">서비스 패브릭 응용 프로그램 **ServiceManifest.xml** 응용 프로그램에 toouse hello 끝점을 정의 하는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="5405e-110">Hello 부하 분산 장치에 업데이트 된 tooexpose 해당 (또는 다른)이 있어야 hello 구성 파일에 대 한 업데이트 된 toodefine 끝점을 수행한 후 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="5405e-111">Toocreate 서비스 패브릭 끝점 hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [끝점 설정](service-fabric-service-manifest-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="5405e-112">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="5405e-112">Create a load balancer rule</span></span>

<span data-ttu-id="5405e-113">부하 분산 장치 규칙 인터넷 연결 포트를 열리고 응용 프로그램에서 사용 하는 트래픽 toohello 내부 노드 포트를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="5405e-114">부하 분산 장치가 없는 경우 [인터넷 연결 부하 분산 장치 구성](..\load-balancer\load-balancer-get-started-internet-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5405e-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="5405e-115">다음 정보는 toocollect hello 해야 toocreate 부하 분산 장치 규칙:</span><span class="sxs-lookup"><span data-stu-id="5405e-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="5405e-116">부하 분산 장치 이름</span><span class="sxs-lookup"><span data-stu-id="5405e-116">Load balancer name.</span></span>
- <span data-ttu-id="5405e-117">리소스 그룹의 hello 부하 분산 장치 및 서비스 패브릭 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="5405e-118">외부 포트</span><span class="sxs-lookup"><span data-stu-id="5405e-118">External port.</span></span>
- <span data-ttu-id="5405e-119">내부 포트</span><span class="sxs-lookup"><span data-stu-id="5405e-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="5405e-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5405e-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="5405e-121">Toodetermine hello hello 부하 분산 장치의 이름으로 필요한 경우이 명령은 tooquickly get 모든 부하 분산 장치 및 연결 된 hello 리소스 그룹의 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="5405e-122">단 하나의 명령 toocreate hello로 부하 분산 장치 규칙 **Azure CLI**합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="5405e-123">하기만 하면 tooknow hello 부하 분산 장치 및 리소스 그룹 toocreate 새 규칙의 이름을 모두 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="5405e-124">hello Azure CLI 명령을 hello 표 다음에 설명 되어 있는 몇 가지 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="5405e-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5405e-125">Parameter</span></span> | <span data-ttu-id="5405e-126">설명</span><span class="sxs-lookup"><span data-stu-id="5405e-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="5405e-127">hello 포트 hello 서비스 패브릭 응용 프로그램을 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="5405e-128">hello 포트 hello 부하 분산 장치 노출 하는 외부 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="5405e-129">hello의 hello 이름 부하 분산 장치 toochange 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="5405e-130">hello 부하 분산 장치 및 서비스 패브릭 클러스터를 모두 있는 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="5405e-131">hello hello 규칙의 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="5405e-132">Toocreate hello Azure CLI로 부하 분산 장치를 확인 하려면 어떻게 대 한 자세한 내용은 [hello Azure CLI를 사용 하 여 부하 분산 장치 만들기](..\load-balancer\load-balancer-get-started-internet-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="5405e-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5405e-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="5405e-134">Toodetermine hello hello 부하 분산 장치의 이름으로 필요한 경우이 명령은 tooquickly get 모든 부하 분산 장치 및 관련된 리소스 그룹의 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="5405e-135">PowerShell은 Azure CLI hello 보다 좀 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="5405e-136">개념적으로 hello 단계 toocreate 다음 규칙을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="5405e-137">Azure의 hello 부하 분산 장치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="5405e-138">규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-138">Create a rule.</span></span>
3. <span data-ttu-id="5405e-139">Hello 규칙 toohello 부하 분산 장치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="5405e-140">Hello 부하 분산 장치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="5405e-141">Hello에 대 한 `New-AzureRmLoadBalancerRuleConfig` 명령을 hello `-FrontendPort` 나타냅니다 hello 포트 hello 부하 분산 장치의 외부 연결 및 hello에 대 한 노출 `-BackendPort` 나타냅니다 hello 포트 hello 서비스 패브릭 응용 프로그램을 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="5405e-142">Toocreate powershell을 부하 분산 장치를 확인 하려면 어떻게 대 한 자세한 내용은 [PowerShell을 사용 하 여 부하 분산 장치 만들기](..\load-balancer\load-balancer-get-started-internet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5405e-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

