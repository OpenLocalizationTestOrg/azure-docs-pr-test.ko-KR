---
title: "연결 라스베리 Pi (노드) tooAzure IoT-2 단원: 도구 (Ubuntu) 가져오기 | Microsoft Docs"
description: "Python을 설치 하 고 Azure CLI (명령줄 인터페이스 Azure) ubuntu hello 키를 누릅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 클라우드 서비스, Azure CLI"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0adf91bef41f502e1333fdcc75cfb2fe912364c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Azure 도구 얻기(Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 이상](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>수행할 사항
Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 tooinstall hello Azure CLI 합니다.
* 어떻게 tooadd hello Azure CLI는 IoT 하위 그룹입니다.

## <a name="what-you-need"></a>필요한 항목
* 인터넷에 연결된 Ubuntu 컴퓨터.
* 활성 Azure 구독. 계정이 없는 경우 몇 분 만에 [무료 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI를 설치 합니다.
hello Azure CLI toowork 명령줄 tooprovision 프로그램에서 직접 사용 하면 Azure에 대 한 다중 플랫폼 명령줄 환경을 제공 하 고 리소스를 관리 합니다.

tooinstall 최신 Azure CLI hello, 다음이 단계를 수행 합니다.

1. Hello 명령을 터미널 창에서 다음을 실행 합니다. 5 분 tooinstall hello Azure CLI 걸릴 수 있습니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.

   ```bash
   az iot -h
   ```

Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.

![성공을 나타내는 출력](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>요약
Hello Azure CLI를 설치 했습니다. 다음 작업은 toocreate Azure IoT hub 및 사용 하 여 장치 id hello Azure CLI 합니다.

## <a name="next-steps"></a>다음 단계
[IoT Hub 만들기 및 Raspberry Pi 3 등록](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

