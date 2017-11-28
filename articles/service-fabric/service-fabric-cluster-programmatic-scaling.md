---
title: "프로그래밍 방식으로 Azure Service Fabric 크기 조정 | Microsoft Docs"
description: "사용자 지정 트리거에 따라 Azure Service Fabric 클러스터를 프로그래밍 방식으로 규모 확장 또는 규모 감축"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="306f8-103">프로그래밍 방식으로 Service Fabric 클러스터의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="306f8-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="306f8-104">Azure에서 Service Fabric 클러스터의 크기를 조정하는 방법에 대한 기본적인 내용은 [클러스터 크기 조정](./service-fabric-cluster-scale-up-down.md)의 문서에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="306f8-105">이 문서에서는 가상 컴퓨터 확장 집합 위에 Service Fabric 클러스터를 구축하고 수동으로 또는 자동 크기 조정 규칙을 사용하여 규모를 조정하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="306f8-106">이 문서에서는 고급 시나리오를 위해 Azure 크기 조정 작업을 프로그래밍 방식으로 조정하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="306f8-107">프로그래밍 방식으로 크기를 조정하는 이유</span><span class="sxs-lookup"><span data-stu-id="306f8-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="306f8-108">여러 시나리오에서 수동으로 또는 자동 크기 조정 규칙을 통해 크기를 조정해도 아무 문제 없습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="306f8-109">하지만 일부 시나리오에서는 좋은 방법이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="306f8-110">이러한 접근 방식의 잠재적 단점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="306f8-111">수동으로 크기를 조정하려면 로그인하여 크기 조정 작업을 명시적으로 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="306f8-112">크기 조정 작업을 자주 또는 예기치 않은 시점에 수행해야 하는 경우에는 이 방법이 좋지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="306f8-113">자동 크기 조정 규칙은 가상 컴퓨터 확장 집합에서 인스턴스를 제거할 때 노드 형식의 내구성 수준이 Silver 또는 Gold가 아닌 한 연결된 Service Fabric 클러스터에서 해당 노드의 지식을 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="306f8-114">자동 크기 조정 규칙은 Service Fabric 수준이 아닌 확장 집합 수준에서 작동하기 때문에 Service Fabric 노드를 정상적으로 종료하지 않아도 자동 크기 조정 규칙이 Service Fabric 노드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="306f8-115">이 강제 노드 제거는 규모 감축 작업 후 'ghost' Service Fabric 노드 상태를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="306f8-116">개인(또는 서비스)은 Service Fabric 클러스터에서 제거된 노드 상태를 주기적으로 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="306f8-117">내구성 수준이 Gold 또는 Silver인 노드 유형은 제거된 노드를 자동으로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="306f8-118">자동 크기 조정 규칙이 지원되는 [여러 메트릭](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)이 있지만 아직은 제한된 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="306f8-119">이 집합에 포함되지 않는 일부 메트릭을 기반으로 하는 크기 조정이 필요한 시나리오의 경우 자동 크기 조정 규칙은 좋은 옵션이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="306f8-120">이러한 제한에 따라 보다 사용자 지정된 자동 크기 조정 모델을 구현하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="306f8-121">크기 조정 API</span><span class="sxs-lookup"><span data-stu-id="306f8-121">Scaling APIs</span></span>
<span data-ttu-id="306f8-122">응용 프로그램이 가상 컴퓨터 확장 집합 및 Service Fabric 클러스터를 프로그래밍 방식으로 작업할 수 있는 Azure API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="306f8-123">기존 자동 크기 조정 옵션이 시나리오에 적합하지 않은 경우 이러한 API를 사용하여 사용자 지정 크기 조정 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="306f8-124">이 '홈 수행 '수제작' 자동 크기 조정 기능을 구현하는 한 가지 방법은 크기 조정 작업을 관리하는 새로운 상태 비저장 서비스를 Service Fabric 응용 프로그램에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="306f8-125">서비스의 `RunAsync` 메서드 내에서 트리거 집합은 크기 조정이 필요한지 여부(최대 클러스터 크기 및 크기 조정 휴지 시간 같은 매개 변수 확인 포함)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="306f8-126">가상 컴퓨터 확장 집합 상호 작용(현재 가상 컴퓨터 인스턴스의 수를 확인하고 수정하는 작업 포함)에 사용되는 API는 [fluent Azure Management Compute 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/)입니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="306f8-127">fluent compute 라이브러리는 가상 컴퓨터 확장 집합과 상호 작용하는 간편한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="306f8-128">Service Fabric 클러스터 자체와 상호 작용하려면 [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="306f8-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="306f8-129">물론 크기를 조정하기 위해 클러스터에서 크기 조정 코드를 서비스로 실행할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="306f8-130">`IAzure` 및 `FabricClient`는 각각 연결된 Azure 리소스에 원격으로 연결하기 때문에 Service Fabric 응용 프로그램 외부에서 실행되는 콘솔 응용 프로그램 또는 Windows 서비스는 손쉽게 크기 조정 서비스가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="306f8-131">자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="306f8-131">Credential management</span></span>
<span data-ttu-id="306f8-132">크기 조정을 처리하는 서비스를 작성할 때 마주치는 한 가지 어려움은 대화형 로그인 없이 서비스가 가상 컴퓨터 확장 집합에 액세스할 수 있어야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="306f8-133">크기 조정 서비스가 자체 Service Fabric 응용 프로그램을 수정하는 경우 Service Fabric 클러스터에 손쉽게 액세스할 수 있지만 자격 증명이 확장 집합에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="306f8-134">로그인하려면 [Azure CLI 2.0](https://github.com/azure/azure-cli)으로 만든 [서비스 주체](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure)를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="306f8-135">서비스 주체는 다음 단계에 따라 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="306f8-136">가상 컴퓨터 확장 집합에 액세스할 수 있는 사용자로 Azure CLI(`az login`)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="306f8-137">`az ad sp create-for-rbac`을 사용하여 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="306f8-138">나중에 사용할 수 있도록 appId(다른 곳에서는 'client ID'라고도 함), 이름, 암호, 테넌트를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="306f8-139">구독 ID도 필요하며 `az account list`를 사용하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="306f8-140">다음과 같이 자격 증명을 사용하여 Fluent 계산 라이브러리에 로그인할 수 있습니다(`IAzure`와 같은 핵심 Fluent Azure 형식은 [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) 패키지에 있음).</span><span class="sxs-lookup"><span data-stu-id="306f8-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="306f8-141">로그인되면 `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`를 통해 확장 집합 인스턴스 수를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="306f8-142">확장</span><span class="sxs-lookup"><span data-stu-id="306f8-142">Scaling out</span></span>
<span data-ttu-id="306f8-143">fluent Azure compute SDK를 사용하면 호출 몇 번으로 가상 컴퓨터 확장 집합에 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="306f8-144">또는 PowerShell cmdlet을 통해 가상 컴퓨터 확장 집합 크기를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="306f8-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)는 가상 컴퓨터 확장 집합 개체를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="306f8-146">현재 용량은 `.sku.capacity` 속성에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="306f8-147">용량을 원하는 값으로 변경한 후 Azure에서 [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) 명령을 통해 가상 컴퓨터 확장 집합을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="306f8-148">노드를 수동으로 추가하는 경우 확장 집합 인스턴스만 추가하면 새로운 Service Fabric 노드를 시작할 수 있습니다. 확장 집합 템플릿에는 새 인스턴스를 자동으로 Service Fabric 클러스터에 조인하는 확장 기능이 포함되어 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="306f8-149">규모 감축</span><span class="sxs-lookup"><span data-stu-id="306f8-149">Scaling in</span></span>

<span data-ttu-id="306f8-150">규모 감축은 규모 확장과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="306f8-151">실제 가상 컴퓨터 확장 집합 변경은 실질적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="306f8-152">하지만 앞서 살펴본 것처럼 Service Fabric은 제거된 노드 중에서 내구성 수준이 Gold 또는 Silver인 노드만 자동으로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="306f8-153">따라서 내구성 수준이 Bronze인 규모 감축에서는 제거할 노드를 종료한 후 상태를 제거하도록 Service Fabric 클러스터와 상호 작용이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="306f8-154">종료할 노드를 준비하는 과정에는 제거할 노드(가장 최근에 추가된 노드)를 찾아서 비활성화하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="306f8-155">비-시드 노드의 경우 `NodeInstanceId`를 비교하여 보다 최근의 노드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="306f8-156">*시드* 노드는 더 큰 인스턴스 ID가 먼저 제거되는 규칙을 따르지 않는 경우도 있다는 점에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="306f8-157">제거할 노드를 찾았으면 이전과 동일한 `FabricClient` 인스턴스 및 `IAzure` 인스턴스를 사용하여 노드를 비활성화하고 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="306f8-158">스크립팅 방식을 선호하는 경우 여기에서 확장과 마찬가지로 가상 컴퓨터 확장 집합 용량을 수정하기 위한 PowerShell cmdlet을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="306f8-159">가상 컴퓨터 인스턴스가 제거되면 Service Fabric 노드 상태를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="306f8-160">잠재적 단점</span><span class="sxs-lookup"><span data-stu-id="306f8-160">Potential drawbacks</span></span>

<span data-ttu-id="306f8-161">위의 코드 조각에서 살펴본 것처럼 사용자 고유의 크기 조정 서비스를 만들면 응용 프로그램 동작을 최대한 원하는 대로 제어하고 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="306f8-162">응용 프로그램을 규모 감축 또는 규모 확장하는 시기와 방법을 정교하게 제어해야 하는 시나리오에는 이 방법이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="306f8-163">그러나 이 제어 방법은 코드가 복잡해지는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="306f8-164">이 방법을 사용하려면 특수한 크기 조정 코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="306f8-165">Service Fabric 크기 조정에 접근하는 방식은 시나리오에 달렸습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="306f8-166">크기 조정을 자주 하지 않는다면 노드를 수동으로 추가 또는 제거할 수만 있으면 충분할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="306f8-167">좀 더 복잡한 시나리오의 경우 프로그래밍 방식으로 확장하는 기능을 노출하는 자동 크기 조정 규칙과 SDK가 강력한 대안이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="306f8-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="306f8-168">Next steps</span></span>

<span data-ttu-id="306f8-169">사용자 고유의 자동 크기 조정 논리를 구현하려면 먼저 다음과 같은 개념과 유용한 API부터 숙지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="306f8-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="306f8-170">수동으로 또는 자동 크기 조정 규칙을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="306f8-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="306f8-171">[.NET용 Fluent Azure Management 라이브러리](https://github.com/Azure/azure-sdk-for-net/tree/Fluent)(Service Fabric 클러스터의 기본 가상 가상 컴퓨터 확장 집합과 상호 작용하는 데 유용함)</span><span class="sxs-lookup"><span data-stu-id="306f8-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="306f8-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient)(Service Fabric 클러스터 및 그 노드와 상호 작용하는 데 유용함)</span><span class="sxs-lookup"><span data-stu-id="306f8-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
