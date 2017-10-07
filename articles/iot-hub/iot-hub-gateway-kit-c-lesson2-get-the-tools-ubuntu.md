---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 2: 도구 다운로드(Ubuntu) | Microsoft Docs"
description: "Ubuntu를 실행 하는 호스트 컴퓨터에 hello 도구와 hello 소프트웨어를 설치 하 고 IoT 허브를 만듭니다. 다음 hello IoT 허브에서 장치를 등록 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, IoT 클라우드 서비스, 사물 인터넷 소프트웨어, Azure CLI, Ubuntu에 Git 설치, gulp 실행, Node Js Ubuntu 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Hello 도구 (Ubuntu 16.04) 가져오기
> [!div class="op_single_selector"]
> * [Windows 7 이상](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>수행할 사항

- Git, Node.js, Gulp, Python을 설치합니다.
- Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다. 

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.
## <a name="what-you-will-learn"></a>알아볼 내용

이 단원에서는 다음 내용을 배웁니다.

- 어떻게 tooinstall Git 및 Node.js 합니다.
  - Git는 오픈 소스 분산 버전 제어 시스템입니다. 이 단원에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.
  - Node.js는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.
- 어떻게 toouse NPM tooinstall Node.js 개발 도구입니다.
  - hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.
  - NPM은 Node.js 용 hello 패키지 관리자 중 하나입니다.
- Tooinstall 어떻게 Visual Studio 코드.
  - Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 플랫폼 간 강력한 소스 코드 편집기입니다. 또한 디버깅, 포함된 Git 컨트롤, 구문 강조, 지능형 코드 완성, 스니펫 및 코드 리팩터링에 대해 탁월한 지원을 제공합니다.
- Tooinstall은 Azure CLI hello 하는 방법
  - hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다. 명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.
- 어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.

## <a name="what-you-need"></a>필요한 항목

- 인터넷 연결 toodownload 도구와 소프트웨어 hello 합니다.
- Ubuntu 16.04 이상을 실행하는 컴퓨터.

## <a name="install-git-and-nodejs"></a>Git 및 Node.js 설치

Git tooinstall 및 Node.js를 다음이 단계를 따르십시오.

1. 키를 눌러 `Ctrl + Alt + T` tooopen 터미널입니다.
2. Hello 다음 명령을 실행 합니다.

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Node.js 개발 도구 설치

사용 하면 [gulp.js](http://gulpjs.com/) tooautomate 배포 및 스크립트를 실행 합니다.

tooinstall gulp: hello 다음 hello 터미널에서 명령을 실행 합니다.

```bash
sudo npm install -g gulp
```

Hello 설치 관련 문제에 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-gateway-kit-c-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.

> [!Note]
> 노드, NPM 및 Gulp는 Node.js에서 개발 된 필요한 toorun 자동화 스크립트입니다.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI를 설치 합니다.

tooinstall hello Azure CLI 다음이 단계를 따르십시오.

1. Hello 명령을 hello 터미널에 다음을 실행 합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   hello 설치에는 5 분 정도 걸릴 수 있습니다.

2. Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.

   ```bash
   az iot -h
   ```
Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.
![Azure CLI 설치 확인](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Visual Studio Code 설치

Hello 자습서 tooedit 구성 파일에서 Visual Studio Code를 나중에 사용 합니다.

Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다.

## <a name="summary"></a>요약

호스트 컴퓨터에서 모든 hello 필요한 도구와 소프트웨어를 설치 했습니다. 다음 작업 toouse hello Azure CLI toocreate IoT hub 이며 IoT hub에 장치를 등록 합니다.

## <a name="next-steps"></a>다음 단계
[IoT Hub 만들기 및 장치 등록](iot-hub-gateway-kit-c-lesson2-register-device.md)
