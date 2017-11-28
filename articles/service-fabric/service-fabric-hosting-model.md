---
title: "서비스 패브릭 호스팅 모델 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a><span data-ttu-id="bfe61-103">Service Fabric 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="bfe61-103">Service Fabric hosting model</span></span>
<span data-ttu-id="bfe61-104">이 문서에서는 서비스 패브릭에서 제공 하는 모델을 호스팅하는 응용 프로그램에 대해 간략하게 설명 하 고 hello hello 차이점에 설명 **공유 프로세스** 및 **단독 프로세스** 모델.</span><span class="sxs-lookup"><span data-stu-id="bfe61-104">This article provides an overview of application hosting models provided by Service Fabric, and describes hello differences between hello **Shared Process** and **Exclusive Process** models.</span></span> <span data-ttu-id="bfe61-105">서비스 패브릭 노드와 hello 서비스 및 hello 서비스 호스트 프로세스의 복제본 (또는 인스턴스) 간의 관계에서 배포 된 응용 프로그램의 모양을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-105">It describes how a deployed application looks on a Service Fabric node and relationship between replicas (or instances) of hello service and hello service-host process.</span></span>

<span data-ttu-id="bfe61-106">계속 진행하기 전에 [Service Fabric 응용 프로그램 모델][a1]을 숙지하고 다양한 개념 및 개념 간의 관계를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-106">Before proceeding further, make sure that you are familiar with [Service Fabric Application Model][a1] and understand various concepts and relation among them.</span></span> 

> [!NOTE]
> <span data-ttu-id="bfe61-107">간단한 설명을 위해 이 문서에서는 명시적으로 언급되지 않은 경우 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-107">In this article, for simplicity, unless explicitly mentioned:</span></span>
>
> - <span data-ttu-id="bfe61-108">단어의 모든 사용 *복제본* tooboth statless 서비스 인스턴스 또는 상태 저장 서비스의 복제를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-108">All uses of word *replica* refers tooboth a replica of a stateful service or an instance of a statless service.</span></span>
> - <span data-ttu-id="bfe61-109">*CodePackage* 취급 같습니다 너무*ServiceHost* 등록 하는 프로세스는 *ServiceType* 및 해당 서비스의 호스트 복제본 *ServiceType*.</span><span class="sxs-lookup"><span data-stu-id="bfe61-109">*CodePackage* is treated equivalent too*ServiceHost* process that registers a *ServiceType* and hosts replicas of services of that *ServiceType*.</span></span>
>

<span data-ttu-id="bfe61-110">toounderstand 호스팅 모델 hello, 예를 통해 직접 알려 주세요.</span><span class="sxs-lookup"><span data-stu-id="bfe61-110">toounderstand hello hosting model, let us walk through an example.</span></span> <span data-ttu-id="bfe61-111">*ApplicationType* 'MyAppType'에 있는 *ServiceType* 'MyServiceType'은 *ServicePackage* 'MyServicePackage'에 의해 제공되고, 이 서비스 패키지에 있는 *CodePackage* 'MyCodePackage'는 실행 시 *ServiceType* 'MyServiceType'을 등록한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-111">Let us say, we have an *ApplicationType* 'MyAppType' which has a *ServiceType* 'MyServiceType' which is provided by *ServicePackage* 'MyServicePackage' which has a *CodePackage* 'MyCodePackage' which registers *ServiceType* 'MyServiceType' when it runs.</span></span>

<span data-ttu-id="bfe61-112">3 노드 클러스터가 있고, 'MyAppType' 유형의 *응용 프로그램* **fabric:/App1**을 만든다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-112">Let's say we have a 3 node cluster and we create an *application* **fabric:/App1** of type 'MyAppType'.</span></span> <span data-ttu-id="bfe61-113">이 *응용 프로그램* **fabric:/App1** 내에 파티션 2개(**P1** & **P2**)와 파티션당 복제본 3개가 있는 'MyServiceType' 유형의 **fabric:/App1/ServiceA** 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-113">Inside this *application* **fabric:/App1** we create a service **fabric:/App1/ServiceA** of type 'MyServiceType' which has 2 partitions (say **P1** & **P2**) and 3 replicas per partition.</span></span> <span data-ttu-id="bfe61-114">hello 다음 그림에이 응용 프로그램으로의 hello 뷰가 배포 된 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-114">hello following diagram shows hello view of this application as it ends up deployed on a node.</span></span>

<span data-ttu-id="bfe61-115"><center>
![배포된 응용 프로그램의 노드 보기][node-view-one]
</center></span><span class="sxs-lookup"><span data-stu-id="bfe61-115"><center>
![Node view of deployed application][node-view-one]
</center></span></span>

