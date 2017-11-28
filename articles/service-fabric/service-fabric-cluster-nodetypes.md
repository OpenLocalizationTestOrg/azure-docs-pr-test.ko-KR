---
title: "Service Fabric 노드 형식 및 VM Scale Sets | Microsoft Docs"
description: "VM 크기 조정 설정과 서비스 패브릭 노드 유형의 관계 및 VM 크기 조정 설정 인스턴스 또는 클러스터 노드에 원격으로 연결하는 방법을 설명합니다."
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
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="92764-103">서비스 패브릭 노드 형식과 가상 컴퓨터 확장 집합 간의 관계</span><span class="sxs-lookup"><span data-stu-id="92764-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="92764-104">가상 컴퓨터 규모 집합은 가상 컴퓨터의 컬렉션을 집합으로 배포하고 관리하는 데 사용할 수 있는 Azure 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="92764-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="92764-105">서비스 패브릭 클러스터에 정의된 모든 노드 유형은 별도의 VM 확장 집합으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="92764-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="92764-106">각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="92764-107">다음 스크린 샷에서는 프런트 엔드 및 백 엔드 등 두 가지 노드 유형이 있는 클러스터를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="92764-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="92764-108">각 노드 형식에는 5개의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-108">Each node type has five nodes each.</span></span>

