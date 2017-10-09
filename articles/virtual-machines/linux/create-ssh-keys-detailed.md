---
title: "Azure에서 Linux Vm에 대 한 aaaDetailed 단계 toocreate는 SSH 키 쌍 | Microsoft Docs"
description: "Azure에서 Linux Vm에 대 한 다른 사용 사례에 대 한 특정 인증서와 함께 추가 단계 toocreate SSH 공용 및 개인 키 쌍에 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>SSH 키 쌍 toocreate 및 Azure에서 Linux VM에 대 한 추가 인증서를 통해 자세한 워크
SSH 키 쌍에서 암호 toolog hello 필요성을 제거 기본 인증을 위해 SSH 키 toousing Azure에서 가상 컴퓨터를 만들 수 있습니다. 암호 해독할 수 있으며 toorelentless 무단 시도 tooguess Vm에 암호를 엽니다. Hello Azure CLI 또는 리소스 관리자 템플릿을 사용 하 여 만든 Vm SSH에 대 한 로그인 암호를 사용 하지 않도록 설정의 게시물 배포 구성 단계를 제거 하는 hello 배포의 일부로 SSH 공개 키를 포함할 수 있습니다. 이 문서에서는 Linux 가상 컴퓨터에서 사용 등을 위한 자세한 단계 및 인증서 생성에 대한 추가 예제를 제공합니다. Tooquickly 하려는 경우 만들기 및 SSH 키 쌍을 사용 하 여, 참조 [toocreate SSH 공용 및 개인 키 쌍 Azure에서 Linux Vm에 대 한 연결 하는 방법을](mac-create-ssh-keys.md)합니다.

## <a name="understanding-ssh-keys"></a>SSH 키 이해

SSH 공개 및 개인 키를 사용 하 여 hello tooyour Linux 서버에 가장 쉬운 방법은 toolog입니다. [공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) 무차별 암호 강제 훨씬 더 쉽게 수 있는 암호 보다는 훨씬 더 안전한 방식으로 toolog tooyour Linux에서에서 또는 Azure에서 VM BSD를 제공 합니다.

