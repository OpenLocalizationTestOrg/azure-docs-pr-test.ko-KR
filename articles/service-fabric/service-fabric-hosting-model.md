---
title: "Azure Service Fabric 호스팅 모델 | Microsoft Docs"
description: "배포된 Servic Fabric 서비스 및 서비스 호스트 프로세스 복제본(또는 인스턴스) 간의 관계에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: ca7092a06a9ffce8383ca8bc9f70ce312cdf9de4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-hosting-model"></a><span data-ttu-id="07c32-103">Service Fabric 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="07c32-103">Service Fabric hosting model</span></span>
<span data-ttu-id="07c32-104">이 문서에서는 Service Fabric에서 제공하는 응용 프로그램 호스팅 모델을 간략하게 설명하고 **공유 프로세스** 및 **단독 프로세스** 모델 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-104">This article provides an overview of application hosting models provided by Service Fabric, and describes the differences between the **Shared Process** and **Exclusive Process** models.</span></span> <span data-ttu-id="07c32-105">배포된 응용 프로그램이 Service Fabric 노드에 표시되는 방식과 서비스 복제본(또는 인스턴스) 및 서비스-호스트 프로세스 간의 관계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-105">It describes how a deployed application looks on a Service Fabric node and relationship between replicas (or instances) of the service and the service-host process.</span></span>

<span data-ttu-id="07c32-106">계속 진행하기 전에 [Service Fabric 응용 프로그램 모델][a1]을 숙지하고 다양한 개념 및 개념 간의 관계를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-106">Before proceeding further, make sure that you are familiar with [Service Fabric Application Model][a1] and understand various concepts and relation among them.</span></span> 

> [!NOTE]
> <span data-ttu-id="07c32-107">간단한 설명을 위해 이 문서에서는 명시적으로 언급되지 않은 경우 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-107">In this article, for simplicity, unless explicitly mentioned:</span></span>
>
> - <span data-ttu-id="07c32-108">*복제본* 단어는 모두 상태 저장 서비스 복제본 또는 상태 비저장 서비스 인스턴스를 둘 다 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-108">All uses of word *replica* refers to both a replica of a stateful service or an instance of a statless service.</span></span>
> - <span data-ttu-id="07c32-109">*CodePackage*는 *ServiceType*을 등록하고 해당 *ServiceType*의 서비스 복제본을 호스트하는 *ServiceHost* 프로세스와 동일한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-109">*CodePackage* is treated equivalent to *ServiceHost* process that registers a *ServiceType* and hosts replicas of services of that *ServiceType*.</span></span>
>

<span data-ttu-id="07c32-110">호스팅 모델을 이해하기 위해 한 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-110">To understand the hosting model, let us walk through an example.</span></span> <span data-ttu-id="07c32-111">*ApplicationType* 'MyAppType'에 있는 *ServiceType* 'MyServiceType'은 *ServicePackage* 'MyServicePackage'에 의해 제공되고, 이 서비스 패키지에 있는 *CodePackage* 'MyCodePackage'는 실행 시 *ServiceType* 'MyServiceType'을 등록한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-111">Let us say, we have an *ApplicationType* 'MyAppType' which has a *ServiceType* 'MyServiceType' which is provided by *ServicePackage* 'MyServicePackage' which has a *CodePackage* 'MyCodePackage' which registers *ServiceType* 'MyServiceType' when it runs.</span></span>

<span data-ttu-id="07c32-112">3 노드 클러스터가 있고, 'MyAppType' 유형의 *응용 프로그램* **fabric:/App1**을 만든다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-112">Let's say we have a 3 node cluster and we create an *application* **fabric:/App1** of type 'MyAppType'.</span></span> <span data-ttu-id="07c32-113">이 *응용 프로그램* **fabric:/App1** 내에 파티션 2개(**P1** & **P2**)와 파티션당 복제본 3개가 있는 'MyServiceType' 유형의 **fabric:/App1/ServiceA** 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-113">Inside this *application* **fabric:/App1** we create a service **fabric:/App1/ServiceA** of type 'MyServiceType' which has 2 partitions (say **P1** & **P2**) and 3 replicas per partition.</span></span> <span data-ttu-id="07c32-114">다음 다이어그램은 이 응용 프로그램이 노드에 배포된 상태 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-114">The following diagram shows the view of this application as it ends up deployed on a node.</span></span>

<span data-ttu-id="07c32-115"><center>
![배포된 응용 프로그램의 노드 보기][node-view-one]
</center></span><span class="sxs-lookup"><span data-stu-id="07c32-115"><center>
![Node view of deployed application][node-view-one]
</center></span></span>

