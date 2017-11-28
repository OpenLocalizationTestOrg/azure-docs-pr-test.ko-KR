---
title: "aaaStorSimple 스냅숏 관리자 및 볼륨 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooview hello 하 및 볼륨과 tooconfigure 백업을 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a><span data-ttu-id="83405-103">StorSimple 스냅숏 관리자 tooview를 사용 하 고 볼륨 관리</span><span class="sxs-lookup"><span data-stu-id="83405-103">Use StorSimple Snapshot Manager tooview and manage volumes</span></span>
## <a name="overview"></a><span data-ttu-id="83405-104">개요</span><span class="sxs-lookup"><span data-stu-id="83405-104">Overview</span></span>
<span data-ttu-id="83405-105">Hello StorSimple 스냅숏 관리자를 사용할 수 있습니다 **볼륨** 노드 (hello에 **범위** 창) tooselect 볼륨에 대 한 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-105">You can use hello StorSimple Snapshot Manager **Volumes** node (on hello **Scope** pane) tooselect volumes and view information about them.</span></span> <span data-ttu-id="83405-106">hello 볼륨 toohello 볼륨 탑재 hello 호스트에서 해당 하는 드라이브로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-106">hello volumes are presented as drives that correspond toohello volumes mounted by hello host.</span></span> <span data-ttu-id="83405-107">hello **볼륨** 로컬 볼륨 및 볼륨 유형을 hello iSCSI와 장치 사용을 통해 검색 한 볼륨을 포함 하 여 StorSimple에서 지원 되는 노드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83405-107">hello **Volumes** node shows local volumes and volume types that are supported by StorSimple, including volumes discovered through hello use of iSCSI and a device.</span></span> 

