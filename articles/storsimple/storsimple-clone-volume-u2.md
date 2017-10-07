---
title: "StorSimple 8000 시리즈 볼륨 aaaClone | Microsoft Docs"
description: "Hello 다른 복제 유형에 대해 설명 및 시기 toouse, 백업 세트 tooclone 개별 볼륨을 사용 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a><span data-ttu-id="34f66-103">Hello StorSimple 관리자 서비스 tooclone (업데이트 2) 볼륨을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="34f66-103">Use hello StorSimple Manager service tooclone a volume (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="34f66-104">개요</span><span class="sxs-lookup"><span data-stu-id="34f66-104">Overview</span></span>
<span data-ttu-id="34f66-105">StorSimple Manager 서비스 hello **백업 카탈로그** 페이지 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="34f66-106">이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

![백업 카탈로그 페이지](./media/storsimple-clone-volume-u2/backupCatalog.png)  

<span data-ttu-id="34f66-108">이 자습서에서는 백업 세트 tooclone 개별 볼륨을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-108">This tutorial describes how you can use a backup set tooclone an individual volume.</span></span> <span data-ttu-id="34f66-109">Hello 차이점에 대해서도 설명 *일시적인* 및 *영구* 를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-109">It also explains hello difference between *transient* and *permanent* clones.</span></span>

