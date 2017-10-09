---
title: "패브릭 aaaService 노드 형식 및 VM 크기 집합이 | Microsoft Docs"
description: "서비스 패브릭 노드 형식 tooVM 크기 집합의 관계 및 tooremote tooa VM 크기 집합 인스턴스 또는 클러스터 노드를 연결 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="90131-103">서비스 패브릭 노드 형식 및 가상 컴퓨터 크기 집합 간의 hello 관계</span><span class="sxs-lookup"><span data-stu-id="90131-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="90131-104">가상 컴퓨터 크기 집합은 toodeploy를 사용 하 고 집합으로 가상 컴퓨터의 컬렉션을 관리할 수는 Azure 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="90131-105">서비스 패브릭 클러스터에 정의된 모든 노드 유형은 별도의 VM 확장 집합으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="90131-106">각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="90131-107">다음 스크린 샷에서 hello 클러스터에는 두 노드 종류를 보여 줍니다: 프런트 엔드 및 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="90131-108">각 노드 형식에는 5개의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-108">Each node type has five nodes each.</span></span>

![두 가지 노드 유형이 있는 클러스터의 스크린 샷][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="90131-110">VM 크기 집합 인스턴스 toonodes 매핑</span><span class="sxs-lookup"><span data-stu-id="90131-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="90131-111">위에서 볼 수 있듯이 hello VM 크기 집합 인스턴스는 인스턴스 0에서에서 시작 하 고 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="90131-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="90131-112">hello 번호 매기기 hello 이름에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="90131-113">예를 들어, BackEnd_0 hello 백 엔드 VM 크기 집합의 인스턴스 0입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="90131-114">이 특정 VM 크기 조정 설정에는 BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 및 BackEnd_4라는 5개의 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="90131-115">VM 크기 조정 설정을 확대하는 경우 새 인스턴스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="90131-116">hello VM 크기 집합 이름 + 인스턴스 번호를 다음 hello hello 새 VM 크기 집합 인스턴스 이름은 일반적으로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="90131-117">이 예제에서는 BackEnd_5입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="90131-118">매핑 VM 크기 집합 부하 분산 장치 tooeach 노드 유형/VM 크기 집합</span><span class="sxs-lookup"><span data-stu-id="90131-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="90131-119">म 때 제공 되는, 다음의 리소스 그룹 아래의 모든 리소스 목록을 가져올 hello 샘플 리소스 관리자 템플릿을 사용 hello 포털에서 클러스터를 배포 하는 경우 각 VM 크기 집합 또는 노드 형식에 대 한 hello 부하 분산 장치 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="90131-120">hello 이름은 다음과 같이: **LB-&lt;NodeType 이름&gt;**합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="90131-121">예를 들어 이 스크린 샷에 표시된 대로 LB-sfcluster4doc-0입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![리소스][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="90131-123">원격 연결 tooa VM 크기 집합 인스턴스 또는 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="90131-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="90131-124">클러스터에 정의된 모든 노드 유형은 별도의 VM 확장 집합으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="90131-125">의미 hello 노드 유형에 확장할 수 있습니다 또는 독립적으로 아래쪽 및 다른 VM Sku 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="90131-126">단일 인스턴스 Vm 달리 hello VM 크기 집합 인스턴스는 자체의 가상 IP 주소를 얻지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="90131-127">비트 될 수 있도록 IP에 대 한 원하는 어려운 주소와 포트 tooremote를 사용할 수 있는 연결 tooa 특정 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="90131-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="90131-128">다음은 hello 단계 toodiscover 따를 수 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="90131-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="90131-129">1 단계: hello hello 노드 형식에 대 한 가상 IP 주소 및 RDP에 대 한 인바운드 NAT 규칙 확인</span><span class="sxs-lookup"><span data-stu-id="90131-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="90131-130">순서 tooget 해야 하는, tooget hello 인바운드 NAT 규칙에 대 한 hello 리소스 정의의 일부로 정의 된 값을 **Microsoft.Network/loadBalancers**합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="90131-131">Hello 포털에서 toohello 부하 분산 장치 블레이드를 탐색 한 다음 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="90131-133">**설정**에서 **인바운드 NAT 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="90131-134">이 구문은 이제 IP 주소와 포트 tooremote를 사용할 수 있는 hello 제공 toohello 첫 번째 VM 크기 집합 인스턴스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="90131-135">아래 hello 스크린샷에서 편이 **104.42.106.156** 및 **3389**</span><span class="sxs-lookup"><span data-stu-id="90131-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="90131-137">2 단계: tooremote를 사용할 수 있는 hello 포트에 대해 알아봅니다 연결 toohello 특정 VM 크기 집합 인스턴스/노드</span><span class="sxs-lookup"><span data-stu-id="90131-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="90131-138">이 문서의 앞부분에서 hello VM 크기 집합 인스턴스 toohello 노드 매핑 하는 방법에 대 한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="90131-139">해당 toofigure 끝 hello 정확한 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="90131-140">hello VM 크기 집합 인스턴스의 오름차순 hello 포트가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="90131-141">따라서 hello 프런트 엔드 노드 형식에 대 한 예제에서 hello 5 개의 인스턴스 각각에 대 한 hello 포트는 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="90131-142">하면 toodo 필요한 VM 크기 집합 인스턴스에 대 한 동일한 매핑을 hello 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="90131-143">**VM 확장 집합 인스턴스**</span><span class="sxs-lookup"><span data-stu-id="90131-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="90131-144">**포트**</span><span class="sxs-lookup"><span data-stu-id="90131-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="90131-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="90131-145">FrontEnd_0</span></span> |<span data-ttu-id="90131-146">3389</span><span class="sxs-lookup"><span data-stu-id="90131-146">3389</span></span> |
| <span data-ttu-id="90131-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="90131-147">FrontEnd_1</span></span> |<span data-ttu-id="90131-148">3390</span><span class="sxs-lookup"><span data-stu-id="90131-148">3390</span></span> |
| <span data-ttu-id="90131-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="90131-149">FrontEnd_2</span></span> |<span data-ttu-id="90131-150">3391</span><span class="sxs-lookup"><span data-stu-id="90131-150">3391</span></span> |
| <span data-ttu-id="90131-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="90131-151">FrontEnd_3</span></span> |<span data-ttu-id="90131-152">3392</span><span class="sxs-lookup"><span data-stu-id="90131-152">3392</span></span> |
| <span data-ttu-id="90131-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="90131-153">FrontEnd_4</span></span> |<span data-ttu-id="90131-154">3393</span><span class="sxs-lookup"><span data-stu-id="90131-154">3393</span></span> |
| <span data-ttu-id="90131-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="90131-155">FrontEnd_5</span></span> |<span data-ttu-id="90131-156">3394</span><span class="sxs-lookup"><span data-stu-id="90131-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="90131-157">3 단계: 원격 연결 toohello 특정 VM 크기 집합 인스턴스</span><span class="sxs-lookup"><span data-stu-id="90131-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="90131-158">아래의 스크린 샷은 hello tooconnect toohello FrontEnd_1 원격 데스크톱 연결을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="90131-160">어떻게 toochange hello RDP 포트 범위 값은</span><span class="sxs-lookup"><span data-stu-id="90131-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="90131-161">클러스터 배포 전에</span><span class="sxs-lookup"><span data-stu-id="90131-161">Before cluster deployment</span></span>
<span data-ttu-id="90131-162">리소스 관리자 템플릿을 사용 하 여 hello 클러스터를 설정 하는 경우 hello에 hello 범위를 지정할 수 있습니다 **inboundNatPools**합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="90131-163">Toohello 리소스 정의 대 한 이동 **Microsoft.Network/loadBalancers**합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="90131-164">에 대 한 hello 설명 하는 아래 **inboundNatPools**합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="90131-165">Hello 대체 *가 frontendPortRangeStart* 및 *frontendPortRangeEnd* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="90131-167">클러스터 배포 후에</span><span class="sxs-lookup"><span data-stu-id="90131-167">After cluster deployment</span></span>
<span data-ttu-id="90131-168">이 좀 더 참여 하 고 재생 되지 hello Vm에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90131-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="90131-169">지금 Azure PowerShell을 사용 하 여 tooset 새 값을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90131-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="90131-170">컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="90131-171">이전 수행 하지 않은 경우 것이 좋다는에 설명 된 hello 단계를 수행한 [어떻게 tooinstall Azure PowerShell 및 구성 합니다.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="90131-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="90131-172">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="90131-173">Powershell이 어떤 이유로 인해 실패하면 Azure PowerShell이 올바르게 설치되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90131-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="90131-174">Hello tooget 부하 분산 장치에 대 한 내용은 다음을 실행 하 고 hello 값에 대 한 hello 설명에 대 한 참조 **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="90131-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="90131-175">이제 설정 *frontendPortRangeEnd* 및 *가 frontendPortRangeStart* 원하는 toohello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="90131-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="90131-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90131-176">Next steps</span></span>
* [<span data-ttu-id="90131-177">Hello "배포 아무 곳 이나" 기능 및 Azure에서 관리 하는 클러스터와 비교의 개요</span><span class="sxs-lookup"><span data-stu-id="90131-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="90131-178">클러스터 보안</span><span class="sxs-lookup"><span data-stu-id="90131-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="90131-179"> 서비스 패브릭 SDK 및 시작</span><span class="sxs-lookup"><span data-stu-id="90131-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
