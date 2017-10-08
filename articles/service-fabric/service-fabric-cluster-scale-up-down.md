---
title: "in 또는 out aaaScale 서비스 패브릭 클러스터 | Microsoft Docs"
description: "각 노드 형식/가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 규칙을 설정 하 여 서비스 패브릭 클러스터 in 또는 out toomatch 요청 크기를 조정 합니다. 추가 또는 노드 tooa 서비스 패브릭 클러스터를 제거 합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a><span data-ttu-id="22ef4-104">자동 크기 조정 규칙을 사용하여 서비스 패브릭 클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="22ef4-104">Scale a Service Fabric cluster in or out using auto-scale rules</span></span>
<span data-ttu-id="22ef4-105">가상 컴퓨터 크기 집합은 toodeploy를 사용 하 고 집합으로 가상 컴퓨터의 컬렉션을 관리할 수 있는 한 Azure 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-105">Virtual machine scale sets are an Azure compute resource that you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="22ef4-106">Service Fabric 클러스터에 정의된 모든 노드 형식은 별도의 가상 컴퓨터 확장 집합으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-106">Every node type that is defined in a Service Fabric cluster is set up as a separate Virtual Machine scale set.</span></span> <span data-ttu-id="22ef4-107">각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-107">Each node type can then be scaled in or out independently, have different sets of ports open, and can have different capacity metrics.</span></span> <span data-ttu-id="22ef4-108">Hello에 대 한 자세한 설명 [서비스 패브릭 nodetypes](service-fabric-cluster-nodetypes.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="22ef4-108">Read more about it in hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) document.</span></span> <span data-ttu-id="22ef4-109">Hello 백 엔드에 가상 컴퓨터 크기 집합의 클러스터 서비스 패브릭 노드 유형에 hello 하므로 각 노드 형식/가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 규칙을 tooset이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-109">Since hello Service Fabric node types in your cluster are made of Virtual Machine scale sets at hello backend, you need tooset up auto-scale rules for each node type/Virtual Machine scale set.</span></span>

> [!NOTE]
> <span data-ttu-id="22ef4-110">구독에 새 Vm이이 클러스터를 구성 하는 hello 충분 한 코어가 tooadd가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-110">Your subscription must have enough cores tooadd hello new VMs that make up this cluster.</span></span> <span data-ttu-id="22ef4-111">모델 유효성 검사 없이 현재 적중 hello 할당량 한도 경우 배포 시간 오류를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-111">There is no model validation currently, so you get a deployment time failure, if any of hello quota limits are hit.</span></span>
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a><span data-ttu-id="22ef4-112">Hello 노드 유형/가상 컴퓨터 크기 집합 tooscale 선택</span><span class="sxs-lookup"><span data-stu-id="22ef4-112">Choose hello node type/Virtual Machine scale set tooscale</span></span>
<span data-ttu-id="22ef4-113">현재 hello 포털을 사용 하 여 가상 컴퓨터 크기 집합에 대 한 hello 자동 크기 조정 규칙 수 toospecify 없는, 따라서 응 Azure PowerShell (1.0 이상) toolist hello 노드 형식을 사용 하 고 자동 크기 조정 규칙 toothem를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-113">Currently, you are not able toospecify hello auto-scale rules for Virtual Machine scale sets using hello portal, so let us use Azure PowerShell (1.0+) toolist hello node types and then add auto-scale rules toothem.</span></span>

<span data-ttu-id="22ef4-114">가상 컴퓨터 크기 집합 하의 tooget hello 목록 hello 다음 cmdlet을 실행 하 여 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-114">tooget hello list of Virtual Machine scale set that make up your cluster, run hello following cmdlets:</span></span>

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a><span data-ttu-id="22ef4-115">Hello 노드 유형/가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="22ef4-115">Set auto-scale rules for hello node type/Virtual Machine scale set</span></span>
<span data-ttu-id="22ef4-116">클러스터에 여러 노드 형식, (in 또는 out) tooscale 되도록 설정 하는 각 노드 형식/가상 컴퓨터 크기에 대해이 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-116">If your cluster has multiple node types, then repeat this for each node types/Virtual Machine scale sets that you want tooscale (in or out).</span></span> <span data-ttu-id="22ef4-117">계정 hello 노드 수를 고려 자동 크기 조정 설정 하기 전에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-117">Take into account hello number of nodes that you must have before you set up auto-scaling.</span></span> <span data-ttu-id="22ef4-118">hello 기본 노드 형식에 대 한 해야 하는 노드의 최소 수 hello 선택한 hello 안정성 수준에 의해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-118">hello minimum number of nodes that you must have for hello primary node type is driven by hello reliability level you have chosen.</span></span> <span data-ttu-id="22ef4-119">[안정성 수준](service-fabric-cluster-capacity.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="22ef4-119">Read more about [reliability levels](service-fabric-cluster-capacity.md).</span></span>

