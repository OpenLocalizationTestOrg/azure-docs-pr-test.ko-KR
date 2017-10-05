---
title: "StorSimple Snapshot Manager 및 볼륨 | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 MMC 스냅인을 사용하여 볼륨을 보고 관리하고 백업을 구성하는 방법을 설명합니다."
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
ms.openlocfilehash: 2c0b211bced99d272a73a7b018a22f99d8d58aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-volumes"></a><span data-ttu-id="cc098-103">StorSimple 스냅숏 관리자를 사용하여 볼륨 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="cc098-103">Use StorSimple Snapshot Manager to view and manage volumes</span></span>
## <a name="overview"></a><span data-ttu-id="cc098-104">개요</span><span class="sxs-lookup"><span data-stu-id="cc098-104">Overview</span></span>
<span data-ttu-id="cc098-105">**범위** 창에서 StorSimple Snapshot Manager **볼륨** 노드를 사용하여 볼륨을 선택하고 관련 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-105">You can use the StorSimple Snapshot Manager **Volumes** node (on the **Scope** pane) to select volumes and view information about them.</span></span> <span data-ttu-id="cc098-106">볼륨은 호스트에 의해 탑재된 볼륨에 해당하는 드라이브로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-106">The volumes are presented as drives that correspond to the volumes mounted by the host.</span></span> <span data-ttu-id="cc098-107">**볼륨** 노드는 iSCSI와 장치를 사용하여 검색한 볼륨을 포함하여 StorSimple에서 지원하는 로컬 볼륨 및 볼륨 유형을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-107">The **Volumes** node shows local volumes and volume types that are supported by StorSimple, including volumes discovered through the use of iSCSI and a device.</span></span> 