<span data-ttu-id="bfe61-116">서비스 패브릭 활성화 즉, 두 hello 파티션이에서 복제본을 호스팅하는 ' MyCodePackage' 시작 ' MyServicePackage' **P1** & **P2**합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-116">Service Fabric activated 'MyServicePackage' which started 'MyCodePackage' which is hosting replicas from both hello partitions i.e. **P1** & **P2**.</span></span> <span data-ttu-id="bfe61-117">참고 hello 클러스터의 노드 파티션 같은 toonumber 당 복제본 수가 선택 했으므로 hello 클러스터의 모든 hello 노드가 같은 보기를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-117">Note that all hello nodes in hello cluster will have same view since we chose number of replicas per partition equal toonumber of nodes in hello cluster.</span></span> <span data-ttu-id="bfe61-118">**fabric:/App1** 응용 프로그램에 파티션 1개(**P3**)와 파티션당 복제본 3개가 있는 다른 서비스 **fabric:/App1/ServiceB**를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-118">Let's create another service **fabric:/App1/ServiceB** in application **fabric:/App1** which has 1 partition (say **P3**) and 3 replicas per partition.</span></span> <span data-ttu-id="bfe61-119">다음 다이어그램에서는 hello hello 노드에서 새 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-119">Following diagram shows hello new view on hello node:</span></span>

<span data-ttu-id="bfe61-120"><center>
![배포된 응용 프로그램의 노드 보기][node-view-two]
</center></span><span class="sxs-lookup"><span data-stu-id="bfe61-120"><center>
![Node view of deployed application][node-view-two]
</center></span></span>

<span data-ttu-id="bfe61-121">서비스 패브릭 배치 파티션에 대 한 새로운 복제본 hello 볼 수 있듯이 **P3** 서비스의 **패브릭: / App1/ServiceB** hello 'MyServicePackage'의 기존 활성화에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-121">As we can see Service Fabric placed hello new replica for partition **P3** of service **fabric:/App1/ServiceB** in hello existing activation of 'MyServicePackage'.</span></span> <span data-ttu-id="bfe61-122">이제 'MyAppType' 유형의 다른 *응용 프로그램* **fabric:/App2**를 만들고, **fabric:/App2** 내부에 파티션 2개(**P4** & **P5**)와 파티션당 복제본 3개가 있는 **fabric:/App2/ServiceA** 서비스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-122">Now lets create another *application* **fabric:/App2** of type 'MyAppType' and inside **fabric:/App2** create service **fabric:/App2/ServiceA** which has 2 partitions (say **P4** & **P5**) and 3 replicas per partition.</span></span> <span data-ttu-id="bfe61-123">다음 다이어그램에서는 hello 새 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-123">Following diagrams shows hello new node view:</span></span>

<span data-ttu-id="bfe61-124"><center>
![배포된 응용 프로그램의 노드 보기][node-view-three]
</center></span><span class="sxs-lookup"><span data-stu-id="bfe61-124"><center>
![Node view of deployed application][node-view-three]
</center></span></span>

<span data-ttu-id="bfe61-125">이번에는 Service Fabric이 새로운 'MyCodePackage' 복사본을 시작하는 새로운 'MyServicePackage' 복사본을 활성화했으며, **fabric:/App2/ServiceA** 서비스의 두 파티션(**P4** & **P5**)에 있던 복제본이 이 새로운 복사본 'MyCodePackage'에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-125">This time Service Fabric has activated a new copy of 'MyServicePackage' which starts a new copy of 'MyCodePackage' and replicas from both partitions of service **fabric:/App2/ServiceA** (i.e. **P4** & **P5**) are placed in this new copy 'MyCodePackage'.</span></span>

## <a name="shared-process-model"></a><span data-ttu-id="bfe61-126">공유 프로세스 모델</span><span class="sxs-lookup"><span data-stu-id="bfe61-126">Shared process model</span></span>
<span data-ttu-id="bfe61-127">Tooas 참조 했으며 그 위에 hello 기본 호스팅 서비스 패브릭에서 제공 하는 모델 이며 **공유 프로세스** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-127">What we saw above is hello default hosting model provided by Service Fabric and is referred tooas **Shared Process** model.</span></span> <span data-ttu-id="bfe61-128">이 모델에에 대 한는 주어진 *응용 프로그램*하나만의 복사는 주어진 *ServicePackage* 에 활성화 되어는 *노드* (시작 되는 모든 hello *CodePackages* 에 포함 된) 복제본의 모든 서비스의 모든 hello 및는 주어진 *ServiceType* hello에 배치 됩니다 *CodePackage* 등록 하는 *ServiceType*.</span><span class="sxs-lookup"><span data-stu-id="bfe61-128">In this model, for a given *application*, only one copy of a given *ServicePackage* is activated on a *Node* (which starts all hello *CodePackages* contained in it) and all hello replicas of all services of a given  *ServiceType* are placed in hello *CodePackage* that registers that *ServiceType*.</span></span> <span data-ttu-id="bfe61-129">복제본의 모든 서비스의 모든 hello 즉, 한 주어진 *ServiceType* 공유 hello 동일한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-129">In other words, all hello replicas of all services of a given *ServiceType* share hello same process.</span></span>

