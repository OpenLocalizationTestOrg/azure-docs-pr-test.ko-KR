---
title: "Azure Linux 가상 컴퓨터에서 Oracle ASM를 aaaSet | Microsoft Docs"
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
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="23dae-103">Azure Linux 가상 컴퓨터에 Oracle ASM 설정</span><span class="sxs-lookup"><span data-stu-id="23dae-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="23dae-104">Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="23dae-105">이 자습서에서는 hello 설치 및 구성의 Oracle 자동화 된 저장소 관리 (ASM)와 결합 하는 기본 Azure 가상 컴퓨터 배포에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="23dae-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="23dae-107">만들고 tooan Oracle 데이터베이스 VM 연결</span><span class="sxs-lookup"><span data-stu-id="23dae-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="23dae-108">Oracle Automated Storage Management 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="23dae-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="23dae-109">Oracle Grid 인프라 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="23dae-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="23dae-110">Oracle ASM 설치 초기화</span><span class="sxs-lookup"><span data-stu-id="23dae-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="23dae-111">ASM에서 관리하는 Oracle DB 만들기</span><span class="sxs-lookup"><span data-stu-id="23dae-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="23dae-112">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="23dae-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="23dae-113">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="23dae-114">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="23dae-115">Hello 환경 준비</span><span class="sxs-lookup"><span data-stu-id="23dae-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="23dae-116">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="23dae-116">Create a resource group</span></span>

<span data-ttu-id="23dae-117">리소스 그룹 toocreate hello를 사용 하 여 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="23dae-118">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="23dae-119">이 예제에서는 리소스 그룹 이름이 *myResourceGroup* hello에 *eastus* 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="23dae-120">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="23dae-120">Create a VM</span></span>

<span data-ttu-id="23dae-121">가상 컴퓨터 toocreate hello Oracle 데이터베이스 이미지를 기반 및 toouse Oracle ASM 구성, hello를 사용 하 여 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="23dae-122">hello 다음 예제에서는 각 50GB의 네 개의 연결 된 데이터 디스크와 Standard_DS2_v2 크기로 사용 되는 myVM 이라는 VM</span><span class="sxs-lookup"><span data-stu-id="23dae-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="23dae-123">이미 hello 기본 키 위치에 존재 하지 않습니다, 하는 경우 또한 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="23dae-124">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="23dae-125">Hello VM을 만든 후 Azure CLI 정보 비슷한 toohello를 다음 예제에서는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="23dae-126">Hello 값을 확인 `publicIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="23dae-127">VM이 주소 tooaccess hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-127">You use this address tooaccess hello VM.</span></span>

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

### <a name="connect-toohello-vm"></a><span data-ttu-id="23dae-128">Toohello VM 연결</span><span class="sxs-lookup"><span data-stu-id="23dae-128">Connect toohello VM</span></span>

<span data-ttu-id="23dae-129">와 SSH 세션 toocreate VM hello, 추가 설정을 구성 하 고 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="23dae-130">Hello로 hello IP 주소를 교체 `publicIpAddress` VM에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="23dae-131">Oracle ASM 설치</span><span class="sxs-lookup"><span data-stu-id="23dae-131">Install Oracle ASM</span></span>

