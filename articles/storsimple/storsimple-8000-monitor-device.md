---
title: "aaaMonitor StorSimple 8000 시리즈 장치 | Microsoft Docs"
description: "StorSimple 장치 관리자 toouse hello toomonitor 사용량, I/O 성능 및 용량 사용률을 서비스 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a><span data-ttu-id="ca9d3-103">StorSimple 장치의 StorSimple 장치 관리자 서비스 toomonitor hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ca9d3-103">Use hello StorSimple Device Manager service toomonitor your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="ca9d3-104">개요</span><span class="sxs-lookup"><span data-stu-id="ca9d3-104">Overview</span></span>
<span data-ttu-id="ca9d3-105">StorSimple 솔루션 내에서 hello toomonitor 특정 장치 StorSimple 장치 관리자 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-105">You can use hello StorSimple Device Manager service toomonitor specific devices within your StorSimple solution.</span></span> <span data-ttu-id="ca9d3-106">I/O 성능, 용량 사용률, 네트워크 처리량 및 장치 성능 메트릭을 기준으로 하는 사용자 지정 차트를 만들고 해당 toohello 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-106">You can create custom charts based on I/O performance, capacity utilization, network throughput, and device performance metrics and pin those toohello dashboard.</span></span> <span data-ttu-id="ca9d3-107">자세한 내용은 이동 너무[포털 대시보드를 사용자 지정할](/articles/azure-portal/azure-portal-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-107">For more information, go too[customize your portal dashboard](/articles/azure-portal/azure-portal-dashboards.md).</span></span>

<span data-ttu-id="ca9d3-108">hello tooview hello Azure 포털에서에서 특정 장치에 대 한 모니터링 정보가 hello StorSimple 장치 관리자 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-108">tooview hello monitoring information for a specific device, in hello Azure portal, select hello StorSimple Device Manager service.</span></span> <span data-ttu-id="ca9d3-109">Hello 장치 목록에서 장치를 선택 하 고 이동 하 여 너무**모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-109">From hello list of devices, select your device and then go too**Monitor**.</span></span> <span data-ttu-id="ca9d3-110">Hello 확인할 수 있습니다 **용량**, **사용량**, 및 **성능** hello 선택한 장치에 대 한 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-110">You can then see hello **Capacity**, **Usage**, and **Performance** charts for hello selected device.</span></span>

## <a name="capacity"></a><span data-ttu-id="ca9d3-111">용량</span><span class="sxs-lookup"><span data-stu-id="ca9d3-111">Capacity</span></span>
<span data-ttu-id="ca9d3-112">**용량** 트랙 hello hello 장치에 남아 있는 hello 공간과 프로 비전 된 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-112">**Capacity** tracks hello provisioned space and hello space remaining on hello device.</span></span> <span data-ttu-id="ca9d3-113">남은 용량 hello 로컬로 고정 또는 계층으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-113">hello remaining capacity is then displayed as locally pinned or tiered.</span></span>

<span data-ttu-id="ca9d3-114">hello를 프로 비전 된 디스크 크기 및 남은 용량 계층화 된 볼륨과 로컬로 고정 된 볼륨으로 구분 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-114">hello provisioned and remaining capacity is further broken down by tiered and locally pinned volumes.</span></span> <span data-ttu-id="ca9d3-115">각 볼륨에 대 한 hello 용량을 프로 비전 하 고 용량 hello 장치에 남아 있는 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-115">For each volume, hello provisioned capacity and hello remaining capacity on hello device is displayed.</span></span>

![IO 수용작업량](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a><span data-ttu-id="ca9d3-117">사용</span><span class="sxs-lookup"><span data-stu-id="ca9d3-117">Usage</span></span>
<span data-ttu-id="ca9d3-118">**사용 현황** hello 볼륨, 볼륨 컨테이너 또는 장치에서 사용 되는 데이터 저장 공간의 양을 메트릭 관련된 toohello 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-118">**Usage** tracks metrics related toohello amount of data storage space that is used by hello volumes, volume containers, or device.</span></span> <span data-ttu-id="ca9d3-119">주 저장소, 클라우드 저장소, 또는 장치 저장소의 용량 사용률을 hello 기반으로 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-119">You can create reports based on hello capacity utilization of your primary storage, your cloud storage, or your device storage.</span></span> <span data-ttu-id="ca9d3-120">용량 사용률은 특정 볼륨, 특정 볼륨 컨테이너 또는 모든 볼륨 컨테이너에 대해 측정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-120">Capacity utilization can be measured on a specific volume, a specific volume container, or all volume containers.</span></span>
<span data-ttu-id="ca9d3-121">기본적으로 지난 24 시간에 대 한 hello 사용이 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-121">By default, hello usage for past 24 hours is reported.</span></span> <span data-ttu-id="ca9d3-122">Hello 차트 toochange hello 기간은 hello를 통해 사용량이에서 선택 하 여 보고 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-122">You can edit hello chart toochange hello duration over which hello usage is reported by selecting from:</span></span>
* <span data-ttu-id="ca9d3-123">지난 24시간</span><span class="sxs-lookup"><span data-stu-id="ca9d3-123">Past 24 hours</span></span>
* <span data-ttu-id="ca9d3-124">지난 7일간</span><span class="sxs-lookup"><span data-stu-id="ca9d3-124">Past 7 days</span></span>
* <span data-ttu-id="ca9d3-125">지난 30일간</span><span class="sxs-lookup"><span data-stu-id="ca9d3-125">Past 30 days</span></span>
* <span data-ttu-id="ca9d3-126">지난 90일간</span><span class="sxs-lookup"><span data-stu-id="ca9d3-126">Past 90 days</span></span>
* <span data-ttu-id="ca9d3-127">지난해</span><span class="sxs-lookup"><span data-stu-id="ca9d3-127">Past year</span></span>


<span data-ttu-id="ca9d3-128">기본 hello, 클라우드 및 사용 하는 로컬 저장소를 다음과 같이 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-128">hello primary, cloud, and local storage used can be described as follows:</span></span>

### <a name="primary-storage-usage"></a><span data-ttu-id="ca9d3-129">기본 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="ca9d3-129">Primary storage usage</span></span>
<span data-ttu-id="ca9d3-130">이러한 차트 hello hello 데이터 중복 제거 되 고 압축 되기 전에 tooStorSimple 볼륨을 기록 하는 데이터 양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-130">These charts show hello amount of data written tooStorSimple volumes before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="ca9d3-131">단일 볼륨 또는 볼륨 컨테이너에서 모든 볼륨에서 사용 하는 hello 주 저장소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-131">You can view hello primary storage used by all volumes in a volume container or for a single volume.</span></span> <span data-ttu-id="ca9d3-132">hello 기본 저장소 사용은 더 이상 기본 계층화 된 저장소 사용 되며 기본 로컬로 고정 된 저장소를 사용 하 여 나누어집니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-132">hello primary storage used is further broken down by primary tiered storage used and primary locally pinned storage used.</span></span>

<span data-ttu-id="ca9d3-133">hello 다음 차트 표시 하는 사용 하기 전에 StorSimple 장치의 클라우드 스냅숏을 만든 후 hello 기본 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-133">hello following charts show hello primary storage used for a StorSimple device before and after a cloud snapshot was taken.</span></span> <span data-ttu-id="ca9d3-134">볼륨 데이터만 그대로 클라우드 스냅숏 hello 주 저장소를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-134">As this is just volume data, a cloud snapshot should not change hello primary storage.</span></span> <span data-ttu-id="ca9d3-135">알 수 없는 차이에 따라 hello 기본 계층 구성 또는 로컬로 고정 된 클라우드 스냅숏을 만드는 결과로 사용 hello 차트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-135">As you can see, hello chart shows no difference in hello primary tiered or locally pinned storage used as a result of taking a cloud snapshot.</span></span> <span data-ttu-id="ca9d3-136">hello 클라우드 스냅숏 약 오후 11 시 50 분 해당 장치에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-136">hello cloud snapshot started at around 11:50 pm on that device.</span></span>

![클라우드 스냅숏 후 기본 용량 사용률](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

<span data-ttu-id="ca9d3-138">이제 hello 연결 호스트 tooyour StorSimple 장치에서 IO를 실행, 기본 계층화 된 저장소의 증가로 나타납니다 또는 기본 로컬 저장소 사용에 따라 고정 된 경우 계층 이동해 왔거나 로컬로 고정 볼륨에 있습니다 hello 데이터를 쓸 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-138">If you now run IO on hello host connected tooyour StorSimple device, you will see an increase in primary tiered storage or primary locally pinned storage used depending upon which volumes (tiered or locally pinned) you write hello data to.</span></span> <span data-ttu-id="ca9d3-139">StorSimple 장치에 대 한 hello 기본 저장소 사용 차트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-139">Here are hello primary storage usage charts for a StorSimple device.</span></span> <span data-ttu-id="ca9d3-140">이 장치에서 시작을 처리 하는 hello StorSimple 호스트 약 오후 2 시 30 분 hello 장치에 계층화 된 볼륨에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-140">On this device, hello StorSimple host started serving writes at around 2:30 pm on a tiered volume on hello device.</span></span> <span data-ttu-id="ca9d3-141">Hello 쓰기 바이트/s toohello IO hello 호스트에서 실행 중에 해당 hello 피크를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-141">You can see hello peak in hello write bytes/s corresponding toohello IO running on hello host.</span></span>

![계층화된 볼륨에서 IO를 실행 중인 경우 성능](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

<span data-ttu-id="ca9d3-143">Hello 기본 계층화 된 저장소를 사용 하는 수 만큼 로컬로 고정 hello 기본 사용 현황 변하지 않습니다 반면를 내려갔습니다를 보면 없습니다 쓰기 hello 장치에서 로컬로 고정 toohello 볼륨을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-143">If you look at hello primary tiered storage used, that has gone up whereas hello primary locally pinned usage stays unchanged as there are no writes served toohello locally pinned volumes on hello device.</span></span>

![계층화된 볼륨에서 IO를 실행 중인 경우 기본 수용작업량 사용률](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

<span data-ttu-id="ca9d3-145">실행 하는 경우 3를 업데이트 하거나 이상 나눌 수 있습니다 hello 주 저장소 용량 사용률이 개별 볼륨, 모든 볼륨을 계층화 된 볼륨을 모두 및 모든 로컬 고정된 볼륨에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-145">If you are running Update 3 or higher, you can break down hello primary storage capacity utilization by an individual volume, all volumes, all tiered volumes, and all locally pinned volumes as shown below.</span></span> <span data-ttu-id="ca9d3-146">모든 로컬로 고정 된 볼륨을 하면 별로 분석 tooquickly 모두 사용 hello 로컬 계층의 양을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-146">Breaking down by all locally pinned volumes will allow you tooquickly ascertain how much of hello local tier is used up.</span></span>

![모든 계층화된 볼륨에 대한 기본 수용작업량 사용률](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![모든 로컬 고정 볼륨에 대한 기본 용량 사용률](./media/storsimple-8000-monitor-device/monitor-usage4.png)

<span data-ttu-id="ca9d3-149">하면 더욱의 hello 볼륨 hello 목록에서 클릭 하 고 hello 해당 사용법을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-149">You can further click on each of hello volumes in hello list and see hello corresponding usage.</span></span>

![모든 로컬 고정 볼륨에 대한 기본 용량 사용률](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a><span data-ttu-id="ca9d3-151">클라우드 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="ca9d3-151">Cloud storage usage</span></span>
<span data-ttu-id="ca9d3-152">이러한 차트 hello 양을 클라우드 저장소 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-152">These charts show hello amount of cloud storage used.</span></span> <span data-ttu-id="ca9d3-153">이 데이터는 중복 제거되고 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-153">This data is deduplicated and compressed.</span></span> <span data-ttu-id="ca9d3-154">이 양에는 모든 기본 볼륨에 반영되지 않으며 레거시 또는 필수 보존 목적을 위해 유지되는 데이터를 포함할 수 있는 클라우드 스냅숏이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-154">This amount includes cloud snapshots which might contain data that isn't reflected in any primary volume and is kept for legacy or required retention purposes.</span></span> <span data-ttu-id="ca9d3-155">Hello 번호 정확한 수 없지만 기본 hello 및 클라우드 저장소 소비 수치 tooget hello 데이터 감소의 예측 등급을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-155">You can compare hello primary and cloud storage consumption figures tooget an idea of hello data reduction rate, although hello number will not be exact.</span></span>

<span data-ttu-id="ca9d3-156">hello 다음 차트 표시 hello 클라우드 저장소 사용 StorSimple 장치의 클라우드 스냅숏을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-156">hello following charts show hello cloud storage utilization of a StorSimple device when a cloud snapshot was taken.</span></span>

* <span data-ttu-id="ca9d3-157">hello 클라우드 스냅숏 약 오전 11시 50분 해당 장치에에서 시작 하 고 hello 클라우드 스냅숏 전에 볼 수 없는 클라우드 저장소를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-157">hello cloud snapshot started at around 11:50 am on that device and you can see that before hello cloud snapshot, there was no cloud storage used.</span></span> 
* <span data-ttu-id="ca9d3-158">한 번 hello 클라우드 스냅숏 완료, hello 클라우드 저장소 사용률 샷 0.89 GB를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-158">Once hello cloud snapshot completed, hello cloud storage utilization shot up 0.89 GB.</span></span> 
* <span data-ttu-id="ca9d3-159">Hello 클라우드 스냅숏 진행 중인 동안에 없는 경우 또한 해당 최대 장치 toocloud에서 IO hello</span><span class="sxs-lookup"><span data-stu-id="ca9d3-159">While hello cloud snapshot was in progress, there is also a corresponding peak in hello IO from device toocloud.</span></span>

    ![클라우드 스냅숏 이전 클라우드 저장소 사용률](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![클라우드 스냅숏 이후 클라우드 저장소 사용률](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![클라우드 스냅숏 중 장치 toocloud에서 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a><span data-ttu-id="ca9d3-163">로컬 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="ca9d3-163">Local storage usage</span></span>
<span data-ttu-id="ca9d3-164">이러한 차트는 hello 보다 더 큽니다 기본 저장소 사용량 hello SSD 선형 계층을 포함 하기 때문에 hello 장치에 대 한 총 사용률을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-164">These charts show hello total utilization for hello device, which will be more than primary storage usage because it includes hello SSD linear tier.</span></span> <span data-ttu-id="ca9d3-165">이 계층에도 있는 hello 다른 계층에 장치의 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-165">This tier contains an amount of data that also exists on hello device's other tiers.</span></span> <span data-ttu-id="ca9d3-166">hello 이전 데이터를 이동된 toohello HDD 계층 (이때 것은 중복 제거 및 압축 된) 및 이후에 toohello 클라우드 내에 새 데이터가 들어오면 있도록 hello 용량 hello SSD 선형 계층에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-166">hello capacity in hello SSD linear tier is cycled so that when new data comes in, hello old data is moved toohello HDD tier (at which time it is deduplicated and compressed) and subsequently toohello cloud.</span></span>

<span data-ttu-id="ca9d3-167">시간이 지남에 따라 사용 되는 및 로컬 저장소 사용 향상 시킵니다 함께 hello 데이터 toobe 시작 될 때까지 주 저장소 toohello 클라우드를 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-167">Over time, primary storage used and local storage used will most likely increase together until hello data begins toobe tiered toohello cloud.</span></span> <span data-ttu-id="ca9d3-168">해당 시점에 사용 하는 hello 로컬 저장소 tooplateau, 시작 아마도 하지만 더 많은 데이터를 기록할 때 사용 된 hello 기본 저장소 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-168">At that point, hello local storage used will probably begin tooplateau, but hello primary storage used will increase as more data is written.</span></span>

<span data-ttu-id="ca9d3-169">hello 다음 차트 표시 hello 기본 저장소 클라우드 스냅숏을 만들 때 StorSimple 장치에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-169">hello following charts show hello primary storage used for a StorSimple device when a cloud snapshot was taken.</span></span> <span data-ttu-id="ca9d3-170">hello 클라우드 스냅숏 오전 11시 50분에 시작 하 고 hello 로컬 저장소 감소 해당 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-170">hello cloud snapshot started at 11:50 am and hello local storage started decreasing at that time.</span></span> <span data-ttu-id="ca9d3-171">1.445 GB too1.09 GB에서에서 떨어졌다 hello 로컬 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-171">hello local storage used went down from 1.445 GB too1.09 GB.</span></span> <span data-ttu-id="ca9d3-172">이 가능성이 hello hello 선형 SSD 계층에 압축 되지 않은 데이터 중복 제거 된, 압축 못하고 나타냅니다 hello HDD 계층으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-172">This indicates that most likely hello uncompressed data in hello linear SSD tier was deduplicated, compressed, and moved into hello HDD tier.</span></span> <span data-ttu-id="ca9d3-173">참고는 hello 장치에 많은 양의 hello SSD 및 HDD 계층 데이터를 이미 있으면 나타나지 않을 수 있습니다이 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-173">Note that if hello device already has a large amount of data in both hello SSD and HDD tiers, you may not see this decrease.</span></span> <span data-ttu-id="ca9d3-174">이 예제에서는 hello 장치 적은 양의 데이터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-174">In this example, hello device has a small amount of data.</span></span>

![클라우드 스냅숏 이후 로컬 저장소 사용률](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a><span data-ttu-id="ca9d3-176">성능</span><span class="sxs-lookup"><span data-stu-id="ca9d3-176">Performance</span></span>
<span data-ttu-id="ca9d3-177">**성능** 메트릭을 추적 관련 읽기 toohello 번호 및에서 쓰기 작업 간에 어느 hello iSCSI 시작자 인터페이스 hello 호스트 서버 및 hello 장치 또는 hello 장치와 hello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-177">**Performance** tracks metrics related toohello number of read and write operations between either hello iSCSI initiator interfaces on hello host server and hello device or hello device and hello cloud.</span></span> <span data-ttu-id="ca9d3-178">이 성능은 특정 볼륨, 특정 볼륨 컨테이너 또는 모든 볼륨 컨테이너에 대해 측정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-178">This performance can be measured for a specific volume, a specific volume container, or all volume containers.</span></span> <span data-ttu-id="ca9d3-179">성능 및도 포함 되어 CPU 사용률 hello에 대 한 네트워크 처리량 장치에서 다양 한 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-179">Performance also includes CPU utilization and Network throughput for hello various network interfaces on your device.</span></span>

### <a name="io-performance-for-initiator-toodevice"></a><span data-ttu-id="ca9d3-180">초기자 toodevice에 대 한 I/O 성능</span><span class="sxs-lookup"><span data-stu-id="ca9d3-180">I/O performance for initiator toodevice</span></span>
<span data-ttu-id="ca9d3-181">아래 hello 차트 프로덕션 장치에 대 한 모든 hello 볼륨에 대 한 hello 초기자 tooyour 장치에 대 한 hello I/O를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-181">hello chart below shows hello I/O for hello initiator tooyour device for all hello volumes for a production device.</span></span> <span data-ttu-id="ca9d3-182">hello 메트릭을 그릴 읽고 초당 바이트 수를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-182">hello metrics plotted are read and write bytes per second.</span></span> <span data-ttu-id="ca9d3-183">또한 읽기, 쓰기 및 미해결 IO 또는 읽기 및 쓰기 대기 시간을 차트로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-183">You can also chart read, write, and outstanding IO, or read and write latencies.</span></span>

![초기자 toodevice에 대 한 IO 성능](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a><span data-ttu-id="ca9d3-185">장치 toocloud에 대 한 I/O 성능</span><span class="sxs-lookup"><span data-stu-id="ca9d3-185">I/O performance for device toocloud</span></span>
<span data-ttu-id="ca9d3-186">Hello에 대 한 동일한 장치, 모든 볼륨 컨테이너를 hello에 대 한 hello 장치 toohello 클라우드에서 hello 데이터에 대 한 hello I/O 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-186">For hello same device, hello I/O operations are plotted for hello data from hello device toohello cloud for all hello volume containers.</span></span> <span data-ttu-id="ca9d3-187">이 장치에서 hello 데이터는 hello 선형 계층만 있고 toohello 클라우드 유출 nothing입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-187">On this device, hello data is only in hello linear tier and nothing has spilled toohello cloud.</span></span> <span data-ttu-id="ca9d3-188">장치 toohello 클라우드에서 발생 읽기 / 쓰기 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-188">There are no read-write operations occurring from device toohello cloud.</span></span> <span data-ttu-id="ca9d3-189">따라서 hello 최대치 hello 차트에서 해당 하는 hello 하트 비트 hello 장치와 hello 서비스 간에 확인란이 toohello 빈도 5 분의 간격에 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-189">Therefore, hello peaks in hello chart are at an interval of 5 minutes that corresponds toohello frequency at which hello heartbeat is checked between hello device and hello service.</span></span>

<span data-ttu-id="ca9d3-190">Hello 동일한 장치, 클라우드 스냅숏은 수행 되었으나 오전 11시 50분에서 시작 하는 볼륨 데이터에 대 한에.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-190">For hello same device, a cloud snapshot was taken for volume data starting at 11:50 am.</span></span> <span data-ttu-id="ca9d3-191">이 hello 장치 toohello 클라우드에서 흐르는 데이터에서 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-191">This resulted in data flowing from hello device toohello cloud.</span></span> <span data-ttu-id="ca9d3-192">이 기간 동안 기록 된 toohello 클라우드를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-192">Writes were served toohello cloud in this duration.</span></span> <span data-ttu-id="ca9d3-193">hello IO 차트 hello 쓰기 바이트/s 해당 toohello 시간 hello 스냅숏을 만들 때에 최고를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-193">hello IO chart shows a peak in hello Write Bytes/s corresponding toohello time when hello snapshot was taken.</span></span>

![클라우드 스냅숏 중 장치 toocloud에서 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a><span data-ttu-id="ca9d3-195">장치 네트워크 인터페이스의 네트워크 처리량</span><span class="sxs-lookup"><span data-stu-id="ca9d3-195">Network throughput for device network interfaces</span></span>
<span data-ttu-id="ca9d3-196">**그 결과 네트워크 처리량** hello iSCSI 초기자 네트워크 인터페이스 hello 호스트 서버와 hello 장치 및 hello 장치와 hello 클라우드 간에 전송 되는 데이터 양을 메트릭 관련된 toohello 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-196">**Network throughput** tracks metrics related toohello amount of data transferred from hello iSCSI initiator network interfaces on hello host server and hello device and between hello device and hello cloud.</span></span> <span data-ttu-id="ca9d3-197">장치에서 각 hello iSCSI 네트워크 인터페이스에 대해이 메트릭을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-197">You can monitor this metric for each of hello iSCSI network interfaces on your device.</span></span>

<span data-ttu-id="ca9d3-198">GbE 네트워크 모두 클라우드 사용 (기본값)가 사용자의 장치에 Data 0, 1 1 hello에 대 한 차트 표시 hello 네트워크 처리량 다음 hello 및 iSCSI를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-198">hello following charts show hello network throughput for hello Data 0, 1 1 GbE network on your device, which was both cloud-enabled (default) and iSCSI-enabled.</span></span> <span data-ttu-id="ca9d3-199">약 9 오후 6 월 14에이 장치에 대해 toohello 클라우드를 제공 하는 IO 했으며 hello 클라우드 (에 스냅숏이 만들어진 지점 tootiering 되는 시간 없음 클라우드 hello 클라우드로 메커니즘 toomove hello 데이터 hello)로 데이터 계층이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-199">On this device on June 14 at around 9 pm, data was tiered into hello cloud (no cloud snapshots were taken at that time which points tootiering being hello mechanism toomove hello data into hello cloud) which resulted in IO being served toohello cloud.</span></span> <span data-ttu-id="ca9d3-200">에 없는 경우 해당 최대 hello 네트워크 처리량 그래프에 대 한 hello 시간과 대부분의 hello 네트워크 트래픽이 동일한 아웃 바운드 toohello 클라우드</span><span class="sxs-lookup"><span data-stu-id="ca9d3-200">There is a corresponding peak in hello network throughput graph for hello same time and most of hello network traffic is outbound toohello cloud.</span></span>

![Data 0에 대한 네트워크 처리량](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

<span data-ttu-id="ca9d3-202">Data 1 hello 인터페이스 처리량 차트를 보면 다른 1 GbE 네트워크 인터페이스를만 iSCSI를 사용 후이 기간 동안 네트워크 트래픽이 없음 거의 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-202">If we look at hello Data 1 interface throughput chart, another 1 GbE network interface which was only iSCSI-enabled, then there was virtually no network traffic in this duration.</span></span>

![Data 1에 대한 네트워크 처리량](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a><span data-ttu-id="ca9d3-204">장치의 CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="ca9d3-204">CPU utilization for device</span></span>
<span data-ttu-id="ca9d3-205">**CPU 사용률** toohello CPU 사용률 장치에서을 관련 된 메트릭을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-205">**CPU utilization** tracks metrics related toohello CPU utilized on your device.</span></span> <span data-ttu-id="ca9d3-206">hello 다음 차트에서는 장치에 대 한 CPU 사용률 통계 hello 프로덕션.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-206">hello following chart shows hello CPU utilization stats for a device in production.</span></span>

![장치의 CPU 사용률](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a><span data-ttu-id="ca9d3-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca9d3-208">Next steps</span></span>
* <span data-ttu-id="ca9d3-209">너무 방법에 대해 알아봅니다[hello StorSimple 장치 관리자 서비스 장치 대시보드를 사용 하 여](storsimple-device-dashboard.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-209">Learn how too[use hello StorSimple Device Manager service device dashboard](storsimple-device-dashboard.md).</span></span>
* <span data-ttu-id="ca9d3-210">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca9d3-210">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