![두 가지 노드 유형이 있는 클러스터의 스크린 샷][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="92764-110">노드에 VM 크기 조정 설정 인스턴스 매핑</span><span class="sxs-lookup"><span data-stu-id="92764-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="92764-111">위에서 볼 수 있듯이 VM 크기 조정 설정 인스턴스는 0에서 시작하여 커집니다.</span><span class="sxs-lookup"><span data-stu-id="92764-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="92764-112">이름에 번호 매기기를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="92764-113">예를 들어 BackEnd_0은 백 엔드 VM 확장 집합의 인스턴스 0입니다.</span><span class="sxs-lookup"><span data-stu-id="92764-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="92764-114">이 특정 VM 크기 조정 설정에는 BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 및 BackEnd_4라는 5개의 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="92764-115">VM 크기 조정 설정을 확대하는 경우 새 인스턴스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="92764-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="92764-116">새 VM 크기 조정 설정 인스턴스 이름은 일반적으로 VM 크기 조정 설정 이름 + 다음 인스턴스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="92764-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="92764-117">이 예제에서는 BackEnd_5입니다.</span><span class="sxs-lookup"><span data-stu-id="92764-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="92764-118">각 노드 형식/VM 크기 조정 집합에 VM 크기 조정 설정 부하 분산 장치 매핑</span><span class="sxs-lookup"><span data-stu-id="92764-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="92764-119">포털에서 클러스터를 배포했거나 제공한 샘플 Resource Manager 템플릿을 사용한 경우 리소스 그룹에서 모든 리소스의 목록을 가져올 때 각 VM 확장 집합 또는 노드 유형에 대한 부하 분산 장치가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92764-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="92764-120">이름은 **LB-&lt;NodeType name&gt;**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="92764-121">예를 들어 이 스크린 샷에 표시된 대로 LB-sfcluster4doc-0입니다.</span><span class="sxs-lookup"><span data-stu-id="92764-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![리소스][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="92764-123">VM 크기 조정 설정 인스턴스 또는 클러스터 노드에 원격 연결</span><span class="sxs-lookup"><span data-stu-id="92764-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="92764-124">클러스터에 정의된 모든 노드 유형은 별도의 VM 확장 집합으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="92764-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="92764-125">노드 유형이 독립적으로 확장 또는 축소될 수 있고 VM SKU로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="92764-126">단일 VM 인스턴스와 달리 VM 크기 조정 설정 인스턴스는 고유한 가상 IP 주소를 가져오지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="92764-127">따라서 특정 인스턴스에 원격으로 연결하는 데 사용할 수 있는 IP 주소 및 포트를 찾기란 조금 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="92764-128">찾기 위해 수행할 수 있는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="92764-129">1단계: 노드 형식에 대한 가상 IP 주소 및 RDP에 대한 인바운드 NAT 규칙 찾기</span><span class="sxs-lookup"><span data-stu-id="92764-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="92764-130">이를 가져오려면 **Microsoft.Network/loadBalancers**에 대한 리소스 정의의 일부로 정의된 인바운드 NAT 규칙 값을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="92764-131">포털에서 부하 분산 장치 블레이드 및 **설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="92764-133">**설정**에서 **인바운드 NAT 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="92764-134">이제 첫 번째 VM 크기 조정 설정 인스턴스에 원격으로 연결하는 데 사용할 수 있는 IP 주소 및 포트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="92764-135">아래 스크린샷에서 **104.42.106.156** 및 **3389**입니다.</span><span class="sxs-lookup"><span data-stu-id="92764-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="92764-137">2단계: 특정 VM 크기 조정 설정 인스턴스/노드에 원격 연결하는 데 사용할 수 있는 포트 찾기</span><span class="sxs-lookup"><span data-stu-id="92764-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="92764-138">이 문서의 앞부분에서 VM 크기 조정 설정 인스턴스를 노드에 매핑하는 방법에 대해 이야기했습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="92764-139">정확한 포트를 찾기 위해 그 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="92764-140">포트는 VM 확장 집합 인스턴스의 오름차순으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="92764-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="92764-141">따라서 프런트 엔드 노드 유형에 대한 예제에서 5개의 인스턴스 각각에 대한 포트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="92764-142">이제 VM 확장 집합 인스턴스에 동일한 매핑을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="92764-143">**VM 확장 집합 인스턴스**</span><span class="sxs-lookup"><span data-stu-id="92764-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="92764-144">**포트**</span><span class="sxs-lookup"><span data-stu-id="92764-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="92764-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="92764-145">FrontEnd_0</span></span> |<span data-ttu-id="92764-146">3389</span><span class="sxs-lookup"><span data-stu-id="92764-146">3389</span></span> |
| <span data-ttu-id="92764-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="92764-147">FrontEnd_1</span></span> |<span data-ttu-id="92764-148">3390</span><span class="sxs-lookup"><span data-stu-id="92764-148">3390</span></span> |
| <span data-ttu-id="92764-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="92764-149">FrontEnd_2</span></span> |<span data-ttu-id="92764-150">3391</span><span class="sxs-lookup"><span data-stu-id="92764-150">3391</span></span> |
| <span data-ttu-id="92764-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="92764-151">FrontEnd_3</span></span> |<span data-ttu-id="92764-152">3392</span><span class="sxs-lookup"><span data-stu-id="92764-152">3392</span></span> |
| <span data-ttu-id="92764-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="92764-153">FrontEnd_4</span></span> |<span data-ttu-id="92764-154">3393</span><span class="sxs-lookup"><span data-stu-id="92764-154">3393</span></span> |
| <span data-ttu-id="92764-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="92764-155">FrontEnd_5</span></span> |<span data-ttu-id="92764-156">3394</span><span class="sxs-lookup"><span data-stu-id="92764-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="92764-157">3단계: 특정 VM 크기 조정 설정 인스턴스에 원격 연결</span><span class="sxs-lookup"><span data-stu-id="92764-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="92764-158">아래 스크린샷에서 원격 데스크톱 연결을 사용하여 FrontEnd_1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="92764-160">RDP 포트 범위 값을 변경하는 방법</span><span class="sxs-lookup"><span data-stu-id="92764-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="92764-161">클러스터 배포 전에</span><span class="sxs-lookup"><span data-stu-id="92764-161">Before cluster deployment</span></span>
<span data-ttu-id="92764-162">Resource Manager 템플릿을 사용하여 클러스터를 설정하는 경우 **inboundNatPools**에서 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="92764-163">**Microsoft.Network/loadBalancers**에 대한 리소스 정의로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="92764-164">여기서 **inboundNatPools**에 대한 설명을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="92764-165">*frontendPortRangeStart* 및 *frontendPortRangeEnd* 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="92764-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="92764-167">클러스터 배포 후에</span><span class="sxs-lookup"><span data-stu-id="92764-167">After cluster deployment</span></span>
<span data-ttu-id="92764-168">조금 더 복잡하고 VM이 재활용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92764-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="92764-169">이제 Azure PowerShell을 사용하여 새 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="92764-170">컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="92764-171">이전에 수행한 적이 없는 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="92764-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="92764-172">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-172">Sign in to your Azure account.</span></span> <span data-ttu-id="92764-173">Powershell이 어떤 이유로 인해 실패하면 Azure PowerShell이 올바르게 설치되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="92764-174">부하 분산 장치에 대한 자세한 내용을 보려면 다음을 실행하고 **inboundNatPools**에 대한 설명에서 값이 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="92764-175">*frontendPortRangeEnd* 및 *frontendPortRangeStart*를 원하는 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92764-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="92764-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92764-176">Next steps</span></span>
* [<span data-ttu-id="92764-177">"어디에나 배포" 기능의 개요 및 Azure 관리된 클러스터와 비교</span><span class="sxs-lookup"><span data-stu-id="92764-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="92764-178">클러스터 보안</span><span class="sxs-lookup"><span data-stu-id="92764-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="92764-179"> 서비스 패브릭 SDK 및 시작</span><span class="sxs-lookup"><span data-stu-id="92764-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
