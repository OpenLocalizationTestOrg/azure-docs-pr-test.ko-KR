---
title: "디스크 tooa Azure에서 Linux VM aaaAttach | Microsoft Docs"
description: "데이터 tooattach tooa Linux VM 디스크 하는 방법에 대해 알아봅니다 hello 클래식 배포를 사용 하 여 모델 및 사용 하기 위해 있도록 hello 디스크를 초기화 합니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>어떻게 tooAttach 데이터 디스크 tooa Linux 가상 컴퓨터
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 어떻게 참조[hello 리소스 관리자 배포 모델을 사용 하 여 데이터 디스크 연결](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

빈 디스크와 데이터 tooyour Azure Vm을 포함 하는 디스크를 연결할 수 있습니다. 두 유형의 디스크 모두 Azure Storage 계정에 상주하는 .vhd 파일입니다. 으로 모든 디스크 tooa Linux 컴퓨터를 추가 하는 hello 디스크를 연결한 후를 사용할 때는 tooinitialize 필요를 사용 하기 위해 있도록 서식을 지정 합니다. 이 문서를 세부 정보 빈 디스크와 toothen 초기화 하 고 새 디스크를 포맷 하는 방법에 따라 데이터 tooyour Vm에도 이미 포함 하는 디스크를 연결 합니다.

> [!NOTE]
> 하나는 모범 사례 toouse 나 가상 컴퓨터의 데이터 디스크 toostore 분리 더 있습니다. Azure 가상 컴퓨터를 만들면 운영 체제 디스크와 임시 디스크가 있습니다. **Hello 임시 디스크 toostore 영구 데이터를 사용 하지 마십시오.** Hello 이름에서 알 수 있듯이 임시 저장소만 제공 합니다. Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.
> 임시 디스크 hello hello Azure Linux 에이전트에서 일반적으로 관리 되 고 자동으로 너무 탑재**/mnt/리소스** (또는 **/mnt** Ubuntu 이미지에). Hello 반면에, 데이터 디스크 이름은 수 있습니다 hello Linux 커널에 의해 다음과 같이 `/dev/sdc`, toopartition, 필요한 서식을 지정 하 고이 리소스를 탑재 합니다. Hello 참조 [Azure Linux 에이전트 사용자 가이드] [ Agent] 대 한 자세한 내용은 합니다.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Linux에서 새 데이터 디스크 초기화
1. SSH tooyour VM입니다. 자세한 내용은 참조 [어떻게 Linux를 실행 하는 tooa 가상 컴퓨터에서 toolog][Logon]합니다.
2. 그런 다음 toofind hello 장치 식별자 hello 데이터 디스크 tooinitialize 필요합니다. 두 가지 방법으로 toodo입니다.
   
    a) Grep hello에 SCSI 장치에 대 한 로그, 다음 명령을 hello와 같이:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    최근 Ubuntu 분포에 대 한 toouse 할 수 있습니다 `sudo grep SCSI /var/log/syslog` 너무 로그인 때문에`/var/log/messages` 기본적으로 사용할 수 없습니다.
   
    표시 되는 hello 메시지에 추가 된 hello 마지막 데이터 디스크의 hello 식별자를 찾을 수 있습니다.
   
    ![Hello 디스크 메시지 가져오기](./media/attach-disk/scsidisklog.png)
   
    또는
   
    b) 사용 하 여 hello `lsscsi` hello 장치 id 아웃 toofind 명령입니다. `lsscsi` 방법으로 설치할 수 있습니다 `yum install lsscsi` (Red Hat 분포 기반) 또는 `apt-get install lsscsi` (Debian 분포 기반). 원하는 hello 디스크를 찾을 수 있습니다는 *lun* 또는 **논리 단위 번호**합니다. 예를 들어 hello *lun* 첨부 hello 디스크에서 쉽게 볼 수에 대 한 `azure vm disk list <virtual-machine>` 로:

    ```azurecli
    azure vm disk list myVM
    ```

    hello 출력은 toohello 다음과 유사 합니다.

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    출력을 hello 사용 하 여이 데이터를 비교 `lsscsi` hello 동일 샘플 가상 컴퓨터:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    각 행에 hello 튜플에 hello 마지막 번호는 hello *lun*합니다. 자세한 내용은 `man lsscsi`를 참조하세요.
3. Hello 프롬프트에서 다음 명령을 toocreate hello 장치를 입력 합니다.
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. 메시지가 나타나면 입력  **n**  toocreate 파티션 합니다.

    ![장치 만들기](./media/attach-disk/fdisknewpartition.png)

5. 메시지가 나타나면 입력 **p** toomake hello 파티션 hello 주 파티션 합니다. 형식 **1** 첫 번째 파티션에 hello 하 한 다음 입력 toomake 실린더 hello에 대 한 tooaccept hello 기본값을 입력 합니다. 일부 시스템에서는 수의 hello hello 기본값을 첫 번째 표시 하 고 hello 실린더 대신 마지막 섹터 hello 합니다. 이러한 기본값 tooaccept를 선택할 수 있습니다.

    ![파티션 만들기](./media/attach-disk/fdisknewpartdetails.png)


6. 형식 **p** 분할 되 고 된 hello 디스크에 대 한 toosee hello 세부 정보입니다.

    ![디스크 정보 나열](./media/attach-disk/fdiskpartitiondetails.png)


