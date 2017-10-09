---
title: "aaaView StorSimple 8000 시리즈에 대 한 작업을 관리 하 고 | Microsoft Docs"
description: "Hello StorSimple 장치 관리자 서비스 작업 블레이드 설명 방법과 toouse 것 tootrack 최근, 현재 및 예약 된 백업 작업입니다."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="74691-103">StorSimple 장치 관리자 서비스 tooview hello를 사용 하 고 작업 (업데이트 3 이상)를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="74691-104">개요</span><span class="sxs-lookup"><span data-stu-id="74691-104">Overview</span></span>
<span data-ttu-id="74691-105">hello **작업** 블레이드 보기에 대 한 단일 중앙 포털이 제공 및 tooyour StorSimple 장치 관리자 서비스에 연결 된 장치에서 시작 된 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="74691-106">여러 장치에 대해 예약, 실행 중, 완료, 취소, 실패한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="74691-107">결과는 표 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="74691-107">Results are presented in a tabular format.</span></span>

![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="74691-109">와 같은 필드를 필터링 하 여 관심 있는 hello 작업을 빠르게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="74691-110">**상태** – 작업은 진행 중, 성공, 취소됨, 실패, 취소 중 또는 오류를 나타내며 성공 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="74691-111">**시간 범위** – 작업에 따라 필터링 된 hello 날짜 및 시간 범위를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="74691-112">hello 범위는 지난 1 시간, 지난 30 일, 지난 해 또는 사용자 지정 날짜 지난 7 일, 지난 24 시간.</span><span class="sxs-lookup"><span data-stu-id="74691-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="74691-113">**형식** – 예약 된 백업, 수동 백업, 복원 백업 hello 작업 유형 수 볼륨을 복제 볼륨 컨테이너를 장애 조치할 로컬로 고정 된 볼륨, 볼륨 수정, 업데이트를 설치, 지원 로그 수집을 만들거나 만들 클라우드 어플라이언스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="74691-114">**장치** – 작업은 특정 연결 된 장치 tooyour 서비스에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74691-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="74691-115">hello 필터링 된 작업은 표 형식으로 표시 hello 특성 뒤의 hello 기준:</span><span class="sxs-lookup"><span data-stu-id="74691-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="74691-116">**이름** – 예약된 백업, 수동 백업, 백업 복원, 볼륨 복제, 볼륨 컨테이너 장애 조치, 로컬로 고정된 볼륨 만들기, 볼륨 수정, 업데이트 설치, 지원 로그 수집 또는 클라우드 어플라이언스 만들기</span><span class="sxs-lookup"><span data-stu-id="74691-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="74691-117">**상태** – 실행 중, 완료, 취소, 실패, 취소 중 또는 완료되었으나 오류 발생입니다.</span><span class="sxs-lookup"><span data-stu-id="74691-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="74691-118">**엔터티** – hello 작업은 볼륨, 백업 정책 또는 장치가 연결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="74691-119">예를 들어 복제 작업은 볼륨과 연관되는 반면, 예약된 백업 작업은 백업 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="74691-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="74691-120">장치 작업은 DR(재해 복구) 또는 복원 작업의 결과로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="74691-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="74691-121">**장치** – hello는 hello 작업이 시작 된 hello 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="74691-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="74691-122">**시작** – hello 작업이 시작 된 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="74691-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="74691-123">**기간** – hello 타이머 필요한 toocomplete hello 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="74691-124">hello 작업 목록은 30 초 마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="74691-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="74691-125">이 페이지에서 작업 관련 동작을 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="74691-126">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="74691-126">View job details</span></span>
* <span data-ttu-id="74691-127">작업 취소</span><span class="sxs-lookup"><span data-stu-id="74691-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="74691-128">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="74691-128">View job details</span></span>
<span data-ttu-id="74691-129">다음 작업의 단계 tooview hello 세부 정보는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="74691-130">tooview 작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="74691-130">tooview job details</span></span>
1. <span data-ttu-id="74691-131">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="74691-132">Hello에 **작업** 블레이드, 적절 한 필터가 포함 된 쿼리를 실행 하 여 관심 있는 hello 개의 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74691-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="74691-133">완료되거나, 실행 중이거나, 취소된 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-133">You can search for completed, running, or canceled jobs.</span></span>

    ![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="74691-135">작업을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-135">Select and click a job.</span></span>

    ![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="74691-137">Hello 작업 세부 정보 블레이드에서 hello 상태, 세부 정보, 시간 통계 및 데이터 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![작업 세부 정보](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="74691-139">작업 취소</span><span class="sxs-lookup"><span data-stu-id="74691-139">Cancel a job</span></span>
<span data-ttu-id="74691-140">Hello 다음 단계 toocancel 실행 중인 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="74691-141">볼륨 toochange hello 볼륨 형식을 수정 하거나, 볼륨 확장 같은 일부 작업을 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74691-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="74691-142">toocancel 작업</span><span class="sxs-lookup"><span data-stu-id="74691-142">toocancel a job</span></span>
1. <span data-ttu-id="74691-143">Hello에 **작업** 페이지에서 적절 한 필터가 포함 된 쿼리를 실행 하 여 toocancel 되도록 hello 실행 중인 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="74691-144">Hello 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-144">Select hello job.</span></span>

2. <span data-ttu-id="74691-145">Hello 선택한 작업 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 클릭 **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![작업 세부 정보](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="74691-147">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="74691-148">이 작업은 이제 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="74691-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74691-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74691-149">Next steps</span></span>
* <span data-ttu-id="74691-150">너무 방법에 대해 알아봅니다[StorSimple 백업 정책 관리](storsimple-8000-manage-backup-policies-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="74691-151">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74691-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

