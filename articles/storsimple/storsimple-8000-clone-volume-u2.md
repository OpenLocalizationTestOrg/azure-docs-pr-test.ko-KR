---
title: "StorSimple 8000 시리즈에서 볼륨 복제 | Microsoft Docs"
description: "다른 복제 유형 및 사용에 대해 설명하고, StorSimple 8000 시리즈 장치에서 개별 볼륨을 복제하는 데 백업 세트를 사용하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 70c85bcb2c26d2ad3d0515d24e028f84495634c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-clone-a-volume"></a><span data-ttu-id="7a1b4-103">Azure Portal에서 StorSimple 장치 관리자 서비스를 사용하여 볼륨 복제</span><span class="sxs-lookup"><span data-stu-id="7a1b4-103">Use the StorSimple Device Manager service in Azure portal to clone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="7a1b4-104">개요</span><span class="sxs-lookup"><span data-stu-id="7a1b4-104">Overview</span></span>

<span data-ttu-id="7a1b4-105">이 자습서에서는 **백업 카탈로그** 블레이드를 통해 개별 볼륨을 복제하는 데 백업 세트를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-105">This tutorial describes how you can use a backup set to clone an individual volume via the **Backup catalog** blade.</span></span> <span data-ttu-id="7a1b4-106">*임시* 및 *영구* 복제의 차이점에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-106">It also explains the difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="7a1b4-107">이 자습서의 지침은 업데이트 3 이상을 실행하는 모든 StorSimple 8000 시리즈 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-107">The guidance in this tutorial applies to all the StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="7a1b4-108">StorSimple 장치 관리자 서비스 **백업 카탈로그** 블레이드는 수동 또는 자동 백업을 수행할 때 생성되는 모든 백업 세트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-108">The StorSimple Device Manager service **Backup catalog** blade displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="7a1b4-109">그런 다음 복제할 백업 세트에서 볼륨을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-109">You can then select a volume in a backup set to clone.</span></span>

 ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="7a1b4-111">볼륨 복제 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7a1b4-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="7a1b4-112">볼륨을 복제하기 전에 다음 정보를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-112">Consider the following information when cloning a volume.</span></span>

- <span data-ttu-id="7a1b4-113">복제본은 일반 볼륨과 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-113">A clone behaves in the same way as a regular volume.</span></span> <span data-ttu-id="7a1b4-114">볼륨에서 사용할 수 있는 모든 작업은 복제에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-114">Any operation that is possible on a volume is available for the clone.</span></span>

- <span data-ttu-id="7a1b4-115">모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="7a1b4-116">모든 백업에 복제된 볼륨을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-116">You would need to configure a cloned volume for any backups.</span></span>

- <span data-ttu-id="7a1b4-117">로컬 고정 볼륨은 계층화된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="7a1b4-118">복제된 볼륨을 로컬로 고정해야 하는 경우 복제 작업이 성공적으로 완료된 후 클론을 로컬로 고정된 볼륨으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-118">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="7a1b4-119">계층화된 볼륨을 로컬로 고정된 볼륨으로 변환하는 방법에 대한 자세한 내용은 [볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-119">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="7a1b4-120">복제 후(여전히 임시 클론일 경우) 즉시 복제된 볼륨을 계층화된 볼륨에서 로컬 고정 볼륨으로 변환하려는 경우 다음 오류 메시지로 전환에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-120">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion fails with the following error message:</span></span>

    `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.`

    <span data-ttu-id="7a1b4-121">다른 장치에 복제하는 경우 이 오류가 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-121">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="7a1b4-122">먼저 임시 클론을 영구 클론으로 변환시키면 성공적으로 볼륨을 로컬로 고정된 볼륨으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-122">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="7a1b4-123">임시 클론의 클라우드 스냅숏을 만들어서 영구 클론으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-123">Take a cloud snapshot of the transient clone to convert it to a permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="7a1b4-124">볼륨의 클론 만들기</span><span class="sxs-lookup"><span data-stu-id="7a1b4-124">Create a clone of a volume</span></span>

