---
title: "aaaCreate 및 Azure에서 Linux CentOS 기반 VHD 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD) CentOS 기반 Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Azure용 CentOS 기반 가상 컴퓨터 준비
* [Azure용 CentOS 6.x 가상 컴퓨터 준비](#centos-6x)
* [Azure용 CentOS 7.0 이상 가상 컴퓨터 준비](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>필수 조건
이 문서는 CentOS 이미 설치한 것으로 가정 (또는 유사한 파생물) Linux 운영 체제 tooa 가상 하드 디스크입니다. 여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다. 자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.

**CentOS 설치 참고 사항**

* Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.
* hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.  Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다. VirtualBox를 사용 하는 경우 선택 하는 것이 즉 **고정 크기** 으로 반대로 toohello 기본 hello 디스크를 만들 때 동적으로 할당 합니다.
* hello Linux 시스템을 설치할 때 *권장* LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하면 됩니다. OS 디스크 연결 toobe tooanother 해야 합니다. 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 방지 합니다이 문제 해결을 위해 동일한 VM입니다. 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.
* UDF 파일 시스템 탑재에 대한 커널 지원이 필요합니다. 첫 번째 부팅 Azure hello에-프로비저닝 구성 toohello Linux VM은 연결 된 toohello 게스트 UDF로 포맷 된 미디어를 통해 전달 됩니다. hello Azure Linux 에이전트는 해당 구성을 수 toomount hello UDF 파일 시스템 tooread 수 하 고 hello VM을 프로 비전 해야 합니다.
* 2.6.37 버전 미만의 Linux 커널은 VM 크기가 더 클 때 Hyper-V에서 NUMA를 지원하지 않습니다. 이 문제를 주로 영향 업스트림 hello를 사용 하 여 이전 분포 Red Hat 2.6.32 커널 RHEL 6.6 (커널 2.6.32 504)에서 수정 되었습니다. 2.6.32-504 설정 해야 하는 보다 2.6.37, 다음 보다 오래 된 사용자 지정 커널 또는 이전 RHEL 기반 커널을 실행 하는 시스템 부팅 매개 변수를 hello `numa=off` hello 커널 grub.conf의 명령줄입니다. 자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.
* 스왑 파티션을 hello OS 디스크에 구성 하지 마십시오. hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.  이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.
* 모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.

## <a name="centos-6x"></a>CentOS 6.x

1. Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.

2. 클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.

3. CentOS 6의 NetworkManager hello Azure Linux 에이전트와 방해할 수 있습니다. Hello 다음 명령을 실행 하 여이 패키지를 제거 합니다.
   
        # sudo rpm -e --nodeps NetworkManager

4. Hello 파일 만들기 또는 편집 `/etc/sysconfig/network` hello 텍스트 다음 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Hello 파일 만들기 또는 편집 `/etc/sysconfig/network-scripts/ifcfg-eth0` hello 텍스트 다음 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다. 이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.
   
        # sudo chkconfig network on

8. Hello Azure 데이터 센터 내에 호스팅되는 toouse hello OpenLogic 미러를 원하는 경우 hello 바꿉니다 `/etc/yum.repos.d/CentOS-Base.repo` 저장소 다음 hello로는 파일입니다.  Hello도 추가 **[openlogic]** hello Azure Linux 에이전트와 같은 추가 패키지를 포함 하는 저장소:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    hello이 가이드의 나머지 부분 가정 사용 하는 hello 이상 `[openlogic]` 리포지토리 사용된 tooinstall hello Azure Linux 에이전트 아래 됩니다.


9. 다음 줄 too/etc/yum.conf hello를 추가 합니다.
    
        http_caching=packages

10. Hello 명령 tooclear hello 현재 yum 메타 데이터 및 업데이트 hello 시스템 hello 최신 패키지와 함께 다음을 실행 합니다.
    
        # yum clean all

    CentOS의 이전 버전에 대 한 이미지를 만드는 경우가 아니면 모든 hello tooupdate toohello를 최신 패키지 것이 좋습니다.

        # sudo yum -y update

    이 명령을 실행한 후 다시 부팅해야 할 수 있습니다.

11. (선택 사항) Linux Integration Services (LIS) hello에 대 한 hello 드라이버를 설치 합니다.
   
    >[!IMPORTANT]
    hello 단계는 **필요한** CentOS 6.3 및 이전 버전 및 이후 릴리스에 대 한 선택 사항에 대 한 합니다.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Hello에서 hello 수동 설치 지침을 따를 수 또는 [LIS 다운로드 페이지](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM VM에 있습니다.
 
12. Hello Azure Linux 에이전트 및 종속성을 설치 합니다.
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    hello WALinuxAgent 패키지는 제거 되지 않은 경우 이미 3 단계에 설명 된 대로 NetworkManager hello 및 NetworkManager gnome 패키지 제거 됩니다.


13. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo이,이 오픈 `/boot/grub/menu.lst` 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 하 고 있습니다.
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.
    
    또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:
    
        rhgb quiet crashkernel=auto
    
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.  hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.

    >[!Important]
    CentOS 6.5 및 이전 버전도 hello 커널 매개 변수를 설정 해야 `numa=off`합니다. Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.

14. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.

15. Hello OS 디스크에 스왑 공간을 만들지 마십시오.
    
    hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조)의 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.


- - -
## <a name="centos-70"></a>CentOS 7.0 이상
**CentOS 7 및 유사한 파생 버전의 변경 내용**

그러나 몇 가지 중요 한 차이점이 주목할 만한 매우 유사한 tooCentOS 6는 CentOS 7 가상 컴퓨터를 Azure에 대 한 준비:

* hello NetworkManager 패키지 더 이상 hello Azure Linux 에이전트와 충돌 합니다. 이 패키지는 기본적으로 설치되며 제거하지 않는 것이 좋습니다.
* 이제 커널 매개 변수를 편집 하기 위해 hello 절차 (아래 참조) 변경 된 하므로 기본 부팅 로더를 hello GRUB2 사용 됩니다.
* XFS는 hello 기본 파일 시스템 되었습니다. 원하는 경우에 여전히 hello ext4 파일 시스템을 사용할 수 있습니다.

**구성 단계**

1. Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.

2. 클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.

3. Hello 파일 만들기 또는 편집 `/etc/sysconfig/network` hello 텍스트 다음 추가:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Hello 파일 만들기 또는 편집 `/etc/sysconfig/network-scripts/ifcfg-eth0` hello 텍스트 다음 추가:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다. 이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Hello Azure 데이터 센터 내에 호스팅되는 toouse hello OpenLogic 미러를 원하는 경우 hello 바꿉니다 `/etc/yum.repos.d/CentOS-Base.repo` 저장소 다음 hello로는 파일입니다.  Hello도 추가 **[openlogic]** hello Azure Linux 에이전트에 대 한 패키지를 포함 하는 저장소:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    hello이 가이드의 나머지 부분 가정 사용 하는 hello 이상 `[openlogic]` 리포지토리 사용된 tooinstall hello Azure Linux 에이전트 아래 됩니다.

7. Hello 명령 tooclear hello 현재 yum 메타 데이터를 다음를 실행 하 고 모든 업데이트를 설치 합니다.
   
        # sudo yum clean all

    CentOS의 이전 버전에 대 한 이미지를 만드는 경우가 아니면 모든 hello tooupdate toohello를 최신 패키지 것이 좋습니다.

        # sudo yum -y update

    이 명령을 실행한 후 다시 부팅해야 할 수 있습니다.

8. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. toodo이,이 오픈 `/etc/default/grub` 텍스트 편집기 및 편집 hello에 `GRUB_CMDLINE_LINUX` 예를 들어 매개 변수:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다. 또한 Nic 동안 CentOS 7 명명 규칙을 새 hello 하지 않습니다. 또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:
   
        rhgb quiet crashkernel=auto
   
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.

9. 완료 되 면 편집 `/etc/default/grub` 당 위에서 실행 같은 명령 toorebuild hello grub 구성이 hello:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Hello 이미지에서 작성 하는 경우 **VMWare, VirtualBox 또는 KVM:** 확인 hello Hyper-v 드라이버 hello initramfs에 포함 됩니다.
   
   `/etc/dracut.conf`를 편집하고 콘텐츠를 추가합니다.
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Hello initramfs 다시 작성 하십시오.
   
        # sudo dracut –f -v

11. Hello Azure Linux 에이전트 및 종속성을 설치 합니다.

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Hello OS 디스크에 스왑 공간을 만들지 마십시오.
   
   hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조)의 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게:
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.

## <a name="next-steps"></a>다음 단계
사용자는 이제 준비 toouse Azure에서 CentOS Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터. 인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

