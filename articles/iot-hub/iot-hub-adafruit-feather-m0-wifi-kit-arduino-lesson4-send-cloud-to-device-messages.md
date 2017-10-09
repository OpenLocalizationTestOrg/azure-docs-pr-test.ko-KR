---
title: "Connect Arduino (C) tooAzure IoT-4 단원: 클라우드-장치 | Microsoft Docs"
description: "샘플 응용 프로그램은 Adafruit Feather M0 WiFi에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 메시지 tooAdafruit 페더 M0 WiFi를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "웹에서 수행한 Arduino 제어, 웹을 통해 수행한 Arduino 제어"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>클라우드-장치 메시지 샘플 응용 프로그램 tooreceive 실행
이 문서에서는 Adafruit Feather M0 WiFi Arduino 보드에 샘플 응용 프로그램을 배포합니다.

샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다. 실행할 수도 있습니다 gulp 작업 컴퓨터 toosend 메시지 tooyour Arduino 보드 IoT 허브에서 합니다. 샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-do"></a>수행할 사항
* Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.
* 배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.
* 프로그램 IoT 허브 tooyour Arduino 보드 tooblink hello LED에서에서 메시지를 전송 합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 IoT 허브에서 toomonitor 들어오는 메시지입니다.
* IoT 허브 tooyour Arduino 보드에서에서 toosend 클라우드-장치 메시지 방법을

## <a name="what-you-need"></a>필요한 항목
* Arduino 보드를 사용하도록 설정합니다. tooset Arduino 보드를 확인 하려면 어떻게 해야 toolearn [장치 구성][configure-your-device]합니다.
* Azure 구독에서 만든 IoT Hub. toolearn 어떻게 toocreate IoT 허브 참조 [Azure IoT Hub를 만들][create-your-azure-iot-hub]합니다.

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Hello 샘플 응용 프로그램 tooyour IoT 허브 연결

1. Hello 리포지토리 폴더에 본인 `iot-hub-c-feather-m0-getting-started`합니다.

   Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.

   ```bash
   cd Lesson4
   code .
   ```

   공지 hello `app.ino` hello에 대 한 파일 `app` 하위 폴더입니다. hello `app.ino` 파일은 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다. hello `blinkLED` 함수 hello led가 깜박입니다.

   ![Hello 샘플 응용 프로그램의 리 포 구조][repo-structure]

2. Hello hello 장치 검색 cli 사용 하 여 hello 장치의 직렬 포트를 가져옵니다.

   ```bash
   devdisco list --usb
   ```

   Toohello 다음과 유사한 출력을 확인 및 Arduino 보드에 대 한 hello usb COM 포트를 찾을 해야 하면:

   ![장치 검색][device-discovery]

3. 파일 열기 hello `config.json` hello 단원 폴더 및 폴더의 COM 포트 번호를 발견 하는 hello 입력된 hello 값에서:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Windows 플랫폼에서 hello COM 포트에 대 한 형식이 지므로 hello의 `COM1, COM2, ...`합니다. macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.

4. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Hello 바꾸기 작업을 수행 하는 hello 확인 `config-arduino.json` 파일:

   Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] 이 컴퓨터에 모든 hello 구성 상속 되므로 hello 단계 toohello 배포 작업을 건너뛸 수 있습니다 및 hello 샘플 응용 프로그램을 실행 합니다. Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-arduino.json` 파일입니다. hello `config-arduino.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.

   ![Hello arduino.json 구성 파일의 내용][config-arduino-json]

   * 대체 **[Wi-fi SSID]** toohello 인터넷 연결에 Wi-fi SSID로 합니다.
   * **[Wi-Fi password]**를 사용자의 Wi-Fi 암호로 바꿉니다. Wi-fi 암호 필요 하지 않은 경우 hello 문자열을 제거 합니다.
   * 대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 명령입니다.
   * 대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name}` 명령입니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 Arduino 보드에 hello 샘플 응용 프로그램을 실행:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

hello gulp 명령은 hello 샘플 응용 프로그램 tooyour Arduino 보드를 배포 합니다. 그런 다음 실행 hello 응용 프로그램 Arduino 보드 및 호스트에 별도 작업 컴퓨터 toosend 20 깜박임 메시지 tooyour Arduino 보드 IoT 허브에서 됩니다.

Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다. 한편, hello gulp 작업 IoT 허브 tooyour Arduino 보드에서에서 여러 개의 "blink" 메시지를 보냅니다. Hello 샘플 응용 프로그램에서는 hello 호출 보드 hello 각 깜박임 메시지 수신에 대 한 `blinkLED` 함수 tooblink hello LED.

Hello LED 표시 되어야 hello gulp 작업 IoT 허브 tooyour Arduino 보드에서에서 20 개의 메시지를 보내는 2 초 마다 깜박이게 합니다. hello 마지막 하나는 "중지" 메시지 hello 응용 프로그램이 실행을 중지 합니다.

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램][sample-application]

## <a name="summary"></a>요약
프로그램 IoT 허브 tooyour Arduino 보드 tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다. hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.

## <a name="next-steps"></a>다음 단계
[Hello 켜고 hello LED의 동작 변경][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md