> [!NOTE]
> <span data-ttu-id="34f66-110">로컬로 고정된 볼륨은 계층화된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-110">A locally pinned volume will be cloned as a tiered volume.</span></span> <span data-ttu-id="34f66-111">로컬로 고정 된 복제 볼륨 toobe hello 필요, hello 복제 작업이 성공적으로 완료 된 후 로컬로 고정 tooa 볼륨을 복제 하는 hello를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-111">If you need hello cloned volume toobe locally pinned, you can convert hello clone tooa locally pinned volume after hello clone operation is successfully completed.</span></span> <span data-ttu-id="34f66-112">로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-manage-volumes-u2.md#change-the-volume-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-112">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
> 
> <span data-ttu-id="34f66-113">Tooconvert 계층화 된 toolocally에서 복제 볼륨 (것은 임시 복제본 여전히) 하는 경우를 복제 한 후 즉시 고정을 시도 하면 다음과 같은 오류 메시지가 hello hello 변환이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-113">If you try tooconvert a cloned volume from tiered toolocally pinned immediately after cloning (when it is still a transient clone), hello conversion will fail with hello following error message:</span></span>
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> <span data-ttu-id="34f66-114">Tooa 다른 장치에 복제 하는 경우에이 오류가 수신 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-114">This error is received only if you are cloning on tooa different device.</span></span> <span data-ttu-id="34f66-115">먼저 hello 임시 복제본 tooa 영구 복제본을 변환 하는 경우 고정 된 hello 볼륨 toolocally 성공적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-115">You can successfully convert hello volume toolocally pinned if you first convert hello transient clone tooa permanent clone.</span></span> <span data-ttu-id="34f66-116">영구 tooconvert hello 임시 복제본 tooa clone의 클라우드 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-116">tooconvert hello transient clone tooa permanent clone, take a cloud snapshot of it.</span></span>
> 
> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="34f66-117">볼륨의 클론 만들기</span><span class="sxs-lookup"><span data-stu-id="34f66-117">Create a clone of a volume</span></span>
<span data-ttu-id="34f66-118">복제본을 만들 수 있습니다에 동일한 장치나 다른 장치는 가상 컴퓨터는 로컬을 사용 하 여 hello 또는 클라우드 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-118">You can create a clone on hello same device, another device, or even a virtual machine by using a local or cloud snapshot.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="34f66-119">tooclone 볼륨</span><span class="sxs-lookup"><span data-stu-id="34f66-119">tooclone a volume</span></span>
1. <span data-ttu-id="34f66-120">Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 하 고 백업 세트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-120">On hello StorSimple Manager service page, click hello **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="34f66-121">Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-121">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="34f66-122">클릭 하 고 hello 백업 세트에서 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-122">Click and select a volume from hello backup set.</span></span>
   
     ![볼륨 복제](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. <span data-ttu-id="34f66-124">클릭 **복제** toobegin hello 선택한 볼륨의 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-124">Click **Clone** toobegin cloning hello selected volume.</span></span>
4. <span data-ttu-id="34f66-125">Hello 복제 볼륨 마법사에서 아래 **이름 및 위치 지정**:</span><span class="sxs-lookup"><span data-stu-id="34f66-125">In hello Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="34f66-126">대상 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-126">Identify a target device.</span></span> <span data-ttu-id="34f66-127">Hello 위치 hello 복제를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-127">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="34f66-128">같은 장치 hello 하거나 다른 장치를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-128">You can choose hello same device or specify another device.</span></span> <span data-ttu-id="34f66-129">다른 클라우드 서비스 공급자와 연결 된 볼륨을 선택 하는 경우 (하지 Azure), hello 드롭 다운 목록에 hello 대상 장치는 물리적 장치에만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-129">If you choose a volume associated with other cloud service providers (not Azure), hello drop-down list for hello target device will only show physical devices.</span></span> <span data-ttu-id="34f66-130">가상 장치에 다른 클라우드 서비스 공급자와 연결된 볼륨을 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-130">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="34f66-131">Hello 복제에 필요한 hello 용량 hello 대상 장치에서 사용 가능한 hello 용량 보다 낮은 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-131">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="34f66-132">해당 클론에 대한 고유 볼륨 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-132">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="34f66-133">hello 이름은 3 ~ 127 자 사이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-133">hello name must contain between 3 and 127 characters.</span></span> 
      
      > [!NOTE]
      > <span data-ttu-id="34f66-134">hello **복제본 볼륨으로** 필드가 **계층화 됨** 로컬로 고정 된 볼륨을 복제 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-134">hello **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="34f66-135">이 설정을 변경할 수 없습니다. 그러나 복제 된 볼륨 toobe 로컬로 고정 hello 필요, hello 복제본을 성공적으로 만들면 hello tooa 로컬로 고정 볼륨 복제 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-135">You cannot change this setting; however, if you need hello cloned volume toobe locally pinned as well, you can convert hello clone tooa locally pinned volume after you successfully create hello clone.</span></span> <span data-ttu-id="34f66-136">로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-manage-volumes-u2.md#change-the-volume-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-136">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
      > 
      > 
      
        ![복제 마법사 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. <span data-ttu-id="34f66-138">Hello 화살표 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-138">Click hello arrow icon</span></span> ![화살표 아이콘](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) <span data-ttu-id="34f66-140">tooproceed toohello 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-140">tooproceed toohello next page.</span></span>
5. <span data-ttu-id="34f66-141">**이 볼륨을 사용할 수 있는 호스트 지정**아래:</span><span class="sxs-lookup"><span data-stu-id="34f66-141">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="34f66-142">Hello 복제에 대 한 액세스 제어 레코드 (ACR)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-142">Specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="34f66-143">새 ACR을 추가 하거나 hello 기존 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-143">You can add a new ACR or choose from hello existing list.</span></span>
      
        ![복제 마법사 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. <span data-ttu-id="34f66-145">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-145">Click hello check icon</span></span> ![check-icon](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)<span data-ttu-id="34f66-147">toocomplete hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-147">toocomplete hello operation.</span></span>
6. <span data-ttu-id="34f66-148">복제 작업 시작 및 알려 hello 복제 성공적으로 만들어지면 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-148">A clone job will be initiated and you will be notified when hello clone is successfully created.</span></span> <span data-ttu-id="34f66-149">클릭 **작업 보기** hello에 toomonitor hello 복제 작업 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="34f66-149">Click **View Job** toomonitor hello clone job on hello **Jobs** page.</span></span> <span data-ttu-id="34f66-150">Hello hello 복제 작업이 완료 되 면 메시지의 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-150">You will see hello following message when hello clone job is finished:</span></span>
   
    ![클론 메시지](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. <span data-ttu-id="34f66-152">Hello 후 복제 작업이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-152">After hello clone job is completed:</span></span>
   
   1. <span data-ttu-id="34f66-153">Toohello 이동 **장치** 페이지 및 선택 hello **볼륨 컨테이너** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-153">Go toohello **Devices** page, and select hello **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="34f66-154">연결 된 복제 hello 원본 볼륨 hello 볼륨 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-154">Select hello volume container that is associated with hello source volume that you cloned.</span></span> <span data-ttu-id="34f66-155">볼륨의 hello 목록에서 방금 만든 hello 복제를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-155">In hello list of volumes, you should see hello clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="34f66-156">모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-156">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="34f66-157">이러한 방식으로 만들어진 클론은 임시 클론입니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-157">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="34f66-158">복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34f66-158">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="34f66-159">이 복제본은 이제 정규 볼륨이 및 볼륨에서 사용할 수 있는 모든 작업 hello 복제에 사용할 수 있는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-159">This clone is now a regular volume, and any operation that is possible on a volume will be available for hello clone.</span></span> <span data-ttu-id="34f66-160">모든 백업에 대 한이 볼륨 tooconfigure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-160">You will need tooconfigure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="34f66-161">임시 및 영구 복제본 비교</span><span class="sxs-lookup"><span data-stu-id="34f66-161">Transient vs. permanent clones</span></span>
<span data-ttu-id="34f66-162">임시 복제본 tooa 다른 장치를 복제 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-162">Transient clones are created only when you are cloning tooa different device.</span></span> <span data-ttu-id="34f66-163">Hello StorSimple Manager에서 관리 하는 백업 세트 tooa 다른 장치에서 특정 볼륨을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-163">You can clone a specific volume from a backup set tooa different device managed by hello StorSimple Manager.</span></span> <span data-ttu-id="34f66-164">hello 임시 복제본 hello 원본 볼륨에 대 한 참조 toohello 데이터가 있는 됩니다 하 고 해당 데이터 tooread 사용 하며 hello 대상 장치에서 로컬로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-164">hello transient clone will have references toohello data in hello original volume and will use that data tooread and write locally on hello target device.</span></span> 

<span data-ttu-id="34f66-165">임시 복제본의 클라우드 스냅숏을 수행한 후 생성 되는 복제본 hello 됩니다는 *영구* 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-165">After you take a cloud snapshot of a transient clone, hello resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="34f66-166">이 과정에서 hello 데이터의 복사본에 hello 클라우드 및이 데이터는 hello 데이터의 hello 크기에 따라 결정 되는 시간 toocopy hello 만들어지고 hello Azure 대기 시간 (이것이 Azure-Azure 복사) 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-166">During this process, a copy of hello data is created on hello cloud and hello time toocopy this data is determined by hello size of hello data and hello Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="34f66-167">일 tooweeks를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-167">This process can take days tooweeks.</span></span> <span data-ttu-id="34f66-168">hello 임시 복제본 영구 복제본이 방식이으로 되며 참조 toohello 원래 볼륨 데이터가 없는에서 복제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-168">hello transient clone becomes a permanent clone this way and doesn’t have any references toohello original volume data that it was cloned from.</span></span> 

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="34f66-169">임시 및 영구 클론에 대한 시나리오</span><span class="sxs-lookup"><span data-stu-id="34f66-169">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="34f66-170">hello 다음 섹션에서는 임시 복제본과 영구 복제본을 사용할 수 있는 예제 상황을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-170">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="34f66-171">임시 클론을 사용하여 항목 수준 복구</span><span class="sxs-lookup"><span data-stu-id="34f66-171">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="34f66-172">1 년 전에 Microsoft PowerPoint 프레젠테이션 파일 toorecover가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-172">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="34f66-173">IT 관리자는 해당 기간의 특정 백업을 hello를 식별 하 고 필터 hello 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-173">Your IT administrator identifies hello specific backup from that time frame, and then filters hello volume.</span></span> <span data-ttu-id="34f66-174">관리자에 게 다음에서 hello 볼륨 복제, hello 파일을 찾고, 찾아 tooyou를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-174">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="34f66-175">이 시나리오에서는 임시 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-175">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="34f66-176">![동영상 사용 가능](./media/storsimple-clone-volume-u2/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="34f66-176">![Video available](./media/storsimple-clone-volume-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="34f66-177">toowatch hello 복제를 사용 하 여 StorSimple 삭제 toorecover 파일의 기능을 복원 하는 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-177">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="34f66-178">영구 복제본을 사용 하는 hello 프로덕션 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="34f66-178">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="34f66-179">Tooverify hello 프로덕션 환경에서 테스트 버그를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-179">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="34f66-180">Hello 프로덕션 환경에서 hello 볼륨의 복제본을 만들고이 복제 toocreate는 독립적인 복제 볼륨의 클라우드 스냅숏을 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-180">You create a clone of hello volume in hello production environment and then take a cloud snapshot of this clone toocreate an independent cloned volume.</span></span> <span data-ttu-id="34f66-181">이 시나리오에서는 영구 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-181">In this scenario, a permanent clone is used.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="34f66-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34f66-182">Next steps</span></span>
* <span data-ttu-id="34f66-183">너무 방법에 대해 알아봅니다[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-183">Learn how too[restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="34f66-184">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f66-184">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

