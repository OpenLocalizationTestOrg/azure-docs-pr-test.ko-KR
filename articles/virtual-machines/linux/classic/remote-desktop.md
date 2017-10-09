---
title: "Linux VM aaaRemote 데스크톱 tooa | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall hello 클래식 배포 모델에 대 한 원격 데스크톱 tooconnect tooa Microsoft Azure Linux VM을 구성 하 고"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>원격 데스크톱 tooconnect tooa Microsoft Azure Linux VM을 사용 하 여
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 이 문서의 버전 리소스 관리자를 업데이트 하는 hello에 대 한 참조 [여기](../use-remote-desktop.md)합니다.

## <a name="overview"></a>개요
RDP(원격 데스크톱 프로토콜)는 Windows에 사용되는 독점 프로토콜입니다. RDP tooconnect tooa Linux VM (가상 컴퓨터)를 원격으로 사용할 수 어떻게 우리?

이 지침은 제공 됩니다 응답 hello! Windows 컴퓨터에서 원격 데스크톱 tooit를 연결할 수 하 여 Microsoft Azure Linux VM에서 tooinstall 및 config xrdp을 도움이 됩니다. 이 설명서에 hello 예로 Ubuntu 또는 OpenSUSE를 실행 하는 Linux VM을 사용 합니다.

hello xrdp 도구는 오픈 소스 RDP 서버 tooconnect 수 있는 Windows 컴퓨터에서 원격 데스크톱을 사용 하 여 Linux 서버입니다. RDP는 VNC(Virtual Network Computing)보다 더 강력한 성능을 구현합니다. RDP는 빠르고 선명한 반면 VNC는 JPEG 수준의 그래픽을 사용하여 렌더링하며 속도가 느려질 수 있습니다.

> [!NOTE]
> Linux를 실행하는 Microsoft Azure VM이 있어야 합니다. toocreate 및 Linux VM 설정을 참조 hello [Azure Linux VM 자습서](createportal.md)합니다.
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>원격 데스크톱에 대한 끝점 만들기
이 문서에서 원격 데스크톱에 대 한 hello 기본 끝점 3389 사용 합니다. 3389 끝점으로 설정 `Remote Desktop` 다음과 유사한 tooyour Linux VM:

![이미지](./media/remote-desktop/endpoint-for-linux-server.png)

알 수 없는 경우 tooset VM에 대 한 끝점을 확인 하려면 어떻게 해야 [이 지침은](setup-endpoints.md)합니다.

## <a name="install-gnome-desktop"></a>Gnome 데스크톱 설치
Tooyour Linux VM에 연결을 통해 `putty`, 설치 및 `Gnome Desktop`합니다.

Ubuntu의 경우 다음을 사용합니다.

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


OpenSUSE의 경우 다음을 사용합니다.

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>xrdp 설치
Ubuntu의 경우 다음을 사용합니다.

    #sudo apt-get install xrdp

OpenSUSE의 경우 다음을 사용합니다.

> [!NOTE]
> Hello 다음 명령을 사용 하는 hello 버전으로 hello OpenSUSE 버전을 업데이트 합니다. 아래 예제에서는 hello에 대 한는 `OpenSUSE 13.2`합니다.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>xrdp를 시작하고 부팅에 xdrp 서비스를 설정합니다.
OpenSUSE의 경우 다음을 사용합니다.

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Ubuntu의 경우 설치 후 부팅 시 자동으로 xrdp가 시작되어 사용됩니다.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Ubuntu 12.04LTS보다 높은 Ubuntu 버전을 사용하는 경우 xfce를 사용
사용 합니다 hello xrdp의 현재 버전에서 지원 하지 않으므로 Gnome 데스크톱 Ubuntu 버전에 대 한 Ubuntu 12.04LTS 이후, `xfce` 데스크톱 대신 합니다.

tooinstall `xfce`,이 명령을 사용 합니다.

    #sudo apt-get install xubuntu-desktop

그런 다음 이 명령을 사용하여 `xfce`를 활성화합니다.

    #echo xfce4-session >~/.xsession

Hello 구성 파일 편집 `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Hello 줄 추가 `xfce4-session` hello 줄 앞 `/etc/X11/Xsession`합니다.

toorestart xrdp 서비스 hello,이 사용 하 여:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Windows 컴퓨터에서 Linux VM 연결
Windows 컴퓨터에서 원격 데스크톱 클라이언트 hello 시작한 Linux VM의 DNS 이름을 입력 하십시오. 또는 toohello hello Azure 포털에서에서 VM의 대시보드를 이동 하 고 클릭 `Connect` tooconnect Linux VM입니다. 이 경우 hello 로그인 창이 표시 됩니다.

![이미지](./media/remote-desktop/no2.png)

Hello 사용자 이름 및 Linux VM의 암호를 로그인 합니다.

## <a name="next-steps"></a>다음 단계
xrdp 사용에 대한 자세한 내용은 [http://www.xrdp.org/](http://www.xrdp.org/)를 참조하세요.
