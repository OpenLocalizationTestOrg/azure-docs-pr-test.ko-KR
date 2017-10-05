---
title: "StorSimple Snapshot Manager에서 장치 관리 | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 MMC 스냅인을 사용하여 StorSimple 장치를 연결하고 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f5e3186a4271e0be781f367fa75ada195c58c960
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-connect-and-manage-storsimple-devices"></a><span data-ttu-id="d62f2-103">StorSimple 스냅숏 관리자를 사용하여 StorSimple 장치 연결 및 관리</span><span class="sxs-lookup"><span data-stu-id="d62f2-103">Use StorSimple Snapshot Manager to connect and manage StorSimple devices</span></span>
## <a name="overview"></a><span data-ttu-id="d62f2-104">개요</span><span class="sxs-lookup"><span data-stu-id="d62f2-104">Overview</span></span>
<span data-ttu-id="d62f2-105">StorSimple 스냅숏 관리자의 **범위** 창에서 노드를 사용하여 가져온 StorSimple 장치 데이터를 확인하고 연결된 저장소 장치를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-105">You can use nodes in the StorSimple Snapshot Manager **Scope** pane to verify imported StorSimple device data and refresh connected storage devices.</span></span> <span data-ttu-id="d62f2-106">또한 **장치**노드를 클릭하면 연결된 장치 목록과 해당 상태 정보를 **결과** 창에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-106">Additionally, when you click the **Devices** node, you can see a list of connected devices and corresponding status information in the **Results** pane.</span></span>

