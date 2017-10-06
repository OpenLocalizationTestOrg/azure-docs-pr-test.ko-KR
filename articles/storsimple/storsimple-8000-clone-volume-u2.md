---
title: "StorSimple 8000 시리즈에 있는 볼륨 aaaClone | Microsoft Docs"
description: "Hello 다른 복제 유형 및 사용법에 설명 하 고 StorSimple 8000 시리즈 장치에 백업 세트 tooclone 개별 볼륨을 사용 하는 방법을 설명 합니다."
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a><span data-ttu-id="01bb8-103">Hello StorSimple 장치 관리자 서비스를 사용 하 여 Azure 포털 tooclone 볼륨에</span><span class="sxs-lookup"><span data-stu-id="01bb8-103">Use hello StorSimple Device Manager service in Azure portal tooclone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="01bb8-104">개요</span><span class="sxs-lookup"><span data-stu-id="01bb8-104">Overview</span></span>

<span data-ttu-id="01bb8-105">이 자습서에서는 백업 세트 tooclone hello 통해 개별 볼륨을 사용 하는 방법을 설명 **백업 카탈로그** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-105">This tutorial describes how you can use a backup set tooclone an individual volume via hello **Backup catalog** blade.</span></span> <span data-ttu-id="01bb8-106">Hello 차이점에 대해서도 설명 *일시적인* 및 *영구* 를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-106">It also explains hello difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="01bb8-107">이 자습서의 지침에 hello tooall hello StorSimple 8000 시리즈 장치를 업데이트 3 이상을 실행 하 고 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-107">hello guidance in this tutorial applies tooall hello StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="01bb8-108">StorSimple 장치 관리자 서비스 hello **백업 카탈로그** 블레이드 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-108">hello StorSimple Device Manager service **Backup catalog** blade displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="01bb8-109">그런 다음 백업 세트 tooclone에서 볼륨을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-109">You can then select a volume in a backup set tooclone.</span></span>

 ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="01bb8-111">볼륨 복제 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="01bb8-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="01bb8-112">Hello 볼륨을 복제할 때는 다음 정보를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-112">Consider hello following information when cloning a volume.</span></span>

- <span data-ttu-id="01bb8-113">복제본을 동일 하 게 작동 hello에 정규 볼륨이 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-113">A clone behaves in hello same way as a regular volume.</span></span> <span data-ttu-id="01bb8-114">Hello 복제에 대 한 볼륨에서 사용할 수 있는 모든 작업 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="01bb8-114">Any operation that is possible on a volume is available for hello clone.</span></span>

- <span data-ttu-id="01bb8-115">모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="01bb8-116">모든 백업 tooconfigure 복제본된 볼륨에서는 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-116">You would need tooconfigure a cloned volume for any backups.</span></span>

- <span data-ttu-id="01bb8-117">로컬 고정 볼륨은 계층화된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="01bb8-118">로컬로 고정 된 복제 볼륨 toobe hello 필요, hello 복제 작업이 성공적으로 완료 된 후 로컬로 고정 tooa 볼륨을 복제 하는 hello를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-118">If you need hello cloned volume toobe locally pinned, you can convert hello clone tooa locally pinned volume after hello clone operation is successfully completed.</span></span> <span data-ttu-id="01bb8-119">로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-119">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="01bb8-120">Tooconvert 계층화 된 toolocally에서 복제 볼륨 (것은 임시 복제본 여전히) 하는 경우를 복제 한 후 즉시 고정을 시도 하면 다음과 같은 오류 메시지가 hello로 hello 변환에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-120">If you try tooconvert a cloned volume from tiered toolocally pinned immediately after cloning (when it is still a transient clone), hello conversion fails with hello following error message:</span></span>

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    <span data-ttu-id="01bb8-121">Tooa 다른 장치에 복제 하는 경우에이 오류가 수신 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-121">This error is received only if you are cloning on tooa different device.</span></span> <span data-ttu-id="01bb8-122">먼저 hello 임시 복제본 tooa 영구 복제본을 변환 하는 경우 고정 된 hello 볼륨 toolocally 성공적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-122">You can successfully convert hello volume toolocally pinned if you first convert hello transient clone tooa permanent clone.</span></span> <span data-ttu-id="01bb8-123">Hello 임시 복제본 tooconvert의 클라우드 스냅숏을 것 tooa 영구 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-123">Take a cloud snapshot of hello transient clone tooconvert it tooa permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="01bb8-124">볼륨의 클론 만들기</span><span class="sxs-lookup"><span data-stu-id="01bb8-124">Create a clone of a volume</span></span>

