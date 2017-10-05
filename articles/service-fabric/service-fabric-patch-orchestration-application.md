---
title: "Azure Service Fabric 패치 오케스트레이션 응용 프로그램 | Microsoft Docs"
description: "Service Fabric 클러스터에 운영 체제 패치를 자동화하는 응용 프로그램입니다."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="6c417-103">Service Fabric 클러스터에서 Windows 운영 체제 패치</span><span class="sxs-lookup"><span data-stu-id="6c417-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="6c417-104">패치 오케스트레이션 응용 프로그램은 Azure의 Service Fabric 클러스터에서 가동 중지 시간 없이 운영 체제 패치를 자동화하는 Azure Service Fabric 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="6c417-105">패치 오케스트레이션 앱은 다음과 같은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="6c417-106">**자동 운영 체제 업데이트 설치**.</span><span class="sxs-lookup"><span data-stu-id="6c417-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="6c417-107">운영 체제 업데이트가 자동으로 다운로드되고 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="6c417-108">클러스터 노드는 필요에 따라 클러스터 가동 중지 시간 없이 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="6c417-109">**클러스터 인식 패치 및 상태 통합**.</span><span class="sxs-lookup"><span data-stu-id="6c417-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="6c417-110">패치 오케스트레이션 앱은 업데이트를 적용하는 동안 클러스터 노드의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="6c417-111">클러스터 노드는 한 번에 하나의 노드씩 또는 한 번에 하나의 업그레이드 도메인씩 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="6c417-112">패치 프로세스로 인해 클러스터의 상태가 다운되는 경우 문제가 악화되는 것을 방지하기 위해 프로세스가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="6c417-113">앱 내부 세부 정보</span><span class="sxs-lookup"><span data-stu-id="6c417-113">Internal details of the app</span></span>

<span data-ttu-id="6c417-114">패치 오케스트레이션 앱은 다음 하위 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="6c417-115">**코디네이터 서비스**: 이 상태 저장 서비스는 다음과 같은 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="6c417-116">전체 클러스터에서 Windows Update 작업을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="6c417-117">완료된 Windows 업데이트 작업의 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="6c417-118">**노드 에이전트 서비스**: 이 상태 비저장 서비스는 모든 Service Fabric 클러스터 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="6c417-119">서비스는 다음과 같은 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-119">The service is responsible for:</span></span>
    - <span data-ttu-id="6c417-120">노드 에이전트 NTService의 부트스트랩</span><span class="sxs-lookup"><span data-stu-id="6c417-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="6c417-121">노드 에이전트 NTService의 모니터링</span><span class="sxs-lookup"><span data-stu-id="6c417-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="6c417-122">**노드 에이전트 NTService**: 이 Windows NT 서비스는 더 높은 수준의 권한(시스템)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="6c417-123">반면, 노드 에이전트 서비스 및 코디네이터 서비스는 하위 수준의 권한(네트워크 서비스)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="6c417-124">서비스는 모든 클러스터 노드에서 다음과 같은 Windows 업데이트 작업을 수행하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="6c417-125">노드에서 자동 Windows Update 비활성화</span><span class="sxs-lookup"><span data-stu-id="6c417-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="6c417-126">사용자가 제공한 정책에 따라 Windows 업데이트 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="6c417-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="6c417-127">Windows 업데이트 설치 이후 컴퓨터 다시 시작</span><span class="sxs-lookup"><span data-stu-id="6c417-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="6c417-128">코디네이터 서비스에 Windows 업데이트 결과 업로드</span><span class="sxs-lookup"><span data-stu-id="6c417-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="6c417-129">모든 재시도가 끝난 다음 작업이 실패한 경우 상태 보고서 보고</span><span class="sxs-lookup"><span data-stu-id="6c417-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="6c417-130">패치 오케스트레이션 앱은 Service Fabric 복구 관리자 시스템 서비스를 사용하여 노드를 사용하도록 또는 사용하지 않도록 설정하고 상태 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="6c417-131">패치 오케스트레이션 앱에서 만든 복구 작업은 각 노드에 대한 Windows 업데이트 진행률을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c417-132">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6c417-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="6c417-133">지원되는 최소 Service Fabric 런타임 버전</span><span class="sxs-lookup"><span data-stu-id="6c417-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="6c417-134">Azure 클러스터</span><span class="sxs-lookup"><span data-stu-id="6c417-134">Azure clusters</span></span>