## <a name="exclusive-process-model"></a><span data-ttu-id="bfe61-130">단독 프로세스 모델</span><span class="sxs-lookup"><span data-stu-id="bfe61-130">Exclusive process model</span></span>
<span data-ttu-id="bfe61-131">hello 서비스 패브릭에서 제공 하는 다른 호스팅 모델은 **단독 프로세스** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-131">hello other hosting model provided by Service Fabric is **Exclusive Process** model.</span></span> <span data-ttu-id="bfe61-132">이 모델에 주어진 *노드*, 각 복제본에 거에 대 한 서비스 패브릭 활성화의 새 복사본을 *ServicePackage* (시작 되는 모든 hello *CodePackages* 에 포함 된 ) 복제본 hello에 배치 되 고 *CodePackage* 해당 등록 된 hello *ServiceType* hello 서비스 toowhich의 복제본이 속하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-132">In this model, on a given *Node*, for placing each replica, Service Fabric activates a new copy of *ServicePackage* (which starts all hello *CodePackages* contained in it) and replica is placed in hello *CodePackage* that registered hello *ServiceType* of hello service toowhich replica belongs.</span></span> <span data-ttu-id="bfe61-133">즉, 각 복제본은 해당 전용 프로세스에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-133">In other words, each replica lives in its own dedicated process.</span></span> 

<span data-ttu-id="bfe61-134">이 모델은 지원되는 Service Fabric의 시작 버전 5.6입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-134">This model is supported starting version 5.6 of Service Fabric.</span></span> <span data-ttu-id="bfe61-135">**단독 프로세스** hello hello 서비스를 만들 때 모델을 선택할 수 있습니다 (사용 하 여 [PowerShell][p1], [REST] [ r1]또는 [FabricClient][c1])를 지정 하 여 **ServicePackageActivationMode** 'ExclusiveProcess'으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-135">**Exclusive Process** model can be chosen at hello time of creating hello service (using [PowerShell][p1], [REST][r1] or [FabricClient][c1]) by specifying **ServicePackageActivationMode** as 'ExclusiveProcess'.</span></span>

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

<span data-ttu-id="bfe61-136">응용 프로그램 매니페스트에 기본 서비스가 있는 경우 아래와 같이 **ServicePackageActivationMode** 특성을 지정하여 **단독 프로세스** 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-136">If you have a default service in your application manifest, you can choose **Exclusive Process** model by specifying **ServicePackageActivationMode** attribute as shown below:</span></span>

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
<span data-ttu-id="bfe61-137">위의 예를 계속, 다른 서비스를 만들 수 있습니다 **패브릭: / App1/ServiceC** 응용 프로그램에서 **패브릭: / App1** 파티션 2 개로 (예를 들어 **P6**  &  **P7**)와 파티션당 복제본 3 개가 **ServicePackageActivationMode** too'ExclusiveProcess'를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-137">Continuing with our example above, lets create another service **fabric:/App1/ServiceC** in application **fabric:/App1** which has 2 partitions (say **P6** & **P7**) and 3 replicas per partition with **ServicePackageActivationMode** set too'ExclusiveProcess'.</span></span> <span data-ttu-id="bfe61-138">다음 다이어그램에서는 hello 노드에서 새 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-138">Following diagram shows new view on hello node:</span></span>

<span data-ttu-id="bfe61-139"><center>
![배포된 응용 프로그램의 노드 보기][node-view-four]
</center></span><span class="sxs-lookup"><span data-stu-id="bfe61-139"><center>
![Node view of deployed application][node-view-four]
</center></span></span>

<span data-ttu-id="bfe61-140">보시는 것처럼 Service Fabric은 **P6** & **P7** 파티션의 각 복제본에 대해 하나씩 새로운 'MyServicePackage' 복제본 2개를 활성화하고 각 복제본을 전용 *CodePackage* 복사본에 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-140">As you can see, Service Fabric activated two new copies of 'MyServicePackage' (one for each replica from partition **P6** & **P7**) and placed each replica in its dedicated copy of *CodePackage*.</span></span> <span data-ttu-id="bfe61-141">다른 것이 toonote은 때 **단독 프로세스** 모델을 사용에 대 한는 주어진 *응용 프로그램*의 복사본을 여러 개는 주어진 *ServicePackage* 는 활성화될수있습니다 *노드*합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-141">Another thing toonote here is, when **Exclusive Process** model is used, for a given *application*, multiple copies of a given *ServicePackage* can be active on a *Node*.</span></span> <span data-ttu-id="bfe61-142">위 예제에서는 'MyServicePackage' 복사본 3개가 **fabric:/App1**에 대해 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-142">In above example, we see that three copies of 'MyServicePackage' are active for **fabric:/App1**.</span></span> <span data-ttu-id="bfe61-143">'MyServicePackage'의 각 활성 복사본에는 *응용 프로그램* **fabric:/App1** 내에서 해당 복사본을 식별하는 **ServicePackageAtivationId**가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-143">Each of these active copies of 'MyServicePackage' has a **ServicePackageAtivationId** associated with it which identifies that copy within *application* **fabric:/App1**.</span></span>

<span data-ttu-id="bfe61-144">위 예제의 **fabric:/App2**와 마찬가지로 **공유 프로세스** 모델만 *응용 프로그램*에 사용되는 경우 *노드*에 활성 *ServicePackage* 복사본 하나만 있고, 이 *ServicePackage* 활성화에 대한 **ServicePackageAtivationId**는 '빈 문자열'입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-144">When only **Shared Process** model is used for an *application*, like **fabric:/App2** in above example, there is only one active copy of *ServicePackage* on a *Node* and **ServicePackageAtivationId** for this activation of *ServicePackage* is 'empty string'.</span></span>