다른 사람과 공개 키를 공유할 수 있지만 사용자(또는 로컬 보안 인프라)만이 개인 키를 소유합니다.  hello SSH 개인 키가 있어야 합니다는 [매우 안전한 방법이 암호](https://www.xkcd.com/936/) (소스:[xkcd.com](https://xkcd.com)) toosafeguard 것입니다.  이 암호는 정당한 tooaccess hello 개인 SSH 키 파일 및 **않습니다** hello 사용자 계정 암호입니다.  Hello 개인 키가 hello 암호 toodecrypt 무용지물이 있도록 128 비트 AES를 사용 하 여 hello 개인 키 암호화 암호 tooyour SSH 키를 추가 하면 것입니다.  공격자가 개인 키로 훔쳐 경우 및 키 암호 없는, 즉 개인 수 toouse 예상 되는 toolog hello 해당 공개 키를 가진 tooany 서버에서 키입니다.  개인 키가 암호로 보호된 경우 공격자가 사용할 수 없어 Azure에서 인프라에 대해 보안 계층을 추가로 제공합니다.

이 문서는 SSH 프로토콜 버전을 2 RSA 공개 및 개인 키 쌍 (또한 참조 tooas "ssh rsa" 키), Azure 리소스 관리자와 배포용으로 권장 되는 만듭니다. *ssh rsa* hello에 키가 필요 [포털](https://portal.azure.com) 기본 및 리소스 관리자 배포에 대 한 합니다.

## <a name="ssh-keys-use-and-benefits"></a>SSH 키 용도 및 이점

Azure는 적어도 2048 비트를 필요한 SSH 프로토콜 버전 2 RSA 형식 공개 및 개인 키입니다. hello 공개 키 파일에 hello `.pub` 컨테이너 형식입니다. toocreate hello 키를 사용 하 여 `ssh-keygen`, 일련의 질문을 요청 하 고 다음 개인 키와 일치 하는 공개 키를 기록 합니다. Azure 복사본 공개 키 toohello hello Azure VM이 만들어지면 `~/.ssh/authorized_keys` hello VM의 폴더입니다. SSH 키에 `~/.ssh/authorized_keys` 사용 되는 toochallenge hello 클라이언트 toomatch hello 해당 개인 키에 대 한 SSH 로그인 연결 됩니다.  Azure Linux VM이 만들어지면 인증을 위해 SSH 키를 사용 하 여 Azure hello SSHD 구성 서버 toonot 로그인 암호, SSH 키만 허용 합니다.  따라서 Azure Linux Vm의 경우 SSH 키를 만들 수 있습니다 hello VM 배포를 보호 하 고 직접 hello에서 암호를 사용 하지 않도록 설정의 hello 일반적인 배포 후 구성 단계를 저장할 **sshd_config** 파일입니다.

## <a name="using-ssh-keygen"></a>ssh-keygen 사용

이 명령은 SSH 키 쌍 (암호화 된) 2048 비트 RSA를 사용 하 여 보안 암호를 만들고이 주석 처리 tooeasily 식별 합니다.  

SSH 키가 hello에 보관 하는 기본적으로 `~/.ssh` 디렉터리입니다.  하지 않은 경우는 `~/.ssh` 디렉터리, hello `ssh-keygen` 명령 그 사용자를 위해 만드는 hello로 올바른 사용 권한이 있습니다.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*설명된 명령*

`ssh-keygen`= hello 사용 프로그램 toocreate hello 키

`-t rsa`hello RSA 형식인 [wikipedia] 키 toocreate 유형의 =[끝에 괄호를](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` hello 키의 비트

`-C "azureuser@myserver"`= 식별 하는 추가 된 toohello hello 공개 키 파일 tooeasily 끝을 설명 합니다.  일반적으로 전자 메일 hello 주석으로 사용 되지만 인프라에 대 한 가장 잘 작동 무엇이 든 사용할 수 있습니다.

## <a name="classic-deploy-using-asm"></a>`asm`을 사용하여 클래식 배포

Hello 클래식 배포 모델을 사용 하는 경우 (`asm` hello CLI에에서는 모드), SSH RSA 공개 키를 사용할 수 있습니다 또는 RFC4716 서식이 지정 된 pem 컨테이너의 키입니다.  hello SSH RSA 공개 키가 사용 하 여이 문서 앞부분에서 만들어진 `ssh-keygen`합니다.

RFC4716 toocreate 기존 SSH 공개 키에서 키 서식이 지정 됩니다.

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>ssh-keygen 예제

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
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

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

이 문서에 대 한 hello 키 쌍 이름입니다.  명명 된 키 쌍을 필요 **id_rsa** hello 기본 템플릿이 고 일부 도구는 hello 예상 **id_rsa** 개인 키 파일 이름을 있으므로 하나 있는 것이 좋습니다. hello 디렉터리 `~/.ssh/` hello SSH 키 쌍과 hello SSH 구성 파일 기본 위치입니다.  전체 경로 지정 되지 않은 경우 `ssh-keygen` hello 현재 작업 디렉터리 hello 기본값이 아닌 hello 키를 만들고 `~/.ssh`합니다.

Hello 목록이 `~/.ssh` 디렉터리입니다.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

키 암호:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`"암호입니다."로 tooa 암호 hello 개인 키 파일에 대 한 참조  *강력한* tooadd 암호 tooyour 개인 키를 권장 합니다. 암호 보호 hello 키 파일 없이 hello 파일에 있는 모든 사용자를 사용할 수 toolog hello 해당 공개 키를 가진 tooany 서버. 암호 (암호)를 추가 더 나은 보호 수 toogain 액세스 tooyour 개인 키 파일은 다른 사용자는 경우를 대비 하 고, 부여 받은 시간 toochange hello 키 사용 tooauthenticate 있습니다.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Ssh-에이전트 toostore 개인 키 암호를 사용 하 여

tooavoid 모든 SSH 로그인 사용 하 여 개인 키 파일 암호를 입력 하는 데 `ssh-agent` toocache 개인 키 파일 암호입니다. Hello OSX 키 집합 호출할 때 안전 하 게 hello 개인 키 암호를 저장 하는 Mac을 사용 하는 경우 `ssh-agent`합니다.

확인 및 ssh-에이전트를 사용 하 고 ssh-추가 hello 키 파일에 대 한 tooinform hello SSH 시스템 되도록 hello 암호 toobe 대화형으로 사용 하지 않아도 됩니다.

```bash
eval "$(ssh-agent -s)"
```

이제 너무 hello 개인 키를 추가할`ssh-agent` hello 명령을 사용 하 여 `ssh-add`합니다.

```bash
ssh-add ~/.ssh/id_rsa
```

hello 개인 키 암호에 따라 저장 `ssh-agent`합니다.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>사용 하 여 `ssh-copy-id` toocopy hello 키 tooan 기존 VM
VM을 이미 만든 경우에 hello 새 SSH 공개 키 tooyour Linux VM을 설치할 수 있습니다 사용:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>SSH 구성 파일 만들기 및 구성

권장된 모범 사례 toocreate 이며 구성는 `~/.ssh/config` 로그인 할 경우 구성 파일 toospeed 및 SSH 클라이언트 동작을 최적화 하기 위한 합니다.

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

다음을 toocreate Azure Linux Vm의 경우 사용 하는 hello 새 SSH 공개 키.  Hello 로그인으로 SSH 공개 키를 사용 하 여 만든 azure Vm은 보안 hello 기본 로그인 방법, 암호를 사용 하 여 만든 Vm 보다 더 합니다.  SSH 키를 사용하여 만든 Azure VM은 기본적으로 비활성화된 암호를 사용하여 구성되고 강제 무차별 암호 추측 시도를 방지합니다.

* [Azure 템플릿을 사용하여 보안 Linux VM 만들기](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure 포털을 사용 하 여 보안 Linux VM 만들기](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure CLI를 사용 하 여 보안 Linux VM 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
