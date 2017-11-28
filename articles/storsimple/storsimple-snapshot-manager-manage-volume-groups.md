---
title: "StorSimple Snapshot Manager 볼륨 그룹 | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 MMC 스냅인을 사용하여 볼륨 그룹을 만들고 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 6067a88cd42d29c3d2f4b74580095424de77561e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="d2734-103">StorSimple 스냅숏 관리자를 사용하여 볼륨 그룹 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d2734-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="d2734-104">개요</span><span class="sxs-lookup"><span data-stu-id="d2734-104">Overview</span></span>
<span data-ttu-id="d2734-105">**범위** 창에서 **볼륨 그룹** 노드를 사용하면 볼륨 그룹에 볼륨을 할당하고 볼륨 그룹에 대한 정보를 확인하고 백업을 예약하고 볼륨 그룹을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="d2734-106">볼륨 그룹은 백업이 응용 프로그램에 일관됨을 보장하는 데 사용되는 관련 볼륨들의 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="d2734-107">자세한 내용은 [볼륨 및 볼륨 그룹](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups)과 [Windows 볼륨 섀도 복사본 서비스와의 통합](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2734-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d2734-108">볼륨 그룹의 모든 볼륨은 단일 클라우드 서비스 공급자에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="d2734-109">볼륨 그룹을 구성할 때는 클러스터 공유 볼륨(CSV)과 비 CSV를 동일한 볼륨 그룹에 혼합하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="d2734-110">StorSimple 스냅숏 관리자는 동일한 스냅숏에 혼합되어 있는 CSV와 비 CSV를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>

![볼륨 그룹 노드](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="d2734-112">**그림 1: StorSimple 스냅숏 관리자 볼륨 그룹 노드**</span><span class="sxs-lookup"><span data-stu-id="d2734-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="d2734-113">이 자습서에서는 StorSimple 스냅숏 관리자를 사용하여 다음 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="d2734-114">볼륨 그룹에 대한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d2734-114">View information about your volume groups</span></span>
* <span data-ttu-id="d2734-115">볼륨 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d2734-115">Create a volume group</span></span>
* <span data-ttu-id="d2734-116">볼륨 그룹 백업</span><span class="sxs-lookup"><span data-stu-id="d2734-116">Back up a volume group</span></span>
* <span data-ttu-id="d2734-117">볼륨 그룹 편집</span><span class="sxs-lookup"><span data-stu-id="d2734-117">Edit a volume group</span></span>
* <span data-ttu-id="d2734-118">볼륨 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="d2734-118">Delete a volume group</span></span>

<span data-ttu-id="d2734-119">이러한 모든 작업을 **작업** 창에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="d2734-120">볼륨 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="d2734-120">View volume groups</span></span>
<span data-ttu-id="d2734-121">**볼륨 그룹** 노드를 클릭하면 선택한 열에 따라 **결과** 창에 각 볼륨 그룹에 대해 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="d2734-122">**결과** 창의 열은 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="d2734-123">**볼륨** 노드를 마우스 오른쪽 단추로 클릭하고 **보기**를 선택한 다음 **열 추가/제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="d2734-124">결과 열</span><span class="sxs-lookup"><span data-stu-id="d2734-124">Results column</span></span> | <span data-ttu-id="d2734-125">설명</span><span class="sxs-lookup"><span data-stu-id="d2734-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d2734-126">이름</span><span class="sxs-lookup"><span data-stu-id="d2734-126">Name</span></span> |<span data-ttu-id="d2734-127">**이름** 열에는 볼륨 그룹의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="d2734-128">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2734-128">Application</span></span> |<span data-ttu-id="d2734-129">**응용 프로그램** 열은 Windows 호스트에 현재 설치되어 실행 중인 VSS 기록기의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="d2734-130">선택</span><span class="sxs-lookup"><span data-stu-id="d2734-130">Selected</span></span> |<span data-ttu-id="d2734-131">**선택** 열은 볼륨 그룹에 포함된 볼륨의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="d2734-132">0이면 볼륨 그룹의 볼륨에 연결된 응용 프로그램이 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="d2734-133">가져옴</span><span class="sxs-lookup"><span data-stu-id="d2734-133">Imported</span></span> |<span data-ttu-id="d2734-134">**가져옴** 열은 가져온 볼륨의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="d2734-135">이 열이 **True**로 설정되면 볼륨 그룹을 Azure Portal에서 가져왔으며 StorSimple 스냅숏 관리자에서 만들지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-135">When set to **True**, this column indicates that a volume group was imported from the Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="d2734-136">StorSimple 스냅숏 관리자 볼륨 그룹은 Azure Portal의 **백업 정책** 탭에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="d2734-137">볼륨 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d2734-137">Create a volume group</span></span>
<span data-ttu-id="d2734-138">다음 절차에 따라 볼륨 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="d2734-139">볼륨 그룹을 만들려면</span><span class="sxs-lookup"><span data-stu-id="d2734-139">To create a volume group</span></span>
1. <span data-ttu-id="d2734-140">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d2734-141">**범위** 창에서 **볼륨 그룹**을 마우스 오른쪽 단추로 클릭한 다음 **볼륨 그룹 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![볼륨 그룹 만들기](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="d2734-143">**볼륨 그룹 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-143">The **Create a volume group** dialog box appears.</span></span>
   
    ![볼륨 그룹 만들기 대화 상자](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="d2734-145">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-145">Enter the following information:</span></span>
   
   1. <span data-ttu-id="d2734-146">**이름** 상자에 새 볼륨 그룹에 대해 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-146">In the **Name** box, type a unique name for the new volume group.</span></span>
   2. <span data-ttu-id="d2734-147">**응용 프로그램** 상자에서 볼륨 그룹에 추가할 볼륨과 연결된 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span>
      
       <span data-ttu-id="d2734-148">**응용 프로그램** 상자에는 StorSimple 볼륨을 사용하고 VSS 기록기를 사용하도록 설정된 응용 프로그램만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="d2734-149">VSS 기록기는 기록기가 인식하는 모든 볼륨이 StorSimple 볼륨인 경우에만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="d2734-150">응용 프로그램 상자가 비어 있으면 Azure StorSimple 볼륨을 사용하고 VSS 기록기를 지원하는 응용 프로그램이 설치되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="d2734-151">(현재 Azure StorSimple은 Microsoft Exchange 및 SQL Server를 지원합니다.) VSS 기록기에 대한 자세한 내용은 [Windows 볼륨 섀도 복사본 서비스와의 통합](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2734-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="d2734-152">응용 프로그램을 선택하면 연결된 모든 볼륨이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="d2734-153">반대로, 특정 응용 프로그램과 연결된 볼륨을 선택하면 **응용 프로그램** 상자에서 해당 응용 프로그램이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="d2734-154">**볼륨** 상자에서 볼륨 그룹에 추가할 StorSimple 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="d2734-155">단일 또는 다중 파티션이 있는 볼륨을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="d2734-156">(다중 파티션 볼륨은 다중 파티션이 있는 기본 디스크 또는 동적 디스크일 수 있습니다.) 다중 파티션이 포함된 볼륨은 단일 단위로 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="d2734-157">따라서 파티션 중 하나만 볼륨 그룹에 추가해도 다른 모든 파티션이 해당 볼륨 그룹에 동시에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="d2734-158">볼륨 그룹에 다중 파티션 볼륨을 추가한 후에도 해당 다중 파티션 볼륨은 계속 단일 단위로 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="d2734-159">볼륨을 할당하지 않으면 빈 볼륨 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="d2734-160">클러스터 공유 볼륨(CSV)과 비 CSV를 동일한 볼륨 그룹에 혼합하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="d2734-161">StorSimple 스냅숏 관리자는 동일한 스냅숏에 혼합되어 있는 CSV 볼륨과 비 CSV 볼륨을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span>
4. <span data-ttu-id="d2734-162">**확인** 을 클릭하여 볼륨 그룹을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="d2734-163">볼륨 그룹 백업</span><span class="sxs-lookup"><span data-stu-id="d2734-163">Back up a volume group</span></span>
<span data-ttu-id="d2734-164">다음 절차에 따라 볼륨 그룹을 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="d2734-165">볼륨 그룹을 백업하려면</span><span class="sxs-lookup"><span data-stu-id="d2734-165">To back up a volume group</span></span>
1. <span data-ttu-id="d2734-166">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d2734-167">**범위** 창에서 **볼륨 그룹** 노드를 확장하고 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭한 다음 **백업 수행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![볼륨 그룹 즉시 백업](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="d2734-169">**백업 수행** 대화 상자에서 **로컬 스냅숏** 또는 **클라우드 스냅숏**를 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![백업 수행 대화 상자](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="d2734-171">백업이 실행되고 있는지 확인하려면 **작업** 노드를 확장한 다음 **실행 중**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="d2734-172">백업이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-172">The backup should be listed.</span></span>
5. <span data-ttu-id="d2734-173">완료된 스냅숏을 보려면 **백업 카탈로그** 노드를 확장하고 볼륨 그룹 이름을 확장한 다음 **로컬 스냅숏** 또는 **클라우드 스냅숏**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="d2734-174">성공적으로 완료되면 백업이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-174">The backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="d2734-175">볼륨 그룹 편집</span><span class="sxs-lookup"><span data-stu-id="d2734-175">Edit a volume group</span></span>
<span data-ttu-id="d2734-176">다음 절차에 따라 볼륨 그룹을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="d2734-177">볼륨 그룹을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="d2734-177">To edit a volume group</span></span>
1. <span data-ttu-id="d2734-178">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d2734-179">**범위** 창에서 **볼륨 그룹** 노드를 확장하고 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="d2734-180">**볼륨 그룹 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-180">The **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="d2734-181">**이름**, **응용 프로그램** 및 **볼륨** 항목을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="d2734-182">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="d2734-183">볼륨 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="d2734-183">Delete a volume group</span></span>
<span data-ttu-id="d2734-184">다음 절차에 따라 볼륨 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="d2734-185">이 작업을 수행하면 볼륨 그룹에 연결된 모든 백업이 함께 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="d2734-186">볼륨 그룹을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="d2734-186">To delete a volume group</span></span>
1. <span data-ttu-id="d2734-187">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d2734-188">**범위** 창에서 **볼륨 그룹** 노드를 확장하고 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="d2734-189">**볼륨 그룹 삭제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="d2734-190">텍스트 상자에 **Confirm**을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-190">Type **Confirm** in the text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="d2734-191">삭제한 볼륨 그룹이 **결과** 창의 목록에서 사라지고 해당 볼륨 그룹에 연결된 모든 백업이 백업 카탈로그에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2734-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2734-192">Next steps</span></span>
* <span data-ttu-id="d2734-193">[StorSimple 스냅숏 관리자를 사용하여 StorSimple 솔루션을 관리](storsimple-snapshot-manager-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="d2734-194">[StorSimple 스냅숏 관리자를 사용하여 백업 정책을 만들고 관리](storsimple-snapshot-manager-manage-backup-policies.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2734-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

