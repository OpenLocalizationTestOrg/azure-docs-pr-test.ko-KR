---
title: "Azure CLI를 사용하여 Linux VM에 디스크 추가 | Microsoft Docs"
description: "Azure CLI 1.0과 2.0을 사용하여 Linux VM에 영구 디스크를 추가하는 방법 알아보기"
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
ms.openlocfilehash: 185dd276cd79cb7053605d651e8ecdc7fd1e7636
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-disk-to-a-linux-vm"></a>Linux VM에 디스크 추가
이 문서에는 유지 관리 또는 크기 조정으로 인해 VM이 다시 프로비전되더라도 데이터를 유지할 수 있도록 VM에 영구 디스크를 연결하는 방법을 보여 줍니다. 

## <a name="quick-commands"></a>빠른 명령
다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`에 `50`GB 디스크를 연결합니다.

관리되는 디스크를 사용하려면:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

관리되지 않는 디스크를 사용하려면:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>관리되는 디스크 연결

관리되는 디스크를 사용하면 Azure Storage 계정에 대한 걱정 없이 VM 및 해당 디스크에 집중할 수 있습니다. 관리되는 디스크를 신속하게 만들고 동일한 Azure 리소스 그룹을 사용하는 VM에 연결하거나 원하는 수의 디스크를 만들고 연결할 수 있습니다.


### <a name="attach-a-new-disk-to-a-vm"></a>VM에 새 디스크 연결

VM에 새 디스크가 필요한 경우 `az vm disk attach` 명령을 사용할 수 있습니다.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>기존 디스크 연결 

대부분의 경우에서 이미 생성된 디스크를 연결합니다. 먼저 디스크 ID를 찾은 다음 `az vm disk attach` 명령에 전달합니다. 다음 예제는 `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`으로 만든 디스크를 사용합니다.

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

출력은 다음과 같이 보입니다(모든 명령에 `-o table` 옵션을 사용하여 출력을 서식 지정할 수 있음).

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


## <a name="attach-an-unmanaged-disk"></a>관리되지 않는 디스크 연결

VM과 동일한 저장소 계정에 디스크를 만들어도 상관없는 경우 새 디스크 연결은 신속합니다. `azure vm disk attach-new`를 입력하여 VM에 대한 새 GB 디스크를 만들어 연결합니다. 저장소 계정을 명시적으로 식별하지 않는 경우 만드는 모든 디스크가 OS 디스크가 있는 동일한 저장소 계정에 배치됩니다. 다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`에 `50`GB 디스크를 연결합니다.

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a>Linux VM에 연결하여 새 디스크 탑재
> [!NOTE]
> 이 항목에서는 사용자 이름 및 암호를 사용하여 VM에 연결합니다. 공용 및 개인 키 쌍을 사용하여 VM과 통신하려면 [Azure에서 Linux와 함께 SSH를 사용하는 방법](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요. 
> 
> 

Linux VM에서 사용할 수 있도록 새 디스크를 파티션, 포맷 및 탑재하기 위해 Azure VM에 SSH해야 합니다. **ssh**를 사용하여 연결하는 데 익숙하지 않을 경우 명령은 `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`의 형식으로 다음과 유사하게 표시됩니다.

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

출력

```bash
The authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) to the list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

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

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ops@myVM:~$
```

VM에 연결했으므로 디스크를 연결할 준비가 되었습니다.  먼저 `dmesg | grep SCSI`를 사용하여 디스크를 찾습니다(새 디스크를 찾는 데 사용하는 방법은 다를 수 있습니다). 이 경우, 다음과 유사하게 표시됩니다.

```bash
dmesg | grep SCSI
```

출력

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

이 항목의 경우에서 `sdc` 디스크는 우리가 원하는 디스크입니다. 이제 `sudo fdisk /dev/sdc`로 디스크를 파티션하고 사용자의 경우에서 디스크는 `sdc`이며, 파티션 1에 기본 디스크를 작성하고 다른 기본값을 적용하는 것으로 가정합니다.

```bash
sudo fdisk /dev/sdc
```

출력

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

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

프롬프트에서 `p`를 입력하여 파티션을 만듭니다.

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
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

**mkfs** 명령을 사용하고, 파일 시스템 형식 및 장치 이름을 지정하여 파티션에 파일 시스템을 작성합니다. 이 항목에서 위의 `ext4` 및 `/dev/sdc1`을 사용합니다.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

출력

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
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

이제 `mkdir`을 사용하여 파일 시스템을 탑재할 디렉터리를 만듭니다.

```bash
sudo mkdir /datadrive
```

`mount`을 사용하여 디렉터리를 탑재합니다.

```bash
sudo mount /dev/sdc1 /datadrive
```

이제 데이터 디스크는 `/datadrive`로 사용할 준비가 되었습니다.

```bash
ls
```

출력

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

다시 부팅 후 드라이브가 자동으로 다시 탑재되도록 하려면 /etc/fstab 파일에 추가해야 합니다. 또한 /etc/fstab에 UUID(Universally Unique IDentifier)를 사용하여 장치 이름(예: `/dev/sdc1`) 대신 드라이브를 가리키는 것이 좋습니다. 부팅하는 동안 OS에서 디스크 오류를 검색하는 경우 UUID를 사용하여 지정된 위치에 탑재되어 있는 잘못된 디스크를 회피합니다. 그런 다음 남아 있는 데이터 디스크를 동일한 장치 ID에 할당합니다. 새 드라이브의 UUID를 찾으려면 **blkid** 유틸리티를 사용합니다.

```bash
sudo -i blkid
```

다음과 유사하게 출력됩니다.

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> **/etc/fstab** 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다. 확실하지 않은 경우 배포 설명서에서 이 파일을 제대로 편집하는 방법에 대한 자세한 내용을 확인하세요. 또한 편집하기 전에 /etc/fstab 파일의 백업을 만드는 것이 좋습니다.
> 
> 

다음으로, 텍스트 편집기에서 **/etc/fstab** 파일을 엽니다.

```bash
sudo vi /etc/fstab
```

이 예제에서는 이전 단계에서 만든 새 **/dev/sdc1** 장치의 UUID 값과 탑재 지점 **/datadrive**를 사용합니다. **/etc/fstab** 파일의 끝에 다음 줄을 추가합니다.

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> 나중에 fstab을 편집하지 않고 데이터 디스크를 제거하면 VM이 부팅되지 않을 수 있습니다. 대부분의 배포는 `nofail` 및/또는 `nobootwait` fstab 옵션을 제공합니다. 이러한 옵션을 사용하면 디스크가 부팅 시 탑재되지 않더라도 시스템을 부팅할 수 있습니다. 이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.
> 
> **nofail** 옵션은 파일 시스템이 손상되었거나 디스크가 부팅 시 존재하지 않더라도 VM이 시작되도록 합니다. 이 옵션이 없으면 [FSTAB 오류로 인해 Linux에 SSH를 사용할 수 없음](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)(영문)에 설명되어 있는 동작이 발생할 수 있습니다.

### <a name="trimunmap-support-for-linux-in-azure"></a>Azure에서 Linux에 대한 TRIM/UNMAP 지원
일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM/UNMAP 작업을 지원합니다. 이것은 Azure에 삭제된 페이지가 더 이상 유효하지 않으며 폐기될 수 있음을 알리는 데 표준 저장소에서 주로 유용합니다. 큰 파일을 만들고 삭제하는 경우 이렇게 하면 비용을 절감할 수 있습니다.

Linux VM에서 TRIM 지원을 사용하는 두 가지 방법이 있습니다. 평소와 같이 권장되는 방법에 대해 배포에 확인하세요.

* `/etc/fstab`에 `discard` 탑재 옵션을 사용합니다. 예:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* 일부 경우 `discard` 옵션에는 성능이 저하 될 수 있습니다. 또는 `fstrim` 명령을 명령줄에서 수동으로 실행하거나, 또는 정기적으로 실행하기 위해 crontab에 추가할 수 있습니다.
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>문제 해결
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>다음 단계
* 해당 정보를 [fstab](http://en.wikipedia.org/wiki/Fstab) 파일에 쓰지 않았는데 다시 부팅하면 새 디스크를 VM에 사용할 수 없게 됩니다.
* Linux VM을 올바르게 구성했는지 확인하려면 [Linux 컴퓨터 성능 최적화](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 권장 사항을 검토합니다.
* 디스크를 추가하여 저장소 용량을 확장하고 추가 성능이 필요할 경우 [RAID를 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