> [!NOTE]
>- <span data-ttu-id="bfe61-145">**공유 프로세스** 너무 해당 호스팅 모델**ServicePackageAtivationMode** 같은 **SharedProcess**합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-145">**Shared Process** hosting model corresponds too**ServicePackageAtivationMode** equal **SharedProcess**.</span></span> <span data-ttu-id="bfe61-146">이것은 호스팅 모델 hello 기본값 및 **ServicePackageAtivationMode** 필요 hello hello 서비스를 만들 때 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-146">This is hello default hosting model and **ServicePackageAtivationMode** need not be specified at hello time of creating hello service.</span></span>
>
>- <span data-ttu-id="bfe61-147">**단독 프로세스** 너무 해당 호스팅 모델**ServicePackageAtivationMode** 같은 **ExclusiveProcess** toobe hello hello를 만들 때 명시적으로 지정 해야 합니다. 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-147">**Exclusive Process** hosting model corresponds too**ServicePackageAtivationMode** equal **ExclusiveProcess** and need toobe explicitly specified at hello time of creating hello service.</span></span> 
>
>- <span data-ttu-id="bfe61-148">서비스의 호스팅 모델을 쿼리하여 hello 알 수 [서비스 설명을] [ p2] 값을 살펴보고 **ServicePackageAtivationMode**합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-148">Hosting model of a service can be known by querying hello [service description][p2] and looking at value of **ServicePackageAtivationMode**.</span></span>
>
>

## <a name="working-with-deployed-service-package"></a><span data-ttu-id="bfe61-149">배포된 서비스 패키지 작업</span><span class="sxs-lookup"><span data-stu-id="bfe61-149">Working with deployed service package</span></span>
<span data-ttu-id="bfe61-150">노드의 활성 *ServicePackage* 복사본을 [배포된 서비스 패키지][p3]라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-150">An active copy of a *ServicePackage* on a node is referred as [deployed service package][p3].</span></span> <span data-ttu-id="bfe61-151">앞서 설명한 것 처럼 위에서 때 **단독 프로세스** 모델에 대 한 서비스를 만드는 데 사용 되는 주어진 *응용 프로그램*, 동일 hello에 대 한 여러 배포 된 서비스 패키지 될 수  *ServicePackage*합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-151">As previously mentioned above, when **Exclusive Process** model is used for creating services, for a given *application*, there could be multiple deployed service packages for hello same *ServicePackage*.</span></span> <span data-ttu-id="bfe61-152">특정 toodeployed 서비스 패키지와 같은 작업을 수행 하는 동안 [배포 된 서비스 패키지의 상태를 보고] [ p4] 또는 [배포된서비스패키지의코드패키지를다시시작] [ p5] 등에 **ServicePackageActivationId** 요구 toobe tooidentify 특정 배포 된 서비스 패키지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-152">While performing operations specific toodeployed service package like [reporting health of a deployed service package][p4] or [restarting code package of a deployed service package][p5] etc., **ServicePackageActivationId** needs toobe provided tooidentify a specific deployed service package.</span></span>

 <span data-ttu-id="bfe61-153">**ServicePackageActivationId** 배포 된 서비스의 패키지 목록이 hello를 쿼리하여 얻을 수 [배포 된 서비스 패키지] [ p3] 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-153">**ServicePackageActivationId** of a deployed service package can be obtained by querying hello list of [deployed service packages][p3] on a node.</span></span> <span data-ttu-id="bfe61-154">쿼리할 때 [서비스 유형을 배포][p6], [복제본 배포] [ p7] 및 [배포 된 코드 패키지] [ p8] 노드에 hello 쿼리 결과 스페이스도 hello **ServicePackageActivationId** 부모 배포 된 서비스 패키지의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-154">When querying [deployed service types][p6], [deployed replicas][p7] and [deployed code packages][p8] on a node, hello query result also contains hello **ServicePackageActivationId** of parent deployed service package.</span></span>

