---
title: "aaaManage StorSimple 백업 정책 | Microsoft Docs"
description: "StorSimple Manager 서비스 toocreate hello를 사용 하 여 수동 백업, 백업 일정 및 백업 보유 관리 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="c4b6b-103">Hello StorSimple 관리자 서비스 toomanage 백업 정책 (업데이트 2)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c4b6b-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="c4b6b-104">개요</span><span class="sxs-lookup"><span data-stu-id="c4b6b-104">Overview</span></span>
<span data-ttu-id="c4b6b-105">이 자습서에서는 어떻게 toouse hello StorSimple Manager 서비스에 설명 **백업 정책** 페이지 toocontrol 백업 프로세스 및 StorSimple 볼륨에 대 한 백업 보존 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="c4b6b-106">에 대해서도 설명 방법을 toocomplete 수동 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="c4b6b-107">볼륨을 백업 하는 경우에 로컬 스냅숏 또는 클라우드 스냅숏을 toocreate를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="c4b6b-108">로컬로 고정된 볼륨을 백업하는 경우 클라우드 스냅숏을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="c4b6b-109">이탈 수가 많은 데이터 집합과 결합하여 로컬로 고정된 볼륨의 로컬 스냅숏을 많이 만들면 로컬 공간이 빨리 소진될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="c4b6b-110">로컬 스냅숏 tootake를 선택 하면 더 적은 일일 스냅숏을 tooback hello 가장 최근 상태를 수행 하는 날에 대 한 유지 한 다음 삭제 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="c4b6b-111">로컬로 고정 된 볼륨의 클라우드 스냅숏을 만들 때만 변경 하는 hello 데이터 toohello 클라우드, 중복 제거 및 압축 된 위치를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="c4b6b-112">hello 백업 정책 페이지</span><span class="sxs-lookup"><span data-stu-id="c4b6b-112">hello Backup Policies page</span></span>
<span data-ttu-id="c4b6b-113">hello **백업 정책** toomanage 백업 정책과 일정 로컬 및 클라우드 스냅숏 페이지에서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="c4b6b-114">(백업 정책이 사용 되는 tooconfigure 백업 일정 및 백업 보존 볼륨의 컬렉션에 대 한 않습니다.) 백업 정책을 사용 하면 여러 볼륨의 스냅숏을 tootake 동시에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="c4b6b-115">이 백업 정책에 의해 생성 된 hello 백업을 크래시 일관성이 있는 복사본 된다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="c4b6b-116">hello **백업 정책** 페이지 hello 백업 정책, 유형, 연결 된 hello 볼륨, 보존 된 백업 hello 수를 나열 하 고 hello 옵션 tooenable 이러한 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="c4b6b-117">hello **백업 정책** 페이지도 있습니다 toofilter hello 기존 백업 정책을 하나 이상의 필드를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="c4b6b-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="c4b6b-118">**정책 이름** – hello hello 정책과 연결 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="c4b6b-119">hello 여러 가지 유형의 정책 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="c4b6b-120">예약 된 정책을 hello 사용자가 명시적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="c4b6b-121">볼륨 만들기의 hello 시간에서이 볼륨 옵션에 대 한 기본 백업 hello를 설정할 때 만들어지는 자동 정책.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="c4b6b-122">이러한 정책은 관계로 명명 됩니다 *VolumeName*_Default 여기서 *VolumeName* hello hello Azure 클래식 포털에서에서 hello 사용자가 구성 된 StorSimple 볼륨의 toohello 이름을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="c4b6b-123">hello 자동 정책 22 시 30 장치 시간부터 시작 하는 일별 클라우드 스냅숏이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="c4b6b-124">StorSimple 스냅숏 관리자 hello에서 원래 만든 하는 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="c4b6b-125">이러한 hello 정책에서 가져온 hello StorSimple 스냅숏 관리자 호스트를 설명 하는 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="c4b6b-126">**볼륨** – hello hello 정책과 연결 된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="c4b6b-127">백업 정책과 연관 된 모든 hello 볼륨은 백업을 만들 때 함께 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="c4b6b-128">**마지막으로 성공한 백업** – hello 날짜 및 시간 hello 마지막으로 성공한 백업에이 정책을 사용 하 여 만든입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="c4b6b-129">**다음 백업** – hello의 날짜 및 시간 hello 예약 된 다음 백업이이 정책에 의해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="c4b6b-130">**일정** – hello hello 백업 정책과 연관 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="c4b6b-131">이 페이지에서 수행할 수 있는 hello 자주 사용 되는 연산은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="c4b6b-132">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="c4b6b-132">Add a backup policy</span></span> 
* <span data-ttu-id="c4b6b-133">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="c4b6b-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="c4b6b-134">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="c4b6b-134">Delete a backup policy</span></span> 
* <span data-ttu-id="c4b6b-135">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="c4b6b-135">Take a manual backup</span></span> 
* <span data-ttu-id="c4b6b-136">여러 볼륨과 일정의 사용자 지정 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b6b-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="c4b6b-137">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="c4b6b-137">Add a backup policy</span></span>
<span data-ttu-id="c4b6b-138">백업 정책 tooautomatically 일정 백업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="c4b6b-139">Azure 클래식 포털 tooadd StorSimple 장치에 대 한 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="c4b6b-140">Hello 정책에 추가한 후에 일정을 정의할 수 있습니다 (참조 [추가 일정을 수정 하거나](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="c4b6b-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="c4b6b-141">![동영상 사용 가능](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="c4b6b-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="c4b6b-142">toowatch toocreate 로컬 또는 클라우드 백업 정책에 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="c4b6b-143">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="c4b6b-143">Add or modify a schedule</span></span>
<span data-ttu-id="c4b6b-144">추가 하거나 StorSimple 장치에 연결 된 tooan 기존 백업 정책이 있는 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="c4b6b-145">Hello hello Azure 클래식 포털 tooadd의에서 단계를 실행 하거나 일정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="c4b6b-146">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="c4b6b-146">Delete a backup policy</span></span>
<span data-ttu-id="c4b6b-147">StorSimple 장치에서 Azure 클래식 포털 toodelete 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="c4b6b-148">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="c4b6b-148">Take a manual backup</span></span>
<span data-ttu-id="c4b6b-149">단일 볼륨에 대 한 hello Azure 클래식 포털 toocreate 주문형 (수동) 백업 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="c4b6b-150">여러 볼륨과 일정의 사용자 지정 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b6b-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="c4b6b-151">Hello hello Azure 클래식 포털 toocreate 여러 볼륨과 일정이 있는 사용자 지정 백업 정책에에서는 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="c4b6b-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4b6b-152">Next steps</span></span>
<span data-ttu-id="c4b6b-153">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b6b-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

