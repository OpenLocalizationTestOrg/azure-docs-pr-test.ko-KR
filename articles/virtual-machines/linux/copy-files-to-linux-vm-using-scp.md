---
title: "aaaMove SCP 통해 Azure Linux Vm에서 tooand 파일 | Microsoft Docs"
description: "SCP 및 SSH 키 쌍을 사용 하 여 Azure에서 Linux VM에서는 파일 tooand를 안전 하 게 이동 합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>SCP를 사용 하 여 Linux VM에서는 tooand 파일 이동

이 문서에서는 Azure Linux VM tooyour 워크스테이션 아래로 Secure 복사본 (SCP)를 사용 하 여 또는 tooan Azure Linux VM을 워크스테이션에서 toomove 파일 하는 방법입니다. 워크스테이션과 Linux VM 간에 신속하고 안전하게 파일을 이동하는 것은 Azure 인프라 관리의 중요한 부분입니다. 

이 문서의 경우 [SSH 공개 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 Azure에 Linux VM이 배포되어 있어야 합니다. 또한 로컬 컴퓨터에 SCP 클라이언트가 필요합니다. SSH 기반 이며 일부 Windows 셸 및 대부분의 Linux 및 Mac 컴퓨터의 기본 Bash 셸의 hello에 포함 합니다.

## <a name="quick-commands"></a>빠른 명령

Linux VM toohello 파일에 복사

```bash
scp file azureuser@azurehost:directory/targetfile
```

Hello Linux VM에서에서 파일을 한 단계 아래로 복사 합니다.

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>자세한 연습

예를 들어 म tooa Linux VM을 Azure 구성 파일로 이동 하 고 로그 파일 디렉터리를 끌어오고 둘 모두 SCP 및 SSH 키를 사용 합니다.   

## <a name="ssh-key-pair-authentication"></a>SSH 키 쌍 인증

SCP은 hello 전송 계층에 대 한 SSH를 사용합니다. SSH 핸들 hello hello 대상 호스트에서 인증 및 SSH와 기본적으로 제공 된 암호화 된 터널의 hello 파일을 이동 합니다. SSH 인증에는 사용자 이름 및 암호를 사용할 수 있습니다. 그러나 SSH 공개 및 개인 키 인증이 보안 모범 사례로 권장됩니다. Hello 연결 SSH가 인증 되 면 SCP 시작 hello 파일을 복사 합니다. 올바르게 구성 된를 사용 하 여 `~/.ssh/config` 및 서버 이름 (또는 IP 주소) 사용 하 여 SSH 공개 및 개인 키, SCP hello 연결을 설정할 수 있습니다. SSH 키 하나만 경우 SCP에서에서 찾습니다 hello `~/.ssh/` 디렉터리를 사용 하 여 toohello VM에서에서 기본 toolog으로 합니다.

`~/.ssh/config`와 SSH 공개 및 개인 키 구성에 대한 자세한 내용은 [SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

## <a name="scp-a-file-tooa-linux-vm"></a>SCP 파일 tooa Linux VM

Hello 첫 번째 예제에서는 tooa toodeploy 사용 되는 자동화 된 Linux VM을는 Azure 구성 파일에 복사 했습니다. 이 파일에는 비밀이 포함된 Azure API 자격 증명이 있으므로 보안이 중요합니다. SSH에서 제공 하는 hello 암호화 터널 hello 파일의 hello 내용을 보호 합니다.

다음 명령은 복사본 hello 로컬 hello *.azure/config* tooan FQDN 사용 하 여 Azure VM 파일 *myserver.eastus.cloudapp.azure.com*. hello Azure VM에서 관리자 사용자 이름이 hello *azureuser* . hello 파일은 대상된 toohello */azureuser/home/* 디렉터리입니다. 이 명령에서 고유한 값을 대체합니다.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>디렉터리를 Linux VM에서 SCP

예를 들어 tooyour 워크스테이션 아래로 hello Linux VM에서에서 로그 파일의 디렉터리를 복사합니다. 로그 파일에는 중요한 데이터 및 비밀 데이터가 있을 수도 있고 없을 수도 있습니다. 그러나 SCP를 사용 하면 hello 로그 파일의 내용을 hello 암호화 됩니다. 가장 쉬운 방법은 tooget hello tootransfer hello 파일 SCP를 사용 하는 유지 하면서도 보안 로그 디렉터리 및 파일 tooyour 워크스테이션 아래로 hello 합니다.

hello 다음 명령은 파일에에서 복사 hello */home/azureuser/로그/* hello Azure VM toohello 로컬 /tmp 디렉터리에 디렉터리:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

hello `-r` cli 플래그 hello 명령에 나열 된 hello 디렉터리의 hello 지점에서 SCP toorecursively 복사본 hello 파일 및 디렉터리에 지시 합니다.  또한 hello 명령줄 구문에 비슷한 tooa `cp` 명령을 복사 합니다.

## <a name="next-steps"></a>다음 단계

* [사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 환영](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
