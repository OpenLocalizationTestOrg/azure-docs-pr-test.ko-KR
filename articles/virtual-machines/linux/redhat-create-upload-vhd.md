---
title: "aaaCreate 및 Red Hat Enterprise Linux VHD를 Azure에서 사용 하기 위해 업로드 | Microsoft Docs"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD) Red Hat Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Azure용 RedHat 기반 가상 컴퓨터 준비
이 문서에서는 살펴보겠습니다 어떻게 tooprepare Azure에서 사용 하기 위해 Red Hat Enterprise Linux (RHEL) 가상 컴퓨터. 이 문서에 설명 된 RHEL hello 버전은 6.7 + 및 7.1 이상입니다. 이 문서에서 설명 하는 준비에 대 한 hello 하이퍼바이저는 Hyper-v, 커널 기반 가상 컴퓨터 (KVM) 및 VMware입니다. Red Hat 클라우드 액세스 프로그램에 참여하기 위한 자격 요구 사항에 대한 자세한 내용은 [Red Hat 클라우드 액세스 웹 사이트](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) 및 [Azure에서 실행 중인 RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure)을 참조하세요.

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Hyper-V 관리자에서 Red Hat 기반 가상 컴퓨터 준비

### <a name="prerequisites"></a>필수 조건
이 섹션에서는 hello Red Hat 웹 사이트와 설치 된 hello RHEL 이미지 tooa 가상 하드 디스크 (VHD)에서 ISO 파일을 이미 얻은 가정 합니다. 방법에 대 한 자세한 내용은 toouse Hyper-v 관리자는 운영 체제 이미지 tooinstall 참조 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.

**RHEL 설치 참고 사항**

* Azure는 hello VHDX 형식을 지원 하지 않습니다. Azure는 고정 VHD만 지원합니다. Hyper-v 관리자 tooconvert hello 디스크 tooVHD 형식을 사용할 수 있습니다 또는 hello convert vhd cmdlet을 사용할 수 있습니다. VirtualBox를 사용 하는 경우 선택 **고정 크기** 달리 toohello 기본 hello 디스크를 만드는 경우 옵션을 동적으로 할당 합니다.
* Azure에서는 1세대 가상 컴퓨터만 지원합니다. 1 세대 가상 컴퓨터와 tooa 고정 크기 디스크를 동적 확장 VHDX toohello VHD 파일 형식에서 변환할 수 있습니다. 가상 컴퓨터의 세대는 변경할 수 없습니다. 자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 하나요?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.
* hello VHD에 대 한 허용 되는 hello 최대 크기는 1, 023 GB입니다.
* Hello Linux 운영 체제를 설치할 때 사용 하는 논리 볼륨 관리자 (LVM) 보다는 표준 파티션을 대부분의 설치에 대 한 hello 기본값 이기도 하는 것이 좋습니다. 이 사례는 tooattach 운영 체제 디스크 tooanother 동일한 가상 컴퓨터 문제 해결을 위해 필요한 경우에 특히 복제 된 가상 컴퓨터와 LVM 이름 충돌을 방지 합니다. 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.
* UDF(범용 디스크 형식) 파일 시스템을 탑재하기 위한 커널 지원이 필요합니다. 연결 된 toohello 게스트, hello UDF로 포맷 된 미디어에 있는 첫 번째 부팅 시 hello 프로 비전 구성 toohello Linux 가상 컴퓨터를 전달 합니다. hello Azure Linux 에이전트는 해당 구성을 수 toomount hello UDF 파일 시스템 tooread 수 하 고 hello 가상 컴퓨터 프로 비전 해야 합니다.
* Hello Linux 커널의 이전 버전은 2.6.37 보다 더 큰 가상 컴퓨터 크기와 비균일 메모리 액세스 (NUMA)를 Hyper-v에서 지원 하지 않습니다. 이 문제를 주로 영향 업스트림 hello를 사용 하는 이전 배포 Red Hat 2.6.32 커널 RHEL 6.6 (커널 2.6.32 504)에서 수정 되었습니다. 사용자 지정 커널을 실행 하는 시스템 2.6.37 보다 오래 된 또는 2.6.32-504 보다 오래 된 RHEL 기반 커널 hello를 설정 해야 `numa=off` grub.conf에 hello 커널 명령줄에서 부트 매개 변수입니다. 자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.
* 스왑 파티션을 hello 운영 체제 디스크에 구성 하지 마십시오. hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.  이 대 한 자세한 내용은 단계를 수행 하는 hello에서 찾을 수 있습니다.
* 모든 VHD 크기는 1MB의 배수여야 합니다.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Hyper-V 관리자에서 RHEL 6 가상 컴퓨터 준비

1. Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.

2. 클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.

3. RHEL 6에서 NetworkManager hello Azure Linux 에이전트와 방해할 수 있습니다. Hello 다음 명령을 실행 하 여이 패키지를 제거 합니다.
   
        # sudo rpm -e --nodeps NetworkManager

4. 만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Hello udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙을 생성 이동 (또는 제거) 합니다. 이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.

        # sudo chkconfig network on

8. Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다. Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo 열려이 수정 작업 `/boot/grub/menu.lst` 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 하 고 있습니다.
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다.
    
    또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.
    
        rhgb quiet crashkernel=auto
    
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.  Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다. 이 매개 변수 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 줄어든다는 note 합니다. 이 구성은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.

    >[!Important]
    6.5 및 이전 RHEL hello 설정 해야 `numa=off` 커널 매개 변수입니다. Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.

11. 해당 hello 보안 셸 (SSH) 서버를 설치 및 hello 기본 설정인 일반적으로 부팅 시 toostart을 구성을 확인 합니다. /Etc/ssh/sshd_config tooinclude hello 다음 줄을 수정 합니다.

        ClientAliveInterval 180

12. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    설치 hello WALinuxAgent 패키지 3 단계에서 이미 제거 되지 않은 경우 NetworkManager hello 및 NetworkManager gnome 패키지를 제거 합니다.

13. Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.

    hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 로컬 리소스 디스크 임시 디스크가 고 hello 가상 컴퓨터 프로 비전 해제 하는 경우 비워야 수는 해당 hello를 note 합니다. Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후 /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 hello를 수정 합니다.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. 구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:

        # sudo subscription-manager unregister

15. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Hyper-V 관리자에서 **작업** > **종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Hyper-V 관리자에서 RHEL 7 가상 컴퓨터 준비

1. Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.

2. 클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.

3. 만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. 만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.

        # sudo chkconfig network on

6. Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo 열려이 수정 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다. 예:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다. 이 구성은 Nic 동안 hello 새 RHEL 7 명명 규칙 하지도 않습니다. 또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.
   
        rhgb quiet crashkernel=auto
   
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다. 이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.

8. 완료 한 후 편집 `/etc/default/grub`실행 hello 명령 toorebuild hello grub 구성을 수행 합니다.

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. 해당 hello SSH 서버를 설치 및 hello 기본 설정인 일반적으로 부팅 시 toostart을 구성을 확인 합니다. 수정 `/etc/ssh/sshd_config` 다음 줄 tooinclude hello:

        ClientAliveInterval 180

10. hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다. Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.

    hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다. Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Toounregister hello 구독 하려는 경우에 hello 다음 명령을 실행 합니다.

        # sudo subscription-manager unregister

14. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Hyper-V 관리자에서 **작업** > **종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>KVM에서 RedHat 기반 가상 컴퓨터 준비
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>KVM에서 RHEL 6 가상 컴퓨터 준비

1. Hello Red Hat 웹 사이트에서의 RHEL 6 hello KVM 이미지를 다운로드 합니다.

2. 루트 암호를 설정합니다.

    암호화 된 암호를 생성 하 고 hello hello 명령의 출력을 복사 합니다.

        # openssl passwd -1 changeme

    guestfish 루트 암호를 설정합니다.
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   변경 hello 두 번째 필드에서 hello 루트 사용자의 "!!" toohello 암호화 된 암호입니다.

3. KVM에서 hello qcow2 이미지에서 가상 컴퓨터를 만듭니다. Hello 디스크 종류를 너무 설정**qcow2**, 너무 hello 가상 네트워크 인터페이스 장치 모델을 설정 하 고**virtio**합니다. 그런 다음 hello 가상 컴퓨터를 시작 하 고 루트로 로그인 합니다.

