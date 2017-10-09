---
title: "aaaClone StorSimple 볼륨 | Microsoft Docs"
description: "Hello 다른 복제 유형에 대해 설명 및 시기 toouse, 백업 세트 tooclone 개별 볼륨을 사용 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a><span data-ttu-id="4a0e0-103">Hello StorSimple 관리자 서비스 tooclone 볼륨을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4a0e0-103">Use hello StorSimple Manager service tooclone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="4a0e0-104">개요</span><span class="sxs-lookup"><span data-stu-id="4a0e0-104">Overview</span></span>
<span data-ttu-id="4a0e0-105">StorSimple Manager 서비스 hello **백업 카탈로그** 페이지 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="4a0e0-106">이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

![백업 카탈로그 페이지](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="4a0e0-108">이 자습서에서는 백업 세트 tooclone 개별 볼륨을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-108">This tutorial describes how you can use a backup set tooclone an individual volume.</span></span> <span data-ttu-id="4a0e0-109">Hello 차이점에 대해서도 설명 *일시적인* 및 *영구* 를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-109">It also explains hello difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="4a0e0-110">볼륨의 클론 만들기</span><span class="sxs-lookup"><span data-stu-id="4a0e0-110">Create a clone of a volume</span></span>
<span data-ttu-id="4a0e0-111">Hello에 복제본을 만들 수 있습니다 동일한 장치나 다른 장치는 로컬 또는 클라우드 스냅숏을 사용 하 여 가상 컴퓨터도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-111">You can create a clone on hello same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="4a0e0-112">tooclone 볼륨</span><span class="sxs-lookup"><span data-stu-id="4a0e0-112">tooclone a volume</span></span>
1. <span data-ttu-id="4a0e0-113">Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 하 고 백업 세트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-113">On hello StorSimple Manager service page, click hello **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="4a0e0-114">Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-114">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="4a0e0-115">클릭 하 고 hello 백업 세트에서 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-115">Click and select a volume from hello backup set.</span></span>
   
     ![볼륨 복제](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="4a0e0-117">클릭 **복제** toobegin hello 선택한 볼륨의 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-117">Click **Clone** toobegin cloning hello selected volume.</span></span>
4. <span data-ttu-id="4a0e0-118">Hello 복제 볼륨 마법사에서 아래 **이름 및 위치 지정**:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-118">In hello Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="4a0e0-119">대상 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-119">Identify a target device.</span></span> <span data-ttu-id="4a0e0-120">Hello 위치 hello 복제를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-120">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="4a0e0-121">같은 장치 hello 하거나 다른 장치를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-121">You can choose hello same device or specify another device.</span></span> <span data-ttu-id="4a0e0-122">다른 클라우드 서비스 공급자와 연결 된 볼륨을 선택 하는 경우 (하지 Azure), hello 드롭 다운 목록에 hello 대상 장치는 물리적 장치에만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-122">If you choose a volume associated with other cloud service providers (not Azure), hello drop-down list for hello target device will only show physical devices.</span></span> <span data-ttu-id="4a0e0-123">가상 장치에 다른 클라우드 서비스 공급자와 연결된 볼륨을 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="4a0e0-124">Hello 복제에 필요한 hello 용량 hello 대상 장치에서 사용 가능한 hello 용량 보다 낮은 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-124">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="4a0e0-125">해당 클론에 대한 고유 볼륨 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="4a0e0-126">hello 이름은 3 ~ 127 자 사이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-126">hello name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="4a0e0-127">Hello 화살표 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-127">Click hello arrow icon</span></span> ![화살표 아이콘](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="4a0e0-129">tooproceed toohello 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-129">tooproceed toohello next page.</span></span>
5. <span data-ttu-id="4a0e0-130">**이 볼륨을 사용할 수 있는 호스트 지정**아래:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="4a0e0-131">Hello 복제에 대 한 액세스 제어 레코드 (ACR)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-131">Specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="4a0e0-132">새 ACR을 추가 하거나 hello 기존 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-132">You can add a new ACR or choose from hello existing list.</span></span>
   2. <span data-ttu-id="4a0e0-133">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-133">Click hello check icon</span></span> ![check-icon](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="4a0e0-135">toocomplete hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-135">toocomplete hello operation.</span></span>
6. <span data-ttu-id="4a0e0-136">복제 작업 시작 및 알려 hello 복제 성공적으로 만들어지면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-136">A clone job will be initiated and you will be notified when hello clone is successfully created.</span></span> <span data-ttu-id="4a0e0-137">클릭 **작업 보기** hello에 toomonitor hello 복제 작업 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-137">Click **View Job** toomonitor hello clone job on hello **Jobs** page.</span></span>
7. <span data-ttu-id="4a0e0-138">Hello 후 복제 작업이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-138">After hello clone job is completed:</span></span>
   
   1. <span data-ttu-id="4a0e0-139">Toohello 이동 **장치** 페이지 및 선택 hello **볼륨 컨테이너** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-139">Go toohello **Devices** page, and select hello **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="4a0e0-140">연결 된 복제 hello 원본 볼륨 hello 볼륨 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-140">Select hello volume container that is associated with hello source volume that you cloned.</span></span> <span data-ttu-id="4a0e0-141">볼륨의 hello 목록에서 방금 만든 hello 복제를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-141">In hello list of volumes, you should see hello clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0e0-142">모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="4a0e0-143">이러한 방식으로 만들어진 클론은 임시 클론입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="4a0e0-144">복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="4a0e0-145">이 복제본은 이제 정규 볼륨이 및 볼륨에서 사용할 수 있는 모든 작업 hello 복제에 사용할 수 있는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for hello clone.</span></span> <span data-ttu-id="4a0e0-146">모든 백업에 대 한이 볼륨 tooconfigure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-146">You will need tooconfigure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="4a0e0-147">임시 및 영구 복제본 비교</span><span class="sxs-lookup"><span data-stu-id="4a0e0-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="4a0e0-148">임시 복제본과 영구 복제본 tooa 다른 장치에 복제 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-148">Transient and permanent clones are created only when you are cloning on tooa different device.</span></span> <span data-ttu-id="4a0e0-149">백업 세트 tooa 다른 장치에서 특정 볼륨을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-149">You can clone a specific volume from a backup set tooa different device.</span></span> <span data-ttu-id="4a0e0-150">이러한 방식으로 만들어진 복제본은 *임시* 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="4a0e0-151">hello 임시 복제본 되 고 참조 toohello 원래 볼륨 없게 로컬로 쓰는 동안 해당 볼륨 tooread를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-151">hello transient clone will have references toohello original volume and will use that volume tooread while writing locally.</span></span> 

<span data-ttu-id="4a0e0-152">임시 복제본의 클라우드 스냅숏을 수행한 후 생성 되는 복제본 hello 됩니다는 *영구* 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-152">After you take a cloud snapshot of a transient clone, hello resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="4a0e0-153">hello 영구 복제본 독립적 이며에서 복제 된 모든 참조가 toohello 원래 볼륨 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-153">hello permanent clone is independent and doesn’t have any references toohello original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="4a0e0-154">임시 및 영구 클론에 대한 시나리오</span><span class="sxs-lookup"><span data-stu-id="4a0e0-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="4a0e0-155">hello 다음 섹션에서는 임시 복제본과 영구 복제본을 사용할 수 있는 예제 상황을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-155">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="4a0e0-156">임시 클론을 사용하여 항목 수준 복구</span><span class="sxs-lookup"><span data-stu-id="4a0e0-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="4a0e0-157">1 년 전에 Microsoft PowerPoint 프레젠테이션 파일 toorecover가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-157">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="4a0e0-158">IT 관리자는 해당 기간의 특정 백업을 hello를 식별 하 고 필터 hello 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-158">Your IT administrator identifies hello specific backup from that time frame, and then filters hello volume.</span></span> <span data-ttu-id="4a0e0-159">관리자에 게 다음에서 hello 볼륨 복제, hello 파일을 찾고, 찾아 tooyou를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-159">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="4a0e0-160">이 시나리오에서는 임시 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="4a0e0-161">![동영상 사용 가능](./media/storsimple-clone-volume/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="4a0e0-162">toowatch hello 복제를 사용 하 여 StorSimple 삭제 toorecover 파일의 기능을 복원 하는 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-162">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="4a0e0-163">영구 복제본을 사용 하는 hello 프로덕션 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="4a0e0-163">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="4a0e0-164">Tooverify hello 프로덕션 환경에서 테스트 버그를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-164">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="4a0e0-165">이 복제본의 클라우드 스냅숏을 만드는 것으로 hello 프로덕션 환경에서 hello 볼륨의 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-165">You create a clone of hello volume in hello production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="4a0e0-166">hello 복제 된 볼륨은 독립적인 볼륨이 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-166">hello cloned volume is now independent.</span></span> <span data-ttu-id="4a0e0-167">이 시나리오에서는 영구 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a0e0-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a0e0-168">Next steps</span></span>
* <span data-ttu-id="4a0e0-169">너무 방법에 대해 알아봅니다[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-169">Learn how too[restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="4a0e0-170">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-170">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

