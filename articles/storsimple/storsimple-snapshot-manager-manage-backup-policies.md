---
title: "aaaStorSimple 스냅숏 관리자에 대 한 백업 정책 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 toocreate hello 하 및 예약 된 백업 제어 하는 hello 백업 정책을 관리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="94ec5-103">StorSimple 스냅숏 관리자 toocreate를 사용 하 고 백업 정책 관리</span><span class="sxs-lookup"><span data-stu-id="94ec5-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="94ec5-104">개요</span><span class="sxs-lookup"><span data-stu-id="94ec5-104">Overview</span></span>
<span data-ttu-id="94ec5-105">백업 정책을 로컬로 또는 hello 클라우드에 볼륨 데이터를 백업 하기 위한 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="94ec5-106">백업 정책을 만들 때 보존 정책을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="94ec5-107">(최대 64개의 스냅숏을 유지할 수 있습니다.) 백업 정책에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 솔루션](storsimple-overview.md)에서 [백업 형식](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94ec5-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="94ec5-108">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="94ec5-109">백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="94ec5-109">Create a backup policy</span></span>
* <span data-ttu-id="94ec5-110">백업 정책 편집</span><span class="sxs-lookup"><span data-stu-id="94ec5-110">Edit a backup policy</span></span>
* <span data-ttu-id="94ec5-111">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="94ec5-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="94ec5-112">백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="94ec5-112">Create a backup policy</span></span>
<span data-ttu-id="94ec5-113">다음 프로시저 toocreate 새 백업 정책을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="94ec5-114">백업 정책 toocreate</span><span class="sxs-lookup"><span data-stu-id="94ec5-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="94ec5-115">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="94ec5-116">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **백업 정책**를 클릭 하 고 **백업 정책 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![백업 정책 만들기](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="94ec5-118">hello **정책 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-118">hello **Create a Policy** dialog box appears.</span></span>

    ![정책 만들기 - 일반 탭](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="94ec5-120">Hello에 **일반** 탭, 다음 정보는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="94ec5-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="94ec5-121">Hello에 **이름** 입력란 hello 정책에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="94ec5-122">Hello에 **볼륨 그룹** 텍스트 상자 hello 정책과 연결 된 hello 볼륨 그룹의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="94ec5-123">**로컬 스냅숏** 또는 **클라우드 스냅숏** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="94ec5-124">스냅숏 tooretain hello 수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="94ec5-125">선택 하는 경우 **모든**, 64 개의 스냅숏을 유지 됩니다 (최대 hello).</span><span class="sxs-lookup"><span data-stu-id="94ec5-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="94ec5-126">Hello 클릭 **일정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-126">Click hello **Schedule** tab.</span></span>

    ![정책 만들기 - 일정 탭](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="94ec5-128">Hello에 **일정** 탭, 다음 정보는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="94ec5-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="94ec5-129">Hello 클릭 **사용** 확인란 tooschedule hello에 대 한 다음 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="94ec5-130">**설정** 아래에서 **한 번**, **매일**, **매주** 또는 **매월**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="94ec5-131">Hello에 **시작** 텍스트 상자 hello 달력 아이콘을 클릭 하 고 시작 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="94ec5-132">**고급 설정**아래에서 선택적 반복 일정과 종료 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="94ec5-133">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-133">Click **OK**.</span></span>

<span data-ttu-id="94ec5-134">다음 정보는 hello hello에 표시 되는 백업 정책을 만든 후 **결과** 창:</span><span class="sxs-lookup"><span data-stu-id="94ec5-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="94ec5-135">**이름** – hello 백업 정책의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="94ec5-136">**유형** – 로컬 스냅숏 또는 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="94ec5-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="94ec5-137">**볼륨 그룹** – hello hello 정책과 연결 된 볼륨 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="94ec5-138">**보존** – hello 보유 스냅숏 개수; hello 최대 64입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="94ec5-139">**만든** – hello이이 정책이 생성 된 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="94ec5-140">**활성화** hello 정책 현재 적용 되는지 여부를 –: **True** 있음을 나타냅니다. **False** 적용에서 하지 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="94ec5-141">백업 정책 편집</span><span class="sxs-lookup"><span data-stu-id="94ec5-141">Edit a backup policy</span></span>
<span data-ttu-id="94ec5-142">다음 프로시저 tooedit 기존 백업 정책이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="94ec5-143">백업 정책 tooedit</span><span class="sxs-lookup"><span data-stu-id="94ec5-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="94ec5-144">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="94ec5-145">Hello에 **범위** 창의 hello 클릭 **백업 정책** 노드.</span><span class="sxs-lookup"><span data-stu-id="94ec5-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="94ec5-146">Hello에 모든 hello 백업 정책 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="94ec5-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="94ec5-147">Hello 정책 tooedit를 원하고 클릭을 마우스 오른쪽 단추로 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![백업 정책 편집](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="94ec5-149">Hello 때 **정책 만들기** 창이 나타나면 변경 내용을 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="94ec5-150">백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="94ec5-150">Delete a backup policy</span></span>
<span data-ttu-id="94ec5-151">다음 프로시저 toodelete 백업 정책을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="94ec5-152">백업 정책 toodelete</span><span class="sxs-lookup"><span data-stu-id="94ec5-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="94ec5-153">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="94ec5-154">Hello에 **범위** 창의 hello 클릭 **백업 정책** 노드.</span><span class="sxs-lookup"><span data-stu-id="94ec5-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="94ec5-155">Hello에 모든 hello 백업 정책 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="94ec5-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="94ec5-156">Hello toodelete를 원하고 클릭 한 다음 백업 정책을 마우스 오른쪽 단추로 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="94ec5-157">Hello 확인 메시지가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![백업 정책 삭제 확인](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="94ec5-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94ec5-159">Next steps</span></span>
* <span data-ttu-id="94ec5-160">너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="94ec5-161">너무 방법에 대해 알아봅니다[tooview StorSimple 스냅숏 관리자를 사용 하 고 백업 작업을 관리](storsimple-snapshot-manager-manage-backup-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec5-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
