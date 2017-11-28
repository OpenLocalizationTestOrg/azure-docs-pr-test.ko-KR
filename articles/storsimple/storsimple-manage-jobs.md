---
title: "StorSimple 작업 보기 및 관리 | Microsoft Docs"
description: "StorSimple Manager 서비스 작업 페이지에 대해 설명하고 이 페이지를 사용하여 최근, 현재 및 예약된 백업 작업을 추적하는 방법을 설명합니다."
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
ms.openlocfilehash: 7d9377bb8f3cb8c587823c2d71d61dfb9b50f52f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a><span data-ttu-id="1de3d-103">StorSimple 관리자 서비스를 사용하여 StorSimple 작업 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="1de3d-103">Use the StorSimple Manager service to view and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="1de3d-104">개요</span><span class="sxs-lookup"><span data-stu-id="1de3d-104">Overview</span></span>
<span data-ttu-id="1de3d-105">**작업** 페이지에서는 StorSimple 관리자 서비스에 연결된 장치에서 시작한 작업을 보고 관리하기 위한 하나 중앙 포털을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="1de3d-106">여러 장치에 대한 예약, 실행, 완료 및 실패한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="1de3d-107">결과는 표 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-107">Results are presented in a tabular format.</span></span> 

![작업 페이지](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="1de3d-109">다음과 같이 필드에서 필터링하여 관심 있는 작업을 빠르게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="1de3d-110">**상태** – 작업 상태는 실행 중, 예약, 실패, 완료, 취소 중 또는 취소입니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="1de3d-111">**유형** – 작업은 예약 또는 요청 시 백업(**백업 수행**), 복제, 장치 복원, 업데이트 작업의 결과로 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="1de3d-112">**장치** – 작업은 서비스에 연결된 특정 장치에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-112">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
* <span data-ttu-id="1de3d-113">**시작 및 종료** – 작업은 날짜 및 시간 범위에 따라 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-113">**From and To** – Jobs can be filtered based on the date and time range.</span></span>

<span data-ttu-id="1de3d-114">필터링된 작업은 다음과 같은 특성을 기반으로 표로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>

* <span data-ttu-id="1de3d-115">**유형** – 백업, 복제, 복원, 장애 조치(failover) 또는 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="1de3d-116">**상태** – 실행 중, 예약, 실패, 완료, 취소 중 또는 취소입니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="1de3d-117">**엔터티** – 작업은 볼륨, 백업 정책 또는 장치에 연관될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="1de3d-118">복제 작업은 볼륨과 연관되는 반면, 예약된 백업 작업은 백업 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="1de3d-119">장치 작업은 DR(재해 복구) 또는 복원 작업의 결과로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="1de3d-120">**장치** – 작업이 시작된 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-120">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="1de3d-121">**시작 시간** – 작업이 시작된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-121">**Started On** – The time when the job was started.</span></span>
* <span data-ttu-id="1de3d-122">**진행률** – 실행 중인 작업의 완료율입니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="1de3d-123">완료된 작업의 경우 항상 100%여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="1de3d-124">작업 목록은 30초마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="1de3d-125">이 페이지에서 다음 작업과 관련된 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="1de3d-126">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="1de3d-126">View job details</span></span>
* <span data-ttu-id="1de3d-127">작업 취소</span><span class="sxs-lookup"><span data-stu-id="1de3d-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="1de3d-128">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="1de3d-128">View job details</span></span>
<span data-ttu-id="1de3d-129">다음 단계에 따라 작업 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="1de3d-130">작업 세부 정보 보는 방법</span><span class="sxs-lookup"><span data-stu-id="1de3d-130">To view job details</span></span>
1. <span data-ttu-id="1de3d-131">**작업** 페이지에서 적절한 필터와 함께 쿼리를 실행하여 관심 있는 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="1de3d-132">완료되거나, 실행 중이거나, 취소된 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="1de3d-133">작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-133">Select a job.</span></span>
3. <span data-ttu-id="1de3d-134">페이지 맨 아래에서 **세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="1de3d-135">**백업 작업 세부 정보** 대화 상자에서 상태, 세부 정보, 시간 통계 및 데이터 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="1de3d-136">작업 취소</span><span class="sxs-lookup"><span data-stu-id="1de3d-136">Cancel a job</span></span>
<span data-ttu-id="1de3d-137">다음 단계에 따라 실행 중인 작업을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-137">Perform the following steps to cancel a running job.</span></span>

### <a name="to-cancel-a-job"></a><span data-ttu-id="1de3d-138">작업 취소 방법</span><span class="sxs-lookup"><span data-stu-id="1de3d-138">To cancel a job</span></span>
1. <span data-ttu-id="1de3d-139">**작업** 페이지에서 적절한 필터와 함께 쿼리를 실행하여 취소하려는 실행 중인 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-139">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="1de3d-140">작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-140">Select the job.</span></span>
3. <span data-ttu-id="1de3d-141">페이지 맨 아래에서 **취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-141">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="1de3d-142">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="1de3d-143">이 작업은 이제 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1de3d-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1de3d-144">Next steps</span></span>
* <span data-ttu-id="1de3d-145">[StorSimple 백업 정책을 관리](storsimple-manage-backup-policies.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-145">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="1de3d-146">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1de3d-146">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

