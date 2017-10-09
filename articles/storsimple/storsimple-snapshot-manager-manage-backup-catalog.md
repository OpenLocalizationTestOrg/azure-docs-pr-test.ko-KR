---
title: "스냅숏 관리자 백업 카탈로그 aaaStorSimple | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooview hello 하 및 hello 백업 카탈로그를 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a><span data-ttu-id="4c630-103">StorSimple 스냅숏 관리자를 사용 하 여 toomanage hello 백업 카탈로그</span><span class="sxs-lookup"><span data-stu-id="4c630-103">Use StorSimple Snapshot Manager toomanage hello backup catalog</span></span>

## <a name="overview"></a><span data-ttu-id="4c630-104">개요</span><span class="sxs-lookup"><span data-stu-id="4c630-104">Overview</span></span>
<span data-ttu-id="4c630-105">hello 기본 기능은 StorSimple 스냅숏 관리자의 tooallow 있습니다 toocreate 응용 프로그램 일치 백업 사본을 스냅숏 형식의 hello에 StorSimple 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-105">hello primary function of StorSimple Snapshot Manager is tooallow you toocreate application-consistent backup copies of StorSimple volumes in hello form of snapshots.</span></span> <span data-ttu-id="4c630-106">스냅숏은 *백업 카탈로그*라는 XML 파일에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-106">Snapshots are then listed in an XML file called a *backup catalog*.</span></span> <span data-ttu-id="4c630-107">hello 백업 카탈로그는 스냅숏을 볼륨 그룹별로 한 다음 로컬 스냅숏 또는 클라우드 스냅숏을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-107">hello backup catalog organizes snapshots by volume group and then by local snapshot or cloud snapshot.</span></span>

<span data-ttu-id="4c630-108">이 자습서에서는 hello를 사용 하는 방법을 설명 **백업 카탈로그** 노드 toocomplete hello 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-108">This tutorial describes how you can use hello **Backup Catalog** node toocomplete hello following tasks:</span></span>

* <span data-ttu-id="4c630-109">볼륨 복원</span><span class="sxs-lookup"><span data-stu-id="4c630-109">Restore a volume</span></span>
* <span data-ttu-id="4c630-110">볼륨 또는 볼륨 그룹 복제</span><span class="sxs-lookup"><span data-stu-id="4c630-110">Clone a volume or volume group</span></span>
* <span data-ttu-id="4c630-111">백업 삭제</span><span class="sxs-lookup"><span data-stu-id="4c630-111">Delete a backup</span></span>
* <span data-ttu-id="4c630-112">파일 복구</span><span class="sxs-lookup"><span data-stu-id="4c630-112">Recover a file</span></span>
* <span data-ttu-id="4c630-113">Hello Storsimple 스냅숏 관리자 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="4c630-113">Restore hello Storsimple Snapshot Manager database</span></span>

<span data-ttu-id="4c630-114">Hello를 확장 하 여 hello 백업 카탈로그를 볼 수 **백업 카탈로그** hello에 대 한 노드 **범위** 창 및 다음 hello 볼륨 그룹을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-114">You can view hello backup catalog by expanding hello **Backup Catalog** node in hello **Scope** pane, and then expanding hello volume group.</span></span>

