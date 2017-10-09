---
title: "Azure에서 aaaIntroduction tooFreeBSD | Microsoft Docs"
description: "Azure에서 FreeBSD 가상 컴퓨터를 사용하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Azure에서 tooFreeBSD 소개
이 항목에서는 Azure에서 FreeBSD 가상 컴퓨터를 실행하는 방법의 개요를 제공합니다.

## <a name="overview"></a>개요
Microsoft Azure에 대 한 FreeBSD toopower 최신 서버, 데스크톱 및 포함 된 플랫폼을 사용 하는 고급 컴퓨터 운영 체제입니다.

Microsoft Corporation은 FreeBSD의 이미지에서 사용할 수 있도록 Azure hello로 [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 미리 구성 합니다. 현재 hello 다음 FreeBSD 버전에서 제공 하는 이미지와 Microsoft:

- FreeBSD 10.3 릴리스
- FreeBSD 11.0 릴리스

hello 에이전트가 hello FreeBSD VM 간의 통신을 담당 하 고 프로 비전 하는 등의 작업에 대 한 Azure 패브릭이 hello 처음 사용할 (사용자 이름, 암호 또는 SSH 키, 호스트 이름, 등) 및 선택적 VM 확장에 사용할 수 있도록 기능에 대해 VM hello 합니다.

FreeBSD의 이후 버전의 경우와 hello 전략은 현재 toostay 고 hello 최신 릴리스에 사용할 수 있도록 hello FreeBSD 릴리스 엔지니어링 팀에서 게시 한 후에 곧 합니다.

## <a name="deploying-a-freebsd-virtual-machine"></a>FreeBSD 가상 컴퓨터 배포
FreeBSD 가상 컴퓨터를 배포할은 hello Azure 포털에서에서 Azure 마켓플레이스 hello에서 이미지를 사용 하 여 간단한 프로세스입니다.

- [Azure 마켓플레이스 hello에 FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [Azure 마켓플레이스 hello에 FreeBSD 11.0](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>FreeBSD에서 Azure CLI 2.0을 통해 FreeBSD VM 만들기
Tooinstall 먼저 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) FreeBSD 컴퓨터에서 다음 명령을 있지만 합니다.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Bash FreeBSD 컴퓨터에 설치 되지 않은 경우 다음 hello 설치 하기 전에 명령을 실행 합니다. 

```bash
sudo pkg install bash
```

Python FreeBSD 컴퓨터에 설치 되지 않은 경우 다음 hello 설치 하기 전에 명령을 실행 합니다. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Hello 설치 하는 동안 요청 `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`합니다. 업그레이드 하도록 `y` 입력 `/etc/rc.conf` 으로 `a path tooan rc file tooupdate`, hello 문제를 충족할 수 `ERROR: [Errno 13] Permission denied`합니다. tooresolve이이 문제를 hello 쓰기 오른쪽 toocurrent 사용자 hello 파일에 대해 부여 하면 `etc/rc.conf`합니다.

이제 Azure에 로그인한 후 FreeBSD VM을 만들 수 있습니다. 다음 예에서는 toocreate FreeBSD 11.0 VM은입니다. Hello 매개 변수를 추가할 수도 있습니다 `--public-ip-address-dns-name` 새로 생성된 된 공용 IP에 대 한 전역적으로 고유 DNS 이름으로 합니다. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

그런 다음 배포 위의 hello 출력으로 인쇄 하는 hello ip 주소를 통해 tooyour FreeBSD VM에에서 로그인 할 수 있습니다. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>FreeBSD에 대한 VM 확장
FreeBSD에서 지원되는 VM 확장은 다음과 같습니다.

### <a name="vmaccess"></a>VMAccess
hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) 확장 수 있습니다.

* Hello 원래 sudo 사용자의 hello 암호 다시 설정 합니다.
* 새 사용자를 sudo hello 암호를 지정 합니다.
* 지정 된 hello 키로 hello 공개 호스트 키를 설정 합니다.
* VM hello 호스트 키를 제공 하지 않으면 프로 비전 중에 제공 된 hello 공개 호스트 키를 다시 설정 합니다.
* Hello SSH 포트 (22)를 열고 reset_ssh tootrue 설정 된 경우 hello sshd_config를 복원 합니다.
* Hello 기존 사용자를 제거 합니다.
* 디스크를 확인합니다.
* 추가된 디스크를 복구합니다.

### <a name="customscript"></a>CustomScript
hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) 확장 수 있습니다.

* 제공 된 경우 Azure 저장소 서비스 또는 외부 공용 저장소 (예를 들어 GitHub)에서 사용자 지정 하는 hello 스크립트를 다운로드 합니다.
* Hello 항목 지점 스크립트를 실행 합니다.
* 인라인 명령을 지원합니다.
* 셸 및 Python 스크립트에서 Windows 스타일 줄 바꿈 문자를 자동으로 변환합니다.
* 셸 및 Python 스크립트의 BOM을 자동으로 제거합니다.
* CommandToExecute의 중요 데이터를 보호합니다.

> [!NOTE]
> FreeBSD VM은 현재 CustomScript 버전 1.x만 지원합니다.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>인증: 사용자 이름, 암호 및 SSH 키
Hello Azure 포털을 사용 하 여 FreeBSD 가상 컴퓨터를 만들 때 사용자 이름, 암호 또는 SSH 공개 키를 제공 해야 합니다.
Azure에서 FreeBSD 가상 컴퓨터를 배포 하기 위한 사용자 이름 해야 시스템 계정 이름과 일치 하지 (UID < 100) hello 가상 컴퓨터 (예: "root")에 이미 존재 합니다.
현재 hello RSA SSH 키만 지원 됩니다. 여러 줄 SSH 키는 `---- BEGIN SSH2 PUBLIC KEY ----`로 시작하고 `---- END SSH2 PUBLIC KEY ----`로 끝나야 합니다.

## <a name="obtaining-superuser-privileges"></a>Superuser 권한 얻기
Azure에서 가상 컴퓨터 인스턴스에 배포 하는 동안 지정 된 hello 사용자 계정은 권한 있는 계정이입니다. hello sudo의 패키지에 설치 되어 hello FreeBSD 이미지를 게시 합니다.
이 사용자 계정을 통해 로그인 한 후에 hello 명령 구문을 사용 하 여 루트로 명령을 실행할 수 있습니다.

```
$ sudo <COMMAND>
```

선택적으로 `sudo -s`를 사용하여 루트 셸을 얻을 수 있습니다.

## <a name="known-issues"></a>알려진 문제
hello [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 버전 2.2.2에 [알려진된 문제가 있습니다.] (https://github.com/Azure/WALinuxAgent/pull/517) 되도록 hello 프로 비전 실패 Azure에 FreeBSD VM에 대 한 합니다. hello 수정 하 여 캡처 되었습니다 [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 2.2.3 버전 또는 이후 버전입니다. 

## <a name="next-steps"></a>다음 단계
* 너무 이동[Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD VM입니다.
* 사용자 고유의 FreeBSD tooAzure toobring을 원하는 경우 너무 참조[만들기 및 업로드 FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md)합니다.
