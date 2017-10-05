---
title: "Azure Linux 가상 컴퓨터에 Oracle ASM 설정 | Microsoft Docs"
description: "Azure 환경에서 Oracle ASM을 빠르게 준비하여 실행합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: 117212a2e7e3da7c3e249798eec804a652e0ef58
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="00d9e-103">Azure Linux 가상 컴퓨터에 Oracle ASM 설정</span><span class="sxs-lookup"><span data-stu-id="00d9e-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="00d9e-104">Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="00d9e-105">이 자습서에서는 Oracle ASM(Automated Storage Management) 설치 및 구성과 결합된 기본 Azure 가상 컴퓨터 배포에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-105">This tutorial covers basic Azure virtual machine deployment combined with the installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="00d9e-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00d9e-107">Oracle 데이터베이스 VM 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="00d9e-107">Create and connect to an Oracle Database VM</span></span>
> * <span data-ttu-id="00d9e-108">Oracle Automated Storage Management 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="00d9e-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="00d9e-109">Oracle Grid 인프라 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="00d9e-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="00d9e-110">Oracle ASM 설치 초기화</span><span class="sxs-lookup"><span data-stu-id="00d9e-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="00d9e-111">ASM에서 관리하는 Oracle DB 만들기</span><span class="sxs-lookup"><span data-stu-id="00d9e-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="00d9e-112">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="00d9e-113">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="00d9e-114">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00d9e-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-the-environment"></a><span data-ttu-id="00d9e-115">환경 준비</span><span class="sxs-lookup"><span data-stu-id="00d9e-115">Prepare the environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="00d9e-116">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="00d9e-116">Create a resource group</span></span>

