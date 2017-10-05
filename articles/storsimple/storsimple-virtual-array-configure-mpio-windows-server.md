---
title: "StorSimple Virtual Array에 연결된 호스트에서 MPIO 구성| Microsoft Docs"
description: "Windows Server 2012 R2를 실행하는 호스트에 연결된 StorSimple 가상 배열에 대해 MPIO(다중 경로 I/O)를 구성하는 방법을 설명합니다."
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
ms.openlocfilehash: c75c6ed40754aee964e2b68f4f569dc1422507f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-the-storsimple-virtual-array"></a><span data-ttu-id="54ee9-103">Windows Server 호스트에 StorSimple 가상 배열에 대한 다중 경로 I/O 구성</span><span class="sxs-lookup"><span data-stu-id="54ee9-103">Configure Multipath I/O on Windows Server host for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="54ee9-104">개요</span><span class="sxs-lookup"><span data-stu-id="54ee9-104">Overview</span></span>
<span data-ttu-id="54ee9-105">이 문서에서는 Windows Server 호스트에 MPIO(다중 경로 I/O) 기능을 설치하고, StorSimple 전용 볼륨에 대한 특정 구성 설정을 적용한 다음 StorSimple 볼륨의 MPIO를 확인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-105">This article describes how to install Multipath I/O feature (MPIO) on your Windows Server host, apply specific configuration settings for StorSimple-only volumes, and then verify MPIO for StorSimple volumes.</span></span> <span data-ttu-id="54ee9-106">이 절차에서는 두 개의 네트워크 인터페이스가 있는 StorSimple 1200 가상 배열이 두 개의 네트워크 인터페이스가 있는 Windows Server 호스트에 연결된 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-106">The procedure assumes that your StorSimple 1200 Virtual Array with two network interfaces is connected to a Windows Server host with two network interfaces.</span></span> <span data-ttu-id="54ee9-107">이 문서에 포함된 정보는 가상 배열에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-107">The information contained in this article applies only to the virtual array.</span></span> <span data-ttu-id="54ee9-108">StorSimple 8000 시리즈 장치에 대한 자세한 내용은 [StorSimple 호스트에 대한 MPIO 구성](storsimple-configure-mpio-windows-server.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54ee9-108">For information on StorSimple 8000 series devices, go to [Configure MPIO for StorSimple host](storsimple-configure-mpio-windows-server.md).</span></span> 

