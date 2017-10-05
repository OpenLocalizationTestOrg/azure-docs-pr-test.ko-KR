---
title: "Linux를 실행하는 가상 컴퓨터에 LVM 구성 | Microsoft Docs"
description: "Azure에서 Linux에 LVM을 구성하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 7926627aaa3f0da935131f491d927ab5cb4b35c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="2178b-103">Azure에서 Linux VM에 LVM 구성</span><span class="sxs-lookup"><span data-stu-id="2178b-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="2178b-104">이 문서에서는 Azure 가상 컴퓨터의 LVM(논리 볼륨 관리자)을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="2178b-105">가상 컴퓨터에 연결된 모든 디스크에 LVM을 구성할 수 있지만 기본적으로 대부분의 클라우드 이미지는 OS 디스크에 LVM을 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="2178b-106">이는 OS 디스크가 동일한 배포와 형식의 다른 VM에 연결되어 있는 경우(예: 복구 시나리오 중), 중복 볼륨 그룹에 대한 문제를 방지하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="2178b-107">따라서 데이터 디스크에만 LVM을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="2178b-108">선형 및 스트라이프 논리 볼륨 비교</span><span class="sxs-lookup"><span data-stu-id="2178b-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="2178b-109">LVM을 사용하여 단일 저장소 볼륨에 여러 실제 디스크를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="2178b-110">기본적으로 LVM은 일반적으로 선형 논리 볼륨을 만듭니다. 즉, 실제 저장소가 함께 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="2178b-111">이 경우 일반적으로 읽기/쓰기 작업은 단일 디스크로만 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="2178b-112">반면 읽기 및 쓰기가 볼륨 그룹에 포함된 여러 디스크에 분산되는 스트라이프 논리 볼륨을 만들 수도 있습니다(예: RAID0과 유사함).</span><span class="sxs-lookup"><span data-stu-id="2178b-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="2178b-113">성능상의 이유로 논리 볼륨을 스트라이프하여 읽기 및 쓰기가 연결된 모든 데이터 디스크를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="2178b-114">이 문서에는 여러 개의 데이터 디스크를 단일 볼륨 그룹으로 결합한 다음 스트라이프 논리 볼륨을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="2178b-115">아래 단계는 대부분의 배포로 작업하도록 다소 일반화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="2178b-116">대부분의 경우 Azure의 LVM을 관리하기 위한 유틸리티 및 워크플로는 다른 환경과 근본적으로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="2178b-117">늘 그렇듯이 특정 배포로 LVM을 사용하는 설명서 및 모범 사례의 경우 Linux 공급업체에도 문의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="2178b-118">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="2178b-118">Attaching data disks</span></span>
<span data-ttu-id="2178b-119">하나의 디스크가 LVM을 사용하는 경우 일반적으로 두 개 이상의 빈 데이터 디스크로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="2178b-120">IO 요구 사항에 따라 표준 저장소에 저장된 디스크(디스크당 최대 500IO/ps) 또는 프리미엄 저장소에 저장된 디스크(디스크당 최대 5000IO/ps)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="2178b-121">Linux 가상 컴퓨터에 데이터 디스크를 프로비전 및 연결하는 방법은 이 문서에서 자세히 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="2178b-122">Azure에서 빈 데이터 디스크를 Linux 가상 컴퓨터에 연결하는 방법에 대한 자세한 내용은 Microsoft Azure 문서 [디스크 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2178b-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="2178b-123">LVM 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="2178b-123">Install the LVM utilities</span></span>
* <span data-ttu-id="2178b-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2178b-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="2178b-125">**RHEL, CentOS 및 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="2178b-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="2178b-126">**SLES 12 및 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="2178b-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="2178b-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="2178b-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="2178b-128">SLES11에서 `/etc/sysconfig/lvm`도 편집하고 `LVM_ACTIVATED_ON_DISCOVERED`을 "사용"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="2178b-129">LVM 구성</span><span class="sxs-lookup"><span data-stu-id="2178b-129">Configure LVM</span></span>
<span data-ttu-id="2178b-130">이 지침에서는 `/dev/sdc`, `/dev/sdd` 및 `/dev/sde`로 참조하는 세 개의 데이터 디스크가 연결되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="2178b-131">이러한 세 디스크는 VM에서 항상 동일한 경로 이름이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="2178b-132">'`sudo fdisk -l`' 또는 유사한 명령을 실행하여 사용 가능한 디스크를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="2178b-133">실제 볼륨을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="2178b-134">볼륨 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-134">Create a volume group.</span></span> <span data-ttu-id="2178b-135">이 예제에서는 볼륨 그룹 `data-vg01`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="2178b-136">논리 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-136">Create the logical volume(s).</span></span> <span data-ttu-id="2178b-137">아래 명령으로 전체 볼륨 그룹에 걸쳐 `data-lv01`이라는 단일 논리 볼륨을 만들지만, 볼륨 그룹에 여러 논리 볼륨을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="2178b-138">논리 볼륨 포맷</span><span class="sxs-lookup"><span data-stu-id="2178b-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="2178b-139">SLES11에서는 ext4가 아닌 `-t ext3`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="2178b-140">SLES11은 ext4 파일 시스템에 읽기 전용 액세스만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="2178b-141">/etc/fstab에 새 파일 시스템 추가</span><span class="sxs-lookup"><span data-stu-id="2178b-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2178b-142">`/etc/fstab` 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="2178b-143">확실하지 않은 경우 배포 설명서에서 이 파일을 제대로 편집하는 방법에 대한 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="2178b-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="2178b-144">또한 편집하기 전에 `/etc/fstab` 파일의 백업을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="2178b-145">새 파일 시스템용으로 원하는 탑재 지점을 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="2178b-146">논리 볼륨 경로 찾기</span><span class="sxs-lookup"><span data-stu-id="2178b-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="2178b-147">텍스트 편집기에서 `/etc/fstab`을 열고 예를 들어 다음과 같이 새 파일 시스템에 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="2178b-148">`/etc/fstab`을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="2178b-149">`/etc/fstab` 항목이 올바른지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="2178b-150">이 명령 결과 오류 메시지가 발생하는 경우 `/etc/fstab` 파일에서 구문을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="2178b-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="2178b-151">그런 다음, `mount` 명령을 실행하여 파일 시스템이 탑재되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="2178b-152">(선택 사항) `/etc/fstab`의 Failsafe 부팅 매개 변수</span><span class="sxs-lookup"><span data-stu-id="2178b-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="2178b-153">많은 배포에는 `/etc/fstab` 파일에 추가할 수 있는 `nobootwait` 또는 `nofail` 탑재 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="2178b-154">이 매개 변수는 특정 파일 시스템 탑재 시 오류를 허용하며 Linux 시스템이 제대로 RAID 파일 시스템을 탑재할 수 없는 경우에도 계속 부팅되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="2178b-155">이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2178b-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="2178b-156">예제(Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="2178b-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="2178b-157">TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="2178b-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="2178b-158">일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM/UNMAP 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="2178b-159">이러한 작업은 Azure에 삭제된 페이지가 더 이상 유효하지 않으며 폐기될 수 있음을 알리는 데 표준 저장소에서 주로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="2178b-160">큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="2178b-161">Linux VM에서 TRIM 지원을 사용하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="2178b-162">평소와 같이 권장되는 방법에 대해 배포에 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="2178b-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="2178b-163">`/etc/fstab`에 `discard` 탑재 옵션을 사용합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2178b-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="2178b-164">일부 경우 `discard` 옵션에는 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="2178b-165">또는 `fstrim` 명령을 명령줄에서 수동으로 실행하거나, 또는 정기적으로 실행하기 위해 crontab에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2178b-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="2178b-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2178b-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="2178b-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="2178b-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
