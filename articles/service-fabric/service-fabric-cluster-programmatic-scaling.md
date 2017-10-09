---
title: "서비스 패브릭 프로그래밍 방식으로 배율을 aaaAzure | Microsoft Docs"
description: "확장 또는 축소 하는 Azure 서비스 패브릭 클러스터 toocustom 트리거에 따라 프로그래밍 방식으로,"
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
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="f657d-103">프로그래밍 방식으로 Service Fabric 클러스터의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f657d-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="f657d-104">Azure에서 Service Fabric 클러스터의 크기를 조정하는 방법에 대한 기본적인 내용은 [클러스터 크기 조정](./service-fabric-cluster-scale-up-down.md)의 문서에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="f657d-105">이 문서에서는 가상 컴퓨터 확장 집합 위에 Service Fabric 클러스터를 구축하고 수동으로 또는 자동 크기 조정 규칙을 사용하여 규모를 조정하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="f657d-106">이 문서에서는 고급 시나리오를 위해 Azure 크기 조정 작업을 프로그래밍 방식으로 조정하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="f657d-107">프로그래밍 방식으로 크기를 조정하는 이유</span><span class="sxs-lookup"><span data-stu-id="f657d-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="f657d-108">여러 시나리오에서 수동으로 또는 자동 크기 조정 규칙을 통해 크기를 조정해도 아무 문제 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="f657d-109">다른 시나리오에서는 하지만 하지 못할 수 있습니다 hello 오른쪽 맞춤 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="f657d-110">가능한 단점 toothese 접근 방식을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="f657d-111">toolog 및 명시적으로 작업을 크기 조정 요청 필요 수동으로 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="f657d-112">크기 조정 작업을 자주 또는 예기치 않은 시점에 수행해야 하는 경우에는 이 방법이 좋지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="f657d-113">가상 컴퓨터 크기 집합 인스턴스를 제거 하는 자동 크기 조정 규칙을은 제거 하지 마십시오 자동으로 해당 노드에 대 한 지식이 hello 연결 된 서비스 패브릭 클러스터에서 hello 노드 형식에는 내구성 수준의 실버 또는 "gold".</span><span class="sxs-lookup"><span data-stu-id="f657d-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="f657d-114">자동 크기 조정 규칙 hello에 크기 집합 수준에서 (아닌 hello 서비스 패브릭 수준) 작업을 하기 때문에 자동 크기 조정 규칙 정상적으로 종료 하지 않고 서비스 패브릭 노드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="f657d-115">이 강제 노드 제거는 규모 감축 작업 후 'ghost' Service Fabric 노드 상태를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="f657d-116">개인 (또는 서비스) tooperiodically hello 서비스 패브릭 클러스터에서 제거 된 노드 상태를 정리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="f657d-117">내구성 수준이 Gold 또는 Silver인 노드 유형은 제거된 노드를 자동으로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="f657d-118">자동 크기 조정 규칙이 지원되는 [여러 메트릭](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)이 있지만 아직은 제한된 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="f657d-119">이 집합에 포함되지 않는 일부 메트릭을 기반으로 하는 크기 조정이 필요한 시나리오의 경우 자동 크기 조정 규칙은 좋은 옵션이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="f657d-120">이러한 제한 사항에 따라, 지정할 수 있습니다 tooimplement 더 사용자 지정 된 자동 크기 조정 모델.</span><span class="sxs-lookup"><span data-stu-id="f657d-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="f657d-121">크기 조정 API</span><span class="sxs-lookup"><span data-stu-id="f657d-121">Scaling APIs</span></span>
<span data-ttu-id="f657d-122">Azure Api 가상 컴퓨터 크기 집합 및 서비스 패브릭 클러스터와 응용 프로그램 tooprogrammatically 작업 수 있는 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="f657d-123">자동 크기 조정 옵션을 기존 시나리오에 대해 작동 하지 않으면 이러한 Api 크기 조정 논리를 사용자 지정 가능한 tooimplement 만드세요.</span><span class="sxs-lookup"><span data-stu-id="f657d-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="f657d-124">이 ' 홈-수행할 ' 자동 크기 조정 하는 한 가지 방법은 tooimplementing 기능 tooadd는 새 상태 비저장 서비스 toohello 서비스 패브릭 응용 프로그램 toomanage 작업 크기 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="f657d-125">Hello 서비스 내에서 `RunAsync` 메서드를 트리거 집합을 확인할 수 크기 조정 (최대 클러스터 크기 같은 매개 변수 검사 및 cooldowns 확장 포함)이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="f657d-126">가상 컴퓨터 크기 조정 설정 상호 작용에 사용 되는 API hello (두 toocheck hello 현재 가상 컴퓨터 인스턴스 수 및 toomodify 것)는 hello [fluent Azure 관리 계산 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="f657d-127">hello fluent 계산 라이브러리는 가상 컴퓨터 크기 집합 상호 작용 하기 위한 사용 하기 쉬운 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="f657d-128">사용 하 여 hello 서비스 패브릭 클러스터 자체와 toointeract [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient)합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="f657d-129">코드 크기를 조정 하는 hello 서비스로 toorun 필요 하지 않은 물론, hello 클러스터 toobe 배율 조정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="f657d-130">둘 다 `IAzure` 및 `FabricClient` tootheir 관련 Azure 리소스 원격으로 연결할 수, 콘솔 응용 프로그램 또는 외부 hello 서비스 패브릭 응용 프로그램에서 실행 되는 Windows 서비스 hello 서비스 조정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="f657d-131">자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="f657d-131">Credential management</span></span>
<span data-ttu-id="f657d-132">크기 조정 서비스 toohandle 작성의 한 가지 문제는 hello service가 대화형 로그인 없이 수 tooaccess 눈금 집합 리소스를 가상 컴퓨터를 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="f657d-133">액세스 hello 서비스 패브릭 클러스터 경우에 쉽게 자체 서비스 패브릭 응용 프로그램을 수정 하는 hello 서비스 크기 조정 되지만 자격 증명이 필요한 tooaccess hello 크기 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="f657d-134">사용할 수 있습니다에 toolog는 [서비스 사용자](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) hello를 사용 하 여 만든 [Azure CLI 2.0](https://github.com/azure/azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="f657d-135">서비스 사용자는 단계를 수행 하는 hello로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="f657d-136">Azure CLI toohello 로그인 (`az login`) 액세스 toohello 가상 컴퓨터 크기를 가진 사용자로 설정</span><span class="sxs-lookup"><span data-stu-id="f657d-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="f657d-137">Hello 서비스와 사용자 만들기`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="f657d-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="f657d-138">Hello appId (다른 곳에서 '클라이언트 ID' 함), 이름, 암호 및 나중에 사용할 테 넌 트의 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="f657d-139">구독 ID도 필요하며 `az account list`를 사용하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="f657d-140">hello fluent 계산 라이브러리 하 여 로그인이 자격 증명 다음과 같습니다 (참고와 같은 핵심 fluent Azure 형식 `IAzure` hello에 [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) 패키지):</span><span class="sxs-lookup"><span data-stu-id="f657d-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="f657d-141">로그인되면 `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`를 통해 확장 집합 인스턴스 수를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="f657d-142">확장</span><span class="sxs-lookup"><span data-stu-id="f657d-142">Scaling out</span></span>
<span data-ttu-id="f657d-143">Azure SDK 계산 fluent hello를 사용 하 여, 인스턴스를 몇 번 호출-를 사용 하 여 설정 toohello 가상 컴퓨터 크기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="f657d-144">또는 PowerShell cmdlet을 통해 가상 컴퓨터 확장 집합 크기를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="f657d-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)hello 가상 컴퓨터 크기 조정 설정 개체를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="f657d-146">hello 현재 용량 hello에 저장 될 `.sku.capacity` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="f657d-147">Hello로 Azure에서 설정 하는 hello 가상 컴퓨터 크기를 업데이트할 수 값 원하는 hello 용량 toohello 변경 후 [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="f657d-148">인스턴스를 설정 하는 눈금 추가 hello 눈금 서식 파일을 설정 하므로 새 서비스 패브릭 노드 포함 된 모든 필요한 toostart 속도가 노드를 수동으로 추가할 때는 확장 tooautomatically 새 인스턴스 toohello 서비스 패브릭 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="f657d-149">규모 감축</span><span class="sxs-lookup"><span data-stu-id="f657d-149">Scaling in</span></span>

<span data-ttu-id="f657d-150">배율에 비슷한 tooscaling 아웃 합니다. 변경 내용이 거의 hello 실제 가상 컴퓨터 크기 집합 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="f657d-151">하지만 앞서 살펴본 것처럼 Service Fabric은 제거된 노드 중에서 내구성 수준이 Gold 또는 Silver인 노드만 자동으로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="f657d-152">Hello 동 내구성 눈금의 경우 서비스 패브릭 hello로 필요한 toointeract 이므로 클러스터 제거 hello 노드 toobe 아래로 tooshut 및 tooremove의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="f657d-153">종료는 hello 노드 toobe를 찾기 위한 hello 노드를 준비 (가장 최근에 추가 된 노드 hello)를 제거 및 비활성화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="f657d-154">비-시드 노드의 경우 `NodeInstanceId`를 비교하여 보다 최근의 노드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="f657d-155">주의 *시드* 노드 tooalways 큰 인스턴스 Id를 먼저 제거 하는 hello 규칙을 따르는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="f657d-156">제거 하는 hello 노드 toobe 발견 되 면 비활성화할 수 있습니다 및 동일한 hello 제거를 사용 하 여 `FabricClient` 인스턴스와 hello `IAzure` 앞에서 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f657d-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
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

<span data-ttu-id="f657d-157">스크립팅 방식을 선호하는 경우 여기에서 확장과 마찬가지로 가상 컴퓨터 확장 집합 용량을 수정하기 위한 PowerShell cmdlet을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="f657d-158">Hello 가상 컴퓨터 인스턴스가 제거 되 면 서비스 패브릭 노드 상태를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="f657d-159">잠재적 단점</span><span class="sxs-lookup"><span data-stu-id="f657d-159">Potential drawbacks</span></span>

<span data-ttu-id="f657d-160">Hello 앞에 코드 조각에서에서 볼 수 있듯이, 크기 조정 서비스를 만들면 hello 가장 높은 수준의 제어 및 사용자 응용 프로그램을 통해 크기 조정 동작 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="f657d-161">응용 프로그램을 규모 감축 또는 규모 확장하는 시기와 방법을 정교하게 제어해야 하는 시나리오에는 이 방법이 유용할 수 있습니다. 그러나 이 제어 방법은 코드가 복잡해지는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="f657d-162">이 방식을 사용 하 여 tooown 특수 코드 크기를 조정 해야 한다는 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="f657d-163">Service Fabric 크기 조정에 접근하는 방식은 시나리오에 달렸습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="f657d-164">확장을 공통 없으면 hello 기능 tooadd / 제거를 노드 수동으로 만으로도 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="f657d-165">자동 크기 조정 규칙 및 hello 기능 tooscale를 프로그래밍 방식으로 노출 하는 Sdk는 보다 복잡 한 시나리오에 대 한 강력한 대체 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f657d-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f657d-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f657d-166">Next steps</span></span>

<span data-ttu-id="f657d-167">고유한 자동 크기 조정 논리를 구현 하기 시작 했습니다 tooget 숙지 hello 개념 및 유용한 Api:</span><span class="sxs-lookup"><span data-stu-id="f657d-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="f657d-168">수동으로 또는 자동 크기 조정 규칙을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f657d-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="f657d-169">[.NET용 Fluent Azure Management 라이브러리](https://github.com/Azure/azure-sdk-for-net/tree/Fluent)(Service Fabric 클러스터의 기본 가상 가상 컴퓨터 확장 집합과 상호 작용하는 데 유용함)</span><span class="sxs-lookup"><span data-stu-id="f657d-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="f657d-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient)(Service Fabric 클러스터 및 그 노드와 상호 작용하는 데 유용함)</span><span class="sxs-lookup"><span data-stu-id="f657d-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
