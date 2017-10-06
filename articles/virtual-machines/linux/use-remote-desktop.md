---
title: "Azure에서 Linux VM aaaUse 원격 데스크톱 tooa | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 그래픽 도구를 사용 하 여 Azure에서 원격 데스크톱 (xrdp) tooconnect tooa Linux VM을 구성 하 고"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>설치 하 고 Azure에서 원격 데스크톱 tooconnect tooa Linux VM 구성
Azure에서 Linux 가상 컴퓨터 (Vm)는 안전한 셸 SSH 연결을 사용 하 여 hello 명령줄에서 일반적으로 관리 됩니다. 때 새 tooLinux 또는 빠른 문제 해결 시나리오에 대 한 원격 데스크톱의 hello 사용이 더 쉬울 수도 있습니다. 이 세부 정보를 어떻게 문서 tooinstall 데스크톱 환경을 구성 하 고 ([xfce](https://www.xfce.org)) 및 원격 데스크톱 ([xrdp](http://www.xrdp.org)) hello 리소스 관리자 배포 모델을 사용 하 여 Linux VM에 대 한 합니다.


## <a name="prerequisites"></a>필수 조건
이 문서에는 Azure의 기존 Linux VM이 필요합니다. VM toocreate 해야 할 경우 hello 메서드를 다음 중 하나를 사용 합니다.

- hello [Azure CLI 2.0](quick-create-cli.md)
- hello [Azure 포털](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Linux VM에서 데스크톱 환경 설치
Azure의 Linux VM은 대부분 데스크톱 환경을 기본적으로 설치할 필요가 없습니다. Linux VM은 일반적으로 데스크톱 환경이 아닌 SSH 연결을 사용하여 관리됩니다. Linux에서 다양한 데스크톱 환경을 선택할 수 있습니다. 데스크톱 환경의 선택에 따라 것 수 too2 1GB의 디스크 공간을 소비 5 too10 분 tooinstall과 모든 hello 필요한 패키지를 구성 합니다.

hello 다음 예제에서는 설치 hello lightweight [xfce4](https://www.xfce.org/) Ubuntu VM에서 데스크톱 환경입니다. 조금씩 다른 배포에 대 한 명령 (사용 하 여 `yum` tooinstall Red Hat Enterprise Linux에 적절 한 구성 및 `selinux` 규칙 또는 사용 `zypper` 예를 들어, SUSE에 tooinstall).

첫째, SSH tooyour VM입니다. hello 다음 예제에서는 연결 toohello 라는 VM *myvm.westus.cloudapp.azure.com* 의 hello username *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Windows를 사용 하는 SSH를 사용 하 여에 자세한 정보가 필요한 경우 참조 [windows toouse SSH 키는 어떻게](ssh-from-windows.md)합니다.

다음으로 다음과 같이 `apt`를 사용하여 xfce를 설치합니다.

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>원격 데스크톱 서버 설치 및 구성
설치 된 데스크톱 환경이가지고 들어오는 연결에 대 한 원격 데스크톱 서비스 toolisten를 구성 합니다. [xrdp](http://xrdp.org)는 대부분의 Linux 배포판에서 사용할 수 있는 오픈 소스 RDP(원격 데스크톱 프로토콜) 서버로 xfce와 함께 잘 작동합니다. 다음과 같이 Ubuntu VM에 xrdp를 설치합니다.

```bash
sudo apt-get install xrdp
```

사용자 세션을 시작할 때 xrdp 어떤 데스크톱 환경 toouse를 지시 합니다. 다음과 같이 xrdp toouse xfce 데스크톱 환경으로 구성 합니다.

```bash
echo xfce4-session >~/.xsession
```

다음과 같이 hello 변경 tootake 효과 대 한 hello xrdp 서비스를 다시 시작 합니다.

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>로컬 사용자 계정 암호 설정
VM을 만들 때 사용자 계정의 암호를 만든 경우 이 단계를 건너뜁니다. 만 SSH 키 인증을 사용 하 고 로컬 계정 암호 설정, xrdp toolog tooyour VM에서에서 사용 하기 전에 암호를 지정 하지 않은 합니다. xrdp는 인증을 위해 SSH 키를 수락할 수 없습니다. hello 다음 예제에서는 지정 hello 사용자 계정에 대 한 암호 *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> 암호를 지정 하는 현재 없는 경우 프로그램 SSHD 구성 toopermit 암호 로그인 업데이트 되지 않습니다. 보안 측면에서 키 기반 인증을 사용 하 여 SSH 터널이와 tooconnect tooyour VM을 원하는 수 고 tooxrdp 다음 연결할 수 있습니다. 이 경우 네트워크 보안 그룹 규칙 tooallow 원격 데스크톱 트래픽이 만드는 방법에 단계를 수행 하는 hello를 건너뜁니다.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>원격 데스크톱 트래픽의 네트워크 보안 그룹 규칙 만들기
원격 데스크톱 트래픽 tooreach tooallow Linux VM 네트워크 보안 그룹 규칙 필요 toobe 만든 VM 포트 3389 tooreach에 TCP를 허용 하 합니다. 네트워크 보안 그룹 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요. 수도 있습니다 [사용 하 여 Azure 포털 toocreate를 네트워크 보안 그룹 규칙 hello](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

hello 다음 예제에서는 네트워크 보안 그룹 규칙으로 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 라는 *myNetworkSecurityGroupRule* 너무*허용* 에서트래픽을*tcp* 포트 *3389*합니다.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>원격 데스크톱 클라이언트와 Linux VM 연결
로컬 원격 데스크톱 클라이언트를 열고 toohello IP 주소 또는 Linux VM의 DNS 이름을 연결 합니다. Hello 사용자 이름 및 암호 hello 사용자 계정에 대 한 VM에 다음과 같이 입력 합니다.

![원격 데스크톱 클라이언트를 사용 하 여 tooxrdp 연결](./media/use-remote-desktop/remote-desktop-client.png)

를 인증 한 후 hello xfce 데스크톱 환경을 로드 하 고 다음 예제와 비슷한 toohello를 찾습니다.

![xrdp를 통한 xfce 데스크톱 환경](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>문제 해결
원격 데스크톱 클라이언트를 사용 하 여 Linux VM tooyour를 연결할 수 없는 경우 사용 하 여 `netstat` VM RDP 연결을 위해 다음과 같이 수신 하 여 Linux VM tooverify에:

```bash
sudo netstat -plnt | grep rdp
```

다음 예제와 hello hello 3389 예상 대로 TCP 포트에서 수신 대기 하는 VM:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Hello xrdp 서비스가 수신 대기 하지 않는 경우 Ubuntu VM에서 서비스를 다시 시작 hello 다음과 같습니다.

```bash
sudo service xrdp restart
```

검토 로그인 */var/로그*몸이 야 toowhy hello 서비스로 표시에 대 한 Ubuntu VM에 응답 하지 않을 수 있습니다. 모든 오류는 원격 데스크톱 연결 시도가 tooview 중 hello syslog를도 모니터링할 수 있습니다.

```bash
tail -f /var/log/syslog
```

다양 한 방법 toorestart 서비스 및 대체 로그 파일 위치 tooreview Red Hat Enterprise Linux 및 SUSE와 같은 다른 Linux 배포판 있을 수 있습니다.

원격 데스크톱 클라이언트에서 받은 모든 응답을 수신 하지 않음 hello 시스템 로그에서 모든 이벤트 표시 되지 않으면 하는 경우이 문제는 원격 데스크톱 트래픽을 hello VM에 연결할 수 없습니다 나타냅니다. 포트 3389에 규칙 toopermit TCP를 포함 하 여 네트워크 보안 그룹 규칙 tooensure를 검토 합니다. 자세한 내용은 [응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md)을 참조하세요.


## <a name="next-steps"></a>다음 단계
Linux VM에서 SSH 키를 만들고 사용하는 방법에 대한 자세한 내용은 [Azure에서 Linux VM의 SSH 키 만들기](mac-create-ssh-keys.md)를 참조하세요.

Windows에서 SSH를 사용 하는 방법은 참조 하십시오. [windows toouse SSH 키는 어떻게](ssh-from-windows.md)합니다.