<span data-ttu-id="01bb8-125">복제본을 만들 수 있습니다에 로컬을 사용 하 여 동일한 장치나 다른 장치 클라우드 어플라이언스에 hello 또는 클라우드 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-125">You can create a clone on hello same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="01bb8-126">아래 hello 절차 toocreate hello에서 복제본을 카탈로그를 백업 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-126">hello procedure below describes how toocreate a clone from hello backup catalog.</span></span>  <span data-ttu-id="01bb8-127">대체 방법 tooinitiate 복제본이 toogo 너무**볼륨**, 볼륨을 선택 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 선택 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-127">An alternative method tooinitiate clone is toogo too**Volumes**, select a volume, then right-click tooinvoke hello context menu and select **Clone**.</span></span>

<span data-ttu-id="01bb8-128">Hello 단계 toocreate 볼륨의 복제본을 hello 백업 카탈로그에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-128">Perform hello following steps toocreate a clone of your volume from hello backup catalog.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="01bb8-129">tooclone 볼륨</span><span class="sxs-lookup"><span data-stu-id="01bb8-129">tooclone a volume</span></span>

1. <span data-ttu-id="01bb8-130">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-130">Go tooyour StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="01bb8-131">백업 세트를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="01bb8-132">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-132">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="01bb8-133">Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-133">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="01bb8-134">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-134">Specify hello time range.</span></span>
   4. <span data-ttu-id="01bb8-135">클릭 **적용** tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-135">Click **Apply** tooexecute this query.</span></span>

    <span data-ttu-id="01bb8-136">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-136">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
   
    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="01bb8-138">Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-138">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="01bb8-139">이러한 볼륨을 복구 하기 전에 hello 호스트와 장치에서 오프 라인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-139">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="01bb8-140">Hello에 hello 볼륨을 액세스할 **볼륨** 단계 장치 및 다음에 따라 hello 블레이드 [볼륨을 오프 라인](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake를 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-140">Access hello volumes on hello **Volumes** blade of your device, and then follow hello steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="01bb8-141">수행 하 여 hello 호스트의 hello 볼륨을 오프 라인으로 먼저 hello 장치에서 hello 볼륨을 오프 라인으로 수행 하기 전에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-141">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="01bb8-142">Hello 호스트에서 오프 라인으로 hello 볼륨을 사용 하지 않는 경우 toodata 손상이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-142">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   
4. <span data-ttu-id="01bb8-143">뒤로 toohello 이동 **백업 카탈로그** 후 백업 세트의 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-143">Navigate back toohello **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="01bb8-144">마우스 오른쪽 단추로 클릭 한 다음 hello 상황에 맞는 메뉴에서 선택 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-144">Right-click and then from hello context menu, select **Clone**.</span></span>

   ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="01bb8-146">Hello에 **복제** 블레이드에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-146">In hello **Clone** blade, do hello following steps:</span></span>
   
    1. <span data-ttu-id="01bb8-147">대상 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-147">Identify a target device.</span></span> <span data-ttu-id="01bb8-148">Hello 위치 hello 복제를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-148">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="01bb8-149">같은 장치 hello 하거나 다른 장치를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-149">You can choose hello same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="01bb8-150">Hello 복제에 필요한 hello 용량 hello 대상 장치에서 사용 가능한 hello 용량 보다 낮은 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-150">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
       
    2. <span data-ttu-id="01bb8-151">해당 클론에 대한 고유 볼륨 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="01bb8-152">hello 이름은 3 ~ 127 자 사이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-152">hello name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="01bb8-153">hello **복제본 볼륨으로** 필드가 **계층화 됨** 로컬로 고정 된 볼륨을 복제 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-153">hello **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="01bb8-154">이 설정을 변경할 수 없습니다. 그러나 복제 된 볼륨 toobe 로컬로 고정 hello 필요, hello 복제본을 성공적으로 만들면 hello tooa 로컬로 고정 볼륨 복제 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-154">You cannot change this setting; however, if you need hello cloned volume toobe locally pinned as well, you can convert hello clone tooa locally pinned volume after you successfully create hello clone.</span></span> <span data-ttu-id="01bb8-155">로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-155">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="01bb8-156">아래 **호스트 연결**, hello 복제에 대 한 액세스 제어 레코드 (ACR)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-156">Under **Connected hosts**, specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="01bb8-157">새 ACR을 추가 하거나 hello 기존 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-157">You can add a new ACR or choose from hello existing list.</span></span> <span data-ttu-id="01bb8-158">ACR hello이이 복제본에 액세스할 수 있는 호스트를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-158">hello ACR will determine which hosts can access this clone.</span></span>
      
        ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="01bb8-160">클릭 **복제** toocomplete hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-160">Click **Clone** toocomplete hello operation.</span></span>

4. <span data-ttu-id="01bb8-161">복제 작업이 시작 되 고 hello 복제 성공적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-161">A clone job is initiated and you are notified when hello clone is successfully created.</span></span> <span data-ttu-id="01bb8-162">너무 hello 작업 알림을 클릭 하거나**작업** 블레이드 toomonitor hello 복제 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-162">Click hello job notification or go too**Jobs** blade toomonitor hello clone job.</span></span>

    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="01bb8-164">Hello 복제 작업이 완료 되 면 tooyour 장치 이동한 다음 클릭 **볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-164">After hello clone job is complete, go tooyour device and then click **Volumes**.</span></span> <span data-ttu-id="01bb8-165">Hello 볼륨 목록에서 방금 만든 hello에 동일한 hello 복제를 확인 해야 hello 원본 볼륨이 있는 볼륨 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-165">In hello list of volumes, you should see hello clone that was just created in hello same volume container that has hello source volume.</span></span>

    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="01bb8-167">이러한 방식으로 만들어진 클론은 임시 클론입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="01bb8-168">복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01bb8-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="01bb8-169">임시 및 영구 복제본 비교</span><span class="sxs-lookup"><span data-stu-id="01bb8-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="01bb8-170">임시 복제본 tooanother 장치를 복제 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-170">Transient clones are created only when you clone tooanother device.</span></span> <span data-ttu-id="01bb8-171">Hello StorSimple 장치 관리자에서 관리 하는 백업 세트 tooa 다른 장치에서 특정 볼륨을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-171">You can clone a specific volume from a backup set tooa different device managed by hello StorSimple Device Manager.</span></span> <span data-ttu-id="01bb8-172">hello 임시 복제본 hello 원본 볼륨에 대 한 참조 toohello 데이터 고 hello 대상 장치에서 해당 데이터 tooread 및 쓰기를 로컬로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-172">hello transient clone has references toohello data in hello original volume and uses that data tooread and write locally on hello target device.</span></span>

<span data-ttu-id="01bb8-173">임시 복제본의 클라우드 스냅숏을 수행 하면 hello 결과 복제는 한 *영구* 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-173">After you take a cloud snapshot of a transient clone, hello resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="01bb8-174">이 과정에서 hello 데이터의 복사본에 hello 클라우드 및이 데이터는 hello 데이터의 hello 크기에 따라 결정 되는 시간 toocopy hello 만들어지고 hello Azure 대기 시간 (이것이 Azure-Azure 복사) 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-174">During this process, a copy of hello data is created on hello cloud and hello time toocopy this data is determined by hello size of hello data and hello Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="01bb8-175">일 tooweeks를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-175">This process can take days tooweeks.</span></span> <span data-ttu-id="01bb8-176">임시 복제본 hello 영구 복제본 되며 참조 toohello 원래 볼륨 데이터가 없는에서 복제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-176">hello transient clone becomes a permanent clone and doesn’t have any references toohello original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="01bb8-177">임시 및 영구 클론에 대한 시나리오</span><span class="sxs-lookup"><span data-stu-id="01bb8-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="01bb8-178">hello 다음 섹션에서는 임시 복제본과 영구 복제본을 사용할 수 있는 예제 상황을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-178">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="01bb8-179">임시 클론을 사용하여 항목 수준 복구</span><span class="sxs-lookup"><span data-stu-id="01bb8-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="01bb8-180">1 년 전에 Microsoft PowerPoint 프레젠테이션 파일 toorecover가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-180">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="01bb8-181">IT 관리자가 시간에서 특정 백업을 hello를 식별 하 고 필터 hello 볼륨.</span><span class="sxs-lookup"><span data-stu-id="01bb8-181">Your IT administrator identifies hello specific backup from that time, and then filters hello volume.</span></span> <span data-ttu-id="01bb8-182">관리자에 게 다음에서 hello 볼륨 복제, hello 파일을 찾고, 찾아 tooyou를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-182">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="01bb8-183">이 시나리오에서는 임시 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="01bb8-184">영구 복제본을 사용 하는 hello 프로덕션 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="01bb8-184">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="01bb8-185">Tooverify hello 프로덕션 환경에서 테스트 버그를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-185">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="01bb8-186">Hello 프로덕션 환경에서 hello 볼륨의 복제본을 만들고이 복제 toocreate는 독립적인 복제 볼륨의 클라우드 스냅숏을 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-186">You create a clone of hello volume in hello production environment and then take a cloud snapshot of this clone toocreate an independent cloned volume.</span></span> <span data-ttu-id="01bb8-187">이 시나리오에서는 영구 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01bb8-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01bb8-188">Next steps</span></span>
* <span data-ttu-id="01bb8-189">너무 방법에 대해 알아봅니다[백업 세트에서 StorSimple 볼륨을 복원](storsimple-8000-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-189">Learn how too[restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="01bb8-190">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb8-190">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

