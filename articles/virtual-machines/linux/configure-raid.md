---
title: "aaaConfigure 소프트웨어 RAID Linux를 실행 하 여 가상 컴퓨터 | Microsoft Docs"
description: "Azure에서 linux toouse mdadm tooconfigure RAID 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="cdc70-103">Linux에서 소프트웨어 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="cdc70-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="cdc70-104">일반적인 시나리오 toouse 소프트웨어 RAID Linux 가상 컴퓨터에서 여러 연결 된 데이터 디스크에 하나의 RAID 장치로 Azure toopresent입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="cdc70-105">일반적으로 사용 되는 tooimprove 성능 고 처리량 비교 toousing만 단일 디스크를 개선 하기 위해 허용 수이 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="cdc70-106">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="cdc70-106">Attaching data disks</span></span>
<span data-ttu-id="cdc70-107">두 개 이상의 빈 데이터 디스크는 필요한 tooconfigure RAID 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="cdc70-108">RAID 장치를 만들기 위한 hello 주된 이유는 디스크 IO의 tooimprove 성능.</span><span class="sxs-lookup"><span data-stu-id="cdc70-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="cdc70-109">IO 요구 사항에 따라, 디스크 또는 디스크 당 too5000 IO/ps를 우리의 프리미엄 저장소와 당 too500 IO/ps를와 우리의 표준 저장소에 저장 된 tooattach 디스크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="cdc70-110">이 문서는 방법에 세부 정보를 시작 하지 못할 tooprovision 및 데이터 디스크 tooa Linux 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="cdc70-111">참조 hello Microsoft Azure 문서 [디스크 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 어떻게 tooattach 빈 데이터 디스크 tooa Linux 가상 컴퓨터에서 Azure에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="cdc70-112">Hello mdadm 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="cdc70-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="cdc70-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="cdc70-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="cdc70-114">**CentOS 및 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="cdc70-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="cdc70-115">**SLES 및 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="cdc70-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="cdc70-116">Hello 디스크 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc70-116">Create hello disk partitions</span></span>
<span data-ttu-id="cdc70-117">이 예에서는 /dev/sdc에 단일 디스크 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="cdc70-118">새 디스크 파티션은 hello /dev/sdc1을 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="cdc70-119">시작 `fdisk` toobegin 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc70-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="cdc70-120">키를 눌러 hello 프롬프트 toocreate에 ' n '는  **n** 우 파티션:</span><span class="sxs-lookup"><span data-stu-id="cdc70-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="cdc70-121">'P' toocreate를 눌러 다음으로 **p**기본 파티션:</span><span class="sxs-lookup"><span data-stu-id="cdc70-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="cdc70-122">'1' tooselect 파티션 번호 1 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="cdc70-123">선택 hello hello 새 파티션 또는 키를 눌러의 시작 지점 `<enter>` tooaccept hello 기본 tooplace hello 파티션을 hello 드라이브에 공간이 hello hello 맨 앞에서:</span><span class="sxs-lookup"><span data-stu-id="cdc70-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="cdc70-124">예를 들어 형식 '+10G' toocreate 10 기가바이트 파티션 hello 파티션의 hello 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="cdc70-125">또는 키를 누릅니다 `<enter>` hello 전체 드라이브에 걸쳐 있는 파티션 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="cdc70-126">다음으로, hello ID를 변경 하 고 **t**hello 기본값과에서 hello 파티션 유형 ID '83' (Linux) tooID 'fd' (Linux raid 자동):</span><span class="sxs-lookup"><span data-stu-id="cdc70-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="cdc70-127">마지막으로 hello 파티션 테이블 toohello 드라이브를 작성 하 고 fdisk 종료:</span><span class="sxs-lookup"><span data-stu-id="cdc70-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="cdc70-128">Hello RAID 배열 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc70-128">Create hello RAID array</span></span>
1. <span data-ttu-id="cdc70-129">다음 예제는 "스트라이프" (RAID 수준 0) 3 개의 파티션과 (sdc1, sdd1, sde1) 세 가지 별도 데이터 디스크에 있는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="cdc70-130">이 명령을 실행하면 **/dev/md127** 이라는 새 RAID 장치가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="cdc70-131">또한 참고 이러한 데이터 디스크에서는 이전에 존재 하지 않는 다른 RAID 배열의 일부 필요한 tooadd hello 수 수 것 `--force` 매개 변수 toohello `mdadm` 명령:</span><span class="sxs-lookup"><span data-stu-id="cdc70-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="cdc70-132">Hello 새 RAID 장치에 hello 파일 시스템 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc70-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="cdc70-133">a.</span><span class="sxs-lookup"><span data-stu-id="cdc70-133">a.</span></span> <span data-ttu-id="cdc70-134">**CentOS, Oracle Linux, SLES 12, openSUSE 및 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="cdc70-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="cdc70-135">b.</span><span class="sxs-lookup"><span data-stu-id="cdc70-135">b.</span></span> <span data-ttu-id="cdc70-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="cdc70-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="cdc70-137">c.</span><span class="sxs-lookup"><span data-stu-id="cdc70-137">c.</span></span> <span data-ttu-id="cdc70-138">**SLES 11** - boot.md 사용 및 mdadm.conf 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc70-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="cdc70-139">SUSE 시스템에서 이렇게 변경한 후에는 다시 부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="cdc70-140">SLES 12에서는 이 단계가 필요하지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="cdc70-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="cdc70-141">Hello 새 파일 시스템 너무/등/fstab 추가</span><span class="sxs-lookup"><span data-stu-id="cdc70-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cdc70-142">Hello /etc/fstab 파일을 잘못 편집 하는 경우 시스템 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="cdc70-143">를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cdc70-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="cdc70-144">또한 편집 하기 전에 hello /etc/fstab 파일의 백업을 만들어졌는지 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="cdc70-145">예를 들어 새로운 파일 시스템에 대 한 원하는 hello 탑재 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="cdc70-146">/Etc/fstab을 편집할 때 hello **UUID** 사용된 tooreference hello 파일 hello 보다는 시스템 장치 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="cdc70-147">사용 하 여 hello `blkid` hello 새로운 파일 시스템에 대 한 유틸리티 toodetermine hello UUID:</span><span class="sxs-lookup"><span data-stu-id="cdc70-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="cdc70-148">텍스트 편집기에서 /etc/fstab을 열고 예를 들어 hello 새로운 파일 시스템에 대 한 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="cdc70-149">또는 **SLES 11**에 대해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="cdc70-150">그런 다음, /etc/fstab를 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="cdc70-151">해당 hello /etc 테스트/fstab 입력 한 내용이 올바른지:</span><span class="sxs-lookup"><span data-stu-id="cdc70-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="cdc70-152">이 명령은 오류 메시지에 결과가 hello /etc/fstab 파일에서 hello 구문을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cdc70-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="cdc70-153">그런 다음 실행 하는 hello `mount` 명령 tooensure hello 파일 시스템은 탑재:</span><span class="sxs-lookup"><span data-stu-id="cdc70-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="cdc70-154">(선택 사항) Failsafe 부팅 매개 변수</span><span class="sxs-lookup"><span data-stu-id="cdc70-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="cdc70-155">**fstab 구성**</span><span class="sxs-lookup"><span data-stu-id="cdc70-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="cdc70-156">많은 배포판에 포함 하거나 hello `nobootwait` 또는 `nofail` 파일 toohello/등/fstab 추가할 수 있는 매개 변수를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="cdc70-157">이러한 매개 변수를 특정 파일 시스템을 탑재 하는 경우 오류에 대 한 허용 경우에 없습니다 tooproperly 탑재 hello RAID 파일 시스템 hello Linux 시스템 toocontinue tooboot을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="cdc70-158">이러한 매개 변수에 대 한 자세한 내용은 tooyour 분포의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cdc70-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="cdc70-159">예제(Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="cdc70-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="cdc70-160">**Linux 부팅 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="cdc70-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="cdc70-161">매개 변수 위에 추가 toohello에서 커널 매개 변수를 hello "`bootdegraded=true`" hello RAID 것으로 인식 됩니다 손상 되거나 예를 들어 hello 가상 컴퓨터에서 데이터 드라이브를 실수로 제거한 경우 성능이 저하 된 경우에 시스템 tooboot hello를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="cdc70-162">기본적으로 이 매개 변수는 시스템이 부팅할 수 없게 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="cdc70-163">Tooproperly 커널 매개 변수를 편집 하는 방법에 대 한 tooyour 분포의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cdc70-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="cdc70-164">예를 들어 많은 배포 (CentOS, Oracle Linux, SLES 11)에서 이러한 매개 변수에 추가할 수 있습니다 수동으로 toohello "`/boot/grub/menu.lst`" 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="cdc70-165">Ubuntu이 매개이 변수에 추가할 수 있습니다 toohello `GRUB_CMDLINE_LINUX_DEFAULT` 에 변수 "/ 등/기본/grub"입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="cdc70-166">TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="cdc70-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="cdc70-167">일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="cdc70-168">이러한 작업은 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에서 주로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="cdc70-169">큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="cdc70-170">RAID는 hello 배열에 대 한 hello 청크 크기 (512KB) hello 기본값과 tooless 설정 된 경우 취소 명령을 실행 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="cdc70-171">Hello 매핑 해제 때문에 이것이 hello 호스트에 대 한 세분성 512KB 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="cdc70-172">Mdadm의 통해 hello 배열 청크 크기를 수정 하는 경우 `--chunk=` hello 커널이 매개 변수를 다음 TRIM/매핑 해제 요청을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="cdc70-173">두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="cdc70-174">일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cdc70-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="cdc70-175">사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:</span><span class="sxs-lookup"><span data-stu-id="cdc70-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="cdc70-176">일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc70-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="cdc70-177">Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:</span><span class="sxs-lookup"><span data-stu-id="cdc70-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="cdc70-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="cdc70-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="cdc70-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="cdc70-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