<span data-ttu-id="54ee9-109">Windows Server의 MPIO 기능은 가용성이 높고 내결함성을 갖춘 저장소 구성을 빌드하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-109">The MPIO feature in Windows Server helps build highly available, fault-tolerant storage configurations.</span></span> <span data-ttu-id="54ee9-110">MPIO는 중복 실제 경로 구성 요소(어댑터, 케이블 및 스위치)를 사용하여 서버 및 저장소 장치 간의 논리 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-110">MPIO uses redundant physical path components — adapters, cables, and switches — to create logical paths between the server and the storage device.</span></span> <span data-ttu-id="54ee9-111">논리 경로에 오류를 일으키는 구성 요소 오류가 발생할 경우 응용 프로그램이 데이터에 계속 액세스할 수 있도록 다중 경로 논리가 I/O에 대한 대체 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-111">If there is a component failure, causing a logical path to fail, multipathing logic uses an alternate path for I/O so that applications can still access their data.</span></span> <span data-ttu-id="54ee9-112">또한 구성에 따라 MPIO가 이러한 모든 경로에서 부하를 다시 분산하여 성능을 향상할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-112">Additionally depending on your configuration, MPIO can also improve performance by re-balancing the load across all these paths.</span></span> <span data-ttu-id="54ee9-113">자세한 내용은 [MPIO 개요](https://technet.microsoft.com/library/cc725907.aspx "MPIO 개요 and features")을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54ee9-113">For more information, see [MPIO overview](https://technet.microsoft.com/library/cc725907.aspx "MPIO overview and features").</span></span>

<span data-ttu-id="54ee9-114">StorSimple 솔루션의 가용성을 높이려면 StorSimple 가상 배열(모델 1200)에 연결된 Windows Server 호스트에 MPIO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-114">For the high-availability of your StorSimple solution, configure MPIO on the Windows Server hosts connected to your StorSimple Virtual Array (model 1200).</span></span> <span data-ttu-id="54ee9-115">그러면 호스트 서버가 링크, 네트워크 또는 인터페이스 장애를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-115">The host servers can then tolerate a link, network, or interface failure.</span></span> 

<span data-ttu-id="54ee9-116">MPIO를 구성하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-116">You will need to follow these steps to configure MPIO:</span></span> 

* <span data-ttu-id="54ee9-117">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="54ee9-117">Configuration prerequisites</span></span>
* <span data-ttu-id="54ee9-118">1단계: Windows Server 호스트에 MPIO 설치</span><span class="sxs-lookup"><span data-stu-id="54ee9-118">Step 1: Install MPIO on the Windows Server host</span></span>
* <span data-ttu-id="54ee9-119">2단계: StorSimple 볼륨에 대한 MPIO 구성</span><span class="sxs-lookup"><span data-stu-id="54ee9-119">Step 2: Configure MPIO for StorSimple volumes</span></span>
* <span data-ttu-id="54ee9-120">3단계: 호스트에 StorSimple 볼륨 탑재</span><span class="sxs-lookup"><span data-stu-id="54ee9-120">Step 3: Mount StorSimple volumes on the host</span></span>

<span data-ttu-id="54ee9-121">위의 각 단계는 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-121">Each of the above steps is discussed in the following sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54ee9-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54ee9-122">Prerequisites</span></span>
<span data-ttu-id="54ee9-123">이 섹션에서는 Windows Server 호스트 및 가상 배열의 필수 구성 요소를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-123">This section details the configuration prerequisites for the Windows Server host and your virtual array.</span></span>

### <a name="on-windows-server-host"></a><span data-ttu-id="54ee9-124">Windows Server 호스트</span><span class="sxs-lookup"><span data-stu-id="54ee9-124">On Windows Server host</span></span>
* <span data-ttu-id="54ee9-125">Windows Server 호스트에 사용 가능한 2개의 네트워크 인터페이스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-125">Make sure that your Windows Server host has 2 network interfaces enabled.</span></span>

### <a name="on-storsimple-virtual-array"></a><span data-ttu-id="54ee9-126">StorSimple 가상 배열에서</span><span class="sxs-lookup"><span data-stu-id="54ee9-126">On StorSimple Virtual Array</span></span>
* <span data-ttu-id="54ee9-127">가상 배열이 iSCSI 서버로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-127">The virtual array should be configured as an iSCSI server.</span></span> <span data-ttu-id="54ee9-128">자세한 내용은 [가상 배열을 iSCSI 서버로 설정](storsimple-virtual-array-deploy3-iscsi-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54ee9-128">To learn more, see [set up virtual array as an iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md).</span></span> <span data-ttu-id="54ee9-129">배열에서 하나 이상의 네트워크 인터페이스가 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-129">One or more network interfaces should be enabled on the array.</span></span>   
* <span data-ttu-id="54ee9-130">Windows Server 호스트에서 가상 배열의 네트워크 인터페이스에 도달할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-130">The network interfaces on your virtual array should be reachable from the Windows Server host.</span></span>
* <span data-ttu-id="54ee9-131">StorSimple 가상 배열에 하나 이상의 볼륨을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-131">One or more volumes should be created on your StorSimple Virtual Array.</span></span> <span data-ttu-id="54ee9-132">자세한 내용은 StorSimple 가상 배열에 [볼륨 추가](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54ee9-132">To learn more, see [Add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) on your StorSimple Virtual Array.</span></span> <span data-ttu-id="54ee9-133">이 절차에서는 가상 배열에 볼륨 3개(아래 그림처럼 1개는 로컬에 고정, 2개는 계층화된 볼륨)를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-133">In this procedure, we created 3 volumes (1 locally pinned and 2 tiered volumes as shown below) on the virtual array.</span></span>
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a><span data-ttu-id="54ee9-135">StorSimple 가상 배열에 대한 하드웨어 구성</span><span class="sxs-lookup"><span data-stu-id="54ee9-135">Hardware configuration for StorSimple Virtual Array</span></span>
<span data-ttu-id="54ee9-136">아래 그림은 이 절차에 사용되는 Windows Server 호스트 및 StorSimple 가상 배열의 고가용성과 다중 경로 부하 분산을 위한 하드웨어 구성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-136">The figure below shows the hardware configuration for high availability and load-balancing multipathing for your Windows Server host and StorSimple Virtual Array used in this procedure.</span></span>

![mpio 하드웨어 구성](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

<span data-ttu-id="54ee9-138">이전 그림에서 표시된 것처럼</span><span class="sxs-lookup"><span data-stu-id="54ee9-138">As shown in the preceding figure:</span></span>

* <span data-ttu-id="54ee9-139">Hyper-V에 프로비전된 StorSimple 가상 배열은 iSCSI 서버로 구성된 단일 노드 활성 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-139">Your StorSimple Virtual Array provisioned on Hyper-V is a single node active device configured as an iSCSI server.</span></span>
* <span data-ttu-id="54ee9-140">배열에 두 개의 가상 네트워크 인터페이스가 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-140">Two virtual network interfaces are enabled on your array.</span></span> <span data-ttu-id="54ee9-141">가상 배열의 로컬 웹 UI에서 아래와 같이 **네트워크 설정**으로 이동하여 두 네트워크 인터페이스가 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-141">In the local web UI of your virtual array, verify that two network interfaces are enabled by navigating to **Network Settings** as shown below:</span></span>
  
    ![1200에 활성화된 네트워크 인터페이스](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    <span data-ttu-id="54ee9-143">활성화된 네트워크 인터페이스의 IPv4 주소(기본적으로 이더넷, 이더넷 2)를 확인하고 나중에 호스트에서 사용할 수 있도록 저장해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-143">Note the IPv4 addresses of the enabled network interfaces (Ethernet, Ethernet 2 by default) and save for later use on the host.</span></span>
* <span data-ttu-id="54ee9-144">Windows Server 호스트에 두 개의 네트워크 인터페이스가 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-144">Two network interfaces are enabled on your Windows Server host.</span></span> <span data-ttu-id="54ee9-145">호스트 및 배열에 대해 연결된 인터페이스가 동일한 서브넷에 있으면 4개 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-145">If the connected interfaces for host and array are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="54ee9-146">이 절차의 사례가 바로 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-146">This was the case in this procedure.</span></span> <span data-ttu-id="54ee9-147">그러나 배열의 각 네트워크 인터페이스와 호스트 인터페이스가 서로 다른 IP 서브넷에 있으면(따라서 라우팅할 수 없음) 2개 경로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-147">However, if each network interface on the array and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span>

## <a name="step-1-install-mpio-on-the-windows-server-host"></a><span data-ttu-id="54ee9-148">1단계: Windows Server 호스트에 MPIO 설치</span><span class="sxs-lookup"><span data-stu-id="54ee9-148">Step 1: Install MPIO on the Windows Server host</span></span>
<span data-ttu-id="54ee9-149">MPIO는 Windows Server에서 선택적 기능이며 기본적으로 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-149">MPIO is an optional feature on Windows Server and is not installed by default.</span></span> <span data-ttu-id="54ee9-150">서버 관리자를 통해 기능으로 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-150">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="54ee9-151">Windows Server 호스트에 이 기능을 설치하려면 다음 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-151">To install this feature on your Windows Server host, complete the following procedure.</span></span>

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a><span data-ttu-id="54ee9-152">2단계: StorSimple 볼륨에 대한 MPIO 구성</span><span class="sxs-lookup"><span data-stu-id="54ee9-152">Step 2: Configure MPIO for StorSimple volumes</span></span>
<span data-ttu-id="54ee9-153">MPIO는 StorSimple 볼륨을 식별하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-153">MPIO needs to be configured to identify StorSimple volumes.</span></span> <span data-ttu-id="54ee9-154">StorSimple 볼륨을 인식하도록 MPIO를 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-154">To configure MPIO to recognize StorSimple volumes, perform the following steps.</span></span>

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-the-host"></a><span data-ttu-id="54ee9-155">3단계: 호스트에 StorSimple 볼륨 탑재</span><span class="sxs-lookup"><span data-stu-id="54ee9-155">Step 3: Mount StorSimple volumes on the host</span></span>
<span data-ttu-id="54ee9-156">MPIO가 Windows Server에 구성된 후 StorSimple 배열에 생성된 볼륨이 탑재될 수 있으며 중복에 대해 MPIO를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-156">After MPIO is configured on Windows Server, volume(s) created on the StorSimple array can be mounted and can then take advantage of MPIO for redundancy.</span></span> <span data-ttu-id="54ee9-157">볼륨을 탑재하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-157">To mount a volume, perform the following steps.</span></span>

#### <a name="to-mount-volumes-on-the-host"></a><span data-ttu-id="54ee9-158">호스트에 볼륨을 탑재 하려면</span><span class="sxs-lookup"><span data-stu-id="54ee9-158">To mount volumes on the host</span></span>
1. <span data-ttu-id="54ee9-159">Windows Server 호스트에서 **iSCSI 초기자 속성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-159">Open the **iSCSI Initiator Properties** window on the Windows Server host.</span></span> <span data-ttu-id="54ee9-160">**서버 관리자 > 대시보드 > 도구 > iSCSI 초기자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-160">Go to **Server Manager > Dashboard > Tools > iSCSI Initiator**.</span></span>
2. <span data-ttu-id="54ee9-161">**iSCSI 초기자 속성** 대화 상자에서 **검색**을 클릭한 다음 **대상 포털 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-161">In the **iSCSI Initiator Properties** dialog box, click **Discovery**, and then click **Discover Target Portal**.</span></span>
3. <span data-ttu-id="54ee9-162">**대상 포털 검색** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-162">In the **Discover Target Portal** dialog box, do the following:</span></span>
   
    1. <span data-ttu-id="54ee9-163">StorSimple 가상 배열에서 첫 번째로 활성화된 네트워크 인터페이스의 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-163">Enter the IP address of the first enabled network interface on your StorSimple Virtual Array.</span></span> <span data-ttu-id="54ee9-164">기본적으로 **이더넷**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-164">By default, this would be **Ethernet**.</span></span> 
    2. <span data-ttu-id="54ee9-165">**확인** 을 클릭하여 **iSCSI 초기자 속성** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-165">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="54ee9-166">iSCSI 연결에 개인 네트워크를 사용하는 경우 개인 네트워크에 연결된 데이터 포트의 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-166">If you are using a private network for iSCSI connections, enter the IP address of the DATA port that is connected to the private network.</span></span>
     
4. <span data-ttu-id="54ee9-167">배열의 두 번째 네트워크 인터페이스(예: 이더넷 2)에 대해 2~3단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-167">Repeat steps 2-3 for a second network interface (for example, Ethernet 2) on your array.</span></span> 
5. <span data-ttu-id="54ee9-168">**iSCSI 초기자 속성** 대화 상자에서 **대상** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-168">Select the **Targets** tab in the **iSCSI Initiator Properties** dialog box.</span></span> <span data-ttu-id="54ee9-169">가상 배열의 경우 각 볼륨 서피스가 **검색된 대상**아래에 대상으로 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-169">For your virtual array, you should see each volume surface as a target under **Discovered Targets**.</span></span> <span data-ttu-id="54ee9-170">이 경우 3개 대상(3개의 볼륨에 해당하는)이 검색될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-170">In this case, three targets (corresponding to three volumes) would be discovered.</span></span>
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. <span data-ttu-id="54ee9-172">**연결**을 클릭하여 StorSimple 가상 배열로 iSCSI 세션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-172">Click **Connect** to establish an iSCSI session with your StorSimple Virtual Array.</span></span> <span data-ttu-id="54ee9-173">**대상에 연결** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-173">A **Connect to Target** dialog box will appear.</span></span> <span data-ttu-id="54ee9-174">**다중 경로 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-174">Select the **Enable multi-path** check box.</span></span> <span data-ttu-id="54ee9-175">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-175">Click **Advanced**.</span></span>
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. <span data-ttu-id="54ee9-177">**고급 설정** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-177">In the **Advanced Settings** dialog box, do the following:</span></span>                                        
   
    1. <span data-ttu-id="54ee9-178">**로컬 어댑터** 드롭다운 목록에서 **Microsoft iSCSI 초기자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-178">On the **Local Adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
    2. <span data-ttu-id="54ee9-179">**초기자 IP** 드롭다운 목록에서 호스트의 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-179">On the **Initiator IP** drop-down list, select the IP address of the host.</span></span>
    3. <span data-ttu-id="54ee9-180">**대상 포털** IP 드롭다운 목록에서 배열 인터페이스의 IP를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-180">On the **Target Portal** IP drop-down list, select the IP of array interface.</span></span>
    4. <span data-ttu-id="54ee9-181">**확인** 을 클릭하여 **iSCSI 초기자 속성** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-181">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. <span data-ttu-id="54ee9-183">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-183">Click **Properties**.</span></span> 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. <span data-ttu-id="54ee9-185">**속성** 대화 상자에서 **세션 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-185">In the **Properties** dialog box, click **Add Session**.</span></span>
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. <span data-ttu-id="54ee9-187">**대상에 연결** 대화 상자에서 **다중 경로 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-187">In the **Connect to Target** dialog box, select the **Enable multi-path** check box.</span></span> <span data-ttu-id="54ee9-188">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-188">Click **Advanced**.</span></span>
11. <span data-ttu-id="54ee9-189">**고급 설정** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="54ee9-189">In the **Advanced Settings** dialog box:</span></span>                                        
    
    1. <span data-ttu-id="54ee9-190">**로컬 어댑터** 드롭다운 목록에서 Microsoft iSCSI 초기자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-190">On the **Local adapter** drop-down list, select Microsoft iSCSI Initiator.</span></span>

    2. <span data-ttu-id="54ee9-191">**초기자 IP** 드롭다운 목록에서 호스트에 해당하는 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-191">On the **Initiator IP** drop-down list, select the IP address corresponding to the host.</span></span> <span data-ttu-id="54ee9-192">이 경우에 해당 배열의 두 네트워크 인터페이스를 호스트의 단일 네트워크 인터페이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-192">In this case, you are connecting two network interfaces on the array to a single network interface on the host.</span></span> <span data-ttu-id="54ee9-193">따라서이 인터페이스는 첫 번째 세션에 제공된 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-193">Therefore, this interface is the same as that provided for the first session.</span></span>

    3. <span data-ttu-id="54ee9-194">**대상 포털 IP** 드롭다운 목록에서 해당 배열에서 사용할 수 있는 두 번째 데이터 인터페이스의 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-194">On the **Target Portal IP** drop-down list, select the IP address for the second data interface enabled on the array.</span></span>

    4. <span data-ttu-id="54ee9-195">**확인** 을 클릭하여 iSCSI 초기자 속성 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-195">Click **OK** to return to the iSCSI Initiator Properties dialog box.</span></span> <span data-ttu-id="54ee9-196">두 번째 세션을 대상에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-196">You have added a second session to the target.</span></span>
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. <span data-ttu-id="54ee9-198">원하는 세션(경로)을 추가한 후 **iSCSI 초기자 속성** 대화 상자에서 대상을 선택하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-198">After adding the desired sessions (paths), in the **iSCSI Initiator Properties** dialog box, select the target and click **Properties**.</span></span> <span data-ttu-id="54ee9-199">**속성** 대화 상자의 세션 탭에서 가능한 경로 순열에 해당하는 네 개의 세션 식별자를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-199">On the Sessions tab of the **Properties** dialog box, note the four session identifiers that correspond to the possible path permutations.</span></span> <span data-ttu-id="54ee9-200">세션을 취소하려면 세션 식별자를 옆에 있는 확인란을 선택하고 **연결 끊기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-200">To cancel a session, select the check box next to a session identifier, and then click **Disconnect**.</span></span>

    6. <span data-ttu-id="54ee9-201">세션 내에 표시되는 장치를 보려면 **장치** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-201">To view devices presented within sessions, select the **Devices** tab.</span></span> <span data-ttu-id="54ee9-202">선택한 장치에 대한 MPIO 정책을 구성하려면 **MPIO**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-202">To configure the MPIO policy for a selected device, click **MPIO**.</span></span>

    7. <span data-ttu-id="54ee9-203">**세부 정보** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-203">The **Details** dialog box will appear.</span></span> <span data-ttu-id="54ee9-204">**MPIO** 탭에서 적절한 **부하 분산 정책** 설정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-204">On the **MPIO** tab, you can select the appropriate **Load Balance Policy** settings.</span></span> <span data-ttu-id="54ee9-205">**활성** 또는 **대기** 경로 유형도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-205">You can also view the **Active** or **Standby** path type.</span></span>
12. <span data-ttu-id="54ee9-206">대상에 추가 세션(경로)을 추가하려면 8-11단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-206">Repeat steps 8-11 to add additional sessions (paths) to the target.</span></span> <span data-ttu-id="54ee9-207">호스트의 두 인터페이스 및 가상 배열의 두 인터페이스를 사용하여 각 대상에 대해 총 네 개의 세션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-207">With two interfaces on the host and two on the virtual array, you can add a total of four sessions for each target.</span></span> 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. <span data-ttu-id="54ee9-209">각 볼륨에 대해 이러한 단계를 반복해야 합니다(서피스를 대상으로).</span><span class="sxs-lookup"><span data-stu-id="54ee9-209">You will need to repeat these steps for each volume (surfaces as a target).</span></span>
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. <span data-ttu-id="54ee9-211">**서버 관리자 > 대시보드 > 컴퓨터 관리**로 이동하여 **컴퓨터 관리**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-211">Open **Computer Management** by navigating to **Server Manager > Dashboard > Computer Management**.</span></span> <span data-ttu-id="54ee9-212">왼쪽 창에서 **저장소 > 디스크 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-212">In the left pane, click **Storage > Disk Management**.</span></span> <span data-ttu-id="54ee9-213">이 호스트에 표시되는 StorSimple 가상 배열에 만들어진 볼륨이 **디스크 관리**에서 새 디스크로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-213">The volume(s) created on the StorSimple Virtual Array that are visible to this host will appear under **Disk Management** as new disk(s).</span></span>
15. <span data-ttu-id="54ee9-214">디스크를 초기화하고 새 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-214">Initialize the disk and create a new volume.</span></span> <span data-ttu-id="54ee9-215">포맷 프로세스에서 할당 단위 크기(AUS)를 64KB로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-215">During the format process, select an allocation unit size (AUS) of 64 KB.</span></span> <span data-ttu-id="54ee9-216">사용 가능한 모든 볼륨에 대해 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-216">Repeat the process for all the available volumes.</span></span>
    
    ![디스크 관리](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. <span data-ttu-id="54ee9-218">**디스크 관리**에서 **디스크**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-218">Under **Disk Management**, right-click the **Disk** and select **Properties**.</span></span>
17. <span data-ttu-id="54ee9-219">**다중 경로 디스크 장치 속성** 대화 상자에서 **MPIO** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-219">In the **Multi-Path Disk Device Properties** dialog box, click the **MPIO** tab.</span></span>
    
    ![디스크 속성](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. <span data-ttu-id="54ee9-221">**DSM 이름** 섹션에서 **세부 정보**를 클릭하고 해당 매개 변수가 기본 매개 변수로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-221">In the **DSM Name** section, click **Details** and verify that the parameters are set to the default parameters.</span></span> <span data-ttu-id="54ee9-222">기본 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-222">The default parameters are:</span></span>
    
    * <span data-ttu-id="54ee9-223">경로 확인 기간 = 30</span><span class="sxs-lookup"><span data-stu-id="54ee9-223">Path Verify Period = 30</span></span>
    * <span data-ttu-id="54ee9-224">재시도 횟수 = 3</span><span class="sxs-lookup"><span data-stu-id="54ee9-224">Retry Count = 3</span></span>
    * <span data-ttu-id="54ee9-225">PDO 제거 기간 = 20</span><span class="sxs-lookup"><span data-stu-id="54ee9-225">PDO Remove Period = 20</span></span>
    * <span data-ttu-id="54ee9-226">재시도 간격 = 1</span><span class="sxs-lookup"><span data-stu-id="54ee9-226">Retry Interval = 1</span></span>
    * <span data-ttu-id="54ee9-227">경로 확인 사용 = 선택하지 않음</span><span class="sxs-lookup"><span data-stu-id="54ee9-227">Path Verify Enabled = Unchecked.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="54ee9-228">**기본 매개 변수를 수정하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="54ee9-228">**Do not modify the default parameters.**</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="54ee9-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54ee9-229">Next steps</span></span>
<span data-ttu-id="54ee9-230">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열을 관리](storsimple-virtual-array-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="54ee9-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span>

