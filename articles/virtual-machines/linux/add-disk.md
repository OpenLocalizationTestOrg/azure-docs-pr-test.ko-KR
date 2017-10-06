---
title: "사용 하 여 디스크 tooLinux VM aaaAdd hello Azure CLI | Microsoft Docs"
description: "Tooadd hello Azure CLI 1.0 및 2.0 영구 디스크 tooyour Linux VM에 알아봅니다."
keywords: "Linux 가상 컴퓨터, 리소스 디스크 추가"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="7c640-104">디스크 tooa Linux VM 추가</span><span class="sxs-lookup"><span data-stu-id="7c640-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="7c640-105">이 문서에서는 어떻게 tooattach는 영구 디스크 tooyour VM-데이터를 유지할 수 있도록 VM 기한 toomaintenance 또는 크기 조정 다시 프로 비전 되는 경우에 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="7c640-106">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="7c640-106">Quick Commands</span></span>
<span data-ttu-id="7c640-107">다음 예에서는 연결 hello는 `50`GB 디스크 toohello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7c640-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="7c640-108">관리 되는 toouse 디스크:</span><span class="sxs-lookup"><span data-stu-id="7c640-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="7c640-109">관리 되지 않는 toouse 디스크:</span><span class="sxs-lookup"><span data-stu-id="7c640-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="7c640-110">관리되는 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="7c640-110">Attach a managed disk</span></span>

<span data-ttu-id="7c640-111">관리 되는 디스크를 사용 하 여 사용 하면 toofocus Vm 및 디스크에서 Azure 저장소 계정에 대 한 걱정 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="7c640-112">신속 하 게 만들어 하는 관리 되는 디스크 연결 같은 Azure 리소스 그룹 hello 사용 하 여 tooa VM 또는 개수에 관계 없이 디스크를 만들고 다음 첨부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="7c640-113">새 디스크 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="7c640-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="7c640-114">VM에 새 디스크만 하면 hello를 사용할 수 있습니다 `az vm disk attach` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="7c640-115">기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="7c640-115">Attach an existing disk</span></span> 

<span data-ttu-id="7c640-116">대부분의 경우에서 이미 생성된 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="7c640-117">먼저 hello 디스크 id를 찾아 그런 다음 해당 toohello `az vm disk attach` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="7c640-118">hello 다음 예제에서는 디스크를 사용 하는 사용 하 여 만든 `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="7c640-119">hello 다음과 같은 출력 hello 다음 (hello를 사용할 수 있습니다 `-o table` tooany 명령 tooformat hello 출력에 옵션):</span><span class="sxs-lookup"><span data-stu-id="7c640-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="7c640-120">관리되지 않는 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="7c640-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="7c640-121">새 디스크 연결를 신속 하 게 hello에서 디스크를 만드는 해도 경우 VM와 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="7c640-122">형식 `azure vm disk attach-new` toocreate 및 VM에 대 한 새 GB 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="7c640-123">저장소 계정을 명시적으로 식별 하지 않는 경우 작성 하는 모든 디스크에에서 배치 됩니다 hello 동일한 운영 체제 디스크에 상주 하는 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="7c640-124">다음 예에서는 연결 hello는 `50`GB 디스크 toohello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7c640-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="7c640-125">Toohello Linux VM toomount hello에 대 한 새 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="7c640-126">이 항목 연결 tooa VM 사용자 이름 및 암호를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="7c640-127">VM와 공용 및 개인 키 쌍 toocommunicate toouse 참조 [어떻게 tooUse와 Azure에서 Linux에 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="7c640-128">TooSSH 필요 하면 Azure VM toopartition에 서식을 지정 하 고 Linux VM에서 사용할 수 있도록 새 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="7c640-129">사용 하 여 연결에 대해 잘 알고 모르겠으면 **ssh**, hello 명령에서는 hello 양식 `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, 다음과 같은 hello 및:</span><span class="sxs-lookup"><span data-stu-id="7c640-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="7c640-130">출력</span><span class="sxs-lookup"><span data-stu-id="7c640-130">Output</span></span>

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="7c640-131">연결 된 했으므로 이제 tooyour VM 수 tooattach 디스크.</span><span class="sxs-lookup"><span data-stu-id="7c640-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="7c640-132">Hello를 찾으려면 먼저 디스크에 사용 하 여 `dmesg | grep SCSI` (hello 메서드 사용 toodiscover 새 디스크에 따라 달라질 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="7c640-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="7c640-133">이 경우, 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="7c640-134">출력</span><span class="sxs-lookup"><span data-stu-id="7c640-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="7c640-135">이 항목의 경우 hello hello 및 `sdc` 디스크는 hello 하나 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="7c640-136">지금 파티션에 hello 디스크 `sudo fdisk /dev/sdc` 프로그램 사례 hello에 디스크를 가정할- `sdc`, 주 디스크 파티션 1에 수행 하 고 동의 hello 다른 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="7c640-137">출력</span><span class="sxs-lookup"><span data-stu-id="7c640-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

