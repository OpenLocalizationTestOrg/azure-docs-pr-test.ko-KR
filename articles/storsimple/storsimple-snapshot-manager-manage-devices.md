---
title: "StorSimple 스냅숏 관리자 aaaManage 장치 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooconnect hello 하 고 StorSimple 장치를 관리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a><span data-ttu-id="43d40-103">StorSimple 스냅숏 관리자 tooconnect를 사용 하 고 StorSimple 장치를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-103">Use StorSimple Snapshot Manager tooconnect and manage StorSimple devices</span></span>
## <a name="overview"></a><span data-ttu-id="43d40-104">개요</span><span class="sxs-lookup"><span data-stu-id="43d40-104">Overview</span></span>
<span data-ttu-id="43d40-105">Hello StorSimple 스냅숏 관리자에서에서 노드를 사용할 수 있습니다 **범위** 창 tooverify StorSimple 장치 데이터를 가져올 연결 된 저장소 장치를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-105">You can use nodes in hello StorSimple Snapshot Manager **Scope** pane tooverify imported StorSimple device data and refresh connected storage devices.</span></span> <span data-ttu-id="43d40-106">또한 클릭할 때 hello **장치** 노드를 연결 된 장치 및 해당 상태 정보 hello의 목록을 볼 수 있습니다 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="43d40-106">Additionally, when you click hello **Devices** node, you can see a list of connected devices and corresponding status information in hello **Results** pane.</span></span>

