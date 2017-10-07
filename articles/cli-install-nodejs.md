---
title: aaaInstall hello Azure CLI 1.0 | Microsoft Docs
description: "Azure 서비스를 사용 하 여 Mac, Linux 및 Windows toostart에 대 한 hello Azure CLI 1.0 설치"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Hello Azure CLI 1.0 설치
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> 이 항목에서는 많은 수의 리소스 관리자 배포 활동 뿐 아니라 tooinstall hello Azure CLI 1.0 nodeJs에서 빌드하고 지 원하는 모든 클래식 배포 API를 호출 하는 방법에 대해 설명 합니다. Hello를 사용 해야 [Azure CLI 2.0](/cli/azure/overview) 새롭거나 특정 CLI 배포 및 관리 합니다.

Hello Azure 명령줄 인터페이스 (Azure CLI 1.0) toouse 만들고 Microsoft Azure의에서 리소스를 관리 하기 위한 오픈 소스 셸 기반 명령 집합을 신속 하 게 설치 합니다. 몇 가지 옵션 tooinstall 이러한 플랫폼 간 도구에 있는 컴퓨터:

* **npm 패키지** 실행-Linux 배포 또는 운영 체제에서 (JavaScript 용 hello 패키지 관리자) npm tooinstall hello 최신 Azure CLI 1.0 패키지 합니다. node.js 및 npm이 컴퓨터에 필요합니다.
* **설치 관리자** - 설치 관리자를 다운로드하여 Mac 또는 Windows에서 손쉽게 설치합니다.
* **Docker 컨테이너** -시작 hello를 사용 하 여 최신 CLI 실행 방식 Docker 컨테이너에 있습니다. Docker 호스트가 컴퓨터에 필요합니다.

많은 옵션과 배경 hello 프로젝트 저장소에서 참조 [GitHub](https://github.com/azure/azure-xplat-cli)합니다.

Hello Azure CLI 1.0 설치 되 면 [Azure 구독과 연결](xplat-cli-connect.md) 및 실행된 hello **azure** 프로그램 명령줄 인터페이스 (예: Bash, 터미널, 명령 프롬프트 및 등)에서 명령으로 toowork Azure 리소스입니다.

## <a name="option-1-install-an-npm-package"></a>옵션 1: npm 패키지 설치
tooinstall hello CLI npm 패키지를 다운로드 하 고 hello 설치 되어 있는지 확인 [최신 Node.js 및 npm](https://nodejs.org/en/download/package-manager/)합니다. 그런 다음 실행 **npm 설치** tooinstall hello azure cli 패키지:

```bash
npm install -g azure-cli
```

Linux 배포판의 toouse 할 수 있습니다 **sudo** 실행 toosuccessfully hello **npm** 명령, 다음과 같습니다.

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> 를 tooinstall 필요 하거나 Node.js 및 npm Linux 배포 또는 운영 체제를 업데이트 하는 경우에 hello 가장 최근의 Node.js LTS 버전 (4.x) 설치 하는 것이 좋습니다. 이전 버전을 사용하는 경우 설치 오류가 발생할 수 있습니다.

원하는 경우 다운로드 최신 Linux hello [tar 파일] [ linux-installer] 로컬로 hello npm 패키지 합니다. 그런 다음 다음과 같이 hello 다운로드 한 npm 패키지를 설치 (Linux 배포판의 해야 toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>옵션 2: 설치 관리자 사용
Mac 또는 Windows 컴퓨터를 사용 하는 경우 hello CLI 설치 관리자가 다음 다운로드할 수 있습니다.

* [Mac OS X 설치 관리자][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> Windows에서 다운로드할 수도 있습니다 hello [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI 합니다. 이 설치 관리자에서는 옵션 tooinstall hello 추가 Azure SDK 및 명령줄 도구를 설치한 후 hello CLI 합니다.

## <a name="option-3-use-a-docker-container"></a>옵션 3: Docker 컨테이너 사용
로 컴퓨터를 설정한 경우는 [Docker](https://docs.docker.com/engine/understanding-docker/) 호스트를 실행할 수 있습니다 최신 Azure CLI 1.0 Docker 컨테이너에서 hello 합니다. 실행 hello 다음 명령을 (Linux 배포판의 해야 toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Azure CLI 1.0 명령 실행
Hello Azure CLI 1.0 설치 된 후 실행 hello **azure** 명령줄 사용자 인터페이스 (예: Bash, 터미널, 명령 프롬프트 및 등)에서 명령을 합니다. 예를 들어, toorun hello 도움말 명령 hello 다음을 입력 합니다.

```azurecli
azure help
```

> [!NOTE]
> 일부 Linux 배포판에 나타날 수 있습니다 유사한 오류가 너무`/usr/bin/env: ‘node’: No such file or directory`합니다. 이 오류는 최근에 Node.js를 /usr/bin/nodejs에 설치할 때 비롯되었습니다. toofix,이 명령을 실행 하 여 기호화 된 링크 너무/usr/bin/노드를 만듭니다.

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

hello Azure CLI 1.0를 설치한 다음 형식 hello toosee hello 버전:

```azurecli
azure --version
```

이제 준비가 되었습니다! 모든 tooaccess hello로 리소스, CLI 명령을 toowork [hello Azure CLI에서에서 tooyour Azure 구독 연결](xplat-cli-connect.md)합니다.

> [!NOTE]
> 먼저 Azure CLI를 사용 하는 경우 Microsoft toocollect 사용 정보 tooallow 설정할지 묻는 메시지가 표시 됩니다. 참여는 자발적입니다. 실행 하 여 언제 든 지 중지할 수 tooparticipate을 선택 하면 `azure telemetry --disable`합니다. 언제 든 지 참여 tooenable 실행 `azure telemetry --enable`합니다.

## <a name="update-hello-cli"></a>Hello CLI를 업데이트 합니다.
Microsoft은 업데이트 된 버전의 hello Azure CLI를 자주 공개합니다. 다시 설치 중인 운영 체제에 대 한 hello 설치 관리자를 사용 하 여 CLI hello 또는 hello 최신 Docker 컨테이너를 실행 합니다. Hello 다음을 입력 하 여 최신 Node.js 및 npm 설치를 hello 있는, 하는 경우 업데이트 또는 (Linux 배포판의 해야 toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>탭 완성 기능 사용
CLI 명령의 탭 완성 기능이 Mac 및 Linux에서 지원됩니다.

tooenable zsh에서 실행 합니다.

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable bash에서 실행 합니다.

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>다음 단계
* [Hello CLI tooyour Azure 구독에서에서 연결](xplat-cli-connect.md) toocreate 및 Azure 리소스를 관리 합니다.
* hello Azure CLI에 대해 자세히 toolearn 소스 코드를 다운로드, 문제를 보고 또는 toohello 프로젝트 참가, hello 방문 [Azure CLI hello에 대 한 GitHub 리포지토리](https://github.com/azure/azure-xplat-cli)합니다.
* Hello Azure CLI 또는 Azure를 사용 하는 방법에 대 한 질문이 있으면 방문 hello [의 Azure 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)합니다.


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
