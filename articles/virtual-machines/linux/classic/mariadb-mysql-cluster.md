---
title: "Azure에서 MariaDB(MySQL) 클러스터 실행 | Microsoft Docs"
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
ms.openlocfilehash: 53e9bf18b26338212411ea7c4f260eb308486738
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="e5d3e-103">MariaDB(MySQL) 클러스터: Azure 자습서</span><span class="sxs-lookup"><span data-stu-id="e5d3e-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e5d3e-104">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="e5d3e-105">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-105">This article covers the classic deployment model.</span></span> <span data-ttu-id="e5d3e-106">대부분의 새로운 배포에서는 Azure Resource Manager 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-106">Microsoft recommends that most new deployments use the Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="e5d3e-107">Azure 마켓플레이스에 MariaDB 엔터프라이즈 클러스터가 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-107">MariaDB Enterprise cluster is now available in the Azure Marketplace.</span></span> <span data-ttu-id="e5d3e-108">새로운 이 서비스는 Azure Resource Manager에 MariaDB Galera 클러스터를 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-108">The new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="e5d3e-109">[Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/)에서 이 서비스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-109">You should use the new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="e5d3e-110">이 문서에서는 Azure 가상 컴퓨터의 고가용성 환경에서 작업할 수 있도록 강력하고, 확장성과 안정성이 뛰어나며, 예약할 필요가 없는 MySQL 대체 도구인 [MariaDB](https://mariadb.org/en/about/)의 다중 마스터 [Galera](http://galeracluster.com/products/) 클러스터를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-110">This article shows you how to create a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) to work in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="e5d3e-111">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="e5d3e-111">Architecture overview</span></span>
<span data-ttu-id="e5d3e-112">이 항목에서는 다음 단계를 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-112">This article describes how to complete the following steps:</span></span>

- <span data-ttu-id="e5d3e-113">3개 노드 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="e5d3e-114">OS 디스크에서 데이터 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-114">Separate the data disks from the OS disk.</span></span>
- <span data-ttu-id="e5d3e-115">RAID-0/스트라이프 설정으로 데이터 디스크를 만들어 IOPS를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-115">Create the data disks in RAID-0/striped setting to increase IOPS.</span></span>
- <span data-ttu-id="e5d3e-116">Azure Load Balancer를 사용하여 3개 노드의 부하를 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-116">Use Azure Load Balancer to balance the load for the three nodes.</span></span>
- <span data-ttu-id="e5d3e-117">반복 작업을 최소화하기 위해 MariaDB+Galera가 포함된 VM 이미지를 만들고 이 이미지를 사용하여 다른 클러스터 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-117">To minimize repetitive work, create a VM image that contains MariaDB + Galera and use it to create the other cluster VMs.</span></span>

