---
title: "Linux를 실행하는 가상 컴퓨터에 소프트웨어 RAID 구성 | Microsoft Docs"
description: "mdadm을 사용하여 Azure에서 Linux에 대해 RAID를 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="a1c31-103">Linux에서 소프트웨어 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="a1c31-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="a1c31-104">Azure에서 Linux 가상 컴퓨터의 소프트웨어 RAID를 사용하여 연결된 여러 데이터 디스크를 단일 RAID 장치로 나타내는 것이 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="a1c31-105">일반적으로 이 시나리오는 단일 디스크만 사용하는 경우와 비교하여 성능을 개선하고 처리량을 향상하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="a1c31-106">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="a1c31-106">Attaching data disks</span></span>
<span data-ttu-id="a1c31-107">RAID 장치를 구성하는 데 두 개 이상의 빈 데이터 디스크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="a1c31-108">RAID 장치를 만드는 주된 이유는 디스크 IO의 성능을 개선하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="a1c31-109">IO 요구 사항에 따라 표준 저장소에 저장된 디스크(디스크당 최대 500IO/ps) 또는 프리미엄 저장소에 저장된 디스크(디스크당 최대 5000IO/ps)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="a1c31-110">Linux 가상 컴퓨터에 데이터 디스크를 프로비전 및 연결하는 방법은 이 문서에서 자세히 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="a1c31-111">Azure에서 빈 데이터 디스크를 Linux 가상 컴퓨터에 연결하는 방법에 대한 자세한 내용은 Microsoft Azure 문서 [디스크 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1c31-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="a1c31-112">mdadm 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="a1c31-112">Install the mdadm utility</span></span>
* <span data-ttu-id="a1c31-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="a1c31-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="a1c31-114">**CentOS 및 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="a1c31-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="a1c31-115">**SLES 및 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="a1c31-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="a1c31-116">디스크 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="a1c31-116">Create the disk partitions</span></span>
<span data-ttu-id="a1c31-117">이 예에서는 /dev/sdc에 단일 디스크 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="a1c31-118">/dev/sdc1이라는 새 디스크 파티션을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="a1c31-119">`fdisk`를 시작하여 파티션 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="a1c31-120">키를 눌러 만들려는 프롬프트에서 ' n '는  **n** 우 파티션:</span><span class="sxs-lookup"><span data-stu-id="a1c31-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="a1c31-121">'p'를 눌러 주( **p**rimary) 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="a1c31-122">'1'을 눌러 파티션 번호 1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="a1c31-123">새 파티션의 시작 지점을 선택하거나 `<enter>` 키를 눌러 드라이브의 가용 공간 시작 부분에 파티션을 배치하는 기본값을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="a1c31-124">파티션 크기를 선택합니다. 예를 들어 10기가바이트 파티션을 만들려면 '+10G'를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="a1c31-125">또는 `<enter>` 키를 눌러 범위가 전체 드라이브인 단일 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="a1c31-126">그런 다음, 파티션의 ID 및 유형( **t**ype)을 기본 ID '83'(Linux)에서 ID 'fd'(Linux raid auto)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="a1c31-127">마지막으로, 드라이브에 파티션 테이블을 쓰고 fdisk를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="a1c31-128">RAID 배열 만들기</span><span class="sxs-lookup"><span data-stu-id="a1c31-128">Create the RAID array</span></span>
1. <span data-ttu-id="a1c31-129">다음 예는 3개의 별도 데이터 디스크(sdc1, sdd1, sde1)에 위치한 3개의 파티션을 "스트라이프"합니다(RAID 수준 0).</span><span class="sxs-lookup"><span data-stu-id="a1c31-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="a1c31-130">이 명령을 실행하면 **/dev/md127** 이라는 새 RAID 장치가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="a1c31-131">이 데이터 디스크가 이전에 작동하지 않는 다른 RAID 배열의 일부였다면 `--force` 매개 변수를 `mdadm` 명령에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="a1c31-132">새 RAID 장치에서 파일 시스템 만들기</span><span class="sxs-lookup"><span data-stu-id="a1c31-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="a1c31-133">a.</span><span class="sxs-lookup"><span data-stu-id="a1c31-133">a.</span></span> <span data-ttu-id="a1c31-134">**CentOS, Oracle Linux, SLES 12, openSUSE 및 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="a1c31-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="a1c31-135">b.</span><span class="sxs-lookup"><span data-stu-id="a1c31-135">b.</span></span> <span data-ttu-id="a1c31-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="a1c31-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="a1c31-137">c.</span><span class="sxs-lookup"><span data-stu-id="a1c31-137">c.</span></span> <span data-ttu-id="a1c31-138">**SLES 11** - boot.md 사용 및 mdadm.conf 만들기</span><span class="sxs-lookup"><span data-stu-id="a1c31-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a1c31-139">SUSE 시스템에서 이렇게 변경한 후에는 다시 부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="a1c31-140">SLES 12에서는 이 단계가 필요하지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="a1c31-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="a1c31-141">/etc/fstab에 새 파일 시스템 추가</span><span class="sxs-lookup"><span data-stu-id="a1c31-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a1c31-142">/etc/fstab 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="a1c31-143">확실하지 않은 경우 배포 설명서에서 이 파일을 제대로 편집하는 방법에 대한 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a1c31-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="a1c31-144">또한 편집하기 전에 /etc/fstab 파일의 백업을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="a1c31-145">새 파일 시스템용으로 원하는 탑재 지점을 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="a1c31-146">/etc/fstab를 편집할 때는 파일 시스템을 참조하는 데 장치 이름 대신 **UUID** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="a1c31-147">`blkid` 유틸리티를 사용하여 새 파일 시스템의 UUID를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="a1c31-148">텍스트 편집기에서 /etc/fstab을 열고 예를 들어 다음과 같이 새 파일 시스템에 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="a1c31-149">또는 **SLES 11**에 대해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="a1c31-150">그런 다음, /etc/fstab를 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="a1c31-151">/etc/fstab 항목이 올바른지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="a1c31-152">이 명령 결과 오류 메시지가 발생하는 경우 /etc/fstab 파일에서 구문을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a1c31-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="a1c31-153">그런 다음, `mount` 명령을 실행하여 파일 시스템이 탑재되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="a1c31-154">(선택 사항) Failsafe 부팅 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a1c31-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="a1c31-155">**fstab 구성**</span><span class="sxs-lookup"><span data-stu-id="a1c31-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="a1c31-156">많은 배포에는 /etc/fstab 파일에 추가할 수 있는 `nobootwait` 또는 `nofail` 탑재 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="a1c31-157">이 매개 변수는 특정 파일 시스템 탑재 시 오류를 허용하며 Linux 시스템이 제대로 RAID 파일 시스템을 탑재할 수 없는 경우에도 계속 부팅되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="a1c31-158">이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="a1c31-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="a1c31-159">예제(Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="a1c31-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="a1c31-160">**Linux 부팅 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="a1c31-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="a1c31-161">위의 매개 변수 외에, 커널 매개 변수 "`bootdegraded=true`"는 RAID가 손상 또는 저하된 것으로 인식되는 경우에도(예: 데이터 드라이브가 실수로 가상 컴퓨터에서 제거된 경우) 시스템이 부팅되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="a1c31-162">기본적으로 이 매개 변수는 시스템이 부팅할 수 없게 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="a1c31-163">커널 매개 변수를 올바르게 편집하는 방법에 대해서는 배포 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="a1c31-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="a1c31-164">예를 들어 CentOS, Oracle Linux, SLES 11 등 많은 배포에서 이 매개 변수를 "`/boot/grub/menu.lst`" 파일에 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="a1c31-165">Ubuntu에서는 "/etc/default/grub"의 `GRUB_CMDLINE_LINUX_DEFAULT` 변수에 이 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="a1c31-166">TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="a1c31-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="a1c31-167">일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM/UNMAP 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="a1c31-168">이러한 작업은 Azure에 삭제된 페이지가 더 이상 유효하지 않으며 폐기될 수 있음을 알리는 데 표준 저장소에서 주로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="a1c31-169">큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="a1c31-170">배열에 대한 청크 크기가 기본값(512KB)보다 작은 값으로 설정된 경우, RAID는 취소 명령을 실행하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="a1c31-171">호스트에서의 unmap 세분성도 512KB이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="a1c31-172">mdadm의 `--chunk=` 매개 변수를 통해 배열의 청크 크기를 수정하는 경우, TRIM/매핑 해제 요청이 커널에서 무시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="a1c31-173">Linux VM에서 TRIM 지원을 사용하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="a1c31-174">평소와 같이 권장되는 방법에 대해 배포에 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a1c31-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="a1c31-175">`/etc/fstab`에 `discard` 탑재 옵션을 사용합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="a1c31-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="a1c31-176">일부 경우 `discard` 옵션에는 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="a1c31-177">또는 `fstrim` 명령을 명령줄에서 수동으로 실행하거나, 또는 정기적으로 실행하기 위해 crontab에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c31-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="a1c31-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="a1c31-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="a1c31-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="a1c31-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
