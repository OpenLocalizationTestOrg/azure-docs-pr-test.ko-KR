---
title: "StorSimple 8000 시리즈의 백업에서 볼륨 복원 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 백업 카탈로그를 사용하여 백업 세트에서 StorSimple 볼륨을 복원하는 방법을 설명합니다."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: aff0710ead4f76bb80c38e2d88fe9cd3ce6a7b48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="2d350-103">백업 세트에서 StorSimple 볼륨 복원</span><span class="sxs-lookup"><span data-stu-id="2d350-103">Restore a StorSimple volume from a backup set</span></span>

## <a name="overview"></a><span data-ttu-id="2d350-104">개요</span><span class="sxs-lookup"><span data-stu-id="2d350-104">Overview</span></span>

<span data-ttu-id="2d350-105">이 자습서에서는 기존 백업 세트를 사용하여 StorSimple 8000 시리즈 장치에서 수행되는 복원 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-105">This tutorial describes the restore operation performed on a StorSimple 8000 series device using an existing backup set.</span></span> <span data-ttu-id="2d350-106">**백업 카탈로그** 블레이드를 사용하여 로컬 또는 클라우드 백업에서 볼륨을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-106">Use the **Backup catalog** blade to restore a volume from a local or cloud backup.</span></span> <span data-ttu-id="2d350-107">**백업 카탈로그** 블레이드에는 수동 또는 자동화된 백업을 수행할 때 만들어지는 모든 백업 세트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-107">The **Backup catalog** blade displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="2d350-108">백그라운드에서 데이터를 다운로드하는 동안 백업 세트의 복원 작업에서는 즉시 볼륨을 온라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-108">The restore operation from a backup set brings the volume online immediately while data is downloaded in the background.</span></span>

<span data-ttu-id="2d350-109">복원을 시작하는 다른 방법은 **장치 > [사용자 장치] > 볼륨**으로 이동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-109">An alternate method to start restore is to go to **Devices > [Your device] > Volumes**.</span></span> <span data-ttu-id="2d350-110">**볼륨** 블레이드에서 볼륨을 선택하고, 마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 호출하고, **복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-110">In the **Volumes** blade, select a volume, right-click to invoke the context menu, and then select **Restore**.</span></span>

## <a name="before-you-restore"></a><span data-ttu-id="2d350-111">복원하기 전에</span><span class="sxs-lookup"><span data-stu-id="2d350-111">Before you restore</span></span>

<span data-ttu-id="2d350-112">복원을 시작하기 전에 다음 주의 사항을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="2d350-112">Before you start a restore, review the following caveats:</span></span>

* <span data-ttu-id="2d350-113">**볼륨을 오프라인해야 합니다.** – 복원 작업을 시작하기 전에 호스트와 장치 모두에서 볼륨을 오프라인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-113">**You must take the volume offline** – Take the volume offline on both the host and the device before you initiate the restore operation.</span></span> <span data-ttu-id="2d350-114">복원 작업은 장치에서 볼륨을 온라인으로 자동으로 전환하지만 호스트에서 장치를 수동으로 온라인 상태로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-114">Although the restore operation automatically brings the volume online on the device, you must manually bring the device online on the host.</span></span> <span data-ttu-id="2d350-115">볼륨이 장치에서 온라인이 되는 즉시 호스트에서 볼륨을 온라인으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-115">You can bring the volume online on the host as soon as the volume is online on the device.</span></span> <span data-ttu-id="2d350-116">(복원 작업이 완료될 때까지 기다릴 필요가 없습니다.) 절차를 보려면 [볼륨을 오프라인으로 전환](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-116">(You do not need to wait until the restore operation is finished.) For procedures, go to [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).</span></span>

