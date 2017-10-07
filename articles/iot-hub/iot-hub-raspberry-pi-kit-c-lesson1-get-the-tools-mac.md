---
title: "Connect Raspberry Pi (C) tooAzure IoT-1 단원: 도구 (macOS) 가져오기 | Microsoft Docs"
description: "다운로드 하 고 macOS에서 hello 필요한 도구와 hello 첫 번째 Pi에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, mac에 git 설치, gulp 실행, node js mac 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Hello 도구 (macOS 10.10) 가져오기
> [!div class="op_single_selector"]
> * [Windows 7 이상](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>수행할 사항
Hello 개발 도구와 hello 첫 번째 라스베리 Pi 3에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.

> [!NOTE]
> 프로그래밍 언어의 기본 논리 hello hello C 이지만, Node.js 도구 hello 단원 toodiscover 장치에 사용 되 빌드 및 배포 예제 응용 프로그램입니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* 어떻게 tooinstall Git 및 Node.js 합니다.
  * [Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다. 이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.
  * [Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.
* 어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.
  * hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.
  * [NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.

## <a name="what-you-need"></a>필요한 항목
toocomplete이 작업을이 수행 해야 합니다.

* 인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.
* macOS Yosemite(10.10) 이상을 실행하는 Mac.

## <a name="install-git-and-nodejs"></a>Git 및 Node.js 설치
Git tooinstall 및 Node.js를 사용 하 여 hello [Homebrew](http://brew.sh) 다음이 단계를 수행 하 여 관리 유틸리티를 패키지:

1. Homebrew를 설치합니다. Homebrew를 이미 설치한 경우 2 toostep를 이동 합니다.
   
   1. 키를 눌러 `Cmd + Space` 입력 `Terminal` tooopen 터미널입니다.
   2. Hello 다음 명령을 실행 합니다.
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Hello 다음 명령을 실행 하 여 Git 및 Node.js를 설치 합니다.
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>추가 Node.js 개발 도구 설치
사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooyour Pi의 tooautomate hello 배포 합니다. 사용 하 여 hello [장치-검색-cli](https://github.com/Azure/device-discovery-cli) IoT 장치에 대 한 tooretrieve 네트워크 정보입니다.

설치 `gulp` 및 `device-discovery-cli` hello 다음 hello 터미널에서 명령을 실행 하 여:

```bash
sudo npm install -g device-discovery-cli gulp
```

MacOS에서 Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-raspberry-pi-kit-c-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.

## <a name="install-visual-studio-code"></a>Visual Studio Code 설치
Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다. Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다. 이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.

## <a name="summary"></a>요약
필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다. hello 다음 작업은 toocreate, 배포 및 원주율 hello 샘플 응용 프로그램을 실행 합니다.

## <a name="next-steps"></a>다음 단계
[만들기 및 hello 깜박임 응용 프로그램 배포](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

