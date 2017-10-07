---
title: "aaaCreate 및 SUSE Linux VHD를 Azure에 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD) SUSE Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Azure용 SLES 또는 openSUSE 가상 컴퓨터 준비
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>필수 조건
이 문서에서는 SUSE 또는 openSUSE Linux 운영 체제 tooa 가상 하드 디스크를 이미 설치 가정 합니다. 여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다. 자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.

### <a name="sles--opensuse-installation-notes"></a>SLES/openSUSE 설치 참고 사항
* Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.
* hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.  Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.
* Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다. OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이. 원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.
* 스왑 파티션을 hello OS 디스크에 구성 하지 마십시오. hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.  이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.
* 모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.

## <a name="use-suse-studio"></a>SUSE Studio 사용
[SUSE Studio](http://www.susestudio.com) 에서는 Azure와 Hyper-V용 SLES 및 openSUSE 이미지를 쉽게 만들고 관리할 수 있습니다. 이 hello SLES 및 openSUSE 사용자 고유의 이미지를 사용자 지정 하기 위한 방법을 권장 합니다.

대체 toobuilding로 사용자 고유의 VHD, SUSE 엔터티에도 BYOS (Bring Your 자신의 구독의) 이미지에서 SLES에 대 한 [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007)합니다.

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>SUSE Linux Enterprise Server 11 SP4 준비
1. Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.
2. 클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.
3. SUSE Linux Enterprise 시스템 tooallow 등록 것 toodownload 업데이트 및 설치 패키지입니다.
4. Hello 최신 패치 사용 hello 시스템을 업데이트 합니다.
   
        # sudo zypper update
5. Hello SLES 리포지토리에서 hello Azure Linux 에이전트를 설치 합니다.
   
        # sudo zypper install WALinuxAgent
6. Chkconfig에서 "에서" waagent 너무 설정 되어 있는지를 확인 하 고 그렇지 않은 경우 자동 시작에 사용 합니다.
   
        # sudo chkconfig waagent on
7. waagent 서비스가 실행 중인지 확인하고 그렇지 않으면 서비스를 시작합니다. 
   
        # sudo service waagent start
8. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. 이 열린 toodo "/ boot/grub/menu.lst" 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 및:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    이 방법을 사용 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.
9. 해당 /boot/grub/menu.lst 및/등/fstab hello 디스크 ID (id 별) 대신 해당 UUID (uuid 여)을 사용 하 여 두 참조 hello 디스크를 확인 합니다. 
   
    디스크 UUID 가져오기
   
        # ls /dev/disk/by-uuid/
   
    경우 /dev/disk/by-id /는 /boot/grub/menu.lst 및/등/fstab hello uuid 하 여 적절 한 값으로 업데이트 사용
   
    변경 전
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    변경 후
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다. 이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Tooedit hello 파일 좋습니다 "/ 등/sysconfig/네트워크/dhcp" hello 변경 `DHCLIENT_SET_HOSTNAME` toohello 다음 매개 변수:
    
     DHCLIENT_SET_HOSTNAME="no"
12. "/ 등/sudoers"에서 주석으로 처리 하거나 hello 있을 경우 줄을 다음를 제거 합니다.
    
     Targetpw 기본값 즉, 루트 모든 ALL=(ALL) 모든 hello 대상 사용자의 hello 암호 # 요청 # 경고! 'Defaults targetpw'와 함께 사용해야 합니다.
13. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.
14. Hello OS 디스크에 스왑 공간을 만들지 마십시오.
    
    hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 참고:이 toowhatever toobe 필요를 설정 합니다.
15. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.

- - -
## <a name="prepare-opensuse-131"></a>openSUSE 13.1+ 준비
1. Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.
2. 클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.
3. Hello 셸 hello 명령을 실행 '`zypper lr`'. 이 명령을 반환 하는 경우 비슷한 toohello hello 저장소 예상-조정 없이 필요한 대로 구성 된 다음을 수행 (버전 번호가 다를 수 있습니다 참고)를 출력 합니다.
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Hello 명령 "저장소 정의..."를 반환 하는 경우 다음 사용 하 여 다음 명령을 tooadd hello 이러한 리포지토리:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    Hello 저장소 hello 명령을 실행 하 여 추가 된 확인할 수 있습니다 '`zypper lr`' 다시 합니다. Hello 관련 업데이트 저장소 중 하나를 사용 하지 않는 경우 다음 명령을 사용 하 여 사용:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Hello 커널 toohello 사용 가능한 최신 버전을 업데이트 합니다.
   
        # sudo zypper up kernel-default
   
    또는 모든 hello 최신 패치 tooupdate hello 시스템:
   
        # sudo zypper update
5. Hello Azure Linux 에이전트를 설치 합니다.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo이,이 열기 "/ boot/grub/menu.lst" 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 하 고 있습니다.
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   이 방법을 사용 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다. 또한 있을 경우 hello 커널 부팅 줄에서 매개 변수 뒤 hello를 제거 합니다.
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. Tooedit hello 파일 좋습니다 "/ 등/sysconfig/네트워크/dhcp" hello 변경 `DHCLIENT_SET_HOSTNAME` toohello 다음 매개 변수:
   
     DHCLIENT_SET_HOSTNAME="no"
8. **중요:** "/ 등/sudoers" 주석으로 처리 하거나 있을 경우 줄을 다음 hello를 제거 합니다.
   
     Targetpw 기본값 즉, 루트 모든 ALL=(ALL) 모든 hello 대상 사용자의 hello 암호 # 요청 # 경고! 'Defaults targetpw'와 함께 사용해야 합니다.
9. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.
10. Hello OS 디스크에 스왑 공간을 만들지 마십시오.
    
    hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 참고:이 toowhatever toobe 필요를 설정 합니다.
11. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. 시작 시 Azure Linux 에이전트를 실행 하는 hello를 확인 합니다.
    
        # sudo systemctl enable waagent.service
13. Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.

## <a name="next-steps"></a>다음 단계
사용자는 이제 준비 toouse Azure에서 SUSE Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터. 인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

