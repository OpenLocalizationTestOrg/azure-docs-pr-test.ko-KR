---
title: "StorSimple Linux 호스트에서 MPIO 구성| Microsoft Docs"
description: "CentOS 6.6를 실행하는 Linux 호스트에 연결된 StorSimple에서 MPIO 구성"
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
ms.openlocfilehash: add539351066f9ff94febeebfd5334773b360e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="081bf-103">CentOS를 실행하는 StorSimple 호스트에서 MPIO 구성</span><span class="sxs-lookup"><span data-stu-id="081bf-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="081bf-104">이 문서에서는 Centos 6.6 호스트 서버에서 다중 경로 IO(MPIO)를 구성하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="081bf-105">호스트 서버는 iSCSI 초기자를 통해 고가용성용 Microsoft Azure StorSimple 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="081bf-106">StorSimple 볼륨에 대한 다중 경로 장치 및 특정 설치의 자동 검색을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="081bf-107">이 절차는 StorSimple 8000 시리즈 장치의 모든 모델에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="081bf-108">StorSimple 가상 장치에 이 절차를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="081bf-109">자세한 내용은 가상 장치에 호스트 서버를 구성하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="081bf-109">For more information, see how to configure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="081bf-110">다중 경로에 대해</span><span class="sxs-lookup"><span data-stu-id="081bf-110">About multipathing</span></span>
<span data-ttu-id="081bf-111">다중 경로 기능을 사용하면 호스트 서버와 저장소 장치 간의 여러 I/O 경로를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="081bf-112">이러한 I/O 경로는 별도 케이블, 스위치, 네트워크 인터페이스 및 컨트롤러를 포함할 수 있는 물리적 SAN 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="081bf-113">다중 경로는 I/O 경로를 집계하여 집계된 모든 경로와 연관된 새 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span></span>

<span data-ttu-id="081bf-114">다중 경로의 목적은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-114">The purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="081bf-115">**고가용성**: I/O 경로의 요소(예: 케이블, 스위치, 네트워크 인터페이스 또는 컨트롤러)가 실패하면 대체 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="081bf-116">**부하 분산**: 저장소 장치의 구성에 따라 I/O 경로에서 부하를 감지하고 동적으로 이러한 부하를 다시 분산하여 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="081bf-117">다중 경로 구성 요소에 대해</span><span class="sxs-lookup"><span data-stu-id="081bf-117">About multipathing components</span></span>
<span data-ttu-id="081bf-118">Linux에서 다중 경로는 아래에 정리된 커널 구성 요소 및 사용자 공간 구성 요소로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="081bf-119">**커널**: 주 구성 요소는 I/O의 경로를 조정하고 경로 및 경로 그룹에 대한 장애 조치를 지원하는 *장치 매퍼* 입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="081bf-120">**사용자 공간**: 이는 장치 매퍼 다중 경로 모듈이 수행할 작업을 지시하여 다중 경로인 장치를 관리하는 *다중 경로 도구* 입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span></span> <span data-ttu-id="081bf-121">도구는 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-121">The tools consist of:</span></span>
   
   * <span data-ttu-id="081bf-122">**다중 경로**: 다중 경로인 장치를 나열하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="081bf-123">**Multipathd**: 다중 경로를 실행하고 경로를 모니터링하는 데몬입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span></span>
   * <span data-ttu-id="081bf-124">**Devmap-name**: devmaps에 대한 udev에 의미 있는 장치 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span></span>
   * <span data-ttu-id="081bf-125">**Kpartx**: 선형 devmaps 장치 파티션에 매핑하여 분할 가능한 다중 경로 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span></span>
   * <span data-ttu-id="081bf-126">**Multipath.conf**: 기본 제공 구성 테이블을 덮어쓰는 데 사용되는 다중 경로 데몬에 대한 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span></span>