> [!NOTE]
>- <span data-ttu-id="bfe61-155">**공유 프로세스** 호스팅 모델 아래의 지정된 *노드*에서 지정된 *응용 프로그램*에 대해 *ServicePackage* 복사본 하나만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-155">Under **Shared Process** hosting model, on a given *node*, for a given *application*, only one copy of a *ServicePackage* is activated.</span></span> <span data-ttu-id="bfe61-156">있기 **ServicePackageActivationId** 너무 같은*빈 문자열* 관련 작업을 수행 하는 배포 된 서비스 패키지 하는 동안 지정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-156">It has **ServicePackageActivationId** equal too*empty string* and need not be specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="bfe61-157">**단독 프로세스** 호스팅 모델 아래의 지정된 *노드*에서 지정된 *응용 프로그램*에 대해 *ServicePackage* 복사본 하나 이상이 활성화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-157">Under **Exclusive Process** hosting model, on a given *node*, for a given *application*, one or more copies of a *ServicePackage* can be active.</span></span> <span data-ttu-id="bfe61-158">각 활성화에는 *비어 있지 않은* **ServicePackageActivationId** toobe 관련 작업을 수행 하는 배포 된 서비스 패키지를 나타내고 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-158">Each activation has a *non-empty* **ServicePackageActivationId** and needs toobe specified while performing deployed service package related operations.</span></span> 
>
> - <span data-ttu-id="bfe61-159">경우 **ServicePackageActivationId** ommited too'empty 문자열 기본값은 '.</span><span class="sxs-lookup"><span data-stu-id="bfe61-159">If **ServicePackageActivationId** is ommited it defaults too'empty string'.</span></span> <span data-ttu-id="bfe61-160">배포 된 서비스를 패키지 하는 경우 아래에서 활성화 된 **공유 프로세스** 모델이 있는 경우 다음 작업이 수행 되도록, 그렇지 않으면 hello 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-160">If a deployed service package that was activated under **Shared Process** model is present, then operation will be performed on it, otherwise hello operation will fail.</span></span>
>
> - <span data-ttu-id="bfe61-161">한 번 tooquery 및 캐시 좋습니다 **ServicePackageActivationId** 동적으로 생성 하 고 다양 한 이유로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-161">It is not recommended tooquery once and cache **ServicePackageActivationId** as it is dynamically generated and can change for various reasons.</span></span> <span data-ttu-id="bfe61-162">에 필요한 작업을 수행 하기 전에 **ServicePackageActivationId**, hello 목록을 쿼리하여 먼저 [배포 된 서비스 패키지] [ p3] 노드와 다음 사용 하 여 에 *ServicePackageActivationId** 쿼리 결과 tooperform hello 원래 작업에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-162">Before performing an operation that needs **ServicePackageActivationId**, you should first query hello list of [deployed service packages][p3] on a node and then use *ServicePackageActivationId** from query result tooperform hello original operation.</span></span>
>
>

## <a name="guest-executable-and-container-applications"></a><span data-ttu-id="bfe61-163">게스트 실행 파일 및 컨테이너 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bfe61-163">Guest executable and container applications</span></span>
<span data-ttu-id="bfe61-164">Service Fabric은 [게스트 실행 파일][a2] 및 [컨테이너][a3] 응용프로그램을 자체 포함된 상태 비저장 서비스로 처리합니다. 즉, *ServiceHost*(프로세스 또는 컨테이너)에 Service Fabric 런타임이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-164">Service Fabric treats [Guest executable][a2] and [container][a3] applications as statless services which are self-contained i.e. there is no Service Fabric runtime in *ServiceHost* (a process or container).</span></span> <span data-ttu-id="bfe61-165">자체 포함된 이러한 서비스에는 *ServiceHost*당 복제본 수가 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-165">Since these services are self-contained, number of replicas per *ServiceHost* is not applicable for these services.</span></span> <span data-ttu-id="bfe61-166">hello 이러한 서비스와 함께 사용 되는 가장 일반적인 구성을 단일 파티션와 [InstanceCount] [ c2] 너무-1 (즉, 클러스터의 각 노드에서 실행 되는 hello 서비스 코드의 한 복사).</span><span class="sxs-lookup"><span data-stu-id="bfe61-166">hello most common configuration used with these services is single-partition with [InstanceCount][c2] equal too-1 (i.e. one copy of hello service code running on each node of cluster).</span></span> 

<span data-ttu-id="bfe61-167">기본 hello **ServicePackageActivationMode** 이러한 서비스는 **SharedProcess** 서비스 패브릭의 복사본이 두 개만 활성화 되는 경우 *ServicePackage* 에 *노드* 에 대 한는 주어진 *응용 프로그램* 즉, 서비스 코드의 복사본을 하나만 실행 됩니다는 *노드*합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-167">hello default **ServicePackageActivationMode** for these services is **SharedProcess** in which case Service Fabric only activates one copy of *ServicePackage* on a *Node* for a given *application* which means only one copy of service code will run a *Node*.</span></span> <span data-ttu-id="bfe61-168">서비스 코드 toorun의 여러 복사본을 원하는 한 *노드* 여러 서비스를 만들 때 (*Service1* 너무*서비스가*)의 *ServiceType* (에 지정 된 *ServiceManifest*)을 지정 하십시오 다중 분할 서비스가 있으면 **ServicePackageActivationMode** 으로 **ExclusiveProcess**hello hello 서비스를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="bfe61-168">If you want multiple copies of your service code toorun on a *Node* when you create multiple services (*Service1* too*ServiceN*) of *ServiceType* (specified in *ServiceManifest*) or when your service is multi-partitioned, you should specify **ServicePackageActivationMode** as **ExclusiveProcess** at hello time of creating hello service.</span></span>

