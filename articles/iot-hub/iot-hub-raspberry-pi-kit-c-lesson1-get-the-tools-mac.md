---
title: "Azure IoT에 Raspberry Pi(C) 연결 - 단원 1: 도구 다운로드(macOS) | Microsoft Docs"
description: "macOS에 Pi의 첫 번째 샘플 응용 프로그램에 필요한 도구 및 소프트웨어를 다운로드하여 설치합니다."
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
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>도구 얻기(macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 이상](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>수행할 사항
Raspberry Pi 3의 첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 다운로드합니다. 문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.

> [!NOTE]
> 기본 논리의 프로그래밍 언어는 C이며, Node.js 도구는 장치를 검색하고 샘플 응용 프로그램을 빌드하고 배포하는 단원에서 사용됩니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* Git 및 Node.js를 설치하는 방법.
  * [Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다. 이 문서에 대한 샘플 응용 프로그램은 Git에 저장됩니다.
  * [Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.
* NPM을 사용하여 추가 Node.js 개발 도구를 설치하는 방법.
  * Node.js의 최소 필수 버전은 4.5 LTS입니다.
  * [NPM](https://www.npmjs.com)은 Node.js에 대한 패키지 관리자 중 하나입니다.

## <a name="what-you-need"></a>필요한 항목
이 작업을 완료하려면 다음이 필요합니다.

* 개발 도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결.
* macOS Yosemite(10.10) 이상을 실행하는 Mac.

## <a name="install-git-and-nodejs"></a>Git 및 Node.js 설치
Git 및 Node.js를 설치하려면 다음 단계를 따라 [Homebrew](http://brew.sh) 패키지 관리 유틸리티를 사용하세요.

1. Homebrew를 설치합니다. Homebrew를 이미 설치한 경우 2단계로 이동하세요.
   
   1. `Cmd + Space`를 누르고 `Terminal`을 입력하여 터미널을 엽니다.
   2. 다음 명령을 실행합니다.
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. 다음 명령을 실행하여 Git 및 Node.js를 설치합니다.
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>추가 Node.js 개발 도구 설치
[gulp.js](http://gulpjs.com)를 사용하여 샘플 응용 프로그램이 Pi에 배포되는 것을 자동화합니다. [device-discovery-cli](https://github.com/Azure/device-discovery-cli)를 사용하여 IoT 장치에 대한 네트워크 정보를 검색합니다.

터미널에 다음 명령을 실행하여 `gulp` 및 `device-discovery-cli`를 설치합니다.

```bash
sudo npm install -g device-discovery-cli gulp
```

macOS에 Node.js 및 이러한 추가 개발 도구를 설치할 때 문제가 있는 경우 일반적인 문제의 솔루션에 관한 [문제 해결 가이드](iot-hub-raspberry-pi-kit-c-troubleshooting.md)를 참조하세요.

## <a name="install-visual-studio-code"></a>Visual Studio Code 설치
Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다. Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다. 이 자습서의 뒷부분에 나오는 샘플 코드를 편집하는 데 이 편집기를 사용합니다.

## <a name="summary"></a>요약
첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 설치했습니다. 다음 작업은 Pi에서 샘플 응용 프로그램을 만들고, 배포하고, 실행하는 것입니다.

## <a name="next-steps"></a>다음 단계
[깜박임 응용 프로그램 만들기 및 배포](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

