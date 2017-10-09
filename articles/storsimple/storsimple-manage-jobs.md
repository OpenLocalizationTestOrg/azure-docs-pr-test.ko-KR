---
title: "aaaView StorSimple 작업을 관리 하 고 | Microsoft Docs"
description: "Hello StorSimple 관리자 서비스 작업 페이지에 설명 하 고 어떻게 toouse 것 tootrack 최근, 현재 및 예약 된 백업 작업입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a><span data-ttu-id="77c94-103">StorSimple Manager 서비스 tooview hello를 사용 하 고 StorSimple 작업 관리</span><span class="sxs-lookup"><span data-stu-id="77c94-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="77c94-104">개요</span><span class="sxs-lookup"><span data-stu-id="77c94-104">Overview</span></span>
<span data-ttu-id="77c94-105">hello **작업** 페이지 보기에 대 한 단일 중앙 포털이 제공 및 tooyour StorSimple Manager 서비스에 연결 된 장치에서 시작 된 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="77c94-106">여러 장치에 대한 예약, 실행, 완료 및 실패한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="77c94-107">결과는 표 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-107">Results are presented in a tabular format.</span></span> 

![작업 페이지](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="77c94-109">와 같은 필드를 필터링 하 여 관심 있는 hello 작업을 빠르게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="77c94-110">**상태** – 작업 상태는 실행 중, 예약, 실패, 완료, 취소 중 또는 취소입니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="77c94-111">**유형** – 작업은 예약 또는 요청 시 백업(**백업 수행**), 복제, 장치 복원, 업데이트 작업의 결과로 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="77c94-112">**장치** – 작업은 특정 연결 된 장치 tooyour 서비스에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-112">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
* <span data-ttu-id="77c94-113">**From 및 To** – 작업에 따라 필터링 된 hello 날짜 및 시간 범위를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-113">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>

<span data-ttu-id="77c94-114">hello 필터링 된 작업은 표 형식으로 표시 hello 특성 뒤의 hello 기준:</span><span class="sxs-lookup"><span data-stu-id="77c94-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>

* <span data-ttu-id="77c94-115">**유형** – 백업, 복제, 복원, 장애 조치(failover) 또는 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="77c94-116">**상태** – 실행 중, 예약, 실패, 완료, 취소 중 또는 취소입니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="77c94-117">**엔터티** – hello 작업은 볼륨, 백업 정책 또는 장치가 연결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="77c94-118">복제 작업은 볼륨과 연관되는 반면, 예약된 백업 작업은 백업 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="77c94-119">장치 작업은 DR(재해 복구) 또는 복원 작업의 결과로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="77c94-120">**장치** – hello는 hello 작업이 시작 된 hello 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-120">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="77c94-121">**시작에** – hello 작업이 시작 된 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-121">**Started On** – hello time when hello job was started.</span></span>
* <span data-ttu-id="77c94-122">**진행률** – hello 실행 중인 작업의 완료 백분율입니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="77c94-123">완료된 작업의 경우 항상 100%여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="77c94-124">hello 작업 목록은 30 초 마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="77c94-125">이 페이지에서 작업 관련 동작을 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="77c94-126">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="77c94-126">View job details</span></span>
* <span data-ttu-id="77c94-127">작업 취소</span><span class="sxs-lookup"><span data-stu-id="77c94-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="77c94-128">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="77c94-128">View job details</span></span>
<span data-ttu-id="77c94-129">다음 작업의 단계 tooview hello 세부 정보는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="77c94-130">tooview 작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="77c94-130">tooview job details</span></span>
1. <span data-ttu-id="77c94-131">Hello에 **작업** 페이지에서 적절 한 필터가 포함 된 쿼리를 실행 하 여 관심 있는 hello 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="77c94-132">완료되거나, 실행 중이거나, 취소된 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="77c94-133">작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-133">Select a job.</span></span>
3. <span data-ttu-id="77c94-134">Hello hello 페이지의 아래쪽에 있는 클릭 **세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="77c94-135">Hello에 **백업 작업 세부 정보** 대화 상자, hello 상태, 세부 정보, 시간 통계 및 데이터 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="77c94-136">작업 취소</span><span class="sxs-lookup"><span data-stu-id="77c94-136">Cancel a job</span></span>
<span data-ttu-id="77c94-137">Hello 다음 단계 toocancel 실행 중인 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-137">Perform hello following steps toocancel a running job.</span></span>

### <a name="toocancel-a-job"></a><span data-ttu-id="77c94-138">toocancel 작업</span><span class="sxs-lookup"><span data-stu-id="77c94-138">toocancel a job</span></span>
1. <span data-ttu-id="77c94-139">Hello에 **작업** 페이지에서 적절 한 필터가 포함 된 쿼리를 실행 하 여 toocancel 되도록 hello 실행 중인 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-139">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="77c94-140">Hello 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-140">Select hello job.</span></span>
3. <span data-ttu-id="77c94-141">Hello hello 페이지의 아래쪽에 있는 클릭 **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-141">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="77c94-142">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="77c94-143">이 작업은 이제 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77c94-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77c94-144">Next steps</span></span>
* <span data-ttu-id="77c94-145">너무 방법에 대해 알아봅니다[StorSimple 백업 정책 관리](storsimple-manage-backup-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-145">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="77c94-146">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c94-146">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

