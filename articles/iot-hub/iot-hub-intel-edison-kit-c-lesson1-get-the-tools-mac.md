---
title: "Connect Intel Edison (C) tooAzure IoT-1 단원: 도구 (macOS) 가져오기 | Microsoft Docs"
description: "다운로드 하 고 macOS에서 hello 필요한 도구와 hello 첫 번째 Edison에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 개발 도구, IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, mac에 Git 설치, gulp 실행, Node Js mac 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 3f764f2e-25fa-4dde-9e8d-d278453fccfd
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a53331b0dce73c3dd51de91f07df86e28cbb6b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Hello 도구 (macOS 10.10) 가져오기
> [!div class="op_single_selector"]
> * [Windows 7 이상][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>수행할 사항
Hello 개발 도구와 hello 첫 번째 Intel Edison에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

> [!NOTE]
> 프로그래밍 언어의 기본 논리 hello hello C 이지만, 샘플 응용 프로그램을 배포 및는 Node.js 도구 hello 단원 toobuild에 사용 됩니다.

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
사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooyour Edison의 tooautomate hello 배포 합니다.

설치 `gulp` hello 다음 hello 터미널에서 명령을 실행 하 여:

```bash
sudo npm install -g gulp
```

MacOS에서 Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.

## <a name="install-visual-studio-code"></a>Visual Studio Code 설치
Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다. Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다. 이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.

## <a name="summary"></a>요약
필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다. hello 다음 작업은 toocreate, 배포 및 Edison에 hello 샘플 응용 프로그램을 실행 합니다.

## <a name="next-steps"></a>다음 단계
[만들기 및 hello 깜박임 응용 프로그램 배포][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
