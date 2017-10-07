---
title: "Azure에서 aaaIntroduction tooLinux | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터를 사용하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>Azure에서 tooLinux 소개
이 항목에서는 일부의 Linux 가상 컴퓨터를 사용 하 여 Azure 클라우드 hello에 대 한 개요를 제공 합니다. Hello 갤러리에서 이미지를 사용 하는 간단한 프로세스는 Linux 가상 컴퓨터를 배포 합니다.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>인증: 사용자 이름, 암호 및 SSH 키
어느 사용자 이름을 tooprovide 묻는 hello Azure 포털을 사용 하 여 Linux 가상 컴퓨터를 만들 때 암호 또는 SSH 공개 키 및 합니다. hello 선택 Azure에서 Linux 가상 컴퓨터를 배포 하기 위한 사용자 이름이 제약 조건에 따라 주체 toohello: 시스템 계정의 이름이 (UID < 100) hello에 이미 있는 가상 컴퓨터가 허용 되지 않으면 '루트' 예입니다.

* [Linux를 실행하는 가상 컴퓨터 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
* 참조 [어떻게 tooUse와 Azure에서 Linux에 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>`sudo`
Azure에서 가상 컴퓨터 인스턴스에 배포 하는 동안 지정 된 hello 사용자 계정은 권한 있는 계정이입니다. Hello Azure Linux 에이전트 toobe 수 tooelevate 권한 tooroot (superuser 계정이) hello를 사용 하 여이 계정이 구성 되어 `sudo` 유틸리티입니다. 이 사용자 계정을 사용 하 여 로그인 한 hello 명령 구문을 사용 하는 루트로 수 toorun 명령 수 있습니다.

    # sudo <COMMAND>

선택적으로 **sudo -s**를 사용하여 루트 셸을 얻을 수 있습니다.

* [Azure의 Linux 가상 컴퓨터에서 루트 권한 사용](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.

## <a name="firewall-configuration"></a>방화벽 구성
Azure 연결 tooports hello Azure 포털에에서 지정 된 제한 하는 인바운드 패킷 필터를 제공 합니다. 기본적으로 hello 허용 되는 포트만 SSH 합니다. Hello Azure 포털에서에서 끝점을 구성 하 여 Linux 가상 컴퓨터에 액세스 tooadditional 포트를 열 수 있습니다.

* 참고: [어떻게 tooSet 끝점 tooa 가상 컴퓨터](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

hello Azure 갤러리의에서 hello Linux 이미지 hello를 사용 하지 않으면 *iptables* 기본적으로 방화벽입니다. 원하는 경우 hello 방화벽을 구성할 수 있습니다 tooprovide 추가 필터링 합니다.

## <a name="hostname-changes"></a>호스트 이름 변경
Linux 이미지의 인스턴스를 처음 배포할 때는 필요한 tooprovide hello 가상 컴퓨터에 대 한 호스트 이름이 됩니다. Hello 가상 컴퓨터가 실행 되 면 여러 연결 된 가상 컴퓨터 tooeach 다른 호스트 이름을 사용 하는 IP 주소 조회를 수행할 수 있도록이 호스트 이름에 게시 된 toohello 플랫폼 DNS 서버입니다.

가상 컴퓨터를 배포한 후 호스트 이름 변경 내용을 원하는 경우 경우 hello 명령을 사용 하십시오.

    # sudo hostname <newname>

기능을 포함 하는 hello Azure Linux 에이전트 tooautomatically이 이름을 변경 내용을 검색 적절 하 게 구성 hello 가상 컴퓨터 toopersist이이 변경 하 고이 변경 toohello 플랫폼 DNS 서버를 게시 합니다.

* [Azure Linux 에이전트 사용자 가이드](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
**Ubuntu** 및 **CoreOS** 이미지는 cloud-init pn Azure를 활용하여 가상 컴퓨터를 부트스트랩하기 위한 추가 기능을 제공합니다.

* [어떻게 tooInject 데이터 사용자 지정](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Microsoft Azure의 사용자 지정 데이터 및 Cloud-Init](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Init 클라우드를 사용하여 Azure 스왑 파티션 만들기](https://wiki.ubuntu.com/AzureSwapPartitions)
* [어떻게 tooUse CoreOS Azure에서](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>가상 컴퓨터 이미지 캡처
Azure는 이후에 사용된 toodeploy 추가 가상 컴퓨터 인스턴스 수 있는 이미지에 기존 가상 컴퓨터의 hello 기능 toocapture hello 상태를 제공 합니다. hello Azure Linux 에이전트에 사용 되는 toorollback 일부 hello hello를 프로 비전 프로세스 중 수행 된 사용자 지정 될 수 있습니다. 이미지 형식으로 toocapture 가상 컴퓨터 아래 hello 단계를 수행 될 수 있습니다.

1. 실행 **waagent-deprovision** tooundo 사용자 지정 프로 비전 합니다. 또는 **waagent-deprovision + 사용자** toooptionally hello 사용자 계정을 프로 비전 및 모든 관련 데이터 중에 지정한를 삭제 합니다.
2. / 전원 hello 가상 컴퓨터를 종료 합니다.
3. 클릭 **캡처** hello Azure 포털 또는 사용 하 여 hello PowerShell 또는 CLI 도구 toocapture hello 가상 컴퓨터를 이미지로 합니다.
   
   * 참고: [어떻게 tooCapture 템플릿으로 Linux 가상 컴퓨터 tooUse](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>디스크 연결
각 가상 컴퓨터에는 임시 로컬 *리소스 디스크* 가 연결되어 있습니다. 다시 부팅 해도 리소스 디스크의 데이터를 영구 수 있습니다, 때문에 종종 응용 프로그램 및 일시적이 지에 대 한 hello 가상 컴퓨터에서 실행 중인 프로세스에서 사용 됩니다 하 고 **임시** 데이터를 저장 합니다. 사용 되는 toostore hello 운영 체제에 대 한 페이지 또는 스왑 파일과 hello 이기도합니다.

Linux hello 리소스 디스크 hello Azure Linux 에이전트에서 관리 하는 않으며 자동으로 너무 탑재**/mnt/리소스** (또는 **/mnt** Ubuntu 이미지에).

> [!NOTE]
> 해당 하는 hello 리소스 디스크는 한 **임시** , 디스크 및 수 삭제 되 고 hello VM 다시 부팅 될 때 다시 포맷 합니다.
> 
> 

Linux에서 hello 데이터 디스크와 hello 커널에서 이름이 수 있습니다 `/dev/sdc`, 사용자가을 toopartition 해야 하 고 서식을 지정 하 고 해당 리소스를 탑재 합니다. 이 내용은 hello 자습서의 단계별 설명: [어떻게 tooAttach 데이터 디스크 tooa 가상 컴퓨터](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

* **참고 항목:** [Linux에서 소프트웨어 RAID 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Azure에서 Linux VM에 대해 LVM 구성](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

