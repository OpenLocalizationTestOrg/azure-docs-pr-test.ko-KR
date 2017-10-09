---
title: "Azure 서비스 패브릭 상태를 확인 하 고 aaaReport | Microsoft Docs"
description: "서비스 코드에서 toosend 상태 보고 하는 방법 및 toocheck hello 상태는 Azure 서비스 패브릭 hello 상태 모니터링 도구를 사용 하 여 서비스를 제공 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="cbf4c-103">서비스 상태 보고 및 확인</span><span class="sxs-lookup"><span data-stu-id="cbf4c-103">Report and check service health</span></span>
<span data-ttu-id="cbf4c-104">서비스에서 문제가 발생할 때 기능 toorespond tooand 수정 인시던트 및 작동 중단 문제에 종속 프로그램 기능 toodetect hello 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="cbf4c-105">서비스 코드에서 문제 및 오류 toohello Azure 서비스 패브릭 상태 관리자를 보고 하는 경우 표준 상태 모니터링 서비스 패브릭 toocheck hello 상태를 제공 하는 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="cbf4c-106">세 가지 방법으로 hello 서비스에서 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="cbf4c-107">[Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) 또는 [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="cbf4c-108">Hello를 사용할 수 있습니다 `Partition` 및 `CodePackageActivationContext` hello 현재 컨텍스트에 포함 되는 요소 tooreport hello 상태 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="cbf4c-109">예를 들어 복제본의 일부로 실행 되는 코드는 해당 복제본는 자신이 속한 hello 파티션 및 hello 응용 프로그램의 일부인 하에 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="cbf4c-110">`FabricClient`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="cbf4c-111">사용할 수 있습니다 `FabricClient` hello 클러스터 없으면 hello 서비스 코드에서 tooreport 상태 [보안](service-fabric-cluster-security.md) 아니면 관리자 권한으로 hello 서비스가 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="cbf4c-112">대부분의 실제 시나리오에서는 보안되지 않은 클러스터를 사용하거나 관리자 권한을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="cbf4c-113">와 `FabricClient`, hello 클러스터의 일부인 모든 엔터티의 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="cbf4c-114">그러나 이상적으로 서비스 코드만 보내야 관련된 tooits 자체 상태에 있는 보고서를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="cbf4c-115">Hello 클러스터, 응용 프로그램, 배포 된 응용 프로그램, 서비스, 서비스 패키지, 파티션, 복제본 또는 노드 수준에서 hello REST Api를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="cbf4c-116">이 컨테이너 내에서 사용 되는 tooreport 상태 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="cbf4c-117">이 문서에서는 hello 서비스 코드에서 상태를 보고 하는 예제를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="cbf4c-118">hello 예제에는 서비스 패브릭에서 제공 하는 hello 도구 사용된 toocheck hello 상태를 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="cbf4c-119">이 문서는 의도 한 toobe 간략 한 소개 toohello 상태 서비스 패브릭의 기능을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="cbf4c-120">자세한 내용을 보려면 hello 일련의 hello 끝이 문서에 링크 hello로 시작 하는 상태에 대 한 심도 있는 문서를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbf4c-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cbf4c-121">Prerequisites</span></span>
<span data-ttu-id="cbf4c-122">Hello 다음이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-122">You must have hello following installed:</span></span>

* <span data-ttu-id="cbf4c-123">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cbf4c-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="cbf4c-124">서비스 패브릭 SDK</span><span class="sxs-lookup"><span data-stu-id="cbf4c-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="cbf4c-125">toocreate 안전한 로컬 개발 클러스터</span><span class="sxs-lookup"><span data-stu-id="cbf4c-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="cbf4c-126">관리자 권한으로 PowerShell을 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![방법을 보여 주는 명령 toocreate 보안 개발 클러스터](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="cbf4c-128">toodeploy 응용 프로그램의 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="cbf4c-129">관리자 권한으로 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="cbf4c-130">Hello를 사용 하 여 프로젝트를 만들 **상태 저장 서비스** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![상태 저장 서비스를 사용하여 서비스 패브릭 응용 프로그램 만들기](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="cbf4c-132">키를 눌러 **F5** 디버그 모드에서 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="cbf4c-133">hello 응용 프로그램은 배포 된 toohello 로컬 클러스터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="cbf4c-134">Hello 응용 프로그램을 실행 한 후 hello 알림 영역에서 hello 로컬 클러스터 관리자 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **로컬 클러스터 관리** hello 바로 가기 메뉴 tooopen 서비스 패브릭 탐색기에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![알림 영역에서 서비스 패브릭 탐색기 열기](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="cbf4c-136">이 이미지와 같이 hello 응용 프로그램 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="cbf4c-137">이때 hello 응용 프로그램 오류 없이 정상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![서비스 패브릭 탐색기에서 정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="cbf4c-139">또한 PowerShell을 사용 하 여 hello 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="cbf4c-140">사용할 수 있습니다 ```Get-ServiceFabricApplicationHealth``` 응용 프로그램의 상태 및 있습니다 사용할 수 toocheck ```Get-ServiceFabricServiceHealth``` toocheck 서비스의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="cbf4c-141">PowerShell에서 동일한 응용 프로그램은이 이미지에 hello에 대 한 상태 보고서를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![PowerShell에서 정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="cbf4c-143">tooadd 사용자 지정 상태 이벤트 tooyour 서비스 코드</span><span class="sxs-lookup"><span data-stu-id="cbf4c-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="cbf4c-144">Visual Studio에서 hello 서비스 패브릭 프로젝트 템플릿은 샘플 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="cbf4c-145">hello 다음 단계 표시 방법을 서비스 코드에서 사용자 지정 상태 이벤트를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="cbf4c-146">이런 종류의 보고서 자동으로 도구에 표시 hello 표준 서비스 패브릭 제공 하는지, PowerShell, 서비스 패브릭 탐색기 및 Azure 포털 상태 보기 등을 모니터링 하는 상태에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="cbf4c-147">Visual Studio에서 이전에 만든 hello 응용 프로그램을 닫았다가 다시 열거나 hello를 사용 하 여 새 응용 프로그램을 만들 **상태 저장 서비스** Visual Studio 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="cbf4c-148">Hello Stateful1.cs 파일을 열고 hello `myDictionary.TryGetValueAsync` hello에서 호출 `RunAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="cbf4c-149">이 메서드가 반환 하는지 확인할 수 있습니다는 `result` 보류 hello 카운터의 현재 값을이 응용 프로그램에서 키 논리 hello tookeep 개수 실행 중 이므로 hello 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="cbf4c-150">실제 응용 프로그램의 경우 및 결과의 hello 부족 오류를 표시 하는 경우 해당 이벤트 tooflag를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="cbf4c-151">결과의 hello 부족 오류를 나타내는 경우 상태 이벤트 tooreport hello 다음 단계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="cbf4c-152">a.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-152">a.</span></span> <span data-ttu-id="cbf4c-153">Hello 추가 `System.Fabric.Health` 네임 스페이스 toohello Stateful1.cs 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="cbf4c-154">b.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-154">b.</span></span> <span data-ttu-id="cbf4c-155">Hello hello 후 코드를 다음 추가 `myDictionary.TryGetValueAsync` 호출</span><span class="sxs-lookup"><span data-stu-id="cbf4c-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="cbf4c-156">이 복제본 상태는 상태 저장 서비스에서 보고되므로 해당 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="cbf4c-157">hello `HealthInformation` 보고 하는 hello 상태 문제에 대 한 정보를 저장 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="cbf4c-158">코드 다음 hello를 사용 하 여 상태 비저장 서비스를 만들 때</span><span class="sxs-lookup"><span data-stu-id="cbf4c-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="cbf4c-159">서비스 관리자 권한으로 실행 되거나 hello 클러스터 없으면 경우 [보안](service-fabric-cluster-security.md), 사용할 수도 있습니다 `FabricClient` hello 다음 단계에에서 표시 된 대로 tooreport 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="cbf4c-160">a.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-160">a.</span></span> <span data-ttu-id="cbf4c-161">Hello 만들기 `FabricClient` hello 후 인스턴스 `var myDictionary` 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="cbf4c-162">b.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-162">b.</span></span> <span data-ttu-id="cbf4c-163">Hello hello 후 코드를 다음 추가 `myDictionary.TryGetValueAsync` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="cbf4c-164">이 오류를 시뮬레이션 하 고 hello 상태 모니터링 도구에서 표시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="cbf4c-165">이전에 추가한 코드를 보고 하는 hello 상태에서 hello 첫 번째 줄의 주석 toosimulate hello 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="cbf4c-166">Hello 첫 번째 줄을 주석 후 hello 코드는 다음 예제는 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="cbf4c-167">이 코드 hello 상태 보고서를 될 때마다 발생 `RunAsync` 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="cbf4c-168">키를 눌러 변경 hello를 변경한 후 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="cbf4c-169">Hello 응용 프로그램을 실행 한 후에 hello 응용 프로그램의 서비스 패브릭 탐색기 toocheck hello 상태를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="cbf4c-170">이 시간 서비스 패브릭 탐색기 hello 응용 프로그램 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="cbf4c-171">이전에 추가한 hello 코드에서 보고 된 hello 오류 때문에 이것이입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![서비스 패브릭 탐색기에서 비정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="cbf4c-173">서비스 패브릭 탐색기의 hello 트리 보기에서 hello 주 복제본을 선택 하면 확인 하 게 **상태** 너무 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="cbf4c-174">서비스 패브릭 탐색기에 내용 추가 toohello hello 상태 보고서도 표시 됩니다 `HealthInformation` hello 코드의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="cbf4c-175">나타나면 PowerShell에서 동일한 상태 보고서 hello 및 Azure 포털 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![서비스 패브릭 탐색기 내 복제본 상태](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="cbf4c-177">이 보고서는 다른 보고서 또는이 복제본이 삭제 될 때까지 교체 될 때까지 hello 상태 관리자에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="cbf4c-178">여백을 설정 하지 않았으므로 때문에 `TimeToLive` hello에서이 상태 보고서에 대 한 `HealthInformation` 개체 hello 보고서 만료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="cbf4c-179">Hello 가장 세분화 된 수준에는 예에서 hello 복제 데이터베이스 상태를 보고 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="cbf4c-180">`Partition`에 대해 상태를 보고할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="cbf4c-181">tooreport 상태 `Application`, `DeployedApplication`, 및 `DeployedServicePackage`를 사용 하 여 `CodePackageActivationContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf4c-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="cbf4c-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cbf4c-182">Next steps</span></span>
* [<span data-ttu-id="cbf4c-183">서비스 패브릭 상태 심층 분석</span><span class="sxs-lookup"><span data-stu-id="cbf4c-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="cbf4c-184">서비스 상태를 보고하기 위한 REST API</span><span class="sxs-lookup"><span data-stu-id="cbf4c-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="cbf4c-185">응용 프로그램 상태를 보고하기 위한 REST API</span><span class="sxs-lookup"><span data-stu-id="cbf4c-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