4. 만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Hello udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙을 생성 이동 (또는 제거) 합니다. 이러한 규칙은 Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.

        # chkconfig network on

8. Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo이이 구성에서는 열기 `/boot/grub/menu.lst` 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 및:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다.
    
    또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.
    
        rhgb quiet crashkernel=auto
    
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다. 이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.

    >[!Important]
    6.5 및 이전 RHEL hello 설정 해야 `numa=off` 커널 매개 변수입니다. Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.

10. Hyper-v 모듈 tooinitramfs를 추가 합니다.  

    편집 `/etc/dracut.conf`, hello 다음 콘텐츠를 추가 합니다.

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Initramfs를 다시 빌드합니다.

        # dracut -f -v

11. Cloud-Init을 제거합니다.

        # yum remove cloud-init

12. 해당 hello SSH 서버를 설치 및 부팅 시 toostart를 구성 해야 합니다.

        # chkconfig sshd on

    /Etc/ssh/sshd_config tooinclude hello 다음 줄을 수정 합니다.

        PasswordAuthentication yes
        ClientAliveInterval 180

13. hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다. Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.

        # yum install WALinuxAgent

        # chkconfig waagent on

15. hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다. Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후 수정에 대 한 매개 변수 뒤 hello **/etc/waagent.conf** 적절 하 게 합니다.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. 구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:

        # subscription-manager unregister

17. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. KVM에 hello 가상 컴퓨터를 종료 합니다.

19. Hello qcow2 이미지 toohello VHD 형식으로 변환 합니다.

    먼저 hello 이미지 tooraw 형식을 변환 합니다.

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다. 그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hello 원시 디스크 tooa 변환 고정 크기의 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>KVM에서 RHEL 7 가상 컴퓨터 준비

1. Hello Red Hat 웹 사이트에서의 RHEL 7 hello KVM 이미지를 다운로드 합니다. 이 절차는 hello 예로 RHEL 7을 사용합니다.

2. 루트 암호를 설정합니다.

    암호화 된 암호를 생성 하 고 hello hello 명령의 출력을 복사 합니다.

        # openssl passwd -1 changeme

    guestfish 루트 암호를 설정합니다.

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   변경 hello 두 번째 필드에서 루트 사용자의 "!!" toohello 암호화 된 암호입니다.

3. KVM에서 hello qcow2 이미지에서 가상 컴퓨터를 만듭니다. Hello 디스크 종류를 너무 설정**qcow2**, 너무 hello 가상 네트워크 인터페이스 장치 모델을 설정 하 고**virtio**합니다. 그런 다음 hello 가상 컴퓨터를 시작 하 고 루트로 로그인 합니다.

4. 만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.

        # chkconfig network on

7. Red Hat 구독 tooenable 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo이이 구성에서는 열기 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다. 예:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   이 명령은 또한 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 하면 문제를 디버깅 지원 합니다. hello 명령 Nic 동안 RHEL 7 명명 규칙을 새 hello 하지도 않습니다. 또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.
   
        rhgb quiet crashkernel=auto
   
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다. 이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.

9. 완료 한 후 편집 `/etc/default/grub`실행 hello 명령 toorebuild hello grub 구성을 수행 합니다.

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Hyper-V 모듈을 initramfs에 추가합니다.

    `/etc/dracut.conf` 을 편집하고 콘텐츠를 추가합니다.

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Initramfs를 다시 빌드합니다.

        # dracut -f -v

11. Cloud-Init을 제거합니다.

        # yum remove cloud-init

12. 해당 hello SSH 서버를 설치 및 부팅 시 toostart를 구성 해야 합니다.

        # systemctl enable sshd

    /Etc/ssh/sshd_config tooinclude hello 다음 줄을 수정 합니다.

        PasswordAuthentication yes
        ClientAliveInterval 180

13. hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다. Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.

        # yum install WALinuxAgent

    Hello waagent 서비스를 사용 하도록 설정 합니다.

        # systemctl enable waagent.service

15. Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.

    hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다. Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. 구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:

        # subscription-manager unregister

17. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. KVM에 hello 가상 컴퓨터를 종료 합니다.