<span data-ttu-id="00d9e-117">리소스 그룹을 만들려면 [az group create](/cli/azure/group#create) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-117">To create a resource group, use the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="00d9e-118">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="00d9e-119">이 예제에서는 *eastus* 지역에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-119">In this example, a resource group named *myResourceGroup* in the *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="00d9e-120">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="00d9e-120">Create a VM</span></span>

<span data-ttu-id="00d9e-121">Oracle Database 이미지에 따라 가상 컴퓨터를 만들고 Oracle ASM을 사용하도록 구성하려면 [az vm create](/cli/azure/vm#create) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-121">To create a virtual machine based on the Oracle Database image and configure it to use Oracle ASM, use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="00d9e-122">다음 예에서는 각 50GB인 네 개의 연결된 데이터 디스크를 포함한 Standard_DS2_v2 크기의 myVM이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-122">The following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="00d9e-123">또한 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-123">If they do not already exist in the default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="00d9e-124">특정 키 집합을 사용하려면 `--ssh-key-value` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-124">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="00d9e-125">VM을 만든 후 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-125">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="00d9e-126">`publicIpAddress`에 대한 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-126">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="00d9e-127">이 주소는 VM에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-127">You use this address to access the VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-to-the-vm"></a><span data-ttu-id="00d9e-128">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="00d9e-128">Connect to the VM</span></span>

<span data-ttu-id="00d9e-129">VM으로 SSH 세션을 만들고 추가 설정을 구성하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-129">To create an SSH session with the VM and configure additional settings, use the following command.</span></span> <span data-ttu-id="00d9e-130">해당 IP 주소를 VM의 `publicIpAddress` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-130">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="00d9e-131">Oracle ASM 설치</span><span class="sxs-lookup"><span data-stu-id="00d9e-131">Install Oracle ASM</span></span>

<span data-ttu-id="00d9e-132">Oracle ASM을 설치하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-132">To install Oracle ASM, complete the following steps.</span></span> 

<span data-ttu-id="00d9e-133">Oracle ASM 설치에 대한 자세한 내용은 [Oracle Linux 6에 대한 Oracle ASMLib 다운로드](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00d9e-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="00d9e-134">ASM 설치를 계속하기 위해 루트로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-134">You need to login as root in order to continue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="00d9e-135">Oracle ASM 구성 요소를 설치하기 위해 이러한 추가 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-135">Run these additional commands to install Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="00d9e-136">Oracle ASM이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="00d9e-137">이 명령의 출력은 다음 구성 요소를 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-137">The output of this command should list the following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="00d9e-138">ASM이 제대로 작동하기 위해 특정 사용자 및 역할이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-138">ASM requires specific users and roles in order to function correctly.</span></span> <span data-ttu-id="00d9e-139">다음 명령은 필수 구성 요소 사용자 계정 및 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-139">The following commands create the pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="00d9e-140">사용자 및 그룹이 올바르게 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="00d9e-141">이 명령의 출력은 다음과 같은 사용자 및 그룹을 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-141">The output of this command should list the following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="00d9e-142">*grid* 사용자를 위한 폴더를 만들고 소유자를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-142">Create a folder for user *grid* and change the owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="00d9e-143">Oracle ASM 설정</span><span class="sxs-lookup"><span data-stu-id="00d9e-143">Set up Oracle ASM</span></span>

<span data-ttu-id="00d9e-144">이 자습서에서는 기본 사용자가 *grid*이며, 기본 그룹은 *asmadmin*입니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-144">For this tutorial, the default user is *grid* and the default group is *asmadmin*.</span></span> <span data-ttu-id="00d9e-145">*oracle* 사용자가 asmadmin 그룹의 구성원인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-145">Ensure that the *oracle* user is part of the asmadmin group.</span></span> <span data-ttu-id="00d9e-146">Oracle ASM 설치를 설정하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-146">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="00d9e-147">Oracle ASM 라이브러리 드라이버를 설정하는 작업에는 드라이브를 부팅하기 시작(y 선택)하고 부팅 시 디스크를 검색(y 선택)하도록 구성할 뿐만 아니라 기본 사용자(그리드) 및 기본 그룹(asmadmin)을 정의하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-147">Setting up the Oracle ASM library driver involves defining the default user (grid) and default group (asmadmin) as well as configuring the drive to start on boot (choose y) and to scan for disks on boot (choose y).</span></span> <span data-ttu-id="00d9e-148">다음 명령에서 표시되는 메시지에 답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-148">You need to answer the prompts from the following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="00d9e-149">이 명령의 출력은 다음 출력과 유사해야 하며 표시되는 메시지에 답하면 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-149">The output of this command should look similar to the following, stopping with prompts to be answered.</span></span>

    ```bash
   Configuring the Oracle ASM library driver.

   This will configure the on-boot properties of the Oracle ASM library
   driver. The following questions will determine whether the driver is
   loaded on boot and what permissions it will have. The current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user to own the driver interface []: grid
   Default group to own the driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="00d9e-150">디스크 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-150">View the disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="00d9e-151">이 명령의 출력은 다음 사용 가능한 디스크 목록과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-151">The output of this command should look similar to the following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="00d9e-152">다음 명령을 실행하고 표시되는 메시지에 답하여 */dev/sdc* 디스크를 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-152">Format disk */dev/sdc* by running the following command and answering the prompts with:</span></span>
   - <span data-ttu-id="00d9e-153">새 파티션의 경우 *n*</span><span class="sxs-lookup"><span data-stu-id="00d9e-153">*n* for new partition</span></span>
   - <span data-ttu-id="00d9e-154">주 파티션의 경우 *p*</span><span class="sxs-lookup"><span data-stu-id="00d9e-154">*p* for primary partition</span></span>
   - <span data-ttu-id="00d9e-155">첫 번째 파티션을 선택하려면 *1*</span><span class="sxs-lookup"><span data-stu-id="00d9e-155">*1* to select the first partition</span></span>
   - <span data-ttu-id="00d9e-156">첫 번째 기본 실린더의 경우 `enter` 키를 누름</span><span class="sxs-lookup"><span data-stu-id="00d9e-156">press `enter` for the default first cylinder</span></span>
   - <span data-ttu-id="00d9e-157">최근 기본 실린더의 경우 `enter` 키를 누름</span><span class="sxs-lookup"><span data-stu-id="00d9e-157">press `enter` for the default last cylinder</span></span>
   - <span data-ttu-id="00d9e-158">파티션 테이블에 변경 내용을 쓰려면 *w* 키를 누름</span><span class="sxs-lookup"><span data-stu-id="00d9e-158">press *w* to write the changes to the partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="00d9e-159">fdisk 명령에 대한 출력은 위에 제공된 답변을 사용하여 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-159">Using the answers provided above, the output for the fdisk command should look like the following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide to write them.
   After that, of course, the previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   The device presents a logical sector size that is smaller than
   the physical sector size. Aligning to a physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off the mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   The partition table has been altered!

   Calling ioctl() to re-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="00d9e-160">`/dev/sdd`, `/dev/sde` 및 `/dev/sdf`의 경우 위의 fdisk 명령을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-160">Repeat the preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="00d9e-161">디스크 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-161">Check the disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="00d9e-162">명령 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-162">The output of the command should look like the following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="00d9e-163">Oracle ASM 서비스 상태를 확인하고 Oracle ASM 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-163">Check the Oracle ASM service status and start the Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="00d9e-164">명령 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-164">The output of the command should look like the following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing the Oracle ASMLib driver:                     [  OK  ]
   Scanning the system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="00d9e-165">Oracle ASM 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="00d9e-166">명령 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-166">The output of the command should look like the following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="00d9e-167">Oracle ASM 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="00d9e-168">이 명령의 출력은 다음 Oracle ASM 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-168">The output of the command should list off the following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="00d9e-169">루트, oracle 및 그리드 사용자에 대한 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-169">Change the passwords for the root, oracle, and grid users.</span></span> <span data-ttu-id="00d9e-170">나중에 설치하는 동안 사용하도록 **이러한 새 암호를 기록**합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-170">**Make note of these new passwords** as you are using them later during the installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="00d9e-171">폴더 사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-171">Change the folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="00d9e-172">Oracle Grid Infrastructure 다운로드 및 준비</span><span class="sxs-lookup"><span data-stu-id="00d9e-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="00d9e-173">Oracle Grid Infrastructure 소프트웨어를 다운로드 및 준비하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-173">To download and prepare the Oracle Grid Infrastructure software, complete the following steps:</span></span>

1. <span data-ttu-id="00d9e-174">[Oracle ASM 다운로드 페이지](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html)에서 Oracle Grid Infrastructure를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-174">Download Oracle Grid Infrastructure from the [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="00d9e-175">다운로드 제목 **Linux x86-64용 Oracle Database 12c 릴리스 1 Grid Infrastructure(12.1.0.2.0)**에서 두 개의 .zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-175">Under the download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download the two .zip files.</span></span>

2. <span data-ttu-id="00d9e-176">클라이언트 컴퓨터에 .zip 파일을 다운로드한 후 SCP(보안 복사 프로토콜)를 사용하여 파일을 VM에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-176">After you download the .zip files to your client computer, you can use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="00d9e-177">.zip 파일을 /opt 폴더로 이동하기 위해 Azure에서 Oracle VM에 다시 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-177">SSH back into your Oracle VM in Azure in order to move the .zip files into the /opt folder.</span></span> <span data-ttu-id="00d9e-178">그런 다음 파일의 소유자를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-178">Then, change the owner of the files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="00d9e-179">파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-179">Unzip the files.</span></span> <span data-ttu-id="00d9e-180">(Linux 압축 풀기 도구가 설치되어 있지 않은 경우 이를 설치합니다.)</span><span class="sxs-lookup"><span data-stu-id="00d9e-180">(Install the Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="00d9e-181">사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="00d9e-182">구성된 스왑 공간을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-182">Update configured swap space.</span></span> <span data-ttu-id="00d9e-183">Oracle Grid 구성 요소에서 Grid를 설치하려면 적어도 6.8GB의 스왑 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-183">Oracle Grid components need at least 6.8 GB of swap space to install Grid.</span></span> <span data-ttu-id="00d9e-184">Azure에서 Oracle Linux 이미지에 대한 기본 스왑 파일 크기는 2048MB입니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-184">The default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="00d9e-185">업데이트된 설정을 적용하기 위해 `/etc/waagent.conf` 파일에서 `ResourceDisk.SwapSizeMB`를 늘리고 WALinuxAgent 서비스를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-185">You need to increase `ResourceDisk.SwapSizeMB` in the `/etc/waagent.conf` file and restart the WALinuxAgent service in order for the updated settings to take effect.</span></span> <span data-ttu-id="00d9e-186">읽기 전용 파일이기 때문에 쓰기 액세스를 사용할 수 있도록 파일 사용 권한을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-186">Because it is a read-only file, you need to change file permissions to enable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="00d9e-187">`ResourceDisk.SwapSizeMB`를 검색하고 값을 **8192**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-187">Search for `ResourceDisk.SwapSizeMB` and change the value to **8192**.</span></span> <span data-ttu-id="00d9e-188">`insert`를 눌러 삽입 모드를 입력하고 **8192** 값을 입력한 다음 `esc` 키를 눌러 명령 모드로 돌아가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-188">You will need to press `insert` to enter insert mode, type in the value of **8192** and then press `esc` to return to command mode.</span></span> <span data-ttu-id="00d9e-189">변경 내용을 쓰고 파일을 종료하려면 `:wq`를 입력하고 `enter` 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-189">To write the changes and quit the file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="00d9e-190">성능을 최대화하기 위해 스왑 공간이 항상 로컬 사용 후 삭제 디스크(임시 디스크)에 만들어지도록 `WALinuxAgent`를 사용하여 스왑 공간을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-190">We highly recommend that you always use `WALinuxAgent` to configure swap space so that it's always created on the local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="00d9e-191">자세한 내용은 [Linux Azure Virtual Machines에 스왑 파일을 추가하는 방법](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-191">For more information on, see [How to add a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-to-run-x11"></a><span data-ttu-id="00d9e-192">로컬 클라이언트와 VM에서 X11 실행 준비</span><span class="sxs-lookup"><span data-stu-id="00d9e-192">Prepare your local client and VM to run x11</span></span>
<span data-ttu-id="00d9e-193">Oracle ASM를 구성하려면 설치 및 구성을 완료할 그래픽 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-193">Configuring Oracle ASM requires a graphical interface to complete the install and configuration.</span></span> <span data-ttu-id="00d9e-194">X11 프로토콜을 사용하여 이 설치를 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-194">We are using the x11 protocol to facilitate this installation.</span></span> <span data-ttu-id="00d9e-195">X11 기능을 사용하도록 설정하고 구성한 클라이언트 시스템(Mac 또는 Linux)을 사용하는 경우 Windows 컴퓨터에만 독점적인 이 구성 및 설정을 건너뛰어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive to Windows machines.</span></span> 

1. <span data-ttu-id="00d9e-196">Windows 컴퓨터에 [PuTTY를 다운로드](http://www.putty.org/)하고 [Xming](https://xming.en.softonic.com/)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) to your Windows computer.</span></span> <span data-ttu-id="00d9e-197">계속하기 전에 기본 값으로 이러한 응용 프로그램의 설치를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-197">You will need to complete the installation of both of these applications with the default values before proceeding.</span></span>

2. <span data-ttu-id="00d9e-198">PuTTY를 설치한 후에 명령 프롬프트를 열고, PuTTY 폴더(예: C:\Program Files\PuTTY)로 변경하고 키를 생성하기 위해 `puttygen.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-198">After you install PuTTY, open a command prompt, change into the PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order to generate a key.</span></span>

3. <span data-ttu-id="00d9e-199">PuTTY 키 생성기에서,</span><span class="sxs-lookup"><span data-stu-id="00d9e-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="00d9e-200">`Generate` 단추를 선택하여 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-200">Generate a key by selecting the `Generate` button.</span></span>
   2. <span data-ttu-id="00d9e-201">키의 콘텐츠를 복사(Ctrl + C)합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-201">Copy the contents of the key (Ctrl+C).</span></span>
   3. <span data-ttu-id="00d9e-202">`Save private key` 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-202">Select the `Save private key` button.</span></span>
   4. <span data-ttu-id="00d9e-203">암호를 사용하여 키를 보호하는 방법에 대한 경고를 무시한 다음 `OK`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-203">Ignore the warning about securing the key with a passphrase, and then select `OK`.</span></span>

   ![PuTTY 키 생성기의 스크린샷](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="00d9e-205">VM에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="00d9e-206">`authorized_keys`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="00d9e-207">키의 콘텐츠를 이 파일에 붙여넣은 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-207">Paste the contents of the key in this file, and then save the file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="00d9e-208">키에는 문자열 `ssh-rsa`가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-208">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="00d9e-209">또한 키의 콘텐츠는 한 줄 텍스트여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-209">Also, the contents of the key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="00d9e-210">클라이언트 컴퓨터에서 PuTTY를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="00d9e-211">**카테고리** 창에서 **연결** > **SSH** > **인증**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-211">In the **Category** pane, go to **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="00d9e-212">**인증에 대한 개인 키 파일** 상자에서 이전에 생성한 키를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-212">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

   ![SSH 인증 옵션의 스크린샷](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="00d9e-214">**카테고리** 창에서 **연결** > **SSH** > **X11**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-214">In the **Category** pane, go to **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="00d9e-215">**X11 전달을 사용하도록 설정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-215">Select the **Enable X11 forwarding** check box.</span></span>

   ![SSH X11 전달 옵션의 스크린샷](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="00d9e-217">**카테고리** 창에서 **세션**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-217">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="00d9e-218">호스트 이름 대화 상자에서 Oracle ASM VM `<publicIPaddress>`를 입력하고 새 `Saved Session` 이름을 채운 다음 `Save`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-218">Enter your Oracle ASM VM `<publicIPaddress>` in the host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="00d9e-219">저장하면 `open`를 클릭하여 Oracle ASM 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-219">Once saved, click on `open` to connect to your Oracle ASM virtual machine.</span></span>  <span data-ttu-id="00d9e-220">처음 연결하면 원격 시스템이 레지스트리에서 캐시되지 않는다는 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-220">The first time you connect you are warned  the remote system is not cached in your registry.</span></span> <span data-ttu-id="00d9e-221">`yes`를 클릭하고 계속 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-221">Click on `yes` to add it and continue.</span></span>

   ![PuTTY 세션 옵션의 스크린샷](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="00d9e-223">Oracle Grid Infrastructure 설치</span><span class="sxs-lookup"><span data-stu-id="00d9e-223">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="00d9e-224">Grid Infrastructure를 설치하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-224">To install Oracle Grid Infrastructure, complete the following steps:</span></span>

1. <span data-ttu-id="00d9e-225">**그리드**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-225">Sign in as **grid**.</span></span> <span data-ttu-id="00d9e-226">(로그인할 때 암호 입력 화면이 나타나지 않아야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="00d9e-226">(You should be able to sign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="00d9e-227">Windows를 실행하는 경우 설치를 시작하기 전에 Xming을 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-227">If you are running Windows, make sure you have started Xming before you begin the installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="00d9e-228">Oracle Grid Infrastructure 12c 릴리스 1 설치 관리자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-228">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="00d9e-229">(설치 관리자를 시작하는 데 몇 분 정도 걸릴 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="00d9e-229">(It might take a few minutes for the  installer to start.)</span></span>

2. <span data-ttu-id="00d9e-230">**설치 옵션 선택** 페이지에서 **독립 실행형 서버에 대한 Oracle Grid Infrastructure 설치 및 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-230">On the **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![설치 관리자 설치 옵션 선택 페이지의 스크린샷](./media/oracle-asm/install01.png)

3. <span data-ttu-id="00d9e-232">**제품 언어 선택** 페이지에서 **영어** 또는 원하는 언어를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-232">On the **Select Product Languages** page, ensure **English** or the language that you want is selected.</span></span>  <span data-ttu-id="00d9e-233">`next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-233">Click `next`.</span></span>

4. <span data-ttu-id="00d9e-234">**ASM 디스크 그룹 만들기** 페이지에서,</span><span class="sxs-lookup"><span data-stu-id="00d9e-234">On the **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="00d9e-235">디스크 그룹에 사용할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-235">Enter a name for the disk group.</span></span>
   - <span data-ttu-id="00d9e-236">**중복**에서 **외부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-236">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="00d9e-237">**할당 단위 크기**에서 **4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-237">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="00d9e-238">**디스크 추가**에서 **ORCLASMSP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-238">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="00d9e-239">`next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-239">Click `next`.</span></span>

5. <span data-ttu-id="00d9e-240">**ASM 암호 지정** 페이지에서 **이러한 계정에 대해 동일한 암호 사용** 옵션을 선택하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-240">On the **Specify ASM Password** page, select the **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![설치 관리자 ASM 암호 지정 페이지의 스크린샷](./media/oracle-asm/install04.png)

6. <span data-ttu-id="00d9e-242">**관리 옵션 지정** 페이지에서는 EM 클라우드 컨트롤을 구성하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-242">On the **Specify Management Options** page, you have the option to configure EM Cloud Control.</span></span> <span data-ttu-id="00d9e-243">이 옵션을 무시하려면 `next`을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-243">We are skipping this option - click `next` to continue.</span></span> 

7. <span data-ttu-id="00d9e-244">**권한있는 운영 체제 그룹** 페이지에서 기본 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-244">On the **Privileged Operating System Groups** page, use the default settings.</span></span> <span data-ttu-id="00d9e-245">계속하려면 `next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-245">Click `next` to continue.</span></span>

8. <span data-ttu-id="00d9e-246">**설치 위치 지정** 페이지에서 기본 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-246">On the **Specify Installation Location** page, use the default settings.</span></span> <span data-ttu-id="00d9e-247">계속하려면 `next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-247">Click `next` to continue.</span></span>

9. <span data-ttu-id="00d9e-248">**인벤토리 만들기** 페이지에서 인벤토리 디렉터리를 `/u01/app/grid/oraInventory`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-248">On the **Create Inventory** page, change the Inventory Directory to `/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="00d9e-249">계속하려면 `next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-249">Click `next` to continue.</span></span>

   ![설치 관리자 인벤토리 만들기 페이지의 스크린샷](./media/oracle-asm/install08.png)

10. <span data-ttu-id="00d9e-251">**루트 스크립트 실행 구성** 페이지에서 **구성 스크립트 자동으로 실행** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-251">On the **Root script execution configuration** page, select the **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="00d9e-252">그런 다음 **"root" 사용자 자격 증명 사용** 옵션을 선택하고 루트 사용자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-252">Then, select the **Use "root" user credential** option, and enter the root user password.</span></span>

    ![설치 관리자 루트 스크립트 실행 구성 페이지의 스크린샷](./media/oracle-asm/install09.png)

11. <span data-ttu-id="00d9e-254">**필수 요소 확인 수행** 페이지에서 오류가 발생하여 현재 설치에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-254">On the **Perform Prerequisite Checks** page, the current setup will fail with errors.</span></span> <span data-ttu-id="00d9e-255">이는 정상적인 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-255">This is an expected behavior.</span></span> <span data-ttu-id="00d9e-256">`Fix & Check Again`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-256">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="00d9e-257">**스크립트 수정** 대화 상자에서 `OK`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-257">In the **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="00d9e-258">**요약** 페이지에서 선택한 설정을 검토한 다음 `Install`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-258">On the **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![설치 관리자 요약 페이지의 스크린샷](./media/oracle-asm/install12.png)

14. <span data-ttu-id="00d9e-260">구성 스크립트를 권한 있는 사용자로 실행해야 한다는 경고 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-260">A warning dialog box appears informing you configuration scripts need to be run as a privileged user.</span></span> <span data-ttu-id="00d9e-261">계속하려면 `Yes`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-261">Click `Yes` to continue.</span></span>

15. <span data-ttu-id="00d9e-262">**마침** 페이지에서 `Close`를 클릭하여 설치를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-262">On the **Finish** page, click `Close` to finish the installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="00d9e-263">Oracle ASM 설치 설정</span><span class="sxs-lookup"><span data-stu-id="00d9e-263">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="00d9e-264">Oracle ASM 설치를 설정하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-264">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="00d9e-265">X11 세션에서 **그리드**로 로그인되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-265">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="00d9e-266">`enter` 키를 눌러서 터미널을 복구할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-266">You might need to hit `enter` to revive the terminal.</span></span> <span data-ttu-id="00d9e-267">Oracle Automated Storage Management Configuration Assistant를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-267">Then launch the Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="00d9e-268">Oracle ASM 구성 도우미가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-268">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="00d9e-269">**ASM 구성: 디스크 그룹** 대화 상자에서 `Create` 단추를 클릭한 다음 `Show Advanced Options`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-269">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="00d9e-270">**디스크 그룹 만들기** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-270">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="00d9e-271">디스크 그룹 이름 **DATA**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-271">Enter the disk group name **DATA**.</span></span>
   - <span data-ttu-id="00d9e-272">**멤버 디스크 선택**에서 **ORCL_DATA** 및 **ORCL_DATA1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-272">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="00d9e-273">**할당 단위 크기**에서 **4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-273">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="00d9e-274">`ok`을 클릭하여 디스크 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-274">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="00d9e-275">`ok`을 클릭하여 확인 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-275">Click `ok` to close the confirmation window.</span></span>

   ![디스크 그룹 만들기 대화 상자의 스크린샷](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="00d9e-277">**ASM 구성: 디스크 그룹** 대화 상자에서 `Create` 단추를 클릭한 다음 `Show Advanced Options`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-277">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="00d9e-278">**디스크 그룹 만들기** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-278">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="00d9e-279">디스크 그룹 이름 **FRA**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-279">Enter the disk group name **FRA**.</span></span>
   - <span data-ttu-id="00d9e-280">**중복**에서 **외부(없음)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-280">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="00d9e-281">**멤버 디스크 선택**에서 **ORCL_FRA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-281">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="00d9e-282">**할당 단위 크기**에서 **4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-282">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="00d9e-283">`ok`을 클릭하여 디스크 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-283">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="00d9e-284">`ok`을 클릭하여 확인 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-284">Click `ok` to close the confirmation window.</span></span>

   ![디스크 그룹 만들기 대화 상자의 스크린샷](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="00d9e-286">**끝내기**를 선택하여 ASM 구성 도우미를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-286">Select **Exit** to close ASM Configuration Assistant.</span></span>

   ![끝내기 단추가 있는 ASM 구성: 디스크 그룹 대화 상자의 스크린샷](./media/oracle-asm/asm05.png)

## <a name="create-the-database"></a><span data-ttu-id="00d9e-288">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00d9e-288">Create the database</span></span>

<span data-ttu-id="00d9e-289">Oracle 데이터베이스 소프트웨어는 이미 Azure Marketplace 이미지에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-289">The Oracle database software is already installed on the Azure Marketplace image.</span></span> <span data-ttu-id="00d9e-290">데이터베이스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-290">To create a database, complete the following steps:</span></span>

1. <span data-ttu-id="00d9e-291">사용자를 Oracle superuser로 전환하고, 다음을 로깅하기 위해 수신기를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-291">Switch users to the Oracle superuser, and then initialize the listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="00d9e-292">데이터베이스 구성 도우미가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-292">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="00d9e-293">**데이터베이스 작업 페이지**에서 `Create Database`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-293">On the **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="00d9e-294">**생성 모드** 페이지에서,</span><span class="sxs-lookup"><span data-stu-id="00d9e-294">On the **Creation Mode** page:</span></span>

   - <span data-ttu-id="00d9e-295">데이터베이스에 사용할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-295">Enter a name for the database.</span></span>
   - <span data-ttu-id="00d9e-296">**저장소 형식**의 경우 **ASM(자동 저장소 관리)**을 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-296">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="00d9e-297">**데이터베이스 파일 위치**의 경우 위치를 제안하는 ASM 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-297">For **Database Files Location**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="00d9e-298">**빠른 복구 영역**의 경우 위치를 제안하는 ASM 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-298">For **Fast Recovery Area**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="00d9e-299">**관리 암호** 및 **암호 확인**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-299">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="00d9e-300">`create as container database`를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-300">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="00d9e-301">`pluggable database name` 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-301">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="00d9e-302">**요약** 페이지에서 선택한 설정을 검토한 다음 `Finish`을 클릭하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-302">On the **Summary** page, review your selected settings, and then click `Finish` to create the database.</span></span>

   ![요약 페이지의 스크린샷](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="00d9e-304">데이터베이스가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-304">The Database has been created.</span></span> <span data-ttu-id="00d9e-305">**마침** 페이지에서는 추가 계정의 잠금을 해제하여 이 데이터베이스를 사용하고 암호를 변경하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-305">On the **Finish** page, you have the option to unlock additional accounts to use this database and change the passwords.</span></span> <span data-ttu-id="00d9e-306">작업을 수행하려는 경우 **암호 관리**를 선택하고 그렇지 않으면 `close`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-306">If you wish to do so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="00d9e-307">VM 삭제</span><span class="sxs-lookup"><span data-stu-id="00d9e-307">Delete the VM</span></span>

<span data-ttu-id="00d9e-308">Azure Marketplace의 Oracle DB 이미지에서 Oracle Automated Storage Management를 성공적으로 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-308">You have successfully configured Oracle Automated Storage Management on the Oracle DB image from the Azure Marketplace.</span></span>  <span data-ttu-id="00d9e-309">더 이상 VM이 필요하지 않은 경우 다음 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d9e-309">When you no longer need this VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="00d9e-310">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00d9e-310">Next steps</span></span>

[<span data-ttu-id="00d9e-311">자습서: Oracle DataGuard 구성</span><span class="sxs-lookup"><span data-stu-id="00d9e-311">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="00d9e-312">자습서: Oracle GoldenGate 구성</span><span class="sxs-lookup"><span data-stu-id="00d9e-312">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="00d9e-313">[Oracle DB 설계](oracle-design.md) 검토</span><span class="sxs-lookup"><span data-stu-id="00d9e-313">Review [Architect an Oracle DB](oracle-design.md)</span></span>
