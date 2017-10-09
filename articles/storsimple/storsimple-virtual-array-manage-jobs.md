---
title: "aaaView StorSimple 가상 배열 작업을 관리 하 고 | Microsoft Docs"
description: "Hello StorSimple 장치 관리자 서비스 작업 페이지에 설명 방법과 toouse 것 hello StorSimple 가상 배열에 대 한 tootrack 최근 및 현재 작업 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="e2946-103">StorSimple 가상 배열 hello에 대 한 hello StorSimple 장치 관리자 서비스 tooview 작업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2946-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="e2946-104">개요</span><span class="sxs-lookup"><span data-stu-id="e2946-104">Overview</span></span>
<span data-ttu-id="e2946-105">hello **작업** 블레이드를 보고 하는 연결 된 tooyour StorSimple 장치 관리자 서비스는 가상 배열에서 시작 된 작업을 관리 하기 위한 단일 중앙 포털이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e2946-106">여러 가상 장치에 대한 실행, 완료 및 실패한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="e2946-107">결과는 표 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-107">Results are presented in a tabular format.</span></span>

![작업 블레이드](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="e2946-109">와 같은 필드를 필터링 하 여 관심 있는 hello 작업을 빠르게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="e2946-110">**시간 범위** – 작업에 따라 필터링 된 hello 날짜 및 시간 범위를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="e2946-111">**장치** – 작업은 연결 된 특정 장치 tooyour 서비스에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="e2946-112">hello 필터링 된 작업은 표 형식으로 표시 hello 특성 다음에 따라:</span><span class="sxs-lookup"><span data-stu-id="e2946-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="e2946-113">**이름** – hello 작업 이름은 수 **모든**, **백업**, **복제**, **장애 조치**, **업데이트 다운로드** , 또는 **업데이트 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="e2946-114">**상태** – 작업은 **모두**, **진행 중**, **성공**이나 **실패** 또는 **취소** 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="e2946-115">**엔터티** – hello 작업 볼륨, 공유 또는 장치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="e2946-116">**장치** – hello는 hello 작업이 시작 된 hello 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="e2946-117">**시작** – hello 작업이 시작 된 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="e2946-118">**기간** – hello에 대 한 기간 hello 작업이 실행 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="e2946-119">**상태** – 모두, 실행 중, 완료 또는 실패한 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="e2946-120">**작업 유형** – hello 작업 유형이 all, 백업, 복원, 장애 조치, 업데이트를 다운로드 하거나 수 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="e2946-121">hello 작업 목록은 30 초 마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="e2946-122">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="e2946-122">View job details</span></span>
<span data-ttu-id="e2946-123">다음 작업의 단계 tooview hello 세부 정보는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="e2946-124">tooview 작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e2946-124">tooview job details</span></span>
1. <span data-ttu-id="e2946-125">Hello에 **작업** 블레이드, 적절 한 필터가 포함 된 쿼리를 실행 하 여 관심 있는 hello 개의 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="e2946-126">완료되거나, 실행 중인 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="e2946-127">작업의 hello 표 형식 목록에서 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![작업 블레이드](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="e2946-129">Hello hello 페이지의 아래쪽에 있는 클릭 **세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="e2946-130">Hello에 **세부 정보** 대화 상자, 상태, 정보 및 시간 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="e2946-131">hello 다음 그림의 예가 나와 hello **백업 작업 세부 정보** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e2946-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![작업 세부 정보](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="e2946-133">Hello 하이퍼바이저에서 hello 가상 컴퓨터를 일시 중지 하면 작업 실패</span><span class="sxs-lookup"><span data-stu-id="e2946-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="e2946-134">작업 중인 경우 진행률 StorSimple 가상 배열 및 hello 장치 (하이퍼바이저에서 프로 비전 된 가상 컴퓨터) 15 분 이상에 대 한 일시 중지, hello 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="e2946-135">이 tooyour StorSimple 가상 배열 시간 인해 동기화 되지 hello Microsoft Azure 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="e2946-136">Hello 다음 오류가 표시 됩니다: "장치 시간은 15 분 초과 하 여 Microsoft Azure 시간 hello와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="e2946-137">Hello 하이퍼바이저 및 hello 장치 시간이 NTP 서비스와 동기화 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="e2946-138">연결 문제가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="e2946-139">tootroubleshoot 연결 문제 진단 테스트 hello 로컬 웹 UI에서에서 실행 하려면 가상 장치의. "</span><span class="sxs-lookup"><span data-stu-id="e2946-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="e2946-140">이러한 오류 toobackup, 복원, 업데이트 및 장애 조치 작업을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="e2946-141">Hyper-v에서 가상 컴퓨터를 프로 비전 경우 hello 컴퓨터는 결국 시간 프로그램 하이퍼바이저와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="e2946-142">이러한 동기화 후 작업을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2946-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2946-143">Next steps</span></span>
<span data-ttu-id="e2946-144">[어떻게 toouse hello 로컬 웹 UI tooadminister StorSimple 가상 배열에 알아봅니다](storsimple-ova-web-ui-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2946-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

