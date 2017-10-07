---
title: "Azure Linux 가상 컴퓨터에서 SSHD aaaConfigure | Microsoft Docs"
description: "보안 모범 사례 및 toolockdown SSH tooAzure Linux 가상 컴퓨터에 대 한 SSHD를 구성 합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Azure Linux VM에서 SSHD 구성

이 문서에서는 toolockdown 암호 대신 SSH 키를 사용 하 여 Linux, tooprovide 모범 사례 보안 및 hello SSH 로그인 프로세스를 toospeed SSH 서버를 hello 하는 방법을 보여 줍니다.  toofurther 잠금 수 toologin 없도록 toodisable hello 루트 사용자를 하겠습니다 SSHD 제한 hello 수 있는 사용자는 승인 된 그룹 목록을 통해 toologin SSH 프로토콜 버전 1을 사용 하지 않도록 설정 하 고, 최소 비트 키를 설정, 유휴 사용자의 자동 로그 아웃을 구성 합니다.  이 문서에 대 한 hello 요구 사항은: Azure 계정 ([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/)) 및 [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="quick-commands"></a>빠른 명령

구성 `/etc/ssh/sshd_config` 설정 다음 hello로:

### <a name="disable-password-logins"></a>암호 로그인 사용 안 함

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Hello 루트 사용자가 로그인을 사용 하지 않도록 설정

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>그룹 목록 허용

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>사용자 목록 허용

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>SSH 프로토콜 버전 1을 사용하지 않도록 설정

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>최소 키 비트

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>유휴 사용자 연결 끊기

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>자세한 연습

SSHD는 hello hello Linux VM에서 실행 되는 SSH 서버입니다.  SSH는 MacBook의 셸, Linux 워크스테이션 또는 Windows의 Bash에서 실행되는 클라이언트입니다.  SSH는 hello toosecure 사용 되는 프로토콜과 워크스테이션 및 hello SSH VPN (가상 사설망)도 수행 하는 Linux VM 간의 hello 통신을 암호화 이기도 합니다.

이 문서는 매우 중요 한 tookeep 하나의 로그인 tooyour hello 전체 연습에 대 한 Linux VM 엽니다.  SSH 연결 설정 되 면로 그대로 남아 세션이 열린으로 hello 창이 닫혀 있지 않습니다.  로그인 한 터미널에 대해 있습니다 변경 내용을 toobe toohello SSHD 서비스를 없이 주요 변경 내용이 경우 잠깁니다.  끊어진된 SSHD 구성 사용 하 여 Linux VM 수행 잠기는, Azure 기능을 제공 hello 기능 tooreset hello로 손상된 된 SSHD 구성 [Azure VM 액세스 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

이러한 이유로 म 열고 두 터미널 SSH toohello Linux VM에서 둘 모두.  Hello 첫 번째 터미널 toomake hello 변경 tooSSHDs 구성 파일을 사용 하 고 hello SSHD 서비스를 다시 시작 합니다.  이러한 변경 사항이 hello 서비스 다시 시작 되 면 터미널 tootest 두 번째 hello를 사용 합니다.  SSH 암호를 해제 하는 것 이므로 엄격 하 게 SSH 키, SSH 키에 잘못 된 하 고 hello 연결 toohello VM을 닫으면에 의존 hello VM 영구적으로 됩니다 잠기고 아무도 수 toologin tooit 삭제 하 고 다시 toobe 요구 됩니다.

## <a name="disable-password-logins"></a>암호 로그인 사용 안 함

가장 빠른 방법은 toosecure hello Linux VM는 toodisable 암호 로그인 합니다.  암호 로그인을 사용할 수 없는 hello 암호 SSH를 사용 하 여 Linux VM에 대 한 강제로 봇 크롤링 hello 웹 toobrute 시도 즉시 시작 됩니다.  로그인 암호를 완전히 해제, 모든 암호 로그인 시도 hello SSH 서버 tooignore 수 있습니다.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Hello 루트 사용자가 로그인을 사용 하지 않도록 설정

다음 Linux 모범 사례를 hello `root` 사용자 되지에 사용 하 여 또는 SSH를 통해 기록 되도록 `sudo su`합니다.  루트 수준의 권한이 필요한 모든 명령을 hello를 통해 항상 실행 해야 `sudo` 모든 작업을 나중에 감사를 기록 하는 명령입니다.  사용 하지 않도록 설정 hello `root` SSH를 통한 로그인에서 사용자는 권한이 있는 사용자만 tooSSH 허용지 않습니다 보장 하는 보안 모범 사례 단계입니다.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>그룹 목록 허용

SSH는 사용자 및 그룹에 SSH를 통한 로그인을 허용하거나 허용하지 않도록 제한하는 메서드를 제공합니다.  이 기능은 목록 tooapprove를 사용 하거나 특정 사용자 및 그룹에 로그인 하지 못하도록 거부 합니다.  Hello 휠 그룹 toohello 설정 `AllowGroups` 목록 hello 휠 그룹에 있는 SSH toojust 사용자 계정을 통해 승인 된 로그인을 제한 합니다.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>사용자 목록 허용

Tooaccomplish hello 같은 보다 구체적인 방식으로 작업 하는 SSH 로그인 toojust 사용자 제한 `AllowGroups` 됩니다.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>SSH 프로토콜 버전 1을 사용하지 않도록 설정

SSH 프로토콜 버전 1은 안전하지 않고 비활성화되어야 합니다.  SSH 프로토콜 버전 2는 안전 하 게 tooSSH tooyour 서버에서 제공 하는 hello 현재 버전입니다.  SSH 버전 1 사용 하 여 hello SSH 서버와 tooestablish를 시도 하는 모든 SSH 클라이언트 연결을 거부 SSH 버전 1 사용 하지 않도록 설정 합니다.  SSH 버전 2 연결 toonegotiate 허용 되며 hello SSH 서버와 연결 합니다.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>최소 키 비트

보안 모범 사례 암호 SSH 로그인을 사용할 수 없습니다 및 SSH 키만 toobe tooauthenticate hello SSH 서버에 사용 되는 허용 됩니다.  비트 단위로 측정된 길이가 다른 키를 사용하여 이러한 SSH 키를 만들 수 있습니다.  모범 사례 키 길이가 2048 비트의 hello 최소 허용 가능한 키 길이 상태.  2048비트 미만의 키는 이론적으로 손상되었을 가능성이 있습니다.  설정 hello `ServerKeyBits` 너무`2048` 2048 비트 이상 키를 사용 하 여 모든 연결을 허용 하 고 보다 작은 2048 비트의 연결을 거부 합니다.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>유휴 사용자 연결 끊기

SSH에 대 한 유휴 시간 (초) 정해진된 기간 보다 그 이상 전문적 열린 연결이 있는 hello 기능 toodisconnect 사용자.  열려 있는 세션 tooonly hello Linux VM의 활성 제한 hello 노출을 인 사용자를 유지 합니다.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>SSHD 다시 시작

tooenable hello 설정을 `/etc/ssh/sshd_config` hello SSH 서버를 다시 시작 하는 hello SSHD 프로세스를 다시 시작 합니다.  hello open SSH 세션을 손실 하지 않고 toorestart hello SSH 서버를 사용 하는 hello 터미널 창을 열려 있게 됩니다.  두 번째 터미널 창이 나 탭을 사용 하는 tootest hello 새 SSH 서버 설정 합니다.  별도 터미널 tootest hello SSH 연결을 사용 하 여 다시 toogo 하 고 있습니다 확인 추가 변경 toohello `/etc/ssh/sshd_config` SSHD 주요 변경 내용에 의해 잠기지 않고 hello 첫 번째 터미널에 있습니다.  

### <a name="on-redhat-centos-and-fedora"></a>Redhat, Centos 및 Fedora에서

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Debian 및 Ubuntu에서

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Azure 재설정 액세스를 사용하여 SSHD 다시 설정

주요 변경 toohello SSHD 구성에서 잠긴 경우 hello Azure VM 액세스 확장 tooreset hello SSHD 구성 뒤로 toohello 원래 구성을 사용할 수 있습니다.

모든 예제 이름을 고유한 설정으로 바꿉니다.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Fail2ban 설치

Tooinstall 및 설정 hello 오픈 소스 응용 프로그램 Fail2ban, 블록 무차별 암호 대입을 사용 하 여 SSH를 통해 시도 toologin tooyour Linux VM 반복 가장 좋습니다.  반복 Fail2ban 로그 시도 toologin SSH를 통해 실패 한 다음 방화벽 규칙을 tooblock hello IP 주소에서 비롯 되는지 hello 시도 만듭니다.

* [Fail2ban 홈페이지](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>다음 단계

구성 하 고 hello SSH 서버 잠겨 있으며 Linux VM에서 추가 보안 모범 사례를 따를 수 있습니다.  

* [사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 환영](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Hello Azure CLI를 사용 하 여 Linux VM에서 디스크를 암호화 합니다.](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Azure Resource Manager 템플릿의 액세스 및 보안](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
