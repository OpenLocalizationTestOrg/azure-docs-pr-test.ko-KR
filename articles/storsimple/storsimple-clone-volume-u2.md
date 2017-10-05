---
title: "StorSimple 8000 시리즈 볼륨 복제 | Microsoft Docs"
description: "다른 복제 유형 및 이를 사용하는 경우에 대해 설명하며, 백업 세트를 개별 볼륨 복제에 사용하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 2b627250df62bbe3299869ef3812947afbb8f29f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume-update-2"></a><span data-ttu-id="548ed-103">StorSimple 관리자 서비스를 사용하여 볼륨 복제(업데이트 2)</span><span class="sxs-lookup"><span data-stu-id="548ed-103">Use the StorSimple Manager service to clone a volume (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="548ed-104">개요</span><span class="sxs-lookup"><span data-stu-id="548ed-104">Overview</span></span>
<span data-ttu-id="548ed-105">StorSimple 관리자 서비스 **백업 카탈로그** 페이지는 수동 또는 자동화된 백업을 수행할 때 생성되는 모든 백업 세트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="548ed-106">이 페이지를 사용하여 백업 정책 또는 볼륨에 대한 모든 백업을 나열하거나, 백업을 선택 또는 삭제하거나 백업을 사용하여 볼륨을 복원 또는 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![백업 카탈로그 페이지](./media/storsimple-clone-volume-u2/backupCatalog.png)  

<span data-ttu-id="548ed-108">이 자습서에서는 개별 볼륨 복제에 백업 세트를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="548ed-109">*임시* 및 *영구* 복제의 차이점에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-109">It also explains the difference between *transient* and *permanent* clones.</span></span>

> [!NOTE]
> <span data-ttu-id="548ed-110">로컬로 고정된 볼륨은 계층화된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-110">A locally pinned volume will be cloned as a tiered volume.</span></span> <span data-ttu-id="548ed-111">복제된 볼륨을 로컬로 고정해야 하는 경우 복제 작업이 성공적으로 완료된 후 클론을 로컬로 고정된 볼륨으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-111">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="548ed-112">계층화된 볼륨을 로컬로 고정된 볼륨으로 변환하는 방법에 대한 자세한 내용은 [볼륨 유형 변경](storsimple-manage-volumes-u2.md#change-the-volume-type)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="548ed-112">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
> 
> <span data-ttu-id="548ed-113">복제 후(여전히 임시 클론일 경우) 즉시 복제된 볼륨을 계층화된 볼륨에서 로컬로 고정된 볼륨으로 변환시키려는 경우 다음 오류 메시지와 함께 변환이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-113">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion will fail with the following error message:</span></span>
> 
> `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.` 
> 
> <span data-ttu-id="548ed-114">다른 장치에 복제하는 경우 이 오류가 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-114">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="548ed-115">먼저 임시 클론을 영구 클론으로 변환시키면 성공적으로 볼륨을 로컬로 고정된 볼륨으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-115">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="548ed-116">임시 클론을 영구 클론으로 변환하려면 해당 클라우드 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-116">To convert the transient clone to a permanent clone, take a cloud snapshot of it.</span></span>
> 
> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="548ed-117">볼륨의 클론 만들기</span><span class="sxs-lookup"><span data-stu-id="548ed-117">Create a clone of a volume</span></span>
<span data-ttu-id="548ed-118">로컬 또는 클라우드 스냅숏을 사용하여 동일한 장치, 다른 장치 또는 가상 컴퓨터에 클론을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-118">You can create a clone on the same device, another device, or even a virtual machine by using a local or cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="548ed-119">볼륨 복제하기</span><span class="sxs-lookup"><span data-stu-id="548ed-119">To clone a volume</span></span>
1. <span data-ttu-id="548ed-120">StorSimple 관리자 서비스 페이지에서 **백업 카탈로그** 탭을 클릭하고 백접 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-120">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="548ed-121">백업 세트를 확장하여 연결된 볼륨을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-121">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="548ed-122">백업 세트에서 볼륨을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-122">Click and select a volume from the backup set.</span></span>
   
     ![볼륨 복제](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. <span data-ttu-id="548ed-124">**복제** 를 클릭하여 선택한 볼륨 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-124">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="548ed-125">볼륨 복제 마법사의 **이름 및 위치 지정**아래:</span><span class="sxs-lookup"><span data-stu-id="548ed-125">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="548ed-126">대상 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-126">Identify a target device.</span></span> <span data-ttu-id="548ed-127">클론이 만들어지는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-127">This is the location where the clone will be created.</span></span> <span data-ttu-id="548ed-128">동일한 장치를 선택하거나 다른 장치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-128">You can choose the same device or specify another device.</span></span> <span data-ttu-id="548ed-129">다른 클라우드 서비스 공급자와 연결 된 볼륨을 선택하는 경우 (Azure가 아님), 대상 장치에 대한 드롭다운 목록에는 물리적 장치만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-129">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="548ed-130">가상 장치에 다른 클라우드 서비스 공급자와 연결된 볼륨을 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-130">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="548ed-131">복제에 필요한 용량은 대상 장치에서 사용 가능한 용량보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-131">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="548ed-132">해당 클론에 대한 고유 볼륨 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-132">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="548ed-133">이름은 3자에서 127자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-133">The name must contain between 3 and 127 characters.</span></span> 
      
      > [!NOTE]
      > <span data-ttu-id="548ed-134">로컬로 고정된 볼륨을 복제하더라도 **다른 이름으로 볼륨 복제** 필드는 **계층화됨**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-134">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="548ed-135">이 설정을 변경할 수 없습니다. 그러나 로컬로 고정된 복제된 볼륨도 필요한 경우 복제본을 성공적으로 만든 후 로컬로 고정된 볼륨으로 복제본을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-135">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="548ed-136">계층화된 볼륨을 로컬로 고정된 볼륨으로 변환하는 방법에 대한 자세한 내용은 [볼륨 유형 변경](storsimple-manage-volumes-u2.md#change-the-volume-type)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="548ed-136">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
      > 
      > 
      
        ![복제 마법사 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. <span data-ttu-id="548ed-138">화살표 아이콘</span><span class="sxs-lookup"><span data-stu-id="548ed-138">Click the arrow icon</span></span> ![화살표 아이콘](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) <span data-ttu-id="548ed-140">을 클릭하여 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-140">to proceed to the next page.</span></span>
5. <span data-ttu-id="548ed-141">**이 볼륨을 사용할 수 있는 호스트 지정**아래:</span><span class="sxs-lookup"><span data-stu-id="548ed-141">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="548ed-142">클론에 대한 ACR(액세스 제어 레코드)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-142">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="548ed-143">새 ACR을 추가하거나 기존 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-143">You can add a new ACR or choose from the existing list.</span></span>
      
        ![복제 마법사 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. <span data-ttu-id="548ed-145">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="548ed-145">Click the check icon</span></span> ![check-icon](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)<span data-ttu-id="548ed-147">을 클릭하여 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-147">to complete the operation.</span></span>
6. <span data-ttu-id="548ed-148">클론 작업이 시작되며 클론이 성공적으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-148">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="548ed-149">**작업 보기**를 클릭하여 **작업** 페이지에서 복제 작업을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-149">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span> <span data-ttu-id="548ed-150">복제 작업이 완료되면 다음과 같은 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-150">You will see the following message when the clone job is finished:</span></span>
   
    ![클론 메시지](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. <span data-ttu-id="548ed-152">복제 작업 완료 후:</span><span class="sxs-lookup"><span data-stu-id="548ed-152">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="548ed-153">**장치** 페이지로 이동하여 **볼륨 컨테이너** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-153">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="548ed-154">복제한 원본 볼륨에 연관된 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-154">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="548ed-155">볼륨 목록에 방금 만든 클론이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-155">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="548ed-156">모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-156">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="548ed-157">이러한 방식으로 만들어진 클론은 임시 클론입니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-157">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="548ed-158">복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="548ed-158">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="548ed-159">이 클론은 이제 정규 볼륨이며 볼륨에 사용할 수 있는 모든 작업은 클론에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-159">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="548ed-160">백업에 대해 이 볼륨을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-160">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="548ed-161">임시 및 영구 복제본 비교</span><span class="sxs-lookup"><span data-stu-id="548ed-161">Transient vs. permanent clones</span></span>
<span data-ttu-id="548ed-162">임시 클론은 다른 장치에 복제하는 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-162">Transient clones are created only when you are cloning to a different device.</span></span> <span data-ttu-id="548ed-163">백업 세트에서 StorSimple Manager에서 관리되는 다른 장치에 특정 볼륨을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-163">You can clone a specific volume from a backup set to a different device managed by the StorSimple Manager.</span></span> <span data-ttu-id="548ed-164">임시 클론에는 원본 볼륨의 데이터에 대한 참조가 있으며 대상 장치에서 로컬로 읽고 쓰는 동안 해당 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-164">The transient clone will have references to the data in the original volume and will use that data to read and write locally on the target device.</span></span> 

<span data-ttu-id="548ed-165">임시 복제본의 클라우드 스냅숏을 수행한 후 결과 복제본은 *영구* 복제본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-165">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="548ed-166">이 과정에서 데이터 복사본이 클라우드에서 생성되고, 이 데이터를 복사하는 시간은 데이터의 크기 및 Azure 지연 시간에 따라 결정됩니다(Azure 간 복사).</span><span class="sxs-lookup"><span data-stu-id="548ed-166">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="548ed-167">이 프로세스는 며칠에서 몇 주까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-167">This process can take days to weeks.</span></span> <span data-ttu-id="548ed-168">임시 클론은 이러한 측면에서 영구 클론이 되며, 복제된 원본 볼륨 데이터에 대한 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-168">The transient clone becomes a permanent clone this way and doesn’t have any references to the original volume data that it was cloned from.</span></span> 

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="548ed-169">임시 및 영구 클론에 대한 시나리오</span><span class="sxs-lookup"><span data-stu-id="548ed-169">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="548ed-170">다음 섹션에서는 임시 및 영구 클론을 사용할 수 있는 예제 상황에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-170">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="548ed-171">임시 클론을 사용하여 항목 수준 복구</span><span class="sxs-lookup"><span data-stu-id="548ed-171">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="548ed-172">1년 된 Microsoft PowerPoint 프레젠테이션 파일을 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-172">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="548ed-173">IT 관리자는 해당 시간 프레임에서 특정 백업을 식별하고 볼륨을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-173">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="548ed-174">그런 다음 관리자는 해당 볼륨을 복제하고, 필요한 파일을 찾아 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-174">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="548ed-175">이 시나리오에서는 임시 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-175">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="548ed-176">![동영상 사용 가능](./media/storsimple-clone-volume-u2/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="548ed-176">![Video available](./media/storsimple-clone-volume-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="548ed-177">StorSimple에서 복제 및 복원 기능을 사용하여 삭제된 파일을 복구하는 방법을 보여 주는 동영상을 시청하려면 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="548ed-177">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="548ed-178">영구 클론을 사용하여 프로덕션 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="548ed-178">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="548ed-179">프로덕션 환경에서 테스트 버그를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-179">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="548ed-180">프로덕션 환경에서 볼륨의 클론을 만들고 이 클론의 클라우드 스냅숏을 만들어서 독립적으로 복제된 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-180">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="548ed-181">이 시나리오에서는 영구 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-181">In this scenario, a permanent clone is used.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="548ed-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="548ed-182">Next steps</span></span>
* <span data-ttu-id="548ed-183">[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set-u2.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-183">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="548ed-184">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="548ed-184">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

