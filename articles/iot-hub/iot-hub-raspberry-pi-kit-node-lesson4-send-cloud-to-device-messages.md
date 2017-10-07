---
featureFlags: usabilla
title: "연결 라스베리 Pi (노드) tooAzure IoT-4 단원: 클라우드-장치 | Microsoft Docs"
description: "hello 샘플 응용 프로그램 플랫폼에서 실행 되 고 IoT 허브에서 들어오는 메시지를 모니터링 합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 tooPi 메시지를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "클라우드 toodevice, 클라우드에서 메시지"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Hello 샘플 응용 프로그램 tooreceive 클라우드-장치 메시지를 실행 합니다.
이 문서에서는 샘플 응용 프로그램을 Raspberry Pi 3에 배포합니다. 샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다. 실행할 수도 있습니다 gulp 작업 사용자 컴퓨터 toosend 메시지 tooPi IoT 허브에서 합니다. 샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다. 문제가 있는 경우 솔루션 hello에 seek [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.

## <a name="what-you-will-do"></a>수행할 사항
* Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.
* 배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.
* IoT 허브 tooPi tooblink hello LED에서에서 메시지를 전송 합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* IoT 허브에서의 toomonitor 받은 메시지
* IoT 허브 tooPi에서 toosend 클라우드-장치 메시지 방법을

## <a name="what-you-need"></a>필요한 항목
* 사용하도록 설정된 Raspberry Pi 3. tooset Pi 확인 하려면 어떻게 해야 toolearn [장치 구성](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)합니다.
* Azure 구독에서 만든 IoT Hub. toolearn 어떻게 toocreate IoT 허브 참조 [IoT 허브를 만들고 등록 라스베리 Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)합니다.

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Hello 샘플 응용 프로그램 tooyour IoT 허브 연결
1. Hello 리포지토리 폴더에 본인 `iot-hub-node-raspberrypi-getting-started`합니다. Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.
   
   ```bash
   cd Lesson4
   code .
   ```
   
   공지 hello `app.js` hello에 대 한 파일 `app` 하위 폴더입니다. hello `app.js` 파일은 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다. hello `blinkLED` 함수 hello led가 깜박입니다.
   
   ![Hello 샘플 응용 프로그램의 리 포 구조](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. 다음 명령을 hello를 사용 하 여 hello 구성 파일을 초기화 합니다.
   
   ```bash
   npm install
   gulp init
   ```
   
   Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) 이 컴퓨터에 모든 hello 구성 상속 되므로 toohello 작업 hello 샘플 응용 프로그램 실행 및 배포를 건너뛸 수 있습니다. Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-raspberrypi.json` 파일입니다. hello `config-raspberrypi.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.
   
   ![Hello raspberrypi.json 구성 파일의 내용](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* 대체 **[장치 호스트 이름 또는 IP 주소]** hello를 실행 하 여 얻을 수 있는 Pi 또는 hello 호스트 이름의 hello IP 주소로 `devdisco list --eth` 명령입니다.
* 대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` 명령입니다.
* 대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` 명령입니다.

> [!NOTE]
> 단원 1에서 **gulp install-tools**를 실행하지 않았다면 이 명령도 실행합니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 원주율 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp deploy && gulp run
```

hello 명령은 hello 샘플 응용 프로그램 tooPi를 배포 합니다. 그런 다음 실행 hello 응용 프로그램 Pi와 호스트에 별도 작업 컴퓨터 toosend 20 깜박임 메시지 tooPi IoT 허브에서 됩니다.

Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다. 한편, hello gulp 작업 IoT 허브 tooPi에서 여러 개의 "blink" 메시지를 보냅니다. Pi를 받는 각 깜박임 메시지에 대 한 hello 샘플 응용 프로그램 호출 hello `blinkLED` 함수 tooblink hello LED.

Hello led가 깜박입니다 hello로 2 초 마다 작업 IoT 허브 tooPi에서 20 메시지 전송 gulp 표시 되어야 합니다. hello 마지막 하나는 "중지" 메시지를 실행 하는 hello 응용 프로그램 toostop 알려주는입니다.

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>요약
IoT 허브 tooPi tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다. hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.

## <a name="next-steps"></a>다음 단계
[Hello 켜고 hello LED의 동작 변경](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