![연결된 장치](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

<span data-ttu-id="43d40-108">**그림 1: StorSimple 스냅숏 관리자 연결된 장치**</span><span class="sxs-lookup"><span data-stu-id="43d40-108">**Figure 1: StorSimple Snapshot Manager connected device**</span></span> 

<span data-ttu-id="43d40-109">에 따라 프로그램 **보기** 선택 항목, hello **결과** 창 hello 다음 각 장치에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-109">Depending on your **View** selections, hello **Results** pane shows hello following information about each device.</span></span> <span data-ttu-id="43d40-110">(너무 보기를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[보기 메뉴](storsimple-use-snapshot-manager.md#view-menu)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-110">(For more information about configuring a view, go too[View menu](storsimple-use-snapshot-manager.md#view-menu).</span></span>

| <span data-ttu-id="43d40-111">결과 열</span><span class="sxs-lookup"><span data-stu-id="43d40-111">Results column</span></span> | <span data-ttu-id="43d40-112">설명</span><span class="sxs-lookup"><span data-stu-id="43d40-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="43d40-113">이름</span><span class="sxs-lookup"><span data-stu-id="43d40-113">Name</span></span> |<span data-ttu-id="43d40-114">hello 장치 hello Azure 클래식 포털에에서 구성 된 대로 hello 이름</span><span class="sxs-lookup"><span data-stu-id="43d40-114">hello name of hello device as configured in hello Azure classic portal</span></span> |
| <span data-ttu-id="43d40-115">모델</span><span class="sxs-lookup"><span data-stu-id="43d40-115">Model</span></span> |<span data-ttu-id="43d40-116">hello hello 장치 모델 번호</span><span class="sxs-lookup"><span data-stu-id="43d40-116">hello model number of hello device</span></span> |
| <span data-ttu-id="43d40-117">버전</span><span class="sxs-lookup"><span data-stu-id="43d40-117">Version</span></span> |<span data-ttu-id="43d40-118">hello 장치에 설치 된 hello 소프트웨어 hello 버전</span><span class="sxs-lookup"><span data-stu-id="43d40-118">hello version of hello software installed on hello device</span></span> |
| <span data-ttu-id="43d40-119">가동 상태</span><span class="sxs-lookup"><span data-stu-id="43d40-119">Status</span></span> |<span data-ttu-id="43d40-120">Hello 장치를 사용할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="43d40-120">Whether hello device is available</span></span> |
| <span data-ttu-id="43d40-121">마지막 동기화</span><span class="sxs-lookup"><span data-stu-id="43d40-121">Last Synced</span></span> |<span data-ttu-id="43d40-122">날짜 및 시간 hello 장치에 마지막으로 동기화</span><span class="sxs-lookup"><span data-stu-id="43d40-122">Date and time when hello device was last synchronized</span></span> |
| <span data-ttu-id="43d40-123">일련 번호</span><span class="sxs-lookup"><span data-stu-id="43d40-123">Serial No.</span></span> |<span data-ttu-id="43d40-124">hello 장치에 대 한 hello 일련 번호</span><span class="sxs-lookup"><span data-stu-id="43d40-124">hello serial number for hello device</span></span> |

<span data-ttu-id="43d40-125">Hello를 마우스 오른쪽 단추로 클릭 하는 경우 **장치** hello에 대 한 노드 **범위** 창에서 작업을 수행 하는 hello에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-125">If you right-click hello **Devices** node in hello **Scope** pane, you can select from hello following actions:</span></span>

* <span data-ttu-id="43d40-126">장치 추가 또는 교체</span><span class="sxs-lookup"><span data-stu-id="43d40-126">Add or replace a device</span></span>
* <span data-ttu-id="43d40-127">장치 연결 및 가져오기 확인</span><span class="sxs-lookup"><span data-stu-id="43d40-127">Connect a device and verify imports</span></span>
* <span data-ttu-id="43d40-128">연결된 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="43d40-128">Refresh connected devices</span></span>

<span data-ttu-id="43d40-129">Hello를 누르면 **장치** hello에 대 한 노드 마우스 오른쪽 단추로 장치 이름을 **결과** 창에서 작업을 수행 하는 hello에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-129">If you click hello **Devices** node and then right-click a device name in hello **Results** pane, you can select from hello following actions:</span></span>

* <span data-ttu-id="43d40-130">장치 인증</span><span class="sxs-lookup"><span data-stu-id="43d40-130">Authenticate a device</span></span>
* <span data-ttu-id="43d40-131">장치 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="43d40-131">View device details</span></span>
* <span data-ttu-id="43d40-132">장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="43d40-132">Refresh a device</span></span>
* <span data-ttu-id="43d40-133">장치 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="43d40-133">Delete a device configuration</span></span>
* <span data-ttu-id="43d40-134">장치 암호 변경</span><span class="sxs-lookup"><span data-stu-id="43d40-134">Change a device password</span></span>

> [!NOTE]
> <span data-ttu-id="43d40-135">이러한 모든 작업 에서도 제공 되 hello **동작** 창.</span><span class="sxs-lookup"><span data-stu-id="43d40-135">All of these actions are also available in hello **Actions** pane.</span></span>


<span data-ttu-id="43d40-136">이 자습서에 설명 어떻게 toouse StorSimple 스냅숏 관리자 tooconnect 및 장치를 관리 하 고 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-136">This tutorial explains how toouse StorSimple Snapshot Manager tooconnect and manage devices and perform hello following tasks:</span></span>

* <span data-ttu-id="43d40-137">장치 추가 또는 교체</span><span class="sxs-lookup"><span data-stu-id="43d40-137">Add or replace a device</span></span>
* <span data-ttu-id="43d40-138">장치 연결 및 가져오기 확인</span><span class="sxs-lookup"><span data-stu-id="43d40-138">Connect a device and verify imports</span></span>
* <span data-ttu-id="43d40-139">연결된 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="43d40-139">Refresh connected devices</span></span>
* <span data-ttu-id="43d40-140">장치 인증</span><span class="sxs-lookup"><span data-stu-id="43d40-140">Authenticate a device</span></span>
* <span data-ttu-id="43d40-141">장치 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="43d40-141">View device details</span></span>
* <span data-ttu-id="43d40-142">개별 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="43d40-142">Refresh an individual device</span></span>
* <span data-ttu-id="43d40-143">장치 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="43d40-143">Delete a device configuration</span></span>
* <span data-ttu-id="43d40-144">만료된 장치 암호 변경</span><span class="sxs-lookup"><span data-stu-id="43d40-144">Change an expired device password</span></span>
* <span data-ttu-id="43d40-145">실패한 장치 바꾸기</span><span class="sxs-lookup"><span data-stu-id="43d40-145">Replace a failed device</span></span>

> [!NOTE]
> <span data-ttu-id="43d40-146">Hello StorSimple 스냅숏 관리자 인터페이스를 사용 하는 방법에 대 한 일반 정보에 대 한 이동 너무[StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-146">For general information about using hello StorSimple Snapshot Manager interface, go too[StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>


## <a name="add-or-replace-a-device"></a><span data-ttu-id="43d40-147">장치 추가 또는 교체</span><span class="sxs-lookup"><span data-stu-id="43d40-147">Add or replace a device</span></span>
<span data-ttu-id="43d40-148">다음 프로시저 tooadd hello를 사용 하거나 StorSimple 장치를 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-148">Use hello following procedure tooadd or replace a StorSimple device.</span></span>

#### <a name="tooadd-or-replace-a-device"></a><span data-ttu-id="43d40-149">tooadd 또는 교체 장치</span><span class="sxs-lookup"><span data-stu-id="43d40-149">tooadd or replace a device</span></span>
1. <span data-ttu-id="43d40-150">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-150">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43d40-151">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **장치** 노드를 차례로 클릭 한 다음 **장치 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-151">In hello **Scope** pane, right-click hello **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="43d40-152">hello **장치 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-152">hello **Configure a Device** dialog box appears.</span></span>
   
    ![StorSimple 장치 구성](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. <span data-ttu-id="43d40-154">Hello에 **장치** 드롭다운 상자, hello 장치나 가상 장치로의 선택 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-154">In hello **Device** drop-down box, select hello IP address of hello device or virtual device.</span></span> 
4. <span data-ttu-id="43d40-155">Hello에 **암호** 텍스트 상자, hello Azure 클래식 포털의에서 hello 장치에 대해 만든 형식 hello StorSimple 스냅숏 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-155">In hello **Password** text box, type hello StorSimple Snapshot Manager password that you created for hello device in hello Azure classic portal.</span></span> <span data-ttu-id="43d40-156">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-156">Click **OK**.</span></span> <span data-ttu-id="43d40-157">StorSimple 스냅숏 관리자는 식별 된 hello 장치를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-157">StorSimple Snapshot Manager searches for hello device that you identified.</span></span> 
   
   * <span data-ttu-id="43d40-158">Hello 장치 표시 되 면 StorSimple 스냅숏 관리자 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-158">If hello device is available, StorSimple Snapshot Manager adds a connection.</span></span>
   * <span data-ttu-id="43d40-159">어떤 이유로 든 hello 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자 오류 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-159">If hello device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="43d40-160">클릭 **확인** tooclose hello 오류 메시지 및 클릭 **취소** tooclose hello **장치 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="43d40-160">Click **OK** tooclose hello error message, and then click **Cancel** tooclose hello **Configure a Device** dialog box.</span></span>

## <a name="connect-a-device-and-verify-imports"></a><span data-ttu-id="43d40-161">장치 연결 및 가져오기 확인</span><span class="sxs-lookup"><span data-stu-id="43d40-161">Connect a device and verify imports</span></span>
<span data-ttu-id="43d40-162">프로시저 tooconnect StorSimple 장치를 다음 hello를 사용 하 고 연결 된 백업을 있는 모든 기존 볼륨 그룹을 가져오는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-162">Use hello following procedure tooconnect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span></span>

#### <a name="tooconnect-a-device-and-verify-imports"></a><span data-ttu-id="43d40-163">장치 tooconnect 고 가져오기를 확인 하려면</span><span class="sxs-lookup"><span data-stu-id="43d40-163">tooconnect a device and verify imports</span></span>
1. <span data-ttu-id="43d40-164">tooconnect 장치 tooStorSimple 스냅숏 관리자 추가의 hello 지침에 따라 또는 장치를 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-164">tooconnect a device tooStorSimple Snapshot Manager, follow hello instructions in Add or replace a device.</span></span> <span data-ttu-id="43d40-165">서버에 연결 tooa 장치 StorSimple 스냅숏 관리자 다음과 같이 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-165">When it connects tooa device, StorSimple Snapshot Manager responds as follows:</span></span>
   
   * <span data-ttu-id="43d40-166">어떤 이유로 든 hello 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자 오류 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-166">If hello device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> 
   
   * <span data-ttu-id="43d40-167">Hello 장치 표시 되 면 StorSimple 스냅숏 관리자 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-167">If hello device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="43d40-168">Hello에 표시 하는 hello 장치를 선택 하면 **결과** 창의 hello 상태 필드에 해당 hello 장치가 표시 및 **사용 가능**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-168">When you select hello device, it appears in hello **Results** pane, and hello status field indicates that hello device is **Available**.</span></span> <span data-ttu-id="43d40-169">StorSimple 스냅숏 관리자 hello 볼륨 그룹에 연결 된 백업을 있는 hello 장치에 대해 구성 된 모든 볼륨 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-169">StorSimple Snapshot Manager imports any volume groups configured for hello device, provided that hello volume groups have associated backups.</span></span> <span data-ttu-id="43d40-170">백업 정책은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-170">Backup policies are not imported.</span></span> <span data-ttu-id="43d40-171">연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-171">Volume groups that do not have associated backups are not imported.</span></span>
2. <span data-ttu-id="43d40-172">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-172">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
3. <span data-ttu-id="43d40-173">Hello에서 마우스 오른쪽 단추로 클릭 hello 최상위 노드 **범위** 창과 클릭 **가져오기 표시 토글**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-173">Right-click hello top node in hello **Scope** pane, and then click **Toggle Imports Display**.</span></span>
   
    ![가져오기 표시 토글 선택](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. <span data-ttu-id="43d40-175">hello **가져오기 표시 토글** 볼륨 그룹과 백업을 가져온 hello 상태 hello 보여 주는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-175">hello **Toggle Imports Display** dialog box appears, showing hello status of hello imported volume groups and backups.</span></span> <span data-ttu-id="43d40-176">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-176">Click **OK**.</span></span>

<span data-ttu-id="43d40-177">StorSimple 스냅숏 관리자 toomanage를 정당한 hello 볼륨 그룹 및 백업을 성공적으로 가져왔는지 후 사용할 수 있습니다 볼륨 그룹과 백업을 만들고 StorSimple 스냅숏 관리자를 구성 하는 관리 하는 경우 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-177">After hello volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager toomanage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span></span> 

## <a name="refresh-connected-devices"></a><span data-ttu-id="43d40-178">연결된 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="43d40-178">Refresh connected devices</span></span>
<span data-ttu-id="43d40-179">다음 프로시저 toosynchronize hello 사용 하 여 hello StorSimple Snapshot Manager로 StorSimple 장치를 연결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-179">Use hello following procedure toosynchronize hello connected StorSimple devices with StorSimple Snapshot Manager.</span></span>

#### <a name="toorefresh-connected-devices"></a><span data-ttu-id="43d40-180">toorefresh 연결 된 장치</span><span class="sxs-lookup"><span data-stu-id="43d40-180">toorefresh connected devices</span></span>
1. <span data-ttu-id="43d40-181">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-181">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43d40-182">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **장치**, 클릭 하 고 **장치 새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-182">In hello **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span></span> <span data-ttu-id="43d40-183">이 동기화 hello 연결 된 장치 StorSimple 스냅숏 관리자를 사용 하 여 hello 볼륨 그룹과 백업을 최근에 추가한을 포함 하 여 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-183">This synchronizes hello connected devices with StorSimple Snapshot Manager so that you can view hello volume groups and backups, including any recent additions.</span></span> 
   
    ![Hello StorSimple 장치 새로 고침](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

<span data-ttu-id="43d40-185">hello **장치 새로 고침** 작업 연결 된 장치에서 모든 새 볼륨 그룹 및 연결 된 모든 백업을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-185">hello **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span></span> <span data-ttu-id="43d40-186">Hello와 달리 **볼륨 다시 검사** hello에 대 한 사용 가능한 동작 **볼륨** 노드를 **장치 새로 고침** hello 백업 레지스트리를 복원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-186">Unlike hello **Rescan volumes** action available for hello **Volumes** node, **Refresh Devices** does not restore hello backup registry.</span></span>

## <a name="authenticate-a-device"></a><span data-ttu-id="43d40-187">장치 인증</span><span class="sxs-lookup"><span data-stu-id="43d40-187">Authenticate a device</span></span>
<span data-ttu-id="43d40-188">다음 프로시저 tooauthenticate StorSimple 장치의 StorSimple 스냅숏 관리자 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-188">Use hello following procedure tooauthenticate a StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="tooauthenticate-a-device"></a><span data-ttu-id="43d40-189">tooauthenticate 장치</span><span class="sxs-lookup"><span data-stu-id="43d40-189">tooauthenticate a device</span></span>
1. <span data-ttu-id="43d40-190">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-190">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43d40-191">Hello에 **범위** 창에서 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-191">In hello **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="43d40-192">Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **Authenticate**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-192">In hello **Results** pane, right-click hello name of hello device, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="43d40-193">hello **Authenticate** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-193">hello **Authenticate** dialog box appears.</span></span> <span data-ttu-id="43d40-194">Hello 장치 암호를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-194">Type hello device password, and then click **OK**.</span></span>
   
    ![인증 대화 상자](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a><span data-ttu-id="43d40-196">장치 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="43d40-196">View device details</span></span>
<span data-ttu-id="43d40-197">다음 프로시저 tooview hello 세부 정보는 StorSimple 장치의 hello를 사용 하 여 하 고 필요한 경우 hello 장치 StorSimple 스냅숏 관리자를 다시 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-197">Use hello following procedure tooview hello details of a StorSimple device and, if necessary, resynchronize hello device with StorSimple Snapshot Manager.</span></span>

#### <a name="tooview-and-resynchronize-device-details"></a><span data-ttu-id="43d40-198">tooview 여 다시 동기화 할 장치 세부 정보</span><span class="sxs-lookup"><span data-stu-id="43d40-198">tooview and resynchronize device details</span></span>
1. <span data-ttu-id="43d40-199">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-199">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43d40-200">Hello에 **범위** 창에서 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-200">In hello **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="43d40-201">Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-201">In hello **Results** pane, right-click hello name of hello device, and then click **Details**.</span></span>

<span data-ttu-id="43d40-202">4. hello **장치 세부 정보** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-202">4.hello **Device Details** dialog box appears.</span></span> <span data-ttu-id="43d40-203">이 상자에 표시 hello 이름, 모델, 버전, 일련 번호, 상태, 대상 iSCSI 정규화 된 이름 (IQN) 마지막 동기화 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-203">This box shows hello name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span></span>

* <span data-ttu-id="43d40-204">클릭 **Resync** toosynchronize hello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-204">Click **Resync** toosynchronize hello device.</span></span>
* <span data-ttu-id="43d40-205">클릭 **확인** 또는 **취소** tooclose hello 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="43d40-205">Click **OK** or **Cancel** tooclose hello dialog box.</span></span>
  
  ![장치 세부 정보](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a><span data-ttu-id="43d40-207">개별 장치 새로 고침</span><span class="sxs-lookup"><span data-stu-id="43d40-207">Refresh an individual device</span></span>
<span data-ttu-id="43d40-208">다음 프로시저 tooresynchronize 개별 StorSimple 장치의 StorSimple 스냅숏 관리자 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-208">Use hello following procedure tooresynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="toorefresh-a-device"></a><span data-ttu-id="43d40-209">toorefresh 장치</span><span class="sxs-lookup"><span data-stu-id="43d40-209">toorefresh a device</span></span>
1. <span data-ttu-id="43d40-210">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-210">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="43d40-211">Hello에 **범위** 창에서 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-211">In hello **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="43d40-212">Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **장치 새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-212">In hello **Results** pane, right-click hello name of hello device, and then click **Refresh Device**.</span></span> <span data-ttu-id="43d40-213">Hello 장치를 StorSimple 스냅숏 관리자 동기화 설정.</span><span class="sxs-lookup"><span data-stu-id="43d40-213">This synchronizes hello device with StorSimple Snapshot Manager.</span></span>

## <a name="delete-a-device-configuration"></a><span data-ttu-id="43d40-214">장치 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="43d40-214">Delete a device configuration</span></span>
<span data-ttu-id="43d40-215">Hello 프로시저 toodelete 개별 StorSimple 장치 구성을 StorSimple 스냅숏 관리자에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-215">Use hello following procedure toodelete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span></span>

#### <a name="toodelete-a-device-configuration"></a><span data-ttu-id="43d40-216">toodelete 장치 구성</span><span class="sxs-lookup"><span data-stu-id="43d40-216">toodelete a device configuration</span></span>
1. <span data-ttu-id="43d40-217">Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-217">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43d40-218">Hello에 **범위** 창에서 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-218">In hello **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="43d40-219">Hello에 **결과** 창의 hello 장치의 hello 이름을 마우스 오른쪽 단추로 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-219">In hello **Results** pane, right-click hello name of hello device, and then click **Delete**.</span></span> 
4. <span data-ttu-id="43d40-220">hello 메시지의 뒤에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-220">hello following message appears.</span></span> <span data-ttu-id="43d40-221">클릭 **예** toodelete hello 구성 하거나 클릭 **아니요** toocancel hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-221">Click **Yes** toodelete hello configuration or click **No** toocancel hello deletion.</span></span>
   
    ![장치 구성 삭제](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a><span data-ttu-id="43d40-223">만료된 장치 암호 변경</span><span class="sxs-lookup"><span data-stu-id="43d40-223">Change an expired device password</span></span>
<span data-ttu-id="43d40-224">암호 tooauthenticate StorSimple 장치의 StorSimple 스냅숏 관리자를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-224">You must enter a password tooauthenticate a StorSimple device with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="43d40-225">Hello 장치를 Windows PowerShell 인터페이스 tooset hello를 사용 하는 경우이 암호를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-225">You configure this password when you use hello Windows PowerShell interface tooset up hello device.</span></span> <span data-ttu-id="43d40-226">그러나 hello 암호 만료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-226">However, hello password can expire.</span></span> <span data-ttu-id="43d40-227">이 경우에 hello Azure 클래식 포털 toochange hello 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-227">If this happens, you can use hello Azure classic portal toochange hello password.</span></span> <span data-ttu-id="43d40-228">다음 hello 장치 hello 암호 만료 되기 전에 StorSimple 스냅숏 관리자 구성에 있으므로 hello StorSimple 스냅숏 관리자에서 장치를 다시 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-228">Then, because hello device was configured in StorSimple Snapshot Manager before hello password expired, you must re-authenticate hello device in StorSimple Snapshot Manager.</span></span>

#### <a name="toochange-hello-expired-password"></a><span data-ttu-id="43d40-229">toochange hello 만료 된 암호</span><span class="sxs-lookup"><span data-stu-id="43d40-229">toochange hello expired password</span></span>
1. <span data-ttu-id="43d40-230">Azure 클래식 포털 hello hello StorSimple Manager 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-230">In hello Azure classic portal, start hello StorSimple Manager service.</span></span>
2. <span data-ttu-id="43d40-231">클릭 **장치** > **구성** hello 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-231">Click **Devices** > **Configure** for hello device.</span></span>
3. <span data-ttu-id="43d40-232">StorSimple 스냅숏 관리자 섹션 toohello 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="43d40-232">Scroll down toohello StorSimple Snapshot Manager section.</span></span> <span data-ttu-id="43d40-233">14-15자로 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-233">Enter a password that is 14-15 characters.</span></span> <span data-ttu-id="43d40-234">해당 hello 암호에 대문자, 소문자, 숫자 및 특수 문자의 조합을 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-234">Make sure that hello password contains a mix of uppercase, lowercase, numeric, and special characters.</span></span>
4. <span data-ttu-id="43d40-235">Hello 암호 tooconfirm 재입력 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-235">Re-enter hello password tooconfirm it.</span></span>
5. <span data-ttu-id="43d40-236">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-236">Click **Save** at hello bottom of hello page.</span></span>

#### <a name="toore-authenticate-hello-device"></a><span data-ttu-id="43d40-237">toore-hello 장치 인증</span><span class="sxs-lookup"><span data-stu-id="43d40-237">toore-authenticate hello device</span></span>
1. <span data-ttu-id="43d40-238">StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-238">Start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43d40-239">Hello에 **범위** 창에서 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-239">In hello **Scope** pane, click **Devices**.</span></span> <span data-ttu-id="43d40-240">Hello에 구성 된 장치 목록을 표시 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="43d40-240">A list of configured devices appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="43d40-241">Hello 장치와 마우스 오른쪽 단추를 클릭 한 다음 선택 **Authenticate**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-241">Select hello device, right-click, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="43d40-242">Hello에 **Authenticate** 창의 hello 새 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-242">In hello **Authenticate** window, enter hello new password.</span></span>
5. <span data-ttu-id="43d40-243">Hello 장치, 마우스 선택 선택 **장치 새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-243">Select hello device, right-click, and select **Refresh device**.</span></span> <span data-ttu-id="43d40-244">Hello 장치를 StorSimple 스냅숏 관리자 동기화 설정.</span><span class="sxs-lookup"><span data-stu-id="43d40-244">This synchronizes hello device with StorSimple Snapshot Manager.</span></span>

## <a name="replace-a-failed-device"></a><span data-ttu-id="43d40-245">실패한 장치 바꾸기</span><span class="sxs-lookup"><span data-stu-id="43d40-245">Replace a failed device</span></span>
<span data-ttu-id="43d40-246">StorSimple 장치 실패 하 고이 경우 대기 (장애 조치) 장치를 사용 하 여 hello tooconnect 단계 다음으로 대체 toohello 새 장치 및 보기 hello 연결 된 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-246">If a StorSimple device fails and is replaced by a standby (failover) device, use hello following steps tooconnect toohello new device and view hello associated backups.</span></span>

#### <a name="tooconnect-tooa-new-device-after-failover"></a><span data-ttu-id="43d40-247">장애 조치 후 tooconnect tooa 새 장치</span><span class="sxs-lookup"><span data-stu-id="43d40-247">tooconnect tooa new device after failover</span></span>
1. <span data-ttu-id="43d40-248">Hello iSCSI 연결 toohello 새 장치를 다시 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-248">Reconfigure hello iSCSI connection toohello new device.</span></span> <span data-ttu-id="43d40-249">자세한 내용은 이동 너무 "7 단계: 탑재, 초기화, 및 서식 볼륨"에서 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-249">For instructions, go too"Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!NOTE]
> <span data-ttu-id="43d40-250">StorSimple 장치를 새 hello 이전과 hello와 같은 IP 주소를 hello에, 수 tooconnect hello 이전 구성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-250">If hello new StorSimple device has hello same IP address as hello old one, you might be able tooconnect hello old configuration.</span></span>


1. <span data-ttu-id="43d40-251">Hello Microsoft StorSimple 관리 서비스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-251">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="43d40-252">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-252">Start Server Manager.</span></span>
   2. <span data-ttu-id="43d40-253">Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-253">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="43d40-254">Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-254">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="43d40-255">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-255">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
2. <span data-ttu-id="43d40-256">Hello 구성 정보 관련된 toohello 오래 된 장치를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-256">Remove hello configuration information related toohello old device:</span></span>
   
   1. <span data-ttu-id="43d40-257">파일 탐색기에서 tooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-257">In File Explorer, browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   2. <span data-ttu-id="43d40-258">Hello BACatalog 폴더의 hello 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-258">Delete hello files in hello BACatalog folder.</span></span>
3. <span data-ttu-id="43d40-259">Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-259">Restart hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="43d40-260">Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-260">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="43d40-261">Hello에 **서비스** 창, 선택 hello **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-261">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="43d40-262">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-262">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span>
4. <span data-ttu-id="43d40-263">StorSimple 스냅숏 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-263">Start StorSimple Snapshot Manager.</span></span>
5. <span data-ttu-id="43d40-264">tooconfigure hello 새 StorSimple 장치 2 단계에서에서 단계를 완료 hello:에 StorSimple 장치를 연결할 [StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-264">tooconfigure hello new StorSimple device, complete hello steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
6. <span data-ttu-id="43d40-265">마우스 오른쪽 단추로 클릭 hello 최상위 노드를 hello **범위** 창 (StorSimple 스냅숏 관리자 hello 예제)을 마우스 클릭 한 다음 **가져오기 표시 토글**합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-265">Right-click hello top-level node in hello **Scope** pane (StorSimple Snapshot Manager in hello example), and then click **Toggle Imports Display**.</span></span> 
7. <span data-ttu-id="43d40-266">Hello 가져온 볼륨 그룹 및 백업을 StorSimple 스냅숏 관리자에 표시 되 면 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-266">A message appears when hello imported volume groups and backups are visible in StorSimple Snapshot Manager.</span></span> <span data-ttu-id="43d40-267">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-267">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43d40-268">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43d40-268">Next steps</span></span>
* <span data-ttu-id="43d40-269">너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-269">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="43d40-270">너무 방법에 대해 알아봅니다[tooview StorSimple 스냅숏 관리자를 사용 하 고 볼륨 관리](storsimple-snapshot-manager-manage-volumes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43d40-270">Learn how too[use StorSimple Snapshot Manager tooview and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span></span>

