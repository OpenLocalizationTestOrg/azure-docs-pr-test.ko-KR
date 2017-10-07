---
title: "Linux를 실행 하는 가상 컴퓨터에서 LVM aaaConfigure | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure LVM Azure에서 linux."
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
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="c4c97-103">Azure에서 Linux VM에 LVM 구성</span><span class="sxs-lookup"><span data-stu-id="c4c97-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="c4c97-104">이 문서에 설명 합니다 어떻게 Azure 가상 컴퓨터의 논리 볼륨 관리자 (LVM) tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="c4c97-105">가능한 tooconfigure LVM 모든 디스크에 연결 된 toohello 가상 컴퓨터를 기본적으로 이미지는 대부분 클라우드 동안 LVM OS 디스크를 hello에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="c4c97-106">OS 디스크는 현재까지 hello tooanother hello의 VM을 연결 하는 경우이 중복 된 볼륨 그룹에 tooprevent 문제가 동일 하 게 분산 및 복구 시나리오 중 즉, 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="c4c97-107">따라서 hello 데이터 디스크에 LVM을 toouse만 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="c4c97-108">선형 및 스트라이프 논리 볼륨 비교</span><span class="sxs-lookup"><span data-stu-id="c4c97-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="c4c97-109">LVM 사용된 toocombine 다양 한 단일 저장소 볼륨에 실제 디스크 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="c4c97-110">기본적으로 LVM 일반적으로 만들어집니다 선형 논리 볼륨을 의미 하는 hello 실제 저장소 서로 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="c4c97-111">이 경우 읽기/쓰기 작업은 일반적으로 전송 되 tooa 단일 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="c4c97-112">반면, 여기서 읽기 및 쓰기는 hello 볼륨 그룹 (예: 유사한 tooRAID0)에 포함 된 분산된 toomultiple 디스크 스트라이프 논리 볼륨 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="c4c97-113">성능상의 이유로 될 것이 좋습니다 toostripe 논리 볼륨 읽기 및 쓰기가 모든 연결 된 데이터 디스크를 활용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="c4c97-114">이 문서에서는 어떻게 toocombine 여러 데이터 디스크를 단일 볼륨 그룹에 설명 하 고 스트라이프 논리 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="c4c97-115">hello 단계 아래에 대부분 분포와 함께 다소 일반화 toowork 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="c4c97-116">대부분의 경우 hello 유틸리티와 Azure에서 LVM 관리에 대 한 워크플로 높지 않습니다 다른 환경에 비해 근본적으로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="c4c97-117">늘 그렇듯이 특정 배포로 LVM을 사용하는 설명서 및 모범 사례의 경우 Linux 공급업체에도 문의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="c4c97-118">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="c4c97-118">Attaching data disks</span></span>
<span data-ttu-id="c4c97-119">일반적으로 LVM를 사용 하는 경우 두 개 이상의 빈 데이터 디스크와 toostart를 합니다는 하나.</span><span class="sxs-lookup"><span data-stu-id="c4c97-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="c4c97-120">IO 요구 사항에 따라, 디스크 또는 디스크 당 too5000 IO/ps를 우리의 프리미엄 저장소와 당 too500 IO/ps를와 우리의 표준 저장소에 저장 된 tooattach 디스크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="c4c97-121">이 문서는 방법에 정보를 확인할 전환 되지 것입니다 tooprovision 및 데이터 디스크 tooa Linux 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="c4c97-122">참조 하십시오 hello Microsoft Azure 문서 [디스크 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 어떻게 tooattach 빈 데이터 디스크 tooa Linux 가상 컴퓨터에서 Azure에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="c4c97-123">Hello LVM 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="c4c97-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="c4c97-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="c4c97-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="c4c97-125">**RHEL, CentOS 및 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="c4c97-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="c4c97-126">**SLES 12 및 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="c4c97-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="c4c97-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="c4c97-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="c4c97-128">SLES11에서 편집 해야 `/etc/sysconfig/lvm` 설정 `LVM_ACTIVATED_ON_DISCOVERED` 너무 "사용":</span><span class="sxs-lookup"><span data-stu-id="c4c97-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="c4c97-129">LVM 구성</span><span class="sxs-lookup"><span data-stu-id="c4c97-129">Configure LVM</span></span>
<span data-ttu-id="c4c97-130">이 가이드 가정 지칭 3 개의 데이터 디스크를 연결 상태 tooas `/dev/sdc`, `/dev/sdd` 및 `/dev/sde`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="c4c97-131">하지 있습니다 이러한 항상 hello을 VM에서 동일한 경로 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="c4c97-132">실행할 수 있습니다 '`sudo fdisk -l`' 또는 유사한 명령 toolist 사용 가능한 디스크.</span><span class="sxs-lookup"><span data-stu-id="c4c97-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="c4c97-133">Hello 실제 볼륨을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="c4c97-134">볼륨 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-134">Create a volume group.</span></span> <span data-ttu-id="c4c97-135">이 예제에서는 호출 하는 hello 볼륨 그룹 `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="c4c97-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="c4c97-136">Hello 논리 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-136">Create hello logical volume(s).</span></span> <span data-ttu-id="c4c97-137">hello 명령에서는 아래 만들어집니다 라는 단일 논리 볼륨 `data-lv01` toospan hello 전체 볼륨 그룹을 참고 하는 것도 가능 toocreate 하지만 hello 볼륨 그룹에 여러 논리 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="c4c97-138">Hello 논리 볼륨 포맷</span><span class="sxs-lookup"><span data-stu-id="c4c97-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="c4c97-139">SLES11에서는 ext4가 아닌 `-t ext3`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="c4c97-140">SLES11만 읽기 전용 액세스 tooext4 파일 시스템을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="c4c97-141">Hello 새 파일 시스템 너무/등/fstab 추가</span><span class="sxs-lookup"><span data-stu-id="c4c97-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c4c97-142">Hello를 잘못 편집 `/etc/fstab` 파일 경우 시스템 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="c4c97-143">를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4c97-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="c4c97-144">또한 hello 백업 하는 권장 `/etc/fstab` 편집 하기 전에 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="c4c97-145">예를 들어 새로운 파일 시스템에 대 한 원하는 hello 탑재 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="c4c97-146">Hello 논리 볼륨 경로 찾기</span><span class="sxs-lookup"><span data-stu-id="c4c97-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="c4c97-147">열기 `/etc/fstab` 텍스트 편집기에서 예를 들어 hello 새로운 파일 시스템에 대 한 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="c4c97-148">`/etc/fstab`을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="c4c97-149">해당 hello 테스트 `/etc/fstab` 입력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="c4c97-150">이 명령은, 오류 메시지를 발생 하는 경우 hello에 hello 구문을 확인 하십시오 `/etc/fstab` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="c4c97-151">그런 다음 실행 하는 hello `mount` 명령 tooensure hello 파일 시스템은 탑재:</span><span class="sxs-lookup"><span data-stu-id="c4c97-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="c4c97-152">(선택 사항) `/etc/fstab`의 Failsafe 부팅 매개 변수</span><span class="sxs-lookup"><span data-stu-id="c4c97-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="c4c97-153">많은 배포판에 포함 하거나 hello `nobootwait` 또는 `nofail` toohello 추가할 수 있는 매개 변수를 탑재 `/etc/fstab` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="c4c97-154">이러한 매개 변수를 특정 파일 시스템을 탑재 하는 경우 오류에 대 한 허용 경우에 없습니다 tooproperly 탑재 hello RAID 파일 시스템 hello Linux 시스템 toocontinue tooboot을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="c4c97-155">이러한 매개 변수에 대 한 자세한 내용은 tooyour 분포의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4c97-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="c4c97-156">예제(Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="c4c97-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="c4c97-157">TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="c4c97-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="c4c97-158">일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="c4c97-159">이러한 작업은 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에서 주로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="c4c97-160">큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="c4c97-161">두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="c4c97-162">일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4c97-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="c4c97-163">사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:</span><span class="sxs-lookup"><span data-stu-id="c4c97-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="c4c97-164">일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c97-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="c4c97-165">Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:</span><span class="sxs-lookup"><span data-stu-id="c4c97-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="c4c97-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="c4c97-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="c4c97-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="c4c97-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