### <a name="about-the-multipathconf-configuration-file"></a><span data-ttu-id="081bf-127">Multipath.conf 구성 파일에 대해</span><span class="sxs-lookup"><span data-stu-id="081bf-127">About the multipath.conf configuration file</span></span>
<span data-ttu-id="081bf-128">구성 파일 `/etc/multipath.conf` 은 사용자를 구성할 수 있는 다양한 다중 경로 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span></span> <span data-ttu-id="081bf-129">`multipath` 명령 및 커널 데몬 `multipathd`은 이 파일에 있는 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="081bf-130">다중 경로 장치를 구성하는 동안에만 파일을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-130">The file is consulted only during the configuration of the multipath devices.</span></span> <span data-ttu-id="081bf-131">`multipath` 명령을 실행하기 전에 모든 변경 내용이 적용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-131">Make sure that all changes are made before you run the `multipath` command.</span></span> <span data-ttu-id="081bf-132">나중에 파일을 수정하면 적용하려는 변경 내용에 다중 경로를 중지하고 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span></span>

<span data-ttu-id="081bf-133">multipath.conf에는 다섯 가지 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-133">The multipath.conf has five sections:</span></span>

- <span data-ttu-id="081bf-134">**시스템 수준 기본값** *(기본값)*: 시스템 수준 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="081bf-135">**블랙 리스트에 올린 장치** *(블랙 리스트)*: 장치 매퍼에서 제어하지 말아야 하는 장치 목록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="081bf-136">**블랙 리스트 예외** *(blacklist_exceptions)*: 블랙 리스트에 나열되면 특정 장치를 식별하여 다중 경로 장치로 취급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span></span>
- <span data-ttu-id="081bf-137">**저장소 컨트롤러 특정 설정** *(장치)*: 공급 업체 및 제품 정보가 있는 장치에 적용될 구성 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span></span>
- <span data-ttu-id="081bf-138">**장치 특정 설정** *(다중 경로)*: 이 섹션을 사용하여 개별 LUN에 구성 설정을 미세하게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-to-linux-host"></a><span data-ttu-id="081bf-139">Linux 호스트에 연결된 StorSimple에서 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="081bf-139">Configure multipathing on StorSimple connected to Linux host</span></span>
<span data-ttu-id="081bf-140">고가용성 및 부하 분산을 위해 Linux 호스트에 연결된 StorSimple 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="081bf-141">예를 들어 Linux 호스트에 SAN에 연결된 두 개의 인터페이스가 있고 장치에 SAN에 연결된 두 개의 인터페이스가 있으면 이러한 인터페이스는 동일한 서브넷에 있고 사용 가능한 4개의 경로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="081bf-142">그러나 장치의 각 데이터 인터페이스 및 호스트 인터페이스가 다른 IP 서브넷에 있으면(또 라우팅할 수 없음) 2개의 경로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="081bf-143">다중 경로를 구성하여 자동으로 사용 가능한 모든 경로를 검색하고 해당 경로에 대한 부하를 분산하는 알고리즘을 선택하며 StorSimple 전용 볼륨에 특정 구성 설정을 적용한 다음 다중 경로를 설정 및 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="081bf-144">다음 절차는 두 네트워크 인터페이스가 있는 StorSimple 장치가 두 네트워크 인터페이스가 있는 호스트에 연결된 경우 다중 경로를 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="081bf-145">필수 조건</span><span class="sxs-lookup"><span data-stu-id="081bf-145">Prerequisites</span></span>
<span data-ttu-id="081bf-146">이 섹션은 CentOS 서버 및 StorSimple 장치에 대한 필수 구성 요소를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="081bf-147">CentOS 호스트에서</span><span class="sxs-lookup"><span data-stu-id="081bf-147">On CentOS host</span></span>
1. <span data-ttu-id="081bf-148">CentOS 호스트에 사용 가능한 2개의 네트워크 인터페이스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="081bf-149">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="081bf-150">다음 예에서는 두 가지 네트워크 인터페이스(`eth0` 및 `eth1`)가 호스트에 있는 경우 출력을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span></span>
   
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
2. <span data-ttu-id="081bf-151">CentOS 서버에 *iSCSI-initiator-utils* 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="081bf-152">다음 단계를 수행하여 *iSCSI-initiator-utils*를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-152">Perform the following steps to install *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="081bf-153">CentOS 호스트에 `root` 로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="081bf-154">*iSCSI-initiator-utils*를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-154">Install the *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="081bf-155">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="081bf-156">*iSCSI-Initiator-utils* 를 성공적으로 설치한 후에 iSCSI 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span></span> <span data-ttu-id="081bf-157">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="081bf-158">경우에 따라 `iscsid`이 실제로 시작되지 않을 수 있고 `--force` 옵션이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span></span>
   4. <span data-ttu-id="081bf-159">부팅 시간 동안 iSCSI 초기자를 사용하도록 설정하려면 `chkconfig` 명령을 사용하여 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="081bf-160">제대로 설치되었는지 확인려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-160">To verify that that it was properly setup, run the command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="081bf-161">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="081bf-162">위의 예제에서 iSCSI 환경이 실행 수준 2, 3, 4 및 5에서 부팅 시간에 실행된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="081bf-163">*device-mapper-multipath*를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="081bf-164">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="081bf-165">설치가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-165">The installation will start.</span></span> <span data-ttu-id="081bf-166">확인하라는 메시지가 표시되면 **Y** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-166">Type **Y** to continue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="081bf-167">StorSimple 장치에서</span><span class="sxs-lookup"><span data-stu-id="081bf-167">On StorSimple device</span></span>
