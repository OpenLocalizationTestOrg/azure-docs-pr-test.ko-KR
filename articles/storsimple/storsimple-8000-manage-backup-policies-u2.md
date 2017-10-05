---
title: "StorSimple 8000 시리즈 백업 정책 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스를 사용하여 StorSimple 8000 시리즈 장치에서 수동 백업, 백업 일정 및 백업 보존을 만들고 관리하는 방법을 설명합니다."
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
ms.openlocfilehash: 569dbfdeb7dcd526cb5a54b487ea1bfb59b13cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-manage-backup-policies"></a><span data-ttu-id="f6a58-103">Azure Portal에서 StorSimple 장치 관리자 서비스를 사용하여 백업 정책 관리</span><span class="sxs-lookup"><span data-stu-id="f6a58-103">Use the StorSimple Device Manager service in Azure portal to manage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="f6a58-104">개요</span><span class="sxs-lookup"><span data-stu-id="f6a58-104">Overview</span></span>

<span data-ttu-id="f6a58-105">이 자습서에서는 StorSimple 장치 관리자 서비스 **백업 정책** 블레이드를 사용하여 StorSimple 볼륨에 대한 백업 프로세스 및 백업 보존을 제어하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-105">This tutorial explains how to use the StorSimple Device Manager service **Backup policy** blade to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="f6a58-106">수동 백업을 완료하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="f6a58-107">볼륨을 백업할 때 로컬 스냅숏 또는 클라우드 스냅숏을 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="f6a58-108">로컬로 고정된 볼륨을 백업하는 경우 클라우드 스냅숏을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="f6a58-109">이탈 수가 많은 데이터 집합과 결합하여 로컬로 고정된 볼륨의 로컬 스냅숏을 많이 만들면 로컬 공간이 빨리 소진될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="f6a58-110">로컬 스냅숏을 만들기로 선택한 경우 가장 최근 상태를 백업하는 일일 스냅숏을 더 적게 만들어 하루 동안 유지한 다음 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="f6a58-111">로컬로 고정된 볼륨의 클라우드 스냅숏을 만드는 경우 중복 제거 및 압축된 클라우드로 변경된 데이터만 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span>

## <a name="the-backup-policy-blade"></a><span data-ttu-id="f6a58-112">백업 정책 블레이드</span><span class="sxs-lookup"><span data-stu-id="f6a58-112">The Backup policy blade</span></span>

<span data-ttu-id="f6a58-113">StorSimple 장치에 대한 **백업 정책** 블레이드에서는 백업 정책을 관리하고 로컬과 클라우드 스냅숏을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-113">The **Backup policy** blade for your StorSimple device allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="f6a58-114">백업 정책이 볼륨의 컬렉션에 대한 백업 보존 및 백업 일정을 구성하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-114">Backup policies are used to configure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="f6a58-115">백업 정책을 통해 동시에 여러 볼륨의 스냅숏을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-115">Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="f6a58-116">이 백업 정책에서 생성된 백업은 크래시 일관성이 있는 복사본임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-116">This means that the backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="f6a58-117">백업 정책 테이블 형식 목록에서 다음 필드 중 하나 이상의 기존 백업 정책을 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-117">The backup policies tabular listing also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="f6a58-118">**정책 이름** – 정책과 연결된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="f6a58-119">다음과 같은 다양한 유형의 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-119">The different types of policies include:</span></span>

  * <span data-ttu-id="f6a58-120">사용자가 명시적으로 만든 예약된 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="f6a58-121">원래 StorSimple 스냅숏 관리자에서 만든 가져온 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-121">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="f6a58-122">이 정책에서 가져온 StorSimple 스냅숏 관리자 호스트를 설명하는 태그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-122">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f6a58-123">볼륨을 만들 때는 자동 또는 기본 백업 정책이 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-123">Automatic or default backup policies are no longer enabled at the time of volume creation.</span></span>

* <span data-ttu-id="f6a58-124">**마지막으로 성공한 백업** –이 정책을 사용하여 수행된 마지막으로 성공한 백업 시간과 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-124">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="f6a58-125">**다음 백업** –이 정책에서 시작될 다음 예약 백업의 시간과 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-125">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="f6a58-126">**볼륨** – 정책과 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="f6a58-127">백업을 만들 때 백업 정책과 연관된 모든 볼륨이 함께 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="f6a58-128">**일정** – 백업 정책과 연관된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-128">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="f6a58-129">백업 정책에 대해 수행할 수 있는 자주 사용되는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-129">The frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="f6a58-130">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="f6a58-130">Add a backup policy</span></span>
* <span data-ttu-id="f6a58-131">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="f6a58-131">Add or modify a schedule</span></span>
* <span data-ttu-id="f6a58-132">볼륨 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="f6a58-132">Add or remove a volume</span></span>
* <span data-ttu-id="f6a58-133">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="f6a58-133">Delete a backup policy</span></span>
* <span data-ttu-id="f6a58-134">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="f6a58-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="f6a58-135">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="f6a58-135">Add a backup policy</span></span>

<span data-ttu-id="f6a58-136">자동 백업을 예약하려면 백업 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-136">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="f6a58-137">볼륨을 처음 만들 때는 볼륨과 연결된 기본 백업 정책이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="f6a58-138">볼륨 데이터를 보호하기 위해 백업 정책을 추가하고 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-138">You need to add and assign a backup policy to protect volume data.</span></span>

<span data-ttu-id="f6a58-139">StorSimple 장치에 대한 백업 정책을 추가하려면 Azure Portal에서 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-139">Perform the following steps in the Azure portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="f6a58-140">정책을 추가한 후 일정을 정의할 수 있습니다( [일정 추가 또는 수정](#add-or-modify-a-schedule)참조).</span><span class="sxs-lookup"><span data-stu-id="f6a58-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="f6a58-141">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="f6a58-141">Add or modify a schedule</span></span>

<span data-ttu-id="f6a58-142">StorSimple 장치의 기존 백업 정책에 첨부된 일정을 추가하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-142">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="f6a58-143">일정을 추가하거나 수정하려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-143">Perform the following steps in the Azure portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="f6a58-144">볼륨 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="f6a58-144">Add or remove a volume</span></span>

<span data-ttu-id="f6a58-145">StorSimple 장치에서 백업 정책에 할당된 볼륨을 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-145">You can add or remove a volume assigned to a backup policy on your StorSimple device.</span></span> <span data-ttu-id="f6a58-146">볼륨을 추가하거나 제거하려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-146">Perform the following steps in the Azure portal to add or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="f6a58-147">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="f6a58-147">Delete a backup policy</span></span>

<span data-ttu-id="f6a58-148">StorSimple 장치에서 백업 정책을 삭제하려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-148">Perform the following steps in the Azure portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="f6a58-149">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="f6a58-149">Take a manual backup</span></span>

<span data-ttu-id="f6a58-150">단일 볼륨에 대한 주문형(수동) 백업을 만들려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-150">Perform the following steps in the Azure portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="f6a58-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6a58-151">Next steps</span></span>

<span data-ttu-id="f6a58-152">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6a58-152">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

