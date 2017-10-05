---
title: "StorSimple 8000 시리즈 장치 요약 사용 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 장치 요약과 이를 사용하여 저장소 메트릭 및 연결된 초기자를 보고 일련 번호 및 IQN을 찾는 방법을 설명합니다."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 784d3ce9d8f926b00ac1c6fbf48a05c0b04f900a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="5cce3-103">StorSimple 장치 관리자 서비스에서 장치 요약 사용</span><span class="sxs-lookup"><span data-stu-id="5cce3-103">Use the device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="5cce3-104">개요</span><span class="sxs-lookup"><span data-stu-id="5cce3-104">Overview</span></span>
<span data-ttu-id="5cce3-105">StorSimple 장치 요약 블레이드는 Microsoft Azure StorSimple 솔루션에 포함된 모든 장치에 대한 정보를 제공하는 서비스 요약 블레이드와 달리, 특정 StorSimple 장치에 대한 정보 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-105">The StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast to the service summary blade, which gives you information about all the devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="5cce3-106">장치 요약 블레이드에서는 지정된 StorSimple 장치 관리자에 등록된 StorSimple 8000 시리즈 장치에 대한 요약 보기를 제공하며 시스템 관리자의 주의가 필요한 장치 문제를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-106">The device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="5cce3-107">이 자습서에서는 장치 요약 블레이드를 소개하고, 콘텐츠와 기능 및 이 브레이드에서 수행할 수 있는 태스크에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-107">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="5cce3-108">장치 요약 블레이드는 다음 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-108">The device summary blade displays the following information:</span></span>