<span data-ttu-id="07c32-116">Service Fabric은 'MyServicePackage'를 활성화했으며, 이 서비스 패키지가 두 파티션 **P1** & **P2**의 복제본을 호스트하는 'MyCodePackage'를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-116">Service Fabric activated 'MyServicePackage' which started 'MyCodePackage' which is hosting replicas from both the partitions i.e. **P1** & **P2**.</span></span> <span data-ttu-id="07c32-117">파티션당 복제본 수를 클러스터의 노드 수와 같도록 선택했으므로 클러스터에 있는 모든 노드 보기가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-117">Note that all the nodes in the cluster will have same view since we chose number of replicas per partition equal to number of nodes in the cluster.</span></span> <span data-ttu-id="07c32-118">**fabric:/App1** 응용 프로그램에 파티션 1개(**P3**)와 파티션당 복제본 3개가 있는 다른 서비스 **fabric:/App1/ServiceB**를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-118">Let's create another service **fabric:/App1/ServiceB** in application **fabric:/App1** which has 1 partition (say **P3**) and 3 replicas per partition.</span></span> <span data-ttu-id="07c32-119">다음 다이어그램은 새로운 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-119">Following diagram shows the new view on the node:</span></span>

<span data-ttu-id="07c32-120"><center>
![배포된 응용 프로그램의 노드 보기][node-view-two]
</center></span><span class="sxs-lookup"><span data-stu-id="07c32-120"><center>
![Node view of deployed application][node-view-two]
</center></span></span>

<span data-ttu-id="07c32-121">보시는 것처럼 Service Fabric이 **fabric:/App1/ServiceB** 서비스의 **P3** 파티션에 대한 새 복제본을 기존 'MyServicePackage' 활성화에 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-121">As we can see Service Fabric placed the new replica for partition **P3** of service **fabric:/App1/ServiceB** in the existing activation of 'MyServicePackage'.</span></span> <span data-ttu-id="07c32-122">이제 'MyAppType' 유형의 다른 *응용 프로그램* **fabric:/App2**를 만들고, **fabric:/App2** 내부에 파티션 2개(**P4** & **P5**)와 파티션당 복제본 3개가 있는 **fabric:/App2/ServiceA** 서비스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-122">Now lets create another *application* **fabric:/App2** of type 'MyAppType' and inside **fabric:/App2** create service **fabric:/App2/ServiceA** which has 2 partitions (say **P4** & **P5**) and 3 replicas per partition.</span></span> <span data-ttu-id="07c32-123">다음 다이어그램은 새 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-123">Following diagrams shows the new node view:</span></span>

<span data-ttu-id="07c32-124"><center>
![배포된 응용 프로그램의 노드 보기][node-view-three]
</center></span><span class="sxs-lookup"><span data-stu-id="07c32-124"><center>
![Node view of deployed application][node-view-three]
</center></span></span>

<span data-ttu-id="07c32-125">이번에는 Service Fabric이 새로운 'MyCodePackage' 복사본을 시작하는 새로운 'MyServicePackage' 복사본을 활성화했으며, **fabric:/App2/ServiceA** 서비스의 두 파티션(**P4** & **P5**)에 있던 복제본이 이 새로운 복사본 'MyCodePackage'에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-125">This time Service Fabric has activated a new copy of 'MyServicePackage' which starts a new copy of 'MyCodePackage' and replicas from both partitions of service **fabric:/App2/ServiceA** (i.e. **P4** & **P5**) are placed in this new copy 'MyCodePackage'.</span></span>

## <a name="shared-process-model"></a><span data-ttu-id="07c32-126">공유 프로세스 모델</span><span class="sxs-lookup"><span data-stu-id="07c32-126">Shared process model</span></span>
<span data-ttu-id="07c32-127">위에서 확인한 모델은 Service Fabric에서 제공하는 기본 호스팅 모델이며, **공유 프로세스** 모델이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-127">What we saw above is the default hosting model provided by Service Fabric and is referred to as **Shared Process** model.</span></span> <span data-ttu-id="07c32-128">이 모델에서는 지정된 *응용 프로그램*에 대해 지정된 *ServicePackage*의 복사본 하나만 *노드*에서 활성화되고(노드에 포함된 모든 *CodePackages*가 시작됨), 지정된 *ServiceType*의 모든 서비스 복제본은 해당 *ServiceType*을 등록하는 *CodePackage*에 모두 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-128">In this model, for a given *application*, only one copy of a given *ServicePackage* is activated on a *Node* (which starts all the *CodePackages* contained in it) and all the replicas of all services of a given  *ServiceType* are placed in the *CodePackage* that registers that *ServiceType*.</span></span> <span data-ttu-id="07c32-129">즉, 지정된 *ServiceType*의 모든 서비스 복제본은 모두 동일한 프로세스를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-129">In other words, all the replicas of all services of a given *ServiceType* share the same process.</span></span>

