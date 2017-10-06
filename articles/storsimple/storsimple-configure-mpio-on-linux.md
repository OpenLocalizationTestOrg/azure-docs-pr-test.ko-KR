---
title: "StorSimple Linux 호스트에 MPIO aaaConfigure | Microsoft Docs"
description: "CentOS 6.6를 실행 하는 연결 된 StorSimple tooa Linux 호스트에 MPIO 구성"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="22bac-103">CentOS를 실행하는 StorSimple 호스트에서 MPIO 구성</span><span class="sxs-lookup"><span data-stu-id="22bac-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="22bac-104">이 문서에서는 Centos 6.6 호스트 서버의 hello 단계 필요한 tooconfigure 다중 경로 IO (MPIO)를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="22bac-105">hello 호스트 서버는 iSCSI 초기자를 통해 고가용성을 위해 연결 된 tooyour Microsoft Azure StorSimple 장치.</span><span class="sxs-lookup"><span data-stu-id="22bac-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="22bac-106">다중 경로 장치 및 hello StorSimple 볼륨에 대 한 특정 설정의 세부 hello 자동 검색에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="22bac-107">이 절차는 StorSimple 8000 시리즈 장치와의 적용 가능한 tooall hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="22bac-108">StorSimple 가상 장치에 이 절차를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="22bac-109">자세한 내용은 tooconfigure 가상 장치에 대 한 서버를 호스트 하는 방법을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="22bac-110">다중 경로에 대해</span><span class="sxs-lookup"><span data-stu-id="22bac-110">About multipathing</span></span>
<span data-ttu-id="22bac-111">hello 다중 경로 제어 기능 tooconfigure을 사용 하면 호스트 서버와 저장소 장치 간에 여러 I/O 경로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="22bac-112">이러한 I/O 경로는 별도 케이블, 스위치, 네트워크 인터페이스 및 컨트롤러를 포함할 수 있는 물리적 SAN 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="22bac-113">다중 경로 제어 hello I/O 경로 tooconfigure 모든 hello 집계 경로와 연결 된 새 장치를 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="22bac-114">다중 경로 제어의 hello 용도는 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="22bac-115">**고가용성**: hello I/O 경로 (예: 케이블, 스위치, 네트워크 인터페이스 또는 컨트롤러)의 요소가 실패할 경우에 대체 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="22bac-116">**부하 분산**: 저장소 장치의 hello 구성에 따라 hello I/O 경로 대 한 부하를 감지 하 고 동적으로 부하를 리 밸런스 hello 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="22bac-117">다중 경로 구성 요소에 대해</span><span class="sxs-lookup"><span data-stu-id="22bac-117">About multipathing components</span></span>
<span data-ttu-id="22bac-118">Linux에서 다중 경로는 아래에 정리된 커널 구성 요소 및 사용자 공간 구성 요소로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="22bac-119">**커널**: hello 주 구성 요소는 hello *장치 매퍼* I/O를 조정 하 고 경로 및 경로 그룹에 대 한 장애 조치를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="22bac-120">**사용자 공간**: 이들은 *다중 경로 도구* 어떤 toodo hello 장치 매퍼 다중 경로 모듈 지시 하 여 경로가 장치를 관리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="22bac-121">hello 도구는 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="22bac-122">**다중 경로**: 다중 경로인 장치를 나열하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="22bac-123">**Multipathd**: hello 경로 다중 경로 및 모니터를 실행 하는 디먼 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="22bac-124">**Devmap 이름**: devmaps에 대 한 의미 있는 장치 이름을 tooudev를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="22bac-125">**Kpartx**: 선형 devmaps toodevice 파티션을 toomake 다중 경로 맵 이러한 시스템이 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="22bac-126">**Multipath.conf**: 다중 경로 데몬을 사용 하는 toooverwrite hello 기본 제공 구성 테이블에 대 한 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="22bac-127">Hello multipath.conf 구성 파일에 대 한</span><span class="sxs-lookup"><span data-stu-id="22bac-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="22bac-128">hello 구성 파일 `/etc/multipath.conf` 사용 하면 다양 한 hello 다중 경로 제어 기능 사용자가 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="22bac-129">hello `multipath` 명령과 hello 커널 데몬 `multipathd` 이 파일에 있는 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="22bac-130">hello 파일을 hello 다중 경로 장치 hello 구성 중에 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="22bac-131">Hello를 실행 하기 전에 모든 변경 내용을 한 않았는지 확인 `multipath` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="22bac-132">Hello 파일을 수정 하는 경우 이후에 toostop 필요를 multipathd hello 변경 tootake 효과 대 한 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="22bac-133">hello multipath.conf에 5 개 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="22bac-134">**시스템 수준 기본값** *(기본값)*: 시스템 수준 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="22bac-135">**장치 차단 목록에 포함할** *(블랙 리스트)*: hello 목록은 장치-맵 편집기에 의해 제어 되지 해야 하는 장치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="22bac-136">**예외 블랙 리스트에 추가** *(blacklist_exceptions)*: hello 블랙 리스트에 나열 된 경우에 다중 경로 장치도 처리 하는 특정 장치 toobe를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="22bac-137">**저장소 컨트롤러에 대 한 특정 설정** *(장치)*: 공급 업체 및 제품 정보를 가진 적용된 toodevices 수 있는 구성 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="22bac-138">**특정 장치 설정을** *(multipaths)*: 개별 Lun에 대 한이 섹션 toofine 조정 hello 구성 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="22bac-139">StorSimple tooLinux 연결 된 호스트에서 다중 경로 제어 구성</span><span class="sxs-lookup"><span data-stu-id="22bac-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="22bac-140">StorSimple 장치 연결 tooa Linux 호스트는 고가용성을 위해 구성할 수 있습니다 및 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="22bac-141">예를 들어 hello Linux 호스트의 두 인터페이스가 연결 된 toohello hello 및 SAN 장치에 두 개의 인터페이스 toohello SAN 연결 동일한 서브넷에 hello 등 이러한 인터페이스에 있는 다음 사용할 수 있는 네 개의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="22bac-142">그러나 hello 장치 및 호스트 인터페이스에서 각 데이터 인터페이스에 있고 다른 IP 서브넷 (라우팅할 수 없음), 2 경로 사용할 수 됩니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="22bac-143">다중 경로 제어 tooautomatically를 구성할 수 있습니다 hello 사용 가능한 모든 경로 검색, 해당 경로 대 한 부하 분산 알고리즘을 선택, StorSimple 전용 볼륨에 대 한 특정 구성 설정을 적용 하 고 다음을 사용 하도록 설정 및 다중 경로 제어를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="22bac-144">hello 다음 절차에서는 설명 방법을 때 두 개의 네트워크 인터페이스를 사용 하 여 StorSimple 장치 tooconfigure 다중 경로 제어는 두 개의 네트워크 인터페이스와 연결 된 tooa 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22bac-145">필수 조건</span><span class="sxs-lookup"><span data-stu-id="22bac-145">Prerequisites</span></span>
<span data-ttu-id="22bac-146">이 섹션 CentOS 서버 및 StorSimple 장치에 대 한 hello 구성 필수 구성 요소에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="22bac-147">CentOS 호스트에서</span><span class="sxs-lookup"><span data-stu-id="22bac-147">On CentOS host</span></span>
1. <span data-ttu-id="22bac-148">CentOS 호스트에 사용 가능한 2개의 네트워크 인터페이스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="22bac-149">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="22bac-150">hello 다음 경우를 보여 줍니다 hello 출력 2 개의 네트워크 인터페이스 (`eth0` 및 `eth1`) hello 호스트에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="22bac-151">CentOS 서버에 *iSCSI-initiator-utils* 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="22bac-152">다음 단계 tooinstall hello 수행 *iSCSI-초기자-유틸리티*합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="22bac-153">CentOS 호스트에 `root` 로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="22bac-154">Hello 설치 *iSCSI-초기자-유틸리티*합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="22bac-155">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="22bac-156">Hello 후 *iSCSI-초기자-유틸리티* 가 성공적으로 설치 hello iSCSI 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="22bac-157">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="22bac-158">경우에 `iscsid` 실제로 시작 하 고 hello 수 `--force` 옵션 필요할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="22bac-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="22bac-159">iSCSI 초기자를 사용 하 여 hello 부팅 시 사용할 수 있음을 tooensure `chkconfig` tooenable hello 서비스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="22bac-160">tooverify 하는 제대로 설치 프로그램에서는 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="22bac-161">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="22bac-162">위 예제는 hello, 2, 3, 4 및 5의 실행된 수준에서 iSCSI 환경 부팅 시간에 실행 됩니다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="22bac-163">*device-mapper-multipath*를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="22bac-164">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="22bac-165">hello 설치가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-165">hello installation will start.</span></span> <span data-ttu-id="22bac-166">형식 **Y** toocontinue 확인 메시지가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="22bac-167">StorSimple 장치에서</span><span class="sxs-lookup"><span data-stu-id="22bac-167">On StorSimple device</span></span>
<span data-ttu-id="22bac-168">StorSimple 장치에는 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="22bac-169">iSCSI에 사용 가능한 두 개의 최소 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="22bac-170">두 인터페이스는 StorSimple 장치에서 iSCSI 사용 tooverify hello StorSimple 장치에 대 한 Azure 클래식 포털의에서 단계를 실행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="22bac-171">StorSimple 장치에 대 한 hello 클래식 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="22bac-172">StorSimple Manager 서비스를 선택를 클릭 **장치** hello 특정 StorSimple 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="22bac-173">클릭 **구성** hello 네트워크 인터페이스 설정을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="22bac-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="22bac-174">두 가지 iSCSI를 사용하는 네트워크 인터페이스가 있는 스크린샷은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="22bac-175">여기서 데이터 2와 데이터 3은 모두 iSCSI에 10GbE 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![MPIO StorsSimple 데이터 2 구성](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple 데이터 3 구성](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="22bac-178">Hello에 **구성** 페이지</span><span class="sxs-lookup"><span data-stu-id="22bac-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="22bac-179">네트워크 인터페이스가 둘 모두  iSCSI를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="22bac-180">hello **iSCSI 사용** 너무 필드를 설정 해야**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="22bac-181">Hello 네트워크 인터페이스가 hello 갖도록 동일한 속도 1gbe 또는 10gbe 둘 다에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="22bac-182">Hello iSCSI 사용 인터페이스의 hello IPv4 주소를 확인 하 고 나중에 사용할 hello 호스트에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="22bac-183">StorSimple 장치에 iSCSI 인터페이스 hello hello CentOS 서버에서 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="22bac-184">tooverify이 호스트 서버에서 StorSimple iSCSI 사용 네트워크 인터페이스의 tooprovide hello IP 주소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="22bac-185">사용 되는 명령을 hello 및 DATA2 사용 하 여 해당 출력 hello (10.126.162.25) 및 data 3 (10.126.162.26)는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="22bac-186">하드웨어 구성</span><span class="sxs-lookup"><span data-stu-id="22bac-186">Hardware configuration</span></span>
<span data-ttu-id="22bac-187">중복성을 위해 별도 경로에 hello 두 iSCSI 네트워크 인터페이스에 연결 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="22bac-188">아래 hello 그림에는 CentOS 서버와 StorSimple 장치에 대 한 다중 경로 제어 부하 분산 및 고가용성에 대 한 hello 권장된 하드웨어 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![StorSimple tooLinux 호스트에 대 한 MPIO 하드웨어 구성](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="22bac-190">와 같이 앞 그림 hello:</span><span class="sxs-lookup"><span data-stu-id="22bac-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="22bac-191">StorSimple 장치가 두 개의 컨트롤러를 사용하여 활성-수동 구성 중입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="22bac-192">두 개의 SAN 스위치는 연결 된 tooyour 장치 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="22bac-193">두 개의 iSCSI 초기자를 StorSimple 장치에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="22bac-194">두 개의 네트워크 인터페이스를 CentOS 호스트에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="22bac-195">hello 호스트와 데이터 인터페이스는 라우팅할 수 있는 경우 구성 이상 hello 장치와 hello 호스트 사이의 4의 개별 경로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="22bac-196">다중 경로에 1GbE 및 10GbE 네트워크 인터페이스를 혼용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="22bac-197">두 개의 네트워크 인터페이스를 사용할 때 두 hello 인터페이스 hello 동일한 유형 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="22bac-198">StorSimple 장치에서 DATA0, DATA1, DATA4 및 DATA5는 1GbE 인터페이스인 반면 DATA2 및 DATA3은 10GbE 네트워크 인터페이스입니다. |</span><span class="sxs-lookup"><span data-stu-id="22bac-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="22bac-199">구성 단계</span><span class="sxs-lookup"><span data-stu-id="22bac-199">Configuration steps</span></span>
<span data-ttu-id="22bac-200">다중 경로 제어에 대 한 구성 단계 hello hello hello 부하 분산 알고리즘 toouse, 다중 경로 제어를 사용 하도록 설정 하 고 마지막으로 hello 구성을 확인 하는 지정 하는 자동 검색에 사용할 수 있는 경로 구성 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="22bac-201">이러한 각 단계는 hello 다음 섹션에서에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="22bac-202">1단계: 자동 검색에 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="22bac-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="22bac-203">hello 다중 경로 지 원하는 장치를 자동으로 검색 및 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="22bac-204">`/etc/multipath.conf` 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="22bac-205">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="22bac-206">명령 위에 hello 만들어집니다는 `sample/etc/multipath.conf` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="22bac-207">다중 경로 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-207">Start multipath service.</span></span> <span data-ttu-id="22bac-208">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="22bac-209">다음 출력 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="22bac-210">다중 경로의 자동 검색을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="22bac-211">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="22bac-212">hello 기본값 섹션을 수정 합니다이 프로그램 `multipath.conf` 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="22bac-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="22bac-213">2단계: StorSimple 볼륨에 대한 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="22bac-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="22bac-214">기본적으로 모든 장치는 검은색 hello multipath.conf 파일에 나열 하 고 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="22bac-215">StorSimple 장치에서 볼륨에 대 한 toocreate 블랙 리스트 예외 tooallow 다중 경로 제어를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="22bac-216">Hello 편집 `/etc/mulitpath.conf` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="22bac-217">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="22bac-218">Hello multipath.conf 파일에 hello blacklist_exceptions 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="22bac-219">StorSimple 장치에는이 섹션의 블랙 리스트 예외로 표시 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="22bac-220">관련 된 줄이 파일 toomodify 것 (사용 하 여만 hello 특정 모델의 사용 중인 hello 장치) 아래와 같이 주석 처리 제거:</span><span class="sxs-lookup"><span data-stu-id="22bac-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="22bac-221">3단계: 라운드 로빈 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="22bac-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="22bac-222">이 부하 분산 알고리즘 균형 잡힌 고 라운드 로빈 방식으로 모든 hello 사용 가능한 multipaths toohello 활성 컨트롤러를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="22bac-223">Hello 편집 `/etc/multipath.conf` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="22bac-224">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="22bac-225">Hello에서 `defaults` 섹션, 집합 hello `path_grouping_policy` 너무`multibus`합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="22bac-226">hello `path_grouping_policy` hello 기본 경로 그룹화 정책 tooapply toounspecified multipaths를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="22bac-227">hello 기본값 섹션 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="22bac-228">가장 일반적인 값 hello `path_grouping_policy` 포함:</span><span class="sxs-lookup"><span data-stu-id="22bac-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="22bac-229">장애 조치 = 우선 순위 그룹 당 1개의 경로</span><span class="sxs-lookup"><span data-stu-id="22bac-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="22bac-230">multibus = 1개의 우선 순위 그룹에서 모든 유효한 경로</span><span class="sxs-lookup"><span data-stu-id="22bac-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="22bac-231">4단계: 다중 경로 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="22bac-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="22bac-232">Hello를 다시 시작 `multipathd` 데몬 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="22bac-233">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="22bac-234">아래와 같이 hello 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="22bac-235">5단계: 다중 경로 확인</span><span class="sxs-lookup"><span data-stu-id="22bac-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="22bac-236">먼저 iSCSI 연결이 hello StorSimple 장치도 다음과 같이 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="22bac-237">a.</span><span class="sxs-lookup"><span data-stu-id="22bac-237">a.</span></span> <span data-ttu-id="22bac-238">StorSimple 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-238">Discover your StorSimple device.</span></span> <span data-ttu-id="22bac-239">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="22bac-240">hello 출력 DATA0 IP 주소는 10.126.162.25 및 아웃 바운드 iSCSI 트래픽에 대 한 hello StorSimple 장치에 포트 3260 열릴 때 아래 표시 된 것과 같이입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="22bac-241">StorSimple 장치의 IQN 복사 hello `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, hello 출력 앞에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="22bac-242">b.</span><span class="sxs-lookup"><span data-stu-id="22bac-242">b.</span></span> <span data-ttu-id="22bac-243">Toohello 장치 대상 IQN을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="22bac-244">hello StorSimple 장치가 여기 hello iSCSI 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="22bac-245">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="22bac-246">hello 다음 예제에서는 대상 IQN 사용 하 여 출력의 `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="22bac-247">hello 출력 장치에 toohello 두 iSCSI 사용 네트워크 인터페이스를 성공적으로 연결 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="22bac-248">호스트가 하나 밖에 인터페이스와 여기에 두 개의 경로 표시 해야 합니다 tooenable 두 hello 인터페이스 호스트에서 iSCSI에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="22bac-249">Hello를 따르면 [Linux 설명서의에서 지침을 자세히](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="22bac-250">볼륨은 hello StorSimple 장치에서 노출 된 toohello CentOS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="22bac-251">자세한 내용은 참조 [6 단계: 볼륨 만들기](storsimple-deployment-walkthrough.md#step-6-create-a-volume) hello StorSimple 장치에서 Azure 클래식 포털을 통해.</span><span class="sxs-lookup"><span data-stu-id="22bac-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="22bac-252">Hello 사용 가능한 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-252">Verify hello available paths.</span></span> <span data-ttu-id="22bac-253">형식:</span><span class="sxs-lookup"><span data-stu-id="22bac-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="22bac-254">다음 예제는 hello 두 개의 사용 가능한 경로 있는 StorSimple 장치 연결 된 tooa 단일 호스트 네트워크 인터페이스에서 두 개의 네트워크 인터페이스에 대 한 hello 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="22bac-255">다중 경로 문제 해결</span><span class="sxs-lookup"><span data-stu-id="22bac-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="22bac-256">이 섹션에서는 다중 경로를 구성하는 동안 문제가 발생하는 경우 유용한 팁을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="22bac-257">Q.</span><span class="sxs-lookup"><span data-stu-id="22bac-257">Q.</span></span> <span data-ttu-id="22bac-258">hello 변경 내용을 볼 수 없는 `multipath.conf` 파일 내용이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="22bac-259">A.</span><span class="sxs-lookup"><span data-stu-id="22bac-259">A.</span></span> <span data-ttu-id="22bac-260">제공한 경우 모든 변경 내용을 toohello `multipath.conf` 파일인 toorestart hello 다중 경로 제어 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="22bac-261">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="22bac-262">Q.</span><span class="sxs-lookup"><span data-stu-id="22bac-262">Q.</span></span> <span data-ttu-id="22bac-263">Hello StorSimple 장치에 두 개의 네트워크 인터페이스 및 두 개의 네트워크 인터페이스 hello 호스트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="22bac-264">Hello 사용 가능한 경로 나열 하는 경우 두 개의 경로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="22bac-265">4 개의 사용 가능한 경로 toosee 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="22bac-266">A.</span><span class="sxs-lookup"><span data-stu-id="22bac-266">A.</span></span> <span data-ttu-id="22bac-267">Hello 두 경로 hello에 있는지 확인 동일한 서브넷 및 라우팅 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="22bac-268">Hello 네트워크 인터페이스에 있고 서로 다른 Vlan 라우팅할 수 없음, 두 경로만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="22bac-269">한 가지 방법은 tooverify toomake hello StorSimple 장치에서 네트워크 인터페이스에서 두 hello 호스트 인터페이스를 연결할 수 있는지입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="22bac-270">너무 해야[Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 으로이 확인이 지원 세션을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="22bac-271">Q.</span><span class="sxs-lookup"><span data-stu-id="22bac-271">Q.</span></span> <span data-ttu-id="22bac-272">사용 가능한 경로를 나열하는 경우 어떤 출력도 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="22bac-273">A.</span><span class="sxs-lookup"><span data-stu-id="22bac-273">A.</span></span> <span data-ttu-id="22bac-274">일반적으로 hello 다중 경로 제어 데몬과 문제가 소개 모든 경로가 경로 표시 되지 하 고는 모든 문제가 여기의 hello에서 찾을 가능성이 높으며 `multipath.conf` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="22bac-275">볼 수 있는 실제로 일부 디스크 toohello 대상에 연결한 후 hello 다중 경로 목록에서 응답이 의미할 수도 디스크 없는으로 확인해 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="22bac-276">다음 명령 toorescan hello SCSI 버스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="22bac-277">`$ rescan-scsi-bus.sh `(sg3_utils 패키지의 일부)</span><span class="sxs-lookup"><span data-stu-id="22bac-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="22bac-278">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="22bac-279">또는</span><span class="sxs-lookup"><span data-stu-id="22bac-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="22bac-280">최근에 추가된 디스크의 세부 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="22bac-281">StorSimple 디스크 인지 toodetermine는 hello 명령 다음에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="22bac-282">StorSimple 디스크인지를 확인하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="22bac-283">또한 가능성이 적지만 가능한 원인은 iscsid pid일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="22bac-284">Hello iSCSI 세션에서 명령을 toolog 오프 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="22bac-285">StorSimple 장치 hello iSCSI 대상에 대해 모든 hello 연결 된 네트워크 인터페이스에 대해이 명령을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="22bac-286">로그인 하면 모든 hello iSCSI 세션에서 hello iSCSI 대상 IQN tooreestablish hello iSCSI 세션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="22bac-287">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="22bac-288">Q.</span><span class="sxs-lookup"><span data-stu-id="22bac-288">Q.</span></span> <span data-ttu-id="22bac-289">장치를 허용 목록에 추가되었는지 잘 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="22bac-290">A.</span><span class="sxs-lookup"><span data-stu-id="22bac-290">A.</span></span> <span data-ttu-id="22bac-291">tooverify 장치 허용 목록, 인지 hello 다음 문제 해결 대화형 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="22bac-292">자세한 내용은 이동 너무[다중 경로 제어에 대 한 대화형 명령 문제 해결을 사용 하 여](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="22bac-293">유용한 명령 목록</span><span class="sxs-lookup"><span data-stu-id="22bac-293">List of useful commands</span></span>
| <span data-ttu-id="22bac-294">확인하라는 메시지가 표시되면 </span><span class="sxs-lookup"><span data-stu-id="22bac-294">Type</span></span> | <span data-ttu-id="22bac-295">명령</span><span class="sxs-lookup"><span data-stu-id="22bac-295">Command</span></span> | <span data-ttu-id="22bac-296">설명</span><span class="sxs-lookup"><span data-stu-id="22bac-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22bac-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="22bac-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="22bac-298">iSCSI 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="22bac-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="22bac-299">iSCSI 서비스 중지</span><span class="sxs-lookup"><span data-stu-id="22bac-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="22bac-300">iSCSI 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="22bac-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="22bac-301">검색에 지정 된 hello 사용 가능한 대상 주소</span><span class="sxs-lookup"><span data-stu-id="22bac-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="22bac-302">Toohello iSCSI 대상에 로그인</span><span class="sxs-lookup"><span data-stu-id="22bac-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="22bac-303">Hello iSCSI 대상에서 로그 아웃</span><span class="sxs-lookup"><span data-stu-id="22bac-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="22bac-304">iSCSI 초기자 이름 인쇄</span><span class="sxs-lookup"><span data-stu-id="22bac-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="22bac-305">Hello iSCSI 세션 및 hello 호스트에서 검색 된 볼륨의 hello 상태 확인</span><span class="sxs-lookup"><span data-stu-id="22bac-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="22bac-306">Hello 호스트와 hello StorSimple 장치 간에 설정 된 모든 hello iSCSI 세션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="22bac-307">**다중 경로 지정**</span><span class="sxs-lookup"><span data-stu-id="22bac-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="22bac-308">다중 경로 디먼 시작</span><span class="sxs-lookup"><span data-stu-id="22bac-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="22bac-309">다중 경로 디먼 중지</span><span class="sxs-lookup"><span data-stu-id="22bac-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="22bac-310">다중 경로 디먼 다시 시작</span><span class="sxs-lookup"><span data-stu-id="22bac-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="22bac-311">또는</span><span class="sxs-lookup"><span data-stu-id="22bac-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="22bac-312">다중 경로 데몬 toostart 부팅 시 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="22bac-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="22bac-313">문제 해결에 대 한 hello 대화형 콘솔 시작</span><span class="sxs-lookup"><span data-stu-id="22bac-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="22bac-314">다중 경로 연결 및 장치 나열</span><span class="sxs-lookup"><span data-stu-id="22bac-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="22bac-315">`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="22bac-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="22bac-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22bac-316">Next steps</span></span>
<span data-ttu-id="22bac-317">Linux 호스트에서 MPIO를 구성 하는 대로 다음 CentoS 6.6 문서 toorefer toohello를 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22bac-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="22bac-318">CentOS에 MPIO 설정</span><span class="sxs-lookup"><span data-stu-id="22bac-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="22bac-319">Linux 교육 가이드</span><span class="sxs-lookup"><span data-stu-id="22bac-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

