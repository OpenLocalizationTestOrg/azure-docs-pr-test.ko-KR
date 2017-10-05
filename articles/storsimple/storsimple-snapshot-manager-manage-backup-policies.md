---
title: "StorSimple Snapshot Manager 백업 정책 | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 MMC 스냅인을 사용하여 예약된 백업을 제어하는 백업 정책을 만들고 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="47b1a-103">StorSimple 스냅숏 관리자를 사용하여 백업 정책 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="47b1a-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="47b1a-104">개요</span><span class="sxs-lookup"><span data-stu-id="47b1a-104">Overview</span></span>
<span data-ttu-id="47b1a-105">백업 정책은 로컬로 또는 클라우드에 볼륨 데이터를 백업하기 위한 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="47b1a-106">백업 정책을 만들 때 보존 정책을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="47b1a-107">(최대 64개의 스냅숏을 유지할 수 있습니다.) 백업 정책에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 솔루션](storsimple-overview.md)에서 [백업 형식](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47b1a-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="47b1a-108">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="47b1a-109">백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="47b1a-109">Create a backup policy</span></span>
* <span data-ttu-id="47b1a-110">백업 정책 편집</span><span class="sxs-lookup"><span data-stu-id="47b1a-110">Edit a backup policy</span></span>
* <span data-ttu-id="47b1a-111">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="47b1a-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="47b1a-112">백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="47b1a-112">Create a backup policy</span></span>
<span data-ttu-id="47b1a-113">다음 절차에 따라 새 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="47b1a-114">백업 정책을 만들려면</span><span class="sxs-lookup"><span data-stu-id="47b1a-114">To create a backup policy</span></span>
1. <span data-ttu-id="47b1a-115">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="47b1a-116">**범위** 창에서 **백업 정책**을 마우스 오른쪽 단추로 클릭하고 **백업 정책 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![백업 정책 만들기](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="47b1a-118">**정책 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-118">The **Create a Policy** dialog box appears.</span></span>

    ![정책 만들기 - 일반 탭](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="47b1a-120">**일반** 탭에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="47b1a-121">**이름** 텍스트 상자에 정책 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="47b1a-122">**볼륨 그룹** 텍스트 상자에 정책과 연결된 볼륨 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="47b1a-123">**로컬 스냅숏** 또는 **클라우드 스냅숏** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="47b1a-124">보존할 스냅숏 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="47b1a-125">**모두**를 선택하면 64개의 스냅숏이 보존됩니다(최대값).</span><span class="sxs-lookup"><span data-stu-id="47b1a-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="47b1a-126">**일정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-126">Click the **Schedule** tab.</span></span>

    ![정책 만들기 - 일정 탭](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="47b1a-128">**일정** 탭에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="47b1a-129">**사용** 확인란을 클릭하여 다음 백업 일정을 정합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="47b1a-130">**설정** 아래에서 **한 번**, **매일**, **매주** 또는 **매월**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="47b1a-131">**시작** 텍스트 상자에서 달력 아이콘을 클릭하고 시작 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="47b1a-132">**고급 설정**아래에서 선택적 반복 일정과 종료 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="47b1a-133">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-133">Click **OK**.</span></span>

<span data-ttu-id="47b1a-134">백업 정책을 만든 후 **결과** 창에 다음 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="47b1a-135">**이름** – 백업 정책의 이름</span><span class="sxs-lookup"><span data-stu-id="47b1a-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="47b1a-136">**유형** – 로컬 스냅숏 또는 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="47b1a-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="47b1a-137">**볼륨 그룹** – 정책과 연결된 볼륨 그룹</span><span class="sxs-lookup"><span data-stu-id="47b1a-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="47b1a-138">**보존** - 보존되는 스냅숏 개수로, 최대 64개</span><span class="sxs-lookup"><span data-stu-id="47b1a-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="47b1a-139">**만든 날짜** - 이 정책을 만든 날짜</span><span class="sxs-lookup"><span data-stu-id="47b1a-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="47b1a-140">**사용** - 정책이 현재 적용되는지 여부. **True**는 적용되고 있음을 나타냅니다. **False**는 적용되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="47b1a-141">백업 정책 편집</span><span class="sxs-lookup"><span data-stu-id="47b1a-141">Edit a backup policy</span></span>
<span data-ttu-id="47b1a-142">다음 절차에 따라 기존 백업 정책을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="47b1a-143">백업 정책을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="47b1a-143">To edit a backup policy</span></span>
1. <span data-ttu-id="47b1a-144">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="47b1a-145">**범위** 창에서 **백업 정책** 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="47b1a-146">모든 백업 정책이 **결과** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="47b1a-147">편집할 정책을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![백업 정책 편집](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="47b1a-149">**정책 만들기** 창이 나타나면 변경 내용을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="47b1a-150">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="47b1a-150">Delete a backup policy</span></span>
<span data-ttu-id="47b1a-151">다음 절차에 따라 백업 정책을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="47b1a-152">백업 정책을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="47b1a-152">To delete a backup policy</span></span>
1. <span data-ttu-id="47b1a-153">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="47b1a-154">**범위** 창에서 **백업 정책** 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="47b1a-155">모든 백업 정책이 **결과** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="47b1a-156">삭제할 백업 정책을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="47b1a-157">확인 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-157">When the confirmation message appears, click **Yes**.</span></span>

    ![백업 정책 삭제 확인](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="47b1a-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47b1a-159">Next steps</span></span>
* <span data-ttu-id="47b1a-160">[StorSimple 스냅숏 관리자를 사용하여 StorSimple 솔루션을 관리](storsimple-snapshot-manager-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="47b1a-161">[StorSimple 스냅숏 관리자를 사용하여 백업 작업을 보고 관리](storsimple-snapshot-manager-manage-backup-jobs.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47b1a-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
