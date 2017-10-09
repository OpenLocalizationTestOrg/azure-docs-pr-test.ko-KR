---
title: "aaaCreate 및 Oracle Linux VHD 업로드 | Microsoft Docs"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD)는 Oracle Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Azure용 Oracle Linux 가상 컴퓨터 준비
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>필수 조건
이 문서는 Oracle Linux 운영 체제 tooa 가상 하드 디스크로 이미 설치한 가정 합니다. 여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다. 자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.

### <a name="oracle-linux-installation-notes"></a>Oracle Linux 설치 참고 사항
* Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.
* Oracle Red Hat 호환 커널 및 해당 UEK3(Unbreakable Enterprise Kernel)은 모두 Hyper-V 및 Azure에서 지원됩니다. 최상의 결과 있는지 tooupdate toohello 최신 커널 Oracle Linux VHD를 준비 하는 동안 모니터링할 하십시오.
* Oracle의 UEK2 hello 필요한 드라이버를 포함 하지 않는 Hyper-v와 Azure에서 지원 되지 않습니다.
* hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.  Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.
* Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다. OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이. 원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.
* NUMA는 2.6.37 아래 Linux 커널 버전의 tooa 버그 때문에 더 큰 VM 크기에 대 한 지원 되지 않습니다. 이 문제를 주로 영향을 미치는 분포를 사용 하 여 hello 업스트림 Red Hat 2.6.32 커널 합니다. (Waagent) hello Azure Linux 에이전트를 수동으로 설치는 자동으로 Linux 커널 hello에 대 한 hello GRUB 구성에서 NUMA를 비활성화 합니다. 이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.
* 스왑 파티션을 hello OS 디스크에 구성 하지 마십시오. hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.  이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.
* 모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.
* 해당 hello 있는지 확인 `Addons` 리포지토리를 사용할 수 있습니다. Hello 파일을 편집 `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) 또는 `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), hello 줄을 변경 하 고 `enabled=0` 너무`enabled=1` 아래 **[ol6_addons]** 또는 **[ol7_addons]** 이 파일입니다.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4 이상
Azure에서 가상 컴퓨터 toorun hello에 대 한 hello 운영 체제에서 특정 구성 단계를 완료 해야 합니다.

1. Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.
2. 클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.
3. NetworkManager hello 다음 명령을 실행 하 여 제거 합니다.
   
        # sudo rpm -e --nodeps NetworkManager
   
    **참고:** hello 패키지 아직 설치 되지 않은 오류 메시지와 함께이 명령이 실패 합니다. 예상된 동작입니다.
4. 라는 파일을 만들어 **네트워크** hello에 `/etc/sysconfig/` hello 텍스트 다음 포함 된 디렉터리:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. 라는 파일을 만들어 **ifcfg eth0** hello에 `/etc/sysconfig/network-scripts/` hello 텍스트 다음 포함 된 디렉터리:
   
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
   
        # chkconfig network on
8. Python pyasn1 hello 다음 명령을 실행 하 여 설치 합니다.
   
        # sudo yum install python-pyasn1
9. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. 이 열린 toodo "/ boot/grub/menu.lst" 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 및:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다. Oracle의 Red Hat 호환 커널에서 tooa 버그 인해 NUMA 해제 됩니다.
   
   또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:
   
        rhgb quiet crashkernel=auto
   
   그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.
   
   hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.
10. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.
11. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다. hello 최신 버전은 2.0.15입니다.
    
        # sudo yum install WALinuxAgent
    
    설치 hello WALinuxAgent 패키지는 hello NetworkManager 제거 및 NetworkManager gnome 패키지는 제거 되지 않은 경우 이미 설명 된 대로 2 단계에서 note 합니다.
12. Hello OS 디스크에 스왑 공간을 만들지 마십시오.
    
    hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:
    
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

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0
**Oracle Linux 7의 변경 내용**

하지만 Oracle Linux 7 가상 컴퓨터를 준비 하 고 Azure에 대 한 매우 유사 몇 가지 중요 한 차이점이 주목할 만한 Linux 6, tooOracle은입니다.

* Red Hat 호환 커널 hello 및 Oracle의 UEK3 모두 Azure에서 지원 됩니다.  hello UEK3 커널 것이 좋습니다.
* hello NetworkManager 패키지 더 이상 hello Azure Linux 에이전트와 충돌 합니다. 이 패키지는 기본적으로 설치되며 제거하지 않는 것이 좋습니다.
* 이제 커널 매개 변수를 편집 하기 위해 hello 절차 (아래 참조) 변경 된 하므로 기본 부팅 로더를 hello GRUB2 사용 됩니다.
* XFS는 hello 기본 파일 시스템 되었습니다. 원하는 경우에 여전히 hello ext4 파일 시스템을 사용할 수 있습니다.

**구성 단계**

1. Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.
2. 클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.
3. 라는 파일을 만들어 **네트워크** hello에 `/etc/sysconfig/` hello 텍스트 다음 포함 된 디렉터리:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. 라는 파일을 만들어 **ifcfg eth0** hello에 `/etc/sysconfig/network-scripts/` hello 텍스트 다음 포함 된 디렉터리:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다. 이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. 확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.
   
        # sudo chkconfig network on
7. Hello 다음 명령을 실행 하 여 hello pyasn1 python 패키지를 설치 합니다.
   
        # sudo yum install python-pyasn1
8. Hello 명령 tooclear hello 현재 yum 메타 데이터를 다음를 실행 하 고 모든 업데이트를 설치 합니다.
   
        # sudo yum clean all
        # sudo yum -y update
9. Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다. 이 열려 "/ 등/기본/grub" toodo 텍스트 편집기 및 편집 hello에 `GRUB_CMDLINE_LINUX` 예를 들어 매개 변수:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다. 또한 Nic 동안 OEL 7 명명 규칙을 새 hello 하지 않습니다. 또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:
   
       rhgb quiet crashkernel=auto
   
   그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.
   
   hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.
10. 편집 "/ 등/기본/grub" 완료 되 면 당 위에서 실행 같은 명령 toorebuild hello grub 구성이 hello:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.
12. Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Hello OS 디스크에 스왑 공간을 만들지 마십시오.
    
    hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (hello 이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.

## <a name="next-steps"></a>다음 단계
사용자는 이제 준비 toouse Azure에서 Oracle Linux.vhd toocreate 새 가상 컴퓨터. 인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

