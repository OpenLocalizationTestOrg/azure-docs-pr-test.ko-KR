---
title: "Azure에서 클러스터 aaaRun MariaDB (MySQL) | Microsoft Docs"
description: "Azure 가상 컴퓨터에 MariaDB + Galera MySQL 클러스터를 만듭니다."
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="2afe9-103">MariaDB(MySQL) 클러스터: Azure 자습서</span><span class="sxs-lookup"><span data-stu-id="2afe9-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2afe9-104">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="2afe9-105">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="2afe9-106">대부분의 새로운 배포 hello Azure 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="2afe9-107">이제 MariaDB Enterprise 클러스터 hello Azure Marketplace에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="2afe9-108">hello 새 제공 MariaDB Galera 클러스터에서 Azure 리소스 관리자를 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="2afe9-109">새 제공 hello를 사용 해야 [Azure 마켓플레이스](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="2afe9-110">이 문서에서는 다중 마스터 toocreate [Galera](http://galeracluster.com/products/) 의 클러스터 [MariaDBs](https://mariadb.org/en/about/) (MySQL에 대 한 대체 하는 강력 하 고 확장 가능한 신뢰할 수 있는 방법) toowork Azure에서 항상 사용 가능한 환경에서 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="2afe9-111">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="2afe9-111">Architecture overview</span></span>
<span data-ttu-id="2afe9-112">이 문서에서는 다음 toocomplete hello 단계 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="2afe9-113">3개 노드 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="2afe9-114">Hello OS 디스크에서 데이터 디스크를 별도 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="2afe9-115">RAID 0/스트라이프 설정 tooincrease IOPS에에서 hello 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="2afe9-116">Hello 3 노드에 대 한 Azure 부하 분산 장치 toobalance hello 부하를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="2afe9-117">반복적인 toominimize 작동 MariaDB + Galera를 포함 하는 VM 이미지를 만들고 사용 하 여 toocreate hello 다른 클러스터 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![시스템 아키텍처](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="2afe9-119">이 항목에서는 hello [Azure CLI](../../../cli-install-nodejs.md) 도구, 만들어지므로 toodownload 있는지를 확인 하 toohello 지침에 따라 tooyour Azure 구독에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="2afe9-120">Hello Azure CLI에서에서 사용할 수 있는 참조 toohello 명령 필요한 경우 참조 hello [Azure CLI 명령 참조](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="2afe9-121">너무 필요 합니다[인증을 위해 SSH 키를 만들려면] hello.pem 파일 위치 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="2afe9-122">Hello 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="2afe9-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="2afe9-123">인프라</span><span class="sxs-lookup"><span data-stu-id="2afe9-123">Infrastructure</span></span>
1. <span data-ttu-id="2afe9-124">선호도 그룹 toohold hello 리소스를 함께 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="2afe9-125">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="2afe9-126">저장소 계정 toohost 우리의 모든 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="2afe9-127">Hello에 40 개 이상의 많이 사용 되는 디스크를 추가 하지 않아야 하면 동일한 저장소 계정 tooavoid hello 20, 000 IOPS 저장소 계정 제한에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="2afe9-128">이 경우 하 한도 보다 상당히 있으므로 hello 단순성에 동일한 계정에서 모든 항목이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="2afe9-129">CentOS 7 hello 가상 컴퓨터 이미지의 hello 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="2afe9-130">다음과 같이 hello 출력 됩니다 `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="2afe9-131">Hello 단계 다음에 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="2afe9-132">Hello VM 템플릿을 만들고 /path/to/key.pem 생성 hello.pem SSH 키를 저장 하는 hello 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="2afe9-133">4 개의 500GB 데이터 디스크 toohello VM hello RAID 구성에서 사용 하기 위해 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="2afe9-134">SSH toosign toohello 템플릿에서 mariadbhatemplate.cloudapp.net:22 때 만든 VM 사용 하 고 사용자의 개인 키를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="2afe9-135">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="2afe9-135">Software</span></span>
1. <span data-ttu-id="2afe9-136">Hello 루트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="2afe9-137">RAID 지원을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-137">Install RAID support:</span></span>

    <span data-ttu-id="2afe9-138">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-138">a.</span></span> <span data-ttu-id="2afe9-139">mdadm을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="2afe9-140">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-140">b.</span></span> <span data-ttu-id="2afe9-141">EXT4 파일 시스템으로 hello RAID0/stripe 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="2afe9-142">c.</span><span class="sxs-lookup"><span data-stu-id="2afe9-142">c.</span></span> <span data-ttu-id="2afe9-143">Hello 탑재 지점 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="2afe9-144">d.</span><span class="sxs-lookup"><span data-stu-id="2afe9-144">d.</span></span> <span data-ttu-id="2afe9-145">Hello hello 새로 만든 RAID 장치의 UUID를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="2afe9-146">e.</span><span class="sxs-lookup"><span data-stu-id="2afe9-146">e.</span></span> <span data-ttu-id="2afe9-147">/etc/fstab을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="2afe9-148">f.</span><span class="sxs-lookup"><span data-stu-id="2afe9-148">f.</span></span> <span data-ttu-id="2afe9-149">다시 시작할 때 hello UUID hello 값으로 대체 탑재 hello 장치 tooenable 자동 이전 hello에서 가져온 추가 **blkid** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="2afe9-150">g.</span><span class="sxs-lookup"><span data-stu-id="2afe9-150">g.</span></span> <span data-ttu-id="2afe9-151">새 파티션을 hello 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="2afe9-152">MariaDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-152">Install MariaDB.</span></span>

    <span data-ttu-id="2afe9-153">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-153">a.</span></span> <span data-ttu-id="2afe9-154">Hello MariaDB.repo 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="2afe9-155">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-155">b.</span></span> <span data-ttu-id="2afe9-156">콘텐츠를 다음 hello로 hello 리포지토리 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="2afe9-157">c.</span><span class="sxs-lookup"><span data-stu-id="2afe9-157">c.</span></span> <span data-ttu-id="2afe9-158">tooavoid 충돌 기존 후 위 및 mariadb 라이브러리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="2afe9-159">d.</span><span class="sxs-lookup"><span data-stu-id="2afe9-159">d.</span></span> <span data-ttu-id="2afe9-160">Galera와 함께 MariaDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="2afe9-161">Hello MySQL 데이터 디렉터리 toohello RAID 블록 장치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="2afe9-162">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-162">a.</span></span> <span data-ttu-id="2afe9-163">새 위치에 hello 현재 MySQL 디렉터리를 복사 하 고 hello 이전 디렉터리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="2afe9-164">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-164">b.</span></span> <span data-ttu-id="2afe9-165">Hello 새 디렉터리에 대 한 사용 권한을 적절 하 게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="2afe9-166">c.</span><span class="sxs-lookup"><span data-stu-id="2afe9-166">c.</span></span> <span data-ttu-id="2afe9-167">Hello 이전 디렉터리 toohello 새 위치에 hello RAID 파티션 가리키는 기호화 된 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="2afe9-168">때문에 [SELinux hello 클러스터 작동을 방해](http://galeracluster.com/documentation-webpages/configuration.html#selinux), 필요한 toodisable는 hello 현재 세션에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="2afe9-169">편집 `/etc/selinux/config` toodisable 후속 다시 시작에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="2afe9-170">MySQL 실행의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="2afe9-171">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-171">a.</span></span> <span data-ttu-id="2afe9-172">MySQL을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="2afe9-173">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-173">b.</span></span> <span data-ttu-id="2afe9-174">MySQL 설치 hello를 보호, hello 루트 암호를 설정, 익명 사용자에 게 toodisable 원격 루트 로그인을 제거 및 hello 테스트 데이터베이스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="2afe9-175">c.</span><span class="sxs-lookup"><span data-stu-id="2afe9-175">c.</span></span> <span data-ttu-id="2afe9-176">클러스터 작업에 대 한 및 필요에 따라 응용 프로그램에 대 한 hello 데이터베이스에 대 한 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="2afe9-177">d.</span><span class="sxs-lookup"><span data-stu-id="2afe9-177">d.</span></span> <span data-ttu-id="2afe9-178">MySQL을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="2afe9-179">구성 자리 표시자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="2afe9-180">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-180">a.</span></span> <span data-ttu-id="2afe9-181">Hello MySQL 구성 toocreate hello 클러스터 설정에 대 한 자리 표시자를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="2afe9-182">Hello를 대체 하지 않고  **`<Variables>`**  또는 지금 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="2afe9-183">이 템플릿에서 VM을 만든 후에 그렇게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="2afe9-184">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-184">b.</span></span> <span data-ttu-id="2afe9-185">Hello 편집  **[galera]**  섹션 및 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="2afe9-186">c.</span><span class="sxs-lookup"><span data-stu-id="2afe9-186">c.</span></span> <span data-ttu-id="2afe9-187">Hello 편집 **[mariadb]** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2afe9-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="2afe9-188">CentOS 7 FirewallD를 사용 하 여 hello 방화벽에 필요한 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="2afe9-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="2afe9-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="2afe9-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="2afe9-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="2afe9-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="2afe9-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="2afe9-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="2afe9-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="2afe9-193">다시 로드 hello 방화벽:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="2afe9-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="2afe9-194">Hello 시스템 성능을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-194">Optimize hello system for performance.</span></span> <span data-ttu-id="2afe9-195">자세한 내용은 [성능 조정 전략](optimize-mysql.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2afe9-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="2afe9-196">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-196">a.</span></span> <span data-ttu-id="2afe9-197">다시 hello 된 MySQL 구성 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="2afe9-198">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-198">b.</span></span> <span data-ttu-id="2afe9-199">Hello 편집 **[mariadb]** 섹션 및 hello 다음 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="2afe9-200">innodb\_buffer\_pool_size를 VM 메모리의 70%로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="2afe9-201">이 예제에서는 그가 설정 된 2.45 GB hello 중간의 RAM이 3.5 g B를 사용 하 여 Azure VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="2afe9-202">MySQL을 중지, 시작 tooavoid hello 클러스터 노드를 추가 하는 경우 중단에서 실행 되지 않도록 MySQL 서비스를 사용 하지 않도록 설정 하 고 hello 컴퓨터를 프로 비전 해제.</span><span class="sxs-lookup"><span data-stu-id="2afe9-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="2afe9-203">Hello 포털을 통해 VM hello를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="2afe9-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="2afe9-204">(현재 [hello Azure CLI 도구에서 #1268 발급](https://github.com/Azure/azure-xplat-cli/issues/1268) hello Azure CLI 도구에서 캡처한 이미지 hello 연결 된 데이터 디스크를 캡처하지 않으면 hello 팩트에 설명 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2afe9-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="2afe9-205">a.</span><span class="sxs-lookup"><span data-stu-id="2afe9-205">a.</span></span> <span data-ttu-id="2afe9-206">Hello 포털을 통해 hello 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="2afe9-207">b.</span><span class="sxs-lookup"><span data-stu-id="2afe9-207">b.</span></span> <span data-ttu-id="2afe9-208">클릭 **캡처** hello 이미지 이름으로 지정 하 고 **mariadb galera 이미지**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="2afe9-209">설명을 입력하고 "waagent를 실행했습니다." 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Hello 가상 컴퓨터 캡처](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="2afe9-211">Hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="2afe9-211">Create hello cluster</span></span>
<span data-ttu-id="2afe9-212">사용자를 만든 다음 구성 하 고 hello 클러스터를 시작 하는 hello 템플릿을 사용 하 여 세 개의 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="2afe9-213">Hello mariadb galera 이미지에서 첫 번째 CentOS 7 VM 이미지를 만든 hello 다음 정보를 제공 하는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="2afe9-214">가상 네트워크 이름: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="2afe9-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="2afe9-215">서브넷: mariadb</span><span class="sxs-lookup"><span data-stu-id="2afe9-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="2afe9-216">컴퓨터 크기: medium</span><span class="sxs-lookup"><span data-stu-id="2afe9-216">Machine size: medium</span></span>
 - <span data-ttu-id="2afe9-217">클라우드 서비스 이름: mariadbha (또는 원하는 이름 원하는 toobe mariadbha.cloudapp.net를 통해 액세스)</span><span class="sxs-lookup"><span data-stu-id="2afe9-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="2afe9-218">컴퓨터 이름: mariadb1</span><span class="sxs-lookup"><span data-stu-id="2afe9-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="2afe9-219">사용자 이름: azureuser</span><span class="sxs-lookup"><span data-stu-id="2afe9-219">Username: azureuser</span></span>
 - <span data-ttu-id="2afe9-220">SSH 액세스: enabled</span><span class="sxs-lookup"><span data-stu-id="2afe9-220">SSH access: enabled</span></span>
 - <span data-ttu-id="2afe9-221">Hello SSH 인증서.pem 파일을 전달 하 고 /path/to/key.pem 생성 hello.pem SSH 키를 저장 하는 hello 경로로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2afe9-222">hello 다음 명령을 분할 명확성을 위해 여러 줄에 있지만 각각 한 줄으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="2afe9-223">Toohello mariadbha 클라우드 서비스를 연결 하 여 두 개 더 많은 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="2afe9-224">Hello VM 이름 변경 및 SSH 포트 tooa 고유한 포트의 다른 Vm와 충돌 하지 hello hello 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="2afe9-225">MariaDB3의 경우:</span><span class="sxs-lookup"><span data-stu-id="2afe9-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="2afe9-226">Hello 다음 단계에 대 한 hello 3 개의 Vm 각각의 tooget hello 내부 IP 주소에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![IP 주소 가져오기](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="2afe9-228">SSH toosign toohello 세 Vm에서 사용 하 고는 각각에 대해 hello 구성 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="2afe9-229">주석 처리 제거  **`wsrep_cluster_name`**  및  **`wsrep_cluster_address`**  hello를 제거 하 여  **#**  hello 줄의 hello 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="2afe9-230">또한 대체  **`<ServerIP>`**  에  **`wsrep_node_address`**  및  **`<NodeName>`**  에  **`wsrep_node_name`**  hello로 VM의 IP 주소 및 이름을 각각 지정 하 고도 해당 줄의 주석 처리 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="2afe9-231">MariaDB1에 hello 클러스터를 시작 하 고 시작 시 실행 되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="2afe9-232">MariaDB2 및 MariaDB3에서 MySQL을 시작하고 시작 시 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="2afe9-233">부하 분산 hello 클러스터</span><span class="sxs-lookup"><span data-stu-id="2afe9-233">Load balance hello cluster</span></span>
<span data-ttu-id="2afe9-234">클러스터 된 hello Vm을 만들 때 추가한 clusteravset tooensure 이러한 서로 다른 장애 도메인과 업데이트 도메인에 추가 된 하 고 있는지 Azure 되지 않는 모든 컴퓨터에서 유지 관리 한 번에 호출 하는 가용성 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="2afe9-235">이 구성은 hello Azure 서비스 수준 계약 (SLA)에서 지 원하는 toobe hello 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="2afe9-236">이제 Azure 부하 분산 장치 toobalance 요청 hello 3 개 노드 사이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="2afe9-237">Hello hello Azure CLI를 사용 하 여 명령을 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="2afe9-238">hello 명령 매개 변수 구조는 같습니다.`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="2afe9-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="2afe9-239">hello CLI hello 부하 분산 장치 프로브 간격 too15 초 약간 너무 오래 될 수 있는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="2afe9-240">Hello 포털에서 변경 **끝점** hello Vm 중 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![끝점 편집](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="2afe9-242">선택 **Load-Balanced 설정 Reconfigure hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![다시 구성 hello 부하 분산 된 집합](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="2afe9-244">변경 **프로브 간격** too5 시간 (초) 하 고 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![프로브 간격 변경](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="2afe9-246">Hello 클러스터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="2afe9-246">Validate hello cluster</span></span>
<span data-ttu-id="2afe9-247">hello 복잡 한 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-247">hello hard work is done.</span></span> <span data-ttu-id="2afe9-248">hello 클러스터에서 액세스할 수 이제 해야 `mariadbha.cloudapp.net:3306`hello 부하 분산 장치를 적중 하는, 및 원활 하 고 효율적으로 사이의 경로 요청 hello 세 개의 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="2afe9-249">즐겨 찾는 MySQL 클라이언트 tooconnect 사용 하거나이 클러스터가 작동 하는 hello Vm tooverify 중 하나에서 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="2afe9-250">그런 다음 데이터베이스를 만들고 일부 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="2afe9-251">hello 데이터베이스를 만든 다음 표에 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="2afe9-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2afe9-252">Next steps</span></span>
<span data-ttu-id="2afe9-253">이 문서에서는 CentOS 7을 실행하는 Azure 가상 컴퓨터에 3개 노드 MariaDB + Galera 고가용성 클러스터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="2afe9-254">hello Vm Azure 부하 분산 장치와 부하가 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="2afe9-255">toolook 할 수 있습니다 [또 다른 방법은 toocluster Linux에서 MySQL](mysql-cluster.md) 방법 너무[최적화 하 고 Azure Linux Vm에서 MySQL 성능 테스트](optimize-mysql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2afe9-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[인증을 위해 SSH 키를 만들려면]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
