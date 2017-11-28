---
title: "서비스 패브릭 패치 오케스트레이션 응용 프로그램 aaaAzure | Microsoft Docs"
description: "응용 프로그램 tooautomate 운영 체제 서비스 패브릭 클러스터에 패치를 적용 합니다."
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
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="ad2c7-103">서비스 패브릭 클러스터에 hello Windows 운영 체제 패치</span><span class="sxs-lookup"><span data-stu-id="ad2c7-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="ad2c7-104">hello 패치 오케스트레이션 응용 프로그램은 Azure에서 가동 중지 시간 없이 서비스 패브릭 클러스터에 패치를 적용 하는 운영 체제를 자동화 하는 Azure 서비스 패브릭 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="ad2c7-105">hello 패치 오케스트레이션 앱 hello 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="ad2c7-106">**자동 운영 체제 업데이트 설치**.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="ad2c7-107">운영 체제 업데이트가 자동으로 다운로드되고 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="ad2c7-108">클러스터 노드는 필요에 따라 클러스터 가동 중지 시간 없이 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="ad2c7-109">**클러스터 인식 패치 및 상태 통합**.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="ad2c7-110">업데이트를 적용 하는 동안 hello 패치 오케스트레이션 앱 hello 클러스터 노드의 hello 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="ad2c7-111">클러스터 노드는 한 번에 하나의 노드씩 또는 한 번에 하나의 업그레이드 도메인씩 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="ad2c7-112">Hello 클러스터의 hello 상태 toohello 패치 프로세스 인해 다운 되 면 hello 문제 만나볼 수도 중지 tooprevent은 패치를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="ad2c7-113">Hello 응용 프로그램의 내부 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ad2c7-113">Internal details of hello app</span></span>

<span data-ttu-id="ad2c7-114">hello 패치 오케스트레이션 앱 hello 하위 구성 요소를 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="ad2c7-115">**코디네이터 서비스**: 이 상태 저장 서비스는 다음과 같은 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="ad2c7-116">Hello 전체 클러스터에서 hello Windows 업데이트 작업을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="ad2c7-117">완료 된 Windows 업데이트 작업의 hello 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="ad2c7-118">**노드 에이전트 서비스**: 이 상태 비저장 서비스는 모든 Service Fabric 클러스터 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="ad2c7-119">hello 서비스는 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="ad2c7-120">Hello 에이전트 NTService 노드를 부트스트랩 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="ad2c7-121">노드 에이전트 NTService hello를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="ad2c7-122">**노드 에이전트 NTService**: 이 Windows NT 서비스는 더 높은 수준의 권한(시스템)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="ad2c7-123">반면, hello 노드 에이전트 서비스 및 hello 코디네이터 서비스 하위 수준의 권한 (네트워크 서비스)에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="ad2c7-124">hello 서비스는 hello 모든 hello 클러스터 노드에서 Windows 업데이트 작업을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="ad2c7-125">Hello 노드에서 자동 Windows Update를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="ad2c7-126">다운로드 및 설치 Windows Update toohello 정책 hello 사용자에 따라 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="ad2c7-127">Hello 컴퓨터 post Windows 업데이트 설치를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="ad2c7-128">Windows 업데이트 toohello Coordinator 서비스의 hello 결과 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="ad2c7-129">모든 재시도가 끝난 다음 작업이 실패한 경우 상태 보고서 보고</span><span class="sxs-lookup"><span data-stu-id="ad2c7-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2c7-130">hello 패치 오케스트레이션 응용 프로그램 사용 하 여 hello 서비스 패브릭 관리자 시스템 서비스 toodisable 복구 또는 hello 노드를 사용 하도록 설정 및 상태 확인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="ad2c7-131">hello 패치 오케스트레이션 앱 트랙 hello 각 노드에 대 한 Windows Update 진행률 만든 hello 복구 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad2c7-132">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ad2c7-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="ad2c7-133">지원되는 최소 Service Fabric 런타임 버전</span><span class="sxs-lookup"><span data-stu-id="ad2c7-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="ad2c7-134">Azure 클러스터</span><span class="sxs-lookup"><span data-stu-id="ad2c7-134">Azure clusters</span></span>
<span data-ttu-id="ad2c7-135">서비스 패브릭 런타임에서 버전 v 5.5 Azure 클러스터에서 실행 해야 하는 hello 패치 오케스트레이션 앱 이상.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="ad2c7-136">독립 실행형 온-프레미스 클러스터</span><span class="sxs-lookup"><span data-stu-id="ad2c7-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="ad2c7-137">서비스 패브릭 런타임에서 버전 v5.6 있는 독립 실행형 클러스터에서 실행 해야 하는 hello 패치 오케스트레이션 앱 이상.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="ad2c7-138">(아직 실행 되지 않는) 하는 경우에 hello 복구 관리자 서비스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ad2c7-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="ad2c7-139">hello 패치 오케스트레이션 앱 hello 복구 관리자 시스템 서비스 toobe hello 클러스터에서 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="ad2c7-140">Azure 클러스터</span><span class="sxs-lookup"><span data-stu-id="ad2c7-140">Azure clusters</span></span>

