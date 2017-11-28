---
title: "부하 분산된 집합으로 MySQL 클러스터화 | Microsoft Docs"
description: "Azure에서 클래식 배포 모델을 사용하여 만든 부하 분산된 고가용성 Linux MySQL 클러스터를 설정합니다."
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
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="4dd6b-103">부하 분산 집합을 사용하여 Linux에서 MySQL 클러스터화</span><span class="sxs-lookup"><span data-stu-id="4dd6b-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4dd6b-104">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="4dd6b-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="4dd6b-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4dd6b-107">[Resource Manager 템플릿](https://azure.microsoft.com/documentation/templates/mysql-replication/)은 MySQL 클러스터를 배포해야 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="4dd6b-108">이 문서에서는 Microsoft Azure에서 고가용성 Linux 기반 서비스를 배포하는 데 사용할 수 있는 다양한 접근 방법을 살펴보고, MySQL 서버 고가용성을 입문서로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="4dd6b-109">이 접근 방법을 보여 주는 비디오는 [채널 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)(영문)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="4dd6b-110">여기서는 DRBD, Corosync 및 Pacemaker에 기반한 비공유 2개 노드 단일 마스터 MySQL 고가용성 솔루션을 개괄적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="4dd6b-111">한 번에 하나의 노드만 MySQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="4dd6b-112">DRBD 리소스를 쓰고 이 리소스에서 읽는 작업도 한 번에 하나의 노드로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="4dd6b-113">Microsoft Azure에서 부하 분산 집합을 사용하여 라운드 로빈 기능과 VIP(가상 IP)의 끝점 검색, 제거 및 안정적 복구 기능을 제공하므로 LVS와 같은 VIP 솔루션이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="4dd6b-114">VIP는 클라우드 서비스를 처음 만들 때 Microsoft Azure에서 할당한 전역으로 라우팅 가능한 IPv4 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="4dd6b-115">MySQL(NBD Cluster, Percona 및 Galera 포함) 및 여러 개의 미들웨어 솔루션([VM Depot](http://vmdepot.msopentech.com)에서 VM으로 사용할 수 있는 하나 이상의 솔루션 포함)에 가능한 다른 아키텍처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="4dd6b-116">이러한 솔루션이 유니캐스트 및 멀티캐스트/브로드캐스트에서 복제 가능하고 공유 저장소나 다중 네트워크 인터페이스에 의존하지 않는 한, 이러한 시나리오는 Microsoft Azure에 배포하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="4dd6b-117">이러한 클러스터링 아키텍처는 비슷한 방식으로 PostgreSQL 및 OpenLDAP와 같은 다른 제품으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="4dd6b-118">예를 들어 공유되지 않은 이러한 부하 분산 절차는 다중 마스터 OpenLDAP를 사용하여 성공적으로 테스트되었으며, 채널 9 블로그에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="4dd6b-119">준비</span><span class="sxs-lookup"><span data-stu-id="4dd6b-119">Get ready</span></span>
<span data-ttu-id="4dd6b-120">다음과 같은 리소스와 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="4dd6b-121">유효한 구독으로 둘 이상의 VM을 만들 수 있는 Microsoft Azure 계정(이 예제에서는 XS를 사용했음)</span><span class="sxs-lookup"><span data-stu-id="4dd6b-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="4dd6b-122">네트워크 및 서브넷</span><span class="sxs-lookup"><span data-stu-id="4dd6b-122">A network and a subnet</span></span>
  - <span data-ttu-id="4dd6b-123">선호도 그룹</span><span class="sxs-lookup"><span data-stu-id="4dd6b-123">An affinity group</span></span>
  - <span data-ttu-id="4dd6b-124">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="4dd6b-124">An availability set</span></span>
  - <span data-ttu-id="4dd6b-125">클라우드 서비스와 동일한 지역에 VHD를 만들고 Linux VM에 연결할 수 있는 기능</span><span class="sxs-lookup"><span data-stu-id="4dd6b-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="4dd6b-126">테스트된 환경</span><span class="sxs-lookup"><span data-stu-id="4dd6b-126">Tested environment</span></span>
* <span data-ttu-id="4dd6b-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="4dd6b-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="4dd6b-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="4dd6b-128">DRBD</span></span>
  * <span data-ttu-id="4dd6b-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4dd6b-129">MySQL Server</span></span>
  * <span data-ttu-id="4dd6b-130">Corosync 및 Pacemaker</span><span class="sxs-lookup"><span data-stu-id="4dd6b-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="4dd6b-131">선호도 그룹</span><span class="sxs-lookup"><span data-stu-id="4dd6b-131">Affinity group</span></span>
