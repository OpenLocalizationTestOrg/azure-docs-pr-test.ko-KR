---
title: "StorSimple 8000 시리즈에 대한 작업 보기 및 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 작업 블레이드에 대해 설명하고 이 페이지를 사용하여 최근, 현재 및 예약된 백업 작업을 추적하는 방법을 설명합니다."
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
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="0ad8d-103">StorSimple 장치 관리자 서비스를 사용하여 작업 보기 및 관리(업데이트 3 이상)</span><span class="sxs-lookup"><span data-stu-id="0ad8d-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="0ad8d-104">개요</span><span class="sxs-lookup"><span data-stu-id="0ad8d-104">Overview</span></span>
<span data-ttu-id="0ad8d-105">**작업** 블레이드에서는 StorSimple 장치 관리자 서비스에 연결된 장치에서 시작한 작업을 보고 관리하기 위한 하나 중앙 포털을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="0ad8d-106">여러 장치에 대해 예약, 실행 중, 완료, 취소, 실패한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="0ad8d-107">결과는 표 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-107">Results are presented in a tabular format.</span></span>

![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="0ad8d-109">다음과 같이 필드에서 필터링하여 관심 있는 작업을 빠르게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="0ad8d-110">**상태** – 작업은 진행 중, 성공, 취소됨, 실패, 취소 중 또는 오류를 나타내며 성공 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="0ad8d-111">**시간 범위** – 작업은 날짜 및 시간 범위에 따라 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="0ad8d-112">범위는 지난 1시간, 지난 24시간, 지난 7일, 지난 30일, 지난 해 및 사용자 지정 날짜일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="0ad8d-113">**유형** – 작업 유형에는 예약된 백업, 수동 백업, 백업 복원, 볼륨 복제, 볼륨 컨테이너 장애 조치, 로컬로 고정된 볼륨 만들기, 볼륨 수정, 업데이트 설치, 지원 로그 수집 및 클라우드 어플라이언스 만들기 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="0ad8d-114">**장치** – 작업은 서비스에 연결된 특정 장치에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="0ad8d-115">필터링된 작업은 다음과 같은 특성을 기반으로 표로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="0ad8d-116">**이름** – 예약된 백업, 수동 백업, 백업 복원, 볼륨 복제, 볼륨 컨테이너 장애 조치, 로컬로 고정된 볼륨 만들기, 볼륨 수정, 업데이트 설치, 지원 로그 수집 또는 클라우드 어플라이언스 만들기</span><span class="sxs-lookup"><span data-stu-id="0ad8d-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="0ad8d-117">**상태** – 실행 중, 완료, 취소, 실패, 취소 중 또는 완료되었으나 오류 발생입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="0ad8d-118">**엔터티** – 작업은 볼륨, 백업 정책 또는 장치에 연관될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="0ad8d-119">예를 들어 복제 작업은 볼륨과 연관되는 반면, 예약된 백업 작업은 백업 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="0ad8d-120">장치 작업은 DR(재해 복구) 또는 복원 작업의 결과로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="0ad8d-121">**장치** – 작업이 시작된 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="0ad8d-122">**시작 시간** – 작업이 시작된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="0ad8d-123">**기간** – 작업을 완료하는 데 필요한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="0ad8d-124">작업 목록은 30초마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="0ad8d-125">이 페이지에서 다음 작업과 관련된 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="0ad8d-126">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="0ad8d-126">View job details</span></span>
* <span data-ttu-id="0ad8d-127">작업 취소</span><span class="sxs-lookup"><span data-stu-id="0ad8d-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="0ad8d-128">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="0ad8d-128">View job details</span></span>
<span data-ttu-id="0ad8d-129">다음 단계에 따라 작업 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="0ad8d-130">작업 세부 정보 보는 방법</span><span class="sxs-lookup"><span data-stu-id="0ad8d-130">To view job details</span></span>
1. <span data-ttu-id="0ad8d-131">StorSimple 장치 관리자 서비스로 이동한 다음 **작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="0ad8d-132">**작업** 블레이드에서 적절한 필터와 함께 쿼리를 실행하여 관심 있는 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="0ad8d-133">완료되거나, 실행 중이거나, 취소된 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-133">You can search for completed, running, or canceled jobs.</span></span>

    ![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="0ad8d-135">작업을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-135">Select and click a job.</span></span>

    ![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="0ad8d-137">작업 세부 정보 블레이드에서 상태, 세부 정보, 시간 통계 및 데이터 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![작업 세부 정보](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="0ad8d-139">작업 취소</span><span class="sxs-lookup"><span data-stu-id="0ad8d-139">Cancel a job</span></span>
<span data-ttu-id="0ad8d-140">다음 단계에 따라 실행 중인 작업을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="0ad8d-141">볼륨 형식을 변경하기 위해 볼륨을 수정하거나 볼륨을 확장하는 등의 일부 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="0ad8d-142">작업 취소 방법</span><span class="sxs-lookup"><span data-stu-id="0ad8d-142">To cancel a job</span></span>
1. <span data-ttu-id="0ad8d-143">**작업** 페이지에서 적절한 필터와 함께 쿼리를 실행하여 취소하려는 실행 중인 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="0ad8d-144">작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-144">Select the job.</span></span>

2. <span data-ttu-id="0ad8d-145">선택한 작업을 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 표시하고 **취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![작업 세부 정보](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="0ad8d-147">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="0ad8d-148">이 작업은 이제 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ad8d-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ad8d-149">Next steps</span></span>
* <span data-ttu-id="0ad8d-150">[StorSimple 백업 정책을 관리](storsimple-8000-manage-backup-policies-u2.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ad8d-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="0ad8d-151">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="0ad8d-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

