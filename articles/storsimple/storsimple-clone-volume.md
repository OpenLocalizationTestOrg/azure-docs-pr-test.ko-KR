---
title: "StorSimple 볼륨 복제 | Microsoft Docs"
description: "다른 복제 유형 및 이를 사용하는 경우에 대해 설명하며, 백업 세트를 개별 볼륨 복제에 사용하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 8f1936fac543f559a44ad0f9c35b30d1a92dce68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a><span data-ttu-id="618a2-103">StorSimple 관리자 서비스를 사용하여 볼륨 복제</span><span class="sxs-lookup"><span data-stu-id="618a2-103">Use the StorSimple Manager service to clone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="618a2-104">개요</span><span class="sxs-lookup"><span data-stu-id="618a2-104">Overview</span></span>
<span data-ttu-id="618a2-105">StorSimple 관리자 서비스 **백업 카탈로그** 페이지는 수동 또는 자동화된 백업을 수행할 때 생성되는 모든 백업 세트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="618a2-106">이 페이지를 사용하여 백업 정책 또는 볼륨에 대한 모든 백업을 나열하거나, 백업을 선택 또는 삭제하거나 백업을 사용하여 볼륨을 복원 또는 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![백업 카탈로그 페이지](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="618a2-108">이 자습서에서는 개별 볼륨 복제에 백업 세트를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="618a2-109">*임시* 및 *영구* 복제의 차이점에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-109">It also explains the difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="618a2-110">볼륨의 클론 만들기</span><span class="sxs-lookup"><span data-stu-id="618a2-110">Create a clone of a volume</span></span>
<span data-ttu-id="618a2-111">로컬 또는 클라우드 스냅숏을 사용하여 동일한 장치, 다른 장치 또는 가상 컴퓨터에 클론을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="618a2-112">볼륨 복제하기</span><span class="sxs-lookup"><span data-stu-id="618a2-112">To clone a volume</span></span>
1. <span data-ttu-id="618a2-113">StorSimple 관리자 서비스 페이지에서 **백업 카탈로그** 탭을 클릭하고 백접 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="618a2-114">백업 세트를 확장하여 연결된 볼륨을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-114">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="618a2-115">백업 세트에서 볼륨을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-115">Click and select a volume from the backup set.</span></span>
   
     ![볼륨 복제](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="618a2-117">**복제** 를 클릭하여 선택한 볼륨 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-117">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="618a2-118">볼륨 복제 마법사의 **이름 및 위치 지정**아래:</span><span class="sxs-lookup"><span data-stu-id="618a2-118">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="618a2-119">대상 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-119">Identify a target device.</span></span> <span data-ttu-id="618a2-120">클론이 만들어지는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-120">This is the location where the clone will be created.</span></span> <span data-ttu-id="618a2-121">동일한 장치를 선택하거나 다른 장치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-121">You can choose the same device or specify another device.</span></span> <span data-ttu-id="618a2-122">다른 클라우드 서비스 공급자와 연결 된 볼륨을 선택하는 경우 (Azure가 아님), 대상 장치에 대한 드롭다운 목록에는 물리적 장치만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="618a2-123">가상 장치에 다른 클라우드 서비스 공급자와 연결된 볼륨을 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="618a2-124">복제에 필요한 용량은 대상 장치에서 사용 가능한 용량보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="618a2-125">해당 클론에 대한 고유 볼륨 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="618a2-126">이름은 3자에서 127자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-126">The name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="618a2-127">화살표 아이콘 </span><span class="sxs-lookup"><span data-stu-id="618a2-127">Click the arrow icon</span></span> ![화살표 아이콘](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="618a2-129">을 클릭하여 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-129">to proceed to the next page.</span></span>
5. <span data-ttu-id="618a2-130">**이 볼륨을 사용할 수 있는 호스트 지정**아래:</span><span class="sxs-lookup"><span data-stu-id="618a2-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="618a2-131">클론에 대한 ACR(액세스 제어 레코드)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-131">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="618a2-132">새 ACR을 추가하거나 기존 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-132">You can add a new ACR or choose from the existing list.</span></span>
   2. <span data-ttu-id="618a2-133">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="618a2-133">Click the check icon</span></span> ![check-icon](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="618a2-135">을 클릭하여 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-135">to complete the operation.</span></span>
6. <span data-ttu-id="618a2-136">클론 작업이 시작되며 클론이 성공적으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="618a2-137">**작업 보기**를 클릭하여 **작업** 페이지에서 복제 작업을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span>
7. <span data-ttu-id="618a2-138">복제 작업 완료 후:</span><span class="sxs-lookup"><span data-stu-id="618a2-138">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="618a2-139">**장치** 페이지로 이동하여 **볼륨 컨테이너** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="618a2-140">복제한 원본 볼륨에 연관된 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-140">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="618a2-141">볼륨 목록에 방금 만든 클론이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-141">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="618a2-142">모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="618a2-143">이러한 방식으로 만들어진 클론은 임시 클론입니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="618a2-144">복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="618a2-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="618a2-145">이 클론은 이제 정규 볼륨이며 볼륨에 사용할 수 있는 모든 작업은 클론에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="618a2-146">백업에 대해 이 볼륨을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-146">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="618a2-147">임시 및 영구 복제본 비교</span><span class="sxs-lookup"><span data-stu-id="618a2-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="618a2-148">임시 및 영구 클론은 다른 장치에 복제하는 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-148">Transient and permanent clones are created only when you are cloning on to a different device.</span></span> <span data-ttu-id="618a2-149">백업 세트에서 다른 장치에 특정 볼륨을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-149">You can clone a specific volume from a backup set to a different device.</span></span> <span data-ttu-id="618a2-150">이러한 방식으로 만들어진 복제본은 *임시* 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="618a2-151">임시 클론에는 원본 볼륨에 대한 참조가 있으며 로컬로 쓰는 동안 읽기위해 해당 볼륨을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span></span> 

<span data-ttu-id="618a2-152">임시 복제본의 클라우드 스냅숏을 수행한 후 결과 복제본은 *영구* 복제본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="618a2-153">영구 클론은 독립적이며 복제된 원본 볼륨에 대한 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="618a2-154">임시 및 영구 클론에 대한 시나리오</span><span class="sxs-lookup"><span data-stu-id="618a2-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="618a2-155">다음 섹션에서는 임시 및 영구 클론을 사용할 수 있는 예제 상황에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-155">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="618a2-156">임시 클론을 사용하여 항목 수준 복구</span><span class="sxs-lookup"><span data-stu-id="618a2-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="618a2-157">1년 된 Microsoft PowerPoint 프레젠테이션 파일을 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="618a2-158">IT 관리자는 해당 시간 프레임에서 특정 백업을 식별하고 볼륨을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="618a2-159">그런 다음 관리자는 해당 볼륨을 복제하고, 필요한 파일을 찾아 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="618a2-160">이 시나리오에서는 임시 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="618a2-161">![동영상 사용 가능](./media/storsimple-clone-volume/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="618a2-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="618a2-162">StorSimple에서 복제 및 복원 기능을 사용하여 삭제된 파일을 복구하는 방법을 보여 주는 동영상을 시청하려면 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="618a2-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="618a2-163">영구 클론을 사용하여 프로덕션 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="618a2-163">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="618a2-164">프로덕션 환경에서 테스트 버그를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-164">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="618a2-165">이 클론의 클라우드 스냅숏을 만들어 프로덕션 환경에서 볼륨의 클론을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="618a2-166">복제된 볼륨은 이제 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-166">The cloned volume is now independent.</span></span> <span data-ttu-id="618a2-167">이 시나리오에서는 영구 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="618a2-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="618a2-168">Next steps</span></span>
* <span data-ttu-id="618a2-169">[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="618a2-170">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="618a2-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

