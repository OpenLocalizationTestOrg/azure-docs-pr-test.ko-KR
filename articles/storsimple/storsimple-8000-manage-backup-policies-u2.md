---
title: "백업 정책이 aaaManage StorSimple 8000 시리즈 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 toocreate hello를 사용 하 여 수동 백업, 백업 일정 및 StorSimple 8000 시리즈 장치에 백업 보존을 관리 하는 방법에 대해 설명 합니다."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="00142-103">Hello StorSimple 장치 관리자 서비스를 사용 하 여 Azure 포털 toomanage 백업 정책에서</span><span class="sxs-lookup"><span data-stu-id="00142-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="00142-104">개요</span><span class="sxs-lookup"><span data-stu-id="00142-104">Overview</span></span>

<span data-ttu-id="00142-105">이 자습서에서는 어떻게 toouse hello StorSimple 장치 관리자 서비스에 설명 **백업 정책** 블레이드 toocontrol 백업 프로세스 및 StorSimple 볼륨에 대 한 백업 보존 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="00142-106">에 대해서도 설명 방법을 toocomplete 수동 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="00142-107">볼륨을 백업 하는 경우에 로컬 스냅숏 또는 클라우드 스냅숏을 toocreate를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="00142-108">로컬로 고정된 볼륨을 백업하는 경우 클라우드 스냅숏을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="00142-109">이탈 수가 많은 데이터 집합과 결합하여 로컬로 고정된 볼륨의 로컬 스냅숏을 많이 만들면 로컬 공간이 빨리 소진될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="00142-110">로컬 스냅숏 tootake를 선택 하면 더 적은 일일 스냅숏을 tooback hello 가장 최근 상태를 수행 하는 날에 대 한 유지 한 다음 삭제 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="00142-111">로컬로 고정 된 볼륨의 클라우드 스냅숏을 만들 때만 변경 하는 hello 데이터 toohello 클라우드, 중복 제거 및 압축 된 위치를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="00142-112">hello 백업 정책 블레이드</span><span class="sxs-lookup"><span data-stu-id="00142-112">hello Backup policy blade</span></span>

<span data-ttu-id="00142-113">hello **백업 정책** toomanage 백업 정책과 일정 로컬 및 클라우드 스냅숏 블레이드 StorSimple 장치에 대 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="00142-114">백업 정책이 사용 되는 tooconfigure 백업 일정 및 백업 보존 볼륨의 컬렉션에 대 한 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="00142-115">백업 정책을 사용 하면 여러 볼륨의 스냅숏을 tootake 동시에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="00142-116">이 백업 정책에 의해 생성 된 hello 백업을 크래시 일관성이 있는 복사본 된다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="00142-117">hello 백업 정책이 테이블 형식 목록에는 수도 있습니다 toofilter hello 기존 백업 정책을 hello 필드를 다음 중 하나 이상이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="00142-118">**정책 이름** – hello hello 정책과 연결 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00142-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="00142-119">hello 여러 가지 유형의 정책 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="00142-120">예약 된 정책을 hello 사용자가 명시적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="00142-121">StorSimple 스냅숏 관리자 hello에서 원래 만든 하는 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00142-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="00142-122">이러한 hello 정책에서 가져온 hello StorSimple 스냅숏 관리자 호스트를 설명 하는 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00142-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="00142-123">자동 또는 기본 백업 정책은 볼륨 생성 hello 시 더 이상 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00142-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="00142-124">**마지막으로 성공한 백업** – hello 날짜 및 시간 hello 마지막으로 성공한 백업에이 정책을 사용 하 여 만든입니다.</span><span class="sxs-lookup"><span data-stu-id="00142-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="00142-125">**다음 백업** – hello의 날짜 및 시간 hello 예약 된 다음 백업이이 정책에 의해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00142-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="00142-126">**볼륨** – hello hello 정책과 연결 된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="00142-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="00142-127">백업 정책과 연관 된 모든 hello 볼륨은 백업을 만들 때 함께 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00142-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="00142-128">**일정** – hello hello 백업 정책과 연관 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="00142-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="00142-129">백업 정책에 대해 수행할 수 있는 hello 자주 사용 되는 연산은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="00142-130">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="00142-130">Add a backup policy</span></span>
* <span data-ttu-id="00142-131">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="00142-131">Add or modify a schedule</span></span>
* <span data-ttu-id="00142-132">볼륨 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="00142-132">Add or remove a volume</span></span>
* <span data-ttu-id="00142-133">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="00142-133">Delete a backup policy</span></span>
* <span data-ttu-id="00142-134">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="00142-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="00142-135">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="00142-135">Add a backup policy</span></span>

<span data-ttu-id="00142-136">백업 정책 tooautomatically 일정 백업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="00142-137">볼륨을 처음 만들 때는 볼륨과 연결된 기본 백업 정책이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="00142-138">Tooadd 필요 하 고이 정보를 백업 정책 tooprotect 볼륨 데이터를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="00142-139">Azure 포털 tooadd StorSimple 장치에 대 한 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="00142-140">Hello 정책에 추가한 후에 일정을 정의할 수 있습니다 (참조 [추가 일정을 수정 하거나](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="00142-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="00142-141">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="00142-141">Add or modify a schedule</span></span>

<span data-ttu-id="00142-142">추가 하거나 StorSimple 장치에 연결 된 tooan 기존 백업 정책이 있는 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="00142-143">Hello hello Azure 포털 tooadd의에서 단계를 실행 하거나 일정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="00142-144">볼륨 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="00142-144">Add or remove a volume</span></span>

<span data-ttu-id="00142-145">추가 하거나 tooa 백업 정책을 StorSimple 장치에 할당 된 볼륨을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00142-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="00142-146">Azure 포털 tooadd hello 단계를 수행 하는 hello 하거나 볼륨을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="00142-147">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="00142-147">Delete a backup policy</span></span>

<span data-ttu-id="00142-148">StorSimple 장치에 Azure 포털 toodelete 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="00142-149">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="00142-149">Take a manual backup</span></span>

<span data-ttu-id="00142-150">단일 볼륨에 대 한 hello Azure 포털 toocreate 주문형 (수동) 백업 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="00142-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00142-151">Next steps</span></span>

<span data-ttu-id="00142-152">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00142-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

