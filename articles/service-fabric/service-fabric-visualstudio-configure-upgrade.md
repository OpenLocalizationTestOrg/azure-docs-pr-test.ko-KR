---
title: "Service Fabric 응용 프로그램의 업그레이드 구성 | Microsoft Docs"
description: "Microsoft Visual Studio를 사용하여 서비스 패브릭 응용 프로그램을 업그레이드하기 위한 설정을 구성하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="968a4-103">Visual Studio에서 서비스 패브릭 응용 프로그램의 업그레이드 구성</span><span class="sxs-lookup"><span data-stu-id="968a4-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="968a4-104">Azure 서비스 패브릭에 대한 Visual Studio Tools는 로컬 또는 원격 클러스터에 게시하기 위한 업그레이드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="968a4-105">테스트 및 디버그 중에 응용 프로그램을 바꾸지 않고 새 버전으로 업그레이드하려는 세 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="968a4-106">업그레이드하는 동안 응용 프로그램 데이터가 손실되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="968a4-107">업그레이드 도메인에 서비스 인스턴스가 충분히 퍼져 있는 경우 가용성이 높은 상태를 유지하므로 업그레이드 중 서비스 중단이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="968a4-108">업그레이드하는 동안 응용 프로그램에 대해 테스트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="968a4-109">업그레이드하기 위해 필요한 매개 변수</span><span class="sxs-lookup"><span data-stu-id="968a4-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="968a4-110">두 가지의 배포 형식(일반 또는 업그레이드)에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="968a4-111">일반 배포는 클러스터에서 이전 배포 정보 및 데이터를 지우는 반면 업그레이드 배포는 이러한 정보 및 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="968a4-112">Visual Studio에서 서비스 패브릭 응용 프로그램을 업그레이드하는 경우 응용 프로그램 업그레이드 매개 변수 및 상태 검사 정책을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="968a4-113">응용 프로그램 업그레이드 매개 변수는 업그레이드를 제어하는 반면 상태 검사 정책은 업그레이드가 성공적인지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="968a4-114">자세한 내용은 [서비스 패브릭 응용 프로그램 업그레이드: 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="968a4-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="968a4-115">*Monitored*, *UnmonitoredAuto* 및 *UnmonitoredManual*의 세 가지 업그레이드 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="968a4-116">Monitored 업그레이드는 업그레이드 및 응용 프로그램 상태 검사를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="968a4-117">UnmonitoredAuto 업그레이드는 업그레이드를 자동화하지만 응용 프로그램 상태 검사는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="968a4-118">UnmonitoredManual 업그레이드를 수행하는 경우 수동으로 각 업그레이드 도메인을 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="968a4-119">업그레이드 모드마다 서로 다른 매개 변수 집합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="968a4-120">사용할 수 있는 업그레이드 옵션에 대해 자세히 알아보려면 [응용 프로그램 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="968a4-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="968a4-121">Visual Studio에서 서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="968a4-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="968a4-122">Visual Studio 서비스 패브릭 도구를 사용하여 서비스 패브릭 응용 프로그램을 업그레이드하는 경우 **응용 프로그램 업그레이드** 확인란을 선택하여 게시 프로세스가 일반 배포가 아닌 업그레이드가 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="968a4-123">업그레이드 매개 변수를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="968a4-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="968a4-124">확인란 옆의 **설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="968a4-125">**업그레이드 매개 변수 편집** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="968a4-126">**업그레이드 매개 변수 편집** 대화 상자는 Monitored, UnmonitoredAuto 및 UnmonitoredManual 업그레이드 모드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="968a4-127">사용하려는 업그레이드 모드를 선택한 다음 매개 변수 그리드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="968a4-128">각 매개 변수에는 기본값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-128">Each parameter has default values.</span></span> <span data-ttu-id="968a4-129">선택적 매개 변수 *DefaultServiceTypeHealthPolicy* 는 해시 테이블 입력을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="968a4-130">다음은 *DefaultServiceTypeHealthPolicy*에 대한 해시 테이블 입력 형식의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="968a4-131">*ServiceTypeHealthPolicyMap* 은 다음과 같은 형식으로 해시 테이블 입력을 사용하는 다른 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="968a4-132">다음은 실제 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="968a4-133">UnmonitoredManual 업그레이드 모드를 선택하는 경우 수동으로 PowerShell 콘솔을 시작하여 업그레이드 프로세스를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="968a4-134">수동 업그레이드 작업 방법을 알아보려면 [서비스 패브릭 응용 프로그램 업그레이드: 고급 항목](service-fabric-application-upgrade-advanced.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="968a4-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="968a4-135">PowerShell을 사용하여 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="968a4-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="968a4-136">PowerShell cmdlet을 사용하여 서비스 패브릭 응용 프로그램을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="968a4-137">자세한 내용을 보려면 [Service Fabric 응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md) 및 [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="968a4-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="968a4-138">응용 프로그램 매니페스트 파일에 상태 검사 정책을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="968a4-139">서비스 패브릭 응용 프로그램의 모든 서비스는 기본값을 재정의하는 자체 상태 정책 매개 변수를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="968a4-140">응용 프로그램 매니페스트 파일에서 이러한 매개 변수 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="968a4-141">다음 예제에서는 응용 프로그램 매니페스트에서 각 서비스에 대한 고유한 상태 검사 정책을 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="968a4-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="968a4-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="968a4-142">Next steps</span></span>
<span data-ttu-id="968a4-143">응용 프로그램을 배포하는 방법에 대한 자세한 내용은 [Azure 서비스 패브릭에서 기존 응용 프로그램 배포](service-fabric-deploy-existing-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="968a4-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>