19. Hello qcow2 이미지 toohello VHD 형식으로 변환 합니다.

    먼저 hello 이미지 tooraw 형식을 변환 합니다.

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다. 그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hello 원시 디스크 tooa 변환 고정 크기의 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>VMware에서 RedHat 기반 가상 컴퓨터 준비
### <a name="prerequisites"></a>필수 조건
이 섹션은 VMWare에 RHEL 가상 컴퓨터가 이미 설치되어 있다고 가정합니다. VMware에서 운영 체제 참조 하는 tooinstall 방법에 대 한 세부 정보에 대 한 [VMware 게스트 운영 체제 설치 가이드](http://partnerweb.vmware.com/GOSIG/home.html)합니다.

* Hello Linux 운영 체제를 설치할 때 사용 하는 LVM 보다는 표준 파티션을 대부분의 설치에 대 한 hello 기본값 이기도 하는 것이 좋습니다. 운영 체제 디스크 문제 해결을 위해 연결 된 toobe tooanother 가상 컴퓨터를 현재까지 있어야 하는 경우에 특히 복제 된 가상 컴퓨터와 LVM 이름 충돌을 피해 야 할이 합니다. 원하는 경우에는 데이터 디스크에서 LVM 또는 RAID를 사용할 수 있습니다.
* 스왑 파티션을 hello 운영 체제 디스크에 구성 하지 마십시오. Hello Linux 에이전트 toocreate hello 일시적인 리소스 디스크의 스왑 파일을 구성할 수 있습니다. 다음에 나오는 hello 단계에서이 대 한 자세한 정보를 찾을 수 있습니다.
* Hello 가상 하드 디스크를 만들 때 선택 **저장소 가상 디스크를 단일 파일로**합니다.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>VMWare에서 RHEL 6 가상 컴퓨터 준비
1. RHEL 6에서 NetworkManager hello Azure Linux 에이전트와 방해할 수 있습니다. Hello 다음 명령을 실행 하 여이 패키지를 제거 합니다.
   
        # sudo rpm -e --nodeps NetworkManager

2. 라는 파일을 만들어 **네트워크** hello /etc/sysconfig/포함 된 디렉터리에서 다음 텍스트를 hello:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. 만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Hello udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙을 생성 이동 (또는 제거) 합니다. 이러한 규칙은 Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.

        # sudo chkconfig network on

6. Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다. Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo이,이 오픈 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다. 예:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다. 또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.
   
        rhgb quiet crashkernel=auto
   
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다. 이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.

9. Hyper-v 모듈 tooinitramfs를 추가 합니다.

    편집 `/etc/dracut.conf`, hello 다음 콘텐츠를 추가 합니다.

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Initramfs를 다시 빌드합니다.

        # dracut -f -v

10. 해당 hello SSH 서버를 설치 및 hello 기본 설정인 일반적으로 부팅 시 toostart을 구성을 확인 합니다. 수정 `/etc/ssh/sshd_config` 다음 줄 tooinclude hello:

    ClientAliveInterval 180

11. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.

    hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다. Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. 구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:

        # sudo subscription-manager unregister

14. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Hello 가상 컴퓨터를 종료 하 고 hello VMDK 파일 tooa.vhd 파일로 변환 합니다.

    먼저 hello 이미지 tooraw 형식을 변환 합니다.

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다. 그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hello 원시 디스크 tooa 변환 고정 크기의 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>VMWare에서 RHEL 7 가상 컴퓨터 준비
1. 만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. 만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.

        # sudo chkconfig network on

4. Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo 열려이 수정 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다. 예:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   이 구성은 갖는지도 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 지원 문제를 디버깅 합니다. 또한 Nic 동안 RHEL 7 명명 규칙을 새 hello 하지 않습니다. 또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.
   
        rhgb quiet crashkernel=auto
   
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다. 이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.

6. 완료 한 후 편집 `/etc/default/grub`실행 hello 명령 toorebuild hello grub 구성을 수행 합니다.

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Hyper-v 모듈 tooinitramfs를 추가 합니다.

    `/etc/dracut.conf`를 편집하고 콘텐츠를 추가합니다.

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Initramfs를 다시 빌드합니다.

        # dracut -f -v

8. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다. 이 설정은 일반적으로 hello 기본값입니다. 수정 `/etc/ssh/sshd_config` 다음 줄 tooinclude hello:

        ClientAliveInterval 180

9. hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다. Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.

    hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다. Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Toounregister hello 구독 하려는 경우에 hello 다음 명령을 실행 합니다.

        # sudo subscription-manager unregister

13. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Hello 가상 컴퓨터를 종료 하 고 hello VMDK 파일 toohello VHD 형식으로 변환 합니다.

    먼저 hello 이미지 tooraw 형식을 변환 합니다.

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다. 그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hello 원시 디스크 tooa 변환 고정 크기의 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>자동으로 kickstart 파일을 사용하여 ISO에서 Red Hat 기반 가상 컴퓨터 준비
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>kickstart 파일에서 RHEL 7 가상 컴퓨터 준비

1.  Hello 다음 콘텐츠를 포함 하는 뿐 파일 만들고 hello 파일을 저장 합니다. 활용 설치에 대 한 자세한 참조 hello [활용 설치 가이드](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html)합니다.

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Hello 설치 시스템 액세스할 수 있는 hello 활용 파일을 배치 합니다.

3. Hyper-V 관리자에서 새 가상 컴퓨터를 만듭니다. Hello에 **가상 하드 디스크 연결** 페이지에서 **나중에 가상 하드 디스크 연결**, 및 새 가상 컴퓨터 마법사 완료 hello 합니다.

4. Hello 가상 컴퓨터 설정을 엽니다.

    a.  새 가상 하드 디스크 toohello 가상 컴퓨터를 연결 합니다. 있는지 tooselect 확인 **VHD 형식** 및 **고정 크기**합니다.

    b.  Hello 설치 ISO toohello DVD 드라이브를 연결 합니다.

    c.  CD에서 hello BIOS tooboot를 설정 합니다.

5. Hello 가상 컴퓨터를 시작 합니다. Hello 설치 가이드에 표시 되 면 키를 눌러 **탭** tooconfigure hello 부팅 옵션입니다.

6. Enter `inst.ks=<hello location of hello kickstart file>` hello 부팅 옵션 및 키를 눌러 hello 끝 **Enter**합니다.

7. Hello 설치 toofinish 될 때까지 기다립니다. 완료 되 면 hello 가상 컴퓨터 종료 됩니다. 자동으로. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.

## <a name="known-issues"></a>알려진 문제
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>비 Hyper-v 하이퍼바이저를 사용 하는 경우 초기 RAM 디스크 hello에에서 hello Hyper-v 드라이버를 포함할 수 없습니다.

경우에 따라 Linux 설치 관리자가 포함 되지 않을 수 hello 드라이버 Hyper-v에 대 한 hello 초기 RAM 디스크 (initrd 또는 initramfs)에서 Linux Hyper-v 환경에서 실행 되 고 있는지를 검색 하지 않는 한 합니다.

다른 가상화 (즉, Virtualbox, Xen 등)의 시스템 tooprepare Linux 이미지를 사용 하는 경우 적어도 hv_vmbus hello toorebuild initrd tooensure 할 수 있습니다 및 hv_storvsc 커널 모듈 hello 초기 RAM 디스크에서 사용할 수 있습니다. 이것은 알려진된 문제 이상 hello 업스트림 Red Hat 배포를 기반으로 하는 시스템에 있습니다.

tooresolve이이 문제는 Hyper-v 모듈 tooinitramfs를 추가 하 고 다시 작성 합니다.

편집 `/etc/dracut.conf`, hello 다음 콘텐츠를 추가 합니다.

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Initramfs를 다시 빌드합니다.

        # dracut -f -v

자세한 내용은 hello 정보에 대 한 참조 [initramfs 다시 작성](https://access.redhat.com/solutions/1958)합니다.

## <a name="next-steps"></a>다음 단계
사용자는 이제 준비 toouse Azure에서 Red Hat Enterprise Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터. 인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

Red Hat Enterprise Linux toorun는 hello 하이퍼바이저에 대 한 자세한 내용은 인증에 대 한 참조 [hello Red Hat 웹 사이트](https://access.redhat.com/certified-hypervisors)합니다.
