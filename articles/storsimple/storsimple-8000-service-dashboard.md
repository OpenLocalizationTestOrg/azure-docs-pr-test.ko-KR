---
title: "StorSimple 8000 시리즈 장치 요약 사용 | Microsoft Docs"
description: "StorSimple 서비스 요약 블레이드 및 이 블레이드를 사용하여 StorSimple 솔루션의 상태를 모니터링하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="9bd3b-103">StorSimple 8000 시리즈 장치에 대한 서비스 요약 블레이드 사용</span><span class="sxs-lookup"><span data-stu-id="9bd3b-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="9bd3b-104">개요</span><span class="sxs-lookup"><span data-stu-id="9bd3b-104">Overview</span></span>

<span data-ttu-id="9bd3b-105">StorSimple 장치 관리자 서비스 요약 블레이드는 StorSimple 장치 관리자 서비스에 연결된 모든 장치에 대한 요약 보기를 통해 시스템 관리자의 주의가 필요한 정보를 중점적으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="9bd3b-106">이 자습서에서는 서비스 요약 블레이드를 소개하고, 대시보드 콘텐츠와 기능 및 이 페이지에서 수행할 수 있는 태스크에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![서비스 요약](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="9bd3b-108">관리 명령</span><span class="sxs-lookup"><span data-stu-id="9bd3b-108">Management commands</span></span>

<span data-ttu-id="9bd3b-109">StorSimple 서비스 요약 블레이드에는 StorSimple 장치 관리자 서비스 및 이 서비스에 등록된 StorSimple 8000 시리즈 장치를 관리하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="9bd3b-110">블레이드 상단과 왼쪽에는 관리 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-110">You see the management commands across the top of the blade and on the left side.</span></span>

![명령 모음](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="9bd3b-112">이 옵션을 사용하여 공유 또는 볼륨을 추가하거나 StorSimple 장치에서 실행 중인 다양한 작업을 모니터링하는 것과 같은 다양한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="9bd3b-113">Essentials</span><span class="sxs-lookup"><span data-stu-id="9bd3b-113">Essentials</span></span>

<span data-ttu-id="9bd3b-114">Essentials 영역은 StorSimple Device Manager를 만든 리소스 그룹, 위치 및 구독과 같은 중요한 속성 중 일부를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Essentials](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="9bd3b-116">StorSimple Device Manager 서비스 요약</span><span class="sxs-lookup"><span data-stu-id="9bd3b-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="9bd3b-117">**경고** 타일에서는 경고 심각도별로 그룹화된 모든 장치 간의 모든 활성 경고에 대한 스냅숏을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![경고 타일](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="9bd3b-119">타일을 클릭하면 **경고** 블레이드가 열리고 여기에서 개별 경고를 클릭하여 권장 조치를 포함하여 해당 경고에 대한 추가적인 정보를 자세히 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="9bd3b-120">또한 문제가 해결된 경고를 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![경고 타일 클릭](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="9bd3b-122">**용량** 타일에서는 모든 장치에서 사용 가능한 총 저장소를 기준으로 모든 장치에 프로비전하고 남아있는 기본 저장소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="9bd3b-123">**프로비전**은 사용하도록 준비되고 할당된 저장소의 양을 나타내며 **나머지**는 모든 장치에 프로비전될 수 있는 남은 용량을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![용량 타일](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="9bd3b-125">**나머지 계층** 용량은 클라우드를 포함하여 프로비전될 수 있는 사용 가능한 용량인 반면 **나머지 로컬**은 StorSimple 8000 시리즈 장치에 연결된 디스크에 남아 있는 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="9bd3b-126">**사용량** 차트에서 장치에 대한 관련 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="9bd3b-127">기본 시간 간격인 지난 7일 동안 장치에서 사용된 클라우드 저장소는 물론, 모든 장치에 걸쳐 사용되는 기본 저장소도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![사용량 타일](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="9bd3b-129">다른 시간 단위를 선택하려면 차트의 오른쪽 위 모서리에서 **편집** 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![사용량 타일 클릭](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![차트 데이터 내보내기](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="9bd3b-132">**장치** 타일에서는 장치 상태별로 그룹화된 StorSimple 장치 관리자에서 StorSimple 8000 시리즈 장치 수의 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![장치 타일](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="9bd3b-134">이 타일을 클릭하여 **장치** 목록 블레이드를 연 다음 개별 장치를 클릭하여 장치에 특정된 장치 요약을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="9bd3b-135">또한 지정된 장치 요약 블레이드에서 장치 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="9bd3b-136">장치 요약 블레이드에 대한 자세한 내용은 [장치 요약 블레이드](storsimple-8000-device-dashboard.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![장치 타일 클릭](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="9bd3b-138">작업 로그 보기</span><span class="sxs-lookup"><span data-stu-id="9bd3b-138">View the activity logs</span></span>

<span data-ttu-id="9bd3b-139">StorSimple Device Manager 내에서 수행된 다양한 작업을 보려면 StorSimple 서비스 요약 블레이드의 왼쪽에 있는 **작업 로그** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="9bd3b-140">그러면 **작업 로그** 블레이드로 이동하여 최근에 수행한 작업의 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![활동 로그](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="9bd3b-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9bd3b-142">Next steps</span></span>

* <span data-ttu-id="9bd3b-143">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9bd3b-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