<span data-ttu-id="7c640-138">입력 하 여 hello 파티션을 만들 `p` hello 프롬프트에서:</span><span class="sxs-lookup"><span data-stu-id="7c640-138">Create hello partition by typing `p` at hello prompt:</span></span>

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

<span data-ttu-id="7c640-139">Hello를 사용 하 여 파일 시스템 toohello 파티션을 작성 및 **mkfs** 명령, 파일 시스템 형식 및 hello 장치 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="7c640-140">이 항목에서 위의 `ext4` 및 `/dev/sdc1`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="7c640-141">출력</span><span class="sxs-lookup"><span data-stu-id="7c640-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

<span data-ttu-id="7c640-142">이제 디렉터리 toomount hello 시스템 사용 하는 파일을 만들 것 `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="7c640-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="7c640-143">Hello 디렉터리를 사용 하 여 탑재 `mount`:</span><span class="sxs-lookup"><span data-stu-id="7c640-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="7c640-144">hello 데이터 디스크가 현재으로 준비 toouse `/datadrive`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="7c640-145">출력</span><span class="sxs-lookup"><span data-stu-id="7c640-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="7c640-146">tooensure hello 드라이브 toohello /etc/fstab 파일을 추가 하는 다시 부팅 해야 자동으로 다시 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="7c640-147">또한 좋습니다 hello UUID (전체적으로 Unique IDentifier)는 /etc/fstab toorefer toohello 정당한 hello 장치 16 진수 드라이브 (예: `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="7c640-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="7c640-148">Hello OS가 부팅 하는 동안 디스크 오류를 발견 하는 경우 hello UUID를 사용 하 여 hello 잘못 된 디스크를 위치를 받아야 하는 탑재 된 tooa 되 고 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="7c640-149">그런 다음 남아 있는 데이터 디스크를 동일한 장치 ID에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="7c640-150">toofind hello 새 드라이브의 UUID hello, hello를 사용 하 여 **blkid** 유틸리티:</span><span class="sxs-lookup"><span data-stu-id="7c640-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="7c640-151">hello 출력은 toohello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="7c640-152">Hello를 잘못 편집 **/등/fstab** 파일 경우 시스템 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="7c640-153">를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7c640-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="7c640-154">또한 편집 하기 전에 hello /etc/fstab 파일의 백업을 만들어졌는지 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="7c640-155">Hello을 열고 **/등/fstab** 파일 텍스트 편집기에서:</span><span class="sxs-lookup"><span data-stu-id="7c640-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="7c640-156">이 예제에서 사용 하 여 hello UUID 값 hello에 대 한 새 **/개발/sdc1** hello 탑재 지점 및 hello 이전 단계에서 만든 장치 **/datadrive**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="7c640-157">줄 toohello의 끝 다음 hello hello 추가 **/등/fstab** 파일:</span><span class="sxs-lookup"><span data-stu-id="7c640-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="7c640-158">나중에 fstab 편집 하지 않고도 데이터 디스크를 제거 하는 hello VM toofail tooboot을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="7c640-159">대부분의 배포판 제공 하거나 hello `nofail` 및/또는 `nobootwait` fstab 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="7c640-160">이 옵션을 부팅 시 toomount hello 디스크에 오류가 발생 하는 경우에 시스템 tooboot을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="7c640-161">이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c640-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="7c640-162">hello **nofail** 옵션을 선택 하면 해당 hello hello 파일 시스템 손상 되었거나 hello 디스크 부팅 시 존재 하지 않는 경우에 VM을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="7c640-163">이 옵션이 없으면 발생할 수에 설명 된 대로 동작 [없습니다 SSH tooLinux VM tooFSTAB 오류 기한](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="7c640-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="7c640-164">Azure에서 Linux에 대한 TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="7c640-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="7c640-165">일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="7c640-166">표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에 주로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="7c640-167">큰 파일을 만들고 삭제하는 경우 이렇게 하면 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="7c640-168">두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="7c640-169">일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7c640-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="7c640-170">사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:</span><span class="sxs-lookup"><span data-stu-id="7c640-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="7c640-171">일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="7c640-172">Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:</span><span class="sxs-lookup"><span data-stu-id="7c640-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="7c640-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7c640-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="7c640-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="7c640-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="7c640-175">문제 해결</span><span class="sxs-lookup"><span data-stu-id="7c640-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="7c640-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c640-176">Next Steps</span></span>
* <span data-ttu-id="7c640-177">기억 새 디스크에 없는 것 사용할 수 있는 toohello VM 해당 정보 tooyour를 작성 하지 않는 경우 다시 부팅 [fstab](http://en.wikipedia.org/wiki/Fstab) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="7c640-178">Linux VM은 tooensure 올바르게 구성 검토 hello [Linux 컴퓨터 성능 최적화](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="7c640-179">디스크를 추가하여 저장소 용량을 확장하고 추가 성능이 필요할 경우 [RAID를 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c640-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