<span data-ttu-id="ad2c7-141">Hello 은색 내구성 계층에 azure 클러스터에는 hello 복구 관리자 서비스를 기본적으로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="ad2c7-142">Hello 골드 내구성 계층에 azure 클러스터 수 또는 hello 복구 관리자 서비스는 클러스터가 작성 된 경우에 따라 사용할 수 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="ad2c7-143">기본적으로 hello 브론즈 내구성 계층에서 azure 클러스터 복구 관리자 서비스를 사용 하는 hello가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="ad2c7-144">Hello 서비스를 사용 하는 이미 실행 hello 서비스 패브릭 탐색기 hello 시스템 서비스 섹션에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="ad2c7-145">Azure portal</span><span class="sxs-lookup"><span data-stu-id="ad2c7-145">Azure portal</span></span>
<span data-ttu-id="ad2c7-146">클러스터의 설정 hello 시 Azure 포털에서 복구 관리자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="ad2c7-147">선택 `Include Repair Manager` 옵션에서 `Add on features` hello 시 클러스터 구성.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="ad2c7-148">![Azure Portal에서 복구 관리자 사용 이미지](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="ad2c7-149">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="ad2c7-149">Azure Resource Manager template</span></span>
<span data-ttu-id="ad2c7-150">Hello 또는 사용할 수 있습니다 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello 복구 관리자 서비스 신규 및 기존 서비스 패브릭 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="ad2c7-151">원하는 toodeploy hello 클러스터에 대 한 hello 서식 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="ad2c7-152">Hello 예제 서식 파일을 사용 하거나 사용자 지정 리소스 관리자 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="ad2c7-153">tooenable hello 복구 관리자 서비스를 사용 하 여 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="ad2c7-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="ad2c7-154">먼저 해당 hello 확인 `apiversion` 너무 설정`2017-07-01-preview` hello에 대 한 `Microsoft.ServiceFabric/clusters` 리소스를 hello 다음 코드 조각에에서 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="ad2c7-155">다를 경우 tooupdate hello 필요한 `apiVersion` toohello 값 `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="ad2c7-156">Hello 다음을 추가 하 여 hello 복구 관리자 서비스를 사용 하는 이제 `addonFeatures` hello 후 섹션 `fabricSettings` 섹션:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="ad2c7-157">클러스터 서식 파일을 이러한 변경 내용으로 업데이트 한 후에 적용 하 고 hello 업그레이드를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="ad2c7-158">이제 클러스터에서 실행 하는 hello 복구 관리자 시스템 서비스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="ad2c7-159">호출 될 `fabric:/System/RepairManagerService` hello 서비스 패브릭 탐색기 hello 시스템 서비스 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="ad2c7-160">독립 실행형 온-프레미스 클러스터</span><span class="sxs-lookup"><span data-stu-id="ad2c7-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="ad2c7-161">Hello를 사용할 수 있습니다 [독립 실행형 Windows 클러스터에 대 한 구성 설정을](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello 복구 관리자 서비스 신규 및 기존 서비스 패브릭 클러스터를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="ad2c7-162">tooenable hello 복구 관리자 서비스:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="ad2c7-163">먼저 해당 hello 확인 `apiversion` 에 [일반 클러스터 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) 너무 설정`04-2017` 이상:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="ad2c7-164">Hello 다음을 추가 하 여 복구 관리자 서비스를 사용 하는 이제 `addonFeaturres` hello 후 섹션 `fabricSettings` 아래와 같이 섹션:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="ad2c7-165">클러스터 매니페스트를 업데이트 하는 hello 클러스터 매니페스트를 사용 하 여 이러한 변경 내용으로 업데이트 [새 클러스터를 만들](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) 또는 [업그레이드 hello 클러스터 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="ad2c7-166">업데이트 된 클러스터 매니페스트가 있는 hello 클러스터를 실행 하 고 볼 수 있습니다 hello 복구 관리자 시스템 서비스가 호출 하 여 클러스터에서 실행 되 고 `fabric:/System/RepairManagerService`아래에서 서비스 섹션 hello 서비스 패브릭 탐색기에서 시스템.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="ad2c7-167">모든 노드에서 자동 Windows 업데이트 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ad2c7-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="ad2c7-168">여러 개의 클러스터 노드를 다시 시작할 수 hello에서 동일 하기 때문에 Windows 자동 업데이트 tooavailability 손실이 발생할 수 있습니다 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="ad2c7-169">hello 패치 오케스트레이션 앱 시도 toodisable 기본적으로 각 클러스터 노드에서 Windows 업데이트 자동 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="ad2c7-170">그러나 경우 hello 설정을 관리자 또는 그룹 정책 관리, 정책 너무 "알림 다운로드 하기 전에" 명시적으로 Windows Update 설정을 hello 보세요.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="ad2c7-171">선택 사항: Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="ad2c7-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="ad2c7-172">Service Fabric 런타임 버전 `5.6.220.9494` 이상을 실행하는 클러스터는 Service Fabric 로그의 일부로 패치 오케스트레이션 앱 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="ad2c7-173">클러스터가 Service Fabric 런타임 버전 `5.6.220.9494` 이상에서 실행 중인 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="ad2c7-174">서비스 패브릭 런타임 버전을 실행 하는 클러스터에 대 한 보다 작은 `5.6.220.9494`, 각 클러스터 노드에서 hello hello 패치 오케스트레이션 응용 프로그램에 대 한 로그는 로컬로 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="ad2c7-175">모든 노드 tooa 중앙 위치에서 Azure 진단 tooupload 로그를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="ad2c7-176">Azure 진단을 사용하도록 설정하는 방법에 대한 자세한 내용은 [Azure 진단을 사용하여 로그 수집](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="ad2c7-177">Hello 패치 오케스트레이션 응용 프로그램에 대 한 로그 Id 공급자를 고정 하는 hello에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="ad2c7-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="ad2c7-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="ad2c7-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="ad2c7-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="ad2c7-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="ad2c7-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="ad2c7-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="ad2c7-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="ad2c7-182">리소스 관리자 템플릿 goto에서 `EtwEventSourceProviderConfiguration` 섹션 아래 `WadCfg` hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

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
> <span data-ttu-id="ad2c7-183">서비스 패브릭 클러스터에 여러 노드 유형에 경우 모든 hello에 대 한 hello 이전 섹션을 추가 해야 `WadCfg` 섹션.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="ad2c7-184">Hello 응용 프로그램 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-184">Download hello app package</span></span>

<span data-ttu-id="ad2c7-185">Hello에서 hello 응용 프로그램을 다운로드 [다운로드 링크](https://go.microsoft.com/fwlink/P/?linkid=849590)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="ad2c7-186">Hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ad2c7-186">Configure hello app</span></span>

<span data-ttu-id="ad2c7-187">hello hello 패치 오케스트레이션 응용 프로그램의 동작 구성된 toomeet 사용자 요구 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="ad2c7-188">응용 프로그램 만들기 또는 업데이트 중 hello 응용 프로그램 매개 변수를 전달 하 여 hello 기본값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="ad2c7-189">응용 프로그램 매개 변수를 지정 하 여 제공 될 수 있습니다 `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` 또는 `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="ad2c7-190">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-190">**Parameter**</span></span>        |<span data-ttu-id="ad2c7-191">**형식**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-191">**Type**</span></span>                          | <span data-ttu-id="ad2c7-192">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="ad2c7-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="ad2c7-193">MaxResultsToCache</span></span>    |<span data-ttu-id="ad2c7-194">long</span><span class="sxs-lookup"><span data-stu-id="ad2c7-194">Long</span></span>                              | <span data-ttu-id="ad2c7-195">캐시되어야 하는 Windows 업데이트 결과의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="ad2c7-196">기본값은 3000입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="ad2c7-197">- 노드 수는 20입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="ad2c7-198">- 매월 노드에서 발생하는 업데이트 수는 5입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="ad2c7-199">- 작업당 결과 수는 10일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="ad2c7-200">-지난 3 달 동안 hello에 대 한 결과 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="ad2c7-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="ad2c7-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="ad2c7-202">열거형</span><span class="sxs-lookup"><span data-stu-id="ad2c7-202">Enum</span></span> <br> <span data-ttu-id="ad2c7-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="ad2c7-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="ad2c7-204">TaskApprovalPolicy는 toobe hello 서비스 패브릭 클러스터 노드 전체 hello 코디네이터 서비스 tooinstall Windows 업데이트에서 사용 하는 hello 정책을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="ad2c7-205">허용되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="ad2c7-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="ad2c7-207">Windows 업데이트가 한 번에 하나의 노드에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="ad2c7-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="ad2c7-209">Windows 업데이트가 한 번에 하나의 업그레이드 도메인에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="ad2c7-210">(최대 hello에서 tooan 업그레이드 도메인에 속하는 모든 hello 노드 이동할 수 있습니다 Windows Update에 대 한.)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="ad2c7-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="ad2c7-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="ad2c7-212">long</span><span class="sxs-lookup"><span data-stu-id="ad2c7-212">Long</span></span>  <br> <span data-ttu-id="ad2c7-213">(기본값: 1024)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-213">(Default: 1024)</span></span>               |<span data-ttu-id="ad2c7-214">패치 오케스트레이션 앱 로그의 최대 크기(MB)로, 노드에서 로컬로 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="ad2c7-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="ad2c7-215">WUQuery</span></span>               | <span data-ttu-id="ad2c7-216">string</span><span class="sxs-lookup"><span data-stu-id="ad2c7-216">string</span></span><br><span data-ttu-id="ad2c7-217">(기본값: "IsInstalled = 0")</span><span class="sxs-lookup"><span data-stu-id="ad2c7-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="ad2c7-218">쿼리 tooget 창을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-218">Query tooget Windows updates.</span></span> <span data-ttu-id="ad2c7-219">자세한 내용은 [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="ad2c7-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="ad2c7-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="ad2c7-221">Bool</span><span class="sxs-lookup"><span data-stu-id="ad2c7-221">Bool</span></span> <br> <span data-ttu-id="ad2c7-222">(기본값: True)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-222">(default: True)</span></span>                 | <span data-ttu-id="ad2c7-223">이 플래그는 Windows를 운영 체제 업데이트 toobe 설치 되어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="ad2c7-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="ad2c7-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="ad2c7-225">int</span><span class="sxs-lookup"><span data-stu-id="ad2c7-225">Int</span></span> <br><span data-ttu-id="ad2c7-226">(기본값: 90)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-226">(Default: 90)</span></span>                   | <span data-ttu-id="ad2c7-227">모든 Windows 업데이트 작업 (예: 검색 또는 다운로드 또는 설치)에 대 한 hello 제한 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="ad2c7-228">Hello 작업 내에서 완료 되지 않은 경우 지정 된 시간 제한 hello, 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="ad2c7-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="ad2c7-229">WURescheduleCount</span></span>     | <span data-ttu-id="ad2c7-230">int</span><span class="sxs-lookup"><span data-stu-id="ad2c7-230">Int</span></span> <br> <span data-ttu-id="ad2c7-231">(기본값: 5)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-231">(Default: 5)</span></span>                  | <span data-ttu-id="ad2c7-232">hello 최대 횟수 hello 서비스 다시 예약 하기 위해 hello 작업이 지속적으로 실패 하는 경우 Windows 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="ad2c7-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="ad2c7-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="ad2c7-234">int</span><span class="sxs-lookup"><span data-stu-id="ad2c7-234">Int</span></span> <br><span data-ttu-id="ad2c7-235">(기본값: 30)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-235">(Default: 30)</span></span> | <span data-ttu-id="ad2c7-236">서비스는 hello에 hello를 다시 예약 하는 hello 간격 오류가 계속 발생 하는 경우 Windows 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="ad2c7-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="ad2c7-237">WUFrequency</span></span>           | <span data-ttu-id="ad2c7-238">쉼표로 구분된 문자열(기본값: "매주, 수요일, 7시")</span><span class="sxs-lookup"><span data-stu-id="ad2c7-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="ad2c7-239">Windows 업데이트를 설치 하기 위한 hello 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="ad2c7-240">hello 형식 및 가능한 값은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-240">hello format and possible values are:</span></span> <br><span data-ttu-id="ad2c7-241">-   매월, DD,HH:MM:SS(예: 매월, 5,12:22:32)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="ad2c7-242">-   매주, DAY,HH:MM:SS(예: 매주, 화요일, 12:22:32)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="ad2c7-243">-   매일, HH:MM:SS(예: 매일, 12:22:32)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="ad2c7-244">-   [없음]은 Windows 업데이트를 수행하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="ad2c7-245">Hello 항상 UTC에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="ad2c7-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="ad2c7-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="ad2c7-247">Bool</span><span class="sxs-lookup"><span data-stu-id="ad2c7-247">Bool</span></span> <br><span data-ttu-id="ad2c7-248">(기본값: True)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-248">(Default: true)</span></span> | <span data-ttu-id="ad2c7-249">이 플래그를 설정 하 여 hello 응용 프로그램 hello 컴퓨터의 hello 소유자를 대신 하 여 hello Windows Update에 대 한 최종 사용자 사용권 계약을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="ad2c7-250">설정 하려는 경우 Windows Update toohappen 즉시, `WUFrequency` 상대 toohello 응용 프로그램 배포 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="ad2c7-251">예를 들어, 약 오후 5시는 테스트 다섯 개 노드 클러스터와 계획 toodeploy hello 앱 있는지 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="ad2c7-252">Hello 응용 프로그램 업그레이드 또는 배포에서 30 분 소요를 가정 하는 경우 "매일 17시 30분: 00입니다."로 설정 하 고 최대 hello WUFrequency hello</span><span class="sxs-lookup"><span data-stu-id="ad2c7-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="ad2c7-253">Hello 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ad2c7-253">Deploy hello app</span></span>

1. <span data-ttu-id="ad2c7-254">모든 hello 사전 요구 사항 단계 tooprepare hello 클러스터를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="ad2c7-255">서비스 패브릭 응용 프로그램 처럼 hello 패치 오케스트레이션 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="ad2c7-256">PowerShell을 사용 하 여 hello 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="ad2c7-257">Hello 단계에 따라 [PowerShell을 사용 하 여 배포 및 제거 응용 프로그램](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="ad2c7-258">패스 hello 배포의 hello 시 tooconfigure hello 응용 프로그램 `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="ad2c7-259">사용자 편의 위해 hello 스크립트 Deploy.ps1 hello 응용 프로그램과 함께 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="ad2c7-260">toouse hello 스크립트:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-260">toouse hello script:</span></span>

    - <span data-ttu-id="ad2c7-261">Tooa 서비스 패브릭 클러스터를 사용 하 여 연결 `Connect-ServiceFabricCluster`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="ad2c7-262">적절 한 hello로 hello PowerShell 스크립트 Deploy.ps1 실행 `ApplicationParameter` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2c7-263">Hello 스크립트와 hello 응용 프로그램 폴더 PatchOrchestrationApplication hello에 유지 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="ad2c7-264">Hello 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="ad2c7-264">Upgrade hello app</span></span>

<span data-ttu-id="ad2c7-265">PowerShell을 사용 하 여 기존 패치 오케스트레이션 앱 tooupgrade hello 단계에 따라 [PowerShell을 사용 하 여 서비스 패브릭 응용 프로그램 업그레이드](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="ad2c7-266">Hello 앱 제거</span><span class="sxs-lookup"><span data-stu-id="ad2c7-266">Remove hello app</span></span>

<span data-ttu-id="ad2c7-267">다음 단계에서 수행 hello tooremove hello 응용 프로그램 [PowerShell을 사용 하 여 배포 및 제거 응용 프로그램](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="ad2c7-268">사용자 편의 위해 hello 스크립트 Undeploy.ps1 hello 응용 프로그램과 함께 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="ad2c7-269">toouse hello 스크립트:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-269">toouse hello script:</span></span>

  - <span data-ttu-id="ad2c7-270">Tooa 서비스 패브릭 클러스터를 사용 하 여 연결 ```Connect-ServiceFabricCluster```합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="ad2c7-271">Undeploy.ps1 hello PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2c7-272">Hello 스크립트와 hello 응용 프로그램 폴더 PatchOrchestrationApplication hello에 유지 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="ad2c7-273">Hello Windows Update 결과 보기</span><span class="sxs-lookup"><span data-stu-id="ad2c7-273">View hello Windows Update results</span></span>

<span data-ttu-id="ad2c7-274">hello 패치 오케스트레이션 앱 REST Api toodisplay hello 기록 결과 toohello 사용자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="ad2c7-275">Hello 결과 JSON의 예:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-275">An example of hello result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
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
<span data-ttu-id="ad2c7-276">업데이트가 아직 예약 hello 결과 JSON 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="ad2c7-277">결과 toohello 클러스터 tooquery Windows Update에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="ad2c7-278">그런 다음 hello Coordinator 서비스의 기본 hello에 대 한 hello 복제 주소를 확인 하 고 hello 브라우저에서 URL hello 적중: http://&lt;복제본 IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v 1 / GetWindowsUpdateResults 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="ad2c7-279">hello 코디네이터 서비스에 대 한 hello REST 끝점에는 동적 포트를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="ad2c7-280">toocheck 정확한 URL hello, toohello 서비스 패브릭 탐색기를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="ad2c7-281">예를 들어 hello 결과에서 제공 됩니다 `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![REST 끝점의 이미지](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="ad2c7-283">Hello 역방향 프록시 hello 클러스터에서 활성화 된 경우에 hello 클러스터 외부에서 hello URL을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="ad2c7-284">끝점에 필요한 toobe hello 적중은 http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="ad2c7-285">hello 클러스터에서 tooenable hello 역방향 프록시 hello 단계에 따라 [역방향 프록시 Azure 서비스 패브릭에서](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="ad2c7-286">Hello 역방향 프록시를 구성한 후에 HTTP 끝점을 노출 하는 hello 클러스터의 모든 마이크로 서비스는 hello 클러스터 외부에서 주소 지정 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="ad2c7-287">진단/상태 이벤트</span><span class="sxs-lookup"><span data-stu-id="ad2c7-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="ad2c7-288">패치 오케스트레이션 앱 로그 수집</span><span class="sxs-lookup"><span data-stu-id="ad2c7-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="ad2c7-289">런타임 버전 `5.6.220.9494` 이상에서는 Service Fabric 로그의 일부로 패치 오케스트레이션 앱 로그가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="ad2c7-290">서비스 패브릭 런타임 버전을 실행 하는 클러스터에 대 한 보다 작은 `5.6.220.9494`, hello 메서드를 다음 중 하나를 사용 하 여 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="ad2c7-291">각 노드에 로컬로</span><span class="sxs-lookup"><span data-stu-id="ad2c7-291">Locally on each node</span></span>

<span data-ttu-id="ad2c7-292">Service Fabric 런타임 버전이 `5.6.220.9494` 미만인 경우 각 Service Fabric 클러스터 노드에서 로그가 로컬로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="ad2c7-293">hello tooaccess hello 로그 위치는 \[서비스 패브릭\_설치\_드라이브\]:\\PatchOrchestrationApplication\\로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="ad2c7-294">예를 들어 서비스 패브릭 D 드라이브에 설치 된 경우 hello 경로 d:\\PatchOrchestrationApplication\\로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="ad2c7-295">중앙 위치</span><span class="sxs-lookup"><span data-stu-id="ad2c7-295">Central location</span></span>

<span data-ttu-id="ad2c7-296">Azure 진단을 사전 요구 사항 단계의 일부로 구성 된 경우에 hello 패치 오케스트레이션 응용 프로그램에 대 한 로그는 Azure 저장소에서 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="ad2c7-297">상태 보고서</span><span class="sxs-lookup"><span data-stu-id="ad2c7-297">Health reports</span></span>

<span data-ttu-id="ad2c7-298">hello 패치 오케스트레이션 응용 프로그램의 경우 다음 hello에 엔터티에도 hello 코디네이터 서비스 또는 hello 노드 에이전트 서비스에 대 한 상태 보고서:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="ad2c7-299">Windows 업데이트 작업 실패</span><span class="sxs-lookup"><span data-stu-id="ad2c7-299">A Windows Update operation failed</span></span>

<span data-ttu-id="ad2c7-300">노드에서 Windows 업데이트 작업이 실패 하면 hello 노드 에이전트 서비스에 대 한 상태 보고서가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="ad2c7-301">Hello 상태 보고서의 정보는 hello 문제가 있는 노드 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="ad2c7-302">패치 hello 문제가 있는 노드에서 성공적으로 완료 되 면 후 hello 보고서 자동으로 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="ad2c7-303">hello 노드 에이전트 NTService 다운 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="ad2c7-304">Hello 노드 에이전트 NTService 노드에서 다운 되는 경우 경고 수준 상태 보고서는 hello 노드 에이전트 서비스에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="ad2c7-305">hello 복구 관리자 서비스는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="ad2c7-306">Hello 복구 관리자 서비스는 hello 클러스터에서 찾을 수 없습니다, hello 코디네이터 서비스에 대 한 경고 수준 상태 보고서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ad2c7-307">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="ad2c7-307">Frequently asked questions</span></span>

<span data-ttu-id="ad2c7-308">Q.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-308">Q.</span></span> <span data-ttu-id="ad2c7-309">**Hello 패치 오케스트레이션 응용 프로그램을 실행 하는 경우 오류 상태에 클러스터 나타나는 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="ad2c7-310">A.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-310">A.</span></span> <span data-ttu-id="ad2c7-311">Hello 설치 과정에서 hello 패치 오케스트레이션 응용 프로그램을 선택 하거나 일시적으로 중지 될 hello 클러스터의 hello 상태에서 발행할 수 있는 노드를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="ad2c7-312">Hello 응용 프로그램에 대 한 hello 정책에 따라, 어느 한 노드에서 감소할 수 있습니다 패치 작업 중 *또는* 전체 업그레이드 도메인 동시에 감소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="ad2c7-313">Windows Update 설치 hello 끝날 때 hello, 노드는 다시 사용 하도록 설정 하는 hello 다시 시작을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="ad2c7-314">다음 예제는 hello, hello 클러스터 tooan 오류 상태가 일시적으로 두 노드는 감소 하 고 hello MaxPercentageUnhealthNodes 정책 때문에 위반 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="ad2c7-315">패치 작업 hello 진행 될 때까지 hello 오류는 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![비정상 클러스터의 이미지](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="ad2c7-317">Hello 문제가 지속 되 면 toohello 문제 해결 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="ad2c7-318">Q.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-318">Q.</span></span> <span data-ttu-id="ad2c7-319">**패치 오케스트레이션 앱이 경고 상태입니다.**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="ad2c7-320">A.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-320">A.</span></span> <span data-ttu-id="ad2c7-321">Toosee hello 응용 프로그램에 대해 게시 된 상태 보고서가 hello 근본 원인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="ad2c7-322">일반적으로 hello 경고 hello 문제에 대 한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="ad2c7-323">Hello 문제가 일시적인 경우 hello 응용 프로그램은이 상태에서 예상된 tooauto 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="ad2c7-324">Q.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-324">Q.</span></span> <span data-ttu-id="ad2c7-325">**클러스터 손상 되었습니다. toodo 긴급 한 운영 체제 업데이트 해야 하는 경우 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="ad2c7-326">A.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-326">A.</span></span> <span data-ttu-id="ad2c7-327">반면 hello 클러스터는 정상인 hello 패치 오케스트레이션 앱 업데이트를 설치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="ad2c7-328">클러스터 tooa 정상 상태로 toounblock hello 패치 오케스트레이션 응용 프로그램 워크플로 toobring를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="ad2c7-329">Q.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-329">Q.</span></span> <span data-ttu-id="ad2c7-330">**이유는 클러스터 간에 패치 시간이 너무 오래 toorun?**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="ad2c7-331">A.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-331">A.</span></span> <span data-ttu-id="ad2c7-332">hello 패치 오케스트레이션 응용 프로그램에 필요한 hello 시간은 주로 hello 요소 뒤에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="ad2c7-333">hello Coordinator 서비스의 hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="ad2c7-334">기본 정책 hello `NodeWise`, 한 번에 하나의 노드만 패치 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="ad2c7-335">특히, 더 큰 클러스터의 hello 경우의에서 hello를 사용 하는 권장 `UpgradeDomainWise` 정책 tooachieve 빠른 클러스터 간에 패치를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="ad2c7-336">업데이트 다운로드 및 설치에 사용할 수 있는 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="ad2c7-337">필요한 평균 시간 toodownload hello 하 고 몇 시간을 초과 하지 않아야 하는 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="ad2c7-338">hello VM 및 네트워크 대역폭의 hello 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="ad2c7-339">Q.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-339">Q.</span></span> <span data-ttu-id="ad2c7-340">**Windows Update 결과에 포함 되지 않은 컴퓨터에서 Windows Update 기록 hello 하지만 REST api를 통해 얻은에서 일부 업데이트가 나타나는 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="ad2c7-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="ad2c7-341">A.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-341">A.</span></span> <span data-ttu-id="ad2c7-342">일부 제품 업데이트 해당 업데이트/패치 기록을 체크인 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="ad2c7-343">예: Windows Defender 업데이트는 Windows Server 2016의 Windows 업데이트에서 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="ad2c7-344">고지 사항</span><span class="sxs-lookup"><span data-stu-id="ad2c7-344">Disclaimers</span></span>

- <span data-ttu-id="ad2c7-345">hello 패치 오케스트레이션 앱 hello 사용자를 대신 하 여 hello Windows Update의 최종 사용자 사용권 계약을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="ad2c7-346">필요에 따라 hello 응용 프로그램의 hello 구성에서 hello 설정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="ad2c7-347">hello 패치 오케스트레이션 앱 원격 분석 tootrack 사용량 및 성능 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="ad2c7-348">hello 응용 프로그램의 원격 분석 hello 서비스 패브릭 런타임 원격 분석 설정 (기본적으로 켜져)의 hello 설정을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ad2c7-349">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ad2c7-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="ad2c7-350">노드 다시 발생 하지 않습니다 tooup 상태</span><span class="sxs-lookup"><span data-stu-id="ad2c7-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="ad2c7-351">**hello 노드 때문에 비활성화 된 상태에서 멈춰 있을 수 있습니다**:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="ad2c7-352">안전 검사가 보류 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-352">A safety check is pending.</span></span> <span data-ttu-id="ad2c7-353">tooremedy 이러한 상황을 정상 상태로 사용할 수 있는 충분 한 노드가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="ad2c7-354">**hello 노드 때문에 사용할 수 없는 상태에서 멈춰 있을 수 있습니다**:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="ad2c7-355">hello 노드는 수동으로 비활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="ad2c7-356">hello 노드 tooan 진행 중인 Azure 인프라 작업 인해 비활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="ad2c7-357">hello 노드 hello 패치 오케스트레이션 앱 toopatch hello 노드가 일시적으로 비활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="ad2c7-358">**hello 노드 멈춰 있을 수 있습니다 다운 상태에 있으므로**:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="ad2c7-359">hello 노드가 다운 상태에 수동으로 배치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="ad2c7-360">hello 노드 (있음 hello 패치 오케스트레이션 앱에 의해 트리거될 수 있습니다)를 다시 시작이 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="ad2c7-361">hello 노드 tooa 결함이 있는 VM 또는 컴퓨터 또는 네트워크 연결 문제로 인해 작동이 중단 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="ad2c7-362">일부 노드에서 업데이트를 건너뛰었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="ad2c7-363">hello 패치 오케스트레이션 앱 tooinstall Windows 업데이트에 따라 toohello 다시 예약 정책 하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="ad2c7-364">hello 서비스 toorecover hello 노드를 시도 하 고 hello 업데이트에 따라 toohello 응용 프로그램 정책을 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="ad2c7-365">이 경우 경고 수준 상태 보고서는 hello 노드 에이전트 서비스에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="ad2c7-366">Windows Update에 대 한 hello 결과는 hello 실패에 대 한 가능한 이유 hello 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="ad2c7-367">hello 클러스터의 hello 상태 보내고 tooerror hello 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="ad2c7-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="ad2c7-368">잘못 된 Windows update 응용 프로그램 또는 특정 노드 또는 업그레이드 도메인에 있는 클러스터의 hello 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="ad2c7-369">hello 패치 오케스트레이션 앱 hello 클러스터가 다시 정상 상태가 될 때까지 후속 Windows 업데이트 작업을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="ad2c7-370">관리자가 개입 하 고 이유 hello 응용 프로그램 또는 클러스터 비정상이 된 인해 결정 해야 tooWindows 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="ad2c7-371">릴리스 정보:</span><span class="sxs-lookup"><span data-stu-id="ad2c7-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="ad2c7-372">버전 1.1.0</span><span class="sxs-lookup"><span data-stu-id="ad2c7-372">Version 1.1.0</span></span>
- <span data-ttu-id="ad2c7-373">공개 릴리스</span><span class="sxs-lookup"><span data-stu-id="ad2c7-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="ad2c7-374">버전 1.1.1</span><span class="sxs-lookup"><span data-stu-id="ad2c7-374">Version 1.1.1</span></span>
- <span data-ttu-id="ad2c7-375">NodeAgentNTService의 설치를 방지하는 NodeAgentService의 SetupEntryPoint에서 버그 수정</span><span class="sxs-lookup"><span data-stu-id="ad2c7-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="ad2c7-376">버전 1.2.0(최신)</span><span class="sxs-lookup"><span data-stu-id="ad2c7-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="ad2c7-377">시스템 다시 시작 워크플로 관련 버그 수정</span><span class="sxs-lookup"><span data-stu-id="ad2c7-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="ad2c7-378">만들 복구 작업을 준비 하는 동안 toowhich 상태 검사에 예정 된 RM 작업의에서 버그 수정 예상 대로 발생 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="ad2c7-379">Windows 서비스 POANodeSvc 자동 toodelayed 자동에서 변경 된 hello 시작 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ad2c7-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
