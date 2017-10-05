---
title: "StorSimple Snapshot Manager 백업 작업 | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 MMC 스냅인을 사용하여 예약된 백업 작업, 현재 실행 중인 백업 작업 및 완료된 백업 작업을 보고 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="8eb71-103">StorSimple 스냅숏 관리자를 사용하여 백업 작업 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="8eb71-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="8eb71-104">개요</span><span class="sxs-lookup"><span data-stu-id="8eb71-104">Overview</span></span>
<span data-ttu-id="8eb71-105">**범위** 창의 **작업** 노드에는 대화형으로 또는 구성된 정책에 따라 시작한 **예약됨**, **최근 24시간** 및 **실행 중** 백업 태스크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="8eb71-106">이 자습서에서는 **작업** 노드를 사용하여 예약된 백업 작업, 최근 백업 작업 및 현재 실행 중인 백업 작업에 대한 정보를 표시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="8eb71-107">(작업 및 해당 정보 목록이 **결과** 창에 나타납니다.) 또한 나열된 작업을 마우스 오른쪽 단추로 클릭하면 사용 가능한 작업이 나열된 상황에 맞는 메뉴를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="8eb71-108">예약된 작업 보기</span><span class="sxs-lookup"><span data-stu-id="8eb71-108">View scheduled jobs</span></span>
<span data-ttu-id="8eb71-109">다음 절차를 사용하여 예약된 백업 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="8eb71-110">예약된 작업을 보려면</span><span class="sxs-lookup"><span data-stu-id="8eb71-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="8eb71-111">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="8eb71-112">**범위** 창에서 **작업** 노드를 확장한 다음 **예약됨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="8eb71-113">**결과** 창에 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="8eb71-114">**이름** – 예약된 스냅숏의 이름</span><span class="sxs-lookup"><span data-stu-id="8eb71-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="8eb71-115">**다음 실행** – 다음으로 예약된 스냅숏의 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="8eb71-116">**마지막 실행** – 가장 최근으로 예약된 스냅숏의 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="8eb71-117">일회성 스냅숏은 **다음 실행** 및 **마지막 실행**이 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![예약된 백업 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="8eb71-119">특정 작업에 대해 추가 작업을 수행하려면 **결과** 창에서 해당 작업 이름을 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="8eb71-120">최근 작업 보기</span><span class="sxs-lookup"><span data-stu-id="8eb71-120">View recent jobs</span></span>
<span data-ttu-id="8eb71-121">다음 절차를 사용하여 최근 24시간 동안 완료된 백업 및 복원 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="8eb71-122">최근 작업을 보려면</span><span class="sxs-lookup"><span data-stu-id="8eb71-122">To view recent jobs</span></span>
1. <span data-ttu-id="8eb71-123">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="8eb71-124">**범위** 창에서 **작업** 노드를 확장한 다음 **최근 24시간**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="8eb71-125">**결과** 창에 최근 24시간 동안의 백업 작업이 표시됩니다(최대 64개 작업까지).</span><span class="sxs-lookup"><span data-stu-id="8eb71-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="8eb71-126">지정한 **보기** 옵션에 따라 **결과** 창에 다음 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="8eb71-127">**이름** – 예약된 스냅숏의 이름</span><span class="sxs-lookup"><span data-stu-id="8eb71-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="8eb71-128">**시작** – 스냅숏이 시작된 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="8eb71-129">**중지** – 스냅숏이 완료되거나 종료된 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="8eb71-130">**경과** – **시작** 및 **중지** 시간 사이의 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="8eb71-131">**상태** - 최근에 완료된 작업의 상태</span><span class="sxs-lookup"><span data-stu-id="8eb71-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="8eb71-132">**성공**은 백업이 성공적으로 만들어졌음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="8eb71-133">**실패**는 작업이 성공적으로 실행되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="8eb71-134">**정보** – 실패한 이유</span><span class="sxs-lookup"><span data-stu-id="8eb71-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="8eb71-135">**처리된 바이트(MB)** – 처리된 볼륨 그룹의 데이터 양(MB)</span><span class="sxs-lookup"><span data-stu-id="8eb71-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![최근 24시간 동안 실행된 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="8eb71-137">특정 작업에 대해 추가 작업을 수행하려면 **결과** 창에서 해당 작업 이름을 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![작업 삭제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="8eb71-139">현재 실행 중인 작업 보기</span><span class="sxs-lookup"><span data-stu-id="8eb71-139">View currently running jobs</span></span>
<span data-ttu-id="8eb71-140">다음 절차를 사용하여 현재 실행 중인 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="8eb71-141">현재 실행 중인 작업을 보려면</span><span class="sxs-lookup"><span data-stu-id="8eb71-141">To view currently running jobs</span></span>
1. <span data-ttu-id="8eb71-142">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="8eb71-143">**범위** 창에서 **작업** 노드를 확장한 다음 **실행 중**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="8eb71-144">지정한 **보기** 옵션에 따라 **결과** 창에 다음 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="8eb71-145">**이름** – 예약된 스냅숏의 이름</span><span class="sxs-lookup"><span data-stu-id="8eb71-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="8eb71-146">**시작** – 스냅숏이 시작된 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="8eb71-147">**검사점** - 백업의 현재 작업</span><span class="sxs-lookup"><span data-stu-id="8eb71-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="8eb71-148">**상태** – 완료율</span><span class="sxs-lookup"><span data-stu-id="8eb71-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="8eb71-149">**경과** - 백업이 시작된 이후 경과된 시간</span><span class="sxs-lookup"><span data-stu-id="8eb71-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="8eb71-150">**평균 처리량(MB)** – 처리하는 데 걸린 총 시간에 대해 처리된 데이터 총 바이트의 비율(MB)</span><span class="sxs-lookup"><span data-stu-id="8eb71-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="8eb71-151">**처리된 바이트(MB)** - 처리된 데이터의 총 바이트(MB)</span><span class="sxs-lookup"><span data-stu-id="8eb71-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="8eb71-152">**작성된 바이트(MB)** - 작성된 데이터의 총 바이트(MB)</span><span class="sxs-lookup"><span data-stu-id="8eb71-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="8eb71-153">메타데이터 뿐만 아니라 데이터를 포함하고 따라서 일반적으로 처리된 바이트보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![현재 실행 중인 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="8eb71-155">특정 작업에 대해 추가 작업을 수행하려면 **결과** 창에서 해당 작업 이름을 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8eb71-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8eb71-156">Next steps</span></span>
* <span data-ttu-id="8eb71-157">[StorSimple 스냅숏 관리자를 사용하여 StorSimple 솔루션을 관리](storsimple-snapshot-manager-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="8eb71-158">[StorSimple 스냅숏 관리자를 사용하여 백업 카탈로그를 관리](storsimple-snapshot-manager-manage-backup-catalog.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8eb71-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