## <a name="exclusive-process-model"></a><span data-ttu-id="07c32-130">단독 프로세스 모델</span><span class="sxs-lookup"><span data-stu-id="07c32-130">Exclusive process model</span></span>
<span data-ttu-id="07c32-131">Service Fabric에서 제공하는 다른 호스팅 모델은 **단독 프로세스** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-131">The other hosting model provided by Service Fabric is **Exclusive Process** model.</span></span> <span data-ttu-id="07c32-132">이 모델에서 지정된 *노드*에 각 복제본을 배치하기 위해 Service Fabric은 새로운 *ServicePackage* 복사본을 활성화하고(노드에 포함된 모든 *CodePackages*가 시작됨), 복제본은 이 복제본이 속하는 서비스의 *ServiceType*을 등록한 *CodePackage*에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-132">In this model, on a given *Node*, for placing each replica, Service Fabric activates a new copy of *ServicePackage* (which starts all the *CodePackages* contained in it) and replica is placed in the *CodePackage* that registered the *ServiceType* of the service to which replica belongs.</span></span> <span data-ttu-id="07c32-133">즉, 각 복제본은 해당 전용 프로세스에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-133">In other words, each replica lives in its own dedicated process.</span></span> 

<span data-ttu-id="07c32-134">이 모델은 지원되는 Service Fabric의 시작 버전 5.6입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-134">This model is supported starting version 5.6 of Service Fabric.</span></span> <span data-ttu-id="07c32-135">[PowerShell][p1], [REST][r1] 또는 [FabricClient][c1]를 사용하여 서비스를 만들 때 **ServicePackageActivationMode**를 'ExclusiveProcess'로 지정하여 **단독 프로세스** 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-135">**Exclusive Process** model can be chosen at the time of creating the service (using [PowerShell][p1], [REST][r1] or [FabricClient][c1]) by specifying **ServicePackageActivationMode** as 'ExclusiveProcess'.</span></span>

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="07c32-136">응용 프로그램 매니페스트에 기본 서비스가 있는 경우 아래와 같이 **ServicePackageActivationMode** 특성을 지정하여 **단독 프로세스** 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-136">If you have a default service in your application manifest, you can choose **Exclusive Process** model by specifying **ServicePackageActivationMode** attribute as shown below:</span></span>

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
<span data-ttu-id="07c32-137">위 예제를 계속하여, **fabric:/App1** 응용 프로그램에 파티션 2개(**P6** & **P7**)와 파티션당 복제본 3개가 있는 다른 서비스 **fabric:/App1/ServiceC**를 만들어 보겠습니다. **ServicePackageActivationMode**는 'ExclusiveProcess'로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-137">Continuing with our example above, lets create another service **fabric:/App1/ServiceC** in application **fabric:/App1** which has 2 partitions (say **P6** & **P7**) and 3 replicas per partition with **ServicePackageActivationMode** set to 'ExclusiveProcess'.</span></span> <span data-ttu-id="07c32-138">다음 다이어그램은 새로운 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-138">Following diagram shows new view on the node:</span></span>

<span data-ttu-id="07c32-139"><center>
![배포된 응용 프로그램의 노드 보기][node-view-four]
</center></span><span class="sxs-lookup"><span data-stu-id="07c32-139"><center>
![Node view of deployed application][node-view-four]
</center></span></span>

<span data-ttu-id="07c32-140">보시는 것처럼 Service Fabric은 **P6** & **P7** 파티션의 각 복제본에 대해 하나씩 새로운 'MyServicePackage' 복제본 2개를 활성화하고 각 복제본을 전용 *CodePackage* 복사본에 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-140">As you can see, Service Fabric activated two new copies of 'MyServicePackage' (one for each replica from partition **P6** & **P7**) and placed each replica in its dedicated copy of *CodePackage*.</span></span> <span data-ttu-id="07c32-141">여기서 주목할 또 다른 사항은 **단독 프로세스** 모델을 사용하는 경우 지정된 *응용 프로그램*에 대해 지정된 *ServicePackage* 복사본이 *노드*에서 여러 개 활성화될 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-141">Another thing to note here is, when **Exclusive Process** model is used, for a given *application*, multiple copies of a given *ServicePackage* can be active on a *Node*.</span></span> <span data-ttu-id="07c32-142">위 예제에서는 'MyServicePackage' 복사본 3개가 **fabric:/App1**에 대해 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-142">In above example, we see that three copies of 'MyServicePackage' are active for **fabric:/App1**.</span></span> <span data-ttu-id="07c32-143">'MyServicePackage'의 각 활성 복사본에는 *응용 프로그램* **fabric:/App1** 내에서 해당 복사본을 식별하는 **ServicePackageAtivationId**가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-143">Each of these active copies of 'MyServicePackage' has a **ServicePackageAtivationId** associated with it which identifies that copy within *application* **fabric:/App1**.</span></span>

<span data-ttu-id="07c32-144">위 예제의 **fabric:/App2**와 마찬가지로 **공유 프로세스** 모델만 *응용 프로그램*에 사용되는 경우 *노드*에 활성 *ServicePackage* 복사본 하나만 있고, 이 *ServicePackage* 활성화에 대한 **ServicePackageAtivationId**는 '빈 문자열'입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-144">When only **Shared Process** model is used for an *application*, like **fabric:/App2** in above example, there is only one active copy of *ServicePackage* on a *Node* and **ServicePackageAtivationId** for this activation of *ServicePackage* is 'empty string'.</span></span>

