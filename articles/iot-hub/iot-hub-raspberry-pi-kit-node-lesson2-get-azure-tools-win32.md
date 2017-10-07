---
title: "연결 라스베리 Pi (노드) tooAzure IoT-2 단원: 도구 (Windows) 가져오기 | Microsoft Docs"
description: "Windows 7 이상 버전에서 Python 및 hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 클라우드 서비스, Azure CLI"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Azure 도구 얻기(Windows 7 이상)
> [!div class="op_single_selector"]
> * [Windows 7 이상](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>수행할 사항
Python을 설치 하 고 hello Azure CLI (명령줄 인터페이스 Azure). 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.

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
hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다. 프로그램 명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.

tooinstall hello Azure CLI 다음이 단계를 따르십시오.

1. 관리자로 명령 프롬프트 창을 엽니다.
2. Hello 다음 명령을 실행 합니다.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.

   ```bash
   az iot -h
   ```

Hello 다음 hello 설치에 성공한 경우 출력 하는 것이 표시 됩니다.

![성공을 나타내는 출력](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>요약
Hello Azure CLI를 설치 했습니다. 다음 번 toocreate Azure IoT hub 및 장치 id hello Azure CLI를 사용 하 여 작업 합니다.

## <a name="next-steps"></a>다음 단계
[IoT Hub 만들기 및 Raspberry Pi 3 등록](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

