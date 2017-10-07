---
title: "aaaStorSimple 스냅숏 관리자에 대 한 백업 작업 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooview hello 하 및 예약 된 시간, 현재 실행 중인 및 완료 된 백업 작업을 관리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="90cfe-103">StorSimple 스냅숏 관리자 tooview를 사용 하 고 백업 작업 관리</span><span class="sxs-lookup"><span data-stu-id="90cfe-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="90cfe-104">개요</span><span class="sxs-lookup"><span data-stu-id="90cfe-104">Overview</span></span>
<span data-ttu-id="90cfe-105">hello **작업** hello에 대 한 노드 **범위** 창 표시 hello **예약 된**, **마지막 24 시간**, 및 **실행**대화형으로 또는 구성된 정책에 따라 시작 작업을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="90cfe-106">이 자습서에서는 hello를 사용 하는 방법에 대해 설명 **작업** 예약, 최근, 및 현재 실행 중인 백업 작업에 대 한 노드 toodisplay 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="90cfe-107">(hello에 작업 및 해당 정보가 hello 목록이 표시 됩니다 **결과** 창입니다.) 또한 나열된 작업을 마우스 오른쪽 단추로 클릭하면 사용 가능한 작업이 나열된 상황에 맞는 메뉴를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="90cfe-108">예약된 작업 보기</span><span class="sxs-lookup"><span data-stu-id="90cfe-108">View scheduled jobs</span></span>
<span data-ttu-id="90cfe-109">예약 된 백업 작업을 사용 하 여 hello tooview 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="90cfe-110">tooview 예약 된 작업</span><span class="sxs-lookup"><span data-stu-id="90cfe-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="90cfe-111">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="90cfe-112">Hello에 **범위** 창 hello 확장 **작업** 노드를 마우스 클릭 **예약 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="90cfe-113">hello에 다음 정보가 나타납니다 hello **결과** 창:</span><span class="sxs-lookup"><span data-stu-id="90cfe-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="90cfe-114">**이름** – hello hello 예약 된 스냅숏 이름</span><span class="sxs-lookup"><span data-stu-id="90cfe-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="90cfe-115">**그런 다음 실행** – hello의 날짜 및 시간 hello 예약 된 다음 스냅숏</span><span class="sxs-lookup"><span data-stu-id="90cfe-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="90cfe-116">**마지막으로 실행** – hello의 날짜 및 시간 hello 가장 최근 예약 된 스냅숏</span><span class="sxs-lookup"><span data-stu-id="90cfe-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="90cfe-117">한 번만 스냅숏에 대 한 hello **다음 실행** 및 **마지막 실행** 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![예약된 백업 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="90cfe-119">특정 작업에 대해 추가 작업 tooperform hello에 hello 작업 이름을 마우스 오른쪽 단추로 클릭 **결과** 창과 hello 메뉴 옵션 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="90cfe-120">최근 작업 보기</span><span class="sxs-lookup"><span data-stu-id="90cfe-120">View recent jobs</span></span>
<span data-ttu-id="90cfe-121">다음 프로시저 tooview 백업 hello를 사용 하 고 지난 24 시간 동안 hello에서 완료 된 작업을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="90cfe-122">tooview 최근 작업</span><span class="sxs-lookup"><span data-stu-id="90cfe-122">tooview recent jobs</span></span>
1. <span data-ttu-id="90cfe-123">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="90cfe-124">Hello에 **범위** 창 hello 확장 **작업** 노드를 마우스 클릭 **마지막 24 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="90cfe-125">hello **결과** 창 지난 24 시간 동안 (tooa입니다 최대 64 개 작업) hello에 대 한 백업 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="90cfe-126">hello에 다음 정보가 나타납니다 hello **결과** hello에 따라 창 **보기** 지정할 옵션:</span><span class="sxs-lookup"><span data-stu-id="90cfe-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="90cfe-127">**이름** – hello hello 예약 된 스냅숏 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="90cfe-128">**시작** – hello 날짜 및 hello 스냅숏 시작 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="90cfe-129">**중지** hello 날짜 및 시간 hello 스냅숏이 완료 되거나 종료 때 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="90cfe-130">**경과 된** – hello hello 사이의 시간 크기 **시작 됨** 및 **Stopped** 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="90cfe-131">**상태** – hello hello 최근에 완료 된 작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="90cfe-132">**성공** hello 백업이 성공적으로 만들어졌는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="90cfe-133">**실패** 해당 hello 작업이 성공적으로 실행 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="90cfe-134">**정보** – hello hello 실패에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="90cfe-135">**바이트 (MB)를 처리** – hello (단위: Mb)에서 처리 된 hello 볼륨 그룹의 데이터 양입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Hello 지난 24 시간 동안 실행 된 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="90cfe-137">특정 작업에 대해 추가 작업 tooperform hello에 hello 작업 이름을 마우스 오른쪽 단추로 클릭 **결과** 창과 hello 메뉴 옵션 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![작업 삭제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="90cfe-139">현재 실행 중인 작업 보기</span><span class="sxs-lookup"><span data-stu-id="90cfe-139">View currently running jobs</span></span>
<span data-ttu-id="90cfe-140">현재 실행 중인 프로시저 tooview 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="90cfe-141">현재 실행 중인 작업 tooview</span><span class="sxs-lookup"><span data-stu-id="90cfe-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="90cfe-142">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="90cfe-143">Hello에 **범위** 창 hello 확장 **작업** 노드를 마우스 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="90cfe-144">Hello에 따라 **보기** hello에 다음 정보는 hello 표시를 지정 하는 옵션 **결과** 창:</span><span class="sxs-lookup"><span data-stu-id="90cfe-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="90cfe-145">**이름** – hello hello 예약 된 스냅숏 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="90cfe-146">**시작** – hello 날짜 및 hello 스냅숏 시작 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="90cfe-147">**검사점** – hello hello 백업의 현재 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="90cfe-148">**상태** – hello 완료 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="90cfe-149">**경과 된** – hello 양을 hello 백업이 시작 된 이후에 경과 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="90cfe-150">**평균 처리량 (MB)** – (Mb)를 처리 하는 데 걸린 총 시간을 처리 하는 데이터 toothat의 총 바이트 수의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="90cfe-151">**처리된 바이트(MB)** - 처리된 데이터의 총 바이트(MB)</span><span class="sxs-lookup"><span data-stu-id="90cfe-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="90cfe-152">**작성된 바이트(MB)** - 작성된 데이터의 총 바이트(MB)</span><span class="sxs-lookup"><span data-stu-id="90cfe-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="90cfe-153">따라서 일반적으로 보다 크면 바이트 처리 hello 및 hello 메타 데이터 뿐만 아니라 hello 데이터 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![현재 실행 중인 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="90cfe-155">특정 작업에 대해 추가 작업 tooperform hello에 hello 작업 이름을 마우스 오른쪽 단추로 클릭 **결과** 창과 hello 메뉴 옵션 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90cfe-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90cfe-156">Next steps</span></span>
* <span data-ttu-id="90cfe-157">너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="90cfe-158">너무 방법에 대해 알아봅니다[StorSimple 스냅숏 관리자 toomanage hello 백업 카탈로그를 사용 하 여](storsimple-snapshot-manager-manage-backup-catalog.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90cfe-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

