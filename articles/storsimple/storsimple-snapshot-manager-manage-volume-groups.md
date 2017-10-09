---
title: "스냅숏 관리자 볼륨 그룹 aaaStorSimple | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 toocreate hello 하 고 볼륨 그룹을 관리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a><span data-ttu-id="b22f9-103">StorSimple 스냅숏 관리자 toocreate를 사용 하 고 볼륨 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="b22f9-103">Use StorSimple Snapshot Manager toocreate and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="b22f9-104">개요</span><span class="sxs-lookup"><span data-stu-id="b22f9-104">Overview</span></span>
<span data-ttu-id="b22f9-105">Hello를 사용할 수 있습니다 **볼륨 그룹** hello에 대 한 노드 **범위** 창 tooassign 볼륨 toovolume 그룹, 볼륨 그룹에 대 한 정보 보기 백업을 예약 하 고 볼륨 그룹을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-105">You can use hello **Volume Groups** node on hello **Scope** pane tooassign volumes toovolume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="b22f9-106">볼륨 그룹은 백업이 응용 프로그램 일치 지 사용 되는 관련된 볼륨 tooensure의 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-106">Volume groups are pools of related volumes used tooensure that backups are application-consistent.</span></span> <span data-ttu-id="b22f9-107">자세한 내용은 [볼륨 및 볼륨 그룹](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups)과 [Windows 볼륨 섀도 복사본 서비스와의 통합](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b22f9-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b22f9-108">볼륨 그룹의 모든 볼륨은 단일 클라우드 서비스 공급자에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="b22f9-109">볼륨 그룹을 구성할 때 클러스터 공유 볼륨 (Csv)와 Csv 이외의 hello에 혼합 하지 않는 같은 볼륨 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="b22f9-110">StorSimple 스냅숏 관리자 Csv의 혼합을 지원 하지 않으며 Csv 이외의 동일한 스냅숏을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in hello same snapshot.</span></span>

![볼륨 그룹 노드](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="b22f9-112">**그림 1: StorSimple 스냅숏 관리자 볼륨 그룹 노드**</span><span class="sxs-lookup"><span data-stu-id="b22f9-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="b22f9-113">이 자습서에서는 StorSimple 스냅숏 관리자를 사용하여 다음 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="b22f9-114">볼륨 그룹에 대한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="b22f9-114">View information about your volume groups</span></span>
* <span data-ttu-id="b22f9-115">볼륨 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b22f9-115">Create a volume group</span></span>
* <span data-ttu-id="b22f9-116">볼륨 그룹 백업</span><span class="sxs-lookup"><span data-stu-id="b22f9-116">Back up a volume group</span></span>
* <span data-ttu-id="b22f9-117">볼륨 그룹 편집</span><span class="sxs-lookup"><span data-stu-id="b22f9-117">Edit a volume group</span></span>
* <span data-ttu-id="b22f9-118">볼륨 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="b22f9-118">Delete a volume group</span></span>

<span data-ttu-id="b22f9-119">이러한 모든 작업 에서도 사용할 수 있는 hello **동작** 창.</span><span class="sxs-lookup"><span data-stu-id="b22f9-119">All of these actions are also available on hello **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="b22f9-120">볼륨 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="b22f9-120">View volume groups</span></span>
<span data-ttu-id="b22f9-121">Hello를 누르면 **볼륨 그룹** 노드, hello **결과** hello 열 선택 내용에 따라, 창 hello 다음 각 볼륨 그룹에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-121">If you click hello **Volume Groups** node, hello **Results** pane shows hello following information about each volume group, depending on hello column selections you make.</span></span> <span data-ttu-id="b22f9-122">(열 hello에 hello **결과** 창을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-122">(hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="b22f9-123">마우스 오른쪽 단추로 클릭 hello **볼륨** 노드를 **보기**를 선택한 후 **열 추가/제거**.)</span><span class="sxs-lookup"><span data-stu-id="b22f9-123">Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="b22f9-124">결과 열</span><span class="sxs-lookup"><span data-stu-id="b22f9-124">Results column</span></span> | <span data-ttu-id="b22f9-125">설명</span><span class="sxs-lookup"><span data-stu-id="b22f9-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b22f9-126">이름</span><span class="sxs-lookup"><span data-stu-id="b22f9-126">Name</span></span> |<span data-ttu-id="b22f9-127">hello **이름** 열 hello 볼륨 그룹의 hello 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-127">hello **Name** column contains hello name of hello volume group.</span></span> |
| <span data-ttu-id="b22f9-128">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b22f9-128">Application</span></span> |<span data-ttu-id="b22f9-129">hello **응용 프로그램** 열 현재 설치 된 VSS 기록기의 hello 수를 표시 하 고 Windows 호스트 hello에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-129">hello **Applications** column shows hello number of VSS writers currently installed and running on hello Windows host.</span></span> |
| <span data-ttu-id="b22f9-130">선택</span><span class="sxs-lookup"><span data-stu-id="b22f9-130">Selected</span></span> |<span data-ttu-id="b22f9-131">hello **선택한** 열 hello 볼륨 그룹에 포함 된 볼륨의 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-131">hello **Selected** column shows hello number of volumes that are contained in hello volume group.</span></span> <span data-ttu-id="b22f9-132">영 (0) 응용 프로그램이 없습니다. hello 볼륨 그룹의 hello 볼륨 연관 되어 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-132">A zero (0) indicates that no application is associated with hello volumes in hello volume group.</span></span> |
| <span data-ttu-id="b22f9-133">가져옴</span><span class="sxs-lookup"><span data-stu-id="b22f9-133">Imported</span></span> |<span data-ttu-id="b22f9-134">hello **가져옴** 열 가져온된 볼륨의 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-134">hello **Imported** column shows hello number of imported volumes.</span></span> <span data-ttu-id="b22f9-135">설정 된 경우 너무**True**,이 열에 표시 하면 볼륨 그룹 hello Azure 포털에서에서 가져온 및 StorSimple 스냅숏 관리자를 만들지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-135">When set too**True**, this column indicates that a volume group was imported from hello Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="b22f9-136">StorSimple 스냅숏 관리자 볼륨 그룹 hello에 표시 됩니다 **백업 정책** hello Azure 포털에서에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-136">StorSimple Snapshot Manager volume groups are also displayed on hello **Backup Policies** tab in hello Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="b22f9-137">볼륨 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b22f9-137">Create a volume group</span></span>
<span data-ttu-id="b22f9-138">다음 프로시저 toocreate 볼륨 그룹 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-138">Use hello following procedure toocreate a volume group.</span></span>

#### <a name="toocreate-a-volume-group"></a><span data-ttu-id="b22f9-139">toocreate 볼륨 그룹</span><span class="sxs-lookup"><span data-stu-id="b22f9-139">toocreate a volume group</span></span>
1. <span data-ttu-id="b22f9-140">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-140">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="b22f9-141">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **볼륨 그룹**, 클릭 하 고 **볼륨 그룹 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-141">In hello **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![볼륨 그룹 만들기](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="b22f9-143">hello **볼륨 그룹 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-143">hello **Create a volume group** dialog box appears.</span></span>
   
    ![볼륨 그룹 만들기 대화 상자](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="b22f9-145">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-145">Enter hello following information:</span></span>
   
   1. <span data-ttu-id="b22f9-146">Hello에 **이름** hello 새 볼륨 그룹에 대 한 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-146">In hello **Name** box, type a unique name for hello new volume group.</span></span>
   2. <span data-ttu-id="b22f9-147">Hello에 **응용 프로그램** 상자의 hello 볼륨을 추가 하려는 toohello 볼륨 그룹에 연결 된 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-147">In hello **Applications** box, select applications associated with hello volumes that you will be adding toohello volume group.</span></span>
      
       <span data-ttu-id="b22f9-148">hello **응용 프로그램** 상자 목록에 StorSimple 볼륨을 사용 하 고 VSS 기록기는 응용 프로그램만 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-148">hello **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="b22f9-149">경우에 볼륨 hello 모든 hello 기록기 인식 VSS 기록기를 사용할 수 볼륨은 StorSimple 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-149">A VSS writer is enabled only if all hello volumes that hello writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="b22f9-150">Hello 응용 프로그램 상자가 비어 있으면 Azure StorSimple 볼륨을 사용 하 고 지원 되는 VSS 기록기는 응용 프로그램이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-150">If hello Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="b22f9-151">(현재 Azure StorSimple은 Microsoft Exchange 및 SQL Server를 지원합니다.) VSS 기록기에 대한 자세한 내용은 [Windows 볼륨 섀도 복사본 서비스와의 통합](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b22f9-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="b22f9-152">응용 프로그램을 선택하면 연결된 모든 볼륨이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="b22f9-153">반대로 특정 응용 프로그램과 관련 된 볼륨을 선택 하면 hello에서 응용 프로그램은 자동으로 선택 hello **응용 프로그램** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-153">Conversely, if you select volumes associated with a specific application, hello application is automatically selected in hello **Applications** box.</span></span> 
   3. <span data-ttu-id="b22f9-154">Hello에 **볼륨** 상자에서 StorSimple 볼륨 tooadd toohello 볼륨 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-154">In hello **Volumes** box, select StorSimple volumes tooadd toohello volume group.</span></span> 
      
      * <span data-ttu-id="b22f9-155">단일 또는 다중 파티션이 있는 볼륨을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="b22f9-156">(다중 파티션 볼륨은 다중 파티션이 있는 기본 디스크 또는 동적 디스크일 수 있습니다.) 다중 파티션이 포함된 볼륨은 단일 단위로 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="b22f9-157">따라서 다른 파티션에 hello 파티션 tooa 볼륨 그룹을 모든 hello 중 하나에 추가 하는 경우는 자동으로 추가 된 toothat 볼륨 그룹에서 hello 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-157">Consequently, if you add only one of hello partitions tooa volume group, all hello other partitions are automatically added toothat volume group at hello same time.</span></span> <span data-ttu-id="b22f9-158">다중 파티션 볼륨 tooa 볼륨 그룹에 추가한 후 hello 다중 파티션 볼륨 계속 toobe 단일 단위로 취급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-158">After you add a multiple partition volume tooa volume group, hello multiple partition volume continues toobe treated as a single unit.</span></span>
      * <span data-ttu-id="b22f9-159">모든 볼륨 toothem 하지 할당 하 여 빈 볼륨 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-159">You can create empty volume groups by not assigning any volumes toothem.</span></span> 
      * <span data-ttu-id="b22f9-160">클러스터 공유 볼륨 (Csv)와 Csv 이외의 hello에 혼합 하지 않는 같은 볼륨 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="b22f9-161">StorSimple 스냅숏 관리자 CSV 볼륨의 혼합을 지원 하지 않으며에서 CSV 이외의 볼륨 hello 같은 스냅숏에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in hello same snapshot.</span></span>
4. <span data-ttu-id="b22f9-162">클릭 **확인** toosave hello 볼륨 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-162">Click **OK** toosave hello volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="b22f9-163">볼륨 그룹 백업</span><span class="sxs-lookup"><span data-stu-id="b22f9-163">Back up a volume group</span></span>
<span data-ttu-id="b22f9-164">볼륨 그룹을 프로시저 tooback 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-164">Use hello following procedure tooback up a volume group.</span></span>

#### <a name="tooback-up-a-volume-group"></a><span data-ttu-id="b22f9-165">볼륨 그룹을 tooback</span><span class="sxs-lookup"><span data-stu-id="b22f9-165">tooback up a volume group</span></span>
1. <span data-ttu-id="b22f9-166">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-166">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="b22f9-167">Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드를 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 **백업 수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-167">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![볼륨 그룹 즉시 백업](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="b22f9-169">Hello에 **백업 수행** 대화 상자에서 **로컬 스냅숏** 또는 **클라우드 스냅숏**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-169">In hello **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![백업 수행 대화 상자](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="b22f9-171">백업 hello tooconfirm 실행 되 고, 확장 hello **작업** 노드를 차례로 클릭 한 다음 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-171">tooconfirm that hello backup is running, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="b22f9-172">hello 백업이 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-172">hello backup should be listed.</span></span>
5. <span data-ttu-id="b22f9-173">완료 tooview hello hello 확장 하 고 스냅숏을 **백업 카탈로그** 노드, hello 볼륨 그룹 이름을 확장 하 고 클릭 **로컬 스냅숏** 또는 **클라우드 스냅숏**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-173">tooview hello completed snapshot, expand hello **Backup Catalog** node, expand hello volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="b22f9-174">성공적으로 완료 되 면 hello 백업이 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-174">hello backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="b22f9-175">볼륨 그룹 편집</span><span class="sxs-lookup"><span data-stu-id="b22f9-175">Edit a volume group</span></span>
<span data-ttu-id="b22f9-176">다음 프로시저 tooedit 볼륨 그룹 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-176">Use hello following procedure tooedit a volume group.</span></span>

#### <a name="tooedit-a-volume-group"></a><span data-ttu-id="b22f9-177">tooedit 볼륨 그룹</span><span class="sxs-lookup"><span data-stu-id="b22f9-177">tooedit a volume group</span></span>
1. <span data-ttu-id="b22f9-178">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-178">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="b22f9-179">Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드를 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-179">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="b22f9-180">hello * * 볼륨 그룹 만들기 * * 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-180">hello **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="b22f9-181">Hello를 변경할 수 있습니다 **이름**, **응용 프로그램**, 및 **볼륨** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-181">You can change hello **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="b22f9-182">클릭 **확인** toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-182">Click **OK** toosave your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="b22f9-183">볼륨 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="b22f9-183">Delete a volume group</span></span>
<span data-ttu-id="b22f9-184">다음 프로시저 toodelete 볼륨 그룹 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-184">Use hello following procedure toodelete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="b22f9-185">Hello 볼륨 그룹과 연결 된 모든 hello 백업이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-185">This also deletes all hello backups associated with hello volume group.</span></span>
> 
> 

#### <a name="toodelete-a-volume-group"></a><span data-ttu-id="b22f9-186">toodelete 볼륨 그룹</span><span class="sxs-lookup"><span data-stu-id="b22f9-186">toodelete a volume group</span></span>
1. <span data-ttu-id="b22f9-187">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-187">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="b22f9-188">Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드를 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-188">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="b22f9-189">hello **볼륨 그룹 삭제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-189">hello **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="b22f9-190">형식 **확인** hello 텍스트 상자와 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-190">Type **Confirm** in hello text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="b22f9-191">hello에 hello 목록에서 볼륨 그룹을 삭제 하는 hello 사라집니다 **결과** 창 및 해당 볼륨 그룹에 연관 된 모든 백업이 hello 백업 카탈로그에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-191">hello deleted volume group vanishes from hello list in hello **Results** pane and all backups that are associated with that volume group are deleted from hello backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b22f9-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b22f9-192">Next steps</span></span>
* <span data-ttu-id="b22f9-193">너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-193">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="b22f9-194">너무 방법에 대해 알아봅니다[toocreate StorSimple 스냅숏 관리자를 사용 하 고 백업 정책 관리](storsimple-snapshot-manager-manage-backup-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b22f9-194">Learn how too[use StorSimple Snapshot Manager toocreate and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

