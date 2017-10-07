---
title: "Azure에서 Linux Vm에 대 한 aaaCreate는 SSH 키 쌍 | Microsoft Docs"
description: "Azure Linux VM을 위한 SSH 공개 및 개인 키 쌍을 안전하게 만듭니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Linux VM에 대한 SSH 공용 및 개인 키 쌍 만들기

이 문서 toogenerate SSH 프로토콜 버전 2 RSA 공개 및 개인 키 쌍 toouse Linux Vm이 포함 된 파일 하는 방법을 보여 줍니다.  SSH 키 쌍에서 암호 toolog hello 필요성을 제거 기본 인증을 위해 SSH 키 toousing Azure에서 가상 컴퓨터를 만들 수 있습니다.  암호 해독할 수 있으며 toorelentless 무단 시도 tooguess Vm에 암호를 엽니다. Azure 템플릿 또는 hello를 사용 하 여 만든 Vm `azure-cli` SSH에 대 한 로그인 암호를 사용 하지 않도록 설정의 게시물 배포 구성 단계를 제거 하는 hello 배포의 일부로 SSH 공개 키를 포함할 수 있습니다.

## <a name="quick-commands"></a>빠른 명령

명령에서 Bash 셸의 다음, 사용자 고유의 선택 하 여 hello 예제 대체 hello를 실행 합니다.

SSH 공개 키 파일은 기본적으로 `~/.ssh/id_rsa.pub`에 생성됩니다. 대화 상자가 나타나면 다음 명령을 hello를 사용 하 여 만들어야 "암호" toosecure 개인 키로 합니다. (hello 암호는 암호 tooencrypt 사용자의 개인 키를 사용 합니다.)

```bash
ssh-keygen -t rsa -b 2048 
```

새로 만든 hello 키 너무 추가`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> 거의 모든 배포판의 Linux 운영 체제 명령 작업 위에 hello 하지만 반드시 작동 하는 컨테이너에서 hello 환경 근본적으로 제한 될 수 있습니다. 

## <a name="detailed-walkthrough"></a>자세한 연습

SSH 공개 및 개인 키를 사용 하 여 hello tooyour Linux 서버에 가장 쉬운 방법은 toolog입니다. [공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) 무차별 암호 강제 훨씬 더 쉽게 수 있는 암호 보다는 훨씬 더 안전한 방식으로 toolog tooyour Linux에서에서 또는 Azure에서 VM BSD를 제공 합니다.

> [!IMPORTANT]
> 다른 사람과 공개 키를 공유할 수 있지만 사용자(또는 로컬 보안 인프라)만이 개인 키를 소유합니다.  hello SSH 개인 키가 있어야 합니다는 [매우 안전한 방법이 암호](https://www.xkcd.com/936/) (소스:[xkcd.com](https://xkcd.com)) toosafeguard 것입니다.  이 암호는 정당한 tooaccess hello 개인 SSH 키 및 **않습니다** hello 사용자 계정 암호입니다.  Hello 개인 키가 hello 암호 toodecrypt 무용지물이 있도록 128 비트 AES를 사용 하 여 hello 개인 키 암호화 암호 tooyour SSH 키를 추가 하면 것입니다.  공격자가 개인 키로 훔쳐 경우 및 키 암호 없는, 즉 개인 수 toouse 예상 되는 toolog hello 해당 공개 키를 가진 tooany 서버에서 키입니다.  개인 키가 암호로 보호된 경우 공격자가 사용할 수 없어 Azure에서 인프라에 대해 보안 계층을 추가로 제공합니다.

이 문서 SSH 프로토콜 버전 2 RSA 공용 및 개인 키 파일을 만든 hello 리소스 관리자에서 배포에 권장 됩니다.  *ssh rsa* hello에 키가 필요 [포털](https://portal.azure.com) 기본 및 리소스 관리자 배포에 대 한 합니다.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>SSH 키를 사용하여 SSH 암호 비활성화

Azure는 최소한 2048비트, ssh rsa 형식 공개 및 개인 키 서식이 필요합니다. toocreate hello 키를 사용 하 여 `ssh-keygen`, 일련의 질문을 요청 하 고 다음 개인 키와 일치 하는 공개 키를 기록 합니다. Hello 공개 키 너무 복사 하 고 Azure VM이 만들어지면`~/.ssh/authorized_keys`합니다.  SSH 키에 `~/.ssh/authorized_keys` 사용 되는 toochallenge hello 클라이언트 toomatch hello 해당 개인 키에 대 한 SSH 로그인 연결 됩니다.  Azure Linux VM이 만들어지면 인증을 위해 SSH 키를 사용 하 여 Azure hello SSHD 구성 서버 toonot 로그인 암호, SSH 키만 허용 합니다.  따라서 Azure Linux Vm의 경우 SSH 키를 만들면 보안 hello VM 배포에 도움이 되 고 직접 hello sshd_config config 파일에서 암호를 사용 하지 않도록 설정의 hello 일반적인 배포 후 구성 단계를 저장할 수 있습니다.

## <a name="using-ssh-keygen"></a>ssh-keygen 사용

이 명령은 SSH 키 쌍 (암호화 된) 2048 비트 RSA를 사용 하 여 보안 암호를 만들고이 주석 처리 tooeasily 식별 합니다.  

SSH 키가 hello에 보관 하는 기본적으로 `~/.ssh` 디렉터리입니다.  하지 않은 경우는 `~/.ssh` 디렉터리, hello `ssh-keygen` 명령 그 사용자를 위해 만드는 hello로 올바른 사용 권한이 있습니다.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*설명된 명령*

`ssh-keygen`= hello 사용 프로그램 toocreate hello 키

`-t rsa`hello RSA 형식인 키 toocreate 유형의 = [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`hello 키의 비트