<span data-ttu-id="4dd6b-132">Azure 클래식 포털에 로그인하고 **설정**을 선택하고 선호도 그룹을 만들어 솔루션에 대한 선호도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="4dd6b-133">나중에 만들어진 할당된 리소스는 이 선호도 그룹에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="4dd6b-134">네트워크</span><span class="sxs-lookup"><span data-stu-id="4dd6b-134">Networks</span></span>
<span data-ttu-id="4dd6b-135">새 네트워크가 만들어지고 네트워크 내에 서브넷이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="4dd6b-136">이 예제에서는 내부에 /24 서브넷 하나만 있는 10.10.10.0/24 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="4dd6b-137">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="4dd6b-137">Virtual machines</span></span>
<span data-ttu-id="4dd6b-138">첫 번째 Ubuntu 13.10 VM이 Endorsed Ubuntu Gallery 이미지를 사용하여 만들어지며 `hadb01`이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="4dd6b-139">새 클라우드 서비스가 hadb라는 프로세스에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="4dd6b-140">이 이름은 더 많은 리소스가 추가될 때 서비스에서 갖추게 될 공유 부하 분산 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="4dd6b-141">`hadb01`을 만드는 작업은 특별하지 않으며 포털을 사용하여 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="4dd6b-142">SSH에 대한 끝점이 자동으로 만들어지고 새 네트워크가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="4dd6b-143">이제 VM에 대한 가용성 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="4dd6b-144">첫 번째 VM을 만든 후에(기술적으로 클라우드 서비스를 만들 때) 두 번째 VM, `hadb02`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="4dd6b-145">두 번째 VM의 경우 포털을 사용하여 갤러리에서 Ubuntu 13.10 VM을 사용하지만 새 클라우드 서비스가 아니라 기존의 `hadb.cloudapp.net` 클라우드 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="4dd6b-146">네트워크 및 가용성 집합도 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="4dd6b-147">SSH 끝점도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="4dd6b-148">두 VM을 모두 만든 후에는 `hadb01`(TCP 22) 및 `hadb02`(Azure에서 자동 할당)에 대한 SSH 포트를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="4dd6b-149">연결된 저장소</span><span class="sxs-lookup"><span data-stu-id="4dd6b-149">Attached storage</span></span>
<span data-ttu-id="4dd6b-150">새 디스크를 두 VM에 연결하고 프로세스에서 5GB 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="4dd6b-151">디스크는 주 운영 체제 디스크로 사용되는 VHD 컨테이너에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="4dd6b-152">디스크를 만들어 연결하면 커널에 새 장치가 표시되므로 Linux를 다시 시작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="4dd6b-153">이 장치는 대개 `/dev/sdc`입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="4dd6b-154">출력에 대해서는 `dmesg`를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="4dd6b-155">각 VM에서 `cfdisk`를 사용하여 파티션(기본, Linux 파티션)을 만들고 새 파티션 테이블을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="4dd6b-156">이 파티션에는 파일 시스템을 만들면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="4dd6b-157">클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="4dd6b-157">Set up the cluster</span></span>
<span data-ttu-id="4dd6b-158">APT를 사용하여 두 Ubuntu VM에 Corosync, Pacemaker 및 DRBD를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="4dd6b-159">`apt-get`을 사용하여 그렇게 하려면 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="4dd6b-160">지금 MySQL을 설치하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="4dd6b-161">Debian 및 Ubuntu 설치 스크립트는 `/var/lib/mysql`에 있는 MySQL 데이터 디렉터리를 초기화하지만, 이 디렉터리가 DRBD 파일 시스템으로 대체되므로 나중에 MySQL을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="4dd6b-162">`/sbin/ifconfig`를 사용하여 두 VM이 모두 10.10.10.0/24 서브넷의 주소를 사용하고 서로 이름을 사용하여 ping할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="4dd6b-163">또한 `ssh-keygen` 및 `ssh-copy-id`를 사용하여 두 VM이 암호를 요구하지 않고 SSH를 통해 통신할 수 있는지도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="4dd6b-164">DRBD 설치</span><span class="sxs-lookup"><span data-stu-id="4dd6b-164">Set up DRBD</span></span>
<span data-ttu-id="4dd6b-165">기본 `/dev/sdc1` 파티션을 사용하여 ext3을 통해 포맷되고 기본 노드와 보조 노드 모두에서 사용될 수 있는 `/dev/drbd1` 리소스를 생성하는 DRBD 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="4dd6b-166">`/etc/drbd.d/r0.res`를 열고 두 VM에서 다음 리소스 정의를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="4dd6b-167">두 VM에서 `drbdadm`을 사용하여 리소스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="4dd6b-168">기본 VM(`hadb01`)에서 DRBD 리소스의 소유권(기본)에 대해 다음을 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="4dd6b-169">두 VM에서 /proc/drbd(`sudo cat /proc/drbd`)의 내용을 검토할 경우 여기서 `hadb01`의 `Primary/Secondary`와 `hadb02`의 `Secondary/Primary`가 솔루션과 일치하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="4dd6b-170">5GB 디스크는 고객에게 무료로 10.10.10.0/24 네트워크를 통해 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="4dd6b-171">디스크가 동기화되면 `hadb01`에 파일 시스템을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="4dd6b-172">테스트를 위해 ext2를 사용했지만 다음 코드는 ext3 파일 시스템을 만듭니다:</span><span class="sxs-lookup"><span data-stu-id="4dd6b-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="4dd6b-173">DRBD 리소스 탑재</span><span class="sxs-lookup"><span data-stu-id="4dd6b-173">Mount the DRBD resource</span></span>
<span data-ttu-id="4dd6b-174">이제 `hadb01`에 DRBD 리소스를 탑재할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="4dd6b-175">Debian 및 파생 배포판은 `/var/lib/mysql` 을 MySQL 데이터 디렉터리로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="4dd6b-176">MySQL을 설치하지 않았으므로 디렉터리를 만들고 DRBD 리소스를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="4dd6b-177">이 옵션을 수행하려면 `hadb01`에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="4dd6b-178">MySQL 설치</span><span class="sxs-lookup"><span data-stu-id="4dd6b-178">Set up MySQL</span></span>
<span data-ttu-id="4dd6b-179">이제 `hadb01`에서 MySQL을 설치할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="4dd6b-180">`hadb02`의 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="4dd6b-181">mysql-server를 설치하면 /var/lib/mysql을 만들고 새 데이터 디렉터리로 채운 다음 내용을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="4dd6b-182">이 옵션을 수행하려면 `hadb02`에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="4dd6b-183">두 번째 옵션은 `hadb02`로 장애 조치(failover)한 다음 mysql-server를 여기에 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="4dd6b-184">설치 스크립트에서 기존 설치를 인식하고 이 설치를 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="4dd6b-185">`hadb01`에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="4dd6b-186">`hadb02`에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="4dd6b-187">지금 DRBD를 장애 조치(Failover)할 계획이 아닌 경우 첫 번째 옵션이 더 쉽지만 확실히 덜 깔끔합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="4dd6b-188">설정이 완료되면 MySQL 데이터베이스에 대해 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="4dd6b-189">`hadb02`(또는 DRBD에 따라 활성 중인 서버 중 하나)에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="4dd6b-190">이 마지막 문은 이 표의 루트 사용자에 대한 인증을 사용할 수 없게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="4dd6b-191">이 문은 프로덕션급 GRANT 문으로 바꾼 후 예시 용도로만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="4dd6b-192">또한 VM 외부에서 쿼리를 수행하려면(이 가이드의 목적) MySQL을 위한 네트워킹을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="4dd6b-193">두 VM에서 `/etc/mysql/my.cnf`를 열고 `bind-address`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="4dd6b-194">주소를 127.0.0.1에서 0.0.0.0으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="4dd6b-195">이 파일을 저장한 후에 현재 기본 노드에 대해 `sudo service mysql restart` 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="4dd6b-196">MySQL 부하 분산 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="4dd6b-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="4dd6b-197">포털로 돌아가서 `hadb01`로 이동하고 **끝점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="4dd6b-198">끝점을 만들려면 드롭다운 목록에서 MySQL(TCP 3306)을 선택하고 **새 부하 분산 집합 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="4dd6b-199">부하 분산 끝점의 이름을 `lb-mysql`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="4dd6b-200">**시간**을 5초 이상으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="4dd6b-201">끝점을 만든 후 `hadb02`로 이동하여 **끝점**을 선택하고 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="4dd6b-202">`lb-mysql`을 선택한 다음 드롭다운 목록에서 MySQL을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="4dd6b-203">이 단계를 위해 Azure CLI를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="4dd6b-204">이제 클러스터의 수동 조작에 필요한 모든 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="4dd6b-205">부하 분산 집합 테스트</span><span class="sxs-lookup"><span data-stu-id="4dd6b-205">Test the load-balanced set</span></span>
<span data-ttu-id="4dd6b-206">MySQL 클라이언트를 사용하거나 Azure 웹 사이트로 실행되는 phpMyAdmin과 같은 특정 응용 프로그램을 사용하여 외부 컴퓨터에서 테스트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="4dd6b-207">이 경우 다른 Linux 상자에서 다음과 같은 MySQL의 명령줄 도구를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="4dd6b-208">수동 장애 조치(Failover)</span><span class="sxs-lookup"><span data-stu-id="4dd6b-208">Manually failing over</span></span>
<span data-ttu-id="4dd6b-209">MySQL을 종료하고 DRBD의 기본 노드를 전환한 다음 MySQL을 다시 시작하여 장애 조치를 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="4dd6b-210">이 작업을 수행하려면 hadb01에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="4dd6b-211">그런 후 hadb02에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="4dd6b-212">수동으로 장애 조치를 수행한 후에는 원격 쿼리를 반복할 수 있으며 완벽하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="4dd6b-213">Corosync 설치</span><span class="sxs-lookup"><span data-stu-id="4dd6b-213">Set up Corosync</span></span>
<span data-ttu-id="4dd6b-214">Corosync는 Pacemaker 작동에 필요한 기본 클러스터 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="4dd6b-215">Heartbeat(및 Ultramonkey와 같은 다른 방법)의 경우 Corosync는 CRM 기능에서 분할된 것이지만 Pacemaker는 기능적인 측면에서 Hearbeat와 더 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="4dd6b-216">Azure에서 나타나는 Corosync의 기본적인 제약 조건은 Corosync가 유니캐스트 통신보다는 브로드캐스트를 통한 멀티캐스트 통신 방식을 선호한다는 것입니다. 그렇지만 Microsoft Azure 네트워킹에서는 유니캐스트만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="4dd6b-217">다행히도 Corosync에는 작동 가능한 유니캐스트 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="4dd6b-218">유일한 실질적 제약 조건은 모든 노드가 서로 통신하지 않기 때문에 IP 주소를 포함하여 구성 파일에 노드를 정의해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="4dd6b-219">유니캐스트에 대한 Corosync 예제 파일을 사용하고, 바인드 주소, 노드 목록 및 로깅 디렉터리를 변경하고(Ubuntu는 `/var/log/corosync`를 사용하지만 예제 파일은 `/var/log/cluster`를 사용함), 쿼럼 도구를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="4dd6b-220">다음 `transport: udpu` 지시문과 두 노드에 대해 수동으로 정의된 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="4dd6b-221">두 노드에 대해 `/etc/corosync/corosync.conf`에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="4dd6b-222">두 VM에서 이 구성 파일을 복사하고 다음과 같이 두 노드에서 Corosync를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="4dd6b-223">서비스를 시작한 직후 클러스터가 현재 링에 설정되고 쿼럼이 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="4dd6b-224">로그를 검토하거나 다음 코드를 실행하여 이 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="4dd6b-225">다음 이미지와 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-225">You will see output similar to the following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="4dd6b-227">Pacemaker 설치</span><span class="sxs-lookup"><span data-stu-id="4dd6b-227">Set up Pacemaker</span></span>
<span data-ttu-id="4dd6b-228">Pacemaker는 클러스터를 사용하여 리소스를 모니터링하고, 기본 노드가 작동 중단될 때를 정의하고, 해당 리소스를 보조 노드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="4dd6b-229">리소스는 여러 방법이 있지만 사용 가능한 스크립트 집합이나 LSB(init-like) 스크립트에서 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="4dd6b-230">Pacemaker에서 DRBD 리소스, 탑재 지점 및 MySQL 서비스를 "소유"하기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="4dd6b-231">기본 노드에 좋지 않은 상황이 발생할 때 Pacemaker에서 올바른 순서로 DRBD를 켜고 끌 수 있고, 탑재/분리할 수 있고, MySQL을 시작/중지할 수 있으면 설치가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="4dd6b-232">Pacemaker를 처음 설치할 때는 구성이 다음과 같이 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="4dd6b-233">`sudo crm configure show`를 실행하여 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="4dd6b-234">이제 다음 리소스를 사용하여 파일(예: `/tmp/cluster.conf`)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

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

