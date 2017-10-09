---
title: "SSH 암호 SSHD를 구성 하 여 Linux VM에 aaaDisable | Microsoft Docs"
description: "SSH에 암호 로그인을 사용하지 않도록 설정하여 Azure에서 Linux VM을 보호합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>SSHD를 구성하여 Linux VM에 SSH 암호 사용 안 함
이 문서는 방법에 중점을 둡니다 toolock Linux VM의 로그인 보안을 hello 다운 합니다.  SSH 포트 22 hello 열릴으로 toohello 세계 봇 toologin 암호를 추측 하 여 시도 시작 합니다.  이 문서에서는 SSH를 통해 암호 로그인을 사용하지 않도록 설정합니다.  Hello 기능을 완전히 제거 하 여 toouse 암호 보호 hello Linux VM에서이 유형의 무차별 암호 대입 공격입니다.  hello 추가 보너스 tooonly 허용 Linux SSHD 구성가 SSH 공용 및 개인 키를 통해 로그인에는 지금까지 가장 안전한 방법은 toologin tooLinux hello 합니다.  가능한 조합을 hello tooguess hello 개인 키는 빚 이며 따라서 봇도 tootry toobrute force SSH 키를 신경에서 지원 되지 필요 합니다.

## <a name="goals"></a>목표
* SSHD toodisallow를 구성 합니다.
  * 암호 로그인
  * 루트 사용자 로그인
  * 시도-응답 인증
* SSHD tooallow를 구성 합니다.
  * SSH 키 로그인만 해당
* 로그인 중에 SSHD 다시 시작
* 테스트 hello 새 SSHD 구성

## <a name="introduction"></a>소개
[정의된 SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD는 hello hello Linux VM에서 실행 되는 SSH 서버입니다.  SSH는 MacBook 또는 Linux 워크스테이션의 셸에서 실행되는 클라이언트입니다.  SSH는 hello toosecure 사용 되는 프로토콜과 워크스테이션 및 hello Linux VM 간의 hello 통신을 암호화 이기도 합니다.

이 문서 것이 매우 중요 한 tookeep 하나의 로그인 tooyour 전체 hello에 대 한 열기 Linux VM을 안내 합니다.  이러한 이유로 열립니다 두 터미널 및 SSH toohello Linux VM에서 둘 모두 합니다.  Hello 첫 번째 터미널 toomake hello 변경 tooSSHDs 구성 파일을 사용 하 고 hello SSHD 서비스를 다시 시작 합니다.  Hello 두 번째 터미널 tootest hello 서비스 다시 시작 되 면 변경 하는 것을 사용 합니다.  SSH 암호를 해제 하는 것 이므로 엄격 하 게 SSH 키, SSH 키에 잘못 된 하 고 hello 연결 toohello VM을 닫으면에 의존 hello VM 영구적으로 됩니다 잠기고 아무도 수 toologin tooit 삭제 하 고 다시 toobe 요구 됩니다.

## <a name="prerequisites"></a>필수 조건
* [Azure의 Linux VM용 Linux 및 Mac에서 SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Azure 계정
  * [무료 평가판 등록](https://azure.microsoft.com/pricing/free-trial/)
  * [Azure 포털](http://portal.azure.com)
* Azure에서 실행 중인 Linux VM
* `~/.ssh/`에서 SSH 공용 및 개인 키 쌍
* SSH 공개 키를 `~/.ssh/authorized_keys` hello Linux VM에
* Hello VM에 대 한 Sudo 권한
* 열린 포트 22

## <a name="quick-commands"></a>빠른 명령
*숙련 된 Linux 관리자에 게 hello TLDR 버전 원하는 여기에서 시작 합니다.  Hello를가 하는 다른 모든 사용자에 대 한 자세한 설명과 워크를 통해이 섹션을 건너뛰십시오.*

```bash
sudo vim /etc/ssh/sshd_config
```

다음과 같이 hello 구성 파일을 편집 합니다.

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Hello SSHD 서비스를 다시 시작 합니다. Debian 기반 배포판에서:

```bash
sudo service ssh restart
```

Red Hat 기반 배포판에서:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>자세한 연습
로그인 toohello Linux VM에 터미널 1 (T1).  로그인 toohello Linux VM에 터미널 2 (T2).

T 2에서 tooedit hello SSHD 구성 파일을 하겠습니다.  

```bash
sudo vim /etc/ssh/sshd_config
```

여기에서 방금 hello 설정을 toodisable 암호를 편집 하 고 SSH 키 로그인을 활성화 합니다.  연구 및 toomake Linux 및 필요에 따라 보안 SSH를 변경 해야이 파일의 여러 설정이 있습니다.

#### <a name="disable-password-logins"></a>암호 로그인 사용 안 함

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>공개 키 인증 사용

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>루트 로그인 사용 안 함

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>시도-응답 인증 사용 안 함
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>SSHD 다시 시작
Hello T1 셸에서 있는지 계속 로그인을 확인 합니다.  암호를 이제 사용하지 않기 때문에 SSH 키가 올바르지 않은 경우 VM을 잠그지 않는 것이 중요합니다.   모든 설정을 사용할 수 있습니다 T1 toofix sshd_config 있습니다 여전히 기록 되 고 SSH 상태로 유지 합니다 hello 연결 hello SSHD 서비스 중 Linux VM에 올바르지 않은 경우 다시 시작 합니다.

T2에서 다음을 실행합니다.

##### <a name="on-hello-debian-family"></a>Hello Debian 제품군에서
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>Hello RedHat 제품군에서
```bash
sudo service sshd restart
```

암호는 이제 무차별 암호 로그인 시도에서 VM을 보호하는 기능을 사용하지 않습니다.  SSH 키만 허용 수 toologin 빠르고 훨씬 더 안전 해야 합니다.