<span data-ttu-id="7a1b4-125">로컬 또는 클라우드 스냅숏을 사용하여 동일한 장치, 다른 장치 또는 클라우드 어플라이언스에 클론을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-125">You can create a clone on the same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="7a1b4-126">아래 절차는 백업 카탈로그에서 클론을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-126">The procedure below describes how to create a clone from the backup catalog.</span></span>  <span data-ttu-id="7a1b4-127">복제를 시작하는 다른 방법은 **볼륨**으로 이동하여 볼륨을 선택한 후 상황에 맞는 메뉴를 호출하도록 마우스 오른쪽 단추로 클릭하고 **복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-127">An alternative method to initiate clone is to go to **Volumes**, select a volume, then right-click to invoke the context menu and select **Clone**.</span></span>

<span data-ttu-id="7a1b4-128">백업 카탈로그에서 볼륨의 클론을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-128">Perform the following steps to create a clone of your volume from the backup catalog.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="7a1b4-129">볼륨 복제하기</span><span class="sxs-lookup"><span data-stu-id="7a1b4-129">To clone a volume</span></span>

1. <span data-ttu-id="7a1b4-130">StorSimple 장치 관리자 서비스로 이동한 다음 **백업 카탈로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-130">Go to your StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="7a1b4-131">백업 세트를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="7a1b4-132">해당 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-132">Select the appropriate device.</span></span>
   2. <span data-ttu-id="7a1b4-133">드롭다운 목록에서 선택하려는 백업에 대 한 볼륨 또는 백업 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-133">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="7a1b4-134">시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-134">Specify the time range.</span></span>
   4. <span data-ttu-id="7a1b4-135">**적용**을 클릭하여 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-135">Click **Apply** to execute this query.</span></span>

    <span data-ttu-id="7a1b4-136">선택한 볼륨와 연결된 백업을 또는 백업 정책이 백업 세트의 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-136">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
   
    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="7a1b4-138">백업 세트를 확장하여 연결된 볼륨을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-138">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="7a1b4-139">이 볼륨은 복원하려면 호스트와 장치에서 오프라인 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-139">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="7a1b4-140">장치의 **볼륨** 블레이드에서 볼륨에 액세스한 다음, [볼륨을 오프라인 상태로 전환](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)의 단계에 따라 오프라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-140">Access the volumes on the **Volumes** blade of your device, and then follow the steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) to take them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7a1b4-141">해당 볼륨을 오프 라인으로 전환하기 전에, 먼저 호스트에서 해당 볼륨을 오프라인으로 전환했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-141">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="7a1b4-142">호스트에서 볼륨을 오프라인으로 전환하지 않은 경우 잠재적으로 데이터가 손상될 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-142">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   
4. <span data-ttu-id="7a1b4-143">**백업 카탈로그**로 다시 이동하고 백업 세트에서 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-143">Navigate back to the **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="7a1b4-144">마우스 오른쪽 단추를 클릭하고 상황에 맞는 메뉴에서 **복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-144">Right-click and then from the context menu, select **Clone**.</span></span>

   ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="7a1b4-146">**복제** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-146">In the **Clone** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="7a1b4-147">대상 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-147">Identify a target device.</span></span> <span data-ttu-id="7a1b4-148">클론이 만들어지는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-148">This is the location where the clone will be created.</span></span> <span data-ttu-id="7a1b4-149">동일한 장치를 선택하거나 다른 장치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-149">You can choose the same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7a1b4-150">복제에 필요한 용량은 대상 장치에서 사용 가능한 용량보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-150">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
       
    2. <span data-ttu-id="7a1b4-151">해당 클론에 대한 고유 볼륨 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="7a1b4-152">이름은 3자에서 127자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-152">The name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="7a1b4-153">로컬로 고정된 볼륨을 복제하더라도 **다른 이름으로 볼륨 복제** 필드는 **계층화됨**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-153">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="7a1b4-154">이 설정을 변경할 수 없습니다. 그러나 로컬로 고정된 복제된 볼륨도 필요한 경우 복제본을 성공적으로 만든 후 로컬로 고정된 볼륨으로 복제본을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-154">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="7a1b4-155">계층화된 볼륨을 로컬로 고정된 볼륨으로 변환하는 방법에 대한 자세한 내용은 [볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-155">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="7a1b4-156">**연결된 호스트** 아래에서 클론에 대한 ACR(액세스 제어 레코드)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-156">Under **Connected hosts**, specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="7a1b4-157">새 ACR을 추가하거나 기존 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-157">You can add a new ACR or choose from the existing list.</span></span> <span data-ttu-id="7a1b4-158">ACR은 이 클론에 액세스할 수 있는 호스트를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-158">The ACR will determine which hosts can access this clone.</span></span>
      
        ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="7a1b4-160">**복제**를 클릭하여 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-160">Click **Clone** to complete the operation.</span></span>