## <a name="changing-hosting-model-of-an-existing-service"></a><span data-ttu-id="bfe61-169">기존 서비스의 호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="bfe61-169">Changing hosting model of an existing service</span></span>
<span data-ttu-id="bfe61-170">기존 서비스에서의 호스팅 모델을 변경 **공유 프로세스** 너무**단독 프로세스** 반대의 통해 업그레이드 또는 업데이트 메커니즘 (또는 기본 서비스 응용 프로그램에서 사양 매니페스트) 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-170">Changing hosting model of an existing service from **Shared Process** too**Exclusive Process** and vice-versa through upgrade or update mechanism (or in default service specification in application manifest) is currently not supported.</span></span> <span data-ttu-id="bfe61-171">이 기능에 대한 지원은 이후 버전에서 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-171">Support for this feature will come in future versions.</span></span>

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a><span data-ttu-id="bfe61-172">공유 프로세스 및 단독 프로세스 모델 중에서 선택</span><span class="sxs-lookup"><span data-stu-id="bfe61-172">Choosing between shared process and exclusive process model</span></span>
<span data-ttu-id="bfe61-173">호스팅 모델은 해당 장점 및 단점 및 사용자에 게 필요한 해당 요구 사항에 가장 적합 한 tooevaluate 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-173">Both these hosting models have its pros and cons and user needs tooevaluate which one fits their requirements best.</span></span> <span data-ttu-id="bfe61-174">**공유 프로세스** 모델 적은 프로세스가 생성 됩니다 때문에 운영 체제 리소스를 더 효율적으로 사용을 통해, 여러 복제본에서 동일한 hello 포트 등 프로세스를 공유할 수 있습니다. 그러나 hello 복제본 중 하나에 도달 toobring hello 서비스 호스트를이 필요한 경우에 오류를 같은 프로세스에서 다른 모든 복제본 영향 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-174">**Shared Process** model enables better utilization of OS resources because fewer processes are spawned, multiple replicas in hello same process can share ports, etc. However, if one of hello replicas hits an error where it needs toobring down hello service host, it will impact all other replicas in same process.</span></span>

 <span data-ttu-id="bfe61-175">**단독 프로세스** 모델은 해당 프로세스의 모든 복제본에 대해 격리를 개선하므로 오동작하는 복제본이 다른 복제본에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-175">**Exclusive Process** model provides better isolation with every replica in its own process and a misbehaving replica will not impact other replicas.</span></span> <span data-ttu-id="bfe61-176">처리 하는 여기서 포트 공유에서 지원 하지 않는 hello 통신 프로토콜의 경우에 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-176">It comes in handy for cases where port sharing is not supported by hello communication protocol.</span></span> <span data-ttu-id="bfe61-177">복제본 수준에서 hello 기능 tooapply 리소스 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-177">It facilitates hello ability tooapply resource governance at replica level.</span></span> <span data-ttu-id="bfe61-178">반면에 hello **단독 프로세스** hello 노드의 각 복제본에 대 한 프로세스를 생성 하는 대로 많은 수의 운영 체제 리소스를 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-178">On hello other hand, **Exclusive Process** will consume more OS resources as it spawns one process for each replica on hello node.</span></span>

## <a name="exclusive-process-model-and-application-model-considerations"></a><span data-ttu-id="bfe61-179">단독 프로세스 모델 및 응용 프로그램 모델 고려 사항</span><span class="sxs-lookup"><span data-stu-id="bfe61-179">Exclusive process model and application model considerations</span></span>
<span data-ttu-id="bfe61-180">hello 권장 방법은 toomodel 서비스 패브릭에서 응용 프로그램은 하나 tookeep *ServiceType* 당 *ServicePackage* 이 모델은 대부분의 hello 응용 프로그램에 적합 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-180">hello recommended way toomodel your application in Service Fabric is tookeep one *ServiceType* per *ServicePackage* and this model works well for most of hello applications.</span></span> 

<span data-ttu-id="bfe61-181">그러나 tooenable 특별 한 시나리오 하나 있는 *ServiceType* 당 *ServicePackage* 되지 않을 수 있습니다, 기능적으로 서비스 패브릭 허용 파일이 둘 이상 toohave *ServiceType* 당 *ServicePackage* (하나의 *CodePackage* 개 이상 등록할 수 *ServiceType*).</span><span class="sxs-lookup"><span data-stu-id="bfe61-181">However, tooenable special scenarios where one *ServiceType* per *ServicePackage* may not be desirable, functionally, Service Fabric allows toohave more than one *ServiceType* per *ServicePackage* (and one *CodePackage* can register more than one *ServiceType*).</span></span> <span data-ttu-id="bfe61-182">다음은 일부의 hello 시나리오 이러한 구성은 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-182">Following are some of hello scenarios where these configurations can be useful:</span></span>

- <span data-ttu-id="bfe61-183">Toooptimize OS 리소스 사용률을 원하는 프로세스당 높은 복제본 밀도 여 더 적은 프로세스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-183">You want toooptimize OS resource utilization by spawning fewer processes and having higher replica density per process.</span></span>
- <span data-ttu-id="bfe61-184">다른 servicetype은에서 복제본 tooshare 높은 초기화 또는 메모리 비용에 몇 가지 일반 데이터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-184">Replicas from different ServiceTypes need tooshare some common data that has a high initialization or memory cost.</span></span>
- <span data-ttu-id="bfe61-185">무료 서비스를 제공 해야 하 고 tooput 리소스 사용률에도 동일한 프로세스에서 hello 서비스의 모든 복제본을 배치 하 여 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-185">You have a free service offering and you want tooput a limit on resource utilization by putting all replicas of hello service in same process.</span></span>