> [!NOTE]
>- <span data-ttu-id="07c32-145">**공유 프로세스** 호스팅 모델은 **ServicePackageAtivationMode** = **SharedProcess**에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-145">**Shared Process** hosting model corresponds to **ServicePackageAtivationMode** equal **SharedProcess**.</span></span> <span data-ttu-id="07c32-146">이것이 기본 호스팅 모델이며, 서비스를 만들 때 **ServicePackageAtivationMode**를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-146">This is the default hosting model and **ServicePackageAtivationMode** need not be specified at the time of creating the service.</span></span>
>
>- <span data-ttu-id="07c32-147">**단독 프로세스** 호스팅 모델은 **ServicePackageAtivationMode** = **ExclusiveProcess**이며, 서비스를 만들 때 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-147">**Exclusive Process** hosting model corresponds to **ServicePackageAtivationMode** equal **ExclusiveProcess** and need to be explicitly specified at the time of creating the service.</span></span> 
>
>- <span data-ttu-id="07c32-148">서비스의 호스팅 모델은 [서비스 설명][p2]을 쿼리하고 **ServicePackageAtivationMode**의 값을 확인하면 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-148">Hosting model of a service can be known by querying the [service description][p2] and looking at value of **ServicePackageAtivationMode**.</span></span>
>
>

## <a name="working-with-deployed-service-package"></a><span data-ttu-id="07c32-149">배포된 서비스 패키지 작업</span><span class="sxs-lookup"><span data-stu-id="07c32-149">Working with deployed service package</span></span>
<span data-ttu-id="07c32-150">노드의 활성 *ServicePackage* 복사본을 [배포된 서비스 패키지][p3]라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-150">An active copy of a *ServicePackage* on a node is referred as [deployed service package][p3].</span></span> <span data-ttu-id="07c32-151">위에서 설명한 대로, **단독 프로세스** 모델을 사용하여 서비스를 만드는 경우 지정된 *응용 프로그램*에서 동일한 *ServicePackage*에 대해 배포된 서비스 패키지가 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-151">As previously mentioned above, when **Exclusive Process** model is used for creating services, for a given *application*, there could be multiple deployed service packages for the same *ServicePackage*.</span></span> <span data-ttu-id="07c32-152">[배포된 서비스 패키지의 상태 보고][p4] 또는 [배포된 서비스 패키지의 코드 패키지 다시 시작][p5] 등 배포된 서비스 패키지와 관련된 작업을 수행하는 동안 **ServicePackageActivationId**를 제공하여 배포된 특정 서비스 패키지를 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-152">While performing operations specific to deployed service package like [reporting health of a deployed service package][p4] or [restarting code package of a deployed service package][p5] etc., **ServicePackageActivationId** needs to be provided to identify a specific deployed service package.</span></span>

 <span data-ttu-id="07c32-153">배포된 서비스 패키지의 **ServicePackageActivationId**는 노드에서 [배포된 서비스 패키지][p3] 목록을 쿼리하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-153">**ServicePackageActivationId** of a deployed service package can be obtained by querying the list of [deployed service packages][p3] on a node.</span></span> <span data-ttu-id="07c32-154">노드에서 [배포된 서비스 유형][p6], [배포된 복제본][p7] 및 [배포된 코드 패키지][p8]를 쿼리하는 경우 쿼리 결과에 배포된 부모 서비스 패키지의 **ServicePackageActivationId**도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-154">When querying [deployed service types][p6], [deployed replicas][p7] and [deployed code packages][p8] on a node, the query result also contains the **ServicePackageActivationId** of parent deployed service package.</span></span>