<span data-ttu-id="23dae-132">tooinstall Oracle ASM, 전체 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="23dae-133">Oracle ASM 설치에 대한 자세한 내용은 [Oracle Linux 6에 대한 Oracle ASMLib 다운로드](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23dae-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="23dae-134">ASM 설치 순서 toocontinue의 루트로 toologin이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="23dae-135">이러한 추가 명령을 tooinstall Oracle ASM 구성 요소를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="23dae-136">Oracle ASM이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="23dae-137">hello이이 명령의 출력에는 다음과 같은 구성 요소가 hello를 수록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="23dae-138">ASM 올바르게 순서 toofunction에서 특정 사용자 및 역할 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="23dae-139">다음 명령을 hello hello 필수 사용자 계정 및 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="23dae-140">사용자 및 그룹이 올바르게 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="23dae-141">hello이 명령의 출력을 나열 해야 hello 다음 사용자 및 그룹:</span><span class="sxs-lookup"><span data-stu-id="23dae-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="23dae-142">사용자에 대 한 폴더를 만들고 *그리드* hello 소유자를 변경 하 고:</span><span class="sxs-lookup"><span data-stu-id="23dae-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="23dae-143">Oracle ASM 설정</span><span class="sxs-lookup"><span data-stu-id="23dae-143">Set up Oracle ASM</span></span>

<span data-ttu-id="23dae-144">이 자습서에서는 hello 기본 사용자가 *그리드* hello 기본 그룹은 및 *asmadmin*합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="23dae-145">해당 hello 확인 *oracle* hello asmadmin 그룹의 일부인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="23dae-146">Oracle ASM 설치 단계를 수행 하는 전체 hello tooset:</span><span class="sxs-lookup"><span data-stu-id="23dae-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="23dae-147">Hello Oracle ASM 라이브러리 드라이버 설정 정의가 포함 됩니다 (표) hello 기본 사용자 및 기본 그룹 (asmadmin) 부팅 시 hello 드라이브 toostart 구성 뿐만 아니라 (y 선택) 및 디스크에서 부팅에 대 한 tooscan (y 선택).</span><span class="sxs-lookup"><span data-stu-id="23dae-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="23dae-148">다음 명령을 hello에서 tooanswer hello 프롬프트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="23dae-149">이 명령의 출력 hello 비슷한 toohello 뒤, 프롬프트 toobe 답변으로 중지 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="23dae-150">Hello 디스크 구성 보기:</span><span class="sxs-lookup"><span data-stu-id="23dae-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="23dae-151">이 명령의 hello 출력의 사용 가능한 디스크 목록을 다음 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-151">hello output of this command should look similar toohello following listing of available disks</span></span>

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

3. <span data-ttu-id="23dae-152">디스크 포맷 */개발/sdc* hello를 실행 하 여 다음 명령 및 hello 응답 프롬프트에:</span><span class="sxs-lookup"><span data-stu-id="23dae-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="23dae-153">새 파티션의 경우 *n*</span><span class="sxs-lookup"><span data-stu-id="23dae-153">*n* for new partition</span></span>
   - <span data-ttu-id="23dae-154">주 파티션의 경우 *p*</span><span class="sxs-lookup"><span data-stu-id="23dae-154">*p* for primary partition</span></span>
   - <span data-ttu-id="23dae-155">*1* tooselect hello 첫 번째 파티션</span><span class="sxs-lookup"><span data-stu-id="23dae-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="23dae-156">키를 눌러 `enter` 기본 첫 번째 실린더 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="23dae-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="23dae-157">키를 눌러 `enter` 기본 마지막 실린더 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="23dae-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="23dae-158">키를 눌러 *w* toowrite hello 변경 toohello 파티션 테이블</span><span class="sxs-lookup"><span data-stu-id="23dae-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="23dae-159">위에 제공 된 hello 답변을 사용 하 여, hello fdisk 명령에 대 한 hello 출력 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
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
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="23dae-160">반복 hello에 대 한 fdisk 명령 앞 `/dev/sdd`, `/dev/sde`, 및 `/dev/sdf`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="23dae-161">Hello 디스크 구성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="23dae-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="23dae-162">hello 명령의 hello 출력 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-162">hello output of hello command should look like hello following:</span></span>

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

6. <span data-ttu-id="23dae-163">Hello Oracle ASM 서비스 상태를 확인 하 고 hello Oracle ASM 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="23dae-164">hello 명령의 hello 출력 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="23dae-165">Oracle ASM 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="23dae-166">hello 명령의 hello 출력 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="23dae-167">Oracle ASM 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="23dae-168">다음 Oracle ASM 디스크 hello 오프 hello 명령의 hello 출력 수록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="23dae-169">Hello 루트, oracle 및 눈금 사용자에 대 한 hello 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="23dae-170">**이러한 새 암호를 기록** 대로 hello 설치 하는 동안에 나중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="23dae-171">Hello 폴더 사용 권한을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-171">Change hello folder permission:</span></span>

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

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="23dae-172">Oracle Grid Infrastructure 다운로드 및 준비</span><span class="sxs-lookup"><span data-stu-id="23dae-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="23dae-173">toodownload hello Oracle 그리드 인프라 소프트웨어, 단계를 수행 하는 전체 hello 준비 및:</span><span class="sxs-lookup"><span data-stu-id="23dae-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="23dae-174">Hello에서 Oracle 그리드 인프라 다운로드 [Oracle ASM 다운로드 페이지](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="23dae-175">라는 hello 다운로드 아래 **Oracle Database 12c 릴리스 1 그리드 인프라 (12.1.0.2.0) Linux x86-64에 대 한**, hello 두 개의.zip 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="23dae-176">Hello.zip tooyour 클라이언트 컴퓨터 파일을 다운로드 한 후 복사 프로토콜 보안 (SCP) toocopy hello 파일 tooyour VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="23dae-177">SSH는 hello로 순서 toomove hello.zip 파일에는 Azure에서 Oracle VM 스풀링됩니다/폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="23dae-178">Hello 파일의 hello 소유자를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="23dae-179">Hello 파일을 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-179">Unzip hello files.</span></span> <span data-ttu-id="23dae-180">(설치 hello Linux의 압축을 푸는 도구가 설치 되어 있지 않은 경우.)</span><span class="sxs-lookup"><span data-stu-id="23dae-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="23dae-181">사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="23dae-182">구성된 스왑 공간을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-182">Update configured swap space.</span></span> <span data-ttu-id="23dae-183">Oracle 그리드 구성 6.8 g B 이상의 스왑 공간 tooinstall 눈금 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="23dae-184">Azure에서 Oracle Linux 이미지 hello 기본 스왑 파일 크기는 2048MB만 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="23dae-185">Tooincrease 해야 `ResourceDisk.SwapSizeMB` hello에 `/etc/waagent.conf` 파일을 업데이트 하는 hello 설정 tootake 효과 대 한 순서 대로 hello WALinuxAgent 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="23dae-186">읽기 전용 파일 이기 때문에 toochange 파일 사용 권한을 tooenable 쓰기 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="23dae-187">검색할 `ResourceDisk.SwapSizeMB` hello 값도 변경 및**8192**합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="23dae-188">Toopress 해야 `insert` tooenter 삽입 모드의 hello 값의 형식 **8192** 누릅니다 `esc` tooreturn toocommand 모드.</span><span class="sxs-lookup"><span data-stu-id="23dae-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="23dae-189">toowrite hello 변경과 quit hello 파일 입력 `:wq` 누릅니다 `enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23dae-190">항상 사용 하는 것이 좋습니다 `WALinuxAgent` tooconfigure 스왑 공간을 hello 로컬 임시 디스크 (임시 디스크에) 최상의 성능을 위해 항상 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="23dae-191">에 대 한 자세한 내용은 참조 하십시오. [tooadd 스왑 Linux Azure 가상 컴퓨터에서 파일을 어떻게](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines)합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="23dae-192">로컬 클라이언트 및 VM toorun x11 준비</span><span class="sxs-lookup"><span data-stu-id="23dae-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="23dae-193">Oracle ASM 구성 그래픽 인터페이스 toocomplete hello 설치 및 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="23dae-194">사용 하 여 hello x11 프로토콜 toofacilitate이이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="23dae-195">X11 이미 클라이언트 시스템 (Mac 또는 Linux)를 사용 하는 경우 기능이 사용 하도록 설정 하 고 구성-있습니다이 구성을 건너뛸 단독 tooWindows 컴퓨터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="23dae-196">[PuTTY 다운로드](http://www.putty.org/) 및 [Xming 다운로드](https://xming.en.softonic.com/) tooyour Windows 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="23dae-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="23dae-197">계속 하기 전에 hello 기본 값으로 이러한 응용 프로그램의 두 가지 toocomplete hello 설치를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="23dae-198">PuTTY를 설치한 후 명령 프롬프트를 열고, PuTTY 폴더 (예: C:\Program Files\PuTTY) hello로 변경 하 고 실행 `puttygen.exe` 의 순서로 toogenerate 키입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="23dae-199">PuTTY 키 생성기에서,</span><span class="sxs-lookup"><span data-stu-id="23dae-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="23dae-200">Hello를 선택 하 여 키를 생성 `Generate` 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="23dae-201">Hello 키 (Ctrl + C)의 hello 내용을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="23dae-202">선택 hello `Save private key` 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="23dae-203">암호를 사용 하 여 hello 키를 보안에 대 한 hello 경고를 무시 한 다음 선택 `OK`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![PuTTY 키 생성기의 스크린샷](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="23dae-205">VM에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="23dae-206">`authorized_keys`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="23dae-207">이 파일의 hello 키의 내용을 hello를 붙여 넣고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="23dae-208">hello 키 hello 문자열을 포함 해야 `ssh-rsa`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="23dae-209">또한 hello 키의 내용을 hello 텍스트 한 줄 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="23dae-210">클라이언트 컴퓨터에서 PuTTY를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="23dae-211">Hello에 **범주** 창 너무 이동**연결** > **SSH** > **Auth**합니다. Hello에 **인증에 대 한 개인 키 파일** 상자 이전에 생성 toohello 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Hello SSH 인증 옵션의 스크린 샷](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="23dae-213">Hello에 **범주** 창 너무 이동**연결** > **SSH** > **X11**합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="23dae-214">선택 hello **사용 X11 전달** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Hello SSH X11의 스크린샷 옵션 전달](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="23dae-216">Hello에 **범주** 창 너무 이동**세션**합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="23dae-217">Oracle ASM VM 입력 `<publicIPaddress>` hello 호스트 이름 대화 상자에서 새 입력 `Saved Session` 이름을 지정 하 고 클릭 `Save`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="23dae-218">저장 한 후 클릭 `open` tooconnect tooyour Oracle ASM 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="23dae-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="23dae-219">hello 처음 연결 하면 경고가 표시 되도록 hello 원격 시스템 레지스트리에서 캐시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="23dae-220">클릭 `yes` tooadd 것 하 고 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-220">Click on `yes` tooadd it and continue.</span></span>

   ![Hello PuTTY 세션 옵션의 스크린 샷](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="23dae-222">Oracle Grid Infrastructure 설치</span><span class="sxs-lookup"><span data-stu-id="23dae-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="23dae-223">tooinstall Oracle 그리드 인프라 전체 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="23dae-224">**그리드**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-224">Sign in as **grid**.</span></span> <span data-ttu-id="23dae-225">(암호를 입력 하지 않고에 수 toosign 수 있어야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="23dae-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="23dae-226">Windows를 실행 하는 경우 Xming hello 설치를 시작 하기 전에 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="23dae-227">Oracle Grid Infrastructure 12c 릴리스 1 설치 관리자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="23dae-228">(Hello installer toostart 몇 분 정도 걸릴 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="23dae-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="23dae-229">Hello에 **설치 옵션을 선택** 페이지 **설치 및 독립 실행형 서버에 대 한 Oracle 그리드 인프라 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Hello 설치 관리자의 설치 옵션 선택 페이지의 스크린샷](./media/oracle-asm/install01.png)

3. <span data-ttu-id="23dae-231">Hello에 **제품 언어 선택** 페이지 **영어** hello 원하는 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="23dae-232">`next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-232">Click `next`.</span></span>

4. <span data-ttu-id="23dae-233">Hello에 **ASM 디스크 그룹 만들기** 페이지:</span><span class="sxs-lookup"><span data-stu-id="23dae-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="23dae-234">Hello 디스크 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="23dae-235">**중복**에서 **외부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="23dae-236">**할당 단위 크기**에서 **4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="23dae-237">**디스크 추가**에서 **ORCLASMSP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="23dae-238">`next`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-238">Click `next`.</span></span>

5. <span data-ttu-id="23dae-239">Hello에 **ASM 암호 지정** 페이지, 선택 hello **이러한 계정에 대해 동일한 암호를 사용 하 여** 옵션을 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Hello 설치 관리자의 ASM 암호 지정 페이지의 스크린샷](./media/oracle-asm/install04.png)

6. <span data-ttu-id="23dae-241">Hello에 **관리 옵션 지정** 페이지 hello 옵션 tooconfigure EM 클라우드 제어 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="23dae-242">이 옵션을 무시-클릭 `next` toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="23dae-243">Hello에 **권한 있는 운영 체제 그룹** 페이지에서 hello 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="23dae-244">클릭 `next` toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="23dae-245">Hello에 **설치 위치 지정** 페이지에서 hello 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="23dae-246">클릭 `next` toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="23dae-247">Hello에 **만들 인벤토리** 페이지, 너무 hello 인벤토리 디렉터리 변경`/u01/app/grid/oraInventory`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="23dae-248">클릭 `next` toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-248">Click `next` toocontinue.</span></span>

   ![Hello 설치 관리자 만들기 인벤토리 페이지의 스크린샷](./media/oracle-asm/install08.png)

10. <span data-ttu-id="23dae-250">Hello에 **루트 스크립트 실행 구성** 페이지, 선택 hello **자동 구성 스크립트를 실행** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="23dae-251">그런 다음 선택 하는 hello **"root" 사용자 자격 증명을 사용 하 여** 옵션을 선택한 hello 루트 사용자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Hello 설치 프로그램의 루트 스크립트 실행 구성 페이지의 스크린샷](./media/oracle-asm/install09.png)