![시스템 아키텍처](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="e5d3e-119">이 항목에서는 [Azure CLI](../../../cli-install-nodejs.md) 도구를 사용하므로 도구를 다운로드하고 지침에 따라 Azure 구독에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-119">This topic uses the [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure to download them and connect them to your Azure subscription according to the instructions.</span></span> <span data-ttu-id="e5d3e-120">Azure CLI에서 사용할 수 있는 명령에 대한 참조가 필요하면 [Azure CLI 명령 참조](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-120">If you need a reference to the commands available in the Azure CLI, see the [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="e5d3e-121">또한 [인증에 사용할 SSH 키를 만들고] pem 파일 위치를 적어 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-121">You will also need to [create an SSH key for authentication] and make note of the .pem file location.</span></span>
>
>

## <a name="create-the-template"></a><span data-ttu-id="e5d3e-122">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="e5d3e-122">Create the template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="e5d3e-123">인프라</span><span class="sxs-lookup"><span data-stu-id="e5d3e-123">Infrastructure</span></span>
1. <span data-ttu-id="e5d3e-124">리소스를 포함할 선호도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-124">Create an affinity group to hold the resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="e5d3e-125">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="e5d3e-126">모든 디스크를 호스팅할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-126">Create a storage account to host all our disks.</span></span> <span data-ttu-id="e5d3e-127">20,000 IOPS 저장소 계정 한도를 초과하지 않도록 동일한 저장소 계정에 자주 사용되는 디스크를 40개 이상 배치하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-127">You shouldn't place more than 40 heavily used disks on the same storage account to avoid hitting the 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="e5d3e-128">여기서는 한도보다 훨씬 작으므로 간단하게 동일한 계정에 모든 것을 저장하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-128">In this case, you're well below that limit, so you'll store everything on the same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="e5d3e-129">CentOS 7 가상 컴퓨터 이미지의 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-129">Find the name of the CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="e5d3e-130">출력은 `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-130">The output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="e5d3e-131">다음 단계에서 해당 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-131">Use that name in the following step.</span></span>
5. <span data-ttu-id="e5d3e-132">VM 템플릿을 만들고 생성된 .pem SSH 키를 저장한 경로로 /path/to/key.pem을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-132">Create the VM template and replace /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="e5d3e-133">RAID 구성에서 사용할 VM에 4개의 500GB 데이터 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-133">Attach four 500-GB data disks to the VM for use in the RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="e5d3e-134">SSH를 사용하여 mariadbhatemplate.cloudapp.net:22에서 만든 템플릿 VM에 로그인하고 개인 키를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-134">Use SSH to sign in to the template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="e5d3e-135">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="e5d3e-135">Software</span></span>
1. <span data-ttu-id="e5d3e-136">루트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-136">Get the root.</span></span>

        sudo su

2. <span data-ttu-id="e5d3e-137">RAID 지원을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-137">Install RAID support:</span></span>

    <span data-ttu-id="e5d3e-138">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-138">a.</span></span> <span data-ttu-id="e5d3e-139">mdadm을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="e5d3e-140">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-140">b.</span></span> <span data-ttu-id="e5d3e-141">EXT4 파일 시스템으로 RAID0/스트라이프 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-141">Create the RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="e5d3e-142">c.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-142">c.</span></span> <span data-ttu-id="e5d3e-143">탑재 지점 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-143">Create the mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="e5d3e-144">d.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-144">d.</span></span> <span data-ttu-id="e5d3e-145">새로 만든 RAID 장치의 UUID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-145">Retrieve the UUID of the newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="e5d3e-146">e.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-146">e.</span></span> <span data-ttu-id="e5d3e-147">/etc/fstab을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="e5d3e-148">f.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-148">f.</span></span> <span data-ttu-id="e5d3e-149">UUID를 이전 **blkid** 명령에서 가져온 값으로 바꾸고, 장치를 추가하여 재부팅할 때 자동 탑재를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-149">Add the device to enable auto mounting on reboot, replacing the UUID with the value obtained from the previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="e5d3e-150">g.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-150">g.</span></span> <span data-ttu-id="e5d3e-151">새 파티션을 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-151">Mount the new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="e5d3e-152">MariaDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-152">Install MariaDB.</span></span>

    <span data-ttu-id="e5d3e-153">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-153">a.</span></span> <span data-ttu-id="e5d3e-154">MariaDB.repo 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-154">Create the MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="e5d3e-155">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-155">b.</span></span> <span data-ttu-id="e5d3e-156">repo 파일을 다음 내용으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-156">Fill the repo file with the following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="e5d3e-157">c.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-157">c.</span></span> <span data-ttu-id="e5d3e-158">충돌을 방지하기 위해 기존 접미사와 mariadb-lib를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-158">To avoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="e5d3e-159">d.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-159">d.</span></span> <span data-ttu-id="e5d3e-160">Galera와 함께 MariaDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="e5d3e-161">MySQL 데이터 디렉터리를 RAID 블록 장치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-161">Move the MySQL data directory to the RAID block device.</span></span>

    <span data-ttu-id="e5d3e-162">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-162">a.</span></span> <span data-ttu-id="e5d3e-163">현재 MySQL 디렉터리를 새 위치에 복사하고 이전 디렉터리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-163">Copy the current MySQL directory into its new location and remove the old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="e5d3e-164">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-164">b.</span></span> <span data-ttu-id="e5d3e-165">이에 따라 새 디렉터리에 대한 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-165">Set permissions for the new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="e5d3e-166">c.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-166">c.</span></span> <span data-ttu-id="e5d3e-167">이전 디렉터리를 RAID 파티션의 새 위치로 가리키는 symlink를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-167">Create a symlink that points the old directory to the new location on the RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="e5d3e-168">[SELinux는 클러스터 작업을 방해](http://galeracluster.com/documentation-webpages/configuration.html#selinux)하기 때문에 현재 세션에서 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-168">Because [SELinux interferes with the cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary to disable it for the current session.</span></span> <span data-ttu-id="e5d3e-169">`/etc/selinux/config`를 편집하여 이후의 다시 시작에서 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-169">Edit `/etc/selinux/config` to disable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` to set `SELINUX=permissive`
6. <span data-ttu-id="e5d3e-170">MySQL 실행의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="e5d3e-171">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-171">a.</span></span> <span data-ttu-id="e5d3e-172">MySQL을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="e5d3e-173">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-173">b.</span></span> <span data-ttu-id="e5d3e-174">MySQL 설치 보안을 유지하고, 루트 암호를 설정하며, 익명 사용자를 제거하여 원격 루트 로그인을 사용하지 않도록 설정하고, 테스트 데이터베이스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-174">Secure the MySQL installation, set the root password, remove anonymous users to disable remote root login, and remove the test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="e5d3e-175">c.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-175">c.</span></span> <span data-ttu-id="e5d3e-176">클러스터 작업 및 선택적으로 응용 프로그램을 위해 데이터베이스에 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-176">Create a user on the database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* TO 'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="e5d3e-177">d.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-177">d.</span></span> <span data-ttu-id="e5d3e-178">MySQL을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="e5d3e-179">구성 자리 표시자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="e5d3e-180">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-180">a.</span></span> <span data-ttu-id="e5d3e-181">MySQL 구성을 편집하여 클러스터 설정에 대한 자리 표시자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-181">Edit the MySQL configuration to create a placeholder for the cluster settings.</span></span> <span data-ttu-id="e5d3e-182">지금은 **`<Variables>`** 를 바꾸거나 주석을 제거하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-182">Do not replace the **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="e5d3e-183">이 템플릿에서 VM을 만든 후에 그렇게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="e5d3e-184">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-184">b.</span></span> <span data-ttu-id="e5d3e-185">**[galera]** 섹션을 편집하여 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-185">Edit the **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="e5d3e-186">c.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-186">c.</span></span> <span data-ttu-id="e5d3e-187">**[mariadb]** 섹션을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-187">Edit the **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set to 0.0.0.0, the server listens to remote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for the SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set the node name of this server
8. <span data-ttu-id="e5d3e-188">CentOS 7에서 FirewallD를 사용하여 방화벽에서 필요한 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-188">Open required ports on the firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="e5d3e-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e5d3e-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="e5d3e-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e5d3e-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="e5d3e-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e5d3e-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="e5d3e-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e5d3e-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="e5d3e-193">방화벽 다시 로드: `firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="e5d3e-193">Reload the firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="e5d3e-194">성능에 대해 시스템을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-194">Optimize the system for performance.</span></span> <span data-ttu-id="e5d3e-195">자세한 내용은 [성능 조정 전략](optimize-mysql.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="e5d3e-196">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-196">a.</span></span> <span data-ttu-id="e5d3e-197">MySQL 구성 파일을 다시 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-197">Edit the MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="e5d3e-198">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-198">b.</span></span> <span data-ttu-id="e5d3e-199">**[mariadb]** 섹션을 편집하고 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-199">Edit the **[mariadb]** section and append the following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5d3e-200">innodb\_buffer\_pool_size를 VM 메모리의 70%로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="e5d3e-201">이 예제에서는 3.5GB RAM을 갖춘 중간 Azure VM에 대해 2.45GB로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-201">In this example, it has been set at 2.45 GB for the medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # The buffer pool contains buffered data and the index. This is usually set to 70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give the server more time to recycle idled connections
           innodb_file_per_table = 1 # Speed up the table space transmission and optimize the debris management performance
           innodb_log_buffer_size = 128M # The log buffer allows transactions to run without having to flush the log to disk before the transactions commit
           innodb_flush_log_at_trx_commit = 2 # The setting of 2 enables the most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="e5d3e-202">MySQL을 중지하고, 시작할 때 MySQL 서비스가 실행되지 않도록 설정하여 노드를 추가할 때 클러스터가 중단되지 않게 하고, 컴퓨터 프로비전을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-202">Stop MySQL, disable MySQL service from running on startup to avoid disrupting the cluster when adding a node, and deprovision the machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="e5d3e-203">포털을 통해 VM을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-203">Capture the VM through the portal.</span></span> <span data-ttu-id="e5d3e-204">(현재 [Azure CLI 도구 문제 #1268](https://github.com/Azure/azure-xplat-cli/issues/1268)(영문)에서는 Azure CLI 도구로 캡처한 이미지가 연결된 데이터 디스크를 캡처하지 않는다는 사실을 설명하고 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e5d3e-204">(Currently, [issue #1268 in the Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes the fact that images captured by the Azure CLI tools do not capture the attached data disks.)</span></span>

    <span data-ttu-id="e5d3e-205">a.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-205">a.</span></span> <span data-ttu-id="e5d3e-206">포털을 통해 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-206">Shut down the machine through the portal.</span></span>

    <span data-ttu-id="e5d3e-207">b.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-207">b.</span></span> <span data-ttu-id="e5d3e-208">**캡처**를 클릭하고 이미지 이름을 **mariadb-galera-image**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-208">Click **Capture** and specify the image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="e5d3e-209">설명을 입력하고 "waagent를 실행했습니다." 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-209">Provide a description and check "I have run waagent."</span></span>
      
      ![가상 컴퓨터 캡처](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-the-cluster"></a><span data-ttu-id="e5d3e-211">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e5d3e-211">Create the cluster</span></span>
<span data-ttu-id="e5d3e-212">만든 템플릿으로 세 개의 VM을 만든 다음 클러스터를 구성하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-212">Create three VMs with the template you created, and then configure and start the cluster.</span></span>

1. <span data-ttu-id="e5d3e-213">만든 mariadb-galera-image 이미지에서 첫 번째 CentOS 7 VM을 만들고 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-213">Create the first CentOS 7 VM from the mariadb-galera-image image you created, providing the following information:</span></span>

 - <span data-ttu-id="e5d3e-214">가상 네트워크 이름: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="e5d3e-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="e5d3e-215">서브넷: mariadb</span><span class="sxs-lookup"><span data-stu-id="e5d3e-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="e5d3e-216">컴퓨터 크기: medium</span><span class="sxs-lookup"><span data-stu-id="e5d3e-216">Machine size: medium</span></span>
 - <span data-ttu-id="e5d3e-217">클라우드 서비스 이름: mariadbha(또는 mariadbha.cloudapp.net을 통해 액세스하려는 이름)</span><span class="sxs-lookup"><span data-stu-id="e5d3e-217">Cloud service name: mariadbha (or whatever name you want to be accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="e5d3e-218">컴퓨터 이름: mariadb1</span><span class="sxs-lookup"><span data-stu-id="e5d3e-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="e5d3e-219">사용자 이름: azureuser</span><span class="sxs-lookup"><span data-stu-id="e5d3e-219">Username: azureuser</span></span>
 - <span data-ttu-id="e5d3e-220">SSH 액세스: enabled</span><span class="sxs-lookup"><span data-stu-id="e5d3e-220">SSH access: enabled</span></span>
 - <span data-ttu-id="e5d3e-221">SSH 인증서 .pem 파일을 전달하고 생성된 .pem SSH 키를 저장한 경로로 /path/to/key.pem을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-221">Passing the SSH certificate .pem file and replacing /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5d3e-222">다음 명령은 명확하게 나타내기 위해 여러 줄로 나누어져 있지만 각각 한 줄로 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-222">The following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="e5d3e-223">mariadbha 클라우드 서비스에 연결하여 두 개의 가상 컴퓨터를 추가로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-223">Create two more virtual machines by connecting them to the mariadbha cloud service.</span></span> <span data-ttu-id="e5d3e-224">VM 이름과 SSH 포트를 동일한 클라우드 서비스의 다른 VM과 충돌하지 않는 고유한 포트로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-224">Change the VM name and the SSH port to a unique port not conflicting with other VMs in the same cloud service.</span></span>

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
  <span data-ttu-id="e5d3e-225">MariaDB3의 경우:</span><span class="sxs-lookup"><span data-stu-id="e5d3e-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="e5d3e-226">다음 단계를 위해 세 개 VM 각각의 내부 IP 주소를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-226">You will need to get the internal IP address of each of the three VMs for the next step:</span></span>

    ![IP 주소 가져오기](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="e5d3e-228">SSH를 사용하여 세 개 VM에 로그인하고 각각의 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-228">Use SSH to sign in to the three VMs and edit the configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="e5d3e-229">줄의 시작 부분에서 **#**을 제거하여 **`wsrep_cluster_name`** 및 **`wsrep_cluster_address`**의 주석을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing the **#** at the beginning of the line.</span></span>
    <span data-ttu-id="e5d3e-230">또한 **`wsrep_node_address`**의 **`<ServerIP>`** 및 **`wsrep_node_name`**의 **`<NodeName>`**을 각각 VM의 IP 주소와 이름으로 바꾸고 해당 줄의 주석도 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with the VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="e5d3e-231">MariaDB1에서 클러스터를 시작하고 시작 시 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-231">Start the cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="e5d3e-232">MariaDB2 및 MariaDB3에서 MySQL을 시작하고 시작 시 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-the-cluster"></a><span data-ttu-id="e5d3e-233">클러스터 부하 분산</span><span class="sxs-lookup"><span data-stu-id="e5d3e-233">Load balance the cluster</span></span>
<span data-ttu-id="e5d3e-234">클러스터된 VM을 만들 때 해당 VM을 ‘clusteravset’라는 가용성 집합에 추가하여 다른 장애 도메인 및 업데이트 도메인에 배치하도록 했으며 Azure를 통해 모든 컴퓨터에서 유지 관리를 동시에 수행하지 않도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-234">When you created the clustered VMs, you added them into an availability set called clusteravset to ensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="e5d3e-235">이 구성은 Azure SLA(서비스 수준 약정)에서 지원해야 하는 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-235">This configuration meets the requirements to be supported by the Azure service level agreement (SLA).</span></span>

<span data-ttu-id="e5d3e-236">이제 Azure Load Balancer를 사용하여 3개 노드 간에 요청을 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-236">Now use Azure Load Balancer to balance requests between the three nodes.</span></span>

<span data-ttu-id="e5d3e-237">Azure CLI를 사용하여 컴퓨터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-237">Run the following commands on your machine by using the Azure CLI.</span></span>

<span data-ttu-id="e5d3e-238">명령 매개 변수 구조는 다음과 같습니다. `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="e5d3e-238">The command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="e5d3e-239">CLI에서 부하 분산 장치 프로브 간격을 15초로 설정합니다. 이 간격이 너무 길 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-239">The CLI sets the load balancer probe interval to 15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="e5d3e-240">VM 중 하나에 대한 **끝점**의 포털에서 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-240">Change it in the portal under **Endpoints** for any of the VMs.</span></span>

![끝점 편집](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="e5d3e-242">**부하 분산 집합 다시 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-242">Select **Reconfigure the Load-Balanced Set**.</span></span>

![부하 분산 집합 다시 구성](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="e5d3e-244">**프로브 간격**을 5초로 변경하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-244">Change **Probe Interval** to 5 seconds and save your changes.</span></span>

![프로브 간격 변경](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-the-cluster"></a><span data-ttu-id="e5d3e-246">클러스터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e5d3e-246">Validate the cluster</span></span>
<span data-ttu-id="e5d3e-247">하드 작업이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-247">The hard work is done.</span></span> <span data-ttu-id="e5d3e-248">클러스터는 이제 `mariadbha.cloudapp.net:3306`에서 액세스할 수 있어야 합니다. 여기서는 부하 분산 장치를 실행하여 세 VM 간의 요청을 원활하고 효율적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-248">The cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits the load balancer and route requests between the three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="e5d3e-249">원하는 MySQL 클라이언트를 사용하여 VM 중 하나에 연결하거나 연결을 끊어 해당 클러스터가 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-249">Use your favorite MySQL client to connect, or connect from one of the VMs to verify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="e5d3e-250">그런 다음 데이터베이스를 만들고 일부 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="e5d3e-251">만든 데이터베이스는 다음 테이블을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-251">The database you created returns the following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="e5d3e-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5d3e-252">Next steps</span></span>
<span data-ttu-id="e5d3e-253">이 문서에서는 CentOS 7을 실행하는 Azure 가상 컴퓨터에 3개 노드 MariaDB + Galera 고가용성 클러스터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="e5d3e-254">VM에서 Azure Load Balancer를 사용하여 부하를 분산했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-254">The VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="e5d3e-255">[Linux에서 MySQL을 클러스터링하는 다른 방법](mysql-cluster.md) 및 [Azure Linux VM에서 MySQL 성능 최적화 및 테스트](optimize-mysql.md)하는 방법을 살펴보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d3e-255">You might want to look at [another way to cluster MySQL on Linux](mysql-cluster.md) and ways to [optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating the template]:#creating-the-template
[Creating the cluster]:#creating-the-cluster
[Load balancing the cluster]:#load-balancing-the-cluster
[Validating the cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
<span data-ttu-id="e5d3e-256">[Galera]:http://galeracluster.com/products/</span><span class="sxs-lookup"><span data-stu-id="e5d3e-256">[Galera]:http://galeracluster.com/products/</span></span>
[MariaDBs]:https://mariadb.org/en/about/
<span data-ttu-id="e5d3e-257">[인증에 사용할 SSH 키를 만들고]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span><span class="sxs-lookup"><span data-stu-id="e5d3e-257">[create an SSH key for authentication]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span></span>
[issue #1268 in the Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