> [!NOTE]
>- <span data-ttu-id="07c32-155">**공유 프로세스** 호스팅 모델 아래의 지정된 *노드*에서 지정된 *응용 프로그램*에 대해 *ServicePackage* 복사본 하나만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-155">Under **Shared Process** hosting model, on a given *node*, for a given *application*, only one copy of a *ServicePackage* is activated.</span></span> <span data-ttu-id="07c32-156">**ServicePackageActivationId**는 *빈 문자열*과 같으며, 배포된 서비스 패키지 관련 작업을 수행하는 동안 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-156">It has **ServicePackageActivationId** equal to *empty string* and need not be specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="07c32-157">**단독 프로세스** 호스팅 모델 아래의 지정된 *노드*에서 지정된 *응용 프로그램*에 대해 *ServicePackage* 복사본 하나 이상이 활성화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-157">Under **Exclusive Process** hosting model, on a given *node*, for a given *application*, one or more copies of a *ServicePackage* can be active.</span></span> <span data-ttu-id="07c32-158">각 활성화의 **ServicePackageActivationId**는 *비어 있지 않으며*, 배포된 서비스 패키지 관련 작업을 수행하는 동안 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-158">Each activation has a *non-empty* **ServicePackageActivationId** and needs to be specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="07c32-159">**ServicePackageActivationId**를 생략하면 기본적으로 '빈 문자열'로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-159">If **ServicePackageActivationId** is ommited it defaults to 'empty string'.</span></span> <span data-ttu-id="07c32-160">**공유 프로세스** 모델 아래에 활성화된 배포된 서비스 패키지가 있으면 해당 패키지에서 작업이 수행되고, 없으면 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-160">If a deployed service package that was activated under **Shared Process** model is present, then operation will be performed on it, otherwise the operation will fail.</span></span>
>
> - <span data-ttu-id="07c32-161">**ServicePackageActivationId**는 동적으로 생성되고 다양한 이유로 변경될 수 있기 때문에 한 번 쿼리한 후 캐시하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-161">It is not recommended to query once and cache **ServicePackageActivationId** as it is dynamically generated and can change for various reasons.</span></span> <span data-ttu-id="07c32-162">**ServicePackageActivationId**가 필요한 작업을 수행하기 전에 먼저 노드에서 [배포된 서비스 패키지][p3] 목록을 쿼리한 후 쿼리 결과의 *ServicePackageActivationId**를 사용하여 원래 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-162">Before performing an operation that needs **ServicePackageActivationId**, you should first query the list of [deployed service packages][p3] on a node and then use *ServicePackageActivationId** from query result to perform the original operation.</span></span>
>
>

## <a name="guest-executable-and-container-applications"></a><span data-ttu-id="07c32-163">게스트 실행 파일 및 컨테이너 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="07c32-163">Guest executable and container applications</span></span>
<span data-ttu-id="07c32-164">Service Fabric은 [게스트 실행 파일][a2] 및 [컨테이너][a3] 응용프로그램을 자체 포함된 상태 비저장 서비스로 처리합니다. 즉, *ServiceHost*(프로세스 또는 컨테이너)에 Service Fabric 런타임이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-164">Service Fabric treats [Guest executable][a2] and [container][a3] applications as statless services which are self-contained i.e. there is no Service Fabric runtime in *ServiceHost* (a process or container).</span></span> <span data-ttu-id="07c32-165">자체 포함된 이러한 서비스에는 *ServiceHost*당 복제본 수가 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-165">Since these services are self-contained, number of replicas per *ServiceHost* is not applicable for these services.</span></span> <span data-ttu-id="07c32-166">이러한 서비스에 사용되는 가장 일반적인 구성은 [InstanceCount][c2]가 -1과 같은 단일 파티션입니다(즉, 클러스터의 각 노드에서 서비스 코드 복사본 하나가 실행되고 있음).</span><span class="sxs-lookup"><span data-stu-id="07c32-166">The most common configuration used with these services is single-partition with [InstanceCount][c2] equal to -1 (i.e. one copy of the service code running on each node of cluster).</span></span> 

<span data-ttu-id="07c32-167">이러한 서비스에 대한 기본 **ServicePackageActivationMode**는 Service Fabric이 *노드*에서 지정된 *응용 프로그램*에 대해 **SharedProcess** 복사본 하나만 활성화하는 *ServicePackage*입니다. 즉, 서비스 코드 복사본 하나만 *노드*를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-167">The default **ServicePackageActivationMode** for these services is **SharedProcess** in which case Service Fabric only activates one copy of *ServicePackage* on a *Node* for a given *application* which means only one copy of service code will run a *Node*.</span></span> <span data-ttu-id="07c32-168">*ServiceManifest*에 지정된 *ServiceType*의 서비스를 여러 개(*Service1* ~ *ServiceN*) 만드는 경우 또는 서비스가 다중 분할된 경우 *노드*에서 서비스 코드의 여러 복사본을 실행하려면 서비스를 만들 때 **ServicePackageActivationMode**를 **ExclusiveProcess**로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-168">If you want multiple copies of your service code to run on a *Node* when you create multiple services (*Service1* to *ServiceN*) of *ServiceType* (specified in *ServiceManifest*) or when your service is multi-partitioned, you should specify **ServicePackageActivationMode** as **ExclusiveProcess** at the time of creating the service.</span></span>

