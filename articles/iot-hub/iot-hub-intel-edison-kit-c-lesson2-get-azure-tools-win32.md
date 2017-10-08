---
title: "Connect Intel Edison (C) tooAzure IoT-2 단원: Azure tools (Windows) | Microsoft Docs"
description: "Windows 7 이상 버전에서 Python 및 hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure cli, IoT 클라우드 서비스, Arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 46f964541c00674500e4f6a072a9a2547b5b24d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Azure 도구 얻기(Windows 7 이상)
> [!div class="op_single_selector"]
> * [Windows 7 이상][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>수행할 사항
Python을 설치 하 고 hello Azure CLI (명령줄 인터페이스 Azure). 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 tooinstall Python 합니다.
* 어떻게 tooinstall hello Azure CLI 합니다.

## <a name="what-you-need"></a>필요한 항목
* 인터넷에 연결된 Windows 컴퓨터.
* 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.

## <a name="install-python"></a>Python 설치
Windows 컴퓨터에 [Python을 설치](https://www.python.org/downloads/)합니다. Python 2.7, 3.4 또는 3.5를 설치할 수 있습니다. 이 자습서는 Python 2.7을 기반으로 합니다. Python을 이미 설치한 경우 다음 섹션 toohello 이동한 다음 hello Azure CLI를 설치 합니다.

또한 python.exe 및 pip.exe는 설치 된 toohello 시스템 hello 폴더의 tooadd hello 경로 해야 `PATH` 환경 변수입니다. 기본적으로 python.exe는 `C:\Python27`에, pip.exe는 `C:\Python27\Scripts`에 설치되어 있습니다.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI를 설치 합니다.
hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다. 명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.

tooinstall hello Azure CLI 다음이 단계를 따르십시오.

1. 관리자로 명령 프롬프트 창을 엽니다.
2. Hello 다음 명령을 실행 합니다.

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.

   ```cmd
   az iot -h
   ```

Hello 다음 hello 설치에 성공한 경우 출력 하는 것이 표시 됩니다.

![성공을 나타내는 출력](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>요약
Hello Azure CLI를 설치 했습니다. 다음 번 toocreate Azure IoT hub 및 장치 id hello Azure CLI를 사용 하 여 작업 합니다.

## <a name="next-steps"></a>다음 단계
[IoT Hub 만들기 및 Intel Edison 등록][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
