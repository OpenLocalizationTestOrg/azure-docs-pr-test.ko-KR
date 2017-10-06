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
# <a name="add-a-disk-tooa-linux-vm"></a>디스크 tooa Linux VM 추가
이 문서에서는 어떻게 tooattach는 영구 디스크 tooyour VM-데이터를 유지할 수 있도록 VM 기한 toomaintenance 또는 크기 조정 다시 프로 비전 되는 경우에 보여 줍니다. 

## <a name="quick-commands"></a>빠른 명령
다음 예에서는 연결 hello는 `50`GB 디스크 toohello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

관리 되는 toouse 디스크:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

관리 되지 않는 toouse 디스크:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>관리되는 디스크 연결

관리 되는 디스크를 사용 하 여 사용 하면 toofocus Vm 및 디스크에서 Azure 저장소 계정에 대 한 걱정 없이 합니다. 신속 하 게 만들어 하는 관리 되는 디스크 연결 같은 Azure 리소스 그룹 hello 사용 하 여 tooa VM 또는 개수에 관계 없이 디스크를 만들고 다음 첨부할 수 있습니다.


### <a name="attach-a-new-disk-tooa-vm"></a>새 디스크 tooa VM 연결

VM에 새 디스크만 하면 hello를 사용할 수 있습니다 `az vm disk attach` 명령입니다.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>기존 디스크 연결 

대부분의 경우에서 이미 생성된 디스크를 연결합니다. 먼저 hello 디스크 id를 찾아 그런 다음 해당 toohello `az vm disk attach` 명령입니다. hello 다음 예제에서는 디스크를 사용 하는 사용 하 여 만든 `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`합니다.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

hello 다음과 같은 출력 hello 다음 (hello를 사용할 수 있습니다 `-o table` tooany 명령 tooformat hello 출력에 옵션):

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