## <a name="changing-hosting-model-of-an-existing-service"></a><span data-ttu-id="07c32-169">기존 서비스의 호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="07c32-169">Changing hosting model of an existing service</span></span>
<span data-ttu-id="07c32-170">업그레이드 또는 업데이트 메커니즘을 통해(또는 응용 프로그램 매니페스트의 기본 서비스 지정에서) 기존 서비스의 호스팅 모델을 **공유 프로세스**에서 **단독 프로세스**로 변경하는 기능은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-170">Changing hosting model of an existing service from **Shared Process** to **Exclusive Process** and vice-versa through upgrade or update mechanism (or in default service specification in application manifest) is currently not supported.</span></span> <span data-ttu-id="07c32-171">이 기능에 대한 지원은 이후 버전에서 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-171">Support for this feature will come in future versions.</span></span>

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a><span data-ttu-id="07c32-172">공유 프로세스 및 단독 프로세스 모델 중에서 선택</span><span class="sxs-lookup"><span data-stu-id="07c32-172">Choosing between shared process and exclusive process model</span></span>
<span data-ttu-id="07c32-173">두 호스팅 모델에는 장단점이 있으며, 사용자가 요구 사항에 가장 적합한 모델을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-173">Both these hosting models have its pros and cons and user needs to evaluate which one fits their requirements best.</span></span> <span data-ttu-id="07c32-174">**공유 프로세스** 모델에서는 더 적은 프로세스가 생성되고 동일한 프로세스의 여러 복제본이 포트를 공유할 수 있기 때문에 OS 리소스 사용률이 향상됩니다. 그러나 복제본 중 하나에서 서비스 호스트를 종료해야 하는 오류가 발생할 경우 동일한 프로세스의 다른 모든 복제본에 영향을 주게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-174">**Shared Process** model enables better utilization of OS resources because fewer processes are spawned, multiple replicas in the same process can share ports, etc. However, if one of the replicas hits an error where it needs to bring down the service host, it will impact all other replicas in same process.</span></span>

 <span data-ttu-id="07c32-175">**단독 프로세스** 모델은 해당 프로세스의 모든 복제본에 대해 격리를 개선하므로 오동작하는 복제본이 다른 복제본에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-175">**Exclusive Process** model provides better isolation with every replica in its own process and a misbehaving replica will not impact other replicas.</span></span> <span data-ttu-id="07c32-176">이 모델은 통신 프로토콜이 포트 공유를 지원하지 않는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-176">It comes in handy for cases where port sharing is not supported by the communication protocol.</span></span> <span data-ttu-id="07c32-177">복제본 수준에서 리소스 관리를 쉽게 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-177">It facilitates the ability to apply resource governance at replica level.</span></span> <span data-ttu-id="07c32-178">반면, **단독 프로세스**는 노드의 각 복제본마다 프로세스 하나를 생성하기 때문에 더 많은 OS 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-178">On the other hand, **Exclusive Process** will consume more OS resources as it spawns one process for each replica on the node.</span></span>

## <a name="exclusive-process-model-and-application-model-considerations"></a><span data-ttu-id="07c32-179">단독 프로세스 모델 및 응용 프로그램 모델 고려 사항</span><span class="sxs-lookup"><span data-stu-id="07c32-179">Exclusive process model and application model considerations</span></span>
<span data-ttu-id="07c32-180">Service Fabric에서 응용 프로그램을 모델링하는 권장 방법은 *ServicePackage*당 *ServiceType* 하나를 유지하는 것이며, 이 모델은 대부분의 응용 프로그램에 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-180">The recommended way to model your application in Service Fabric is to keep one *ServiceType* per *ServicePackage* and this model works well for most of the applications.</span></span> 

<span data-ttu-id="07c32-181">그러나 *ServicePackage*당 *ServiceType* 하나가 부적합한 특별한 시나리오를 지원하기 위해 Service Fabric은 *ServicePackage*당 둘 이상의 *ServiceType*을 사용할 수 있고 *CodePackage* 하나가 둘 이상의 *ServiceType*을 등록할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-181">However, to enable special scenarios where one *ServiceType* per *ServicePackage* may not be desirable, functionally, Service Fabric allows to have more than one *ServiceType* per *ServicePackage* (and one *CodePackage* can register more than one *ServiceType*).</span></span> <span data-ttu-id="07c32-182">다음은 이러한 구성이 유용할 수 있는 몇 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-182">Following are some of the scenarios where these configurations can be useful:</span></span>

- <span data-ttu-id="07c32-183">더 적은 프로세스를 생성하고 프로세스당 더 높은 복제본 밀도를 사용하여 OS 리소스 사용률을 최적화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-183">You want to optimize OS resource utilization by spawning fewer processes and having higher replica density per process.</span></span>
- <span data-ttu-id="07c32-184">서로 다른 ServiceTypes의 복제본이 초기화 또는 메모리 비용이 높은 몇 가지 공통 데이터를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-184">Replicas from different ServiceTypes need to share some common data that has a high initialization or memory cost.</span></span>
- <span data-ttu-id="07c32-185">무료 서비스 제품이 있으며, 서비스의 모든 복제본을 동일한 프로세스에 배치하여 리소스 사용률에 제한을 적용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-185">You have a free service offering and you want to put a limit on resource utilization by putting all replicas of the service in same process.</span></span>