* <span data-ttu-id="4c630-115">Hello 볼륨 그룹 이름을 클릭 hello **결과** 창 로컬 스냅숏과 클라우드 스냅숏 hello 볼륨 그룹에 사용할 수 있는 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-115">If you click hello volume group name, hello **Results** pane shows hello number of local snapshots and cloud snapshots available for hello volume group.</span></span> 
* <span data-ttu-id="4c630-116">클릭 하면 **로컬 스냅숏** 또는 **클라우드 스냅숏**, hello **결과** 창에는 다음 각 백업 스냅숏에 대 한 정보는 hello 표시 (사용자 에따라**보기** 설정):</span><span class="sxs-lookup"><span data-stu-id="4c630-116">If you click **Local Snapshot** or **Cloud Snapshot**, hello **Results** pane shows hello following information about each backup snapshot (depending on your **View** settings):</span></span>
  
  * <span data-ttu-id="4c630-117">**이름** – hello 시간 hello 스냅숏이 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-117">**Name** – hello time hello snapshot was taken.</span></span>
  * <span data-ttu-id="4c630-118">**유형** – 로컬 스냅숏인지 또는 클라우드 스냅숏인지.</span><span class="sxs-lookup"><span data-stu-id="4c630-118">**Type** – whether this is a local snapshot or a cloud snapshot.</span></span>
  * <span data-ttu-id="4c630-119">**소유자** – hello 콘텐츠 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-119">**Owner** – hello content owner.</span></span> 
  * <span data-ttu-id="4c630-120">**사용 가능한** hello 스냅숏이 현재 사용할 수 있는지 여부를 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-120">**Available** – whether hello snapshot is currently available.</span></span> <span data-ttu-id="4c630-121">**True** 나타내고 해당 hello 스냅숏을 ´ ï ´ 복원할 수 있습니다. **False** 해당 hello 스냅숏을 더 이상 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-121">**True** indicates that hello snapshot is available and can be restored; **False** indicates that hello snapshot is no longer available.</span></span> 
  * <span data-ttu-id="4c630-122">**가져온** – hello 백업을 가져왔는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-122">**Imported** – whether hello backup was imported.</span></span> <span data-ttu-id="4c630-123">**True** hello 백업 hello 서비스 hello 시간 hello 장치에서 StorSimple 스냅숏 관리자에 구성 된 StorSimple 장치 관리자에서에서 가져온 나타냅니다. **False** 를 가져오지 못한 있지만 StorSimple 스냅숏 관리자가 만든 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-123">**True** indicates that hello backup was imported from hello StorSimple Device Manager service at hello time hello device was configured in StorSimple Snapshot Manager; **False** indicates that it was not imported, but was created by StorSimple Snapshot Manager.</span></span> <span data-ttu-id="4c630-124">(쉽게 식별할 수 있습니다는 가져온된 볼륨 그룹 이므로 hello 볼륨 그룹 가져온 hello 장치를 식별 하는 접미사가 추가 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="4c630-124">(You can easily identify an imported volume group because a suffix is added that identifies hello device from which hello volume group was imported.)</span></span>
    
    ![백업 카탈로그](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* <span data-ttu-id="4c630-126">확장 하는 경우 **로컬 스냅숏** 또는 **클라우드 스냅숏**, 누른 다음 개별 스냅숏 이름을 hello **결과** 창 hello 다음 hello에 대 한 정보를 보여 줍니다. 선택한 스냅숏:</span><span class="sxs-lookup"><span data-stu-id="4c630-126">If you expand **Local Snapshot** or **Cloud Snapshot**, and then click an individual snapshot name, hello **Results** pane shows hello following information about hello snapshot that you selected:</span></span>
  
  * <span data-ttu-id="4c630-127">**이름** – 드라이브 문자로 식별 되는 볼륨 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-127">**Name** – hello volume identified by drive letter.</span></span> 
  * <span data-ttu-id="4c630-128">**로컬 이름** – hello hello 드라이브 (사용 가능한 경우)의 로컬 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-128">**Local Name** – hello local name of hello drive (if available).</span></span> 
  * <span data-ttu-id="4c630-129">**장치** – hello는 hello에 볼륨이 있는 hello 장치의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-129">**Device** – hello name of hello device on which hello volume resides.</span></span> 
  * <span data-ttu-id="4c630-130">**사용 가능한** hello 스냅숏이 현재 사용할 수 있는지 여부를 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-130">**Available** – whether hello snapshot is currently available.</span></span> <span data-ttu-id="4c630-131">**True** 나타내고 해당 hello 스냅숏을 ´ ï ´ 복원할 수 있습니다. **False** 해당 hello 스냅숏을 더 이상 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-131">**True** indicates that hello snapshot is available and can be restored; **False** indicates that hello snapshot is no longer available.</span></span> 

## <a name="restore-a-volume"></a><span data-ttu-id="4c630-132">볼륨 복원</span><span class="sxs-lookup"><span data-stu-id="4c630-132">Restore a volume</span></span>
<span data-ttu-id="4c630-133">Hello 프로시저 toorestore 볼륨을 백업에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-133">Use hello following procedure toorestore a volume from backup.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="4c630-134">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4c630-134">Prerequisites</span></span>
<span data-ttu-id="4c630-135">이미 수행 하는 경우 볼륨 및 볼륨 그룹을 만들고 hello 볼륨을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-135">If you have not already done so, create a volume and volume group, and then delete hello volume.</span></span> <span data-ttu-id="4c630-136">기본적으로 toobe 삭제를 허용 하기 전에 StorSimple 스냅숏 관리자 볼륨을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-136">By default, StorSimple Snapshot Manager backs up a volume before permitting it toobe deleted.</span></span> <span data-ttu-id="4c630-137">이 예방 조치로 hello 볼륨을 실수로 삭제 하거나 hello 데이터 toobe 어떤 이유로 든 복구할 경우 데이터 손실을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-137">This precaution can prevent data loss if hello volume is deleted unintentionally or if hello data needs toobe recovered for any reason.</span></span> 

<span data-ttu-id="4c630-138">StorSimple 스냅숏 관리자 hello hello 문제 예방용 백업을 생성 되는 동안 메시지의 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-138">StorSimple Snapshot Manager displays hello following message while it creates hello precautionary backup.</span></span>

![자동 스냅숏 메시지](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> <span data-ttu-id="4c630-140">볼륨 그룹에 속해 있는 볼륨은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-140">You cannot delete a volume that is part of a volume group.</span></span> <span data-ttu-id="4c630-141">hello 삭제 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-141">hello delete option is unavailable.</span></span> <br>
> 
> 

#### <a name="toorestore-a-volume"></a><span data-ttu-id="4c630-142">toorestore 볼륨</span><span class="sxs-lookup"><span data-stu-id="4c630-142">toorestore a volume</span></span>
1. <span data-ttu-id="4c630-143">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-143">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="4c630-144">Hello에 **범위** 창의 hello 확장 **백업 카탈로그** 노드, 볼륨 그룹을 확장 하 고 클릭 **로컬 스냅숏** 또는 **클라우드 스냅숏**.</span><span class="sxs-lookup"><span data-stu-id="4c630-144">In hello **Scope** pane, expand hello **Backup Catalog** node, expand a volume group, and then click **Local Snapshots** or **Cloud Snapshots**.</span></span> <span data-ttu-id="4c630-145">백업 스냅숏 목록이 hello에 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="4c630-145">A list of backup snapshots appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="4c630-146">찾기 hello 백업 toorestore 마우스 오른쪽 단추를 클릭 한 다음 원하는 **복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-146">Find hello backup that you want toorestore, right-click, and then click **Restore**.</span></span>
   
    ![백업 카탈로그 복원](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. <span data-ttu-id="4c630-148">Hello 확인 페이지에서 hello 세부 사항 입력 **확인**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-148">On hello confirmation page, review hello details, type **Confirm**, and then click **OK**.</span></span> <span data-ttu-id="4c630-149">StorSimple 스냅숏 관리자 hello 백업 toorestore hello 볼륨을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-149">StorSimple Snapshot Manager uses hello backup toorestore hello volume.</span></span>
   
    ![확인 메시지 복원](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. <span data-ttu-id="4c630-151">실행할 때 hello 복원 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-151">You can monitor hello restore action as it runs.</span></span> <span data-ttu-id="4c630-152">Hello에 **범위** 창의 hello 확장 **작업** 노드를 차례로 클릭 한 다음 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-152">In hello **Scope** pane, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="4c630-153">hello에 hello 작업 세부 정보 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="4c630-153">hello job details appear in hello **Results** pane.</span></span> <span data-ttu-id="4c630-154">Hello 작업 세부 정보는 전송 된 toohello hello 복원 작업이 완료 되 면 **마지막 24 시간** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-154">When hello restore job is finished, hello job details are transferred toohello **Last 24 hours** list.</span></span>

## <a name="clone-a-volume-or-volume-group"></a><span data-ttu-id="4c630-155">볼륨 또는 볼륨 그룹 복제</span><span class="sxs-lookup"><span data-stu-id="4c630-155">Clone a volume or volume group</span></span>
<span data-ttu-id="4c630-156">다음 프로시저 toocreate 볼륨 또는 볼륨 그룹의 복제본 (클론) hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-156">Use hello following procedure toocreate a duplicate (clone) of a volume or volume group.</span></span>

#### <a name="tooclone-a-volume-or-volume-group"></a><span data-ttu-id="4c630-157">tooclone 볼륨 또는 볼륨 그룹</span><span class="sxs-lookup"><span data-stu-id="4c630-157">tooclone a volume or volume group</span></span>
1. <span data-ttu-id="4c630-158">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-158">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="4c630-159">Hello에 **범위** 창의 hello 확장 **백업 카탈로그** 노드, 볼륨 그룹을 확장 하 고 클릭 **클라우드 스냅숏**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-159">In hello **Scope** pane, expand hello **Backup Catalog** node, expand a volume group, and then click **Cloud Snapshots**.</span></span> <span data-ttu-id="4c630-160">Hello에 백업 목록이 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="4c630-160">A list of backups appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="4c630-161">Hello 볼륨 또는 볼륨 그룹을 클릭 하 고 tooclone, 마우스 오른쪽 단추로 클릭 hello 볼륨 또는 볼륨 그룹 이름을 지정 하 찾기 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-161">Find hello volume or volume group that you want tooclone, right-click hello volume or volume group name, and click **Clone**.</span></span> <span data-ttu-id="4c630-162">hello **클라우드 스냅숏 복제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-162">hello **Clone Cloud Snapshot** dialog box appears.</span></span>
   
    ![클라우드 스냅숏 복제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. <span data-ttu-id="4c630-164">전체 hello **클라우드 스냅숏 복제** 다음과 같이 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="4c630-164">Complete hello **Clone Cloud Snapshot** dialog box as follows:</span></span> 
   
   1. <span data-ttu-id="4c630-165">Hello에 **이름** 입력란 hello에 대 한 이름 입력 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-165">In hello **Name** text box, type a name for hello cloned volume.</span></span> <span data-ttu-id="4c630-166">이 이름은 hello에 나타납니다. **볼륨** 노드.</span><span class="sxs-lookup"><span data-stu-id="4c630-166">This name will appear in hello **Volumes** node.</span></span> 
   2. <span data-ttu-id="4c630-167">(선택 사항) 선택 **드라이브**, hello 드롭 다운 목록에서 드라이브 문자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-167">(Optional) select **Drive**, and then select a drive letter from hello drop-down list.</span></span>
   3. <span data-ttu-id="4c630-168">(선택 사항) 선택 **폴더 (NTFS)**, 및 폴더 경로 입력 하거나 찾아보기를 클릭 하 고 hello 폴더에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-168">(Optional) select **Folder (NTFS)**, and type a folder path or click Browse and select a location for hello folder.</span></span> 
   4. <span data-ttu-id="4c630-169">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-169">Click **Create**.</span></span>
5. <span data-ttu-id="4c630-170">Hello 복제 프로세스가 완료 되 면 hello 복제 볼륨을 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-170">When hello cloning process is finished, you must initialize hello cloned volume.</span></span> <span data-ttu-id="4c630-171">서버 관리자를 시작한 다음 디스크 관리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-171">Start Server Manager, and then start Disk Management.</span></span> <span data-ttu-id="4c630-172">자세한 지침은 [볼륨 탑재](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c630-172">For detailed instructions, see [Mount volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes).</span></span> <span data-ttu-id="4c630-173">초기화 되 면 hello 볼륨 hello 나열 됩니다 **볼륨** hello에 대 한 노드 **범위** 창.</span><span class="sxs-lookup"><span data-stu-id="4c630-173">After it is initialized, hello volume will be listed under hello **Volumes** node in hello **Scope** pane.</span></span> <span data-ttu-id="4c630-174">Hello 볼륨이 나열 되어 표시 되지 않으면 hello 볼륨 목록을 새로 고칩니다 (마우스 오른쪽 단추 클릭 hello **볼륨** 노드를 차례로 클릭 한 다음 **새로 고침**).</span><span class="sxs-lookup"><span data-stu-id="4c630-174">If you do not see hello volume listed, refresh hello list of volumes (right-click hello **Volumes** node, and then click **Refresh**).</span></span>

## <a name="delete-a-backup"></a><span data-ttu-id="4c630-175">백업 삭제</span><span class="sxs-lookup"><span data-stu-id="4c630-175">Delete a backup</span></span>
<span data-ttu-id="4c630-176">Hello 프로시저 toodelete 스냅숏으로 hello 백업 카탈로그에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-176">Use hello following procedure toodelete a snapshot from hello backup catalog.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c630-177">Hello 스냅숏와 관련 된 데이터를 백업 하는 hello를 삭제에서 스냅숏을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-177">Deleting a snapshot deletes hello backed up data associated with hello snapshot.</span></span> <span data-ttu-id="4c630-178">그러나 hello hello 클라우드에서 데이터 정리 프로세스는 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-178">However, hello process of cleaning up data from hello cloud may take some time.</span></span><br>


#### <a name="toodelete-a-backup"></a><span data-ttu-id="4c630-179">toodelete 백업</span><span class="sxs-lookup"><span data-stu-id="4c630-179">toodelete a backup</span></span>
1. <span data-ttu-id="4c630-180">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-180">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="4c630-181">Hello에 **범위** 창의 hello 확장 **백업 카탈로그** 노드, 볼륨 그룹을 확장 하 고 클릭 **로컬 스냅숏** 또는 **클라우드 스냅숏**.</span><span class="sxs-lookup"><span data-stu-id="4c630-181">In hello **Scope** pane, expand hello **Backup Catalog** node, expand a volume group, and then click **Local Snapshots** or **Cloud Snapshots**.</span></span> <span data-ttu-id="4c630-182">Hello에 스냅숏 목록이 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="4c630-182">A list of snapshots appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="4c630-183">마우스 오른쪽 단추로 클릭 hello 스냅숏 toodelete을 차례로 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-183">Right-click hello snapshot you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="4c630-184">Hello 확인 메시지가 나타나면 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-184">When hello confirmation message appears, click **OK**.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="4c630-185">파일 복구</span><span class="sxs-lookup"><span data-stu-id="4c630-185">Recover a file</span></span>
<span data-ttu-id="4c630-186">볼륨에서 파일을 실수로 삭제 되는 경우 이전 hello 삭제, 스냅숏 toocreate hello를 사용 하 여 날짜 스냅숏 hello 볼륨의 복제본을 검색 하 여 hello 파일을 복구할 수 있습니다 및 복제 볼륨 toohello 원래 볼륨 hello hello 파일을 복사 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-186">If a file is accidentally deleted from a volume, you can recover hello file by retrieving a snapshot that pre-dates hello deletion, using hello snapshot toocreate a clone of hello volume, and then copying hello file from hello cloned volume toohello original volume.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="4c630-187">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4c630-187">Prerequisites</span></span>
<span data-ttu-id="4c630-188">시작 하기 전에 hello 볼륨 그룹의 최신 백업이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-188">Before you begin, make sure that you have a current backup of hello volume group.</span></span> <span data-ttu-id="4c630-189">그런 다음 해당 볼륨 그룹의 hello 볼륨 중 하나에 저장 된 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-189">Then, delete a file stored on one of hello volumes in that volume group.</span></span> <span data-ttu-id="4c630-190">마지막으로 사용 하 여 hello toorestore hello 단계를 수행 하려면 백업에서 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-190">Finally, use hello following steps toorestore hello deleted file from your backup.</span></span> 

#### <a name="toorecover-a-deleted-file"></a><span data-ttu-id="4c630-191">toorecover 삭제 된 파일</span><span class="sxs-lookup"><span data-stu-id="4c630-191">toorecover a deleted file</span></span>
1. <span data-ttu-id="4c630-192">바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-192">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="4c630-193">hello StorSimple 스냅숏 관리자 콘솔 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-193">hello StorSimple Snapshot Manager console window appears.</span></span> 
2. <span data-ttu-id="4c630-194">Hello에 **범위** 창 hello 확장 **백업 카탈로그** 노드와 찾아보기 tooa 스냅숏을 삭제 하는 hello 파일이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-194">In hello **Scope** pane, expand hello **Backup Catalog** node, and browse tooa snapshot that contains hello deleted file.</span></span> <span data-ttu-id="4c630-195">일반적으로 hello 삭제 되기 바로 전에 만든 스냅숏을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-195">Typically, you should select a snapshot that was created just before hello deletion.</span></span>
3. <span data-ttu-id="4c630-196">찾기 hello 볼륨 tooclone 마우스 오른쪽 단추를 클릭 하 여 원하는 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-196">Find hello volume that you want tooclone, right-click, and click **Clone**.</span></span> <span data-ttu-id="4c630-197">hello **클라우드 스냅숏 복제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-197">hello **Clone Cloud Snapshot** dialog box appears.</span></span>
   
    ![클라우드 스냅숏 복제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. <span data-ttu-id="4c630-199">전체 hello **클라우드 스냅숏 복제** 다음과 같이 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="4c630-199">Complete hello **Clone Cloud Snapshot** dialog box as follows:</span></span> 
   
   1. <span data-ttu-id="4c630-200">Hello에 **이름** 입력란 hello에 대 한 이름 입력 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-200">In hello **Name** text box, type a name for hello cloned volume.</span></span> <span data-ttu-id="4c630-201">이 이름은 hello에 나타납니다. **볼륨** 노드.</span><span class="sxs-lookup"><span data-stu-id="4c630-201">This name will appear in hello **Volumes** node.</span></span> 
   2. <span data-ttu-id="4c630-202">(선택 사항) 선택 **드라이브**, hello 드롭 다운 목록에서 드라이브 문자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-202">(Optional) Select **Drive**, and then select a drive letter from hello drop-down list.</span></span> 
   3. <span data-ttu-id="4c630-203">(선택 사항) 선택 **폴더 (NTFS)**, 폴더 경로 입력 하거나 클릭 하 고 **찾아보기** hello 폴더의 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-203">(Optional) Select **Folder (NTFS)**, and type a folder path or click **Browse** and select a location for hello folder.</span></span> 
   4. <span data-ttu-id="4c630-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-204">Click **Create**.</span></span> 
5. <span data-ttu-id="4c630-205">Hello 복제 프로세스가 완료 되 면 hello 복제 볼륨을 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-205">When hello cloning process is finished, you must initialize hello cloned volume.</span></span> <span data-ttu-id="4c630-206">서버 관리자를 시작한 다음 디스크 관리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-206">Start Server Manager, and then start Disk Management.</span></span> <span data-ttu-id="4c630-207">자세한 지침은 [볼륨 탑재](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c630-207">For detailed instructions, see [Mount volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes).</span></span> <span data-ttu-id="4c630-208">초기화 되 면 hello 볼륨 hello 나열 됩니다 **볼륨** hello에 대 한 노드 **범위** 창.</span><span class="sxs-lookup"><span data-stu-id="4c630-208">After it is initialized, hello volume will be listed under hello **Volumes** node in hello **Scope** pane.</span></span> 
   
    <span data-ttu-id="4c630-209">Hello 볼륨이 나열 되어 표시 되지 않으면 hello 볼륨 목록을 새로 고칩니다 (마우스 오른쪽 단추 클릭 hello **볼륨** 노드를 차례로 클릭 한 다음 **새로 고침**).</span><span class="sxs-lookup"><span data-stu-id="4c630-209">If you do not see hello volume listed, refresh hello list of volumes (right-click hello **Volumes** node, and then click **Refresh**).</span></span>
6. <span data-ttu-id="4c630-210">Hello 복제 볼륨을 포함 하는 hello open NTFS 폴더 확장 hello **볼륨** 노드를 차례로 연 다음 hello 복제 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-210">Open hello NTFS folder that contains hello cloned volume, expand hello **Volumes** node, and then open hello cloned volume.</span></span> <span data-ttu-id="4c630-211">Toorecover, 원하는 toohello 기본 볼륨을 복사 하는 hello 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-211">Find hello file that you want toorecover, and copy it toohello primary volume.</span></span>
7. <span data-ttu-id="4c630-212">Hello 파일을 복원한 후에 hello 복제 볼륨을 포함 하는 hello NTFS 폴더를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-212">After you restore hello file, you can delete hello NTFS folder that contains hello cloned volume.</span></span>

## <a name="restore-hello-storsimple-snapshot-manager-database"></a><span data-ttu-id="4c630-213">Hello StorSimple 스냅숏 관리자 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="4c630-213">Restore hello StorSimple Snapshot Manager database</span></span>
<span data-ttu-id="4c630-214">Hello StorSimple 스냅숏 관리자 데이터베이스 hello 호스트 컴퓨터에서 정기적으로 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-214">You should regularly back up hello StorSimple Snapshot Manager database on hello host computer.</span></span> <span data-ttu-id="4c630-215">재해가 발생 또는 hello 호스트 컴퓨터에서 어떤 이유로 든 오류가 발생 하는 경우 hello 백업에서 다음 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-215">If a disaster occurs or hello host computer fails for any reason, you can then restore it from hello backup.</span></span> <span data-ttu-id="4c630-216">Hello 데이터베이스 백업 만들기는 수동 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-216">Creating hello database backup is a manual process.</span></span>

#### <a name="tooback-up-and-restore-hello-database"></a><span data-ttu-id="4c630-217">tooback 및 hello 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="4c630-217">tooback up and restore hello database</span></span>
1. <span data-ttu-id="4c630-218">Hello Microsoft StorSimple 관리 서비스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-218">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="4c630-219">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-219">Start Server Manager.</span></span>
   2. <span data-ttu-id="4c630-220">Hello에 hello 서버 관리자 대시보드의 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-220">On hello Server Manager dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="4c630-221">Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-221">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="4c630-222">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-222">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
2. <span data-ttu-id="4c630-223">Hello 호스트 컴퓨터에서 tooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-223">On hello host computer, browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4c630-224">ProgramData는 숨겨진 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-224">ProgramData is a hidden folder.</span></span>
   > 
   > 
3. <span data-ttu-id="4c630-225">Hello 클라우드 또는 안전한 장소에 hello 카탈로그 XML 파일, 복사 hello 파일 및 저장소 hello 복사본을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-225">Find hello catalog XML file, copy hello file, and store hello copy in a safe location or in hello cloud.</span></span> <span data-ttu-id="4c630-226">Hello 호스트가 실패 하면이 백업 파일 toohelp 복구 hello 백업 만든 정책을 StorSimple 스냅숏 관리자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-226">If hello host fails, you can use this backup file toohelp recover hello backup policies that you created in StorSimple Snapshot Manager.</span></span>
   
    ![Azure StorSimple 백업 카탈로그 파일](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. <span data-ttu-id="4c630-228">Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-228">Restart hello Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="4c630-229">Hello에 hello 서버 관리자 대시보드의 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-229">On hello Server Manager dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="4c630-230">Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-230">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="4c630-231">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-231">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span>
5. <span data-ttu-id="4c630-232">Hello 호스트 컴퓨터에서 tooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-232">On hello host computer, browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
6. <span data-ttu-id="4c630-233">Hello 카탈로그 XML 파일을 삭제 하 고 만든 hello 백업 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-233">Delete hello catalog XML file, and replace it with hello backup version that you created.</span></span> 
7. <span data-ttu-id="4c630-234">Hello 데스크톱 StorSimple 스냅숏 관리자 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-234">Click hello desktop StorSimple Snapshot Manager icon toostart StorSimple Snapshot Manager.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c630-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c630-235">Next steps</span></span>
* <span data-ttu-id="4c630-236">에 대 한 자세한 내용은 [StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-236">Learn more about [using StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="4c630-237">[StorSimple 스냅숏 관리자 작업 및 워크플로](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c630-237">Learn more about [StorSimple Snapshot Manager tasks and workflows](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).</span></span>

