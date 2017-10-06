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
# <a name="configure-software-raid-on-linux"></a>Linux에서 소프트웨어 RAID 구성
일반적인 시나리오 toouse 소프트웨어 RAID Linux 가상 컴퓨터에서 여러 연결 된 데이터 디스크에 하나의 RAID 장치로 Azure toopresent입니다. 일반적으로 사용 되는 tooimprove 성능 고 처리량 비교 toousing만 단일 디스크를 개선 하기 위해 허용 수이 합니다.

## <a name="attaching-data-disks"></a>데이터 디스크 연결
두 개 이상의 빈 데이터 디스크는 필요한 tooconfigure RAID 장치입니다.  RAID 장치를 만들기 위한 hello 주된 이유는 디스크 IO의 tooimprove 성능.  IO 요구 사항에 따라, 디스크 또는 디스크 당 too5000 IO/ps를 우리의 프리미엄 저장소와 당 too500 IO/ps를와 우리의 표준 저장소에 저장 된 tooattach 디스크를 선택할 수 있습니다. 이 문서는 방법에 세부 정보를 시작 하지 못할 tooprovision 및 데이터 디스크 tooa Linux 가상 컴퓨터를 연결 합니다.  참조 hello Microsoft Azure 문서 [디스크 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 어떻게 tooattach 빈 데이터 디스크 tooa Linux 가상 컴퓨터에서 Azure에 대 한 자세한 내용은 합니다.

## <a name="install-hello-mdadm-utility"></a>Hello mdadm 유틸리티 설치
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS 및 Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES 및 openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Hello 디스크 파티션 만들기
이 예에서는 /dev/sdc에 단일 디스크 파티션을 만듭니다. 새 디스크 파티션은 hello /dev/sdc1을 호출 됩니다.

1. 시작 `fdisk` toobegin 파티션 만들기

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

2. 키를 눌러 hello 프롬프트 toocreate에 ' n '는  **n** 우 파티션:

    ```bash
    Command (m for help): n
    ```

3. 'P' toocreate를 눌러 다음으로 **p**기본 파티션:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. '1' tooselect 파티션 번호 1 키를 누릅니다.

    ```bash
    Partition number (1-4): 1
    ```

5. 선택 hello hello 새 파티션 또는 키를 눌러의 시작 지점 `<enter>` tooaccept hello 기본 tooplace hello 파티션을 hello 드라이브에 공간이 hello hello 맨 앞에서:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. 예를 들어 형식 '+10G' toocreate 10 기가바이트 파티션 hello 파티션의 hello 크기를 선택 합니다. 또는 키를 누릅니다 `<enter>` hello 전체 드라이브에 걸쳐 있는 파티션 하나를 만듭니다.

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. 다음으로, hello ID를 변경 하 고 **t**hello 기본값과에서 hello 파티션 유형 ID '83' (Linux) tooID 'fd' (Linux raid 자동):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. 마지막으로 hello 파티션 테이블 toohello 드라이브를 작성 하 고 fdisk 종료:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Hello RAID 배열 만들기
1. 다음 예제는 "스트라이프" (RAID 수준 0) 3 개의 파티션과 (sdc1, sdd1, sde1) 세 가지 별도 데이터 디스크에 있는 번호입니다.  이 명령을 실행하면 **/dev/md127** 이라는 새 RAID 장치가 만들어집니다. 또한 참고 이러한 데이터 디스크에서는 이전에 존재 하지 않는 다른 RAID 배열의 일부 필요한 tooadd hello 수 수 것 `--force` 매개 변수 toohello `mdadm` 명령:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Hello 새 RAID 장치에 hello 파일 시스템 만들기
   
    a. **CentOS, Oracle Linux, SLES 12, openSUSE 및 Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** - boot.md 사용 및 mdadm.conf 만들기

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > SUSE 시스템에서 이렇게 변경한 후에는 다시 부팅해야 할 수 있습니다. SLES 12에서는 이 단계가 필요하지 *않습니다* .
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Hello 새 파일 시스템 너무/등/fstab 추가
> [!IMPORTANT]
> Hello /etc/fstab 파일을 잘못 편집 하는 경우 시스템 될 수 있습니다. 를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 문서를 참조 하십시오. 또한 편집 하기 전에 hello /etc/fstab 파일의 백업을 만들어졌는지 것이 좋습니다.

1. 예를 들어 새로운 파일 시스템에 대 한 원하는 hello 탑재 지점을 만듭니다.

    ```bash
    sudo mkdir /data
    ```
2. /Etc/fstab을 편집할 때 hello **UUID** 사용된 tooreference hello 파일 hello 보다는 시스템 장치 이름 이어야 합니다.  사용 하 여 hello `blkid` hello 새로운 파일 시스템에 대 한 유틸리티 toodetermine hello UUID:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. 텍스트 편집기에서 /etc/fstab을 열고 예를 들어 hello 새로운 파일 시스템에 대 한 항목을 추가 합니다.

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    또는 **SLES 11**에 대해 다음을 수행합니다.

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    그런 다음, /etc/fstab를 저장하고 닫습니다.

4. 해당 hello /etc 테스트/fstab 입력 한 내용이 올바른지:

    ```bash  
    sudo mount -a
    ```

    이 명령은 오류 메시지에 결과가 hello /etc/fstab 파일에서 hello 구문을 확인 하십시오.
   
    그런 다음 실행 하는 hello `mount` 명령 tooensure hello 파일 시스템은 탑재:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (선택 사항) Failsafe 부팅 매개 변수
   
    **fstab 구성**
   
    많은 배포판에 포함 하거나 hello `nobootwait` 또는 `nofail` 파일 toohello/등/fstab 추가할 수 있는 매개 변수를 탑재 합니다. 이러한 매개 변수를 특정 파일 시스템을 탑재 하는 경우 오류에 대 한 허용 경우에 없습니다 tooproperly 탑재 hello RAID 파일 시스템 hello Linux 시스템 toocontinue tooboot을 허용 합니다. 이러한 매개 변수에 대 한 자세한 내용은 tooyour 분포의 설명서를 참조 하십시오.
   
    예제(Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Linux 부팅 매개 변수**
   
    매개 변수 위에 추가 toohello에서 커널 매개 변수를 hello "`bootdegraded=true`" hello RAID 것으로 인식 됩니다 손상 되거나 예를 들어 hello 가상 컴퓨터에서 데이터 드라이브를 실수로 제거한 경우 성능이 저하 된 경우에 시스템 tooboot hello를 허용할 수 있습니다. 기본적으로 이 매개 변수는 시스템이 부팅할 수 없게 만들 수도 있습니다.
   
    Tooproperly 커널 매개 변수를 편집 하는 방법에 대 한 tooyour 분포의 설명서를 참조 하십시오. 예를 들어 많은 배포 (CentOS, Oracle Linux, SLES 11)에서 이러한 매개 변수에 추가할 수 있습니다 수동으로 toohello "`/boot/grub/menu.lst`" 파일입니다.  Ubuntu이 매개이 변수에 추가할 수 있습니다 toohello `GRUB_CMDLINE_LINUX_DEFAULT` 에 변수 "/ 등/기본/grub"입니다.


## <a name="trimunmap-support"></a>TRIM/UNMAP 지원
일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다. 이러한 작업은 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에서 주로 유용 합니다. 큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.

> [!NOTE]
> RAID는 hello 배열에 대 한 hello 청크 크기 (512KB) hello 기본값과 tooless 설정 된 경우 취소 명령을 실행 하지 않을 수 있습니다. Hello 매핑 해제 때문에 이것이 hello 호스트에 대 한 세분성 512KB 이기도 합니다. Mdadm의 통해 hello 배열 청크 크기를 수정 하는 경우 `--chunk=` hello 커널이 매개 변수를 다음 TRIM/매핑 해제 요청을 무시할 수 있습니다.

두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다. 일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.

- 사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- 일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다. Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