<span data-ttu-id="83405-108">지원 되는 볼륨에 대 한 자세한 내용은 이동 너무[여러 볼륨 유형에 대 한 지원](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-108">For more information about supported volumes, go too[Support for multiple volume types](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).</span></span>

![결과 창의 볼륨 목록](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

<span data-ttu-id="83405-110">hello **볼륨** 노드 수도 있습니다를 다시 검색 하거나 StorSimple 스냅숏 관리자에서 검색 한 후 볼륨을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-110">hello **Volumes** node also lets you rescan or delete volumes after StorSimple Snapshot Manager discovers them.</span></span> 

<span data-ttu-id="83405-111">이 자습서에서는 볼륨을 탑재, 초기화 및 포맷한 다음 StorSimple Snapshot Manager를 사용하여 다음 작업을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-111">This tutorial explains how you can mount, initialize, and format volumes and then use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="83405-112">볼륨에 대한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="83405-112">View information about volumes</span></span> 
* <span data-ttu-id="83405-113">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="83405-113">Delete volumes</span></span>
* <span data-ttu-id="83405-114">볼륨 다시 검사</span><span class="sxs-lookup"><span data-stu-id="83405-114">Rescan volumes</span></span> 
* <span data-ttu-id="83405-115">기본 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="83405-115">Configure a basic volume and back it up</span></span>
* <span data-ttu-id="83405-116">동적 미러 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="83405-116">Configure a dynamic mirrored volume and back it up</span></span>

> [!NOTE]
> <span data-ttu-id="83405-117">모든 hello **볼륨** 노드 작업은 또한 hello에서 사용할 수 있는 **동작** 창.</span><span class="sxs-lookup"><span data-stu-id="83405-117">All of hello **Volume** node actions are also available in hello **Actions** pane.</span></span>
> 
> 

## <a name="mount-volumes"></a><span data-ttu-id="83405-118">볼륨 탑재</span><span class="sxs-lookup"><span data-stu-id="83405-118">Mount volumes</span></span>
<span data-ttu-id="83405-119">사용 하 여 hello 프로시저 toomount 다음 초기화 및 StorSimple 볼륨을 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-119">Use hello following procedure toomount, initialize, and format StorSimple volumes.</span></span> <span data-ttu-id="83405-120">이 프로시저는 디스크 관리를 하드 디스크 및 hello 해당 볼륨이 나 파티션을 관리 하기 위한 시스템 유틸리티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-120">This procedure uses Disk Management, a system utility for managing hard disks and hello corresponding volumes or partitions.</span></span> <span data-ttu-id="83405-121">디스크 관리에 대 한 자세한 내용은 이동 너무[디스크 관리](https://technet.microsoft.com/library/cc770943.aspx) hello Microsoft TechNet 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-121">For more information about Disk Management, go too[Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on hello Microsoft TechNet website.</span></span>

#### <a name="toomount-volumes"></a><span data-ttu-id="83405-122">toomount 볼륨</span><span class="sxs-lookup"><span data-stu-id="83405-122">toomount volumes</span></span>
1. <span data-ttu-id="83405-123">호스트 컴퓨터에서 hello Microsoft iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-123">On your host computer, start hello Microsoft iSCSI initiator.</span></span>
2. <span data-ttu-id="83405-124">대상 포털 hello hello 인터페이스 IP 주소 또는 검색 IP 주소 중 하나를 제공 하 고 toohello 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-124">Supply one of hello interface IP addresses as hello target portal or discovery IP address, and connect toohello device.</span></span> <span data-ttu-id="83405-125">Hello 장치가 연결 된 hello 볼륨 tooyour 액세스할 수 있는 Windows 시스템 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-125">After hello device is connected, hello volumes will be accessible tooyour Windows system.</span></span> <span data-ttu-id="83405-126">Hello Microsoft iSCSI 초기자를 사용 하는 방법에 대 한 자세한 내용은 "연결 tooan iSCSI 대상 장치" toohello 섹션에서 go [iSCSI 초기자 설치 및 구성 하는 Microsoft][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-126">For more information about using hello Microsoft iSCSI initiator, go toohello section “Connecting tooan iSCSI target device” in [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
3. <span data-ttu-id="83405-127">Hello 옵션 toostart 디스크 관리를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-127">Use any of hello following options toostart Disk Management:</span></span>
   
   * <span data-ttu-id="83405-128">Hello에 Diskmgmt.msc 입력 **실행** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-128">Type Diskmgmt.msc in hello **Run** box.</span></span>
   * <span data-ttu-id="83405-129">서버 관리자를 시작, hello 확장 **저장소** 노드를 선택한 후 **디스크 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-129">Start Server Manager, expand hello **Storage** node, and then select **Disk Management**.</span></span>
   * <span data-ttu-id="83405-130">시작 **관리 도구**, hello 확장 **컴퓨터 관리** 노드를 선택한 후 **디스크 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-130">Start **Administrative Tools**, expand hello **Computer Management** node, and then select **Disk Management**.</span></span> 
     
     > [!NOTE]
     > <span data-ttu-id="83405-131">관리자 권한 toorun 디스크 관리를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-131">You must use administrator privileges toorun Disk Management.</span></span>
     > 
     > 
4. <span data-ttu-id="83405-132">온라인 hello 볼륨을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-132">Take hello volume(s) online:</span></span>
   
   1. <span data-ttu-id="83405-133">디스크 관리에서 **오프라인**으로 표시된 볼륨을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-133">In Disk Management, right-click any volume marked **Offline**.</span></span>
   2. <span data-ttu-id="83405-134">**디스크 다시 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-134">Click **Reactivate Disk**.</span></span> <span data-ttu-id="83405-135">hello 디스크를 표시 해야 **온라인** 후 hello 디스크 다시 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-135">hello disk should be marked **Online** after hello disk is reactivated.</span></span>
5. <span data-ttu-id="83405-136">Hello 볼륨을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-136">Initialize hello volume(s):</span></span>
   
   1. <span data-ttu-id="83405-137">발견 된 hello 볼륨을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-137">Right-click hello discovered volumes.</span></span>
   2. <span data-ttu-id="83405-138">Hello 메뉴에서 선택 **디스크 초기화**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-138">On hello menu, select **Initialize Disk**.</span></span>
   3. <span data-ttu-id="83405-139">Hello에 **디스크 초기화** 선택 hello 디스크 tooinitialize를 원하고 클릭 한 다음 대화 상자, **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-139">In hello **Initialize Disk** dialog box, select hello disks that you want tooinitialize, and then click **OK**.</span></span>
6. <span data-ttu-id="83405-140">단순 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-140">Format simple volumes:</span></span>
   
   1. <span data-ttu-id="83405-141">Tooformat 되도록 볼륨을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-141">Right-click a volume that you want tooformat.</span></span>
   2. <span data-ttu-id="83405-142">Hello 메뉴에서 선택 **새 단순 볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-142">On hello menu, select **New Simple Volume**.</span></span>
   3. <span data-ttu-id="83405-143">Hello 새 단순 볼륨 마법사 tooformat hello 볼륨을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-143">Use hello New Simple Volume wizard tooformat hello volume:</span></span>
      
      * <span data-ttu-id="83405-144">Hello 볼륨 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-144">Specify hello volume size.</span></span>
      * <span data-ttu-id="83405-145">드라이브 문자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-145">Supply a drive letter.</span></span>
      * <span data-ttu-id="83405-146">Hello NTFS 파일 시스템을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-146">Select hello NTFS file system.</span></span>
      * <span data-ttu-id="83405-147">64KB 할당 단위 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-147">Specify a 64 KB allocation unit size.</span></span>
      * <span data-ttu-id="83405-148">빠른 포맷을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-148">Perform a quick format.</span></span>
7. <span data-ttu-id="83405-149">다중 파티션 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-149">Format multi-partition volumes.</span></span> <span data-ttu-id="83405-150">자세한 내용은 "파티션 및 볼륨" toohello 섹션에서 go [디스크 관리 구현](https://msdn.microsoft.com/library/dd163556.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-150">For instructions, go toohello section, "Partitions and Volumes" in [Implementing Disk Management](https://msdn.microsoft.com/library/dd163556.aspx).</span></span>

## <a name="view-information-about-your-volumes"></a><span data-ttu-id="83405-151">볼륨에 대한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="83405-151">View information about your volumes</span></span>
<span data-ttu-id="83405-152">다음 로컬 및 Azure StorSimple 볼륨에 대 한 프로시저 tooview 정보 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-152">Use hello following procedure tooview information about local and Azure StorSimple volumes.</span></span>

#### <a name="tooview-volume-information"></a><span data-ttu-id="83405-153">tooview 볼륨 정보</span><span class="sxs-lookup"><span data-stu-id="83405-153">tooview volume information</span></span>
1. <span data-ttu-id="83405-154">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-154">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="83405-155">Hello에 **범위** 창의 hello 클릭 **볼륨** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-155">In hello **Scope** pane, click hello **Volumes** node.</span></span> <span data-ttu-id="83405-156">Hello에 Azure StorSimple 볼륨을 모두 포함 하 여 로컬 및 마운트된 볼륨 목록이 표시 됩니다 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="83405-156">A list of local and mounted volumes, including all Azure StorSimple volumes, appears in hello **Results** pane.</span></span> <span data-ttu-id="83405-157">hello에 대 한 열 hello **결과** 창을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-157">hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="83405-158">(마우스 오른쪽 단추 클릭 hello **볼륨** 노드를 **보기**를 선택한 후 **열 추가/제거**.)</span><span class="sxs-lookup"><span data-stu-id="83405-158">(Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>
   
    ![Hello 열 구성](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | <span data-ttu-id="83405-160">결과 열</span><span class="sxs-lookup"><span data-stu-id="83405-160">Results column</span></span> | <span data-ttu-id="83405-161">설명</span><span class="sxs-lookup"><span data-stu-id="83405-161">Description</span></span> |
   |:--- |:--- |
   |  <span data-ttu-id="83405-162">이름</span><span class="sxs-lookup"><span data-stu-id="83405-162">Name</span></span> |<span data-ttu-id="83405-163">hello **이름** 열 hello 드라이브 문자가 할당 tooeach 발견 된 볼륨을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-163">hello **Name** column contains hello drive letter assigned tooeach discovered volume.</span></span> |
   |  <span data-ttu-id="83405-164">장치</span><span class="sxs-lookup"><span data-stu-id="83405-164">Device</span></span> |<span data-ttu-id="83405-165">hello **장치** 열 hello 장치 연결된 toohello 호스트 컴퓨터의 hello IP 주소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-165">hello **Device** column contains hello IP address of hello device connected toohello host computer.</span></span> |
   |  <span data-ttu-id="83405-166">장치 볼륨 이름</span><span class="sxs-lookup"><span data-stu-id="83405-166">Device Volume Name</span></span> |<span data-ttu-id="83405-167">hello **장치 볼륨 이름** hello 이름이의 hello 장치 볼륨 toowhich hello 선택한 볼륨이 속해 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-167">hello **Device Volume Name** column contains hello name of hello device volume toowhich hello selected volume belongs.</span></span> <span data-ttu-id="83405-168">Hello 해당 특정 볼륨에 대해 Azure 포털에에서 정의 된 hello 볼륨 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-168">This is hello volume name defined in hello Azure portal for that specific volume.</span></span> |
   |  <span data-ttu-id="83405-169">액세스 경로</span><span class="sxs-lookup"><span data-stu-id="83405-169">Access Paths</span></span> |<span data-ttu-id="83405-170">hello **액세스 경로** hello 액세스 경로 toohello 볼륨 열에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-170">hello **Access Paths** column displays hello access path toohello volume.</span></span> <span data-ttu-id="83405-171">이 hello 드라이브 문자나 탑재 지점이 있는 hello에 볼륨은 hello 호스트 컴퓨터에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-171">This is hello drive letter or mount point at which hello volume is accessible on hello host computer.</span></span> |

## <a name="delete-a-volume"></a><span data-ttu-id="83405-172">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="83405-172">Delete a volume</span></span>
<span data-ttu-id="83405-173">Hello 프로시저 toodelete 볼륨을 StorSimple 스냅숏 관리자에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-173">Use hello following procedure toodelete a volume from StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="83405-174">볼륨 그룹에 속해 있는 볼륨은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-174">You cannot delete a volume if it is a part of any volume group.</span></span> <span data-ttu-id="83405-175">(hello 삭제 옵션은 볼륨 그룹의 구성원 인 볼륨에 사용할 수 있습니다.) Hello 전체 볼륨 그룹 toodelete hello 볼륨을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-175">(hello delete option is not available for volumes that are members of a volume group.) You must delete hello entire volume group toodelete hello volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="83405-176">toodelete 볼륨</span><span class="sxs-lookup"><span data-stu-id="83405-176">toodelete a volume</span></span>
1. <span data-ttu-id="83405-177">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-177">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="83405-178">Hello에 **범위** 창의 hello 클릭 **볼륨** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-178">In hello **Scope** pane, click hello **Volumes** node.</span></span> 
3. <span data-ttu-id="83405-179">Hello에 **결과** 창, 마우스 오른쪽 단추로 클릭 hello 볼륨 toodelete 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-179">In hello **Results** pane, right-click hello volume that you want toodelete.</span></span>
4. <span data-ttu-id="83405-180">Hello 메뉴를 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-180">On hello menu, click **Delete**.</span></span> 
   
    ![볼륨 삭제](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. <span data-ttu-id="83405-182">hello **볼륨 삭제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="83405-182">hello **Delete Volume** dialog box appears.</span></span> <span data-ttu-id="83405-183">형식 **확인** hello 텍스트 상자와 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-183">Type **Confirm** in hello text box, and then click **OK**.</span></span>
6. <span data-ttu-id="83405-184">기본적으로 StorSimple Snapshot Manager는 삭제하기 전에 볼륨을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-184">By default, StorSimple Snapshot Manager backs up a volume before deleting it.</span></span> <span data-ttu-id="83405-185">이 예방 조치로 의도 하지 않은 hello 삭제 하는 경우 데이터 손실 로부터 있습니다 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-185">This precaution can protect you from data loss if hello deletion was unintentional.</span></span> <span data-ttu-id="83405-186">StorSimple 스냅숏 관리자를 표시 한 **자동 스냅숏** hello 볼륨을 백업 하는 동안 진행률 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-186">StorSimple Snapshot Manager displays an **Automatic Snapshot** progress message while it backs up hello volume.</span></span> 
   
    ![자동 스냅숏 메시지](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a><span data-ttu-id="83405-188">볼륨 다시 검사</span><span class="sxs-lookup"><span data-stu-id="83405-188">Rescan volumes</span></span>
<span data-ttu-id="83405-189">다음 프로시저 toorescan hello 볼륨 사용 하 여 hello tooStorSimple 스냅숏 관리자 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-189">Use hello following procedure toorescan hello volumes connected tooStorSimple Snapshot Manager.</span></span>

#### <a name="toorescan-hello-volumes"></a><span data-ttu-id="83405-190">toorescan hello 볼륨</span><span class="sxs-lookup"><span data-stu-id="83405-190">toorescan hello volumes</span></span>
1. <span data-ttu-id="83405-191">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-191">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="83405-192">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **볼륨**, 클릭 하 고 **볼륨 다시 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-192">In hello **Scope** pane, right-click **Volumes**, and then click **Rescan volumes**.</span></span>
   
    ![볼륨 다시 검사](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    <span data-ttu-id="83405-194">이 절차는 StorSimple 스냅숏 관리자를 사용 하 여 hello 볼륨 목록을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-194">This procedure synchronizes hello volume list with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="83405-195">새 볼륨 또는 삭제 된 볼륨과 같은 변경 내용이 hello 결과에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-195">Any changes, such as new volumes or deleted volumes, will be reflected in hello results.</span></span>

## <a name="configure-and-back-up-a-basic-volume"></a><span data-ttu-id="83405-196">기본 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="83405-196">Configure and back up a basic volume</span></span>
<span data-ttu-id="83405-197">다음 프로시저 tooconfigure 기본 볼륨의 백업을 hello를 사용 하 여 백업을 바로 시작 하거나 예약 된 백업에 대 한 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83405-197">Use hello following procedure tooconfigure a backup of a basic volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="83405-198">필수 조건</span><span class="sxs-lookup"><span data-stu-id="83405-198">Prerequisites</span></span>
<span data-ttu-id="83405-199">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="83405-199">Before you begin:</span></span>

* <span data-ttu-id="83405-200">Hello StorSimple 장치 및 호스트 컴퓨터 올바르게 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-200">Make sure that hello StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="83405-201">자세한 내용은 이동 너무[온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-201">For more information, go too[Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="83405-202">StorSimple Snapshot Manager 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="83405-202">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="83405-203">자세한 내용은 이동 너무[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-203">For more information, go too[Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>

#### <a name="tooconfigure-backup-of-a-basic-volume"></a><span data-ttu-id="83405-204">기본 볼륨의 tooconfigure 백업</span><span class="sxs-lookup"><span data-stu-id="83405-204">tooconfigure backup of a basic volume</span></span>
1. <span data-ttu-id="83405-205">Hello StorSimple 장치에서 기본 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83405-205">Create a basic volume on hello StorSimple device.</span></span>
2. <span data-ttu-id="83405-206">탑재, 초기화 및에 설명 된 대로 hello 볼륨을 포맷 [볼륨을 탑재](#mount-volumes)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-206">Mount, initialize, and format hello volume as described in [Mount volumes](#mount-volumes).</span></span> 
3. <span data-ttu-id="83405-207">바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-207">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="83405-208">hello StorSimple 스냅숏 관리자 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="83405-208">hello StorSimple Snapshot Manager window appears.</span></span> 
4. <span data-ttu-id="83405-209">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **볼륨** 노드를 선택한 후 **볼륨 다시 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-209">In hello **Scope** pane, right-click hello **Volumes** node, and then select **Rescan volumes**.</span></span> <span data-ttu-id="83405-210">Hello에 볼륨 목록이 나타나야 hello 검색이 완료 되 면 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="83405-210">When hello scan is finished, a list of volumes should appear in hello **Results** pane.</span></span> 
5. <span data-ttu-id="83405-211">Hello에 **결과** 창의 hello 볼륨을 마우스 오른쪽 단추로 클릭 한 다음 선택 **볼륨 그룹 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-211">In hello **Results** pane, right-click hello volume, and then select **Create Volume Group**.</span></span> 
   
    ![볼륨 그룹 만들기](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. <span data-ttu-id="83405-213">Hello에 **볼륨 그룹 만들기** 대화 상자 hello 볼륨 그룹에 대 한 이름을 입력 볼륨 tooit 할당 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-213">In hello **Create Volume Group** dialog box, type a name for hello volume group, assign volumes tooit, and then click **OK**.</span></span>
7. <span data-ttu-id="83405-214">Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-214">In hello **Scope** pane, expand hello **Volume Groups** node.</span></span> <span data-ttu-id="83405-215">hello 새 볼륨 그룹은 hello 아래에 나타나야 합니다. **볼륨 그룹** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-215">hello new volume group should appear under hello **Volume Groups** node.</span></span> 
8. <span data-ttu-id="83405-216">Hello 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-216">Right-click hello volume group name.</span></span>
   
   * <span data-ttu-id="83405-217">toostart은 대화형 (주문형) 백업 작업을 클릭 하 여 **백업 수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-217">toostart an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="83405-218">자동 백업 tooschedule 클릭 **백업 정책 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-218">tooschedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="83405-219">Hello에 **일반** 페이지 hello 목록에서 볼륨 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-219">On hello **General** page, select a volume group from hello list.</span></span> <span data-ttu-id="83405-220">Hello에 **일정** 페이지에서 hello 일정 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-220">On hello **Schedule** page, enter hello schedule details.</span></span> <span data-ttu-id="83405-221">작업을 마쳤으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-221">When you are finished, click **OK**.</span></span> 
9. <span data-ttu-id="83405-222">hello, 백업 작업이 hello tooconfirm 시작 **작업** hello에 대 한 노드 **범위** 창 hello를 클릭 한 다음 **실행** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-222">tooconfirm that hello backup job has started, expand hello **Jobs** node in hello **Scope** pane, and then click hello **Running** node.</span></span> <span data-ttu-id="83405-223">hello에 hello 현재 실행 중인 작업 목록이 표시 됩니다 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="83405-223">hello list of currently running jobs appears in hello **Results** pane.</span></span> 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a><span data-ttu-id="83405-224">동적 미러 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="83405-224">Configure and back up a dynamic mirrored volume</span></span>
<span data-ttu-id="83405-225">동적 미러 볼륨의 tooconfigure 백업 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-225">Complete hello following steps tooconfigure backup of a dynamic mirrored volume:</span></span>

* <span data-ttu-id="83405-226">1 단계: 사용 하 여 디스크 관리 toocreate 동적 미러 볼륨</span><span class="sxs-lookup"><span data-stu-id="83405-226">Step 1: Use Disk Management toocreate a dynamic mirrored volume.</span></span> 
* <span data-ttu-id="83405-227">2 단계: StorSimple 스냅숏 관리자를 사용 하 여 tooconfigure 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-227">Step 2: Use StorSimple Snapshot Manager tooconfigure backup.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="83405-228">필수 조건</span><span class="sxs-lookup"><span data-stu-id="83405-228">Prerequisites</span></span>
<span data-ttu-id="83405-229">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="83405-229">Before you begin:</span></span>

* <span data-ttu-id="83405-230">Hello StorSimple 장치 및 호스트 컴퓨터 올바르게 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-230">Make sure that hello StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="83405-231">자세한 내용은 이동 너무[온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-231">For more information, go too[Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="83405-232">StorSimple Snapshot Manager 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="83405-232">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="83405-233">자세한 내용은 이동 너무[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-233">For more information, go too[Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
* <span data-ttu-id="83405-234">Hello StorSimple 장치에 두 개의 볼륨을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-234">Configure two volumes on hello StorSimple device.</span></span> <span data-ttu-id="83405-235">(Hello 예제 hello 사용할 수 있는 볼륨은 **디스크 1** 및 **디스크 2**.)</span><span class="sxs-lookup"><span data-stu-id="83405-235">(In hello examples, hello available volumes are **Disk 1** and **Disk 2**.)</span></span> 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a><span data-ttu-id="83405-236">1 단계: 사용 하 여 디스크 관리 toocreate 동적 미러 볼륨</span><span class="sxs-lookup"><span data-stu-id="83405-236">Step 1: Use Disk Management toocreate a dynamic mirrored volume</span></span>
<span data-ttu-id="83405-237">디스크 관리는 하드 디스크와 hello 볼륨 또는 파티션이 포함 된 관리 하기 위한 시스템 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-237">Disk Management is a system utility for managing hard disks and hello volumes or partitions that they contain.</span></span> <span data-ttu-id="83405-238">디스크 관리에 대 한 자세한 내용은 이동 너무[디스크 관리](https://technet.microsoft.com/library/cc770943.aspx) hello Microsoft TechNet 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-238">For more information about Disk Management, go too[Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on hello Microsoft TechNet website.</span></span>

#### <a name="toocreate-a-dynamic-mirrored-volume"></a><span data-ttu-id="83405-239">toocreate 동적 미러 볼륨</span><span class="sxs-lookup"><span data-stu-id="83405-239">toocreate a dynamic mirrored volume</span></span>
1. <span data-ttu-id="83405-240">Hello 옵션 toostart 디스크 관리를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-240">Use any of hello following options toostart Disk Management:</span></span> 
   
   * <span data-ttu-id="83405-241">열기 hello **실행** 상자에서 입력 **Diskmgmt.msc**, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="83405-241">Open hello **Run** box, type **Diskmgmt.msc**, and press Enter.</span></span>
   * <span data-ttu-id="83405-242">서버 관리자를 시작, hello 확장 **저장소** 노드를 선택한 후 **디스크 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-242">Start Server Manager, expand hello **Storage** node, and then select **Disk Management**.</span></span> 
   * <span data-ttu-id="83405-243">시작 **관리 도구**, hello 확장 **컴퓨터 관리** 노드를 선택한 후 **디스크 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-243">Start **Administrative Tools**, expand hello **Computer Management** node, and then select **Disk Management**.</span></span> 
2. <span data-ttu-id="83405-244">Hello StorSimple 장치에 두 개의 볼륨을 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-244">Make sure that you have two volumes available on hello StorSimple device.</span></span> <span data-ttu-id="83405-245">(Hello 예에서 사용할 수 있는 볼륨 hello는 **디스크 1** 및 **디스크 2**.)</span><span class="sxs-lookup"><span data-stu-id="83405-245">(In hello example, hello available volumes are **Disk 1** and **Disk 2**.)</span></span> 
3. <span data-ttu-id="83405-246">Hello 디스크 관리 창의 hello hello 아래쪽 창 오른쪽 열에서 마우스 오른쪽 단추로 클릭 **디스크 1** 선택 **새 미러 볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-246">In hello Disk Management window, in hello right column of hello lower pane, right-click **Disk 1** and select **New Mirrored Volume**.</span></span> 
   
    ![새 미러 볼륨](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. <span data-ttu-id="83405-248">Hello에 **새 미러 볼륨** 마법사 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-248">On hello **New Mirrored Volume** wizard page, click **Next**.</span></span>
5. <span data-ttu-id="83405-249">Hello에 **디스크 선택** 페이지 **디스크 2** hello에 **선택한** 창에서 클릭 **추가**, 클릭 하 고 **다음**.</span><span class="sxs-lookup"><span data-stu-id="83405-249">On hello **Select Disks** page, select **Disk 2** in hello **Selected** pane, click **Add**, and then click **Next**.</span></span> 
6. <span data-ttu-id="83405-250">Hello에 **할당할 드라이브 문자 또는 경로** 페이지 hello 기본값을 적용 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-250">On hello **Assign Drive Letter or Path** page, accept hello defaults, and then click **Next**.</span></span> 
7. <span data-ttu-id="83405-251">Hello에 **볼륨 포맷** 페이지 hello **할당 단위 크기** 상자 **64k**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-251">On hello **Format Volume** page, in hello **Allocation Unit Size** box, select **64K**.</span></span> <span data-ttu-id="83405-252">선택 hello **빠른 포맷 수행** 확인란을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-252">Select hello **Perform a quick format** check box, and then click **Next**.</span></span> 
8. <span data-ttu-id="83405-253">Hello에 **새 미러 볼륨 완료 hello** 페이지에서 설정을 검토 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-253">On hello **Completing hello New Mirrored Volume** page, review your settings, and then click **Finish**.</span></span> 
9. <span data-ttu-id="83405-254">기본 디스크 hello tooindicate 동적 디스크 변환된 tooa 됩니다 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-254">A message appears tooindicate that hello basic disk will be converted tooa dynamic disk.</span></span> <span data-ttu-id="83405-255">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-255">Click **Yes**.</span></span>
   
    ![동적 디스크 변환 메시지](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. <span data-ttu-id="83405-257">디스크 관리에서 디스크 1과 디스크 2가 동적 미러 볼륨으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-257">In Disk Management, verify that Disk 1 and Disk 2 are shown as dynamic mirrored volumes.</span></span> <span data-ttu-id="83405-258">(**동적** hello 상태 열에 표시 되어야 하 고 용량 막대 색 hello 미러 볼륨을 나타내는 toored 변경 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="83405-258">(**Dynamic** should appear in hello status column, and hello capacity bar color should change toored, indicating a mirrored volume.)</span></span> 
    
    ![디스크 관리에서 미러링한 동적 디스크](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a><span data-ttu-id="83405-260">2 단계: StorSimple 스냅숏 관리자를 사용 하 여 tooconfigure 백업</span><span class="sxs-lookup"><span data-stu-id="83405-260">Step 2: Use StorSimple Snapshot Manager tooconfigure backup</span></span>
<span data-ttu-id="83405-261">다음 프로시저 tooconfigure 동적 미러 볼륨 hello를 사용 하 여 백업을 바로 시작 하거나 예약 된 백업에 대 한 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83405-261">Use hello following procedure tooconfigure a dynamic mirrored volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a><span data-ttu-id="83405-262">동적 미러 볼륨의 tooconfigure 백업</span><span class="sxs-lookup"><span data-stu-id="83405-262">tooconfigure backup of a dynamic mirrored volume</span></span>
1. <span data-ttu-id="83405-263">바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-263">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="83405-264">hello StorSimple 스냅숏 관리자 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="83405-264">hello StorSimple Snapshot Manager window appears.</span></span> 
2. <span data-ttu-id="83405-265">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **볼륨** 노드 선택한 **볼륨 다시 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-265">In hello **Scope** pane, right-click hello **Volumes** node and select **Rescan volumes**.</span></span> <span data-ttu-id="83405-266">Hello에 볼륨 목록이 나타나야 hello 검색이 완료 되 면 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="83405-266">When hello scan is finished, a list of volumes should appear in hello **Results** pane.</span></span> <span data-ttu-id="83405-267">hello 동적 미러 볼륨은 단일 볼륨으로 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83405-267">hello dynamic mirrored volume is listed as a single volume.</span></span> 
3. <span data-ttu-id="83405-268">Hello에 **결과** 창의 hello 동적 미러 볼륨을 마우스 오른쪽 단추로 클릭 **볼륨 그룹 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-268">In hello **Results** pane, right-click hello dynamic mirrored volume, and then click **Create Volume Group**.</span></span> 
4. <span data-ttu-id="83405-269">Hello에 **볼륨 그룹 만들기** 대화 상자 hello 볼륨 그룹에 대 한 이름을 입력 hello 동적 미러 볼륨 toothis 그룹에 할당 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-269">In hello **Create Volume Group** dialog box, type a name for hello volume group, assign hello dynamic mirrored volume toothis group, and then click **OK**.</span></span> 
5. <span data-ttu-id="83405-270">Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-270">In hello **Scope** pane, expand hello **Volume Groups** node.</span></span> <span data-ttu-id="83405-271">hello 새 볼륨 그룹은 hello 아래에 나타나야 합니다. **볼륨 그룹** 노드.</span><span class="sxs-lookup"><span data-stu-id="83405-271">hello new volume group should appear under hello  **Volume Groups** node.</span></span> 
6. <span data-ttu-id="83405-272">Hello 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-272">Right-click hello volume group name.</span></span> 
   
   * <span data-ttu-id="83405-273">toostart은 대화형 (주문형) 백업 작업을 클릭 하 여 **백업 수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-273">toostart an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="83405-274">자동 백업 tooschedule 클릭 **백업 정책 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-274">tooschedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="83405-275">Hello에 **일반** 페이지, hello 목록에서 선택 hello 볼륨 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-275">On hello **General** page, select hello volume group from hello list.</span></span> <span data-ttu-id="83405-276">Hello에 **일정** 페이지에서 hello 일정 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-276">On hello **Schedule** page, enter hello schedule details.</span></span> <span data-ttu-id="83405-277">작업을 마쳤으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-277">When you are finished, click **OK**.</span></span> 
7. <span data-ttu-id="83405-278">이 실행 될 때 hello 백업 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83405-278">You can monitor hello backup job as it runs.</span></span> <span data-ttu-id="83405-279">Hello에 **범위** 창 hello 확장 **작업** 노드를 차례로 클릭 한 다음 **실행**, hello에 hello 작업 세부 정보 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="83405-279">In hello **Scope** pane, expand hello **Jobs** node, and then click **Running**, hello job details appear in hello **Results** pane.</span></span> <span data-ttu-id="83405-280">Hello 세부 정보는 전송 된 toohello hello 백업 작업이 완료 되 면 **마지막 24** 시간 작업 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="83405-280">When hello backup job is finished, hello details are transferred toohello **Last 24** hours job list.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="83405-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83405-281">Next steps</span></span>
* <span data-ttu-id="83405-282">너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-282">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="83405-283">너무 방법에 대해 알아봅니다[toocreate StorSimple 스냅숏 관리자를 사용 하 고 볼륨 그룹을 관리](storsimple-snapshot-manager-manage-volume-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83405-283">Learn how too[use StorSimple Snapshot Manager toocreate and manage volume groups](storsimple-snapshot-manager-manage-volume-groups.md).</span></span>

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
