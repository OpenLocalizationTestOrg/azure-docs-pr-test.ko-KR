---
title: "StorSimple 가상 배열 작업 보기 및 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 작업 페이지에 대해 설명하고 이 페이지를 사용하여 StorSimple 가상 배열에 대한 최근 및 현재 작업을 추적하는 방법을 설명합니다."
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="ff7f6-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열에 대한 작업 보기</span><span class="sxs-lookup"><span data-stu-id="ff7f6-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="ff7f6-104">개요</span><span class="sxs-lookup"><span data-stu-id="ff7f6-104">Overview</span></span>
<span data-ttu-id="ff7f6-105">**작업** 블레이드에서는 StorSimple 장치 관리자 서비스에 연결된 가상 배열에서 시작한 작업을 보고 관리하기 위한 단일 중앙 포털을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="ff7f6-106">여러 가상 장치에 대한 실행, 완료 및 실패한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="ff7f6-107">결과는 표 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-107">Results are presented in a tabular format.</span></span>

![작업 블레이드](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="ff7f6-109">다음과 같이 필드에서 필터링하여 관심 있는 작업을 빠르게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="ff7f6-110">**시간 범위** – 작업은 날짜 및 시간 범위에 따라 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="ff7f6-111">**장치** – 작업은 서비스에 연결된 특정 장치에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="ff7f6-112">그런 다음 필터링된 작업은 다음 특성을 기반으로 표로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="ff7f6-113">**이름** – 작업 이름은 **모두**, **백업**, **복제**, **장애 조치**, **업데이트 다운로드** 또는 **업데이트 설치**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="ff7f6-114">**상태** – 작업은 **모두**, **진행 중**, **성공**이나 **실패** 또는 **취소** 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="ff7f6-115">**엔터티** – 작업은 볼륨, 공유 또는 장치에 연관될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="ff7f6-116">**장치** – 작업이 시작된 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="ff7f6-117">**시작 시간** – 작업이 시작된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="ff7f6-118">**기간** – 작업이 실행되는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="ff7f6-119">**상태** – 모두, 실행 중, 완료 또는 실패한 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="ff7f6-120">**작업 유형** – 작업 유형은 모두, 백업, 복원, 장애 조치, 업데이트 다운로드 또는 업데이트 설치일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="ff7f6-121">작업 목록은 30초마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="ff7f6-122">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="ff7f6-122">View job details</span></span>
<span data-ttu-id="ff7f6-123">다음 단계에 따라 작업 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="ff7f6-124">작업 세부 정보 보는 방법</span><span class="sxs-lookup"><span data-stu-id="ff7f6-124">To view job details</span></span>
1. <span data-ttu-id="ff7f6-125">**작업** 블레이드에서 적절한 필터와 함께 쿼리를 실행하여 관심 있는 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="ff7f6-126">완료되거나, 실행 중인 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="ff7f6-127">작업 테이블 형식 목록에서 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-127">Select a job from the tabular list of jobs.</span></span>
   
    ![작업 블레이드](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="ff7f6-129">페이지 맨 아래에서 **세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="ff7f6-130">**세부 정보** 대화 상자에서 상태, 세부 정보 및 시간 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="ff7f6-131">다음 그림은 **백업 작업 세부 정보** 대화 상자의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![작업 세부 정보](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="ff7f6-133">가상 컴퓨터가 하이퍼바이저에서 일시 중지되는 경우 작업 실패</span><span class="sxs-lookup"><span data-stu-id="ff7f6-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="ff7f6-134">StorSimple 가상 배열에서 작업이 진행 중인 경우 장치(하이퍼바이저에 프로비전된 가상 컴퓨터)가 15분 넘게 일시 중지되면 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="ff7f6-135">이는 StorSimple 가상 배열 시간과 Microsoft Azure 시간이 동기화 해제되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="ff7f6-136">다음과 같은 오류가 표시됩니다. "장치 시간이 15분 넘게 Microsoft Azure와 동기화가 끊어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="ff7f6-137">하이퍼바이저와 장치 시간이 NTP 서비스와 동기화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="ff7f6-138">연결 문제가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="ff7f6-139">연결 문제를 해결하려면 가상 장치의 로컬 웹 UI에서 진단 테스트를 실행하세요."</span><span class="sxs-lookup"><span data-stu-id="ff7f6-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="ff7f6-140">이러한 실패는 백업, 복원, 업데이트 및 장애 조치(failover) 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="ff7f6-141">가상 컴퓨터가 Hyper-V에 프로비전된 경우 이 컴퓨터는 최종적으로 하이퍼바이저와 시간을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="ff7f6-142">이러한 동기화 후 작업을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff7f6-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff7f6-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff7f6-143">Next steps</span></span>
<span data-ttu-id="ff7f6-144">[로컬 웹 UI를 사용하여 StorSimple 가상 배열을 관리하는 방법을 알아봅니다.](storsimple-ova-web-ui-admin.md)</span><span class="sxs-lookup"><span data-stu-id="ff7f6-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

