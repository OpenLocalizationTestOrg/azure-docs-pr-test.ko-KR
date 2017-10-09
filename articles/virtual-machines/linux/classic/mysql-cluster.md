---
title: "부하 분산 된 집합으로 MySQL aaaClusterize | Microsoft Docs"
description: "Azure의 hello 클래식 배포 모델을 사용 하 여 Linux MySQL 클러스터 만든 부하 분산, 높은 가용성을 설정 합니다."
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="61cab-103">부하 분산 집합 tooclusterize MySQL을 사용 하 여 Linux에서</span><span class="sxs-lookup"><span data-stu-id="61cab-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61cab-104">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="61cab-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="61cab-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="61cab-107">A [리소스 관리자 템플릿](https://azure.microsoft.com/documentation/templates/mysql-replication/) toodeploy MySQL 클러스터 해야 할 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="61cab-108">이 문서를 탐색 하 고 hello 두 가지 방법을 사용할 수 있는 toodeploy 항상 사용 가능한 Linux 기반 Microsoft Azure에서 서비스, 탐색을 입문서로 MySQL Server의 고가용성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="61cab-109">이 접근 방법을 보여 주는 비디오는 [채널 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)(영문)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="61cab-110">여기서는 DRBD, Corosync 및 Pacemaker에 기반한 비공유 2개 노드 단일 마스터 MySQL 고가용성 솔루션을 개괄적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="61cab-111">한 번에 하나의 노드만 MySQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="61cab-112">Hello DRBD 리소스에서에서 읽기와 쓰기 이기도 제한 tooonly 한 노드에서 한 번에 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="61cab-113">Microsoft Azure tooprovide 라운드 로빈 기능과 끝점 검색, 제거 및 hello VIP의 적절 한 복구에 대 한 부하 분산 집합을 사용 하 여 때문에 같은 LVS, VIP 솔루션에 대 한 않아도가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="61cab-114">hello VIP는 hello 클라우드 서비스를 처음 만들 때 Microsoft Azure에 의해 할당 되는 전역적으로 라우팅 가능 IPv4 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="61cab-115">MySQL(NBD Cluster, Percona 및 Galera 포함) 및 여러 개의 미들웨어 솔루션([VM Depot](http://vmdepot.msopentech.com)에서 VM으로 사용할 수 있는 하나 이상의 솔루션 포함)에 가능한 다른 아키텍처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="61cab-116">이러한 솔루션 유니캐스트 및 멀티 캐스트 또는 브로드캐스트에 복제할 수 있고 공유 저장소 또는 여러 개의 네트워크 인터페이스에 의존 하지 않습니다, hello 시나리오에는 Microsoft Azure에서 쉽게 toodeploy 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="61cab-117">Tooother 제품 PostgreSQL OpenLDAP 유사한 방식으로 확장할 수 있습니다 이러한 아키텍처를 클러스터링.</span><span class="sxs-lookup"><span data-stu-id="61cab-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="61cab-118">예를 들어 공유되지 않은 이러한 부하 분산 절차는 다중 마스터 OpenLDAP를 사용하여 성공적으로 테스트되었으며, 채널 9 블로그에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="61cab-119">준비</span><span class="sxs-lookup"><span data-stu-id="61cab-119">Get ready</span></span>
<span data-ttu-id="61cab-120">Hello 다음 필요한 리소스 및 기능:</span><span class="sxs-lookup"><span data-stu-id="61cab-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="61cab-121">두 개 이상의 Vm 수 toocreate 유효한 구독을 사용 하면 Microsoft Azure 계정 (XS이이 예제에서 사용 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="61cab-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="61cab-122">네트워크 및 서브넷</span><span class="sxs-lookup"><span data-stu-id="61cab-122">A network and a subnet</span></span>
  - <span data-ttu-id="61cab-123">선호도 그룹</span><span class="sxs-lookup"><span data-stu-id="61cab-123">An affinity group</span></span>
  - <span data-ttu-id="61cab-124">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="61cab-124">An availability set</span></span>
  - <span data-ttu-id="61cab-125">기능 toocreate Vhd hello hello 클라우드 서비스와 동일한 지역 hello와 toohello Linux Vm에 연결</span><span class="sxs-lookup"><span data-stu-id="61cab-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="61cab-126">테스트된 환경</span><span class="sxs-lookup"><span data-stu-id="61cab-126">Tested environment</span></span>
* <span data-ttu-id="61cab-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="61cab-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="61cab-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="61cab-128">DRBD</span></span>
  * <span data-ttu-id="61cab-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="61cab-129">MySQL Server</span></span>
  * <span data-ttu-id="61cab-130">Corosync 및 Pacemaker</span><span class="sxs-lookup"><span data-stu-id="61cab-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="61cab-131">선호도 그룹</span><span class="sxs-lookup"><span data-stu-id="61cab-131">Affinity group</span></span>
<span data-ttu-id="61cab-132">Toohello Azure 클래식 포털에에서 로그인 하 여 hello 솔루션에 대 한 선호도 그룹 만들기를 선택 하 **설정을**, 및 선호도 그룹 만들기.</span><span class="sxs-lookup"><span data-stu-id="61cab-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="61cab-133">나중에 만들어진 할당 된 리소스 toothis 선호도 그룹에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="61cab-134">네트워크</span><span class="sxs-lookup"><span data-stu-id="61cab-134">Networks</span></span>
<span data-ttu-id="61cab-135">새 네트워크를 만들고 서브넷 hello 네트워크 내부에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="61cab-136">이 예제에서는 내부에 /24 서브넷 하나만 있는 10.10.10.0/24 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="61cab-137">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="61cab-137">Virtual machines</span></span>
<span data-ttu-id="61cab-138">첫 번째 Ubuntu 13.10 VM Endorsed Ubuntu 갤러리 이미지를 사용 하 여 만들어지고 라고 hello `hadb01`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="61cab-139">새 클라우드 서비스는 hadb 라고 하는 hello 프로세스에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="61cab-140">이 이름은 hello를, 이전에 공유 리소스를 더 추가 되 면 hello 서비스 있는 부하 분산 된 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="61cab-141">만들기 hello `hadb01` hello 포털을 사용 하 여 정상적인 시간 및 완료 된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="61cab-142">SSH에 대 한 끝점은 자동으로 만들어지고 hello 새 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="61cab-143">이제 가용성 집합 hello Vm 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="61cab-144">만듭니다 (기술적으로 hello 클라우드 서비스를 만드는 경우) 첫 번째 VM이 생성 하는 hello, 후 두 번째 VM hello `hadb02`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="61cab-145">Hello에 대 한 VM의 두 번째, hello 포털을 사용 하 여 hello 갤러리에서에서 Ubuntu 13.10 VM을 사용 하지만 기존 클라우드 서비스를 사용 하 여 `hadb.cloudapp.net`, 새로 만드는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="61cab-146">hello 네트워크 및 가용성 집합을 자동으로 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="61cab-147">SSH 끝점도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="61cab-148">두 Vm을 만든 후 기록해 hello SSH 포트가 `hadb01` (TCP 22) 및 `hadb02` (자동으로 할당 된 Azure에서).</span><span class="sxs-lookup"><span data-stu-id="61cab-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="61cab-149">연결된 저장소</span><span class="sxs-lookup"><span data-stu-id="61cab-149">Attached storage</span></span>
<span data-ttu-id="61cab-150">새 디스크 tooboth Vm 꽂고 hello 프로세스에 5GB 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="61cab-151">hello 디스크는 주 운영 체제 디스크에 대 한 사용 hello VHD 컨테이너에 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="61cab-152">디스크를 만들고 연결 된 후 없습니다 필요 toorestart Linux 되므로 hello 커널 hello 새 장치에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="61cab-153">이 장치는 대개 `/dev/sdc`입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="61cab-154">확인 `dmesg` hello 출력에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="61cab-155">각 VM에서 사용 하 여 파티션을 만들려면 `cfdisk` (Linux, 주 파티션) hello 새 파티션 테이블을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="61cab-156">이 파티션에는 파일 시스템을 만들면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="61cab-157">Hello 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="61cab-157">Set up hello cluster</span></span>
<span data-ttu-id="61cab-158">APT tooinstall Corosync, Pacemaker, 및 DRBD 두 Ubuntu Vm에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="61cab-159">toodo 사용 `apt-get`실행 hello 다음 코드:</span><span class="sxs-lookup"><span data-stu-id="61cab-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="61cab-160">지금 MySQL을 설치하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="61cab-161">Debian 및 Ubuntu 설치 스크립트에 MySQL 데이터 디렉터리를 초기화 합니다 `/var/lib/mysql`, 하지만 나중에 MySQL tooinstall hello 디렉터리는 DRBD 파일 시스템에 의해 교체 됩니다, 때문에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="61cab-162">확인 (사용 하 여 `/sbin/ifconfig`) 두 Vm hello 10.10.10.0/24 서브넷의 주소 및 이러한 ping 수 있는지 다른 이름으로 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="61cab-163">사용할 수도 있습니다 `ssh-keygen` 및 `ssh-copy-id` toomake 두 Vm 암호를 요구 하지 않고 SSH를 통해 통신할 수 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="61cab-164">DRBD 설치</span><span class="sxs-lookup"><span data-stu-id="61cab-164">Set up DRBD</span></span>
<span data-ttu-id="61cab-165">기본 hello를 사용 하 여 DRBD 리소스 만들기 `/dev/sdc1` tooproduce 파티션는 `/dev/drbd1` ext3를 사용 하 여 포맷 하 고 기본 및 보조 노드에서 사용할 수 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="61cab-166">열기 `/etc/drbd.d/r0.res` 복사 hello 두 Vm에서 리소스 정의 따라:</span><span class="sxs-lookup"><span data-stu-id="61cab-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="61cab-167">Hello 리소스를 사용 하 여 초기화 `drbdadm` 두 Vm에서:</span><span class="sxs-lookup"><span data-stu-id="61cab-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="61cab-168">주 VM hello (`hadb01`)를 강제로 hello DRBD 리소스의 소유권이 (주 서버):</span><span class="sxs-lookup"><span data-stu-id="61cab-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="61cab-169">/ Proc/drbd의 hello 내용을 검사 하는 경우 (`sudo cat /proc/drbd`) 두 Vm에서 표시 되어야 `Primary/Secondary` 에 `hadb01` 및 `Secondary/Primary` 에 `hadb02`hello 솔루션과 시점에서 일관 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="61cab-170">hello 5GB 디스크에 없는 충전 toocustomers hello 10.10.10.0/24 네트워크를 통해 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="61cab-171">Hello 디스크 동기화 된 후에 hello 파일 시스템을 만들 수 있습니다 `hadb01`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="61cab-172">테스트를 위해 e x t 2를 사용 하지만 코드 다음 hello ext3 파일 시스템 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="61cab-173">Hello DRBD 리소스 탑재</span><span class="sxs-lookup"><span data-stu-id="61cab-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="61cab-174">이제 준비 toomount hello DRBD 리소스에는 `hadb01`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="61cab-175">Debian 및 파생 배포판은 `/var/lib/mysql` 을 MySQL 데이터 디렉터리로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="61cab-176">MySQL를 설치 하지 않은 때문에 hello 디렉터리 만들고 hello DRBD 리소스 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="61cab-177">tooperform hello 코드 다음을 실행 하는이 옵션을 `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="61cab-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="61cab-178">MySQL 설치</span><span class="sxs-lookup"><span data-stu-id="61cab-178">Set up MySQL</span></span>
<span data-ttu-id="61cab-179">이제 준비 tooinstall MySQL에서 `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="61cab-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="61cab-180">`hadb02`의 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="61cab-181">Mysql 서버 /var/lib/mysql, 새 데이터 디렉터리를 채울 만들고 다음 hello 콘텐츠를 제거를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="61cab-182">tooperform hello 코드 다음을 실행 하는이 옵션을 `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="61cab-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="61cab-183">hello 두 번째 방법은 toofailover 너무`hadb02` 다음 mysql 서버 있습니다를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="61cab-184">설치 스크립트는 hello 기존 설치 및 것을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="61cab-185">실행 hello 다음 코드에 `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="61cab-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="61cab-186">실행 hello 다음 코드에 `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="61cab-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="61cab-187">Toofailover DRBD을 지금 않으려는 hello 첫 번째 옵션 이지만 다소 덜 세련 된 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="61cab-188">설정이 완료되면 MySQL 데이터베이스에 대해 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="61cab-189">실행 hello 다음 코드에 `hadb02` (또는 hello 서버 중 하나가 활성 상태 이면 tooDRBD에 따라):</span><span class="sxs-lookup"><span data-stu-id="61cab-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="61cab-190">이 마지막 문은이 테이블에 루트 사용자 hello에 대 한 인증을 효과적으로 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="61cab-191">이 문은 프로덕션급 GRANT 문으로 바꾼 후 예시 용도로만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="61cab-192">(즉,이 가이드의 목적은 hello) 외부 hello Vm에서 toomake 쿼리를 원하는 경우 MySQL에 대 한 네트워킹 tooenable를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="61cab-193">두 Vm에서 엽니다 `/etc/mysql/my.cnf` 너무 이동`bind-address`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="61cab-194">Hello 주소 127.0.0.1에서 변경 too0.0.0.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="61cab-195">Hello 파일을 저장 후 실행 하는 `sudo service mysql restart` 현재 주입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="61cab-196">Hello MySQL 부하 분산 된 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="61cab-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="61cab-197">Toohello 포털 돌아가서, 너무 이동`hadb01`, 선택 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="61cab-198">hello 드롭 다운 목록 및 선택에서 MySQL (TCP 3306)를 선택 하는 끝점, toocreate **만들기 새 부하 분산 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="61cab-199">이름 hello 부하 분산 끝점 `lb-mysql`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="61cab-200">설정 **시간** 최소 too5 초입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="61cab-201">Hello 끝점을 만든 후 너무 이동`hadb02`, 선택 **끝점**, 한 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="61cab-202">선택 `lb-mysql`, MySQL hello 드롭 다운 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="61cab-203">또한이 단계에 대 한 hello Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="61cab-204">이제 hello 클러스터의 수동 작업을 위해 필요한 모든 항목이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="61cab-205">Hello 부하 분산 집합을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-205">Test hello load-balanced set</span></span>
<span data-ttu-id="61cab-206">MySQL 클라이언트를 사용하거나 Azure 웹 사이트로 실행되는 phpMyAdmin과 같은 특정 응용 프로그램을 사용하여 외부 컴퓨터에서 테스트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="61cab-207">이 경우 다른 Linux 상자에서 다음과 같은 MySQL의 명령줄 도구를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="61cab-208">수동 장애 조치(Failover)</span><span class="sxs-lookup"><span data-stu-id="61cab-208">Manually failing over</span></span>
<span data-ttu-id="61cab-209">MySQL을 종료하고 DRBD의 기본 노드를 전환한 다음 MySQL을 다시 시작하여 장애 조치를 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="61cab-210">tooperform hello hadb01에 코드를 다음을 실행 하는이 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="61cab-211">그런 후 hadb02에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="61cab-212">수동으로 장애 조치를 수행한 후에는 원격 쿼리를 반복할 수 있으며 완벽하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="61cab-213">Corosync 설치</span><span class="sxs-lookup"><span data-stu-id="61cab-213">Set up Corosync</span></span>
<span data-ttu-id="61cab-214">Corosync는 Pacemaker toowork에 필요한 hello 기반이 되는 클러스터 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="61cab-215">하트 비트 (및 Ultramonkey와 같은 기타 다른 방법) Corosync는 hello CRM 기능 분할 때 유사한 tooHeartbeat Pacemaker 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="61cab-216">Azure에서 Corosync에 대 한 hello 기본적인 제약 Corosync 유니캐스트 통신 보다 브로드캐스트를 통해 멀티 캐스트를 선호 하지만 Microsoft Azure 네트워킹 유니캐스트 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="61cab-217">다행히도 Corosync에는 작동 가능한 유니캐스트 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="61cab-218">hello 유일한 제약 조건은 모든 노드가 서로 통신 하지 않습니다, 때문에 해당 IP 주소를 포함 하 여 구성 파일에서 toodefine hello 노드를 필요로 한다는입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="61cab-219">유니캐스트 및 변경 바인딩 주소, 노드 목록 및 로깅 디렉터리에 대 한 hello Corosync 예제 파일을 사용할 수 있습니다 (사용 하 여 Ubuntu `/var/log/corosync` hello 예제 파일에서 사용 하는 동안 `/var/log/cluster`), 쿼럼 도구를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="61cab-220">Hello 다음을 사용 하 여 `transport: udpu` 지시문과 hello 수동으로 두 노드 모두에 대 한 IP 주소를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="61cab-221">실행 hello 다음 코드에 `/etc/corosync/corosync.conf` 노드 모두에 대해:</span><span class="sxs-lookup"><span data-stu-id="61cab-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="61cab-222">두 VM에서 이 구성 파일을 복사하고 다음과 같이 두 노드에서 Corosync를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="61cab-223">Hello 서비스를 시작한 후에 곧 hello 클러스터 hello 현재 링에 반영할 수 및 쿼럼을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="61cab-224">이 기능은 코드 다음 hello를 실행 하거나 로그를 검토 하 여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="61cab-225">다음 이미지는 출력 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-225">You will see output similar toohello following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="61cab-227">Pacemaker 설치</span><span class="sxs-lookup"><span data-stu-id="61cab-227">Set up Pacemaker</span></span>
<span data-ttu-id="61cab-228">Pacemaker 사용 하 여 리소스에 대 한 클러스터 toomonitor hello를 정의한 기본 아래로 이동 하는 경우 이러한 리소스 toosecondaries 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="61cab-229">리소스는 여러 방법이 있지만 사용 가능한 스크립트 집합이나 LSB(init-like) 스크립트에서 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="61cab-230">Pacemaker 너무 "직접" hello DRBD 리소스, hello 탑재 지점 및 hello MySQL 서비스 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="61cab-231">Pacemaker DRBD 켜거나 끌 수, 하는 경우 탑재 및 분리를 하 고으로 시작 및 중지 MySQL hello 순서 때 문제가 발생 하는 기본, hello로 설치가 완료 되 고 오른쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="61cab-232">Pacemaker를 처음 설치할 때는 구성이 다음과 같이 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="61cab-233">실행 하 여 hello 구성을 확인 `sudo crm configure show`합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="61cab-234">파일을 만듭니다 (같은 `/tmp/cluster.conf`) 리소스 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="61cab-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="61cab-235">Hello 구성에 hello 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="61cab-236">하기만 하면 toodo이를 하나의 노드에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="61cab-237">두 노드에서 부팅할 때 Pacemaker가 시작되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="61cab-238">사용 하 여 `sudo crm_mon –L`, hello 클러스터에 대 한 hello 마스터 바뀌었기 노드 중 하나 및 hello 리소스를 모두 실행 되 고 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="61cab-239">탑재 및 ps toocheck hello 리소스를 실행 하는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="61cab-240">다음 스크린 샷에 표시 hello `crm_mon` 하나의 노드가 중지 (Ctrl + C를 선택 하 여 종료):</span><span class="sxs-lookup"><span data-stu-id="61cab-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="61cab-242">다음 스크린샷에서는 두 노드, 즉 하나의 마스터와 하나의 슬레이브를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="61cab-244">테스트</span><span class="sxs-lookup"><span data-stu-id="61cab-244">Testing</span></span>
<span data-ttu-id="61cab-245">자동 장애 조치(Failover) 시뮬레이션을 위한 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="61cab-246">두 가지 방법으로 toodo이: 소프트 및 하드 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="61cab-247">hello 소프트 방식으로 함수 사용 하 여 hello 클러스터의 종료: ``crm_standby -U `uname -n` -v on``합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="61cab-248">이 사용 하 여 hello 마스터 hello 슬레이브 빠른 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="61cab-249">이 백 toooff tooset를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="61cab-250">이렇게 하지 않으면 crm_mon에서 대기 중인 노드 하나를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="61cab-251">hello 복잡 한 과정을 종료 하 고 hello 다운 기본 VM (hadb01) hello 포털을 통해 또는 변경 하 여 hello hello (즉, 중지, 종료) VM에서 실행 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="61cab-252">아래로 hello 마스터 하락 신호를 보내 Corosync 및 Pacemaker를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="61cab-253">이 테스트할 수 있습니다 (유지 관리 기간에 유용) 하지만 VM hello 고정 하 여 hello 시나리오를 강제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="61cab-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="61cab-254">STONITH</span></span>
<span data-ttu-id="61cab-255">가능한 tooissue hello Azure CLI STONITH 스크립트는 물리적 장치를 제어 하는 대신이 대화 상자를 통해 VM 종료 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="61cab-256">사용할 수 있습니다 `/usr/lib/stonith/plugins/external/ssh` 자료 및 STONITH hello 클러스터 구성에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="61cab-257">Azure CLI 전역으로 설치 해야 하 고 hello 게시 설정 hello 클러스터의 사용자에 대 한 프로필을 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="61cab-258">Hello 리소스에 대 한 예제 코드에서 사용할 수는 [GitHub](https://github.com/bureado/aztonith)합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="61cab-259">Hello 너무 다음을 추가 하 여 hello 클러스터의 구성을 변경`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="61cab-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="61cab-260">hello 스크립트 위쪽/아래쪽 검사를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="61cab-261">hello 원래 SSH 리소스 15 ping 검사 있지만 Azure VM에 대 한 복구 시간에 더 많은 변수가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="61cab-262">제한 사항</span><span class="sxs-lookup"><span data-stu-id="61cab-262">Limitations</span></span>
<span data-ttu-id="61cab-263">다음과 같은 제한을 hello에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-263">hello following limitations apply:</span></span>

* <span data-ttu-id="61cab-264">linbit DRBD 리소스 스크립트의 Pacemaker 사용 리소스로 DRBD를 관리 하는 hello `drbdadm down` hello 노드 대기 것 이죠 하는 경우에 노드를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="61cab-265">이 않으므로 이상적인 hello 슬레이브 됩니다 하지 수 hello DRBD 리소스 동안 동기화 hello 마스터 쓰기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="61cab-266">Hello 마스터 정중 실패 하지 않는 경우 hello 슬레이브 오래 된 파일 시스템 상태가 대신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="61cab-267">이러한 문제를 해결할 수 있는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="61cab-268">로컬(클러스터화되지 않은) Watchdog을 통해 모든 클러스터 노드에서 `drbdadm up r0` 적용</span><span class="sxs-lookup"><span data-stu-id="61cab-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="61cab-269">Hello linbit DRBD 스크립트를 편집 하 고 있는지 확인 합니다 `down` 호출 하지 않습니다`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="61cab-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="61cab-270">hello 부하 분산 장치는 응용 프로그램 클러스터와 되어야 시간 제한의 보다 적절 하 게 되므로 적어도 5 초 toorespond가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="61cab-271">앱 내 큐 및 쿼리 미들웨어와 같은 다른 아키텍처도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="61cab-272">MySQL 튜닝 필요한 tooensure 관리 가능한 속도로 작성이 수행 되며 캐시 플러시 toodisk를 가능한 toominimize 메모리 손실로 자주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="61cab-273">쓰기 성능 VM에 따라 달라 집니다.이 속성은 DRBD tooreplicate hello 장치에서 사용 하는 hello 메커니즘 때문에 hello 가상 스위치에 상호 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="61cab-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