<span data-ttu-id="081bf-168">StorSimple 장치에는 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="081bf-169">iSCSI에 사용 가능한 두 개의 최소 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="081bf-170">두 인터페이스가 StorSimple 장치에서 iSCSI를 사용할 수 있는지를 확인하려면 StorSimple 장치에 대한 Azure 클래식 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="081bf-171">StorSimple 장치에 대한 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-171">Log into the classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="081bf-172">StorSimple Manager 서비스를 선택하고 **장치** 를 클릭한 다음 특정 StorSimple 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span></span> <span data-ttu-id="081bf-173">**구성** 을 클릭하고 네트워크 인터페이스 설정을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-173">Click **Configure** and verify the network interface settings.</span></span> <span data-ttu-id="081bf-174">두 가지 iSCSI를 사용하는 네트워크 인터페이스가 있는 스크린샷은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="081bf-175">여기서 데이터 2와 데이터 3은 모두 iSCSI에 10GbE 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![MPIO StorsSimple 데이터 2 구성](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple 데이터 3 구성](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="081bf-178">**구성** 페이지에서</span><span class="sxs-lookup"><span data-stu-id="081bf-178">In the **Configure** page</span></span>
     
     1. <span data-ttu-id="081bf-179">네트워크 인터페이스가 둘 모두  iSCSI를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="081bf-180">**iSCSI를 사용 가능한** 필드를 **예**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-180">The **iSCSI enabled** field should be set to **Yes**.</span></span>
     2. <span data-ttu-id="081bf-181">네트워크 인터페이스의 속도가 동일한지 확인합니다. 둘 모두 1GbE 또는 10GbE여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="081bf-182">iSCSI를 사용 가능한 인터페이스의 IPv4 주소를 확인하고 나중에 사용하기 위해 호스트에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span></span>
* <span data-ttu-id="081bf-183">CentOS 서버에서 StorSimple 장치의 iSCSI 인터페이스를 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span></span>
      <span data-ttu-id="081bf-184">이를 확인하려면 호스트 서버에서 StorSimple iSCSI를 사용 가능한 네트워크 인터페이스의 IP 주소를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="081bf-185">DATA2(10.126.162.25) 및 DATA3 (10.126.162.26)로 사용된 명령 및 해당 출력은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="081bf-186">하드웨어 구성</span><span class="sxs-lookup"><span data-stu-id="081bf-186">Hardware configuration</span></span>
<span data-ttu-id="081bf-187">중복성을 위해 별도 경로에 두 개의 iSCSI 네트워크 인터페이스를 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="081bf-188">아래 그림에서는 고가용성을 위한 권장 하드웨어 구성과 CentOS 서버 및 StorSimple 장치를 위한 다중 경로 부하 분산을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Linux 호스트에 StorSimple을 위한 MPIO 하드웨어 구성](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="081bf-190">이전 그림에서 표시된 것처럼</span><span class="sxs-lookup"><span data-stu-id="081bf-190">As shown in the preceding figure:</span></span>

* <span data-ttu-id="081bf-191">StorSimple 장치가 두 개의 컨트롤러를 사용하여 활성-수동 구성 중입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="081bf-192">두 개의 SAN 스위치가 장치 컨트롤러에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-192">Two SAN switches are connected to your device controllers.</span></span>
* <span data-ttu-id="081bf-193">두 개의 iSCSI 초기자를 StorSimple 장치에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="081bf-194">두 개의 네트워크 인터페이스를 CentOS 호스트에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="081bf-195">위의 구성은 호스트와 데이터 인터페이스가 라우팅될 수 있는 경우 장치와 호스트 사이에 4개의 개별 경로를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="081bf-196">다중 경로에 1GbE 및 10GbE 네트워크 인터페이스를 혼용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="081bf-197">두 네트워크 인터페이스를 사용하면 두 인터페이스 모두 동일한 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-197">When using two network interfaces, both the interfaces should be the identical type.</span></span>
> * <span data-ttu-id="081bf-198">StorSimple 장치에서 DATA0, DATA1, DATA4 및 DATA5는 1GbE 인터페이스인 반면 DATA2 및 DATA3은 10GbE 네트워크 인터페이스입니다. |</span><span class="sxs-lookup"><span data-stu-id="081bf-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="081bf-199">구성 단계</span><span class="sxs-lookup"><span data-stu-id="081bf-199">Configuration steps</span></span>
<span data-ttu-id="081bf-200">다중 경로를 위한 구성 단계는 자동 검색에 사용 가능한 경로 구성, 사용할 부하 분산 알고리즘 지정, 다중 경로를 사용하도록 설정 및 마지막으로 구성 확인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span></span> <span data-ttu-id="081bf-201">이러한 각 단계는 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-201">Each of these steps is discussed in detail in the following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="081bf-202">1단계: 자동 검색에 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="081bf-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="081bf-203">다중 경로를 지원하는 장치를 자동으로 검색 및 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-203">The multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="081bf-204">`/etc/multipath.conf` 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="081bf-205">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="081bf-206">위의 명령은 `sample/etc/multipath.conf` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-206">The above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="081bf-207">다중 경로 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-207">Start multipath service.</span></span> <span data-ttu-id="081bf-208">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="081bf-209">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-209">You will see the following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="081bf-210">다중 경로의 자동 검색을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="081bf-211">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="081bf-212">아래와 같이 `multipath.conf` 의 기본값 섹션을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-212">This will modify the defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="081bf-213">2단계: StorSimple 볼륨에 대한 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="081bf-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="081bf-214">기본적으로 모든 장치는 multipath.conf 파일에서 블랙 리스트에 오르고 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="081bf-215">블랙 리스트 예외를 만들어서 StorSimple 장치에서 볼륨에 다중 경로를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="081bf-216">`/etc/mulitpath.conf` 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-216">Edit the `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="081bf-217">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="081bf-218">multipath.conf 파일에서 blacklist_exceptions 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-218">Locate the blacklist_exceptions section in the multipath.conf file.</span></span> <span data-ttu-id="081bf-219">StorSimple 장치는 이 섹션에서 블랙 리스트 예외로 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span></span> <span data-ttu-id="081bf-220">이 파일에서 관련된 줄의 주석 처리를 제거하여 아래 그림과 같이 수정할 수 있습니다.(사용하는 장치의 특정 모델에만 사용)</span><span class="sxs-lookup"><span data-stu-id="081bf-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span></span>
   
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

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="081bf-221">3단계: 라운드 로빈 다중 경로 구성</span><span class="sxs-lookup"><span data-stu-id="081bf-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="081bf-222">이 부하 분산 알고리즘은 분산된 라운드 로빈 방식으로 활성 컨트롤러에 사용 가능한 모든 다중 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="081bf-223">`/etc/multipath.conf` 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-223">Edit the `/etc/multipath.conf` file.</span></span> <span data-ttu-id="081bf-224">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="081bf-225">`defaults` 섹션에서 `path_grouping_policy`를 `multibus`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span></span> <span data-ttu-id="081bf-226">`path_grouping_policy` 는 기본 경로 그룹화 정책을 지정하여 지정되지 않은 다중 경로에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span></span> <span data-ttu-id="081bf-227">기본값 섹션은 아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-227">The defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="081bf-228">`path_grouping_policy`의 가장 일반적인 값은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-228">The most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="081bf-229">장애 조치 = 우선 순위 그룹 당 1개의 경로</span><span class="sxs-lookup"><span data-stu-id="081bf-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="081bf-230">multibus = 1개의 우선 순위 그룹에서 모든 유효한 경로</span><span class="sxs-lookup"><span data-stu-id="081bf-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="081bf-231">4단계: 다중 경로 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="081bf-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="081bf-232">`multipathd` 데몬을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-232">Restart the `multipathd` daemon.</span></span> <span data-ttu-id="081bf-233">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="081bf-234">출력은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-234">The output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="081bf-235">5단계: 다중 경로 확인</span><span class="sxs-lookup"><span data-stu-id="081bf-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="081bf-236">먼저 iSCSI 연결이 StorSimple 장치에 다음과 같이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span></span>
   
   <span data-ttu-id="081bf-237">a.</span><span class="sxs-lookup"><span data-stu-id="081bf-237">a.</span></span> <span data-ttu-id="081bf-238">StorSimple 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-238">Discover your StorSimple device.</span></span> <span data-ttu-id="081bf-239">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on the device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="081bf-240">DATA0의 IP 주소가 10.126.162.25이고 포트 3260이 아웃 바운드 iSCSI 트래픽에 대한 StorSimple 장치에 열린 경우 출력은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="081bf-241">이전 출력에서 StorSimple 장치 `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`의 IQN을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span></span>

   <span data-ttu-id="081bf-242">b.</span><span class="sxs-lookup"><span data-stu-id="081bf-242">b.</span></span> <span data-ttu-id="081bf-243">대상 IQN을 사용하여 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-243">Connect to the device using target IQN.</span></span> <span data-ttu-id="081bf-244">StorSimple 장치는 여기서 iSCSI 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-244">The StorSimple device is the iSCSI target here.</span></span> <span data-ttu-id="081bf-245">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="081bf-246">다음 예제에서는 `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`의 대상 IQN를 사용하여 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="081bf-247">이 출력은 장치에서 두 개의 iSCSI를 사용하는 네트워크 인터페이스에 성공적으로 연결할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="081bf-248">하나의 호스트 인터페이스 및 두 개의 경로가 표시되면 iSCSI용 호스트에 두 개의 인터페이스를 모두 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span></span> <span data-ttu-id="081bf-249">[Linux 설명서의 자세한 지침](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html)을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="081bf-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="081bf-250">볼륨은 StorSimple 장치에서 CentOS 서버에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-250">A volume is exposed to the CentOS server from the StorSimple device.</span></span> <span data-ttu-id="081bf-251">자세한 내용은 StorSimple 장치에서 Azure 클래식 포털을 통한 [6단계: 볼륨 만들기](storsimple-deployment-walkthrough.md#step-6-create-a-volume) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="081bf-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="081bf-252">사용 가능한 경로를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-252">Verify the available paths.</span></span> <span data-ttu-id="081bf-253">형식:</span><span class="sxs-lookup"><span data-stu-id="081bf-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="081bf-254">다음 예제에서는 두 개의 사용 가능한 경로를 사용하여 단일 호스트 네트워크 인터페이스에 연결된 StorSimple 장치에 두 네트워크 인터페이스에 대한 출력을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        The following example shows the output for two network interfaces on a StorSimple device connected to two host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After the paths are configured, refer to the specific instructions on your host operating system (Centos 6.6) to mount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="081bf-255">다중 경로 문제 해결</span><span class="sxs-lookup"><span data-stu-id="081bf-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="081bf-256">이 섹션에서는 다중 경로를 구성하는 동안 문제가 발생하는 경우 유용한 팁을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="081bf-257">Q.</span><span class="sxs-lookup"><span data-stu-id="081bf-257">Q.</span></span> <span data-ttu-id="081bf-258">`multipath.conf` 파일에서 적용된 변경 내용을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-258">I do not see the changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="081bf-259">A.</span><span class="sxs-lookup"><span data-stu-id="081bf-259">A.</span></span> <span data-ttu-id="081bf-260">`multipath.conf` 파일을 변경한 경우 경로 지정 서비스를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span></span> <span data-ttu-id="081bf-261">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-261">Type the following command:</span></span>

    service multipathd restart

<span data-ttu-id="081bf-262">Q.</span><span class="sxs-lookup"><span data-stu-id="081bf-262">Q.</span></span> <span data-ttu-id="081bf-263">StorSimple 장치에 두 개의 네트워크 인터페이스, 호스트에 두 개의 네트워크 인터페이스를 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span></span> <span data-ttu-id="081bf-264">사용 가능한 경로를 나열하는 경우 두 개의 경로만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-264">When I list the available paths, I see only two paths.</span></span> <span data-ttu-id="081bf-265">네 개의 사용 가능한 경로가 확인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-265">I expected to see four available paths.</span></span>

<span data-ttu-id="081bf-266">A.</span><span class="sxs-lookup"><span data-stu-id="081bf-266">A.</span></span> <span data-ttu-id="081bf-267">두 개의 경로를 라우팅할 수 있으며 동일한 서브넷에 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-267">Make sure that the two paths are on the same subnet and routable.</span></span> <span data-ttu-id="081bf-268">네트워크 인터페이스가 다른 vLAN에 있고 라우팅할 수 없으면 두 개의 경로만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="081bf-269">이를 확인하는 방법은 StorSimple 장치의 네트워크 인터페이스에서 호스트 인터페이스 모두를 연결할 수 있는지 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span></span> <span data-ttu-id="081bf-270">이 방법은 지원 세션을 통해 수행할 수 있으므로 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="081bf-271">Q.</span><span class="sxs-lookup"><span data-stu-id="081bf-271">Q.</span></span> <span data-ttu-id="081bf-272">사용 가능한 경로를 나열하는 경우 어떤 출력도 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="081bf-273">A.</span><span class="sxs-lookup"><span data-stu-id="081bf-273">A.</span></span> <span data-ttu-id="081bf-274">일반적으로 다중 경로인 경로가 표시 되지 않으면 다중 경로인 데몬과 문제가 있을 수 있고 `multipath.conf` 파일에 어떤 문제가 있을 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span></span>

<span data-ttu-id="081bf-275">또한 다중 경로 목록으로부터 응답이 없으면 디스크가 없다는 것을 의미할 수 있으므로 대상에 연결한 후에 일부 디스크를 실제로 볼 수 있는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="081bf-276">다음 명령을 사용하여 SCSI 버스를 다시 스캔합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-276">Use the following command to rescan the SCSI bus:</span></span>
  
    <span data-ttu-id="081bf-277">`$ rescan-scsi-bus.sh `(sg3_utils 패키지의 일부)</span><span class="sxs-lookup"><span data-stu-id="081bf-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="081bf-278">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-278">Type the following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="081bf-279">또는</span><span class="sxs-lookup"><span data-stu-id="081bf-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="081bf-280">최근에 추가된 디스크의 세부 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="081bf-281">StorSimple 디스크인지를 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-281">To determine whether it is a StorSimple disk, use the following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="081bf-282">StorSimple 디스크인지를 확인하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="081bf-283">또한 가능성이 적지만 가능한 원인은 iscsid pid일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="081bf-284">다음 명령을 사용하여 iSCSI 세션에서 로그오프합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-284">Use the following command to log off from the iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="081bf-285">StorSimple 장치인 iSCSI 대상에서 연결된 모든 네트워크 인터페이스에 이 명령을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="081bf-286">모든 iSCSI 세션에서 로그오프하면 iSCSI 대상 IQN을 사용하여 iSCSI 세션을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span></span> <span data-ttu-id="081bf-287">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-287">Type the following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="081bf-288">Q.</span><span class="sxs-lookup"><span data-stu-id="081bf-288">Q.</span></span> <span data-ttu-id="081bf-289">장치를 허용 목록에 추가되었는지 잘 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="081bf-290">A.</span><span class="sxs-lookup"><span data-stu-id="081bf-290">A.</span></span> <span data-ttu-id="081bf-291">장치를 허용 목록에 추가되었는지를 확인하려면 다음 문제 해결 대화형 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span></span>

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


<span data-ttu-id="081bf-292">자세한 내용은 [다중 경로에 문제 해결 대화형 명령 사용](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="081bf-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="081bf-293">유용한 명령 목록</span><span class="sxs-lookup"><span data-stu-id="081bf-293">List of useful commands</span></span>
| <span data-ttu-id="081bf-294">확인하라는 메시지가 표시되면 </span><span class="sxs-lookup"><span data-stu-id="081bf-294">Type</span></span> | <span data-ttu-id="081bf-295">명령</span><span class="sxs-lookup"><span data-stu-id="081bf-295">Command</span></span> | <span data-ttu-id="081bf-296">설명</span><span class="sxs-lookup"><span data-stu-id="081bf-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="081bf-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="081bf-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="081bf-298">iSCSI 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="081bf-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="081bf-299">iSCSI 서비스 중지</span><span class="sxs-lookup"><span data-stu-id="081bf-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="081bf-300">iSCSI 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="081bf-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="081bf-301">지정된 주소에서 사용할 수 있는 대상 검색</span><span class="sxs-lookup"><span data-stu-id="081bf-301">Discover available targets on the specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="081bf-302">iSCSI 대상에 로그인</span><span class="sxs-lookup"><span data-stu-id="081bf-302">Log in to the iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="081bf-303">iSCSI 대상에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="081bf-303">Log out from the iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="081bf-304">iSCSI 초기자 이름 인쇄</span><span class="sxs-lookup"><span data-stu-id="081bf-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="081bf-305">iSCSI 세션 및 호스트에서 검색된 볼륨의 상태 확인</span><span class="sxs-lookup"><span data-stu-id="081bf-305">Check the state of the iSCSI session and volume discovered on the host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="081bf-306">호스트와 StorSimple 장치 간에 설정된 모든 iSCSI 세션 표시</span><span class="sxs-lookup"><span data-stu-id="081bf-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="081bf-307">**다중 경로 지정**</span><span class="sxs-lookup"><span data-stu-id="081bf-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="081bf-308">다중 경로 디먼 시작</span><span class="sxs-lookup"><span data-stu-id="081bf-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="081bf-309">다중 경로 디먼 중지</span><span class="sxs-lookup"><span data-stu-id="081bf-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="081bf-310">다중 경로 디먼 다시 시작</span><span class="sxs-lookup"><span data-stu-id="081bf-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="081bf-311">또는</span><span class="sxs-lookup"><span data-stu-id="081bf-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="081bf-312">부팅 시 시작되도록 다중 경로 디먼 설정</span><span class="sxs-lookup"><span data-stu-id="081bf-312">Enable multipath daemon to start at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="081bf-313">문제 해결을 위한 대화형 콘솔 시작</span><span class="sxs-lookup"><span data-stu-id="081bf-313">Start the interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="081bf-314">다중 경로 연결 및 장치 나열</span><span class="sxs-lookup"><span data-stu-id="081bf-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="081bf-315">`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="081bf-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="081bf-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="081bf-316">Next steps</span></span>
<span data-ttu-id="081bf-317">또한 Linux 호스트에서 MPIO를 구성했기 때문에 다음 CentoS 6.6 문서를 참조해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="081bf-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="081bf-318">CentOS에 MPIO 설정</span><span class="sxs-lookup"><span data-stu-id="081bf-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="081bf-319">Linux 교육 가이드</span><span class="sxs-lookup"><span data-stu-id="081bf-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

