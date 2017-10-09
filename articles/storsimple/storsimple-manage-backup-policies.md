---
title: "aaaManage StorSimple 백업 정책 | Microsoft Docs"
description: "StorSimple Manager 서비스 toocreate hello를 사용 하 여 수동 백업, 백업 일정 및 백업 보유 관리 하는 방법에 대해 설명 합니다."
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
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="5f9bf-103">Hello StorSimple 관리자 서비스 toomanage 백업 정책을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5f9bf-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="5f9bf-104">개요</span><span class="sxs-lookup"><span data-stu-id="5f9bf-104">Overview</span></span>
<span data-ttu-id="5f9bf-105">이 자습서에서는 어떻게 toouse hello StorSimple Manager 서비스에 설명 **백업 정책** 페이지 toocontrol 백업 프로세스 및 StorSimple 볼륨에 대 한 백업 보존 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="5f9bf-106">에 대해서도 설명 방법을 toocomplete 수동 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="5f9bf-107">hello **백업 정책** toomanage 백업 정책과 일정 로컬 및 클라우드 스냅숏 페이지에서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="5f9bf-108">(백업 정책이 사용 되는 tooconfigure 백업 일정 및 백업 보존 볼륨의 컬렉션에 대 한 않습니다.) 백업 정책을 사용 하면 여러 볼륨의 스냅숏을 tootake 동시에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="5f9bf-109">이 백업 정책에 의해 생성 된 hello 백업을 크래시 일관성이 있는 복사본 된다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="5f9bf-110">이 페이지는 hello 백업 정책, 유형, 연결 된 hello 볼륨, 보존 된 백업 hello 수를 나열 하 고 이러한 정책을 옵션 tooenable hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="5f9bf-111">hello **백업 정책** 페이지도 있습니다 toofilter hello 기존 백업 정책을 하나 이상의 필드를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="5f9bf-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="5f9bf-112">**정책 이름** – hello hello 정책과 연결 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="5f9bf-113">hello 여러 가지 유형의 정책 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="5f9bf-114">예약 된 정책을 hello 사용자가 명시적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="5f9bf-115">볼륨 만들기의 hello 시간에서이 볼륨 옵션에 대 한 기본 백업 hello를 설정할 때 만들어지는 자동 정책.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="5f9bf-116">이러한 정책은 VolumeName_Default 볼륨 이름을 hello hello Azure 클래식 포털에서에서 hello 사용자가 구성 된 StorSimple 볼륨의 toohello 이름 여기서은 참조로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="5f9bf-117">hello 자동 정책 22 시 30 장치 시간부터 시작 하는 일별 클라우드 스냅숏이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="5f9bf-118">StorSimple 스냅숏 관리자 hello에서 원래 만든 하는 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5f9bf-119">이러한 hello 정책에서 가져온 hello StorSimple 스냅숏 관리자 호스트를 설명 하는 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="5f9bf-120">**볼륨** – hello hello 정책과 연결 된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="5f9bf-121">백업 정책과 연관 된 모든 hello 볼륨은 백업을 만들 때 함께 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="5f9bf-122">**마지막으로 성공한 백업** – hello 날짜 및 시간 hello 마지막으로 성공한 백업에이 정책을 사용 하 여 만든입니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="5f9bf-123">**다음 백업** – hello의 날짜 및 시간 hello 예약 된 다음 백업이이 정책에 의해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="5f9bf-124">**일정** – hello hello 백업 정책과 연관 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="5f9bf-125">이 페이지에서 수행할 수 있는 hello 자주 사용 되는 연산은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="5f9bf-126">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="5f9bf-126">Add a backup policy</span></span> 
* <span data-ttu-id="5f9bf-127">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="5f9bf-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="5f9bf-128">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="5f9bf-128">Delete a backup policy</span></span> 
* <span data-ttu-id="5f9bf-129">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="5f9bf-129">Take a manual backup</span></span> 
* <span data-ttu-id="5f9bf-130">여러 볼륨과 일정의 사용자 지정 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="5f9bf-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="5f9bf-131">백업 정책 추가</span><span class="sxs-lookup"><span data-stu-id="5f9bf-131">Add a backup policy</span></span>
<span data-ttu-id="5f9bf-132">백업 정책 tooautomatically 일정 백업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="5f9bf-133">Azure 클래식 포털 tooadd StorSimple 장치에 대 한 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="5f9bf-134">Hello 정책에 추가한 후에 일정을 정의할 수 있습니다 (참조 [추가 일정을 수정 하거나](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="5f9bf-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="5f9bf-135">![동영상 사용 가능](./media/storsimple-manage-backup-policies/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="5f9bf-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="5f9bf-136">toowatch toocreate 로컬 또는 클라우드 백업 정책에 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="5f9bf-137">일정 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="5f9bf-137">Add or modify a schedule</span></span>
<span data-ttu-id="5f9bf-138">추가 하거나 StorSimple 장치에 연결 된 tooan 기존 백업 정책이 있는 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="5f9bf-139">Hello hello Azure 클래식 포털 tooadd의에서 단계를 실행 하거나 일정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="5f9bf-140">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="5f9bf-140">Delete a backup policy</span></span>
<span data-ttu-id="5f9bf-141">StorSimple 장치에서 Azure 클래식 포털 toodelete 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="5f9bf-142">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="5f9bf-142">Take a manual backup</span></span>
<span data-ttu-id="5f9bf-143">단일 볼륨에 대 한 hello Azure 클래식 포털 toocreate 주문형 (수동) 백업 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="5f9bf-144">여러 볼륨과 일정의 사용자 지정 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="5f9bf-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="5f9bf-145">Hello hello Azure 클래식 포털 toocreate 여러 볼륨과 일정이 있는 사용자 지정 백업 정책에에서는 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="5f9bf-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f9bf-146">Next steps</span></span>
<span data-ttu-id="5f9bf-147">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f9bf-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

