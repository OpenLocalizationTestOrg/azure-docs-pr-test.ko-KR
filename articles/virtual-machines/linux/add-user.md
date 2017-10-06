---
title: "사용자 tooa Azure에서 Linux VM aaaAdd | Microsoft Docs"
description: "Azure에서 사용자 tooa Linux VM을 추가 합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>사용자 tooan Azure VM 추가
모든 새로운 Linux VM에 있는 hello 첫 번째 작업의 하나 toocreate 새 사용자입니다.  이 문서에서는 SSH 공개 키를 추가, sudo 사용자 계정, hello 암호를 설정 하는, 만드는 과정을 설명 하 고 마지막으로 사용 하 여 `visudo` 암호 없이 tooallow sudo.

필수 구성 요소는: [Azure 계정이 있으세요](https://azure.microsoft.com/pricing/free-trial/), [SSH 공개 및 개인 키](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Azure 리소스 그룹 및 hello Azure CLI를 설치 하 고 사용 하 여 tooAzure 리소스 관리자 모드로 전환한 `azure config mode arm`합니다.

## <a name="quick-commands"></a>빠른 명령
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>자세한 연습
### <a name="introduction"></a>소개
새 서버와 hello 첫 번째 및 가장 일반적인 작업 중 하나 tooadd 사용자 계정입니다.  루트 로그인을 비활성화 해야 및 Linux 서버에 sudo hello 루트 계정 자체를 사용할 수 해야 합니다.  사용자 루트 에스컬레이션 적절 한 방법은 tooadminister hello 하 고 Linux를 사용 하 여 sudo를 사용 하 여 권한 부여입니다.

Hello 명령을 사용 하 여 `useradd` 사용자 계정 toohello Linux VM을 추가 하는 것입니다.  `useradd`를 실행하면 `/etc/passwd`, `/etc/shadow`, `/etc/group` 및 `/etc/gshadow`가 수정됩니다.  명령줄 플래그 toohello 추가 하 고 `useradd` 명령 tooalso linux hello 새 사용자 toohello sudo 적절 한 그룹을 추가 합니다.  가 `useradd` 에 항목을 만드는 `/etc/passwd` 부여 하지 않습니다 hello 새 사용자 계정 암호입니다.  단순 hello를 사용 하 여 hello 새 사용자에 대 한 초기 암호 생성 `passwd` 명령입니다.  hello 마지막 단계 toomodify hello sudo 규칙 tooallow sudo 권한이 있는 사용자 tooexecute 명령을 사용 하는 모든 명령에 대 한 암호 tooenter 필요 없이입니다.  해당 사용자 계정의 했다고 간주 하는 hello 개인 키를 사용 하 여 로그인 믿지 못할 자 으로부터 안전한 및 암호 없이 tooallow sudo 액세스 하려고 합니다.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>단일 sudo 사용자 tooan Azure VM을 추가합니다.
SSH 키를 사용 하 여 Azure VM toohello에 로그인 합니다.  SSH 공개 키 액세스를 설정하지 않은 경우 먼저 [Azure에서 공개 키 인증 사용](http://link.to/article)문서를 완료합니다.  

hello `useradd` 명령을 완료 작업을 수행 하는 hello:

* 새 사용자 계정 만들기
* hello로 새 사용자 그룹을 만들 같은 이름
* 빈 항목을 너무 추가`/etc/passwd`
* 빈 항목을 너무 추가`/etc/gpasswd`

hello `-G` 명령줄 플래그 hello 새 사용자 계정 toohello 적절 한 Linux 그룹 추가 hello 새 사용자 계정의 루트 에스컬레이션 권한을 제공 합니다.

#### <a name="add-hello-user"></a>Hello 사용자 추가
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>암호 설정
hello `useradd` 명령은 hello 사용자를 만들고 추가 하는 항목 tooboth `/etc/passwd` 및 `/etc/gpasswd` 하지만 실제로 hello 암호를 설정 하지 않습니다.  hello 암호는 추가 hello를 사용 하 여 toohello 항목 `passwd` 명령입니다.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

이제 했으므로 sudo 권한이 있는 사용자 hello 서버에 있습니다.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>SSH 공개 키 toohello 새 사용자 계정 추가
Hello를 사용 하 여 컴퓨터에서 `ssh-copy-id` hello 새 암호로 명령입니다.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>암호 없이 visudo tooallow sudo 사용 사용 하 여
사용 하 여 `visudo` tooedit hello `/etc/sudoers` 몇 가지 중요 한이 파일을 올바르게 수정에 대 한 보호 계층을 추가 하는 파일입니다.  실행 시 `visudo`, hello `/etc/sudoers` 파일이 잠긴된 tooensure 적극적으로 편집 중인 동안 다른 사용자 변경을 수행할 수 있습니다.  hello `/etc/sudoers` 파일에서 실수에 대 한 확인란도 선택 `visudo` toosave 시도 또는 종료 되므로 끊어진된 sudoers 파일을 저장할 수 없습니다.

Sudo 액세스에 대 한 hello 올바른 기본 그룹에 사용자가 이미 보유 합니다.  이제 하겠습니다 tooenable 암호가 없는 그룹 toouse sudo 해당 합니다.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>확인 hello 사용자, ssh 키 및 sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
