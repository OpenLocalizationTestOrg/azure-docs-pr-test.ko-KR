---
title: "호스트에 MPIO aaaConfigure 연결 tooStorSimple 가상 배열 | Microsoft Docs"
description: "Tooconfigure 다중 경로 I/O (MPIO) StorSimple 가상 배열에 대 한 Windows Server 2012 r 2를 실행 하는 tooa 호스트를 연결 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a><span data-ttu-id="f0df6-103">StorSimple 가상 배열 hello에 대 한 Windows Server 호스트에서 다중 경로 I/O를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-103">Configure Multipath I/O on Windows Server host for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="f0df6-104">개요</span><span class="sxs-lookup"><span data-stu-id="f0df6-104">Overview</span></span>
<span data-ttu-id="f0df6-105">이 문서에 tooinstall 다중 경로 I/O 기능 (MPIO) Windows Server 호스트에 StorSimple 전용 볼륨에 대 한 특정 구성 설정을 적용 하 고 다음 StorSimple 볼륨에 대 한 MPIO를 확인 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-105">This article describes how tooinstall Multipath I/O feature (MPIO) on your Windows Server host, apply specific configuration settings for StorSimple-only volumes, and then verify MPIO for StorSimple volumes.</span></span> <span data-ttu-id="f0df6-106">hello 프로시저 1200 StorSimple 가상 배열 두 네트워크 인터페이스가 있는 두 개의 네트워크 인터페이스와 연결 된 tooa Windows Server 호스트 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-106">hello procedure assumes that your StorSimple 1200 Virtual Array with two network interfaces is connected tooa Windows Server host with two network interfaces.</span></span> <span data-ttu-id="f0df6-107">이 문서에 포함 된 hello 정보 toohello 가상 배열만을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-107">hello information contained in this article applies only toohello virtual array.</span></span> <span data-ttu-id="f0df6-108">StorSimple 8000 시리즈 장치에 대 한 내용은 이동 너무[StorSimple 호스트에 대 한 MPIO 구성](storsimple-configure-mpio-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-108">For information on StorSimple 8000 series devices, go too[Configure MPIO for StorSimple host](storsimple-configure-mpio-windows-server.md).</span></span> 