11. <span data-ttu-id="23dae-253">Hello에 **Prerequisite Checks 수행** 페이지, 오류와 함께 hello 현재 설치에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="23dae-254">이는 정상적인 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-254">This is an expected behavior.</span></span> <span data-ttu-id="23dae-255">`Fix & Check Again`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="23dae-256">Hello에 **픽스업 스크립트** 대화 상자를 클릭 하 여 `OK`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="23dae-257">Hello에 **요약** 페이지에서 선택한 설정을 검토 한 다음 클릭 `Install`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Hello 설치 관리자의 요약 페이지의 스크린샷](./media/oracle-asm/install12.png)

14. <span data-ttu-id="23dae-259">권한 있는 사용자로 실행 toobe 구성 스크립트를 알리는 경고 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="23dae-260">클릭 `Yes` toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="23dae-261">Hello에 **마침** 페이지 `Close` toofinish hello 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="23dae-262">Oracle ASM 설치 설정</span><span class="sxs-lookup"><span data-stu-id="23dae-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="23dae-263">Oracle ASM 설치 단계를 수행 하는 전체 hello tooset:</span><span class="sxs-lookup"><span data-stu-id="23dae-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="23dae-264">X11 세션에서 **그리드**로 로그인되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="23dae-265">Toohit 해야 `enter` toorevive hello 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="23dae-266">다음 Oracle 자동화 된 저장소 관리 Configuration Assistant hello를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="23dae-267">Oracle ASM 구성 도우미가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="23dae-268">Hello에 **ASM 구성: 디스크 그룹** 대화 상자를 클릭 hello `Create` 단추를 선택한 다음 클릭 `Show Advanced Options`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="23dae-269">Hello에 **디스크 그룹 만들기** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="23dae-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="23dae-270">Hello 디스크 그룹 이름을 입력 **데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="23dae-271">**멤버 디스크 선택**에서 **ORCL_DATA** 및 **ORCL_DATA1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="23dae-272">**할당 단위 크기**에서 **4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="23dae-273">클릭 `ok` toocreate hello 디스크 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="23dae-274">클릭 `ok` tooclose hello 확인 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Hello 디스크 그룹 만들기 대화 상자의 스크린 샷](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="23dae-276">Hello에 **ASM 구성: 디스크 그룹** 대화 상자를 클릭 hello `Create` 단추를 선택한 다음 클릭 `Show Advanced Options`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="23dae-277">Hello에 **디스크 그룹 만들기** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="23dae-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="23dae-278">Hello 디스크 그룹 이름을 입력 **FRA**합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="23dae-279">**중복**에서 **외부(없음)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="23dae-280">**멤버 디스크 선택**에서 **ORCL_FRA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="23dae-281">**할당 단위 크기**에서 **4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="23dae-282">클릭 `ok` toocreate hello 디스크 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="23dae-283">클릭 `ok` tooclose hello 확인 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Hello 디스크 그룹 만들기 대화 상자의 스크린 샷](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="23dae-285">선택 **종료** tooclose ASM Configuration Assistant 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![스크린 샷 hello 구성 ASM: 끝내기 단추와 디스크 그룹 대화 상자](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="23dae-287">Hello 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="23dae-287">Create hello database</span></span>

<span data-ttu-id="23dae-288">Oracle 데이터베이스 소프트웨어 hello hello Azure 마켓플레이스 이미지에 이미 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="23dae-289">toocreate 데이터베이스를 전체 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="23dae-290">사용자가 toohello Oracle superuser 전환한 다음 로깅에 대 한 hello 수신기를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="23dae-291">데이터베이스 구성 도우미가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="23dae-292">Hello에 **데이터베이스 작업** 페이지 `Create Database`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="23dae-293">Hello에 **생성 모드** 페이지:</span><span class="sxs-lookup"><span data-stu-id="23dae-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="23dae-294">Hello 데이터베이스에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="23dae-295">**저장소 형식**의 경우 **ASM(자동 저장소 관리)**을 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="23dae-296">에 대 한 **데이터베이스 파일 위치**, hello 기본값을 사용 하 여 ASM 제안 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="23dae-297">에 대 한 **빠른 복구 영역**, hello 기본값을 사용 하 여 ASM 제안 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="23dae-298">**관리 암호** 및 **암호 확인**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="23dae-299">`create as container database`를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="23dae-300">`pluggable database name` 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="23dae-301">Hello에 **요약** 페이지에서 선택한 설정을 검토 한 다음 클릭 `Finish` toocreate hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Hello 요약 페이지의 스크린샷](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="23dae-303">hello 데이터베이스 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-303">hello Database has been created.</span></span> <span data-ttu-id="23dae-304">Hello에 **마침** 페이지에서는 hello toounlock 추가 계정을 toouse이이 데이터베이스 옵션 및 hello 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="23dae-305">Toodo 하므로, 선택 **암호 관리** -그렇지 않으면 클릭 `close`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="23dae-306">Hello VM 삭제</span><span class="sxs-lookup"><span data-stu-id="23dae-306">Delete hello VM</span></span>

<span data-ttu-id="23dae-307">저장소 관리를 자동화 하는 Oracle hello Azure Marketplace에서에서 hello Oracle DB 이미지에서 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="23dae-308">이 VM이 필요 없는 경우 hello 다음 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23dae-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="23dae-309">다음 단계</span><span class="sxs-lookup"><span data-stu-id="23dae-309">Next steps</span></span>

[<span data-ttu-id="23dae-310">자습서: Oracle DataGuard 구성</span><span class="sxs-lookup"><span data-stu-id="23dae-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="23dae-311">자습서: Oracle GoldenGate 구성</span><span class="sxs-lookup"><span data-stu-id="23dae-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="23dae-312">[Oracle DB 설계](oracle-design.md) 검토</span><span class="sxs-lookup"><span data-stu-id="23dae-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