<span data-ttu-id="6c417-135">패치 오케스트레이션 앱은 Service Fabric 런타임 버전 v5.5 이상이 설치된 Azure 클러스터에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="6c417-136">독립 실행형 온-프레미스 클러스터</span><span class="sxs-lookup"><span data-stu-id="6c417-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="6c417-137">패치 오케스트레이션 앱은 Service Fabric 런타임 버전 v5.6 이상이 설치된 독립 실행형 클러스터에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="6c417-138">복구 관리자 서비스 사용(아직 실행되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="6c417-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="6c417-139">패치 오케스트레이션 앱은 복구 관리자 시스템 서비스를 클러스터에서 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="6c417-140">Azure 클러스터</span><span class="sxs-lookup"><span data-stu-id="6c417-140">Azure clusters</span></span>

<span data-ttu-id="6c417-141">실버 내구성 계층의 Azure 클러스터에는 복구 관리자 서비스가 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="6c417-142">골드 내구성 계층의 Azure 클러스터에는 해당 클러스터가 만들어진 시기에 따라 복구 관리자 서비스가 사용하도록 설정되어 있을 수도 있고 그렇지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="6c417-143">브론즈 내구성 계층의 Azure 클러스터에는 복구 관리자 서비스가 기본적으로 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="6c417-144">서비스가 이미 사용하도록 설정되어 있는 경우 Service Fabric Explorer의 시스템 서비스 섹션에서 서비스가 실행되고 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="6c417-145">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6c417-145">Azure portal</span></span>
<span data-ttu-id="6c417-146">클러스터를 설정할 때 Azure Portal에서 복구 관리자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="6c417-147">클러스터 구성 시 `Add on features`에서 `Include Repair Manager` 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="6c417-148">![Azure Portal에서 복구 관리자 사용 이미지](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="6c417-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="6c417-149">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="6c417-149">Azure Resource Manager template</span></span>
<span data-ttu-id="6c417-150">또는 [Azure Resource Manager 템플릿](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)을 사용하여 신규 및 기존 Service Fabric 클러스터에서 복구 관리자 서비스를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="6c417-151">배포하려는 클러스터에 대한 템플릿을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="6c417-152">예제 템플릿을 사용하거나 사용자 지정 Resource Manager 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="6c417-153">[Azure Resource Manager 템플릿](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)을 사용하여 복구 관리자 서비스를 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="6c417-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="6c417-154">먼저 다음 코드 조각과 같이 `Microsoft.ServiceFabric/clusters` 리소스에 대해 `apiversion`이 `2017-07-01-preview`로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="6c417-155">값이 다르면 `apiVersion`을 `2017-07-01-preview` 값으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="6c417-156">이제 아래와 같이 다음 `addonFeatures` 섹션을 `fabricSettings` 섹션 뒤에 추가하여 복구 관리자 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="6c417-157">이러한 변경 내용으로 클러스터 템플릿을 업데이트한 후 변경 내용을 적용하고 업그레이드가 완료되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="6c417-158">이제 클러스터에서 복구 관리자 시스템 서비스가 실행되고 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="6c417-159">Service Fabric Explorer의 시스템 서비스 섹션에 있는 `fabric:/System/RepairManagerService`입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="6c417-160">독립 실행형 온-프레미스 클러스터</span><span class="sxs-lookup"><span data-stu-id="6c417-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="6c417-161">[독립 실행형 Windows 클러스터에 대한 구성 설정](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest)을 사용하여 신규 및 기존 Service Fabric 클러스터에서 복구 관리자 서비스를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="6c417-162">복구 관리자 서비스를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="6c417-163">먼저 아래와 같이 [일반 클러스터 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations)의 `apiversion`이 `04-2017` 이상으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="6c417-164">이제 아래와 같이 다음 `addonFeaturres` 섹션을 `fabricSettings` 섹션 뒤에 추가하여 복구 관리자 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="6c417-165">업데이트된 클러스터 매니페스트의 [새 클러스터 만들기](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) 또는 [클러스터 구성 업그레이드](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration)를 사용하여 이러한 변경 내용으로 클러스터 매니페스트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="6c417-166">업데이트된 클러스터 매니페스트로 클러스터가 실행되면 Service Fabric Explorer의 시스템 서비스 섹션에서 `fabric:/System/RepairManagerService`라는, 클러스터에서 실행되고 있는 복구 관리자 시스템 서비스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="6c417-167">모든 노드에서 자동 Windows 업데이트 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="6c417-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="6c417-168">자동 Windows 업데이트를 사용하면 여러 클러스터 노드를 동시에 다시 시작할 수 있으므로 가용성 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="6c417-169">패치 오케스트레이션 앱은 기본적으로 각 클러스터 노드에서 자동 Windows 업데이트를 사용하지 않으려 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="6c417-170">그러나 설정이 관리자 또는 그룹 정책에 따라 관리되는 경우 명시적으로 Windows 업데이트 정책을 "다운로드하기 전에 알림"으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="6c417-171">선택 사항: Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="6c417-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="6c417-172">Service Fabric 런타임 버전 `5.6.220.9494` 이상을 실행하는 클러스터는 Service Fabric 로그의 일부로 패치 오케스트레이션 앱 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="6c417-173">클러스터가 Service Fabric 런타임 버전 `5.6.220.9494` 이상에서 실행 중인 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="6c417-174">Service Fabric 런타임 버전 `5.6.220.9494` 미만을 실행하는 클러스터의 경우 패치 오케스트레이션 앱에 대한 로그가 각 클러스터 노드에서 로컬로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="6c417-175">모든 노드에서 중앙 위치로 로그를 업로드하도록 Azure 진단을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="6c417-176">Azure 진단을 사용하도록 설정하는 방법에 대한 자세한 내용은 [Azure 진단을 사용하여 로그 수집](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c417-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="6c417-177">다음과 같은 고정된 공급자 ID에서 패치 오케스트레이션 앱의 로그가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="6c417-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="6c417-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="6c417-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="6c417-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="6c417-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="6c417-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="6c417-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="6c417-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="6c417-182">Resource Manager 템플릿에서 `WadCfg` 아래의 `EtwEventSourceProviderConfiguration` 섹션으로 이동한 후 다음 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="6c417-183">Service Fabric 클러스터에 여러 노드 형식이 있는 경우 이전 섹션은 모든 `WadCfg` 섹션에 대해 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="6c417-184">앱 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="6c417-184">Download the app package</span></span>

<span data-ttu-id="6c417-185">[다운로드 링크](https://go.microsoft.com/fwlink/P/?linkid=849590)에서 응용 프로그램을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="6c417-186">앱 구성</span><span class="sxs-lookup"><span data-stu-id="6c417-186">Configure the app</span></span>

<span data-ttu-id="6c417-187">요구 사항에 맞게 패치 오케스트레이션 앱의 동작을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="6c417-188">응용 프로그램 만들기 또는 업데이트 중에 응용 프로그램 매개 변수를 전달하여 기본값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="6c417-189">응용 프로그램 매개 변수는 `Start-ServiceFabricApplicationUpgrade` 또는 `New-ServiceFabricApplication` cmdlet에 `ApplicationParameter`를 지정하여 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="6c417-190">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="6c417-190">**Parameter**</span></span>        |<span data-ttu-id="6c417-191">**형식**</span><span class="sxs-lookup"><span data-stu-id="6c417-191">**Type**</span></span>                          | <span data-ttu-id="6c417-192">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="6c417-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="6c417-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="6c417-193">MaxResultsToCache</span></span>    |<span data-ttu-id="6c417-194">long</span><span class="sxs-lookup"><span data-stu-id="6c417-194">Long</span></span>                              | <span data-ttu-id="6c417-195">캐시되어야 하는 Windows 업데이트 결과의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="6c417-196">기본값은 3000입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="6c417-197">- 노드 수는 20입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="6c417-198">- 매월 노드에서 발생하는 업데이트 수는 5입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="6c417-199">- 작업당 결과 수는 10일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="6c417-200">- 지난 3개월 동안의 결과를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="6c417-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="6c417-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="6c417-202">열거형</span><span class="sxs-lookup"><span data-stu-id="6c417-202">Enum</span></span> <br> <span data-ttu-id="6c417-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="6c417-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="6c417-204">TaskApprovalPolicy는 Service Fabric 클러스터 노드에서 Windows 업데이트를 설치하기 위해 코디네이터 서비스에서 사용하는 정책을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="6c417-205">허용되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="6c417-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="6c417-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="6c417-207">Windows 업데이트가 한 번에 하나의 노드에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="6c417-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="6c417-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="6c417-209">Windows 업데이트가 한 번에 하나의 업그레이드 도메인에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="6c417-210">최대, 한 업그레이드 도메인에 속하는 모든 노드가 Windows 업데이트에 해당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="6c417-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="6c417-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="6c417-212">long</span><span class="sxs-lookup"><span data-stu-id="6c417-212">Long</span></span>  <br> <span data-ttu-id="6c417-213">(기본값: 1024)</span><span class="sxs-lookup"><span data-stu-id="6c417-213">(Default: 1024)</span></span>               |<span data-ttu-id="6c417-214">패치 오케스트레이션 앱 로그의 최대 크기(MB)로, 노드에서 로컬로 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="6c417-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="6c417-215">WUQuery</span></span>               | <span data-ttu-id="6c417-216">string</span><span class="sxs-lookup"><span data-stu-id="6c417-216">string</span></span><br><span data-ttu-id="6c417-217">(기본값: "IsInstalled = 0")</span><span class="sxs-lookup"><span data-stu-id="6c417-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="6c417-218">Windows 업데이트를 가져올 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-218">Query to get Windows updates.</span></span> <span data-ttu-id="6c417-219">자세한 내용은 [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c417-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="6c417-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="6c417-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="6c417-221">Bool</span><span class="sxs-lookup"><span data-stu-id="6c417-221">Bool</span></span> <br> <span data-ttu-id="6c417-222">(기본값: True)</span><span class="sxs-lookup"><span data-stu-id="6c417-222">(default: True)</span></span>                 | <span data-ttu-id="6c417-223">이 플래그를 사용하면 Windows 운영 체제 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="6c417-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="6c417-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="6c417-225">int</span><span class="sxs-lookup"><span data-stu-id="6c417-225">Int</span></span> <br><span data-ttu-id="6c417-226">(기본값: 90)</span><span class="sxs-lookup"><span data-stu-id="6c417-226">(Default: 90)</span></span>                   | <span data-ttu-id="6c417-227">Windows 업데이트 작업에 대한 시간 제한을 지정합니다(검색, 다운로드 또는 설치).</span><span class="sxs-lookup"><span data-stu-id="6c417-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="6c417-228">지정된 시간 제한 내에 작업이 완료되지 않으면 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="6c417-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="6c417-229">WURescheduleCount</span></span>     | <span data-ttu-id="6c417-230">int</span><span class="sxs-lookup"><span data-stu-id="6c417-230">Int</span></span> <br> <span data-ttu-id="6c417-231">(기본값: 5)</span><span class="sxs-lookup"><span data-stu-id="6c417-231">(Default: 5)</span></span>                  | <span data-ttu-id="6c417-232">작업이 영구적으로 실패하는 경우 서비스에서 Windows 업데이트를 다시 예약하는 최대 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="6c417-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="6c417-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="6c417-234">int</span><span class="sxs-lookup"><span data-stu-id="6c417-234">Int</span></span> <br><span data-ttu-id="6c417-235">(기본값: 30)</span><span class="sxs-lookup"><span data-stu-id="6c417-235">(Default: 30)</span></span> | <span data-ttu-id="6c417-236">오류가 계속 발생하는 경우 서비스에서 Windows 업데이트를 다시 예약하는 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="6c417-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="6c417-237">WUFrequency</span></span>           | <span data-ttu-id="6c417-238">쉼표로 구분된 문자열(기본값: "매주, 수요일, 7시")</span><span class="sxs-lookup"><span data-stu-id="6c417-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="6c417-239">Windows Update를 설치하는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="6c417-240">형식 및 가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-240">The format and possible values are:</span></span> <br><span data-ttu-id="6c417-241">-   매월, DD,HH:MM:SS(예: 매월, 5,12:22:32)</span><span class="sxs-lookup"><span data-stu-id="6c417-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="6c417-242">-   매주, DAY,HH:MM:SS(예: 매주, 화요일, 12:22:32)</span><span class="sxs-lookup"><span data-stu-id="6c417-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="6c417-243">-   매일, HH:MM:SS(예: 매일, 12:22:32)</span><span class="sxs-lookup"><span data-stu-id="6c417-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="6c417-244">-   [없음]은 Windows 업데이트를 수행하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="6c417-245">모든 시간은 UTC 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="6c417-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="6c417-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="6c417-247">Bool</span><span class="sxs-lookup"><span data-stu-id="6c417-247">Bool</span></span> <br><span data-ttu-id="6c417-248">(기본값: True)</span><span class="sxs-lookup"><span data-stu-id="6c417-248">(Default: true)</span></span> | <span data-ttu-id="6c417-249">이 플래그를 설정하면 응용 프로그램이 컴퓨터의 소유자를 대신하여 Windows 업데이트에 대한 최종 사용자 사용권 계약에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="6c417-250">Windows 업데이트가 즉시 처리되도록 하려면 응용 프로그램 배포 시간에 관한 `WUFrequency`를 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="6c417-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="6c417-251">예를 들어 5노드 테스트 클러스터가 있고 약 5PM UTC에 앱을 배포할 계획이라고 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="6c417-252">응용 프로그램 업그레이드 또는 배포에 최대 30분이 소요된다고 가정하는 경우 WUFrequency를 "매일, 17:30:00"으로 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="6c417-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="6c417-253">앱 배포</span><span class="sxs-lookup"><span data-stu-id="6c417-253">Deploy the app</span></span>

1. <span data-ttu-id="6c417-254">모든 필수 구성 요소 단계를 완료하여 클러스터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="6c417-255">다른 Service Fabric 앱과 마찬가지로 패치 오케스트레이션 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="6c417-256">PowerShell을 사용하여 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="6c417-257">[PowerShell을 사용하여 응용 프로그램 배포 및 제거](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="6c417-258">배포 시 응용 프로그램을 구성하려면 `ApplicationParamater`를 `New-ServiceFabricApplication` cmdlet에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="6c417-259">편의를 위해 Deploy.ps1 스크립트가 응용 프로그램과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="6c417-260">스크립트를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-260">To use the script:</span></span>

    - <span data-ttu-id="6c417-261">`Connect-ServiceFabricCluster`를 사용하여 Service Fabric 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="6c417-262">적절한 `ApplicationParameter` 값을 사용하여 PowerShell 스크립트 Deploy.ps1을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="6c417-263">스크립트 및 응용 프로그램 폴더 PatchOrchestrationApplication을 동일한 디렉터리에 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="6c417-264">앱 업그레이드</span><span class="sxs-lookup"><span data-stu-id="6c417-264">Upgrade the app</span></span>

<span data-ttu-id="6c417-265">PowerShell을 사용하여 기존 패치 오케스트레이션 앱을 업그레이드하려면 [PowerShell을 사용하여 Service Fabric 응용 프로그램 업그레이드](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="6c417-266">앱 제거</span><span class="sxs-lookup"><span data-stu-id="6c417-266">Remove the app</span></span>

<span data-ttu-id="6c417-267">응용 프로그램을 제거하려면 [PowerShell을 사용하여 응용 프로그램 배포 및 제거](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="6c417-268">편의를 위해 Undeploy.ps1 스크립트가 응용 프로그램과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="6c417-269">스크립트를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-269">To use the script:</span></span>

  - <span data-ttu-id="6c417-270">```Connect-ServiceFabricCluster```를 사용하여 Service Fabric 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="6c417-271">PowerShell 스크립트 Undeploy.ps1을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="6c417-272">스크립트 및 응용 프로그램 폴더 PatchOrchestrationApplication을 동일한 디렉터리에 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="6c417-273">Windows 업데이트 결과 보기</span><span class="sxs-lookup"><span data-stu-id="6c417-273">View the Windows Update results</span></span>

<span data-ttu-id="6c417-274">패치 오케스트레이션 앱은 사용자에게 기록 결과를 표시하는 REST API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="6c417-275">결과 JSON의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-275">An example of the result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="6c417-276">업데이트가 아직 예약되어 있지 않으면 결과 JSON은 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="6c417-277">Windows 업데이트 결과를 쿼리하려면 클러스터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="6c417-278">그런 다음 주 코디네이터 서비스의 복제본 주소를 찾아 브라우저에서 URL을 입력합니다(http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults).</span><span class="sxs-lookup"><span data-stu-id="6c417-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="6c417-279">코디네이터 서비스의 REST 끝점에는 동적 포트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="6c417-280">정확한 URL을 확인하려면 Service Fabric Explorer를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c417-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="6c417-281">예를 들어 `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`에 결과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![REST 끝점의 이미지](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="6c417-283">클러스터에서 역방향 프록시를 사용하는 경우 사용자는 클러스터 외부에서도 URL에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="6c417-284">적중되어야 하는 끝점은 http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="6c417-285">클러스터에서 역방향 프록시를 사용하려면 [Azure Service Fabric의 역방향 프록시](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)에 있는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="6c417-286">역방향 프록시가 구성된 후에는 HTTP 끝점을 표시하는 클러스터에 있는 모든 마이크로 서비스의 주소를 클러스터 외부에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="6c417-287">진단/상태 이벤트</span><span class="sxs-lookup"><span data-stu-id="6c417-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="6c417-288">패치 오케스트레이션 앱 로그 수집</span><span class="sxs-lookup"><span data-stu-id="6c417-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="6c417-289">런타임 버전 `5.6.220.9494` 이상에서는 Service Fabric 로그의 일부로 패치 오케스트레이션 앱 로그가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="6c417-290">`5.6.220.9494` 이하의 Service Fabric 런타임 버전을 실행하는 클러스터에서는 다음 방법 중 하나를 사용하여 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="6c417-291">각 노드에 로컬로</span><span class="sxs-lookup"><span data-stu-id="6c417-291">Locally on each node</span></span>

<span data-ttu-id="6c417-292">Service Fabric 런타임 버전이 `5.6.220.9494` 미만인 경우 각 Service Fabric 클러스터 노드에서 로그가 로컬로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="6c417-293">로그에 액세스하는 위치는 \[Service Fabric\_설치\_드라이브\]:\\PatchOrchestrationApplication\\logs입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="6c417-294">예를 들어 Service Fabric이 드라이브 D에 설치된 경우 경로는 D:\\PatchOrchestrationApplication\\logs입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="6c417-295">중앙 위치</span><span class="sxs-lookup"><span data-stu-id="6c417-295">Central location</span></span>

<span data-ttu-id="6c417-296">Azure 진단이 필수 구성 요소 단계의 일부로 구성된 경우 Azure Storage에서 패치 오케스트레이션 앱 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="6c417-297">상태 보고서</span><span class="sxs-lookup"><span data-stu-id="6c417-297">Health reports</span></span>

<span data-ttu-id="6c417-298">패치 오케스트레이션 앱은 다음과 같은 경우에도 코디네이터 서비스 또는 노드 에이전트 서비스에 대한 상태 보고서를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="6c417-299">Windows 업데이트 작업 실패</span><span class="sxs-lookup"><span data-stu-id="6c417-299">A Windows Update operation failed</span></span>

<span data-ttu-id="6c417-300">노드에서 Windows 업데이트 작업이 실패하면 노드 에이전트 서비스에 대한 상태 보고서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="6c417-301">상태 보고서의 세부 정보에 문제가 있는 노드 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="6c417-302">문제가 있는 노드에서 패치 작업이 성공적으로 완료되면 보고서가 자동으로 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="6c417-303">노드 에이전트 NTService 중단</span><span class="sxs-lookup"><span data-stu-id="6c417-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="6c417-304">노드에서 노드 에이전트 NTService가 중단되면 노드 에이전트 서비스에 대한 경고 수준 상태 보고서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="6c417-305">복구 관리자 서비스가 사용하도록 설정되지 않음</span><span class="sxs-lookup"><span data-stu-id="6c417-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="6c417-306">복구 관리자 서비스가 클러스터에 없는 경우 코디네이터 서비스에 대해 경고 수준 상태 보고서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="6c417-307">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="6c417-307">Frequently asked questions</span></span>

<span data-ttu-id="6c417-308">Q.</span><span class="sxs-lookup"><span data-stu-id="6c417-308">Q.</span></span> <span data-ttu-id="6c417-309">**패치 오케스트레이션 앱이 실행 중인 경우 오류 상태인 클러스터가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="6c417-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="6c417-310">A.</span><span class="sxs-lookup"><span data-stu-id="6c417-310">A.</span></span> <span data-ttu-id="6c417-311">패치 오케스트레이션 앱은 설치 과정에서 노드를 사용하지 않도록 설정하거나 다시 시작하므로 클러스터의 상태가 일시적으로 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="6c417-312">응용 프로그램의 정책에 따라 패치 작업 중에 하나의 노드가 중단되거나 *또는* 전체 업그레이드 도메인이 동시에 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="6c417-313">Windows 업데이트 설치가 끝날 때까지 노드는 다시 시작된 후 다시 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="6c417-314">다음 예제에서는 두 노드가 중단되고 MaxPercentageUnhealthNodes 정책이 위반되었으므로 클러스터가 일시적으로 오류 상태가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="6c417-315">이 오류는 패치 작업이 진행될 때까지 일시적으로 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-315">The error is temporary until the patching operation is ongoing.</span></span>

![비정상 클러스터의 이미지](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="6c417-317">문제가 계속되는 경우 문제 해결 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c417-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="6c417-318">Q.</span><span class="sxs-lookup"><span data-stu-id="6c417-318">Q.</span></span> <span data-ttu-id="6c417-319">**패치 오케스트레이션 앱이 경고 상태입니다.**</span><span class="sxs-lookup"><span data-stu-id="6c417-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="6c417-320">A.</span><span class="sxs-lookup"><span data-stu-id="6c417-320">A.</span></span> <span data-ttu-id="6c417-321">응용 프로그램에 대해 게시된 상태 보고서가 근본 원인인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="6c417-322">일반적으로 경고에는 문제에 대한 세부 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="6c417-323">문제가 일시적인 경우 응용 프로그램은 이 상태에서 자동으로 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="6c417-324">Q.</span><span class="sxs-lookup"><span data-stu-id="6c417-324">Q.</span></span> <span data-ttu-id="6c417-325">**클러스터가 비정상 상태이나 긴급한 운영 체제 업데이트를 수행해야 하는 경우 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="6c417-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="6c417-326">A.</span><span class="sxs-lookup"><span data-stu-id="6c417-326">A.</span></span> <span data-ttu-id="6c417-327">클러스터 상태가 정상이 아닌 경우 패치 오케스트레이션 앱은 업데이트를 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="6c417-328">패치 오케스트레이션 앱 워크플로의 차단을 해제하기 위해 클러스터를 정상 상태로 전환하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="6c417-329">Q.</span><span class="sxs-lookup"><span data-stu-id="6c417-329">Q.</span></span> <span data-ttu-id="6c417-330">**클러스터에 패치를 실행하는 데 시간이 너무 오래 걸리는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="6c417-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="6c417-331">A.</span><span class="sxs-lookup"><span data-stu-id="6c417-331">A.</span></span> <span data-ttu-id="6c417-332">패치 오케스트레이션 앱에 필요한 시간은 대개 다음과 같은 요인에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="6c417-333">코디네이터 서비스 정책</span><span class="sxs-lookup"><span data-stu-id="6c417-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="6c417-334">기본 정책인 `NodeWise`에 따라, 한 번에 하나의 노드에만 패치를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="6c417-335">특히 클러스터의 크기가 큰 경우 `UpgradeDomainWise` 정책을 사용하여 클러스터의 패치 적용 속도를 빠르게 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="6c417-336">다운로드 및 설치에 사용할 수 있는 업데이트 수</span><span class="sxs-lookup"><span data-stu-id="6c417-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="6c417-337">업데이트를 다운로드하고 설치하는 데 필요한 평균 시간, 1-2시간을 넘지 않아야 함</span><span class="sxs-lookup"><span data-stu-id="6c417-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="6c417-338">VM 및 네트워크 대역폭의 성능</span><span class="sxs-lookup"><span data-stu-id="6c417-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="6c417-339">Q.</span><span class="sxs-lookup"><span data-stu-id="6c417-339">Q.</span></span> <span data-ttu-id="6c417-340">**REST API를 통해 가져온 Windows Update 결과에 표시된 일부 업데이트가 컴퓨터에서 Windows Update 기록에서 표시되지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="6c417-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="6c417-341">A.</span><span class="sxs-lookup"><span data-stu-id="6c417-341">A.</span></span> <span data-ttu-id="6c417-342">일부 제품 업데이트는 해당하는 업데이트/패치 기록에서 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="6c417-343">예: Windows Defender 업데이트는 Windows Server 2016의 Windows 업데이트에서 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="6c417-344">고지 사항</span><span class="sxs-lookup"><span data-stu-id="6c417-344">Disclaimers</span></span>

- <span data-ttu-id="6c417-345">패치 오케스트레이션 앱은 사용자를 대신하여 Windows 업데이트에 대한 최종 사용자 사용권 계약에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="6c417-346">필요에 따라 응용 프로그램 구성에서 설정을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="6c417-347">패치 오케스트레이션 앱은 사용 및 성능을 추적하기 위해 원격 분석을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="6c417-348">응용 프로그램의 원격 분석은 Service Fabric 런타임의 원격 분석 설정을 따릅니다(기본적으로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="6c417-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6c417-349">문제 해결</span><span class="sxs-lookup"><span data-stu-id="6c417-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="6c417-350">노드가 활성 상태로 전환되지 않음</span><span class="sxs-lookup"><span data-stu-id="6c417-350">A node is not coming back to up state</span></span>

<span data-ttu-id="6c417-351">**노드는 다음과 같은 이유로 사용 불가능 상태에 멈춰 있을 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="6c417-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="6c417-352">안전 검사가 보류 중입니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-352">A safety check is pending.</span></span> <span data-ttu-id="6c417-353">이 문제를 해결하려면 정상 상태에서 충분히 노드를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="6c417-354">**노드는 다음과 같은 이유로 사용 안 함 상태에 멈춰 있을 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="6c417-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="6c417-355">노드가 수동으로 사용하지 않도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-355">The node was disabled manually.</span></span>
- <span data-ttu-id="6c417-356">노드가 진행 중인 Azure 인프라 작업으로 인해 사용하지 않도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="6c417-357">노드가 노드를 패치하는 패치 오케스트레이션 앱에 의해 일시적으로 사용하지 않도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="6c417-358">**노드는 다음과 같은 이유로 중단 상태에 멈춰 있을 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="6c417-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="6c417-359">노드가 수동으로 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="6c417-360">노드가 다시 시작하는 중입니다(패치 오케스트레이션 앱에 의해 트리거될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="6c417-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="6c417-361">노드가 결함이 있는 VM, 컴퓨터 또는 네트워크 연결 문제로 인해 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="6c417-362">일부 노드에서 업데이트를 건너뛰었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="6c417-363">패치 오케스트레이션 앱은 다시 예약 정책에 따라 Windows 업데이트를 설치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="6c417-364">이 서비스는 노드를 복구하고 응용 프로그램 정책에 따라 업데이트를 건너뛰려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="6c417-365">이러한 경우에 노드 에이전트 서비스에 대한 경고 수준 상태 보고서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="6c417-366">Windows 업데이트 결과에도 가능한 실패 원인이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="6c417-367">업데이트가 설치되는 동안 클러스터의 상태가 오류로 전환됨</span><span class="sxs-lookup"><span data-stu-id="6c417-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="6c417-368">잘못된 Windows 업데이트는 특정 노드 또는 업그레이드 도메인에 있는 응용 프로그램 또는 클러스터의 상태를 중단시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="6c417-369">패치 오케스트레이션 앱은 클러스터가 다시 정상 상태가 될 때까지 후속 Windows 업데이트 작업을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="6c417-370">관리자가 개입하여 Windows 업데이트로 인해 응용 프로그램 또는 클러스터가 비정상 상태가 된 이유를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c417-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="6c417-371">릴리스 정보:</span><span class="sxs-lookup"><span data-stu-id="6c417-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="6c417-372">버전 1.1.0</span><span class="sxs-lookup"><span data-stu-id="6c417-372">Version 1.1.0</span></span>
- <span data-ttu-id="6c417-373">공개 릴리스</span><span class="sxs-lookup"><span data-stu-id="6c417-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="6c417-374">버전 1.1.1</span><span class="sxs-lookup"><span data-stu-id="6c417-374">Version 1.1.1</span></span>
- <span data-ttu-id="6c417-375">NodeAgentNTService의 설치를 방지하는 NodeAgentService의 SetupEntryPoint에서 버그 수정</span><span class="sxs-lookup"><span data-stu-id="6c417-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="6c417-376">버전 1.2.0(최신)</span><span class="sxs-lookup"><span data-stu-id="6c417-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="6c417-377">시스템 다시 시작 워크플로 관련 버그 수정</span><span class="sxs-lookup"><span data-stu-id="6c417-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="6c417-378">복구 중 상태 확인이 예상 대로 작동하지 않는 문제로 인해 RM 작업 생성의 버그 수정</span><span class="sxs-lookup"><span data-stu-id="6c417-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="6c417-379">Windows 서비스 POANodeSvc 시작 모드를 자동에서 지연 자동으로 변경</span><span class="sxs-lookup"><span data-stu-id="6c417-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
