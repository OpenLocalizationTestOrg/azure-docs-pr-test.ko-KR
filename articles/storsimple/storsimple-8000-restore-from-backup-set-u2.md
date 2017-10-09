---
title: "StorSimple 8000 시리즈에는 백업에서 볼륨 aaaRestore | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 장치 관리자 서비스 백업 카탈로그 toorestore 백업 세트에서 StorSimple 볼륨에 설명 합니다."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="b17b6-103">백업 세트에서 StorSimple 볼륨 복원</span><span class="sxs-lookup"><span data-stu-id="b17b6-103">Restore a StorSimple volume from a backup set</span></span>

## <a name="overview"></a><span data-ttu-id="b17b6-104">개요</span><span class="sxs-lookup"><span data-stu-id="b17b6-104">Overview</span></span>

<span data-ttu-id="b17b6-105">이 자습서에서는 기존 백업 세트를 사용 하 여 StorSimple 8000 시리즈 장치에 수행 하는 hello 복원 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-105">This tutorial describes hello restore operation performed on a StorSimple 8000 series device using an existing backup set.</span></span> <span data-ttu-id="b17b6-106">사용 하 여 hello **백업 카탈로그** 블레이드 toorestore 로컬에서 볼륨 또는 클라우드 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-106">Use hello **Backup catalog** blade toorestore a volume from a local or cloud backup.</span></span> <span data-ttu-id="b17b6-107">hello **백업 카탈로그** 블레이드 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-107">hello **Backup catalog** blade displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="b17b6-108">백업 세트에서 복원 작업 hello hello 백그라운드에서 데이터를 다운로드 하는 동안에 즉시 hello 볼륨을 온라인를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-108">hello restore operation from a backup set brings hello volume online immediately while data is downloaded in hello background.</span></span>

<span data-ttu-id="b17b6-109">대체 방법 toostart 복원 하는 경우이 toogo 너무**장치 > [장치] > 볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-109">An alternate method toostart restore is toogo too**Devices > [Your device] > Volumes**.</span></span> <span data-ttu-id="b17b6-110">Hello에 **볼륨** 블레이드에서 인 볼륨을 마우스 오른쪽 단추로 클릭 tooinvoke hello 상황에 맞는 메뉴를 선택한 다음 선택 **복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-110">In hello **Volumes** blade, select a volume, right-click tooinvoke hello context menu, and then select **Restore**.</span></span>

## <a name="before-you-restore"></a><span data-ttu-id="b17b6-111">복원하기 전에</span><span class="sxs-lookup"><span data-stu-id="b17b6-111">Before you restore</span></span>

<span data-ttu-id="b17b6-112">복원을 시작 하기 전에 다음 제한 사항을 적용 하는 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-112">Before you start a restore, review hello following caveats:</span></span>

* <span data-ttu-id="b17b6-113">**Hello 볼륨을 오프 라인으로 수행 해야** – hello 호스트 모두에서 hello 볼륨을 오프 라인 상태로 전환한 hello 복원 작업을 시작 하기 전에 장치 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-113">**You must take hello volume offline** – Take hello volume offline on both hello host and hello device before you initiate hello restore operation.</span></span> <span data-ttu-id="b17b6-114">Hello 복원 작업에 자동으로 hello 장치에서 hello 볼륨을 온라인 상태로, 있지만 hello 호스트에 hello 장치를 온라인을 수동으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-114">Although hello restore operation automatically brings hello volume online on hello device, you must manually bring hello device online on hello host.</span></span> <span data-ttu-id="b17b6-115">Hello 볼륨이 hello 장치에서 온라인으로 hello 호스트에서 볼륨을 온라인 hello를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-115">You can bring hello volume online on hello host as soon as hello volume is online on hello device.</span></span> <span data-ttu-id="b17b6-116">(않아도 toowait hello 복원 작업이 완료 될 때까지 합니다.) 너무 절차를 보려면[볼륨을 오프 라인](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-116">(You do not need toowait until hello restore operation is finished.) For procedures, go too[Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).</span></span>

