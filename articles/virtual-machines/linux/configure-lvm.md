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
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Azure에서 Linux VM에 LVM 구성
이 문서에 설명 합니다 어떻게 Azure 가상 컴퓨터의 논리 볼륨 관리자 (LVM) tooconfigure 합니다. 가능한 tooconfigure LVM 모든 디스크에 연결 된 toohello 가상 컴퓨터를 기본적으로 이미지는 대부분 클라우드 동안 LVM OS 디스크를 hello에서 구성 합니다. OS 디스크는 현재까지 hello tooanother hello의 VM을 연결 하는 경우이 중복 된 볼륨 그룹에 tooprevent 문제가 동일 하 게 분산 및 복구 시나리오 중 즉, 형식입니다. 따라서 hello 데이터 디스크에 LVM을 toouse만 좋습니다.

## <a name="linear-vs-striped-logical-volumes"></a>선형 및 스트라이프 논리 볼륨 비교
LVM 사용된 toocombine 다양 한 단일 저장소 볼륨에 실제 디스크 일 수 있습니다. 기본적으로 LVM 일반적으로 만들어집니다 선형 논리 볼륨을 의미 하는 hello 실제 저장소 서로 연결 됩니다. 이 경우 읽기/쓰기 작업은 일반적으로 전송 되 tooa 단일 디스크입니다. 반면, 여기서 읽기 및 쓰기는 hello 볼륨 그룹 (예: 유사한 tooRAID0)에 포함 된 분산된 toomultiple 디스크 스트라이프 논리 볼륨 만들 수도 있습니다. 성능상의 이유로 될 것이 좋습니다 toostripe 논리 볼륨 읽기 및 쓰기가 모든 연결 된 데이터 디스크를 활용할 수 있도록 합니다.

이 문서에서는 어떻게 toocombine 여러 데이터 디스크를 단일 볼륨 그룹에 설명 하 고 스트라이프 논리 볼륨을 만듭니다. hello 단계 아래에 대부분 분포와 함께 다소 일반화 toowork 됩니다. 대부분의 경우 hello 유틸리티와 Azure에서 LVM 관리에 대 한 워크플로 높지 않습니다 다른 환경에 비해 근본적으로 다릅니다. 늘 그렇듯이 특정 배포로 LVM을 사용하는 설명서 및 모범 사례의 경우 Linux 공급업체에도 문의하시기 바랍니다.

## <a name="attaching-data-disks"></a>데이터 디스크 연결
일반적으로 LVM를 사용 하는 경우 두 개 이상의 빈 데이터 디스크와 toostart를 합니다는 하나. IO 요구 사항에 따라, 디스크 또는 디스크 당 too5000 IO/ps를 우리의 프리미엄 저장소와 당 too500 IO/ps를와 우리의 표준 저장소에 저장 된 tooattach 디스크를 선택할 수 있습니다. 이 문서는 방법에 정보를 확인할 전환 되지 것입니다 tooprovision 및 데이터 디스크 tooa Linux 가상 컴퓨터를 연결 합니다. 참조 하십시오 hello Microsoft Azure 문서 [디스크 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 어떻게 tooattach 빈 데이터 디스크 tooa Linux 가상 컴퓨터에서 Azure에 대 한 자세한 내용은 합니다.

## <a name="install-hello-lvm-utilities"></a>Hello LVM 유틸리티 설치
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS 및 Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 및 openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    SLES11에서 편집 해야 `/etc/sysconfig/lvm` 설정 `LVM_ACTIVATED_ON_DISCOVERED` 너무 "사용":

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>LVM 구성
이 가이드 가정 지칭 3 개의 데이터 디스크를 연결 상태 tooas `/dev/sdc`, `/dev/sdd` 및 `/dev/sde`합니다. 하지 있습니다 이러한 항상 hello을 VM에서 동일한 경로 이름 이어야 합니다. 실행할 수 있습니다 '`sudo fdisk -l`' 또는 유사한 명령 toolist 사용 가능한 디스크.

1. Hello 실제 볼륨을 준비 합니다.

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. 볼륨 그룹을 만듭니다. 이 예제에서는 호출 하는 hello 볼륨 그룹 `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Hello 논리 볼륨을 만듭니다. hello 명령에서는 아래 만들어집니다 라는 단일 논리 볼륨 `data-lv01` toospan hello 전체 볼륨 그룹을 참고 하는 것도 가능 toocreate 하지만 hello 볼륨 그룹에 여러 논리 볼륨입니다.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Hello 논리 볼륨 포맷

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > SLES11에서는 ext4가 아닌 `-t ext3`을 사용합니다. SLES11만 읽기 전용 액세스 tooext4 파일 시스템을 지원 합니다.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Hello 새 파일 시스템 너무/등/fstab 추가
> [!IMPORTANT]
> Hello를 잘못 편집 `/etc/fstab` 파일 경우 시스템 될 수 있습니다. 를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 설명서를 참조 하십시오. 또한 hello 백업 하는 권장 `/etc/fstab` 편집 하기 전에 파일이 만들어집니다.

1. 예를 들어 새로운 파일 시스템에 대 한 원하는 hello 탑재 지점을 만듭니다.

    ```bash  
    sudo mkdir /data
    ```

2. Hello 논리 볼륨 경로 찾기

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. 열기 `/etc/fstab` 텍스트 편집기에서 예를 들어 hello 새로운 파일 시스템에 대 한 항목을 추가 합니다.

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    `/etc/fstab`을 저장하고 닫습니다.

4. 해당 hello 테스트 `/etc/fstab` 입력이 있습니다.

    ```bash    
    sudo mount -a
    ```

    이 명령은, 오류 메시지를 발생 하는 경우 hello에 hello 구문을 확인 하십시오 `/etc/fstab` 파일입니다.
   
    그런 다음 실행 하는 hello `mount` 명령 tooensure hello 파일 시스템은 탑재:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (선택 사항) `/etc/fstab`의 Failsafe 부팅 매개 변수
   
    많은 배포판에 포함 하거나 hello `nobootwait` 또는 `nofail` toohello 추가할 수 있는 매개 변수를 탑재 `/etc/fstab` 파일입니다. 이러한 매개 변수를 특정 파일 시스템을 탑재 하는 경우 오류에 대 한 허용 경우에 없습니다 tooproperly 탑재 hello RAID 파일 시스템 hello Linux 시스템 toocontinue tooboot을 허용 합니다. 이러한 매개 변수에 대 한 자세한 내용은 tooyour 분포의 설명서를 참조 하십시오.
   
    예제(Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>TRIM/UNMAP 지원
일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다. 이러한 작업은 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에서 주로 유용 합니다. 큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.

두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다. 일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.

- 사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- 일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다. Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