* <span data-ttu-id="2d350-117">**복원 후 볼륨 유형** – 삭제된 볼륨은 스냅숏의 유형에 따라 복원됩니다. 즉, 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복원되고 계층화된 볼륨은 계층화된 볼륨으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-117">**Volume type after restore** – Deleted volumes are restored based on the type in the snapshot; that is, volumes that were locally pinned are restored as locally pinned volumes and volumes that were tiered are restored as tiered volumes.</span></span>

    <span data-ttu-id="2d350-118">기존 볼륨의 경우 현재 볼륨의 사용 유형은 스냅숏에 저장되는 유형을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-118">For existing volumes, the current usage type of the volume overrides the type that is stored in the snapshot.</span></span> <span data-ttu-id="2d350-119">예를 들어 볼륨 유형이 계층화였을 때 수행한 스냅숏의 볼륨을 복원하고 볼륨 유형이 이제 로컬로 고정되는 경우(수행된 변환 작업으로 인해) 볼륨은 로컬로 고정된 볼륨으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-119">For example, if you restore a volume from a snapshot that was taken when the volume type was tiered and that volume type is now locally pinned (due to a conversion operation that was performed), then the volume will be restored as a locally pinned volume.</span></span> <span data-ttu-id="2d350-120">마찬가지로, 기존 로컬로 고정된 볼륨이 확장되고 이후에 볼륨이 더 작은 경우에 수행된 이전 스냅숏에서 복원된 경우 복원된 볼륨은 현재 확장된 크기를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-120">Similarly, if an existing locally pinned volume was expanded and subsequently restored from an older snapshot taken when the volume was smaller, the restored volume will retain the current expanded size.</span></span>

    <span data-ttu-id="2d350-121">볼륨을 복원하는 동안 계층화된 볼륨에서 로컬로 고정된 볼륨으로 또는 로컬로 고정된 볼륨에서 계층화된 볼륨으로 볼륨을 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-121">You cannot convert a volume from a tiered volume to a locally pinned volume or from a locally pinned volume to a tiered volume while the volume is being restored.</span></span> <span data-ttu-id="2d350-122">복원 작업이 완료될 때까지 기다린 다음 볼륨을 다른 종류로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-122">Wait until the restore operation is finished, and then you can convert the volume to another type.</span></span> <span data-ttu-id="2d350-123">볼륨 변환에 대한 자세한 내용은 [볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-123">For information about converting a volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span> 

* <span data-ttu-id="2d350-124">**볼륨 크기는 복원된 볼륨에 반영됩니다.** – 삭제된(로컬로 고정된 볼륨이 완전히 프로비전되었기 때문에) 로컬로 고정된 볼륨을 복원하는 경우 중요한 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-124">**The volume size is reflected in the restored volume** – This is an important consideration if you are restoring a locally pinned volume that has been deleted (because locally pinned volumes are fully provisioned).</span></span> <span data-ttu-id="2d350-125">이전에 삭제된 로컬로 고정된 볼륨을 복원하기 전에 충분한 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-125">Make sure that you have sufficient space before you attempt to restore a locally pinned volume that was previously deleted.</span></span>

* <span data-ttu-id="2d350-126">**복원하는 동안 볼륨을 확장할 수 없습니다.** – 볼륨을 확장하기 전에 복원 작업이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-126">**You cannot expand a volume while it is being restored** – Wait until the restore operation is finished before you attempt to expand the volume.</span></span> <span data-ttu-id="2d350-127">볼륨 확장에 대한 정보는 [볼륨 수정](storsimple-8000-manage-volumes-u2.md#modify-a-volume)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-127">For information about expanding a volume, go to [Modify a volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).</span></span>

* <span data-ttu-id="2d350-128">**로컬 볼륨을 복원하는 동안 백업을 수행할 수 있습니다.** – 해당 절차를 보려면 [StorSimple 장치 관리자 서비스를 사용하여 백업 정책 관리](storsimple-8000-manage-backup-policies-u2.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-128">**You can perform a backup while you restore a local volume** – For procedures go to [Use the StorSimple Device Manager service to manage backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>

* <span data-ttu-id="2d350-129">**복원 작업을 취소할 수 있습니다.** - 복원 작업을 취소하는 경우 볼륨은 복원 작업을 시작하기 전의 상태로 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-129">**You can cancel a restore operation** – If you cancel the restore job, then the volume will be rolled back to the state that it was in before you initiated the restore operation.</span></span> <span data-ttu-id="2d350-130">절차를 보려면 [작업 취소](storsimple-8000-manage-jobs-u2.md#cancel-a-job)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-130">For procedures, go to [Cancel a job](storsimple-8000-manage-jobs-u2.md#cancel-a-job).</span></span>

## <a name="how-does-restore-work"></a><span data-ttu-id="2d350-131">복원 작업 방법</span><span class="sxs-lookup"><span data-stu-id="2d350-131">How does restore work</span></span>

<span data-ttu-id="2d350-132">업데이트 4 이상을 실행하는 장치의 경우 heatmap 기반 복원이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-132">For devices running Update 4 or later, a heatmap-based restore is implemented.</span></span> <span data-ttu-id="2d350-133">데이터에 액세스하는 호스트의 요청이 장치에 도달하면 이러한 요청이 추적되고 heatmap이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-133">As the host requests to access data reach the device, these requests are tracked and a heatmap is created.</span></span> <span data-ttu-id="2d350-134">요청 비율이 높으면 열이 많은 데이터 청크가 발생하고 요청 비율이 낮으면 열이 더 낮은 청크로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-134">High request rate results in data chunks with higher heat whereas lower request rate translates to chunks with lower heat.</span></span> <span data-ttu-id="2d350-135">_hot_으로 표시되려면 최소한 두 번 이상 데이터에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-135">You must access the data atleast twice to be marked as _hot_.</span></span> <span data-ttu-id="2d350-136">수정된 파일도 _hot_으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-136">A file that is modified is also marked as _hot_.</span></span> <span data-ttu-id="2d350-137">복원을 시작하면 heatmap을 기반으로 데이터의 자동 관리 하이드레이션이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-137">Once you initiate the restore, then proactive hydration of data occurs based on the heatmap.</span></span> <span data-ttu-id="2d350-138">업데이트 4 이전 버전의 경우 데이터는 액세스 시에만 복원 중에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-138">For versions earlier than Update 4, the data is downloaded during restore based on access only.</span></span>

<span data-ttu-id="2d350-139">열 지도 기반 복원에는 다음 주의 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-139">The following caveats apply to heatmap-based restores:</span></span>

* <span data-ttu-id="2d350-140">열 지도 추적은 계층화된 볼륨에 대해서만 사용하도록 설정되고 로컬로 고정된 볼륨은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-140">Heatmap tracking is enabled only for tiered volumes and locally pinned volumes are not supported.</span></span>

* <span data-ttu-id="2d350-141">다른 장치에 볼륨을 복제하는 경우에는 열 지도 기반 복원이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-141">Heatmap-based restore is not supported when cloning a volume to another device.</span></span> 

* <span data-ttu-id="2d350-142">현재 위치 복원이 있고 복원할 볼륨에 대한 로컬 스냅숏은 장치에 있는 경우 (데이터를 이미 로컬에서 사용할 수 있으므로) 리하이드레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-142">If there is an in-place restore and a local snapshot for the volume to be restored exists on the device, then we do not rehydrate (as data is already available locally).</span></span> 

* <span data-ttu-id="2d350-143">기본적으로 복원할 때 heatmap을 기반으로 데이터를 사전에 리하이드레이션하는 리하이드레이션 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-143">By default, when you restore, the rehydration jobs are initiated that proactively rehydrate data based on the heatmap.</span></span> 

<span data-ttu-id="2d350-144">업데이트 4에서 Windows PowerShell cmdlet은 리하이드레이션 작업 실행을 쿼리하고, 리하이드레이션 작업을 취소하며, 리하이드레이션 작업 작업의 상태를 가져오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-144">In Update 4, Windows PowerShell cmdlets can be used to query running rehydration jobs, cancel a rehydration job, and get the status of the rehydration job.</span></span>

* <span data-ttu-id="2d350-145">`Get-HcsRehydrationJob` - 이 cmdlet은 리하이드레이션 작업의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-145">`Get-HcsRehydrationJob` - This cmdlet gets the status of the rehydration job.</span></span> <span data-ttu-id="2d350-146">하나의 볼륨에 대해 단일 리하이드레이션 작업이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-146">A single rehydration job is triggered for one volume.</span></span>

* <span data-ttu-id="2d350-147">`Set-HcsRehydrationJob` - 이 cmdlet을 사용하면 리하이드레이션이 진행 중일 때 해당 작업을 일시 중지, 중지 또는 재개할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-147">`Set-HcsRehydrationJob` - This cmdlet allows you to pause, stop, resume the rehydration job, when the rehydration is in progress.</span></span>

<span data-ttu-id="2d350-148">리하이드레이션 cmdlet에 대한 자세한 내용은 [StorSimple용 Windows PowerShell cmdlet 참조](https://technet.microsoft.com/library/dn688168.aspx)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="2d350-148">For more information on rehydration cmdlets, go to [Windows PowerShell cmdlet reference for StorSimple](https://technet.microsoft.com/library/dn688168.aspx).</span></span>

<span data-ttu-id="2d350-149">자동 리하이드레이션을 사용하면 일반적으로 일시적인 더 높은 읽기 성능이 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-149">With automatic rehdyration, typically higher transient read performance is expected.</span></span> <span data-ttu-id="2d350-150">실제 개선되는 정도는 액세스 패턴, 데이터 변동 및 데이터 형식 등 다양한 요인에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-150">The actual magniutde of improvements depends on various factors such as access pattern, data churn, and data type.</span></span> 

<span data-ttu-id="2d350-151">리하이드레이션 작업을 취소하려면 PowerShell cmdlet을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-151">To cancel a rehydration job, you can use the PowerShell cmdlet.</span></span> <span data-ttu-id="2d350-152">이후 모든 복원 작업에 대해 리하이드레이션 작업을 영구적으로 사용하지 않도록 설정하려면 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="2d350-152">If you wish to permanently disable rehydration jobs for all the future restores, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="2d350-153">백업 카탈로그를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="2d350-153">How to use the backup catalog</span></span>

<span data-ttu-id="2d350-154">**백업 카탈로그** 블레이드는 백업 세트 선택 범위를 좁히는 데 도움이 되는 쿼리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-154">The **Backup Catalog** blade provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="2d350-155">다음 매개 변수를 기반으로 검색되는 백업 세트를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-155">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="2d350-156">**시간 범위** – 백업 세트를 만든 날짜 및 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-156">**Time range** – The date and time range when the backup set was created.</span></span>
* <span data-ttu-id="2d350-157">**장치** – 백업 세트를 만든 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-157">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="2d350-158">**백업 정책** 또는 **볼륨** – 백업 정책 또는 이 백업 세트와 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-158">**Backup policy** or **Volume** – The backup policy or volume associated with this backup set.</span></span>

<span data-ttu-id="2d350-159">그런 다음 필터링된 백업 세트는 다음 특성을 기반으로 표로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-159">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="2d350-160">**이름** – 백업 정책 또는 이 백업 세트와 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-160">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="2d350-161">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-161">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="2d350-162">로컬 스냅숏은 장치에 로컬로 저장된 모든 볼륨 데이터의 백업인 반면 클라우드 스냅숏은 클라우드에 상주하는 볼륨 데이터의 백업을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-162">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="2d350-163">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-163">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="2d350-164">**크기** – 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-164">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="2d350-165">**만든 날짜** – 백업이 만들어진 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-165">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="2d350-166">**볼륨** -백업 세트와 연결된 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-166">**Volumes** - The number of volumes associated with the backup set.</span></span>
* <span data-ttu-id="2d350-167">**시작** – 일정에 따라 자동으로 또는 사용자가 수동으로 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-167">**Initiated** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="2d350-168">(백업을 예약하기 위해 백업 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-168">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="2d350-169">또는 **백업 수행** 옵션을 사용하여 대화형 또는 요청 시 백업을 수행할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="2d350-169">Alternatively, you can use the **Take backup** option to take an interactive or on-demand backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="2d350-170">백업에서 StorSimple 볼륨을 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="2d350-170">How to restore your StorSimple volume from a backup</span></span>

<span data-ttu-id="2d350-171">**백업 카탈로그** 블레이드를 사용하여 특정 백업에서 StorSimple 볼륨을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-171">You can use the **Backup Catalog** blade to restore your StorSimple volume from a specific backup.</span></span> <span data-ttu-id="2d350-172">그러나 볼륨을 복원하면 백업이 수행된 시점의 상태로 볼륨이 되돌려진다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="2d350-172">Keep in mind, however, that restoring a volume will revert the volume to the state it was in when the backup was taken.</span></span> <span data-ttu-id="2d350-173">백업 작업 후 추가된 모든 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-173">Any data that was added after the backup operation will be lost.</span></span>

> [!WARNING]
> <span data-ttu-id="2d350-174">백업에서 복원되면 백업에서 기존 볼륨을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-174">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="2d350-175">백업이 수행된 후 작성된 모든 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-175">This may cause the loss of any data that was written after the backup was taken.</span></span>


### <a name="to-restore-your-volume"></a><span data-ttu-id="2d350-176">볼륨을 복원하려면</span><span class="sxs-lookup"><span data-stu-id="2d350-176">To restore your volume</span></span>
1. <span data-ttu-id="2d350-177">StorSimple 장치 관리자 서비스로 이동한 다음 **백업 카탈로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-177">Go to your StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="2d350-178">백업 세트를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-178">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="2d350-179">시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-179">Specify the time range.</span></span>
   2. <span data-ttu-id="2d350-180">해당 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-180">Select the appropriate device.</span></span>
   3. <span data-ttu-id="2d350-181">드롭다운 목록에서 선택하려는 백업에 대 한 볼륨 또는 백업 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-181">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="2d350-182">**적용**을 클릭하여 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-182">Click **Apply** to execute this query.</span></span>

    <span data-ttu-id="2d350-183">선택한 볼륨와 연결된 백업을 또는 백업 정책이 백업 세트의 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-183">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
   
    ![백업 세트 목록](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. <span data-ttu-id="2d350-185">백업 세트를 확장하여 연결된 볼륨을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-185">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="2d350-186">이 볼륨은 복원하려면 호스트와 장치에서 오프라인 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-186">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="2d350-187">장치의 **볼륨** 블레이드에서 볼륨에 액세스한 다음, [볼륨을 오프라인 상태로 전환](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)의 단계에 따라 오프라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-187">Access the volumes on the **Volumes** blade of your device, and then follow the steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) to take them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2d350-188">해당 볼륨을 오프 라인으로 전환하기 전에, 먼저 호스트에서 해당 볼륨을 오프라인으로 전환했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-188">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="2d350-189">호스트에서 볼륨을 오프라인으로 전환하지 않은 경우 잠재적으로 데이터가 손상될 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-189">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   
4. <span data-ttu-id="2d350-190">**백업 카탈로그** 탭으로 다시 이동하고 백업 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-190">Navigate back to the **Backup Catalog** tab and select a backup set.</span></span> <span data-ttu-id="2d350-191">마우스 오른쪽 단추를 클릭하고 상황에 맞는 메뉴에서 **복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-191">Right-click and then from the context menu, select **Restore**.</span></span>

    ![백업 세트 목록](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. <span data-ttu-id="2d350-193">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-193">You will be prompted for confirmation.</span></span> <span data-ttu-id="2d350-194">복원 정보를 검토하고 확인 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-194">Review the restore information, and then select the confirmation check box.</span></span>
   
    ![확인 페이지](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  <span data-ttu-id="2d350-196">**복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-196">Click **Restore**.</span></span> <span data-ttu-id="2d350-197">그러면 **작업** 페이지에 액세스하여 볼 수 있는 복원 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-197">This initiates a restore job that you can view by accessing the **Jobs** page.</span></span>

    ![확인 페이지](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. <span data-ttu-id="2d350-199">복원이 완료되면 볼륨의 콘텐츠가 백업의 볼륨으로 바뀌는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-199">After the restore is complete, verify that the contents of your volumes are replaced by volumes from the backup.</span></span>


## <a name="if-the-restore-fails"></a><span data-ttu-id="2d350-200">복원에 실패하는 경우</span><span class="sxs-lookup"><span data-stu-id="2d350-200">If the restore fails</span></span>

<span data-ttu-id="2d350-201">복원 작업이 어떤 이유로든 실패하는 경우에 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-201">You will receive an alert if the restore operation fails for any reason.</span></span> <span data-ttu-id="2d350-202">이 경우 백업이 여전히 유효한지 확인하려면 백업 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-202">If this occurs, refresh the backup list to verify that the backup is still valid.</span></span> <span data-ttu-id="2d350-203">백업이 유효하고 클라우드로부터 복원하는 경우 연결 문제를 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-203">If the backup is valid and you are restoring from the cloud, then connectivity issues might be causing the problem.</span></span>

<span data-ttu-id="2d350-204">복원 작업을 완료하려면 호스트에서 오프라인으로 볼륨을 가져오고 복원 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-204">To complete the restore operation, take the volume offline on the host and retry the restore operation.</span></span> <span data-ttu-id="2d350-205">복원 프로세스 중에 수행된 볼륨 데이터에 대한 수정은 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-205">Note that any modifications to the volume data that were performed during the restore process will be lost.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d350-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d350-206">Next steps</span></span>
* <span data-ttu-id="2d350-207">[StorSimple 볼륨을 관리](storsimple-8000-manage-volumes-u2.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-207">Learn how to [Manage StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="2d350-208">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2d350-208">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