* <span data-ttu-id="b17b6-117">**복원 후 볼륨 종류가** – 삭제 된 볼륨이 복원 hello 스냅숏의 hello 형식에 따라; 즉, 로컬로 고정 된 볼륨은 로컬로 고정 된 볼륨에서 복원 되 고 된 계층화 된 볼륨은 계층화 된 볼륨으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-117">**Volume type after restore** – Deleted volumes are restored based on hello type in hello snapshot; that is, volumes that were locally pinned are restored as locally pinned volumes and volumes that were tiered are restored as tiered volumes.</span></span>

    <span data-ttu-id="b17b6-118">기존 볼륨에 대 한 hello 볼륨의 현재 사용 유형을 hello hello 스냅숏에 저장 된 hello 형식을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-118">For existing volumes, hello current usage type of hello volume overrides hello type that is stored in hello snapshot.</span></span> <span data-ttu-id="b17b6-119">예를 들어 hello 볼륨 종류가 계층을 지정할 때 만들어진 스냅숏으로에서 볼륨을 복원 하는 경우 수행 된 tooa 변환 작업) (인해 고정 된 볼륨 종류가 이제 인지 로컬로 hello 볼륨을 로컬 고정된 볼륨으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-119">For example, if you restore a volume from a snapshot that was taken when hello volume type was tiered and that volume type is now locally pinned (due tooa conversion operation that was performed), then hello volume will be restored as a locally pinned volume.</span></span> <span data-ttu-id="b17b6-120">마찬가지로, 기존 로컬 고정된 볼륨 확장 고 이후에 hello 볼륨을 더 작은 경우에 수행 되는 이전 스냅숏에서 복원 인 경우 hello 복원 된 볼륨 유지 됩니다 hello 현재 확장 된 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-120">Similarly, if an existing locally pinned volume was expanded and subsequently restored from an older snapshot taken when hello volume was smaller, hello restored volume will retain hello current expanded size.</span></span>

    <span data-ttu-id="b17b6-121">계층화 된 볼륨 tooa 로컬로 고정 된 볼륨에서 볼륨을 변환할 수 없습니다 또는 로컬 고정된 볼륨 tooa에서 계층으로 계층화 된 볼륨 hello 볼륨을 복원 하는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-121">You cannot convert a volume from a tiered volume tooa locally pinned volume or from a locally pinned volume tooa tiered volume while hello volume is being restored.</span></span> <span data-ttu-id="b17b6-122">Hello 복원 작업이 완료 되 면 다음 hello 볼륨 tooanother 유형을 변환할 수 있습니다 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-122">Wait until hello restore operation is finished, and then you can convert hello volume tooanother type.</span></span> <span data-ttu-id="b17b6-123">볼륨을 변환 하는 방법에 대 한 내용은 이동 너무[hello 볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-123">For information about converting a volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span> 

* <span data-ttu-id="b17b6-124">**hello 볼륨 크기에에서 반영 되어 복원 hello 볼륨** – 삭제 (로컬 고정된 볼륨이 완전히 프로 비전) 되므로 로컬로 고정 된 볼륨을 복원 하는 경우이 중요 한 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-124">**hello volume size is reflected in hello restored volume** – This is an important consideration if you are restoring a locally pinned volume that has been deleted (because locally pinned volumes are fully provisioned).</span></span> <span data-ttu-id="b17b6-125">이전에 삭제 된 로컬 고정된 볼륨 toorestore를 시도 하기 전에 충분 한 공간이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-125">Make sure that you have sufficient space before you attempt toorestore a locally pinned volume that was previously deleted.</span></span>

* <span data-ttu-id="b17b6-126">**복원 하는 동안 볼륨을 확장할 수 없지만** – tooexpand hello 볼륨을 시도 하기 전에 hello 복원 작업이 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-126">**You cannot expand a volume while it is being restored** – Wait until hello restore operation is finished before you attempt tooexpand hello volume.</span></span> <span data-ttu-id="b17b6-127">볼륨을 확장 하는 방법에 대 한 내용은 이동 너무[볼륨 수정](storsimple-8000-manage-volumes-u2.md#modify-a-volume)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-127">For information about expanding a volume, go too[Modify a volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).</span></span>

* <span data-ttu-id="b17b6-128">**로컬 볼륨을 복원 하는 동안에 백업을 수행할 수** 에 대 한 프로시저 너무 –[hello StorSimple 장치 관리자 서비스 toomanage 백업 정책을 사용 하 여](storsimple-8000-manage-backup-policies-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-128">**You can perform a backup while you restore a local volume** – For procedures go too[Use hello StorSimple Device Manager service toomanage backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>

* <span data-ttu-id="b17b6-129">**복원 작업을 취소할 수** -hello 볼륨 롤백되어 toohello 상태에 있었던 hello 복원 작업을 시작 하기 전에 다음 hello 복원 작업을 취소 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b17b6-129">**You can cancel a restore operation** – If you cancel hello restore job, then hello volume will be rolled back toohello state that it was in before you initiated hello restore operation.</span></span> <span data-ttu-id="b17b6-130">너무 절차를 보려면[작업 취소](storsimple-8000-manage-jobs-u2.md#cancel-a-job)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-130">For procedures, go too[Cancel a job](storsimple-8000-manage-jobs-u2.md#cancel-a-job).</span></span>

## <a name="how-does-restore-work"></a><span data-ttu-id="b17b6-131">복원 작업 방법</span><span class="sxs-lookup"><span data-stu-id="b17b6-131">How does restore work</span></span>

<span data-ttu-id="b17b6-132">업데이트 4 이상을 실행하는 장치의 경우 heatmap 기반 복원이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-132">For devices running Update 4 or later, a heatmap-based restore is implemented.</span></span> <span data-ttu-id="b17b6-133">Hello 호스트 요청 tooaccess 데이터 hello 장치에 도달 하는 대로 이러한 요청은 추적 하 고는 heatmap 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-133">As hello host requests tooaccess data reach hello device, these requests are tracked and a heatmap is created.</span></span> <span data-ttu-id="b17b6-134">높은 요청 속도 요청 속도가 느린 toochunks 낮은 열으로 변환 하는 반면 더 높은 열으로는 데이터 청크를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-134">High request rate results in data chunks with higher heat whereas lower request rate translates toochunks with lower heat.</span></span> <span data-ttu-id="b17b6-135">Hello 데이터 적어도 두 번 toobe로 표시 된 액세스 해야 _핫_합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-135">You must access hello data atleast twice toobe marked as _hot_.</span></span> <span data-ttu-id="b17b6-136">수정된 파일도 _hot_으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-136">A file that is modified is also marked as _hot_.</span></span> <span data-ttu-id="b17b6-137">Hello 복원을 시작한 후의 데이터 사전 하이드레이션 hello heatmap에 따라 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-137">Once you initiate hello restore, then proactive hydration of data occurs based on hello heatmap.</span></span> <span data-ttu-id="b17b6-138">업데이트 4 이전 버전에 대 한 hello 데이터 액세스만에 따라 복원 하는 동안 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-138">For versions earlier than Update 4, hello data is downloaded during restore based on access only.</span></span>

<span data-ttu-id="b17b6-139">다음 제한 사항을 적용 하는 hello tooheatmap 기반 복원 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-139">hello following caveats apply tooheatmap-based restores:</span></span>

* <span data-ttu-id="b17b6-140">열 지도 추적은 계층화된 볼륨에 대해서만 사용하도록 설정되고 로컬로 고정된 볼륨은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-140">Heatmap tracking is enabled only for tiered volumes and locally pinned volumes are not supported.</span></span>

* <span data-ttu-id="b17b6-141">Heatmap 기반 복원 tooanother 장치 볼륨을 복제할 때 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-141">Heatmap-based restore is not supported when cloning a volume tooanother device.</span></span> 

* <span data-ttu-id="b17b6-142">원위치에서 복원 하는 경우 hello 장치에 hello 볼륨 toobe 복원에 대 한 로컬 스냅숏이 있는 경우 다음 म 수행 하지 리하이드레이션 (한 데이터를 로컬로 사용할 수 이미).</span><span class="sxs-lookup"><span data-stu-id="b17b6-142">If there is an in-place restore and a local snapshot for hello volume toobe restored exists on hello device, then we do not rehydrate (as data is already available locally).</span></span> 

* <span data-ttu-id="b17b6-143">기본적으로 복원 하면 hello 리하이드레이션 작업 시작 됩니다 hello heatmap를 기반으로 데이터를 리하이드레이션 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-143">By default, when you restore, hello rehydration jobs are initiated that proactively rehydrate data based on hello heatmap.</span></span> 

<span data-ttu-id="b17b6-144">업데이트 4에서 Windows PowerShell cmdlet 수 리하이드레이션 작업을 실행 하는 사용 되는 tooquery, 리하이드레이션 작업을 취소 있으며 hello 리하이드레이션 작업의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-144">In Update 4, Windows PowerShell cmdlets can be used tooquery running rehydration jobs, cancel a rehydration job, and get hello status of hello rehydration job.</span></span>

* <span data-ttu-id="b17b6-145">`Get-HcsRehydrationJob`-이 cmdlet는 hello 리하이드레이션 작업의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-145">`Get-HcsRehydrationJob` - This cmdlet gets hello status of hello rehydration job.</span></span> <span data-ttu-id="b17b6-146">하나의 볼륨에 대해 단일 리하이드레이션 작업이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-146">A single rehydration job is triggered for one volume.</span></span>

* <span data-ttu-id="b17b6-147">`Set-HcsRehydrationJob`-이 cmdlet toopause, 중지, hello 리하이드레이션 진행 중인 경우 hello 리하이드레이션 작업을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-147">`Set-HcsRehydrationJob` - This cmdlet allows you toopause, stop, resume hello rehydration job, when hello rehydration is in progress.</span></span>

<span data-ttu-id="b17b6-148">리하이드레이션 cmdlet에 대 한 자세한 내용은 이동 너무[StorSimple 용 Windows PowerShell cmdlet 참조](https://technet.microsoft.com/library/dn688168.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-148">For more information on rehydration cmdlets, go too[Windows PowerShell cmdlet reference for StorSimple](https://technet.microsoft.com/library/dn688168.aspx).</span></span>

<span data-ttu-id="b17b6-149">자동 리하이드레이션을 사용하면 일반적으로 일시적인 더 높은 읽기 성능이 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-149">With automatic rehdyration, typically higher transient read performance is expected.</span></span> <span data-ttu-id="b17b6-150">향상 된 hello 실제 magniutde 액세스 패턴, 데이터 청크 및 데이터 형식 등의 다양 한 요인에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-150">hello actual magniutde of improvements depends on various factors such as access pattern, data churn, and data type.</span></span> 

<span data-ttu-id="b17b6-151">리하이드레이션 작업 toocancel hello PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-151">toocancel a rehydration job, you can use hello PowerShell cmdlet.</span></span> <span data-ttu-id="b17b6-152">이후 복원 hello 모두에 대 한 toopermanently 사용 안 함 리하이드레이션 작업 하려는 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-152">If you wish toopermanently disable rehydration jobs for all hello future restores, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="b17b6-153">어떻게 toouse hello 백업 카탈로그</span><span class="sxs-lookup"><span data-stu-id="b17b6-153">How toouse hello backup catalog</span></span>

<span data-ttu-id="b17b6-154">hello **백업 카탈로그** 블레이드 백업 세트 선택 toonarrow 수 있는 쿼리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-154">hello **Backup Catalog** blade provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="b17b6-155">Hello 백업 세트를 검색 하는 hello 매개 변수 뒤에 따라 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-155">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="b17b6-156">**시간 범위** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-156">**Time range** – hello date and time range when hello backup set was created.</span></span>
* <span data-ttu-id="b17b6-157">**장치** – hello 장치는 hello에 백업 세트 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-157">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="b17b6-158">**백업 정책** 또는 **볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-158">**Backup policy** or **Volume** – hello backup policy or volume associated with this backup set.</span></span>

<span data-ttu-id="b17b6-159">hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:</span><span class="sxs-lookup"><span data-stu-id="b17b6-159">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="b17b6-160">**이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-160">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="b17b6-161">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-161">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="b17b6-162">로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-162">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="b17b6-163">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-163">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="b17b6-164">**크기** – hello hello 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-164">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="b17b6-165">**만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-165">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="b17b6-166">**볼륨** -hello hello 백업 세트와 연결 된 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-166">**Volumes** - hello number of volumes associated with hello backup set.</span></span>
* <span data-ttu-id="b17b6-167">**시작** – hello 백업을 tooa 일정에 따라 자동으로 시작 될 수 있습니다 또는 사용자가 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-167">**Initiated** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="b17b6-168">(백업 정책 tooschedule 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-168">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="b17b6-169">Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 대화형 또는 요청 시 백업 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b17b6-169">Alternatively, you can use hello **Take backup** option tootake an interactive or on-demand backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="b17b6-170">어떻게 toorestore 백업에서 StorSimple 볼륨</span><span class="sxs-lookup"><span data-stu-id="b17b6-170">How toorestore your StorSimple volume from a backup</span></span>

<span data-ttu-id="b17b6-171">Hello를 사용할 수 있습니다 **백업 카탈로그** 블레이드 toorestore 특정 백업에서 StorSimple 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-171">You can use hello **Backup Catalog** blade toorestore your StorSimple volume from a specific backup.</span></span> <span data-ttu-id="b17b6-172">그러나 점을 기억할 해당 볼륨을 복원 hello 볼륨 toohello의 상태로 hello 백업을 만들 때 사용 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-172">Keep in mind, however, that restoring a volume will revert hello volume toohello state it was in when hello backup was taken.</span></span> <span data-ttu-id="b17b6-173">Hello 백업 작업 후 추가 된 모든 데이터는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-173">Any data that was added after hello backup operation will be lost.</span></span>

> [!WARNING]
> <span data-ttu-id="b17b6-174">백업에서 복원 hello hello 백업에서 기존 볼륨이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-174">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="b17b6-175">Hello 백업을 수행한 후에 기록 된 모든 데이터의 손실을 hello 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-175">This may cause hello loss of any data that was written after hello backup was taken.</span></span>


### <a name="toorestore-your-volume"></a><span data-ttu-id="b17b6-176">toorestore 볼륨</span><span class="sxs-lookup"><span data-stu-id="b17b6-176">toorestore your volume</span></span>
1. <span data-ttu-id="b17b6-177">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-177">Go tooyour StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="b17b6-178">백업 세트를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-178">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="b17b6-179">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-179">Specify hello time range.</span></span>
   2. <span data-ttu-id="b17b6-180">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-180">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="b17b6-181">Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-181">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="b17b6-182">클릭 **적용** tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-182">Click **Apply** tooexecute this query.</span></span>

    <span data-ttu-id="b17b6-183">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-183">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
   
    ![백업 세트 목록](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. <span data-ttu-id="b17b6-185">Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-185">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="b17b6-186">이러한 볼륨을 복구 하기 전에 hello 호스트와 장치에서 오프 라인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-186">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="b17b6-187">Hello에 hello 볼륨을 액세스할 **볼륨** 단계 장치 및 다음에 따라 hello 블레이드 [볼륨을 오프 라인](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake를 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-187">Access hello volumes on hello **Volumes** blade of your device, and then follow hello steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b17b6-188">수행 하 여 hello 호스트의 hello 볼륨을 오프 라인으로 먼저 hello 장치에서 hello 볼륨을 오프 라인으로 수행 하기 전에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-188">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="b17b6-189">Hello 호스트에서 오프 라인으로 hello 볼륨을 사용 하지 않는 경우 toodata 손상이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-189">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   
4. <span data-ttu-id="b17b6-190">뒤로 toohello 이동 **백업 카탈로그** 탭 하 고 백업 세트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-190">Navigate back toohello **Backup Catalog** tab and select a backup set.</span></span> <span data-ttu-id="b17b6-191">마우스 오른쪽 단추로 클릭 한 다음 hello 상황에 맞는 메뉴에서 선택 **복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-191">Right-click and then from hello context menu, select **Restore**.</span></span>

    ![백업 세트 목록](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. <span data-ttu-id="b17b6-193">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-193">You will be prompted for confirmation.</span></span> <span data-ttu-id="b17b6-194">검토 hello 정보를 복원 하 고 hello 확인 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-194">Review hello restore information, and then select hello confirmation check box.</span></span>
   
    ![확인 페이지](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  <span data-ttu-id="b17b6-196">**복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-196">Click **Restore**.</span></span> <span data-ttu-id="b17b6-197">이 명령은 hello에 액세스 하 여 볼 수 있는 복원 작업을 시작 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b17b6-197">This initiates a restore job that you can view by accessing hello **Jobs** page.</span></span>

    ![확인 페이지](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. <span data-ttu-id="b17b6-199">Hello 복원이 완료 된 후 볼륨의 hello 내용을 hello 백업에서 볼륨으로 바뀌는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-199">After hello restore is complete, verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>


## <a name="if-hello-restore-fails"></a><span data-ttu-id="b17b6-200">Hello 복원 실패</span><span class="sxs-lookup"><span data-stu-id="b17b6-200">If hello restore fails</span></span>

<span data-ttu-id="b17b6-201">어떤 이유로 든 hello 복원 작업이 실패 하는 경우 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-201">You will receive an alert if hello restore operation fails for any reason.</span></span> <span data-ttu-id="b17b6-202">이 경우 백업 hello 새로 고침 hello 백업 목록 tooverify 계속 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-202">If this occurs, refresh hello backup list tooverify that hello backup is still valid.</span></span> <span data-ttu-id="b17b6-203">Hello 백업을 유효한 hello 클라우드에서 복원 하는 경우 다음 연결 문제가 있습니다 수 hello 문제가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-203">If hello backup is valid and you are restoring from hello cloud, then connectivity issues might be causing hello problem.</span></span>

<span data-ttu-id="b17b6-204">toocomplete hello 복원 작업, hello 호스트에서 hello 볼륨을 오프 라인 및 hello 복원 작업을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b17b6-204">toocomplete hello restore operation, take hello volume offline on hello host and retry hello restore operation.</span></span> <span data-ttu-id="b17b6-205">참고 hello 중에 수행 된 모든 수정 내용을 toohello 볼륨 데이터 복원 프로세스는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-205">Note that any modifications toohello volume data that were performed during hello restore process will be lost.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b17b6-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b17b6-206">Next steps</span></span>
* <span data-ttu-id="b17b6-207">너무 방법에 대해 알아봅니다[관리 StorSimple 볼륨](storsimple-8000-manage-volumes-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-207">Learn how too[Manage StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="b17b6-208">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b17b6-208">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