3. <span data-ttu-id="4dd6b-235">구성에 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-235">Load the file into the configuration.</span></span> <span data-ttu-id="4dd6b-236">하나의 노드에서만 이 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="4dd6b-237">두 노드에서 부팅할 때 Pacemaker가 시작되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="4dd6b-238">`sudo crm_mon –L`을 사용하여 노드 중 하나가 클러스터의 마스터가 되고 모든 리소스를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="4dd6b-239">mount 및 ps를 사용하여 리소스가 실행 중인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="4dd6b-240">다음 스크린샷에서는 한 노드가 중지된 `crm_mon`을 보여 줍니다(종료하려면 Ctrl+C 사용).</span><span class="sxs-lookup"><span data-stu-id="4dd6b-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="4dd6b-242">다음 스크린샷에서는 두 노드, 즉 하나의 마스터와 하나의 슬레이브를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="4dd6b-244">테스트</span><span class="sxs-lookup"><span data-stu-id="4dd6b-244">Testing</span></span>
<span data-ttu-id="4dd6b-245">자동 장애 조치(Failover) 시뮬레이션을 위한 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="4dd6b-246">이 작업을 수행하는 방법에는 소프트 방법과 하드 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="4dd6b-247">소프트 방법은 클러스터의 종료 함수인 ``crm_standby -U `uname -n` -v on``을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="4dd6b-248">마스터에서 이 함수를 사용하면 슬레이브가 대신합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="4dd6b-249">이 값을 다시 off로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-249">Remember to set this back to off.</span></span> <span data-ttu-id="4dd6b-250">이렇게 하지 않으면 crm_mon에서 대기 중인 노드 하나를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="4dd6b-251">하드 방법은 포털을 통하거나 VM의 실행 수준(즉 중지, 종료)을 변경하여 기본 VM(hadb01)을 종료하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="4dd6b-252">이렇게 하면 마스터가 작동 중단되었음을 알리는 신호를 보냄으로써 Corosync 및 Pacemaker에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="4dd6b-253">이러한 동작을 테스트할 수 있지만(유지 관리 창에 유용함) VM을 동결하여 이 시나리오를 강제로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="4dd6b-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="4dd6b-254">STONITH</span></span>
<span data-ttu-id="4dd6b-255">실제 장치를 제어하는 STONITH 스크립트 대신, Azure CLI를 통해 VM 종료를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="4dd6b-256">`/usr/lib/stonith/plugins/external/ssh` 를 기반으로 사용하고 클러스터의 구성에서 STONITH를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="4dd6b-257">Azure CLI는 전역적으로 설치해야 하며 클러스터 사용자를 위해 게시 설정과 프로필을 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="4dd6b-258">리소스의 샘플 코드는 [GitHub](https://github.com/bureado/aztonith)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="4dd6b-259">`sudo crm configure`에 다음을 추가하여 클러스터 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="4dd6b-260">이 스크립트는 up/down 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="4dd6b-261">원래의 SSH 리소스는 ping 검사를 15번 수행했지만 Azure VM의 복구 시간은 좀 더 가변적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="4dd6b-262">제한 사항</span><span class="sxs-lookup"><span data-stu-id="4dd6b-262">Limitations</span></span>
<span data-ttu-id="4dd6b-263">다음 제한 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-263">The following limitations apply:</span></span>

* <span data-ttu-id="4dd6b-264">Pacemaker에서 DRBD를 리소스로 관리하는 linbit DRBD 리소스 스크립트는 노드가 대기 상태일 때도 노드를 종료할 때 `drbdadm down`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="4dd6b-265">슬레이브는 마스터가 쓰기를 받는 동안 DRBD 리소스를 동기화하지 않기 때문에 이러한 방식은 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="4dd6b-266">다행히도 마스터가 실패하지 않으면 슬레이브에서 이전 파일 시스템 상태를 인계받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="4dd6b-267">이러한 문제를 해결할 수 있는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="4dd6b-268">로컬(클러스터화되지 않은) Watchdog을 통해 모든 클러스터 노드에서 `drbdadm up r0` 적용</span><span class="sxs-lookup"><span data-stu-id="4dd6b-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="4dd6b-269">linbit DRBD 스크립트를 편집하여 `/usr/lib/ocf/resource.d/linbit/drbd`에서 `down`이 호출되지 않았는지 확인</span><span class="sxs-lookup"><span data-stu-id="4dd6b-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="4dd6b-270">부하 분산 장치는 응답하는 데 5초 이상 필요하므로 응용 프로그램에서 클러스터를 인식하고 시간 제한을 더 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="4dd6b-271">앱 내 큐 및 쿼리 미들웨어와 같은 다른 아키텍처도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="4dd6b-272">MySQL 튜닝을 통해 쓰기가 관리 가능한 속도로 수행되고 캐시가 가능한 한 자주 디스크로 플러시되어 메모리 손실을 최소화하도록 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="4dd6b-273">쓰기 성능은 가상 스위치의 VM 상호 연결에 따라 달라집니다. 이는 DRBD에서 장치를 복제하는 데 사용하는 메커니즘이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dd6b-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