<span data-ttu-id="bfe61-186">**단독 프로세스** 호스팅 모델은 *ServicePackage*당 여러 *ServiceTypes*가 있는 응용 프로그램 모델과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-186">**Exclusive Process** hosting model is not coherent with application model having multiple *ServiceTypes* per *ServicePackage*.</span></span> <span data-ttu-id="bfe61-187">즉, 여러 *servicetype은* 당 *ServicePackage* 디자인 된 tooachieve 더 높은 리소스 복제본 간에 공유 되며 프로세스당 높은 복제본 밀도 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-187">This is because multiple *ServiceTypes* per *ServicePackage* is designed tooachieve higher resource sharing among replicas and enables higher replica density per process.</span></span> <span data-ttu-id="bfe61-188">이 반대 toowhat **단독 프로세스** 모델은 설계 된 tooachieve 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-188">This is contrary toowhat **Exclusive Process** model is designed tooachieve.</span></span>

<span data-ttu-id="bfe61-189">여러 hello 경우 *servicetype은* 당 *ServicePackage* 서로 다른 *CodePackage* 각 등록 *ServiceType*.</span><span class="sxs-lookup"><span data-stu-id="bfe61-189">Consider hello case of multiple *ServiceTypes* per *ServicePackage* with different *CodePackage* registering each *ServiceType*.</span></span> <span data-ttu-id="bfe61-190">가령, *CodePackages* 2개가 있는 *ServicePackage* 'MultiTypeServicePackge'가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-190">Let's say we have a *ServicePackage* 'MultiTypeServicePackge' which has two *CodePackages*:</span></span>

- <span data-ttu-id="bfe61-191">'MyCodePackageA'는 *ServiceType* 'MyServiceTypeA'를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-191">'MyCodePackageA' which registers *ServiceType* 'MyServiceTypeA'.</span></span>
- <span data-ttu-id="bfe61-192">'MyCodePackageB'는 *ServiceType* 'MyServiceTypeB'를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-192">'MyCodePackageB' which registers *ServiceType* 'MyServiceTypeB'.</span></span>

<span data-ttu-id="bfe61-193">이제 *응용 프로그램* **fabric:/SpecialApp**을 만들고, **단독 프로세스** 모델을 사용하여 **fabric:/SpecialApp** 내부에 다음 두 개의 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-193">Now, lets say, we create an *application* **fabric:/SpecialApp** and inside **fabric:/SpecialApp** we create following two services with **Exclusive Process** model:</span></span>

- <span data-ttu-id="bfe61-194">파티션 2개(**P1** 및 **P2**)와 파티션당 복제본 3개가 있는 'MyServiceTypeA' 유형의 **fabric:/SpecialApp/ServiceA** 서비스</span><span class="sxs-lookup"><span data-stu-id="bfe61-194">Service **fabric:/SpecialApp/ServiceA** of type 'MyServiceTypeA' with two partitions (say **P1** and **P2**) and 3 replicas per partition.</span></span>
- <span data-ttu-id="bfe61-195">파티션 2개(**P3** 및 **P4**)와 파티션당 복제본 3개가 있는 'MyServiceTypeB' 유형의 **fabric:/SpecialApp/ServiceB** 서비스</span><span class="sxs-lookup"><span data-stu-id="bfe61-195">Service **fabric:/SpecialApp/ServiceB** of type 'MyServiceTypeB' with two partitions (say **P3** and **P4**) and 3 replicas per partition.</span></span>

<span data-ttu-id="bfe61-196">지정 된 노드에서 두 hello 서비스 각 복제본 두 개가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-196">On a given node, both hello services will have two replicas each.</span></span> <span data-ttu-id="bfe61-197">사용 하므로 **단독 프로세스** 모델 toocreate hello 서비스, 서비스 패브릭 각 복제본에 대 한 'MyServicePackge'의 새 복사본을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-197">Since we used **Exclusive Process** model toocreate hello services, Service Fabric will activate a new copy of 'MyServicePackge' for each replica.</span></span> <span data-ttu-id="bfe61-198">'MultiTypeServicePackge'를 활성화할 때마다 'MyCodePackageA' 및 'MyCodePackageB'의 복사본이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-198">Each activation of 'MultiTypeServicePackge' will start a copy of 'MyCodePackageA' and 'MyCodePackageB'.</span></span> <span data-ttu-id="bfe61-199">그러나를 'MultiTypeServicePackge' 활성화 된 hello 복제본을 호스트 'MyCodePackageA' 또는 'MyCodePackageB' 중 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-199">However, only one of 'MyCodePackageA' or 'MyCodePackageB' will host hello replica for which 'MultiTypeServicePackge' was activated.</span></span> <span data-ttu-id="bfe61-200">다음 다이어그램에서는 hello 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-200">Following diagram shows hello node view:</span></span>