<span data-ttu-id="cc098-108">지원되는 볼륨에 대한 자세한 내용은 [여러 볼륨 유형에 대한 지원](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-108">For more information about supported volumes, go to [Support for multiple volume types](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).</span></span>

![결과 창의 볼륨 목록](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

<span data-ttu-id="cc098-110">또한 **볼륨** 노드를 사용하면 StorSimple 스냅숏 관리자에서 검색한 후에도 볼륨을 다시 검사하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-110">The **Volumes** node also lets you rescan or delete volumes after StorSimple Snapshot Manager discovers them.</span></span> 

<span data-ttu-id="cc098-111">이 자습서에서는 볼륨을 탑재, 초기화 및 포맷한 다음 StorSimple Snapshot Manager를 사용하여 다음 작업을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-111">This tutorial explains how you can mount, initialize, and format volumes and then use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="cc098-112">볼륨에 대한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="cc098-112">View information about volumes</span></span> 
* <span data-ttu-id="cc098-113">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="cc098-113">Delete volumes</span></span>
* <span data-ttu-id="cc098-114">볼륨 다시 검사</span><span class="sxs-lookup"><span data-stu-id="cc098-114">Rescan volumes</span></span> 
* <span data-ttu-id="cc098-115">기본 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="cc098-115">Configure a basic volume and back it up</span></span>
* <span data-ttu-id="cc098-116">동적 미러 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="cc098-116">Configure a dynamic mirrored volume and back it up</span></span>

> [!NOTE]
> <span data-ttu-id="cc098-117">모든 **볼륨** 노드 작업은 **작업** 창에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-117">All of the **Volume** node actions are also available in the **Actions** pane.</span></span>
> 
> 

## <a name="mount-volumes"></a><span data-ttu-id="cc098-118">볼륨 탑재</span><span class="sxs-lookup"><span data-stu-id="cc098-118">Mount volumes</span></span>
<span data-ttu-id="cc098-119">다음 절차에 따라 StorSimple 볼륨을 탑재, 초기화 및 포맷할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-119">Use the following procedure to mount, initialize, and format StorSimple volumes.</span></span> <span data-ttu-id="cc098-120">이 절차는 하드 디스크 및 해당 볼륨 또는 파티션을 관리하기 위해 디스크 관리, 시스템 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-120">This procedure uses Disk Management, a system utility for managing hard disks and the corresponding volumes or partitions.</span></span> <span data-ttu-id="cc098-121">디스크 관리에 대한 자세한 내용은 Microsoft TechNet 웹 사이트에서 [디스크 관리](https://technet.microsoft.com/library/cc770943.aspx)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-121">For more information about Disk Management, go to [Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on the Microsoft TechNet website.</span></span>

#### <a name="to-mount-volumes"></a><span data-ttu-id="cc098-122">볼륨을 탑재하려면</span><span class="sxs-lookup"><span data-stu-id="cc098-122">To mount volumes</span></span>
1. <span data-ttu-id="cc098-123">호스트 컴퓨터에서 Microsoft iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-123">On your host computer, start the Microsoft iSCSI initiator.</span></span>
2. <span data-ttu-id="cc098-124">대상 포털로 인터페이스 IP 주소 중 하나를 제공하거나 IP 주소를 검색한 후 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-124">Supply one of the interface IP addresses as the target portal or discovery IP address, and connect to the device.</span></span> <span data-ttu-id="cc098-125">장치가 연결된 후 Windows 시스템에서 볼륨에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-125">After the device is connected, the volumes will be accessible to your Windows system.</span></span> <span data-ttu-id="cc098-126">Microsoft iSCSI 초기자 사용에 대한 자세한 내용은 [Microsoft iSCSI 초기자 설치 및 구성][1]에서 “iSCSI 대상 장치에 연결” 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-126">For more information about using the Microsoft iSCSI initiator, go to the section “Connecting to an iSCSI target device” in [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
3. <span data-ttu-id="cc098-127">다음 옵션 중 하나를 사용하여 디스크 관리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-127">Use any of the following options to start Disk Management:</span></span>
   
   * <span data-ttu-id="cc098-128">**실행** 상자에 Diskmgmt.msc를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-128">Type Diskmgmt.msc in the **Run** box.</span></span>
   * <span data-ttu-id="cc098-129">서버 관리자를 시작하고 **저장소** 노드를 확장한 다음 **디스크 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-129">Start Server Manager, expand the **Storage** node, and then select **Disk Management**.</span></span>
   * <span data-ttu-id="cc098-130">**관리 도구**를 시작하고 **컴퓨터 관리** 노드를 확장한 다음 **디스크 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-130">Start **Administrative Tools**, expand the **Computer Management** node, and then select **Disk Management**.</span></span> 
     
     > [!NOTE]
     > <span data-ttu-id="cc098-131">관리자 권한을 사용하여 디스크 관리를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-131">You must use administrator privileges to run Disk Management.</span></span>
     > 
     > 
4. <span data-ttu-id="cc098-132">볼륨을 온라인 상태로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-132">Take the volume(s) online:</span></span>
   
   1. <span data-ttu-id="cc098-133">디스크 관리에서 **오프라인**으로 표시된 볼륨을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-133">In Disk Management, right-click any volume marked **Offline**.</span></span>
   2. <span data-ttu-id="cc098-134">**디스크 다시 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-134">Click **Reactivate Disk**.</span></span> <span data-ttu-id="cc098-135">디스크를 다시 활성화한 후에는 해당 디스크가 **온라인**으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-135">The disk should be marked **Online** after the disk is reactivated.</span></span>
5. <span data-ttu-id="cc098-136">볼륨 초기화:</span><span class="sxs-lookup"><span data-stu-id="cc098-136">Initialize the volume(s):</span></span>
   
   1. <span data-ttu-id="cc098-137">검색된 볼륨을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-137">Right-click the discovered volumes.</span></span>
   2. <span data-ttu-id="cc098-138">메뉴에서 **디스크 초기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-138">On the menu, select **Initialize Disk**.</span></span>
   3. <span data-ttu-id="cc098-139">**디스크 초기화** 대화 상자에서 초기화하려는 디스크를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-139">In the **Initialize Disk** dialog box, select the disks that you want to initialize, and then click **OK**.</span></span>
6. <span data-ttu-id="cc098-140">단순 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-140">Format simple volumes:</span></span>
   
   1. <span data-ttu-id="cc098-141">포맷할 볼륨을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-141">Right-click a volume that you want to format.</span></span>
   2. <span data-ttu-id="cc098-142">메뉴에서 **새 단순 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-142">On the menu, select **New Simple Volume**.</span></span>
   3. <span data-ttu-id="cc098-143">새 단순 볼륨 마법사를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-143">Use the New Simple Volume wizard to format the volume:</span></span>
      
      * <span data-ttu-id="cc098-144">볼륨 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-144">Specify the volume size.</span></span>
      * <span data-ttu-id="cc098-145">드라이브 문자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-145">Supply a drive letter.</span></span>
      * <span data-ttu-id="cc098-146">NTFS 파일 시스템을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-146">Select the NTFS file system.</span></span>
      * <span data-ttu-id="cc098-147">64KB 할당 단위 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-147">Specify a 64 KB allocation unit size.</span></span>
      * <span data-ttu-id="cc098-148">빠른 포맷을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-148">Perform a quick format.</span></span>
7. <span data-ttu-id="cc098-149">다중 파티션 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-149">Format multi-partition volumes.</span></span> <span data-ttu-id="cc098-150">자세한 지침은 [디스크 관리 구현](https://msdn.microsoft.com/library/dd163556.aspx)에서 "파티션 및 볼륨" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-150">For instructions, go to the section, "Partitions and Volumes" in [Implementing Disk Management](https://msdn.microsoft.com/library/dd163556.aspx).</span></span>

## <a name="view-information-about-your-volumes"></a><span data-ttu-id="cc098-151">볼륨에 대한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="cc098-151">View information about your volumes</span></span>
<span data-ttu-id="cc098-152">다음 절차에 따라 로컬 및 Azure StorSimple 볼륨에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-152">Use the following procedure to view information about local and Azure StorSimple volumes.</span></span>

#### <a name="to-view-volume-information"></a><span data-ttu-id="cc098-153">볼륨 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="cc098-153">To view volume information</span></span>
1. <span data-ttu-id="cc098-154">바탕 화면 아이콘을 클릭하여 StorSimple Snapshot Manager를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-154">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="cc098-155">**범위** 창에서 **볼륨** 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-155">In the **Scope** pane, click the **Volumes** node.</span></span> <span data-ttu-id="cc098-156">모든 Azure StorSimple 볼륨을 포함하여 로컬 볼륨 및 탑재된 볼륨 목록이 **결과** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-156">A list of local and mounted volumes, including all Azure StorSimple volumes, appears in the **Results** pane.</span></span> <span data-ttu-id="cc098-157">**결과** 창의 열은 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-157">The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="cc098-158">(**볼륨** 노드를 마우스 오른쪽 단추로 클릭하고 **보기**를 선택한 다음 **열 추가/제거**를 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="cc098-158">(Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>
   
    ![열 구성](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | <span data-ttu-id="cc098-160">결과 열</span><span class="sxs-lookup"><span data-stu-id="cc098-160">Results column</span></span> | <span data-ttu-id="cc098-161">설명</span><span class="sxs-lookup"><span data-stu-id="cc098-161">Description</span></span> |
   |:--- |:--- |
   |  <span data-ttu-id="cc098-162">이름</span><span class="sxs-lookup"><span data-stu-id="cc098-162">Name</span></span> |<span data-ttu-id="cc098-163">**이름** 열에는 검색된 각 볼륨에 할당된 드라이브 문자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-163">The **Name** column contains the drive letter assigned to each discovered volume.</span></span> |
   |  <span data-ttu-id="cc098-164">장치</span><span class="sxs-lookup"><span data-stu-id="cc098-164">Device</span></span> |<span data-ttu-id="cc098-165">**장치** 열은 호스트 컴퓨터에 연결된 장치의 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-165">The **Device** column contains the IP address of the device connected to the host computer.</span></span> |
   |  <span data-ttu-id="cc098-166">장치 볼륨 이름</span><span class="sxs-lookup"><span data-stu-id="cc098-166">Device Volume Name</span></span> |<span data-ttu-id="cc098-167">**장치 볼륨 이름** 열은 선택한 볼륨이 속한 장치 볼륨의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-167">The **Device Volume Name** column contains the name of the device volume to which the selected volume belongs.</span></span> <span data-ttu-id="cc098-168">이 이름은 해당 특정 볼륨에 대해 Azure Portal에서 정의한 볼륨 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-168">This is the volume name defined in the Azure portal for that specific volume.</span></span> |
   |  <span data-ttu-id="cc098-169">액세스 경로</span><span class="sxs-lookup"><span data-stu-id="cc098-169">Access Paths</span></span> |<span data-ttu-id="cc098-170">**액세스 경로** 열은 볼륨에 대한 액세스 경로를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-170">The **Access Paths** column displays the access path to the volume.</span></span> <span data-ttu-id="cc098-171">호스트 컴퓨터에서 볼륨에 액세스할 수 있는 드라이브 문자 또는 탑재 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-171">This is the drive letter or mount point at which the volume is accessible on the host computer.</span></span> |

## <a name="delete-a-volume"></a><span data-ttu-id="cc098-172">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="cc098-172">Delete a volume</span></span>
<span data-ttu-id="cc098-173">다음 절차에 따라 StorSimple Snapshot Manager에서 볼륨을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-173">Use the following procedure to delete a volume from StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="cc098-174">볼륨 그룹에 속해 있는 볼륨은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-174">You cannot delete a volume if it is a part of any volume group.</span></span> <span data-ttu-id="cc098-175">(볼륨 그룹에 속한 볼륨에 대해서는 삭제 옵션을 사용할 수 없습니다.) 볼륨을 삭제하려면 전체 볼륨 그룹을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-175">(The delete option is not available for volumes that are members of a volume group.) You must delete the entire volume group to delete the volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="cc098-176">볼륨을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="cc098-176">To delete a volume</span></span>
1. <span data-ttu-id="cc098-177">바탕 화면 아이콘을 클릭하여 StorSimple Snapshot Manager를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-177">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="cc098-178">**범위** 창에서 **볼륨** 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-178">In the **Scope** pane, click the **Volumes** node.</span></span> 
3. <span data-ttu-id="cc098-179">**결과** 창에서 삭제하려는 볼륨을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-179">In the **Results** pane, right-click the volume that you want to delete.</span></span>
4. <span data-ttu-id="cc098-180">메뉴에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-180">On the menu, click **Delete**.</span></span> 
   
    ![볼륨 삭제](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. <span data-ttu-id="cc098-182">**볼륨 삭제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-182">The **Delete Volume** dialog box appears.</span></span> <span data-ttu-id="cc098-183">텍스트 상자에 **확인**을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-183">Type **Confirm** in the text box, and then click **OK**.</span></span>
6. <span data-ttu-id="cc098-184">기본적으로 StorSimple Snapshot Manager는 삭제하기 전에 볼륨을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-184">By default, StorSimple Snapshot Manager backs up a volume before deleting it.</span></span> <span data-ttu-id="cc098-185">이 예방 조치를 통해 실수로 삭제하는 경우의 데이터 손실을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-185">This precaution can protect you from data loss if the deletion was unintentional.</span></span> <span data-ttu-id="cc098-186">StorSimple Snapshot Manager는 볼륨을 백업하는 동안 **자동 스냅숏** 진행률 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-186">StorSimple Snapshot Manager displays an **Automatic Snapshot** progress message while it backs up the volume.</span></span> 
   
    ![자동 스냅숏 메시지](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a><span data-ttu-id="cc098-188">볼륨 다시 검사</span><span class="sxs-lookup"><span data-stu-id="cc098-188">Rescan volumes</span></span>
<span data-ttu-id="cc098-189">다음 절차에 따라 StorSimple 스냅숏 관리자에 연결된 볼륨을 다시 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-189">Use the following procedure to rescan the volumes connected to StorSimple Snapshot Manager.</span></span>

#### <a name="to-rescan-the-volumes"></a><span data-ttu-id="cc098-190">볼륨을 다시 검사하려면</span><span class="sxs-lookup"><span data-stu-id="cc098-190">To rescan the volumes</span></span>
1. <span data-ttu-id="cc098-191">바탕 화면 아이콘을 클릭하여 StorSimple Snapshot Manager를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-191">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="cc098-192">**범위** 창에서 **볼륨**을 마우스 오른쪽 단추로 클릭한 다음 **볼륨 다시 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-192">In the **Scope** pane, right-click **Volumes**, and then click **Rescan volumes**.</span></span>
   
    ![볼륨 다시 검사](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    <span data-ttu-id="cc098-194">이 절차는 볼륨 목록을 StorSimple Snapshot Manager와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-194">This procedure synchronizes the volume list with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="cc098-195">새로운 볼륨이나 삭제된 볼륨 등의 모든 변경 내용이 결과에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-195">Any changes, such as new volumes or deleted volumes, will be reflected in the results.</span></span>

## <a name="configure-and-back-up-a-basic-volume"></a><span data-ttu-id="cc098-196">기본 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="cc098-196">Configure and back up a basic volume</span></span>
<span data-ttu-id="cc098-197">다음 절차에 따라 기본 볼륨의 백업을 구성한 다음 백업을 즉시 시작하거나 예약된 백업에 대한 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-197">Use the following procedure to configure a backup of a basic volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cc098-198">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cc098-198">Prerequisites</span></span>
<span data-ttu-id="cc098-199">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cc098-199">Before you begin:</span></span>

* <span data-ttu-id="cc098-200">StorSimple 장치 및 호스트 컴퓨터가 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-200">Make sure that the StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="cc098-201">자세한 내용은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-201">For more information, go to [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="cc098-202">StorSimple Snapshot Manager 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="cc098-202">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="cc098-203">자세한 내용은 [StorSimple Snapshot Manager 배포](storsimple-snapshot-manager-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-203">For more information, go to [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>

#### <a name="to-configure-backup-of-a-basic-volume"></a><span data-ttu-id="cc098-204">기본 볼륨의 백업을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="cc098-204">To configure backup of a basic volume</span></span>
1. <span data-ttu-id="cc098-205">StorSimple 장치에서 기본 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-205">Create a basic volume on the StorSimple device.</span></span>
2. <span data-ttu-id="cc098-206">[볼륨 탑재](#mount-volumes)에 설명된 대로 볼륨을 탑재, 초기화 및 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-206">Mount, initialize, and format the volume as described in [Mount volumes](#mount-volumes).</span></span> 
3. <span data-ttu-id="cc098-207">바탕 화면에서 StorSimple Snapshot Manager 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-207">Click the StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="cc098-208">StorSimple Snapshot Manager 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-208">The StorSimple Snapshot Manager window appears.</span></span> 
4. <span data-ttu-id="cc098-209">**범위** 창에서 **볼륨** 노드를 마우스 오른쪽 단추로 클릭한 다음 **볼륨 다시 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-209">In the **Scope** pane, right-click the **Volumes** node, and then select **Rescan volumes**.</span></span> <span data-ttu-id="cc098-210">검사가 끝나면 볼륨 목록이 **결과** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-210">When the scan is finished, a list of volumes should appear in the **Results** pane.</span></span> 
5. <span data-ttu-id="cc098-211">**결과** 창에서 볼륨을 마우스 오른쪽 단추로 클릭한 다음 **볼륨 그룹 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-211">In the **Results** pane, right-click the volume, and then select **Create Volume Group**.</span></span> 
   
    ![볼륨 그룹 만들기](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. <span data-ttu-id="cc098-213">**볼륨 그룹 만들기** 대화 상자에서 볼륨 그룹의 이름을 입력하고 이 그룹에 볼륨을 할당한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-213">In the **Create Volume Group** dialog box, type a name for the volume group, assign volumes to it, and then click **OK**.</span></span>
7. <span data-ttu-id="cc098-214">**범위** 창에서 **볼륨 그룹** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-214">In the **Scope** pane, expand the **Volume Groups** node.</span></span> <span data-ttu-id="cc098-215">새 볼륨 그룹이 **볼륨 그룹** 노드 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-215">The new volume group should appear under the **Volume Groups** node.</span></span> 
8. <span data-ttu-id="cc098-216">볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-216">Right-click the volume group name.</span></span>
   
   * <span data-ttu-id="cc098-217">대화형(주문형) 백업 작업을 시작하려면 **백업 수행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-217">To start an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="cc098-218">자동 백업을 예약하려면 **백업 정책 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-218">To schedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="cc098-219">**일반** 페이지의 목록에서 볼륨 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-219">On the **General** page, select a volume group from the list.</span></span> <span data-ttu-id="cc098-220">**일정** 페이지에서 일정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-220">On the **Schedule** page, enter the schedule details.</span></span> <span data-ttu-id="cc098-221">작업을 마쳤으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-221">When you are finished, click **OK**.</span></span> 
9. <span data-ttu-id="cc098-222">백업 작업이 시작되었는지 확인하려면 **범위** 창에서 **작업** 노드를 확장한 다음 **실행 중** 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-222">To confirm that the backup job has started, expand the **Jobs** node in the **Scope** pane, and then click the **Running** node.</span></span> <span data-ttu-id="cc098-223">현재 실행 중인 작업의 목록이 **결과** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-223">The list of currently running jobs appears in the **Results** pane.</span></span> 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a><span data-ttu-id="cc098-224">동적 미러 볼륨 구성 및 백업</span><span class="sxs-lookup"><span data-stu-id="cc098-224">Configure and back up a dynamic mirrored volume</span></span>
<span data-ttu-id="cc098-225">다음 단계를 완료하여 동적 미러 볼륨에 대한 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-225">Complete the following steps to configure backup of a dynamic mirrored volume:</span></span>

* <span data-ttu-id="cc098-226">1단계: 디스크 관리를 사용하여 동적 미러 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-226">Step 1: Use Disk Management to create a dynamic mirrored volume.</span></span> 
* <span data-ttu-id="cc098-227">2단계: StorSimple Snapshot Manager를 사용하여 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-227">Step 2: Use StorSimple Snapshot Manager to configure backup.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cc098-228">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cc098-228">Prerequisites</span></span>
<span data-ttu-id="cc098-229">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cc098-229">Before you begin:</span></span>

* <span data-ttu-id="cc098-230">StorSimple 장치 및 호스트 컴퓨터가 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-230">Make sure that the StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="cc098-231">자세한 내용은 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-231">For more information, go to [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="cc098-232">StorSimple Snapshot Manager 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="cc098-232">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="cc098-233">자세한 내용은 [StorSimple Snapshot Manager 배포](storsimple-snapshot-manager-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-233">For more information, go to [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
* <span data-ttu-id="cc098-234">StorSimple 장치에 두 볼륨을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-234">Configure two volumes on the StorSimple device.</span></span> <span data-ttu-id="cc098-235">(예제에서 사용할 수 있는 볼륨은 **디스크 1** 및 **디스크 2**입니다.)</span><span class="sxs-lookup"><span data-stu-id="cc098-235">(In the examples, the available volumes are **Disk 1** and **Disk 2**.)</span></span> 

### <a name="step-1-use-disk-management-to-create-a-dynamic-mirrored-volume"></a><span data-ttu-id="cc098-236">1단계: 디스크 관리를 사용하여 동적 미러 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="cc098-236">Step 1: Use Disk Management to create a dynamic mirrored volume</span></span>
<span data-ttu-id="cc098-237">디스크 관리는 하드 디스크 및 볼륨 또는 하드 디스크와 볼륨이 포함된 파티션을 관리하기 위한 시스템 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-237">Disk Management is a system utility for managing hard disks and the volumes or partitions that they contain.</span></span> <span data-ttu-id="cc098-238">디스크 관리에 대한 자세한 내용은 Microsoft TechNet 웹 사이트에서 [디스크 관리](https://technet.microsoft.com/library/cc770943.aspx)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="cc098-238">For more information about Disk Management, go to [Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on the Microsoft TechNet website.</span></span>

#### <a name="to-create-a-dynamic-mirrored-volume"></a><span data-ttu-id="cc098-239">동적 미러 볼륨을 만들려면</span><span class="sxs-lookup"><span data-stu-id="cc098-239">To create a dynamic mirrored volume</span></span>
1. <span data-ttu-id="cc098-240">다음 옵션 중 하나를 사용하여 디스크 관리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-240">Use any of the following options to start Disk Management:</span></span> 
   
   * <span data-ttu-id="cc098-241">**실행** 상자를 열고 **Diskmgmt.msc**를 입력한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-241">Open the **Run** box, type **Diskmgmt.msc**, and press Enter.</span></span>
   * <span data-ttu-id="cc098-242">서버 관리자를 시작하고 **저장소** 노드를 확장한 다음 **디스크 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-242">Start Server Manager, expand the **Storage** node, and then select **Disk Management**.</span></span> 
   * <span data-ttu-id="cc098-243">**관리 도구**를 시작하고 **컴퓨터 관리** 노드를 확장한 다음 **디스크 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-243">Start **Administrative Tools**, expand the **Computer Management** node, and then select **Disk Management**.</span></span> 
2. <span data-ttu-id="cc098-244">StorSimple 장치에서 사용할 수 있는 두 볼륨이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-244">Make sure that you have two volumes available on the StorSimple device.</span></span> <span data-ttu-id="cc098-245">(예제에서 사용할 수 있는 볼륨은 **디스크 1** 및 **디스크 2**입니다.)</span><span class="sxs-lookup"><span data-stu-id="cc098-245">(In the example, the available volumes are **Disk 1** and **Disk 2**.)</span></span> 
3. <span data-ttu-id="cc098-246">디스크 관리 창에서 아래쪽 창의 오른쪽 열에 있는 **디스크 1**을 마우스 오른쪽 단추로 클릭하고 **새 미러 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-246">In the Disk Management window, in the right column of the lower pane, right-click **Disk 1** and select **New Mirrored Volume**.</span></span> 
   
    ![새 미러 볼륨](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. <span data-ttu-id="cc098-248">**새 미러 볼륨** 마법사 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-248">On the **New Mirrored Volume** wizard page, click **Next**.</span></span>
5. <span data-ttu-id="cc098-249">**디스크 선택** 페이지의 **선택된** 창에서 **디스크 2**를 선택하고 **추가**를 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-249">On the **Select Disks** page, select **Disk 2** in the **Selected** pane, click **Add**, and then click **Next**.</span></span> 
6. <span data-ttu-id="cc098-250">**드라이브 문자 또는 경로 할당** 페이지에서 기본값을 적용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-250">On the **Assign Drive Letter or Path** page, accept the defaults, and then click **Next**.</span></span> 
7. <span data-ttu-id="cc098-251">**볼륨 포맷** 페이지의 **할당 단위 크기** 상자에서 **64K**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-251">On the **Format Volume** page, in the **Allocation Unit Size** box, select **64K**.</span></span> <span data-ttu-id="cc098-252">**빠른 포맷 실행** 확인란을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-252">Select the **Perform a quick format** check box, and then click **Next**.</span></span> 
8. <span data-ttu-id="cc098-253">**새 미러 볼륨 완료** 페이지에서 설정을 검토하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-253">On the **Completing the New Mirrored Volume** page, review your settings, and then click **Finish**.</span></span> 
9. <span data-ttu-id="cc098-254">기본 디스크가 동적 디스크로 변환된다는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-254">A message appears to indicate that the basic disk will be converted to a dynamic disk.</span></span> <span data-ttu-id="cc098-255">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-255">Click **Yes**.</span></span>
   
    ![동적 디스크 변환 메시지](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. <span data-ttu-id="cc098-257">디스크 관리에서 디스크 1과 디스크 2가 동적 미러 볼륨으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-257">In Disk Management, verify that Disk 1 and Disk 2 are shown as dynamic mirrored volumes.</span></span> <span data-ttu-id="cc098-258">(**동적**이 상태 열에 표시되고 용량 막대의 색은 미러 볼륨을 나타내는 빨강으로 변경되어야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="cc098-258">(**Dynamic** should appear in the status column, and the capacity bar color should change to red, indicating a mirrored volume.)</span></span> 
    
    ![디스크 관리에서 미러링한 동적 디스크](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-to-configure-backup"></a><span data-ttu-id="cc098-260">2단계: StorSimple Snapshot Manager를 사용하여 백업 구성</span><span class="sxs-lookup"><span data-stu-id="cc098-260">Step 2: Use StorSimple Snapshot Manager to configure backup</span></span>
<span data-ttu-id="cc098-261">다음 절차에 따라 동적 미러 볼륨을 구성한 다음 백업을 즉시 시작하거나 예약된 백업에 대한 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-261">Use the following procedure to configure a dynamic mirrored volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

#### <a name="to-configure-backup-of-a-dynamic-mirrored-volume"></a><span data-ttu-id="cc098-262">동적 미러 볼륨의 백업을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="cc098-262">To configure backup of a dynamic mirrored volume</span></span>
1. <span data-ttu-id="cc098-263">바탕 화면에서 StorSimple Snapshot Manager 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-263">Click the StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="cc098-264">StorSimple Snapshot Manager 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-264">The StorSimple Snapshot Manager window appears.</span></span> 
2. <span data-ttu-id="cc098-265">**범위** 창에서 **볼륨** 노드를 마우스 오른쪽 단추로 클릭하고 **볼륨 다시 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-265">In the **Scope** pane, right-click the **Volumes** node and select **Rescan volumes**.</span></span> <span data-ttu-id="cc098-266">검사가 끝나면 볼륨 목록이 **결과** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-266">When the scan is finished, a list of volumes should appear in the **Results** pane.</span></span> <span data-ttu-id="cc098-267">동적 미러 볼륨은 단일 볼륨으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-267">The dynamic mirrored volume is listed as a single volume.</span></span> 
3. <span data-ttu-id="cc098-268">**결과** 창에서 동적 미러 볼륨을 마우스 오른쪽 단추로 클릭한 다음 **볼륨 그룹 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-268">In the **Results** pane, right-click the dynamic mirrored volume, and then click **Create Volume Group**.</span></span> 
4. <span data-ttu-id="cc098-269">**볼륨 그룹 만들기** 대화 상자에서 볼륨 그룹의 이름을 입력하고 이 그룹에 동적 미러 볼륨을 할당한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-269">In the **Create Volume Group** dialog box, type a name for the volume group, assign the dynamic mirrored volume to this group, and then click **OK**.</span></span> 
5. <span data-ttu-id="cc098-270">**범위** 창에서 **볼륨 그룹** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-270">In the **Scope** pane, expand the **Volume Groups** node.</span></span> <span data-ttu-id="cc098-271">새 볼륨 그룹이 **볼륨 그룹** 노드 아래에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-271">The new volume group should appear under the  **Volume Groups** node.</span></span> 
6. <span data-ttu-id="cc098-272">볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-272">Right-click the volume group name.</span></span> 
   
   * <span data-ttu-id="cc098-273">대화형(주문형) 백업 작업을 시작하려면 **백업 수행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-273">To start an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="cc098-274">자동 백업을 예약하려면 **백업 정책 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-274">To schedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="cc098-275">**일반** 페이지의 목록에서 볼륨 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-275">On the **General** page, select the volume group from the list.</span></span> <span data-ttu-id="cc098-276">**일정** 페이지에서 일정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-276">On the **Schedule** page, enter the schedule details.</span></span> <span data-ttu-id="cc098-277">작업을 마쳤으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-277">When you are finished, click **OK**.</span></span> 
7. <span data-ttu-id="cc098-278">실행되는 백업 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-278">You can monitor the backup job as it runs.</span></span> <span data-ttu-id="cc098-279">**범위** 창에서 **작업** 노드를 확장한 다음 **실행 중**을 클릭합니다. 작업 세부 정보가 **결과** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-279">In the **Scope** pane, expand the **Jobs** node, and then click **Running**, The job details appear in the **Results** pane.</span></span> <span data-ttu-id="cc098-280">백업 작업이 완료되면 세부 정보가 **최근 24**시간 작업 목록으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-280">When the backup job is finished, the details are transferred to the **Last 24** hours job list.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cc098-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc098-281">Next steps</span></span>
* <span data-ttu-id="cc098-282">[StorSimple Snapshot Manager를 사용하여 StorSimple 솔루션을 관리](storsimple-snapshot-manager-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-282">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="cc098-283">[StorSimple Snapshot Manager를 사용하여 볼륨 그룹을 만들고 관리](storsimple-snapshot-manager-manage-volume-groups.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc098-283">Learn how to [use StorSimple Snapshot Manager to create and manage volume groups](storsimple-snapshot-manager-manage-volume-groups.md).</span></span>

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