![장치 요약 블레이드](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="5cce3-110">관리 명령 모음</span><span class="sxs-lookup"><span data-stu-id="5cce3-110">Management command bar</span></span>

<span data-ttu-id="5cce3-111">StorSimple 장치 블레이드에는 StorSimple 장치를 관리하기 위한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-111">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="5cce3-112">블레이드 상단과 왼쪽에는 관리 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-112">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="5cce3-113">이러한 옵션을 사용하여 공유 또는 볼륨을 추가하거나 장치를 업데이트 또는 장애 조치(failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-113">Use these options to add shares or volumes, or update or fail over your device.</span></span>

![관리 명령 모음](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="5cce3-115">Essentials</span><span class="sxs-lookup"><span data-stu-id="5cce3-115">Essentials</span></span>

<span data-ttu-id="5cce3-116">Essentials 영역은 상태, 모델, 대상 IQN 및 소프트웨어 버전과 같은 일부 중요한 속성을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-116">The essentials area captures some of the important properties such as, the status, model, target IQN, and the software version.</span></span> 

![장치 Essentials](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="5cce3-118">모니터링</span><span class="sxs-lookup"><span data-stu-id="5cce3-118">Monitoring</span></span>

* <span data-ttu-id="5cce3-119">**경고** 타일에서는 경고 심각도별로 그룹화된 장치에 대한 모든 활성 경고의 스냅숏을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-119">The **Alerts** tile provides a snapshot of all the active alerts for your device, grouped by alert severity.</span></span>

    ![경고 타일](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="5cce3-121">타일을 클릭하면 **경고** 블레이드가 열리고 개별 경고를 클릭하여 권장 조치를 포함하여 해당 경고에 대한 추가 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-121">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="5cce3-122">또한 문제가 해결된 경고를 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-122">You can also clear the alert if the issue has been resolved.</span></span>

    ![경고 타일 클릭](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="5cce3-124">**상태** 타일에서는 장치 상태를 비롯하여 장치의 하드웨어 구성 요소 상태에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-124">The **Status and health** tile provides insights into the hardware component health for a device including the device status.</span></span> <span data-ttu-id="5cce3-125">장치 상태는 오프라인, 온라인, 비활성화 또는 설정 준비 완료 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-125">The device status may be offline, online, deactivated, or ready to set up.</span></span>

    ![상태 타일](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="5cce3-127">**볼륨** 타일에서는 상태별로 그룹화된, 장치의 볼륨 수에 대한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-127">The **Volumes** tile provides a summary of the number of volumes in your device grouped by status.</span></span>

    ![볼륨 타일](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="5cce3-129">타일을 클릭하여 **볼륨** 목록 블레이드를 연 다음 개별 볼륨을 클릭하여 해당 속성을 보거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-129">Click the tile to open the **Volumes** list blade, and then click on an individual volume to view or modify its properties.</span></span>
    
    ![볼륨 타일 클릭](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="5cce3-131">자세한 내용은 [볼륨 관리](storsimple-8000-manage-volumes-u2.md) 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cce3-131">For more information, see how to [manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="5cce3-132">**사용 현황** 차트에서는 기본 기간인 지난 7일 동안 사용된 클라우드 저장소와 장치에서 사용된 기본 저장소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-132">In the **Usage** chart, you can view the primary storage used across your device, and the cloud storage consumed over the past 7 days, the default time period.</span></span>

     ![사용량 타일](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="5cce3-134">다른 시간 단위를 선택하려면 차트의 오른쪽 위 모서리에서 **편집** 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5cce3-134">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![사용 현황 차트 편집](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="5cce3-136">이 차트에서 총 기본 저장소(장치에 대한 호스트가 기록한 데이터의 양)와 일정 기간 동안 장치가 사용한 총 클라우드 저장소에 대한 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-136">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="5cce3-137">이 컨텍스트에서 *기본 저장소*는 호스트가 기록한 데이터의 총 크기를 나타내며 볼륨 유형별로 세분화될 수 있습니다. *계층화된 기본 저장소*는 로컬에 저장된 데이터 및 클라우드에 계층화된 데이터를 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-137">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud.</span></span> <span data-ttu-id="5cce3-138">*로컬로 고정된 기본 저장소*는 로컬로 저장된 데이터만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="5cce3-139">반면에 *클라우드 저장소*는 클라우드에 계층화된 총 데이터를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-139">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="5cce3-140">이 저장소에는 계층화된 데이터 및 백업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="5cce3-141">클라우드에 저장된 데이터는 중복 제거되고 압축되는 반면 기본 저장소는 데이터가 중복 제거되고 압축되기 전에 사용된 저장소의 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-141">The data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="5cce3-142">(압축 비율을 파악하도록 이러한 두 값을 비교할 수 있습니다.) 기본 및 클라우드 저장소의 경우 표시되는 양은 사용자가 구성하는 추적 빈도에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-142">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown are based on the tracking frequency you configure.</span></span> <span data-ttu-id="5cce3-143">예를 들어, 1주일 빈도를 선택하면 이전 주의 각 날짜에 대한 데이터가 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-143">For example, if you choose a one week frequency, then the chart shows data for each day in the previous week.</span></span>

     <span data-ttu-id="5cce3-144">시간이 지남에 따라 사용되는 클라우드 저장소의 크기를 보려면 **CLOUD STORAGE USED(사용된 클라우드 저장소)** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-144">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="5cce3-145">호스트가 작성한 총 저장소를 보려면 **계층화되고 사용된 기본 저장소** 및 **로컬로 고정된 사용된 기본 저장소** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-145">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="5cce3-146">자세한 내용은 [StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 모니터링](storsimple-monitor-device.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cce3-146">For more information, see [Use the StorSimple Device Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="5cce3-147">**용량** 타일에서는 동일한 경우에 사용 가능한 총 저장소를 기준으로 장치에 프로비전하고 남아있는 기본 저장소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-147">The **Capacity** tile displays the primary storage that is provisioned and remaining across the device relative to the total storage available for the same.</span></span> <span data-ttu-id="5cce3-148">**프로비전**은 사용하도록 준비되고 할당된 저장소의 양을 나타내며 **나머지**는 이 장치에 프로비전될 수 있는 남은 용량을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-148">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> 

    ![사용량 타일](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="5cce3-150">계층화된 볼륨 및 로컬로 고정된 볼륨에서 용량이 프로비전된 방식을 보려면 이 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-150">Click this tile to view how the capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="5cce3-151">**나머지 계층** 용량은 클라우드를 포함하여 프로비전될 수 있는 사용 가능한 용량인 반면 **나머지 로컬**은 이 장치에 연결된 디스크에 남아 있는 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-151">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this device.</span></span>

    ![사용 현황 차트 클릭](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="5cce3-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cce3-153">Next steps</span></span>
* <span data-ttu-id="5cce3-154">[StorSimple 서비스 요약 블레이드](storsimple-8000-service-dashboard.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-154">Learn more about the [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="5cce3-155">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5cce3-155">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

