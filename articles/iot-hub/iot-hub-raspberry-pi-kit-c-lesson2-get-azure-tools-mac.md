---
title: "Connect Raspberry Pi (C) tooAzure IoT-2 단원: Azure tools (macOS) | Microsoft Docs"
description: "macOS에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 클라우드 서비스, Azure CLI"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Azure 도구 얻기(macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 이상](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>수행할 사항
Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 tooinstall Azure CLI 합니다.
* 어떻게 tooadd hello Azure CLI는 IoT 하위 그룹입니다.

## <a name="what-you-need"></a>필요한 항목
* 인터넷에 연결된 Mac.
* 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.

## <a name="install-python"></a>Python 설치
MacOS는 hello 초기 Python 2.7 함께 제공, 되지만 Homebrew 통해 Python을 설치 하는 것이 좋습니다. [macOS에서 Python 설치](http://docs.python-guide.org/en/latest/starting/install/osx/)를 참조하세요.

Python 및 pip hello 다음 명령을 실행 하 여 설치 합니다.

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Hello Azure CLI를 설치 합니다.
hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다. 명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다. 

tooinstall 최신 Azure CLI hello, 다음이 단계를 수행 합니다.

1. Hello 명령을 터미널 창에서 다음을 실행 합니다. 5 분 tooinstall hello Azure CLI 걸릴 수 있습니다.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.

   ```bash
   az iot -h
   ```

Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.

![성공을 나타내는 출력](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>요약
Hello Azure CLI를 설치 했습니다. 다음 작업은 toocreate Azure IoT hub 및 장치 id를 사용 하 여 hello Azure CLI 합니다.

## <a name="next-steps"></a>다음 단계
[IoT Hub 만들기 및 Raspberry Pi 3 등록](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