새 디스크 연결를 신속 하 게 hello에서 디스크를 만드는 해도 경우 VM와 동일한 저장소 계정입니다. 형식 `azure vm disk attach-new` toocreate 및 VM에 대 한 새 GB 디스크를 연결 합니다. 저장소 계정을 명시적으로 식별 하지 않는 경우 작성 하는 모든 디스크에에서 배치 됩니다 hello 동일한 운영 체제 디스크에 상주 하는 저장소 계정입니다. 다음 예에서는 연결 hello는 `50`GB 디스크 toohello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Toohello Linux VM toomount hello에 대 한 새 디스크를 연결 합니다.
> [!NOTE]
> 이 항목 연결 tooa VM 사용자 이름 및 암호를 사용 하 여 합니다. VM와 공용 및 개인 키 쌍 toocommunicate toouse 참조 [어떻게 tooUse와 Azure에서 Linux에 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 
> 
> 

TooSSH 필요 하면 Azure VM toopartition에 서식을 지정 하 고 Linux VM에서 사용할 수 있도록 새 디스크를 탑재 합니다. 사용 하 여 연결에 대해 잘 알고 모르겠으면 **ssh**, hello 명령에서는 hello 양식 `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, 다음과 같은 hello 및:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

출력

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

연결 된 했으므로 이제 tooyour VM 수 tooattach 디스크.  Hello를 찾으려면 먼저 디스크에 사용 하 여 `dmesg | grep SCSI` (hello 메서드 사용 toodiscover 새 디스크에 따라 달라질 수 있습니다). 이 경우, 다음과 유사하게 표시됩니다.

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

이 항목의 경우 hello hello 및 `sdc` 디스크는 hello 하나 주시기 바랍니다. 지금 파티션에 hello 디스크 `sudo fdisk /dev/sdc` 프로그램 사례 hello에 디스크를 가정할- `sdc`, 주 디스크 파티션 1에 수행 하 고 동의 hello 다른 기본값입니다.

```bash
sudo fdisk /dev/sdc
```

출력

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

입력 하 여 hello 파티션을 만들 `p` hello 프롬프트에서:

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

Hello를 사용 하 여 파일 시스템 toohello 파티션을 작성 및 **mkfs** 명령, 파일 시스템 형식 및 hello 장치 이름을 지정 합니다. 이 항목에서 위의 `ext4` 및 `/dev/sdc1`을 사용합니다.

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

이제 디렉터리 toomount hello 시스템 사용 하는 파일을 만들 것 `mkdir`:

```bash
sudo mkdir /datadrive
```

Hello 디렉터리를 사용 하 여 탑재 `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

hello 데이터 디스크가 현재으로 준비 toouse `/datadrive`합니다.

```bash
ls
```

출력

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

tooensure hello 드라이브 toohello /etc/fstab 파일을 추가 하는 다시 부팅 해야 자동으로 다시 탑재 됩니다. 또한 좋습니다 hello UUID (전체적으로 Unique IDentifier)는 /etc/fstab toorefer toohello 정당한 hello 장치 16 진수 드라이브 (예: `/dev/sdc1`). Hello OS가 부팅 하는 동안 디스크 오류를 발견 하는 경우 hello UUID를 사용 하 여 hello 잘못 된 디스크를 위치를 받아야 하는 탑재 된 tooa 되 고 발생 하지 않습니다. 그런 다음 남아 있는 데이터 디스크를 동일한 장치 ID에 할당합니다. toofind hello 새 드라이브의 UUID hello, hello를 사용 하 여 **blkid** 유틸리티:

```bash
sudo -i blkid
```

hello 출력은 toohello 다음과 유사 합니다.

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Hello를 잘못 편집 **/등/fstab** 파일 경우 시스템 될 수 있습니다. 를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 문서를 참조 하십시오. 또한 편집 하기 전에 hello /etc/fstab 파일의 백업을 만들어졌는지 것이 좋습니다.
> 
> 

Hello을 열고 **/등/fstab** 파일 텍스트 편집기에서:

```bash
sudo vi /etc/fstab
```

이 예제에서 사용 하 여 hello UUID 값 hello에 대 한 새 **/개발/sdc1** hello 탑재 지점 및 hello 이전 단계에서 만든 장치 **/datadrive**합니다. 줄 toohello의 끝 다음 hello hello 추가 **/등/fstab** 파일:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> 나중에 fstab 편집 하지 않고도 데이터 디스크를 제거 하는 hello VM toofail tooboot을 발생할 수 있습니다. 대부분의 배포판 제공 하거나 hello `nofail` 및/또는 `nobootwait` fstab 옵션입니다. 이 옵션을 부팅 시 toomount hello 디스크에 오류가 발생 하는 경우에 시스템 tooboot을 사용 합니다. 이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.
> 
> hello **nofail** 옵션을 선택 하면 해당 hello hello 파일 시스템 손상 되었거나 hello 디스크 부팅 시 존재 하지 않는 경우에 VM을 시작 합니다. 이 옵션이 없으면 발생할 수에 설명 된 대로 동작 [없습니다 SSH tooLinux VM tooFSTAB 오류 기한](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Azure에서 Linux에 대한 TRIM/UNMAP 지원
일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다. 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에 주로 유용 합니다. 큰 파일을 만들고 삭제하는 경우 이렇게 하면 비용을 절감할 수 있습니다.

두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다. 일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.

* 사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* 일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다. Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:
  
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
* 기억 새 디스크에 없는 것 사용할 수 있는 toohello VM 해당 정보 tooyour를 작성 하지 않는 경우 다시 부팅 [fstab](http://en.wikipedia.org/wiki/Fstab) 파일입니다.
* Linux VM은 tooensure 올바르게 구성 검토 hello [Linux 컴퓨터 성능 최적화](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 권장 사항입니다.
* 디스크를 추가하여 저장소 용량을 확장하고 추가 성능이 필요할 경우 [RAID를 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

