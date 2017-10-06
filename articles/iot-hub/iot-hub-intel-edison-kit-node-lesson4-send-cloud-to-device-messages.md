---
title: "연결 Intel Edison (노드) tooAzure IoT-4 단원: 메시지를 받을 | Microsoft Docs"
description: "샘플 응용 프로그램은 Edison에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 tooEdison 메시지를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "웹에서 수행한 Arduino 제어, 웹을 통해 수행한 Arduino 제어"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>클라우드-장치 메시지 샘플 응용 프로그램 tooreceive 실행
이 문서에서는 샘플 응용 프로그램을 Intel Edison에 배포합니다. 샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다. 실행할 수도 있습니다 gulp 작업 사용자 컴퓨터 toosend 메시지 tooEdison IoT 허브에서 합니다. 샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-do"></a>수행할 사항
* Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.
* 배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.
* IoT 허브 tooEdison tooblink hello LED에서에서 메시지를 전송 합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 IoT 허브에서 toomonitor 들어오는 메시지입니다.
* IoT 허브 tooEdison에서 toosend 클라우드-장치 메시지 방법을

## <a name="what-you-need"></a>필요한 항목
* Intel Edison, 사용하도록 설정. tooset Edison를 확인 하려면 어떻게 해야 toolearn [장치 구성][configure-your-device]합니다.
* Azure 구독에서 만든 IoT Hub. toolearn 어떻게 toocreate IoT 허브 참조 [Azure IoT Hub를 만들][create-your-azure-iot-hub]합니다.

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Hello 샘플 응용 프로그램 tooyour IoT 허브 연결
1. Hello 리포지토리 폴더에 본인 `iot-hub-node-edison-getting-started`합니다. Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.

   ```bash
   cd Lesson4
   code .
   ```

   hello에 hello 파일 `app` 하위 폴더는 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다. hello `blinkLED` 함수 hello led가 깜박입니다.

   ![Hello 샘플 응용 프로그램의 리 포 구조][repo-structure]
2. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.

   ```bash
   npm install
   gulp init
   ```

   Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] 이 컴퓨터에 모든 hello 구성 상속 되므로 hello 단계 toohello 배포 작업을 건너뛸 수 있습니다 및 hello 샘플 응용 프로그램을 실행 합니다. Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-edison.json` 파일입니다. hello `config-edison.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.

   ![Hello edison.json 구성 파일의 내용](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * 대체 **[장치 호스트 이름 또는 IP 주소]** hello 장치 IP 주소 장치를 구성 했을 때를 표시 합니다.
   * 대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 명령입니다.
   * 대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name}` 명령입니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 및 실행 hello 샘플 응용 프로그램 Edison hello 다음 명령을 실행 하 여:

```bash
gulp deploy && gulp run
```

hello gulp 명령은 hello 샘플 응용 프로그램 tooEdison를 배포 합니다. 그런 다음 실행 hello 응용 프로그램 호스트에 별도 작업 및 Edison 컴퓨터 toosend 20 깜박임 메시지 tooEdison IoT 허브에서 됩니다.

Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다. 한편, hello gulp 작업 IoT 허브 tooEdison에서 여러 개의 "blink" 메시지를 보냅니다. Edison 받는 각 깜박임 메시지에 대 한 hello 샘플 응용 프로그램 호출 hello `blinkLED` 함수 tooblink hello LED.

Hello led가 깜박입니다 hello로 2 초 마다 작업 IoT 허브 tooEdison에서 20 메시지 전송 gulp 표시 되어야 합니다. hello 마지막 하나는 "중지" 메시지 hello 응용 프로그램이 실행을 중지 합니다.

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램][gulp-command-and-blink-messages]

## <a name="summary"></a>요약
IoT 허브 tooEdison tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다. hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.

## <a name="next-steps"></a>다음 단계
[Hello 켜고 hello LED의 동작 변경][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md