<span data-ttu-id="07c32-186">**단독 프로세스** 호스팅 모델은 *ServicePackage*당 여러 *ServiceTypes*가 있는 응용 프로그램 모델과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-186">**Exclusive Process** hosting model is not coherent with application model having multiple *ServiceTypes* per *ServicePackage*.</span></span> <span data-ttu-id="07c32-187">이는 *ServicePackage*당 여러 *ServiceTypes*가 복제본 간의 리소스 공유를 높이도록 설계되었으며 프로세스당 더 높은 복제본 밀도를 지원하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-187">This is because multiple *ServiceTypes* per *ServicePackage* is designed to achieve higher resource sharing among replicas and enables higher replica density per process.</span></span> <span data-ttu-id="07c32-188">**단독 프로세스** 모델은 이와 다른 목표를 달성하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-188">This is contrary to what **Exclusive Process** model is designed to achieve.</span></span>

<span data-ttu-id="07c32-189">*ServicePackage*당 여러 *ServiceTypes*가 있고, 서로 다른 *CodePackage*가 각 *ServiceType*을 등록하는 경우를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="07c32-189">Consider the case of multiple *ServiceTypes* per *ServicePackage* with different *CodePackage* registering each *ServiceType*.</span></span> <span data-ttu-id="07c32-190">가령, *CodePackages* 2개가 있는 *ServicePackage* 'MultiTypeServicePackge'가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-190">Let's say we have a *ServicePackage* 'MultiTypeServicePackge' which has two *CodePackages*:</span></span>

- <span data-ttu-id="07c32-191">'MyCodePackageA'는 *ServiceType* 'MyServiceTypeA'를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-191">'MyCodePackageA' which registers *ServiceType* 'MyServiceTypeA'.</span></span>
- <span data-ttu-id="07c32-192">'MyCodePackageB'는 *ServiceType* 'MyServiceTypeB'를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-192">'MyCodePackageB' which registers *ServiceType* 'MyServiceTypeB'.</span></span>

<span data-ttu-id="07c32-193">이제 *응용 프로그램* **fabric:/SpecialApp**을 만들고, **단독 프로세스** 모델을 사용하여 **fabric:/SpecialApp** 내부에 다음 두 개의 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-193">Now, lets say, we create an *application* **fabric:/SpecialApp** and inside **fabric:/SpecialApp** we create following two services with **Exclusive Process** model:</span></span>

- <span data-ttu-id="07c32-194">파티션 2개(**P1** 및 **P2**)와 파티션당 복제본 3개가 있는 'MyServiceTypeA' 유형의 **fabric:/SpecialApp/ServiceA** 서비스</span><span class="sxs-lookup"><span data-stu-id="07c32-194">Service **fabric:/SpecialApp/ServiceA** of type 'MyServiceTypeA' with two partitions (say **P1** and **P2**) and 3 replicas per partition.</span></span>
- <span data-ttu-id="07c32-195">파티션 2개(**P3** 및 **P4**)와 파티션당 복제본 3개가 있는 'MyServiceTypeB' 유형의 **fabric:/SpecialApp/ServiceB** 서비스</span><span class="sxs-lookup"><span data-stu-id="07c32-195">Service **fabric:/SpecialApp/ServiceB** of type 'MyServiceTypeB' with two partitions (say **P3** and **P4**) and 3 replicas per partition.</span></span>

<span data-ttu-id="07c32-196">지정된 노드에서 두 서비스에 각각 복제본 2개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-196">On a given node, both the services will have two replicas each.</span></span> <span data-ttu-id="07c32-197">**단독 프로세스** 모델을 사용하여 서비스를 만들었기 때문에 Service Fabric은 각 복제본에 대해 새로운 'MyServicePackge' 복사본을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-197">Since we used **Exclusive Process** model to create the services, Service Fabric will activate a new copy of 'MyServicePackge' for each replica.</span></span> <span data-ttu-id="07c32-198">'MultiTypeServicePackge'를 활성화할 때마다 'MyCodePackageA' 및 'MyCodePackageB'의 복사본이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-198">Each activation of 'MultiTypeServicePackge' will start a copy of 'MyCodePackageA' and 'MyCodePackageB'.</span></span> <span data-ttu-id="07c32-199">그러나 'MyCodePackageA' 또는 'MyCodePackageB' 중 하나만 'MultiTypeServicePackge'가 활성화된 복제본을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-199">However, only one of 'MyCodePackageA' or 'MyCodePackageB' will host the replica for which 'MultiTypeServicePackge' was activated.</span></span> <span data-ttu-id="07c32-200">다음 다이어그램은 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-200">Following diagram shows the node view:</span></span>