![연결된 장치](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

<span data-ttu-id="d62f2-108">**그림 1: StorSimple 스냅숏 관리자 연결된 장치**</span><span class="sxs-lookup"><span data-stu-id="d62f2-108">**Figure 1: StorSimple Snapshot Manager connected device**</span></span> 

<span data-ttu-id="d62f2-109">**보기** 선택 항목에 따라 각 장치에 대해 **결과** 창에 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-109">Depending on your **View** selections, the **Results** pane shows the following information about each device.</span></span> <span data-ttu-id="d62f2-110">(보기 구성에 대한 자세한 내용은 [보기 메뉴](storsimple-use-snapshot-manager.md#view-menu)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="d62f2-110">(For more information about configuring a view, go to [View menu](storsimple-use-snapshot-manager.md#view-menu).</span></span>

| <span data-ttu-id="d62f2-111">결과 열</span><span class="sxs-lookup"><span data-stu-id="d62f2-111">Results column</span></span> | <span data-ttu-id="d62f2-112">설명</span><span class="sxs-lookup"><span data-stu-id="d62f2-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d62f2-113">이름</span><span class="sxs-lookup"><span data-stu-id="d62f2-113">Name</span></span> |<span data-ttu-id="d62f2-114">장치의 이름은 Azure 클래식 포털에서 구성된 이름을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-114">The name of the device as configured in the Azure classic portal</span></span> |
| <span data-ttu-id="d62f2-115">모델</span><span class="sxs-lookup"><span data-stu-id="d62f2-115">Model</span></span> |<span data-ttu-id="d62f2-116">장치의 모델 번호</span><span class="sxs-lookup"><span data-stu-id="d62f2-116">The model number of the device</span></span> |
| <span data-ttu-id="d62f2-117">버전</span><span class="sxs-lookup"><span data-stu-id="d62f2-117">Version</span></span> |<span data-ttu-id="d62f2-118">장치에 설치된 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d62f2-118">The version of the software installed on the device</span></span> |
| <span data-ttu-id="d62f2-119">상태</span><span class="sxs-lookup"><span data-stu-id="d62f2-119">Status</span></span> |<span data-ttu-id="d62f2-120">장치를 사용할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="d62f2-120">Whether the device is available</span></span> |
| <span data-ttu-id="d62f2-121">마지막 동기화</span><span class="sxs-lookup"><span data-stu-id="d62f2-121">Last Synced</span></span> |<span data-ttu-id="d62f2-122">장치를 마지막으로 동기화한 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="d62f2-122">Date and time when the device was last synchronized</span></span> |
| <span data-ttu-id="d62f2-123">일련 번호</span><span class="sxs-lookup"><span data-stu-id="d62f2-123">Serial No.</span></span> |<span data-ttu-id="d62f2-124">장치의 일련 번호</span><span class="sxs-lookup"><span data-stu-id="d62f2-124">The serial number for the device</span></span> |

<span data-ttu-id="d62f2-125">**범위** 창에서 **장치** 노드를 마우스 오른쪽 단추로 클릭하면 다음 작업 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-125">If you right-click the **Devices** node in the **Scope** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="d62f2-126">장치 추가 또는 교체</span><span class="sxs-lookup"><span data-stu-id="d62f2-126">Add or replace a device</span></span>
* <span data-ttu-id="d62f2-127">장치 연결 및 가져오기 확인</span><span class="sxs-lookup"><span data-stu-id="d62f2-127">Connect a device and verify imports</span></span>
* <span data-ttu-id="d62f2-128">연결된 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="d62f2-128">Refresh connected devices</span></span>

<span data-ttu-id="d62f2-129">**장치** 노드를 클릭하고 **결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭하면 다음 작업 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-129">If you click the **Devices** node and then right-click a device name in the **Results** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="d62f2-130">장치 인증</span><span class="sxs-lookup"><span data-stu-id="d62f2-130">Authenticate a device</span></span>
* <span data-ttu-id="d62f2-131">장치 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d62f2-131">View device details</span></span>
* <span data-ttu-id="d62f2-132">장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="d62f2-132">Refresh a device</span></span>
* <span data-ttu-id="d62f2-133">장치 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="d62f2-133">Delete a device configuration</span></span>
* <span data-ttu-id="d62f2-134">장치 암호 변경</span><span class="sxs-lookup"><span data-stu-id="d62f2-134">Change a device password</span></span>

> [!NOTE]
> <span data-ttu-id="d62f2-135">이러한 모든 작업을 **작업** 창에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-135">All of these actions are also available in the **Actions** pane.</span></span>


<span data-ttu-id="d62f2-136">이 자습서에서는 StorSimple 스냅숏 관리자를 사용하여 장치를 연결 및 관리하고 다음 작업을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-136">This tutorial explains how to use StorSimple Snapshot Manager to connect and manage devices and perform the following tasks:</span></span>

* <span data-ttu-id="d62f2-137">장치 추가 또는 교체</span><span class="sxs-lookup"><span data-stu-id="d62f2-137">Add or replace a device</span></span>
* <span data-ttu-id="d62f2-138">장치 연결 및 가져오기 확인</span><span class="sxs-lookup"><span data-stu-id="d62f2-138">Connect a device and verify imports</span></span>
* <span data-ttu-id="d62f2-139">연결된 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="d62f2-139">Refresh connected devices</span></span>
* <span data-ttu-id="d62f2-140">장치 인증</span><span class="sxs-lookup"><span data-stu-id="d62f2-140">Authenticate a device</span></span>
* <span data-ttu-id="d62f2-141">장치 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d62f2-141">View device details</span></span>
* <span data-ttu-id="d62f2-142">개별 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="d62f2-142">Refresh an individual device</span></span>
* <span data-ttu-id="d62f2-143">장치 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="d62f2-143">Delete a device configuration</span></span>
* <span data-ttu-id="d62f2-144">만료된 장치 암호 변경</span><span class="sxs-lookup"><span data-stu-id="d62f2-144">Change an expired device password</span></span>
* <span data-ttu-id="d62f2-145">실패한 장치 바꾸기</span><span class="sxs-lookup"><span data-stu-id="d62f2-145">Replace a failed device</span></span>

> [!NOTE]
> <span data-ttu-id="d62f2-146">StorSimple 스냅숏 관리자 인터페이스 사용에 대한 일반적인 정보는 [StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d62f2-146">For general information about using the StorSimple Snapshot Manager interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>


## <a name="add-or-replace-a-device"></a><span data-ttu-id="d62f2-147">장치 추가 또는 교체</span><span class="sxs-lookup"><span data-stu-id="d62f2-147">Add or replace a device</span></span>
<span data-ttu-id="d62f2-148">다음 절차에 따라 StorSimple 장치를 추가하거나 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-148">Use the following procedure to add or replace a StorSimple device.</span></span>

#### <a name="to-add-or-replace-a-device"></a><span data-ttu-id="d62f2-149">장치를 추가 또는 교체하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-149">To add or replace a device</span></span>
1. <span data-ttu-id="d62f2-150">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-150">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d62f2-151">**범위** 창에서 **장치** 노드를 마우스 오른쪽 단추로 클릭한 다음 **장치 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-151">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="d62f2-152">**장치 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-152">The **Configure a Device** dialog box appears.</span></span>
   
    ![StorSimple 장치 구성](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. <span data-ttu-id="d62f2-154">**장치** 드롭다운 상자에서 장치 또는 가상 장치의 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-154">In the **Device** drop-down box, select the IP address of the device or virtual device.</span></span> 
4. <span data-ttu-id="d62f2-155">암호 **텍스트 상자** 에 Azure 클래식 포털에서 장치에 대한 StorSimple 스냅숏 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-155">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure classic portal.</span></span> <span data-ttu-id="d62f2-156">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-156">Click **OK**.</span></span> <span data-ttu-id="d62f2-157">StorSimple 스냅숏 관리자에서 사용자가 지정한 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-157">StorSimple Snapshot Manager searches for the device that you identified.</span></span> 
   
   * <span data-ttu-id="d62f2-158">장치를 사용할 수 있으면 StorSimple 스냅숏 관리자가 연결을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-158">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span>
   * <span data-ttu-id="d62f2-159">어떤 이유로든 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자에서 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-159">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="d62f2-160">**확인**을 클릭하여 오류 메시지를 닫은 다음 **취소**를 클릭하여 **장치 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-160">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span></span>

## <a name="connect-a-device-and-verify-imports"></a><span data-ttu-id="d62f2-161">장치 연결 및 가져오기 확인</span><span class="sxs-lookup"><span data-stu-id="d62f2-161">Connect a device and verify imports</span></span>
<span data-ttu-id="d62f2-162">다음 절차에 따라 StorSimple 장치를 연결하고 연결된 백업이 있는 모든 기존 볼륨 그룹을 가져왔는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-162">Use the following procedure to connect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span></span>

#### <a name="to-connect-a-device-and-verify-imports"></a><span data-ttu-id="d62f2-163">장치를 연결하고 가져오기를 확인하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-163">To connect a device and verify imports</span></span>
1. <span data-ttu-id="d62f2-164">StorSimple 스냅숏 관리자에 장치를 연결하려면 장치 추가 또는 교체에 나온 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-164">To connect a device to StorSimple Snapshot Manager, follow the instructions in Add or replace a device.</span></span> <span data-ttu-id="d62f2-165">장치에 연결되면 StorSimple 스냅숏 관리자가 다음과 같이 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-165">When it connects to a device, StorSimple Snapshot Manager responds as follows:</span></span>
   
   * <span data-ttu-id="d62f2-166">어떤 이유로든 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자에서 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-166">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> 
   
   * <span data-ttu-id="d62f2-167">장치를 사용할 수 있으면 StorSimple 스냅숏 관리자가 연결을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-167">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="d62f2-168">장치를 선택하면 **결과** 창에 해당 장치가 나타나고 상태 필드에 장치를 **사용 가능**한지 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-168">When you select the device, it appears in the **Results** pane, and the status field indicates that the device is **Available**.</span></span> <span data-ttu-id="d62f2-169">볼륨 그룹에 연결된 백업이 있는 경우 StorSimple 스냅숏 관리자는 해당 장치에 대해 구성된 모든 볼륨 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-169">StorSimple Snapshot Manager imports any volume groups configured for the device, provided that the volume groups have associated backups.</span></span> <span data-ttu-id="d62f2-170">백업 정책은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-170">Backup policies are not imported.</span></span> <span data-ttu-id="d62f2-171">연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-171">Volume groups that do not have associated backups are not imported.</span></span>
2. <span data-ttu-id="d62f2-172">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-172">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
3. <span data-ttu-id="d62f2-173">**범위** 창에서 최상위 노드를 마우스 오른쪽 단추로 클릭한 다음 **가져오기 표시 토글**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-173">Right-click the top node in the **Scope** pane, and then click **Toggle Imports Display**.</span></span>
   
    ![가져오기 표시 토글 선택](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. <span data-ttu-id="d62f2-175">가져온 볼륨 그룹과 백업의 상태가 표시된 **가져오기 표시 토글** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-175">The **Toggle Imports Display** dialog box appears, showing the status of the imported volume groups and backups.</span></span> <span data-ttu-id="d62f2-176">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-176">Click **OK**.</span></span>

<span data-ttu-id="d62f2-177">볼륨 그룹과 백업을 성공적으로 가져온 후에는 StorSimple 스냅숏 관리자로 만들고 구성한 볼륨 그룹과 백업을 관리하는 것과 마찬가지로 StorSimple 스냅숏 관리자를 사용하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-177">After the volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager to manage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span></span> 

## <a name="refresh-connected-devices"></a><span data-ttu-id="d62f2-178">연결된 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="d62f2-178">Refresh connected devices</span></span>
<span data-ttu-id="d62f2-179">다음 절차에 따라 연결된 StorSimple 장치를 StorSimple 스냅숏 관리자와 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-179">Use the following procedure to synchronize the connected StorSimple devices with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-connected-devices"></a><span data-ttu-id="d62f2-180">연결된 장치를 새로 고치려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-180">To refresh connected devices</span></span>
1. <span data-ttu-id="d62f2-181">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-181">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d62f2-182">**범위** 창에서 **장치**를 마우스 오른쪽 단추로 클릭하고 **장치 새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-182">In the **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span></span> <span data-ttu-id="d62f2-183">그러면 연결된 장치와 StorSimple 스냅숏 관리자가 동기화되어 최근에 추가된 모든 항목을 비롯한 볼륨 그룹 및 백업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-183">This synchronizes the connected devices with StorSimple Snapshot Manager so that you can view the volume groups and backups, including any recent additions.</span></span> 
   
    ![StorSimple 장치 새로 고침](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

<span data-ttu-id="d62f2-185">**장치 새로 고침** 작업은 연결된 장치에서 모든 새 볼륨 그룹과 연결된 백업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-185">The **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span></span> <span data-ttu-id="d62f2-186">**볼륨** 노드에서 사용할 수 있는 **볼륨 다시 검사** 작업과 달리 **장치 새로 고침**은 백업 레지스트리를 복원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-186">Unlike the **Rescan volumes** action available for the **Volumes** node, **Refresh Devices** does not restore the backup registry.</span></span>

## <a name="authenticate-a-device"></a><span data-ttu-id="d62f2-187">장치 인증</span><span class="sxs-lookup"><span data-stu-id="d62f2-187">Authenticate a device</span></span>
<span data-ttu-id="d62f2-188">다음 절차에 따라 StorSimple 스냅숏 관리자에서 StorSimple 장치를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-188">Use the following procedure to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-authenticate-a-device"></a><span data-ttu-id="d62f2-189">장치를 인증하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-189">To authenticate a device</span></span>
1. <span data-ttu-id="d62f2-190">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-190">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d62f2-191">**범위** 창에서 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-191">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="d62f2-192">**결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭하고 **인증**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-192">In the **Results** pane, right-click the name of the device, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="d62f2-193">**인증** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-193">The **Authenticate** dialog box appears.</span></span> <span data-ttu-id="d62f2-194">장치 암호를 다시 입력한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-194">Type the device password, and then click **OK**.</span></span>
   
    ![인증 대화 상자](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a><span data-ttu-id="d62f2-196">장치 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d62f2-196">View device details</span></span>
<span data-ttu-id="d62f2-197">다음 절차에 따라 StorSimple 장치의 세부 정보를 볼 수 있으며 필요한 경우 StorSimple 스냅숏 관리자와 장치를 다시 동기화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-197">Use the following procedure to view the details of a StorSimple device and, if necessary, resynchronize the device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-view-and-resynchronize-device-details"></a><span data-ttu-id="d62f2-198">장치 세부 정보를 보고 다시 동기화하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-198">To view and resynchronize device details</span></span>
1. <span data-ttu-id="d62f2-199">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-199">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d62f2-200">**범위** 창에서 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-200">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="d62f2-201">**결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭하고 **세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-201">In the **Results** pane, right-click the name of the device, and then click **Details**.</span></span>

<span data-ttu-id="d62f2-202">4. **장치 세부 정보** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-202">4.The **Device Details** dialog box appears.</span></span> <span data-ttu-id="d62f2-203">이 상자에는 이름, 모델, 버전, 일련 번호, 상태, 대상 IQN(정규화된 iSCSI 이름), 마지막 동기화 날짜 및 시간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-203">This box shows the name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span></span>

* <span data-ttu-id="d62f2-204">**다시 동기화** 를 클릭하여 장치를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-204">Click **Resync** to synchronize the device.</span></span>
* <span data-ttu-id="d62f2-205">**확인** 또는 **취소**를 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-205">Click **OK** or **Cancel** to close the dialog box.</span></span>
  
  ![장치 세부 정보](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a><span data-ttu-id="d62f2-207">개별 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="d62f2-207">Refresh an individual device</span></span>
<span data-ttu-id="d62f2-208">다음 절차에 따라 개별 StorSimple 장치를 StorSimple 스냅숏 관리자와 다시 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-208">Use the following procedure to resynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-a-device"></a><span data-ttu-id="d62f2-209">장치를 새로 고치려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-209">To refresh a device</span></span>
1. <span data-ttu-id="d62f2-210">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-210">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="d62f2-211">**범위** 창에서 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-211">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="d62f2-212">**결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭하고 **장치 새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-212">In the **Results** pane, right-click the name of the device, and then click **Refresh Device**.</span></span> <span data-ttu-id="d62f2-213">그러면 StorSimple 스냅숏 관리자와 장치가 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-213">This synchronizes the device with StorSimple Snapshot Manager.</span></span>

## <a name="delete-a-device-configuration"></a><span data-ttu-id="d62f2-214">장치 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="d62f2-214">Delete a device configuration</span></span>
<span data-ttu-id="d62f2-215">다음 절차에 따라 개별 StorSimple 장치 구성을 StorSimple 스냅숏 관리자에서 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-215">Use the following procedure to delete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span></span>

#### <a name="to-delete-a-device-configuration"></a><span data-ttu-id="d62f2-216">장치 구성을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-216">To delete a device configuration</span></span>
1. <span data-ttu-id="d62f2-217">바탕 화면 아이콘을 클릭하여 StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-217">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d62f2-218">**범위** 창에서 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-218">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="d62f2-219">**결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-219">In the **Results** pane, right-click the name of the device, and then click **Delete**.</span></span> 
4. <span data-ttu-id="d62f2-220">다음과 같은 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-220">The following message appears.</span></span> <span data-ttu-id="d62f2-221">**예**를 클릭하여 구성을 삭제하거나 **아니요**를 클릭하여 삭제를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-221">Click **Yes** to delete the configuration or click **No** to cancel the deletion.</span></span>
   
    ![장치 구성 삭제](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a><span data-ttu-id="d62f2-223">만료된 장치 암호 변경</span><span class="sxs-lookup"><span data-stu-id="d62f2-223">Change an expired device password</span></span>
<span data-ttu-id="d62f2-224">다음 절차에 따라 StorSimple 스냅숏 관리자에서 StorSimple 장치를 인증하기 위한 암호를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-224">You must enter a password to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="d62f2-225">Windows PowerShell 인터페이스를 사용하여 장치를 설정할 때 이 암호를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-225">You configure this password when you use the Windows PowerShell interface to set up the device.</span></span> <span data-ttu-id="d62f2-226">그러나 암호는 만료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-226">However, the password can expire.</span></span> <span data-ttu-id="d62f2-227">이 경우에는 Azure 클래식 포털을 사용하여 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-227">If this happens, you can use the Azure classic portal to change the password.</span></span> <span data-ttu-id="d62f2-228">그런 다음, 암호가 만료되기 전에 StorSimple 스냅숏 관리자에서 장치를 구성했기 때문에 StorSimple 스냅숏 관리자에서 장치를 다시 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-228">Then, because the device was configured in StorSimple Snapshot Manager before the password expired, you must re-authenticate the device in StorSimple Snapshot Manager.</span></span>

#### <a name="to-change-the-expired-password"></a><span data-ttu-id="d62f2-229">만료된 암호를 변경하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-229">To change the expired password</span></span>
1. <span data-ttu-id="d62f2-230">Azure 클래식 포털에서 StorSimple Manager 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-230">In the Azure classic portal, start the StorSimple Manager service.</span></span>
2. <span data-ttu-id="d62f2-231">**장치** > **구성** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-231">Click **Devices** > **Configure** for the device.</span></span>
3. <span data-ttu-id="d62f2-232">StorSimple 스냅숏 관리자 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-232">Scroll down to the StorSimple Snapshot Manager section.</span></span> <span data-ttu-id="d62f2-233">14-15자로 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-233">Enter a password that is 14-15 characters.</span></span> <span data-ttu-id="d62f2-234">암호에는 대문자, 소문자, 숫자 및 특수 문자가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-234">Make sure that the password contains a mix of uppercase, lowercase, numeric, and special characters.</span></span>
4. <span data-ttu-id="d62f2-235">확인을 위해 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-235">Re-enter the password to confirm it.</span></span>
5. <span data-ttu-id="d62f2-236">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-236">Click **Save** at the bottom of the page.</span></span>

#### <a name="to-re-authenticate-the-device"></a><span data-ttu-id="d62f2-237">장치를 다시 인증하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-237">To re-authenticate the device</span></span>
1. <span data-ttu-id="d62f2-238">StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-238">Start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d62f2-239">**범위** 창에서 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-239">In the **Scope** pane, click **Devices**.</span></span> <span data-ttu-id="d62f2-240">구성된 장치 목록이 **결과** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-240">A list of configured devices appears in the **Results** pane.</span></span>
3. <span data-ttu-id="d62f2-241">장치를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **인증**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-241">Select the device, right-click, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="d62f2-242">**인증** 창에서 새 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-242">In the **Authenticate** window, enter the new password.</span></span>
5. <span data-ttu-id="d62f2-243">장치를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **장치 새로 고침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-243">Select the device, right-click, and select **Refresh device**.</span></span> <span data-ttu-id="d62f2-244">그러면 StorSimple 스냅숏 관리자와 장치가 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-244">This synchronizes the device with StorSimple Snapshot Manager.</span></span>

## <a name="replace-a-failed-device"></a><span data-ttu-id="d62f2-245">실패한 장치 바꾸기</span><span class="sxs-lookup"><span data-stu-id="d62f2-245">Replace a failed device</span></span>
<span data-ttu-id="d62f2-246">StorSimple 장치에서 오류가 발생하여 대기(장애 조치(failover)) 장치로 교체하는 경우 다음 단계에 따라 새 장치에 연결하고 연결된 백업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-246">If a StorSimple device fails and is replaced by a standby (failover) device, use the following steps to connect to the new device and view the associated backups.</span></span>

#### <a name="to-connect-to-a-new-device-after-failover"></a><span data-ttu-id="d62f2-247">장애 조치(failover) 후 새 장치에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="d62f2-247">To connect to a new device after failover</span></span>
1. <span data-ttu-id="d62f2-248">새 장치에 대한 iSCSI 연결을 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-248">Reconfigure the iSCSI connection to the new device.</span></span> <span data-ttu-id="d62f2-249">자세한 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)에서 "7단계: 볼륨 탑재, 초기화 및 포맷"을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d62f2-249">For instructions, go to "Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d62f2-250">새 StorSimple 장치에 이전 장치와 동일한 IP 주소가 있으면 이전 구성을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-250">If the new StorSimple device has the same IP address as the old one, you might be able to connect the old configuration.</span></span>


1. <span data-ttu-id="d62f2-251">Microsoft StorSimple 관리 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-251">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="d62f2-252">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-252">Start Server Manager.</span></span>
   2. <span data-ttu-id="d62f2-253">서버 관리자 대시보드의 **도구** 메뉴에서 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-253">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="d62f2-254">**서비스** 창에서 **Microsoft StorSimple 관리 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-254">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="d62f2-255">오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-255">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
2. <span data-ttu-id="d62f2-256">이전 장치 관련 구성 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-256">Remove the configuration information related to the old device:</span></span>
   
   1. <span data-ttu-id="d62f2-257">파일 탐색기에서 C:\ProgramData\Microsoft\StorSimple\BACatalog로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-257">In File Explorer, browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   2. <span data-ttu-id="d62f2-258">BACatalog 폴더의 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-258">Delete the files in the BACatalog folder.</span></span>
3. <span data-ttu-id="d62f2-259">Microsoft StorSimple 관리 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-259">Restart the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="d62f2-260">서버 관리자 대시보드의 **도구** 메뉴에서 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-260">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="d62f2-261">**서비스** 창에서 **Microsoft StorSimple 관리 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-261">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="d62f2-262">오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-262">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span>
4. <span data-ttu-id="d62f2-263">StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-263">Start StorSimple Snapshot Manager.</span></span>
5. <span data-ttu-id="d62f2-264">새 StorSimple 장치를 구성하려면 [StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)에서 2단계: StorSimple 장치 연결의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-264">To configure the new StorSimple device, complete the steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
6. <span data-ttu-id="d62f2-265">**범위** 창에서 최상위 노드(예제의 StorSimple Snapshot Manager)를 마우스 오른쪽 단추로 클릭한 다음 **가져오기 표시 토글**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-265">Right-click the top-level node in the **Scope** pane (StorSimple Snapshot Manager in the example), and then click **Toggle Imports Display**.</span></span> 
7. <span data-ttu-id="d62f2-266">가져온 볼륨 그룹과 백업을 StorSimple 스냅숏 관리자에서 볼 수 있으면 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-266">A message appears when the imported volume groups and backups are visible in StorSimple Snapshot Manager.</span></span> <span data-ttu-id="d62f2-267">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-267">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d62f2-268">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d62f2-268">Next steps</span></span>
* <span data-ttu-id="d62f2-269">[StorSimple 스냅숏 관리자를 사용하여 StorSimple 솔루션을 관리](storsimple-snapshot-manager-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-269">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="d62f2-270">[StorSimple 스냅숏 관리자를 사용하여 볼륨을 보고 관리](storsimple-snapshot-manager-manage-volumes.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d62f2-270">Learn how to [use StorSimple Snapshot Manager to view and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span></span>