> [!NOTE]
> <span data-ttu-id="22ef4-120">Hello 최소한 hello 클러스터 불안정 하거나 중단 시킬 보다 hello 주 노드 유형 tooless 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-120">Scaling down hello primary node type tooless than hello minimum number make hello cluster unstable or bring it down.</span></span> <span data-ttu-id="22ef4-121">이 hello 시스템 서비스 및 응용 프로그램에 대 한 데이터가 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-121">This could result in data loss for your applications and for hello system services.</span></span>
> 
> 

<span data-ttu-id="22ef4-122">현재 hello 자동 크기 조정 기능 하지 hello 로드 응용 프로그램 수 tooService 패브릭 보고 수에 의해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-122">Currently hello auto-scale feature is not driven by hello loads that your applications may be reporting tooService Fabric.</span></span> <span data-ttu-id="22ef4-123">따라서이 시간 hello에 자동 크기 조정 얻게 각 hello 가상 컴퓨터 크기 조정 설정 인스턴스에 의해 발생 하는 hello 성능 카운터에 의해 좌우 순수 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-123">So at this time hello auto-scale you get is purely driven by hello performance counters that are emitted by each of hello Virtual Machine scale set instances.</span></span>  

<span data-ttu-id="22ef4-124">다음이 지침에 따라 [각 가상 컴퓨터 크기 집합에 대 한 자동 크기 조정을 tooset](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-124">Follow these instructions [tooset up auto-scale for each Virtual Machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="22ef4-125">시나리오 축소 노드 형식에 "gold" 또는 실버 내구성 수준 해야 toocall hello [제거 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) hello 적합 한 노드 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-125">In a scale down scenario, unless your node type has a durability level of Gold or Silver you need toocall hello [Remove-ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) with hello appropriate node name.</span></span>
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a><span data-ttu-id="22ef4-126">Vm tooa 노드 유형/가상 컴퓨터 크기 집합을 수동으로 추가</span><span class="sxs-lookup"><span data-stu-id="22ef4-126">Manually add VMs tooa node type/Virtual Machine scale set</span></span>
<span data-ttu-id="22ef4-127">Hello 샘플/의 지침에에서 따라 hello [빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) 각 Nodetype에 있는 Vm의 toochange hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-127">Follow hello sample/instructions in hello [quick start template gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello number of VMs in each Nodetype.</span></span> 

> [!NOTE]
> <span data-ttu-id="22ef4-128">Vm의 추가 데 하지 않을 hello 추가 toobe 순간 되므로 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-128">Adding of VMs takes time, so do not expect hello additions toobe instantaneous.</span></span> <span data-ttu-id="22ef4-129">따라서 tooallow hello VM 용량 hello 복제본에 대 한 사용 가능 해지기 전에 10 분 동안에 대 한 시간 내에 잘 tooadd 용량 계획/서비스 인스턴스 tooget 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-129">So plan tooadd capacity well in time, tooallow for over 10 minutes before hello VM capacity is available for hello replicas/ service instances tooget placed.</span></span>
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a><span data-ttu-id="22ef4-130">Hello 주 노드 유형/가상 컴퓨터 크기 집합에서 Vm을 수동으로 제거</span><span class="sxs-lookup"><span data-stu-id="22ef4-130">Manually remove VMs from hello primary node type/Virtual Machine scale set</span></span>
> [!NOTE]
> <span data-ttu-id="22ef4-131">클러스터의 주 노드 종류 hello에서에서 hello 서비스 패브릭 시스템 서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-131">hello service fabric system services run in hello Primary node type in your cluster.</span></span> <span data-ttu-id="22ef4-132">종료 하거나 해당 노드 형식에 있는 인스턴스의 hello 수 축소 안 되므로 어떤 hello 안정성 계층 보다 작은 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-132">So should never shut down or scale down hello number of instances in that node types less than what hello reliability tier warrants.</span></span> <span data-ttu-id="22ef4-133">너무 참조[여기에 안정성 계층에 대 한 내용은 hello](service-fabric-cluster-capacity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-133">Refer too[hello details on reliability tiers here](service-fabric-cluster-capacity.md).</span></span> 
> 
> 

<span data-ttu-id="22ef4-134">Tooexecute 필요한 hello 다음 단계를 한 번에 하나의 VM 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="22ef4-134">You need tooexecute hello following steps one VM instance at a time.</span></span> <span data-ttu-id="22ef4-135">이렇게 하면 hello 시스템 서비스 (및 상태 저장 서비스)에 대 한 toobe 정상적으로 종료를 제거 하는 hello VM 인스턴스 및 다른 노드에서 만든 새 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-135">This allows for hello system services (and your stateful services) toobe shut down gracefully on hello VM instance you are removing and new replicas created on other nodes.</span></span>

1. <span data-ttu-id="22ef4-136">실행 [사용 안 함 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) 의도 'RemoveNode' toodisable hello 노드 (노드 형식에서 가장 높은 인스턴스 hello) tooremove 겠 군요.</span><span class="sxs-lookup"><span data-stu-id="22ef4-136">Run [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) with intent ‘RemoveNode’ toodisable hello node you’re going tooremove (hello highest instance in that node type).</span></span>
2. <span data-ttu-id="22ef4-137">실행 [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake hello 노드에 toodisabled 실제로 전환 하십시오.</span><span class="sxs-lookup"><span data-stu-id="22ef4-137">Run [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake sure that hello node has indeed transitioned toodisabled.</span></span> <span data-ttu-id="22ef4-138">파일이 없으면 hello 노드 해제 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-138">If not, wait until hello node is disabled.</span></span> <span data-ttu-id="22ef4-139">이 단계는 서두를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-139">You cannot hurry this step.</span></span>
3. <span data-ttu-id="22ef4-140">Hello 샘플/의 지침에에서 따라 hello [빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) 해당 Nodetype에 따라 Vm의 toochange hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-140">Follow hello sample/instructions in hello [quick start template gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello number of VMs by one in that Nodetype.</span></span> <span data-ttu-id="22ef4-141">제거 하는 hello 인스턴스는 hello 가장 높은 VM 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-141">hello instance removed is hello highest VM instance.</span></span> 
4. <span data-ttu-id="22ef4-142">단계 1-3 필요에 따라 반복 hello 주 노드 종류에서 어떤 hello 안정성 계층 수행 되도록 하는 보다 작은 인스턴스의 hello 수를 축소 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="22ef4-142">Repeat steps 1 through 3 as needed, but never scale down hello number of instances in hello primary node types less than what hello reliability tier warrants.</span></span> <span data-ttu-id="22ef4-143">너무 참조[여기에 안정성 계층에 대 한 내용은 hello](service-fabric-cluster-capacity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-143">Refer too[hello details on reliability tiers here](service-fabric-cluster-capacity.md).</span></span> 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a><span data-ttu-id="22ef4-144">Hello 기본이 아닌 노드 유형/가상 컴퓨터 크기 집합에서에서 Vm을 수동으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-144">Manually remove VMs from hello non-primary node type/Virtual Machine scale set</span></span>
> [!NOTE]
> <span data-ttu-id="22ef4-145">상태 저장 서비스에 대 한 필요한 특정 개수의 노드 toobe 항상 toomaintain 가용성과 preserve 서비스의 상태를 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-145">For a stateful service, you need a certain number of nodes toobe always up toomaintain availability and preserve state of your service.</span></span> <span data-ttu-id="22ef4-146">Hello 매우 최소에서 hello 수가 hello 파티션/서비스의 노드 같은 toohello 대상 복제본 집합 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-146">At hello very minimum, you need hello number of nodes equal toohello target replica set count of hello partition/service.</span></span> 
> 
> 

<span data-ttu-id="22ef4-147">Hello 필요한 hello 한 번에 하나의 VM 인스턴스 단계를 따라를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-147">You need hello execute hello following steps one VM instance at a time.</span></span> <span data-ttu-id="22ef4-148">이렇게 하면 toobe 정상적으로 종료 hello에 VM 인스턴스를 제거 하는 hello 시스템 서비스 (및 상태 저장 서비스)에 대 한 있고 else where 새 복제본은 생성.</span><span class="sxs-lookup"><span data-stu-id="22ef4-148">This allows for hello system services (and your stateful services) toobe shut down gracefully on hello VM instance you are removing and new replicas created else where.</span></span>

1. <span data-ttu-id="22ef4-149">실행 [사용 안 함 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) 의도 'RemoveNode' toodisable hello 노드 (노드 형식에서 가장 높은 인스턴스 hello) tooremove 겠 군요.</span><span class="sxs-lookup"><span data-stu-id="22ef4-149">Run [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) with intent ‘RemoveNode’ toodisable hello node you’re going tooremove (hello highest instance in that node type).</span></span>
2. <span data-ttu-id="22ef4-150">실행 [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake hello 노드에 toodisabled 실제로 전환 하십시오.</span><span class="sxs-lookup"><span data-stu-id="22ef4-150">Run [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake sure that hello node has indeed transitioned toodisabled.</span></span> <span data-ttu-id="22ef4-151">그렇지 않으면 요 hello 노드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-151">If not wait till hello node is disabled.</span></span> <span data-ttu-id="22ef4-152">이 단계는 서두를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-152">You cannot hurry this step.</span></span>
3. <span data-ttu-id="22ef4-153">Hello 샘플/의 지침에에서 따라 hello [빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) 해당 Nodetype에 따라 Vm의 toochange hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-153">Follow hello sample/instructions in hello [quick start template gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello number of VMs by one in that Nodetype.</span></span> <span data-ttu-id="22ef4-154">이제 hello 가장 높은 VM 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-154">This will now remove hello highest VM instance.</span></span> 
4. <span data-ttu-id="22ef4-155">단계 1-3 필요에 따라 반복 hello 주 노드 종류에서 어떤 hello 안정성 계층 수행 되도록 하는 보다 작은 인스턴스의 hello 수를 축소 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="22ef4-155">Repeat steps 1 through 3 as needed, but never scale down hello number of instances in hello primary node types less than what hello reliability tier warrants.</span></span> <span data-ttu-id="22ef4-156">너무 참조[여기에 안정성 계층에 대 한 내용은 hello](service-fabric-cluster-capacity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-156">Refer too[hello details on reliability tiers here](service-fabric-cluster-capacity.md).</span></span>

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a><span data-ttu-id="22ef4-157">Service Fabric Explorer에서 볼 수 있는 동작</span><span class="sxs-lookup"><span data-stu-id="22ef4-157">Behaviors you may observe in Service Fabric Explorer</span></span>
<span data-ttu-id="22ef4-158">클러스터 hello 수직 확장 서비스 패브릭 탐색기 hello hello 클러스터의 일부인 (가상 컴퓨터 크기는 인스턴스를 설정 하는 데 사용) 하는 노드 수를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-158">When you scale up a cluster hello Service Fabric Explorer will reflect hello number of nodes (Virtual Machine scale set instances) that are part of hello cluster.</span></span>  <span data-ttu-id="22ef4-159">그러나 크기를 조정할 때 다운 클러스터 볼 수를 호출 하지 않으면 비정상 상태에 표시 되는 제거 하는 hello 노드/v M 인스턴스에 [제거 ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) hello 적합 한 노드 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-159">However, when you scale a cluster down you will see hello removed node/VM instance displayed in an unhealthy state unless you call [Remove-ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) with hello appropriate node name.</span></span>   

<span data-ttu-id="22ef4-160">이 동작에 대 한 hello 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-160">Here is hello explanation for this behavior.</span></span>

<span data-ttu-id="22ef4-161">hello 서비스 패브릭 탐색기에 나열 된 노드를 반영 하 고 hello 서비스 패브릭 시스템 서비스의 (FM 특히) hello에 /가 노드 hello 클러스터 수에 대해 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-161">hello nodes listed in Service Fabric Explorer are a reflection of what hello Service Fabric system services (FM specifically) knows about hello number of nodes hello cluster had/has.</span></span> <span data-ttu-id="22ef4-162">가상 컴퓨터 크기 집합 hello 크기를 조정할 때 hello VM이 에서만 삭제 FM 시스템 서비스 여전히 것으로 생각 (있던, 매핑된 toohello 삭제 된 VM) 해당 hello 노드는 다시 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-162">When you scale hello Virtual Machine scale set down, hello VM was deleted but FM system service still thinks that hello node (that was mapped toohello VM that was deleted) will come back.</span></span> <span data-ttu-id="22ef4-163">따라서 서비스 패브릭 탐색기 계속 toodisplay 해당 노드 (하지만 hello 성능 상태는 오류 또는 알 수 없는 일 수 있음).</span><span class="sxs-lookup"><span data-stu-id="22ef4-163">So Service Fabric Explorer continues toodisplay that node (though hello health state may be error or unknown).</span></span>

<span data-ttu-id="22ef4-164">순서 toomake 노드 VM 제거 될 때 제거 되었는지에 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-164">In order toomake sure that a node is removed when a VM is removed, you have two options:</span></span>

1) <span data-ttu-id="22ef4-165">"Gold" 또는 실버 내구성 수준을 선택 (사용 가능한 빨리) 클러스터의 노드 형식을 hello에 대 한를 제공 하는 hello infrastructure 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-165">Choose a durability level of Gold or Silver (available soon) for hello node types in your cluster, which gives you hello infrastructure integration.</span></span> <span data-ttu-id="22ef4-166">다음 자동으로 제거 됩니다 hello 노드 우리의 시스템 (FM) 서비스 상태에서 규모 축소 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="22ef4-166">Which will then automatically remove hello nodes from our system services (FM) state when you scale down.</span></span>
<span data-ttu-id="22ef4-167">너무 참조[hello 내구성 수준 여기에 세부 정보](service-fabric-cluster-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="22ef4-167">Refer too[hello details on durability levels here](service-fabric-cluster-capacity.md)</span></span>

2) <span data-ttu-id="22ef4-168">Hello VM 인스턴스 축소 되어, 해야 toocall hello [제거 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-168">Once hello VM instance has been scaled down, you need toocall hello [Remove-ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="22ef4-169">서비스 패브릭 클러스터 노드 toobe 특정 수를에서 필요한 모든 hello 시간 순서 toomaintain 가용성 및 preserve 상태-참조 tooas "쿼럼을 유지 관리 합니다."</span><span class="sxs-lookup"><span data-stu-id="22ef4-169">Service Fabric clusters require a certain number of nodes toobe up at all hello time in order toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="22ef4-170">따라서 것이 일반적으로 안전 하지 않은 tooshut hello 클러스터의 모든 hello 컴퓨터 다운 처음 수행 하지 않는 한는 [시/도의 전체 백업](service-fabric-reliable-services-backup-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22ef4-170">So, it is typically unsafe tooshut down all hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="22ef4-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22ef4-171">Next steps</span></span>
<span data-ttu-id="22ef4-172">클러스터 용량 계획, 클러스터를 업그레이드 및 서비스를 분할 하는 방법에 대 한 자세한 내용은 tooalso 다음 읽기 hello:</span><span class="sxs-lookup"><span data-stu-id="22ef4-172">Read hello following tooalso learn about planning cluster capacity, upgrading a cluster, and partitioning services:</span></span>

* [<span data-ttu-id="22ef4-173">클러스터 용량 계획</span><span class="sxs-lookup"><span data-stu-id="22ef4-173">Plan your cluster capacity</span></span>](service-fabric-cluster-capacity.md)
* [<span data-ttu-id="22ef4-174">클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="22ef4-174">Cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="22ef4-175">최대 크기를 위해 상태 저장 서비스 분할</span><span class="sxs-lookup"><span data-stu-id="22ef4-175">Partition stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