<span data-ttu-id="f0df6-109">Windows Server는 데 도움이 됩니다 빌드 내결함성 / 고가용성 저장소 구성의 hello MPIO 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-109">hello MPIO feature in Windows Server helps build highly available, fault-tolerant storage configurations.</span></span> <span data-ttu-id="f0df6-110">중복 된 실제 경로 구성 요소를 사용 하는 MPIO-어댑터, 케이블 및 스위치-hello 서버와 hello 저장소 장치 사이 toocreate 논리 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-110">MPIO uses redundant physical path components — adapters, cables, and switches — toocreate logical paths between hello server and hello storage device.</span></span> <span data-ttu-id="f0df6-111">구성 요소 오류가 있으면 발생 논리 경로 toofail 다중 경로 제어 논리는 사용 대체 경로 I/O에 대 한 응용 프로그램 데이터에 계속 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-111">If there is a component failure, causing a logical path toofail, multipathing logic uses an alternate path for I/O so that applications can still access their data.</span></span> <span data-ttu-id="f0df6-112">또한 구성에 따라 MPIO도 성능을 향상 시킬 수 이러한 모든 경로에서 다시 hello 부하 균형을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-112">Additionally depending on your configuration, MPIO can also improve performance by re-balancing hello load across all these paths.</span></span> <span data-ttu-id="f0df6-113">자세한 내용은 [MPIO 개요](https://technet.microsoft.com/library/cc725907.aspx "MPIO 개요 and features")을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0df6-113">For more information, see [MPIO overview](https://technet.microsoft.com/library/cc725907.aspx "MPIO overview and features").</span></span>

<span data-ttu-id="f0df6-114">고가용성에 대 한 hello StorSimple 솔루션의, Windows Server 호스트 연결 된 tooyour StorSimple 가상 배열 (모델 1200) hello에서 MPIO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-114">For hello high-availability of your StorSimple solution, configure MPIO on hello Windows Server hosts connected tooyour StorSimple Virtual Array (model 1200).</span></span> <span data-ttu-id="f0df6-115">호스트 서버 hello 링크, 네트워크 또는 인터페이스 오류에 다음 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-115">hello host servers can then tolerate a link, network, or interface failure.</span></span> 

<span data-ttu-id="f0df6-116">이러한 단계 tooconfigure MPIO toofollow이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-116">You will need toofollow these steps tooconfigure MPIO:</span></span> 

* <span data-ttu-id="f0df6-117">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f0df6-117">Configuration prerequisites</span></span>
* <span data-ttu-id="f0df6-118">1 단계: hello Windows Server 호스트에 MPIO 설치</span><span class="sxs-lookup"><span data-stu-id="f0df6-118">Step 1: Install MPIO on hello Windows Server host</span></span>
* <span data-ttu-id="f0df6-119">2단계: StorSimple 볼륨에 대한 MPIO 구성</span><span class="sxs-lookup"><span data-stu-id="f0df6-119">Step 2: Configure MPIO for StorSimple volumes</span></span>
* <span data-ttu-id="f0df6-120">3 단계:에 StorSimple 볼륨 탑재 hello 호스트</span><span class="sxs-lookup"><span data-stu-id="f0df6-120">Step 3: Mount StorSimple volumes on hello host</span></span>

<span data-ttu-id="f0df6-121">각 단계는 hello hello 다음 섹션에서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-121">Each of hello above steps is discussed in hello following sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0df6-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f0df6-122">Prerequisites</span></span>
<span data-ttu-id="f0df6-123">이 섹션 hello Windows Server 호스트 및 가상 배열에 대 한 hello 구성 필수 구성 요소에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-123">This section details hello configuration prerequisites for hello Windows Server host and your virtual array.</span></span>

### <a name="on-windows-server-host"></a><span data-ttu-id="f0df6-124">Windows Server 호스트</span><span class="sxs-lookup"><span data-stu-id="f0df6-124">On Windows Server host</span></span>
* <span data-ttu-id="f0df6-125">Windows Server 호스트에 사용 가능한 2개의 네트워크 인터페이스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-125">Make sure that your Windows Server host has 2 network interfaces enabled.</span></span>

### <a name="on-storsimple-virtual-array"></a><span data-ttu-id="f0df6-126">StorSimple 가상 배열에서</span><span class="sxs-lookup"><span data-stu-id="f0df6-126">On StorSimple Virtual Array</span></span>
* <span data-ttu-id="f0df6-127">hello 가상 배열 iSCSI 서버로 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-127">hello virtual array should be configured as an iSCSI server.</span></span> <span data-ttu-id="f0df6-128">toolearn 더 참조 [iSCSI 서버와 가상 배열 설정](storsimple-virtual-array-deploy3-iscsi-setup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-128">toolearn more, see [set up virtual array as an iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md).</span></span> <span data-ttu-id="f0df6-129">Hello 배열에서 하나 이상의 네트워크 인터페이스를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-129">One or more network interfaces should be enabled on hello array.</span></span>   
* <span data-ttu-id="f0df6-130">가상 배열에서 네트워크 인터페이스 hello hello Windows Server 호스트에서 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-130">hello network interfaces on your virtual array should be reachable from hello Windows Server host.</span></span>
* <span data-ttu-id="f0df6-131">StorSimple 가상 배열에 하나 이상의 볼륨을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-131">One or more volumes should be created on your StorSimple Virtual Array.</span></span> <span data-ttu-id="f0df6-132">toolearn 더 참조 [볼륨 추가](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) StorSimple 가상 배열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-132">toolearn more, see [Add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) on your StorSimple Virtual Array.</span></span> <span data-ttu-id="f0df6-133">이 절차에서는 hello 가상 배열에 3 볼륨 (1 로컬로 고정 된 볼륨 및 2 계층화 된 볼륨에 표시 된 대로 아래) 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-133">In this procedure, we created 3 volumes (1 locally pinned and 2 tiered volumes as shown below) on hello virtual array.</span></span>
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a><span data-ttu-id="f0df6-135">StorSimple 가상 배열에 대한 하드웨어 구성</span><span class="sxs-lookup"><span data-stu-id="f0df6-135">Hardware configuration for StorSimple Virtual Array</span></span>
<span data-ttu-id="f0df6-136">아래 hello 그림 고가용성에 대 한 hello 하드웨어 구성 및 Windows Server 호스트와이 절차에 사용 되는 StorSimple 가상 배열에 대 한 다중 경로 제어 부하 분산을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-136">hello figure below shows hello hardware configuration for high availability and load-balancing multipathing for your Windows Server host and StorSimple Virtual Array used in this procedure.</span></span>

![mpio 하드웨어 구성](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

<span data-ttu-id="f0df6-138">와 같이 앞 그림 hello:</span><span class="sxs-lookup"><span data-stu-id="f0df6-138">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="f0df6-139">Hyper-V에 프로비전된 StorSimple 가상 배열은 iSCSI 서버로 구성된 단일 노드 활성 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-139">Your StorSimple Virtual Array provisioned on Hyper-V is a single node active device configured as an iSCSI server.</span></span>
* <span data-ttu-id="f0df6-140">배열에 두 개의 가상 네트워크 인터페이스가 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-140">Two virtual network interfaces are enabled on your array.</span></span> <span data-ttu-id="f0df6-141">Hello 로컬 웹 UI 가상 배열에서 너무 이동 하 여 두 개의 네트워크 인터페이스를 사용할 수 있는지를 확인**네트워크 설정을** 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="f0df6-141">In hello local web UI of your virtual array, verify that two network interfaces are enabled by navigating too**Network Settings** as shown below:</span></span>
  
    ![1200에 활성화된 네트워크 인터페이스](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    <span data-ttu-id="f0df6-143">참고 hello IPv4 주소를 사용 하도록 설정 하는 hello 네트워크 인터페이스 (이더넷, 기본적으로 Ethernet 2)을 나중에 사용할 hello 호스트에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-143">Note hello IPv4 addresses of hello enabled network interfaces (Ethernet, Ethernet 2 by default) and save for later use on hello host.</span></span>
* <span data-ttu-id="f0df6-144">Windows Server 호스트에 두 개의 네트워크 인터페이스가 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-144">Two network interfaces are enabled on your Windows Server host.</span></span> <span data-ttu-id="f0df6-145">호스트 및 배열에 대 한 연결 된 인터페이스에는 경우 hello 동일한 서브넷을 사용할 수 있는 네 개의 경로 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-145">If hello connected interfaces for host and array are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="f0df6-146">이이 절차에서는 대/소문자 hello 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-146">This was hello case in this procedure.</span></span> <span data-ttu-id="f0df6-147">그러나 hello 배열과 호스트 인터페이스의 각 네트워크 인터페이스에 있고 다른 IP 서브넷 (라우팅할 수 없음), 2 경로 사용할 수 됩니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-147">However, if each network interface on hello array and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span>

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a><span data-ttu-id="f0df6-148">1 단계: hello Windows Server 호스트에 MPIO 설치</span><span class="sxs-lookup"><span data-stu-id="f0df6-148">Step 1: Install MPIO on hello Windows Server host</span></span>
<span data-ttu-id="f0df6-149">MPIO는 Windows Server에서 선택적 기능이며 기본적으로 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-149">MPIO is an optional feature on Windows Server and is not installed by default.</span></span> <span data-ttu-id="f0df6-150">서버 관리자를 통해 기능으로 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-150">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="f0df6-151">Windows Server 호스트에서이 기능을 완료 tooinstall 프로시저 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-151">tooinstall this feature on your Windows Server host, complete hello following procedure.</span></span>

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a><span data-ttu-id="f0df6-152">2단계: StorSimple 볼륨에 대한 MPIO 구성</span><span class="sxs-lookup"><span data-stu-id="f0df6-152">Step 2: Configure MPIO for StorSimple volumes</span></span>
<span data-ttu-id="f0df6-153">MPIO 구성 toobe tooidentify StorSimple 볼륨 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-153">MPIO needs toobe configured tooidentify StorSimple volumes.</span></span> <span data-ttu-id="f0df6-154">tooconfigure MPIO toorecognize StorSimple 볼륨 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-154">tooconfigure MPIO toorecognize StorSimple volumes, perform hello following steps.</span></span>

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a><span data-ttu-id="f0df6-155">3 단계:에 StorSimple 볼륨 탑재 hello 호스트</span><span class="sxs-lookup"><span data-stu-id="f0df6-155">Step 3: Mount StorSimple volumes on hello host</span></span>
<span data-ttu-id="f0df6-156">Windows 서버에서 MPIO를 구성한 후 hello StorSimple 배열에서 만들었으며 탑재할 수 있으며 그러면 중복성을 위해 MPIO 활용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-156">After MPIO is configured on Windows Server, volume(s) created on hello StorSimple array can be mounted and can then take advantage of MPIO for redundancy.</span></span> <span data-ttu-id="f0df6-157">볼륨을 toomount hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-157">toomount a volume, perform hello following steps.</span></span>

#### <a name="toomount-volumes-on-hello-host"></a><span data-ttu-id="f0df6-158">hello 호스트에서 toomount 볼륨</span><span class="sxs-lookup"><span data-stu-id="f0df6-158">toomount volumes on hello host</span></span>
1. <span data-ttu-id="f0df6-159">열기 hello **iSCSI 초기자 속성** hello Windows Server 호스트에는 창입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-159">Open hello **iSCSI Initiator Properties** window on hello Windows Server host.</span></span> <span data-ttu-id="f0df6-160">너무 이동**서버 관리자 > 대시보드 > 도구 > iSCSI 초기자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-160">Go too**Server Manager > Dashboard > Tools > iSCSI Initiator**.</span></span>
2. <span data-ttu-id="f0df6-161">Hello에 **iSCSI 초기자 속성** 대화 상자를 클릭 **검색**, 클릭 하 고 **대상 포털 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-161">In hello **iSCSI Initiator Properties** dialog box, click **Discovery**, and then click **Discover Target Portal**.</span></span>
3. <span data-ttu-id="f0df6-162">Hello에 **대상 포털 검색** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-162">In hello **Discover Target Portal** dialog box, do hello following:</span></span>
   
    1. <span data-ttu-id="f0df6-163">StorSimple 가상 배열에 지원 되는 네트워크 인터페이스를 첫 번째 hello hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-163">Enter hello IP address of hello first enabled network interface on your StorSimple Virtual Array.</span></span> <span data-ttu-id="f0df6-164">기본적으로 **이더넷**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-164">By default, this would be **Ethernet**.</span></span> 
    2. <span data-ttu-id="f0df6-165">클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f0df6-165">Click **OK** tooreturn toohello **iSCSI Initiator Properties** dialog box.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="f0df6-166">ISCSI 연결에 대 한 개인 네트워크를 사용 하는 연결 된 toohello 개인 네트워크 hello 데이터 포트의 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-166">If you are using a private network for iSCSI connections, enter hello IP address of hello DATA port that is connected toohello private network.</span></span>
     
4. <span data-ttu-id="f0df6-167">배열의 두 번째 네트워크 인터페이스(예: 이더넷 2)에 대해 2~3단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-167">Repeat steps 2-3 for a second network interface (for example, Ethernet 2) on your array.</span></span> 
5. <span data-ttu-id="f0df6-168">선택 hello **대상** hello 탭 **iSCSI 초기자 속성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f0df6-168">Select hello **Targets** tab in hello **iSCSI Initiator Properties** dialog box.</span></span> <span data-ttu-id="f0df6-169">가상 배열의 경우 각 볼륨 서피스가 **검색된 대상**아래에 대상으로 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-169">For your virtual array, you should see each volume surface as a target under **Discovered Targets**.</span></span> <span data-ttu-id="f0df6-170">이 경우 3 개의 대상 (해당 toothree 볼륨)는 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-170">In this case, three targets (corresponding toothree volumes) would be discovered.</span></span>
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. <span data-ttu-id="f0df6-172">클릭 **연결** tooestablish StorSimple 가상 배열와 iSCSI 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-172">Click **Connect** tooestablish an iSCSI session with your StorSimple Virtual Array.</span></span> <span data-ttu-id="f0df6-173">A **tooTarget 연결** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-173">A **Connect tooTarget** dialog box will appear.</span></span> <span data-ttu-id="f0df6-174">선택 hello **다중 경로 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-174">Select hello **Enable multi-path** check box.</span></span> <span data-ttu-id="f0df6-175">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-175">Click **Advanced**.</span></span>
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. <span data-ttu-id="f0df6-177">Hello에 **고급 설정** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-177">In hello **Advanced Settings** dialog box, do hello following:</span></span>                                        
   
    1. <span data-ttu-id="f0df6-178">Hello에 **로컬 어댑터** 드롭 다운 목록 **Microsoft iSCSI 초기자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-178">On hello **Local Adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
    2. <span data-ttu-id="f0df6-179">Hello에 **초기자 IP** 드롭 다운 목록, hello 호스트의 IP 주소 선택 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-179">On hello **Initiator IP** drop-down list, select hello IP address of hello host.</span></span>
    3. <span data-ttu-id="f0df6-180">Hello에 **대상 포털** IP 드롭 다운 목록, 배열 인터페이스의 선택 hello IP입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-180">On hello **Target Portal** IP drop-down list, select hello IP of array interface.</span></span>
    4. <span data-ttu-id="f0df6-181">클릭 **확인** tooreturn toohello **iSCSI 초기자 속성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f0df6-181">Click **OK** tooreturn toohello **iSCSI Initiator Properties** dialog box.</span></span>
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. <span data-ttu-id="f0df6-183">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-183">Click **Properties**.</span></span> 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. <span data-ttu-id="f0df6-185">Hello에 **속성** 대화 상자를 클릭 **세션 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-185">In hello **Properties** dialog box, click **Add Session**.</span></span>
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. <span data-ttu-id="f0df6-187">Hello에 **tooTarget 연결** 대화 상자, 선택 hello **다중 경로 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-187">In hello **Connect tooTarget** dialog box, select hello **Enable multi-path** check box.</span></span> <span data-ttu-id="f0df6-188">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-188">Click **Advanced**.</span></span>
11. <span data-ttu-id="f0df6-189">Hello에 **고급 설정** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="f0df6-189">In hello **Advanced Settings** dialog box:</span></span>                                        
    
    1. <span data-ttu-id="f0df6-190">Hello에 **로컬 어댑터** 드롭 다운 목록에서 선택 Microsoft iSCSI 초기자입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-190">On hello **Local adapter** drop-down list, select Microsoft iSCSI Initiator.</span></span>

    2. <span data-ttu-id="f0df6-191">Hello에 **초기자 IP** 드롭 다운 목록, 선택 hello IP 주소 해당 toohello 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-191">On hello **Initiator IP** drop-down list, select hello IP address corresponding toohello host.</span></span> <span data-ttu-id="f0df6-192">이 경우에 hello 호스트에 hello 배열 tooa 단일 네트워크 인터페이스에서 두 개의 네트워크 인터페이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-192">In this case, you are connecting two network interfaces on hello array tooa single network interface on hello host.</span></span> <span data-ttu-id="f0df6-193">따라서이 인터페이스는 첫 번째 세션 hello에 대 한 제공 된 것과 동일한 안녕 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-193">Therefore, this interface is hello same as that provided for hello first session.</span></span>

    3. <span data-ttu-id="f0df6-194">Hello에 **대상 포털 IP** 드롭 다운 목록, hello hello 배열에서 사용할 수는 두 번째 데이터 인터페이스에 대 한 선택 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-194">On hello **Target Portal IP** drop-down list, select hello IP address for hello second data interface enabled on hello array.</span></span>

    4. <span data-ttu-id="f0df6-195">클릭 **확인** tooreturn toohello iSCSI 초기자 속성 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f0df6-195">Click **OK** tooreturn toohello iSCSI Initiator Properties dialog box.</span></span> <span data-ttu-id="f0df6-196">두 번째 세션 toohello 대상을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-196">You have added a second session toohello target.</span></span>
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. <span data-ttu-id="f0df6-198">Hello에 원하는 hello 세션 (경로)를 추가한 후 **iSCSI 초기자 속성** 대화 상자, 선택 hello 대상 및 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-198">After adding hello desired sessions (paths), in hello **iSCSI Initiator Properties** dialog box, select hello target and click **Properties**.</span></span> <span data-ttu-id="f0df6-199">Hello 세션 탭의 hello **속성** 대화 상자, 참고 hello 4 개 세션 식별자는 toohello 가능한 경로 순열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-199">On hello Sessions tab of hello **Properties** dialog box, note hello four session identifiers that correspond toohello possible path permutations.</span></span> <span data-ttu-id="f0df6-200">세션을 toocancel hello 확인란 다음 tooa 세션 식별자를 선택한 다음 클릭 **연결 끊기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-200">toocancel a session, select hello check box next tooa session identifier, and then click **Disconnect**.</span></span>

    6. <span data-ttu-id="f0df6-201">선택 hello 세션 내에서 제공 되는 tooview 장치 **장치** 탭 tooconfigure hello 선택한 장치에 대해 MPIO 정책을 클릭 **MPIO**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-201">tooview devices presented within sessions, select hello **Devices** tab. tooconfigure hello MPIO policy for a selected device, click **MPIO**.</span></span>

    7. <span data-ttu-id="f0df6-202">hello **세부 정보** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-202">hello **Details** dialog box will appear.</span></span> <span data-ttu-id="f0df6-203">Hello에 **MPIO** 탭을 적절 한 hello를 선택할 수 있습니다 **부하 분산 정책** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-203">On hello **MPIO** tab, you can select hello appropriate **Load Balance Policy** settings.</span></span> <span data-ttu-id="f0df6-204">Hello를 볼 수도 있습니다 **활성** 또는 **대기** 경로 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-204">You can also view hello **Active** or **Standby** path type.</span></span>
12. <span data-ttu-id="f0df6-205">Tooadd 추가 세션 (경로) toohello 대상 8-11 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-205">Repeat steps 8-11 tooadd additional sessions (paths) toohello target.</span></span> <span data-ttu-id="f0df6-206">Hello 호스트에 두 개의 인터페이스 및 hello 가상 배열에 2 개 사용 하 여 각 대상에 대 한 4 개 세션의 합계를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-206">With two interfaces on hello host and two on hello virtual array, you can add a total of four sessions for each target.</span></span> 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. <span data-ttu-id="f0df6-208">각 볼륨 (화면을 대상으로 표시)에 대해 이러한 단계 toorepeat를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-208">You will need toorepeat these steps for each volume (surfaces as a target).</span></span>
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. <span data-ttu-id="f0df6-210">열기 **컴퓨터 관리** 너무 이동 하 여**서버 관리자 > 대시보드 > 컴퓨터 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-210">Open **Computer Management** by navigating too**Server Manager > Dashboard > Computer Management**.</span></span> <span data-ttu-id="f0df6-211">Hello 왼쪽된 창에서 클릭 **저장소 > 디스크 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-211">In hello left pane, click **Storage > Disk Management**.</span></span> <span data-ttu-id="f0df6-212">hello는 표시 toothis 호스트 hello StorSimple 가상 배열에서 만든 볼륨 아래에 표시 될 **디스크 관리** 새 디스크로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-212">hello volume(s) created on hello StorSimple Virtual Array that are visible toothis host will appear under **Disk Management** as new disk(s).</span></span>
15. <span data-ttu-id="f0df6-213">Hello 디스크를 초기화 하 고 새 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-213">Initialize hello disk and create a new volume.</span></span> <span data-ttu-id="f0df6-214">Hello 포맷 프로세스 동안 64kb 할당 단위 크기 (AUS)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-214">During hello format process, select an allocation unit size (AUS) of 64 KB.</span></span> <span data-ttu-id="f0df6-215">Hello 사용 가능한 모든 볼륨에 대 한 hello 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-215">Repeat hello process for all hello available volumes.</span></span>
    
    ![디스크 관리](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. <span data-ttu-id="f0df6-217">**디스크 관리**를 마우스 오른쪽 단추로 클릭 hello **디스크** 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-217">Under **Disk Management**, right-click hello **Disk** and select **Properties**.</span></span>
17. <span data-ttu-id="f0df6-218">Hello에 **다중 경로 디스크 장치 속성** 대화 상자를 클릭 hello **MPIO** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-218">In hello **Multi-Path Disk Device Properties** dialog box, click hello **MPIO** tab.</span></span>
    
    ![디스크 속성](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. <span data-ttu-id="f0df6-220">Hello에 **DSM 이름** 섹션에서 클릭 **세부 정보** hello 매개 변수 toohello 기본 매개 변수를 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-220">In hello **DSM Name** section, click **Details** and verify that hello parameters are set toohello default parameters.</span></span> <span data-ttu-id="f0df6-221">hello 기본 매개 변수는:</span><span class="sxs-lookup"><span data-stu-id="f0df6-221">hello default parameters are:</span></span>
    
    * <span data-ttu-id="f0df6-222">경로 확인 기간 = 30</span><span class="sxs-lookup"><span data-stu-id="f0df6-222">Path Verify Period = 30</span></span>
    * <span data-ttu-id="f0df6-223">재시도 횟수 = 3</span><span class="sxs-lookup"><span data-stu-id="f0df6-223">Retry Count = 3</span></span>
    * <span data-ttu-id="f0df6-224">PDO 제거 기간 = 20</span><span class="sxs-lookup"><span data-stu-id="f0df6-224">PDO Remove Period = 20</span></span>
    * <span data-ttu-id="f0df6-225">재시도 간격 = 1</span><span class="sxs-lookup"><span data-stu-id="f0df6-225">Retry Interval = 1</span></span>
    * <span data-ttu-id="f0df6-226">경로 확인 사용 = 선택하지 않음</span><span class="sxs-lookup"><span data-stu-id="f0df6-226">Path Verify Enabled = Unchecked.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f0df6-227">**Hello 기본 매개 변수를 수정 하지 마십시오.**</span><span class="sxs-lookup"><span data-stu-id="f0df6-227">**Do not modify hello default parameters.**</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="f0df6-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0df6-228">Next steps</span></span>
<span data-ttu-id="f0df6-229">에 대 한 자세한 내용은 [StorSimple 장치 관리자 서비스 tooadminister StorSimple 가상 배열 hello를 사용 하 여](storsimple-virtual-array-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0df6-229">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span>