7. 형식 **w** hello 디스크에 대 한 toowrite hello 설정 합니다.

    ![Hello 디스크 변경 기록](./media/attach-disk/fdiskwritedisk.png)

8. 이제 hello 새 파티션에 hello 파일 시스템을 만들 수 있습니다. Hello 파티션 번호 toohello 장치 ID를 추가 (다음 예제는 hello에 `/dev/sdc1`). hello 다음 예제에서는 ext4에 파티션을 만듭니다 /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![파일 시스템 만들기](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > SuSE Linux Enterprise 11 시스템에서는 ext4 파일 시스템에 대해 읽기 전용 권한만 지원합니다. 이러한 시스템 ext4 아닌 ext3 tooformat hello 새 파일 시스템을 좋습니다.

9. 디렉터리 toomount hello 새 파일 시스템의 경우 다음과 같이 확인 합니다.
   
    ```bash
    sudo mkdir /datadrive
    ```

10. 마지막으로 다음과 같이 hello 드라이브를 탑재할 수 있습니다.
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    hello 데이터 디스크가 현재으로 준비 toouse **/datadrive**합니다.
   
    ![Hello 디렉터리 및 탑재 hello 디스크 만들기](./media/attach-disk/mkdirandmount.png)

11. Hello 새 드라이브 너무/등/fstab를 추가 합니다.
   
    tooensure hello 드라이브 toohello /etc/fstab 파일을 추가 하는 다시 부팅 해야 자동으로 다시 탑재 됩니다. 또한 해당 hello UUID (전체적으로 Unique IDentifier) 방금 hello 장치 이름 (예: /dev/sdc1)이 아닌 /etc/fstab toorefer toohello 드라이브는 것이 좋습니다. UUID는 hello를 사용 하 여 지정 된 위치로 hello 운영 체제 부팅 하는 동안 디스크 오류를 검색 하 고 장치 Id 할당 되 고 그런 다음 모든 나머지 데이터 디스크를 탑재 된 tooa 되 고 hello 잘못 된 디스크를 방지 합니다. toofind hello 새 드라이브의 UUID hello hello를 사용할 수 있습니다, **blkid** 유틸리티:
   
    ```bash
    sudo -i blkid
    ```
   
    hello 출력은 다음 예제와 비슷한 toohello 합니다.
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Hello를 잘못 편집 **/등/fstab** 파일 경우 시스템 될 수 있습니다. 를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 문서를 참조 하십시오. 또한 편집 하기 전에 hello /etc/fstab 파일의 백업을 만들어졌는지 것이 좋습니다.

    Hello을 열고 **/등/fstab** 파일 텍스트 편집기에서:

    ```bash
    sudo vi /etc/fstab
    ```

    이 예제에서 사용 하 여 hello UUID 값 hello에 대 한 새 **/개발/sdc1** hello 탑재 지점 및 hello 이전 단계에서 만든 장치 **/datadrive**합니다. 줄 toohello의 끝 다음 hello hello 추가 **/등/fstab** 파일:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    또는 SuSE Linux 기반 시스템에서 약간 다른 형식 toouse 할 수 있습니다.

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > hello `nofail` 옵션을 선택 하면 해당 hello hello 파일 시스템 손상 되었거나 hello 디스크 부팅 시 존재 하지 않는 경우에 VM을 시작 합니다. 이 옵션이 없으면 발생할 수에 설명 된 대로 동작 [없습니다 SSH tooLinux VM tooFSTAB 오류 인해](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)합니다.

    파일 시스템 hello 탑재 되어 이제 테스트할 수 있습니다 제대로 분리 하 고 다음 hello 파일 시스템 다시 탑재할 즉, 사용 하 여 hello 예제 탑재 지점 `/datadrive` hello에서 만든 이전 단계:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    경우 hello `mount` 오류를 생성 하는 명령, 파일 hello/등/fstab 구문이 올바른지 확인 하십시오. 추가 데이터 드라이브 또는 파티션을 만든 경우에는 /etc/fstab에 해당 드라이브나 파티션도 별도로 입력합니다.

    이 명령을 사용 하 여 hello 드라이브에 쓸 수 있게 합니다.

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > 이후에 fstab 편집 하지 않고도 데이터 디스크를 제거 하는 hello VM toofail tooboot을 발생할 수 있습니다. 이 경우 경우가 종종, 대부분의 배포판 제공 하거나 hello `nofail` 및/또는 `nobootwait` 부팅 시 toomount hello 디스크에 오류가 발생 하는 경우에 시스템 tooboot 수 있는 fstab 옵션. 이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.

### <a name="trimunmap-support-for-linux-in-azure"></a>Azure에서 Linux에 대한 TRIM/UNMAP 지원
일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다. 이러한 작업은 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에서 주로 유용 합니다. 큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.

두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다. 일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.

* 사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:

    ```sh
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
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 문서는 hello에서 Linux VM을 사용 하 여 하는 방법에 대 한:

* [어떻게 toolog Linux를 실행 하는 tooa 가상 컴퓨터][Logon]
* [어떻게 toodetach Linux 가상 컴퓨터에서 디스크](detach-disk.md)
* [Hello Azure CLI를 사용 하 여 hello 클래식 배포 모델](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure에서 Linux VM에 RAID 구성](../configure-raid.md)
* [Azure에서 Linux VM에 LVM 구성](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
