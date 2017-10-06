---
title: "aaaCreate 및 Ubuntu Linux VHD를 사용 하 여 Azure에 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD)는 Ubuntu Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Azure용 Ubuntu 가상 컴퓨터 준비
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>공식 Ubuntu 클라우드 이미지
이제 Ubuntu는 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/)에서 다운로드할 수 있도록 공식 Azure VHD를 게시합니다. 그 아래 hello 수동 절차를 사용 하지 않고 toobuild 특수 Ubuntu 이미지 Azure에 필요한 경우 이러한 알려진와 권장된 toostart Vhd 작업 이며 필요에 따라 사용자 지정 합니다. 항상 hello 다음 위치에서 hello 최신 이미지 버전을 찾을 수 있습니다.

* Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>필수 조건
이 문서는 Ubuntu Linux 운영 체제 tooa 가상 하드 디스크로 이미 설치한 가정 합니다. 여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다. 자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.

**Ubuntu 설치 참고 사항**

* Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.
* hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.  Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.
* Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다. OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이. 원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.
* 스왑 파티션을 hello OS 디스크에 구성 하지 마십시오. hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.  이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.
* 모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.

## <a name="manual-steps"></a>수동 단계
> [!NOTE]
> Toocreate 시도 하기 전에 Azure에서 사용자 고유의 사용자 지정 Ubuntu 이미지를 고려 하십시오 hello를 사용 하 여 미리 처음 빌드되고 테스트에서 이미지 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) 대신 합니다.
> 
> 

1. Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.

2. 클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.

3. Hello 현재 저장소에서 Azure hello 이미지 toouse Ubuntu 리포지토리를 대체 합니다. hello 단계 hello Ubuntu 버전에 따라 약간 달라 집니다.
   
    편집 하기 전에 `/etc/apt/sources.list`, 것이 권장 toomake 백업:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. hello Ubuntu Azure 이미지는 이제 다음과 같습니다. hello *하드웨어 사용* 커널 (HWE). Hello 다음 명령을 실행 하 여 hello 운영 체제 toohello 최신 커널을 업데이트 합니다.

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **참고 항목:**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Azure 용 hello 커널 부팅 줄 Grub tooinclude 추가 커널 매개 변수를 수정 합니다. 이 열려 toodo `/etc/default/grub` 텍스트 편집기에서 호출 하는 hello 변수를 찾을 `GRUB_CMDLINE_LINUX_DEFAULT` (또는 필요에 따라 추가) 하 고 매개 변수 뒤 tooinclude hello 편집:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    이 파일을 저장하고 닫은 다음 `sudo update-grub`을 실행합니다. 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트를 Azure 기술 지원 문제 디버깅에 도움이 될 수 있습니다.

6. 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.

7. Hello Azure Linux 에이전트를 설치 합니다.
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    hello `walinuxagent` 패키지 hello 제거 될 수 있습니다 `NetworkManager` 및 `NetworkManager-gnome` 패키지 설치 되어 있는 경우.

8. Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다. Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.

## <a name="next-steps"></a>다음 단계
사용자는 이제 준비 toouse Azure의 Ubuntu Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터. 인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

## <a name="references"></a>참조
Ubuntu 하드웨어 지원(HWE) 커널

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

