---
title: "Intel Edison (노드) tooAzure IoT-1과 연결: 도구 (Ubuntu) 가져오기 | Microsoft Docs"
description: "다운로드 및 ubuntu hello 필요한 도구와 hello 첫 번째 Edison에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 개발 도구, IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, Ubuntu에 Git 설치, gulp 실행, Node Js Ubuntu 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Hello 도구 (Ubuntu 16.04) 가져오기

> [!div class="op_single_selector"]
> * [Windows 7 이상][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>수행할 사항
Hello 개발 도구와 hello 첫 번째 Intel Edison에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* 어떻게 tooinstall Git 및 Node.js
  * [Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다. 이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.
  * [Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.
* 어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.
  * hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.
  * [NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.

## <a name="what-you-need"></a>필요한 항목
toocomplete이 작업을이 수행 해야 합니다.
* 인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.
* Ubuntu 16.04 이상을 실행하는 컴퓨터.

## <a name="install-git-nodejs-and-npm"></a>Git, Node.js 및 NPM 설치
사용 하 여 hello에 대 한 바로 가기 키 `Ctrl + Alt + T` tooopen 다음 터미널 하 고 실행할 hello 명령:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>추가 Node.js 개발 도구 설치
사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooEdison의 tooautomate hello 배포 합니다.

설치 `gulp` hello 다음 hello 터미널에서 명령을 실행 하 여:

```bash
sudo npm install -g gulp
```

Ubuntu Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.

## <a name="install-visual-studio-code"></a>Visual Studio Code 설치
Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다. Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다. 이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.

## <a name="summary"></a>요약
필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다. hello 다음 작업은 toocreate, 배포 및 Edison에 hello 샘플 응용 프로그램을 실행 합니다.

## <a name="next-steps"></a>다음 단계
[만들기 및 hello 깜박임 샘플 응용 프로그램 배포][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
