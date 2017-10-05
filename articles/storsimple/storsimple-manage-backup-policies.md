---
title: "StorSimple 백업 정책 관리 | Microsoft Docs"
description: "StorSimple Manager 서비스를 사용하여 수동 백업, 백업 일정 및 백업 보존을 만들고 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: c1e9d5d0450bab5d371aafb40fd7c5920d39dfdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies"></a><span data-ttu-id="37054-103">StorSimple 관리자 서비스를 사용하여 백업 정책 관리</span><span class="sxs-lookup"><span data-stu-id="37054-103">Use the StorSimple Manager service to manage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="37054-104">개요</span><span class="sxs-lookup"><span data-stu-id="37054-104">Overview</span></span>
<span data-ttu-id="37054-105">이 자습서에서는 StorSimple Manager 서비스 **백업 정책** 페이지를 사용하여 StorSimple 볼륨에 대한 백업 프로세스 및 백업 보존을 제어하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="37054-106">수동 백업을 완료하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="37054-107">**백업 정책** 페이지에서는 백업 정책을 관리하고 로컬과 클라우드 스냅숏을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37054-107">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="37054-108">(백업 정책이 볼륨의 컬렉션에 대한 백업 보존 및 백업 일정을 구성하는데 사용됩니다.) 백업 정책을 통해 동시에 여러 볼륨의 스냅숏을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37054-108">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="37054-109">이 백업 정책에서 생성된 백업은 크래시 일관성이 있는 복사본임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-109">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="37054-110">이 페이지는 백업 정책, 해당 형식, 연결된 볼륨, 보존된 백업의 수 및 이 정책을 사용하도록 설정하는 옵션을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-110">This page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="37054-111">**백업 정책** 페이지에서 다음 필드 중 하나 이상의 기존 백업 정책을 필터링 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37054-111">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="37054-112">**정책 이름** – 정책과 연결된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-112">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="37054-113">다음과 같은 다양한 유형의 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37054-113">The different types of policies include:</span></span>
  
  * <span data-ttu-id="37054-114">사용자가 명시적으로 만든 예약된 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-114">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="37054-115">볼륨 생성 시 이 볼륨 옵션에 대한 기본 백업이 활성화되면 만들어지는 자동 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-115">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="37054-116">이 정책은 사용자가 Azure 클래식 포털에서 구성한 StoreSimple 볼륨의 이름을 참조한 볼륨 이름에서 VolumeName_Default로 이름이 지정됩니다. </span><span class="sxs-lookup"><span data-stu-id="37054-116">These policies are named as VolumeName_Default where Volume name refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="37054-117">자동 정책을 사용하면 22시 30분 장치 시간에서 시작하는 일일 클라우드 스냅숏이 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="37054-117">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="37054-118">원래 StorSimple 스냅숏 관리자에서 만든 가져온 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-118">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="37054-119">이 정책에서 가져온 StorSimple 스냅숏 관리자 호스트를 설명하는 태그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37054-119">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="37054-120">**볼륨** – 정책과 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-120">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="37054-121">백업을 만들 때 백업 정책과 연관된 모든 볼륨이 함께 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="37054-121">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="37054-122">**마지막으로 성공한 백업** –이 정책을 사용하여 수행된 마지막으로 성공한 백업 시간과 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-122">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="37054-123">**다음 백업** –이 정책에서 시작될 다음 예약 백업의 시간과 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-123">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="37054-124">**일정** – 백업 정책과 연관된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="37054-124">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="37054-125">이 페이지에서 수행할 수 있는 자주 사용 되는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37054-125">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="37054-126">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="37054-126">Add a backup policy</span></span> 
* <span data-ttu-id="37054-127">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="37054-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="37054-128">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="37054-128">Delete a backup policy</span></span> 
* <span data-ttu-id="37054-129">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="37054-129">Take a manual backup</span></span> 
* <span data-ttu-id="37054-130">여러 볼륨과 일정의 사용자 지정 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="37054-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="37054-131">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="37054-131">Add a backup policy</span></span>
<span data-ttu-id="37054-132">자동 백업을 예약하려면 백업 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-132">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="37054-133">StorSimple 장치에 대한 백업 정책을 추가할뎌면 Azure 클래식 포털에서 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-133">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="37054-134">정책을 추가한 후 일정을 정의할 수 있습니다( [일정 추가 또는 수정](#add-or-modify-a-schedule)참조).</span><span class="sxs-lookup"><span data-stu-id="37054-134">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="37054-135">![동영상 사용 가능](./media/storsimple-manage-backup-policies/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="37054-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="37054-136">로컬 또는 클라우드 백업 정책을 만드는 방법을 보여 주는 동영상을 시청하려면 [여기](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="37054-136">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="37054-137">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="37054-137">Add or modify a schedule</span></span>
<span data-ttu-id="37054-138">StorSimple 장치의 기존 백업 정책에 첨부된 일정을 추가하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37054-138">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="37054-139">일정을 추가하거나 수정하려면 Azure 클래식 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-139">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="37054-140">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="37054-140">Delete a backup policy</span></span>
<span data-ttu-id="37054-141">StorSimple 장치에서 백업 정책을 삭제하려면 Azure 클래식 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-141">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="37054-142">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="37054-142">Take a manual backup</span></span>
<span data-ttu-id="37054-143">단일 볼륨에 대한 주문형(수동) 백업을 만들려면 Azure 클래식 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-143">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="37054-144">여러 볼륨과 일정의 사용자 지정 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="37054-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="37054-145">다중 볼륨 및 일정이 포함된 사용자 백업 정책을 만들려면 Azure 클래식 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37054-145">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="37054-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37054-146">Next steps</span></span>
<span data-ttu-id="37054-147">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="37054-147">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

