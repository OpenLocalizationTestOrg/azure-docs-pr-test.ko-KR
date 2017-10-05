---
title: "StorSimple Virtual Array 장치 요약 블레이드 | Microsoft Docs"
description: "StorSimple Manager 장치 관리자에 대한 장치 요약 블레이드 및 이 기능을 사용하여 StorSimple 가상 배열의 상태를 모니터링하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="a3822-103">StorSimple 가상 배열에 연결된 StorSimple 장치 관리자에 대한 장치 요약 블레이드 사용</span><span class="sxs-lookup"><span data-stu-id="a3822-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="a3822-104">개요</span><span class="sxs-lookup"><span data-stu-id="a3822-104">Overview</span></span>

<span data-ttu-id="a3822-105">StorSimple 장치 관리자 장치 블레이드에서는 지정된 StorSimple 장치 관리자에 등록된 StorSimple 가상 배열의 요약 보기를 제공하며 시스템 관리자의 주의가 필요한 해당 장치 문제를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="a3822-106">이 자습서에서는 장치 요약 블레이드를 소개하고, 콘텐츠와 기능 및 이 브레이드에서 수행할 수 있는 태스크에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="a3822-107">장치 요약 블레이드는 다음 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-107">The device summary blade displays the following information:</span></span>

![장치 대시보드](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="a3822-109">관리</span><span class="sxs-lookup"><span data-stu-id="a3822-109">Management</span></span>

<span data-ttu-id="a3822-110">StorSimple 장치 블레이드에는 StorSimple 장치를 관리하기 위한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="a3822-111">블레이드 상단과 왼쪽에는 관리 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="a3822-112">이러한 옵션을 사용하여 공유 또는 볼륨을 추가하거나 가상 배열을 업데이트 또는 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="a3822-113">Essentials 영역은 상태, 모델, 소프트웨어 버전뿐만 아니라 배열 **웹 UI**에 대한 링크와 같은 일부 중요한 속성을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="a3822-114">사용자가 내부 네트워크에 있는 경우 [로컬 웹 UI](storsimple-ova-web-ui-admin.md)를 직접 시작하여 가상 배열을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![장치 Essentials](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="a3822-116">StorSimple 장치 요약</span><span class="sxs-lookup"><span data-stu-id="a3822-116">StorSimple device summary</span></span>

* <span data-ttu-id="a3822-117">**경고** 타일에서는 경고 심각도별로 그룹화된 가상 배열에 대한 모든 활성 경고의 스냅숏을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="a3822-118">타일을 클릭하면 **경고** 블레이드가 열리고 개별 경고를 클릭하여 권장 조치를 포함하여 해당 경고에 대한 추가 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="a3822-119">또한 문제가 해결된 경고를 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="a3822-120">**용량** 타일에서는 동일한 경우에 사용 가능한 총 저장소를 기준으로 모든 가상 장치에 프로비전하고 남아있는 기본 저장소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="a3822-121">**프로비전**은 사용하도록 준비되고 할당된 저장소의 양을 나타내며 **나머지**는 이 장치에 프로비전될 수 있는 남은 용량을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="a3822-122">**나머지 계층** 용량은 클라우드를 포함하여 프로비전될 수 있는 사용 가능한 용량인 반면 **나머지 로컬**은 이 가상 배열에 연결된 디스크에 남아 있는 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="a3822-123">**사용** 차트에서 기본 시간 간격인 지난 7일 동안 사용된 클라우드 저장소뿐만 아니라 가상 배열에 사용되는 기본 저장소도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="a3822-124">차트의 오른쪽 위 모서리에서 **편집** 옵션을 사용하여 다른 시간 단위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="a3822-125">**공유** 또는 **볼륨** 타일에서는 상태별로 그룹화된 장치에서 공유 또는 볼륨의 수를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="a3822-126">타일을 클릭하여 **공유** 또는 **볼륨** 목록 블레이드를 연 다음 개별 공유 또는 볼륨을 클릭하여 해당 속성을 확인하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3822-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="a3822-127">자세한 내용은 [공유 관리](storsimple-virtual-array-manage-shares.md) 또는 [볼륨 관리](storsimple-virtual-array-manage-volumes.md) 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3822-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3822-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3822-128">Next steps</span></span>
<span data-ttu-id="a3822-129">방법 배우기:</span><span class="sxs-lookup"><span data-stu-id="a3822-129">Learn how to:</span></span>
- [<span data-ttu-id="a3822-130">StorSimple 가상 배열에서 공유 관리</span><span class="sxs-lookup"><span data-stu-id="a3822-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="a3822-131">StorSimple 가상 배열에서 볼륨 관리</span><span class="sxs-lookup"><span data-stu-id="a3822-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