<span data-ttu-id="bfe61-201"><center>
![배포된 응용 프로그램의 노드 보기][node-view-five]
</center></span><span class="sxs-lookup"><span data-stu-id="bfe61-201"><center>
![Node view of deployed application][node-view-five]
</center></span></span>

 <span data-ttu-id="bfe61-202">볼 수 있듯이, 파티션의 복제본에 대 한 'MultiTypeServicePackge' hello 활성화에 **P1** 서비스의 **패브릭: / SpecialApp/ServiceA**, 'MyCodePackageA' hello 복제본을 호스팅 중인 및 ' MyCodePackageB' 바로 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-202">As we can see, in hello activation of 'MultiTypeServicePackge' for replica of partition **P1** of service **fabric:/SpecialApp/ServiceA**, 'MyCodePackageA' is hosting hello replica and 'MyCodePackageB' is just up and running.</span></span> <span data-ttu-id="bfe61-203">마찬가지로, 파티션의 복제본에 대 한 'MultiTypeServicePackge'의 활성화에 **P3** 서비스의 **패브릭: / SpecialApp/ServiceB**'MyCodePackageB' hello 복제본을 호스팅하는, 및 'MyCodePackageA'가 방금 실행 되 고 기타 등등</span><span class="sxs-lookup"><span data-stu-id="bfe61-203">Similarly, in activation of 'MultiTypeServicePackge' for replica of partition **P3** of service **fabric:/SpecialApp/ServiceB**, 'MyCodePackageB' is hosting hello replica and 'MyCodePackageA' is just up and running and so on.</span></span> <span data-ttu-id="bfe61-204">따라서 수가 더 hello *CodePackages* (서로 다른 등록 *servicetype은*) 당 *ServicePackage*, 더 높은 됩니다 중복 리소스 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-204">Hence, more hello number of *CodePackages* (registering different *ServiceTypes*) per *ServicePackage*, higher will be redundant resource usage.</span></span> 
 
 <span data-ttu-id="bfe61-205">서비스를 만들면 다른 손에 hello **패브릭: / SpecialApp/ServiceA** 및 **패브릭: / SpecialApp/ServiceB** 와 **공유 프로세스** 모델 서비스 패브릭 됩니다 에 대 한 'MultiTypeServicePackge' 인스턴스의 복사본이 하나만 활성화 *응용 프로그램* **패브릭: / SpecialApp** (보았듯이 이전에).</span><span class="sxs-lookup"><span data-stu-id="bfe61-205">On hello other hand if we create services **fabric:/SpecialApp/ServiceA** and **fabric:/SpecialApp/ServiceB** with **Shared Process** model, Service Fabric will activate only one copy of 'MultiTypeServicePackge' for *application* **fabric:/SpecialApp** (as we saw previously).</span></span> <span data-ttu-id="bfe61-206">'MyCodePackageA' 서비스에 대 한 모든 복제본을 호스팅할 **패브릭: / SpecialApp/ServiceA** (또는 보다 정확 하 게 'MyServiceTypeA' toobe 유형의 모든 서비스의) 'MyCodePackageB' 서비스에 대 한 모든 복제본을 호스트 하 고 **패브릭: / SpecialApp/ServiceB** (또는 보다 정확 하 게 'MyServiceTypeB' toobe 유형의 모든 서비스의).</span><span class="sxs-lookup"><span data-stu-id="bfe61-206">'MyCodePackageA' will host all replicas for service **fabric:/SpecialApp/ServiceA** (or of any service of type 'MyServiceTypeA' toobe more precise) and 'MyCodePackageB' will host all replicas for service **fabric:/SpecialApp/ServiceB** (or of any service of type 'MyServiceTypeB' toobe more precise).</span></span> <span data-ttu-id="bfe61-207">다음 다이어그램에서는이 설정에 hello 노드 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-207">Following diagram shows hello node view in this setting:</span></span> 

<span data-ttu-id="bfe61-208"><center>
![배포된 응용 프로그램의 노드 보기][node-view-six]
</center></span><span class="sxs-lookup"><span data-stu-id="bfe61-208"><center>
![Node view of deployed application][node-view-six]
</center></span></span>

<span data-ttu-id="bfe61-209">위 예제는 hello에서 'MyCodePackageA' 등록 'MyServiceTypeA'와 'MyServiceTypeB' 없음 'MyCodePackageB' 없을 경우 있을 더 중복으로 생각할 수 있습니다 *CodePackage* 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-209">In hello above example, you might think if 'MyCodePackageA' registers both 'MyServiceTypeA' and 'MyServiceTypeB' and there is no 'MyCodePackageB', then there will be no redundant *CodePackage* running.</span></span> <span data-ttu-id="bfe61-210">이 가정은 맞지만, 앞에서 설명한 대로 이 응용 프로그램 모델은 **단독 프로세스** 호스팅 모델과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-210">This is correct, however, as mentioned previously, this application model does not align with **Exclusive Process** hosting model.</span></span> <span data-ttu-id="bfe61-211">Tooput ´ ֲ 자체에서 각 복제본 둘 다를 등록 하는 프로세스 전용 전용 *servicetype은* 동일한 *CodePackage* 는 필요 하지 않으며 각 배치 *ServiceType* 에서 자체 *ServicePacakge* 더 자연 스러운 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-211">If goal is tooput each replica in its own dedicated process then registering both *ServiceTypes* from same *CodePackage* is not needed and putting each *ServiceType* in its own *ServicePacakge* is a more natural choice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfe61-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfe61-212">Next steps</span></span>
<span data-ttu-id="bfe61-213">[응용 프로그램 패키지] [ a4] 준비 toodeploy 가져오기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe61-213">[Package an application][a4] and get it ready toodeploy.</span></span>

<span data-ttu-id="bfe61-214">[배포 및 응용 프로그램을 제거할] [ a5] 설명 방법을 toouse PowerShell toomanage 응용 프로그램 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="bfe61-214">[Deploy and remove applications][a5] describes how toouse PowerShell toomanage application instances.</span></span>

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
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