<span data-ttu-id="07c32-201"><center>
![배포된 응용 프로그램의 노드 보기][node-view-five]
</center></span><span class="sxs-lookup"><span data-stu-id="07c32-201"><center>
![Node view of deployed application][node-view-five]
</center></span></span>

 <span data-ttu-id="07c32-202">보시는 것처럼, **fabric:/SpecialApp/ServiceA** 서비스의 **P1** 파티션 복제본에 대한 'MultiTypeServicePackge' 활성화에서 'MyCodePackageA'는 복제본을 호스트하고 'MyCodePackageB'는 작동하여 실행되기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-202">As we can see, in the activation of 'MultiTypeServicePackge' for replica of partition **P1** of service **fabric:/SpecialApp/ServiceA**, 'MyCodePackageA' is hosting the replica and 'MyCodePackageB' is just up and running.</span></span> <span data-ttu-id="07c32-203">마찬가지로, **fabric:/SpecialApp/ServiceB** 서비스의 **P3** 파티션 복제본에 대한 'MultiTypeServicePackge' 활성화에서 'MyCodePackageB'는 복제본을 호스트하고 'MyCodePackageA'는 작동하여 실행되기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-203">Similarly, in activation of 'MultiTypeServicePackge' for replica of partition **P3** of service **fabric:/SpecialApp/ServiceB**, 'MyCodePackageB' is hosting the replica and 'MyCodePackageA' is just up and running and so on.</span></span> <span data-ttu-id="07c32-204">따라서 *ServicePackage*당 다른 *ServiceTypes*를 등록하는 *CodePackages* 수가 많을수록 중복 리소스 사용량이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-204">Hence, more the number of *CodePackages* (registering different *ServiceTypes*) per *ServicePackage*, higher will be redundant resource usage.</span></span> 
 
 <span data-ttu-id="07c32-205">반면, **공유 프로세스** 모델을 사용하여 **fabric:/SpecialApp/ServiceA** 및 **fabric:/SpecialApp/ServiceB** 서비스를 만드는 경우 Service Fabric은 앞에서 본 것처럼 *응용 프로그램* **fabric:/SpecialApp**에 대해 'MultiTypeServicePackge' 복사본 하나만 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-205">On the other hand if we create services **fabric:/SpecialApp/ServiceA** and **fabric:/SpecialApp/ServiceB** with **Shared Process** model, Service Fabric will activate only one copy of 'MultiTypeServicePackge' for *application* **fabric:/SpecialApp** (as we saw previously).</span></span> <span data-ttu-id="07c32-206">'MyCodePackageA'는 **fabric:/SpecialApp/ServiceA** 서비스(또는 더 정확히 말해 'MyServiceTypeA' 유형의 모든 서비스)에 대한 모든 복제본을 호스트하고, 'MyCodePackageB'는 **fabric:/SpecialApp/ServiceB** 서비스(또는 더 정확히 말해 'MyServiceTypeB' 유형의 모든 서비스)에 대한 모든 복제본을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-206">'MyCodePackageA' will host all replicas for service **fabric:/SpecialApp/ServiceA** (or of any service of type 'MyServiceTypeA' to be more precise) and 'MyCodePackageB' will host all replicas for service **fabric:/SpecialApp/ServiceB** (or of any service of type 'MyServiceTypeB' to be more precise).</span></span> <span data-ttu-id="07c32-207">다음 다이어그램은 이 설정의 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-207">Following diagram shows the node view in this setting:</span></span> 

<span data-ttu-id="07c32-208"><center>
![배포된 응용 프로그램의 노드 보기][node-view-six]
</center></span><span class="sxs-lookup"><span data-stu-id="07c32-208"><center>
![Node view of deployed application][node-view-six]
</center></span></span>

<span data-ttu-id="07c32-209">위 예제에서 'MyCodePackageA'가 'MyServiceTypeA'와 'MyServiceTypeB'를 둘 다 등록하고 'MyCodePackageB'가 없을 경우 중복 *CodePackage*가 실행되지 않는다고 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-209">In the above example, you might think if 'MyCodePackageA' registers both 'MyServiceTypeA' and 'MyServiceTypeB' and there is no 'MyCodePackageB', then there will be no redundant *CodePackage* running.</span></span> <span data-ttu-id="07c32-210">이 가정은 맞지만, 앞에서 설명한 대로 이 응용 프로그램 모델은 **단독 프로세스** 호스팅 모델과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-210">This is correct, however, as mentioned previously, this application model does not align with **Exclusive Process** hosting model.</span></span> <span data-ttu-id="07c32-211">각 복제본을 전용 프로세스에 배치하려는 경우 동일한 *CodePackage*에서 두 *ServiceTypes*를 모두 등록할 필요는 없으며 각 *ServiceType*을 해당 *ServicePacakge*에 배치하는 것이 더 자연스러운 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-211">If goal is to put each replica in its own dedicated process then registering both *ServiceTypes* from same *CodePackage* is not needed and putting each *ServiceType* in its own *ServicePacakge* is a more natural choice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07c32-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07c32-212">Next steps</span></span>
<span data-ttu-id="07c32-213">[응용 프로그램을 패키지][a4]하고 배포를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-213">[Package an application][a4] and get it ready to deploy.</span></span>

<span data-ttu-id="07c32-214">[응용 프로그램 배포 및 제거][a5]에서는 PowerShell을 사용하여 응용 프로그램 인스턴스를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07c32-214">[Deploy and remove applications][a5] describes how to use PowerShell to manage application instances.</span></span>

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage