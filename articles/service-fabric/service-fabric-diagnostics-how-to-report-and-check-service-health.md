---
title: "Azure 서비스 패브릭을 사용하여 상태를 보고하고 확인 | Microsoft Docs"
description: "Azure 서비스 패브릭에서 제공하는 상태 모니터링 도구를 사용하여 서비스 코드에서 상태 보고서를 보내고 서비스의 상태를 확인하는 방법에 대해 알아보세요."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="dfd14-103">서비스 상태 보고 및 확인</span><span class="sxs-lookup"><span data-stu-id="dfd14-103">Report and check service health</span></span>
<span data-ttu-id="dfd14-104">서비스에 문제가 발생할 때 인시던트 및 중단에 응답하고 수정하는 능력은 문제를 빠르게 검색할 수 있는 능력과 밀접한 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="dfd14-105">서비스 코드에서 Azure 서비스 패브릭 상태 관리자로 문제 및 오류를 보고하면 서비스 패브릭이 제공하는 표준 상태 모니터링 도구를 사용하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="dfd14-106">세 가지 방법으로 서비스에서 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="dfd14-107">[Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) 또는 [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="dfd14-108">`Partition` 및 `CodePackageActivationContext` 개체를 사용하여 현재 컨텍스트의 일부인 요소의 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="dfd14-109">예를 들어 복제본의 일부로 실행되는 코드는 해당 복제본, 복제본이 속하는 파티션 및 복제본을 포함하는 응용 프로그램에 대해서만 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="dfd14-110">`FabricClient`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="dfd14-111">`FabricClient` 를 사용하면 클러스터가 [보안](service-fabric-cluster-security.md) 상태가 아니거나 서비스가 관리자 권한으로 실행되는 경우에 서비스 코드에서 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="dfd14-112">대부분의 실제 시나리오에서는 보안되지 않은 클러스터를 사용하거나 관리자 권한을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="dfd14-113">`FabricClient`를 사용하면 클러스터의 일부인 모든 엔터티의 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="dfd14-114">하지만 이상적으로 서비스 코드는 자체 상태와 관련된 보고서만 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="dfd14-115">클러스터, 응용 프로그램, 배포된 응용 프로그램, 서비스, 서비스 패키지, 파티션, 복제본 또는 노드 수준에서 REST API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="dfd14-116">이는 컨테이너 내에서 상태를 보고하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="dfd14-117">이 문서에서는 서비스 코드에서 상태를 보고하는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="dfd14-118">또한 이 예제에서는 Service Fabric에서 제공하는 도구를 사용하여 상태를 확인할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="dfd14-119">이 문서는 서비스 패브릭의 상태 모니터링 기능을 신속하게 소개할 목적으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="dfd14-120">보다 자세한 내용은 이 문서의 마지막 부분에 있는 링크를 누르면 시작되는 상태에 대한 심화 문서 시리즈를 통해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfd14-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dfd14-121">Prerequisites</span></span>
<span data-ttu-id="dfd14-122">다음이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-122">You must have the following installed:</span></span>

* <span data-ttu-id="dfd14-123">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="dfd14-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="dfd14-124">서비스 패브릭 SDK</span><span class="sxs-lookup"><span data-stu-id="dfd14-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="dfd14-125">로컬 보안 개발자 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="dfd14-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="dfd14-126">관리자 권한으로 PowerShell을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![보안 개발자 클러스터를 만드는 방법을 보여 주는 명령](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="dfd14-128">응용 프로그램을 배포하고 해당 상태를 확인하려면</span><span class="sxs-lookup"><span data-stu-id="dfd14-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="dfd14-129">관리자 권한으로 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="dfd14-130">**상태 저장 서비스** 템플릿을 사용하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![상태 저장 서비스를 사용하여 서비스 패브릭 응용 프로그램 만들기](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="dfd14-132">**F5** 키를 눌러 디버그 모드에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="dfd14-133">응용 프로그램이 로컬 클러스터에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="dfd14-134">응용 프로그램을 실행한 후 알림 영역에서 로컬 클러스터 관리자 아이콘을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **로컬 클러스터 관리** 를 선택하여 서비스 패브릭 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![알림 영역에서 서비스 패브릭 탐색기 열기](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="dfd14-136">응용 프로그램의 상태는 이 이미지와 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="dfd14-137">이때 응용 프로그램은 오류 없이 정상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![서비스 패브릭 탐색기에서 정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="dfd14-139">PowerShell을 사용하여 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="dfd14-140">```Get-ServiceFabricApplicationHealth```를 사용하여 응용 프로그램의 상태를 확인하고 ```Get-ServiceFabricServiceHealth```를 사용하여 서비스의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="dfd14-141">이 이미지에 동일한 응용 프로그램에 대해 PowerShell에서 제공하는 상태 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![PowerShell에서 정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="dfd14-143">서비스 코드에 사용자 지정 상태 이벤트를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="dfd14-143">To add custom health events to your service code</span></span>
<span data-ttu-id="dfd14-144">Visual Studio의 서비스 패브릭 프로젝트 템플릿에는 샘플 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="dfd14-145">다음 단계는 서비스 코드에서 사용자 지정 상태 이벤트를 보고할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="dfd14-146">이런 보고서는 Service Fabric 탐색기, Azure Portal 상태 보기 및 PowerShell과 같이 상태 모니터링을 위해 서비스 패브릭이 제공하는 표준 도구에 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="dfd14-147">Visual Studio에서 이전에 만든 응용 프로그램을 다시 열거나 **상태 저장 서비스** Visual Studio 템플릿을 사용하여 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="dfd14-148">Stateful1.cs 파일을 열고 `RunAsync` 메서드의 `myDictionary.TryGetValueAsync` 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="dfd14-149">이 응용 프로그램의 핵심 논리는 카운트 실행을 계속 유지하는 것이므로 이 메서드가 카운터의 현재 값을 보유하는 `result` 를 반환하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="dfd14-150">실제 응용 프로그램에서 결과 부족이 오류를 나타낸 경우 해당 이벤트에 플래그를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="dfd14-151">결과 부족이 오류를 나타내는 경우 상태 이벤트를 보고하려면 다음 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="dfd14-152">a.</span><span class="sxs-lookup"><span data-stu-id="dfd14-152">a.</span></span> <span data-ttu-id="dfd14-153">`System.Fabric.Health` 네임스페이스를 Stateful1.cs 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="dfd14-154">b.</span><span class="sxs-lookup"><span data-stu-id="dfd14-154">b.</span></span> <span data-ttu-id="dfd14-155">`myDictionary.TryGetValueAsync` 호출 후 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="dfd14-156">이 복제본 상태는 상태 저장 서비스에서 보고되므로 해당 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="dfd14-157">`HealthInformation` 매개 변수가 보고되는 상태 문제에 대한 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="dfd14-158">상태 비저장 서비스를 만든 경우 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="dfd14-159">서비스가 관리자 권한으로 실행되거나 클러스터가 [보안](service-fabric-cluster-security.md) 상태가 아닌 경우 다음 단계와 같이 `FabricClient`를 사용하여 상태를 보고할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="dfd14-160">a.</span><span class="sxs-lookup"><span data-stu-id="dfd14-160">a.</span></span> <span data-ttu-id="dfd14-161">`var myDictionary` 선언 다음에 `FabricClient` 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="dfd14-162">b.</span><span class="sxs-lookup"><span data-stu-id="dfd14-162">b.</span></span> <span data-ttu-id="dfd14-163">`myDictionary.TryGetValueAsync` 호출 후 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="dfd14-164">이 오류를 시뮬레이트하여 상태 모니터링 도구에서 오류가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="dfd14-165">오류를 시뮬레이트하려면 이전에 추가한 상태 보고 코드의 첫 번째 줄을 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="dfd14-166">첫 번째 줄을 주석 처리하고 나면 코드가 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="dfd14-167">이제 이 코드는 `RunAsync`가 실행될 때마다 이 상태 보고서를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="dfd14-168">변경한 후 **F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="dfd14-169">응용 프로그램을 실행한 후에 서비스 패브릭 탐색기를 열어 응용 프로그램의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="dfd14-170">이번에는 Service Fabric 탐색기가 응용 프로그램이 비정상이라고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="dfd14-171">이는 이전에 추가한 코드에서 보고된 오류 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![서비스 패브릭 탐색기에서 비정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="dfd14-173">서비스 패브릭 탐색기의 트리 뷰에서 주 복제본을 선택하면 **성능 상태** 도 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="dfd14-174">서비스 패브릭 탐색기는 코드에서 `HealthInformation` 매개 변수에 추가된 상태 보고서 세부 정보도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="dfd14-175">PowerShell 및 Azure Portal에서도 동일한 상태 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![서비스 패브릭 탐색기 내 복제본 상태](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="dfd14-177">이 보고서는 다른 보고서로 대체되거나 이 복제본이 삭제될 때까지 상태 관리자에 그대로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="dfd14-178">`HealthInformation` 개체의 이 상태 보고서에 대해 `TimeToLive`를 설정하지 않았기 때문에 보고서는 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="dfd14-179">가장 세분화된 수준(이 경우에서는 복제본)에서 상태를 보고하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="dfd14-180">`Partition`에 대해 상태를 보고할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="dfd14-181">`Application`, `DeployedApplication` 및 `DeployedServicePackage`에 대한 상태를 보고하려면 `CodePackageActivationContext`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfd14-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="dfd14-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfd14-182">Next steps</span></span>
* [<span data-ttu-id="dfd14-183">서비스 패브릭 상태 심층 분석</span><span class="sxs-lookup"><span data-stu-id="dfd14-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="dfd14-184">서비스 상태를 보고하기 위한 REST API</span><span class="sxs-lookup"><span data-stu-id="dfd14-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="dfd14-185">응용 프로그램 상태를 보고하기 위한 REST API</span><span class="sxs-lookup"><span data-stu-id="dfd14-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