## <a name="classic-portal-and-x509-certs"></a>클래식 포털 및 X.509 인증서

사용 중인 경우 Azure hello [클래식 포털](https://manage.windowsazure.com/), hello SSH 키에 대 한 X.509 인증서를 필요로 합니다.  다른 형식의 SSH 공개 키는 허용되지 않으며 *X.509 인증서여야 합니다*.

toocreate 기존 SSH RSA 개인 키에서 된 X.509 인증서:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>`asm`을 사용하여 클래식 배포

Hello 클래식을 사용 하는 경우 모델을 배포 (Azure 서비스 관리 CLI `asm`), SSH RSA 공개 키를 사용할 수 있습니다 또는 RFC4716 서식이 지정 된 키에 **.pem** 컨테이너입니다.  hello SSH RSA 공개 키가 사용 하 여이 문서 앞부분에서 만들어진 `ssh-keygen`합니다.

RFC4716 toocreate 기존 SSH 공개 키에서 키 서식이 지정 됩니다.

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>ssh-keygen 예제

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

저장된 키 파일:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

이 문서에 대 한 hello 키 쌍 이름입니다.  명명 된 키 쌍을 필요 **id_rsa** hello 기본 템플릿이 고 일부 도구는 hello 예상 **id_rsa** 개인 키 파일 이름을 있으므로 하나 있는 것이 좋습니다. hello 디렉터리 `~/.ssh/` hello SSH 키 쌍과 hello SSH 구성 파일 기본 위치입니다.  전체 경로 지정 되지 않은 경우 `ssh-keygen` hello 현재 작업 디렉터리의 hello 키 만들 되 면 기본 하지 hello `~/.ssh`합니다.

Hello 목록이 `~/.ssh` 디렉터리입니다.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

키 암호:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`"암호입니다."로 tooa 사용 되는 암호 tooencrypt hello 개인 키를 참조  *강력한* tooadd 암호 tooyour 키 쌍을 권장 합니다. 암호 보호 hello 개인 키 없이 hello 키 파일에 있는 모든 사용자에서 사용할 수 toolog hello 해당 공개 키를 가진 tooany 서버입니다. Tooauthenticate를 사용 되는 시간 toochange hello 키 제공에 수 toogain 액세스 tooyour 개인 키 파일을 사용자가 경우에 더 나은 보호를 제공 암호를 추가 하면 됩니다.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Ssh-에이전트 toostore 개인 키 암호를 사용 하 여

사용자의 개인 키를 입력 하는 tooavoid 파일 암호 모든 SSH 로그인 사용 하면 `ssh-agent` toocache 개인 키 파일 암호입니다. Hello OSX 키 집합 호출할 때 안전 하 게 hello 개인 키 암호를 저장 하는 Mac을 사용 하는 경우 `ssh-agent`합니다.

확인 하 고 사용 하 여 `ssh-agent` 및 `ssh-add` tooinform hello hello 키 파일에 대 한 SSH 시스템을 hello 암호 toobe 대화형으로 사용 하지 않아도 됩니다.

```bash
eval "$(ssh-agent -s)"
```

이제 너무 hello 개인 키를 추가할`ssh-agent` hello 명령을 사용 하 여 `ssh-add`합니다.

```bash
ssh-add ~/.ssh/id_rsa
```

hello 개인 키 암호에 따라 저장 `ssh-agent`합니다.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>사용 하 여 `ssh-copy-id` tooinstall hello에 대 한 새 키
VM을 이미 만든 경우 다음 명령을, hello VM 사용자 이름 및 hello 서버 주소를 원하는 값으로 교체 hello로 hello 새 SSH 공개 키 tooyour Linux VM을 설치할 수 있습니다.

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>SSH 구성 파일 만들기 및 구성

모범 사례 toocreate 이며 구성는 `~/.ssh/config` 로그인 할 경우 구성 파일 toospeed 및 SSH 클라이언트 동작을 최적화 하기 위한 합니다.

다음 예제는 hello 표준 구성을 보여 줍니다.

### <a name="create-hello-file"></a>Hello 파일 만들기

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Hello 파일 tooadd hello 새 SSH 구성을 편집 합니다.

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>예제 `~/.ssh/config` 파일:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

SSH 구성 하면 있습니다 섹션에 대 한 각 서버 tooenable 각 toohave 자체 전용된 키 쌍이 됩니다. 기본 설정 hello (`Host *`) hello 특정 호스트에서 위쪽 hello 구성 파일에서 일치 하지 않는 모든 호스트 됩니다.

### <a name="config-file-explained"></a>설명된 구성 파일

`Host`= 터미널 hello에 호출 되는 hello 호스트의 hello 이름입니다.  `ssh fedora22`지시 `SSH` 레이블이 지정 된 hello settings 블록에 toouse hello 값 `Host fedora22` 참고: 호스트 사용량에 대 한 논리는 모든 서버 hello 실제 호스트를 나타내지 않는 레이블과 될 수 있습니다.

`Hostname 102.160.203.241`= hello IP 주소 또는 액세스 하 고 hello 서버에 대 한 DNS 이름입니다.

`User ahmet`toohello 서버에 로그인 할 때 hello 원격 사용자 계정 toouse를 = 합니다.

`PubKeyAuthentication yes`= toouse SSH 키 toolog에서 원하는 SSH에 알려 줍니다.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`hello SSH 개인 키와 인증을 위해 해당 공개 키 toouse =입니다.

## <a name="ssh-into-linux-without-a-password"></a>암호 없이 Linux에 SSH

SSH 키 쌍과 구성 된 SSH config 파일을가지고 빠르고 안전 하 게 tooyour Linux VM의에서 수 toolog 됩니다. 처음에 로그인 할 때 SSH 키 hello 명령 프롬프트를 사용 하 여 tooa 서버 하면 해당 키 파일에 대 한 hello 암호에 대 한 번호입니다.

```bash
ssh fedora22
```

### <a name="command-explained"></a>설명된 명령

때 `ssh fedora22` 실행 SSH 먼저 찾아서 hello에서 모든 설정을 로드 `Host fedora22` 블록 및 모든 hello 남은 hello 마지막 블록에서에서 설정을 로드 `Host *`합니다.

## <a name="next-steps"></a>다음 단계

다음을 toocreate Azure Linux Vm의 경우 사용 하는 hello 새 SSH 공개 키.  Hello 로그인으로 SSH 공개 키를 사용 하 여 만든 azure Vm은 보안 hello 기본 로그인 방법, 암호를 사용 하 여 만든 Vm 보다 더 합니다.  SSH 키를 사용하여 만든 Azure VM은 기본적으로 비활성화된 암호를 사용하여 구성되고 강제 무차별 암호 추측 시도를 방지합니다. SSH 키 쌍 만들기에 도움이 필요 하거나 추가 인증서가 필요한 경우 다음을 참조 하세요 hello 클래식 포털에 사용할 구조의 등 [단계 toocreate SSH 키 쌍과 인증서 세부](create-ssh-keys-detailed.md)합니다.

* [Azure 템플릿을 사용하여 보안 Linux VM 만들기](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure 포털을 사용 하 여 보안 Linux VM 만들기](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure CLI를 사용 하 여 보안 Linux VM 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