4. <span data-ttu-id="7a1b4-161">클론 작업이 시작되고 클론이 성공적으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-161">A clone job is initiated and you are notified when the clone is successfully created.</span></span> <span data-ttu-id="7a1b4-162">작업 알림을 클릭하거나 **작업** 블레이드로 이동하여 복제 작업을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-162">Click the job notification or go to **Jobs** blade to monitor the clone job.</span></span>

    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="7a1b4-164">복제 작업이 완료되면 장치로 이동한 다음 **볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-164">After the clone job is complete, go to your device and then click **Volumes**.</span></span> <span data-ttu-id="7a1b4-165">볼륨의 목록에서 원본 볼륨이 있는 동일한 볼륨 컨테이너에서 방금 만든 클론이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-165">In the list of volumes, you should see the clone that was just created in the same volume container that has the source volume.</span></span>

    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="7a1b4-167">이러한 방식으로 만들어진 클론은 임시 클론입니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="7a1b4-168">복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="7a1b4-169">임시 및 영구 복제본 비교</span><span class="sxs-lookup"><span data-stu-id="7a1b4-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="7a1b4-170">다른 장치에 복제하는 경우 임시 클론을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-170">Transient clones are created only when you clone to another device.</span></span> <span data-ttu-id="7a1b4-171">백업 세트로부터 StorSimple 장치 관리자에서 관리하는 다른 장치에 특정 볼륨을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-171">You can clone a specific volume from a backup set to a different device managed by the StorSimple Device Manager.</span></span> <span data-ttu-id="7a1b4-172">임시 클론에는 원본 볼륨의 데이터에 대한 참조가 있으며 대상 장치에서 로컬로 읽고 쓰는 동안 해당 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-172">The transient clone has references to the data in the original volume and uses that data to read and write locally on the target device.</span></span>

<span data-ttu-id="7a1b4-173">임시 클론의 클라우드 스냅숏을 수행한 후 결과 클론은 *영구* 클론이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-173">After you take a cloud snapshot of a transient clone, the resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="7a1b4-174">이 과정에서 데이터 복사본이 클라우드에서 생성되고, 이 데이터를 복사하는 시간은 데이터의 크기 및 Azure 지연 시간에 따라 결정됩니다(Azure 간 복사).</span><span class="sxs-lookup"><span data-stu-id="7a1b4-174">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="7a1b4-175">이 프로세스는 며칠에서 몇 주까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-175">This process can take days to weeks.</span></span> <span data-ttu-id="7a1b4-176">임시 클론은 영구 클론이 되며, 복제된 원본 볼륨 데이터에 대한 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-176">The transient clone becomes a permanent clone and doesn’t have any references to the original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="7a1b4-177">임시 및 영구 클론에 대한 시나리오</span><span class="sxs-lookup"><span data-stu-id="7a1b4-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="7a1b4-178">다음 섹션에서는 임시 및 영구 클론을 사용할 수 있는 예제 상황에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-178">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="7a1b4-179">임시 클론을 사용하여 항목 수준 복구</span><span class="sxs-lookup"><span data-stu-id="7a1b4-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="7a1b4-180">1년 된 Microsoft PowerPoint 프레젠테이션 파일을 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-180">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="7a1b4-181">IT 관리자는 해당 시간에서 특정 백업을 식별하고 볼륨을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-181">Your IT administrator identifies the specific backup from that time, and then filters the volume.</span></span> <span data-ttu-id="7a1b4-182">그런 다음 관리자는 해당 볼륨을 복제하고, 필요한 파일을 찾아 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-182">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="7a1b4-183">이 시나리오에서는 임시 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="7a1b4-184">영구 클론을 사용하여 프로덕션 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="7a1b4-184">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="7a1b4-185">프로덕션 환경에서 테스트 버그를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-185">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="7a1b4-186">프로덕션 환경에서 볼륨의 클론을 만들고 이 클론의 클라우드 스냅숏을 만들어서 독립적으로 복제된 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-186">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="7a1b4-187">이 시나리오에서는 영구 클론이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a1b4-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a1b4-188">Next steps</span></span>
* <span data-ttu-id="7a1b4-189">[백업 세트에서 StorSimple 볼륨을 복원](storsimple-8000-restore-from-backup-set-u2.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-189">Learn how to [restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="7a1b4-190">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a1b4-190">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

