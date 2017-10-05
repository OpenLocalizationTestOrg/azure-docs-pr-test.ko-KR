---
title: "Azure IoT에 Raspberry Pi(C) 연결 - 단원 4: 앱 수정 | Microsoft Docs"
description: "LED의 켜기 및 끄기 동작을 변경하도록 메시지를 사용자 지정합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Raspberry Pi로 LED 제어, Raspberry Pi LED 제어, Raspberry Pi 제어 LED"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b1e441b20e161f4a03d4c2c300b21aca4fedb2a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>LED 켜기 및 끄기 동작 변경
## <a name="what-you-will-do"></a>수행할 사항
LED의 켜기 및 끄기 동작을 변경하도록 메시지를 사용자 지정합니다. 문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.

## <a name="what-you-will-learn"></a>알아볼 내용
추가적인 Node.js 함수를 사용하여 LED 켜기 및 끄기 동작 변경.

## <a name="what-you-need"></a>필요한 항목
[Raspberry Pi에서 샘플 응용 프로그램을 실행하여 클라우드-장치 메시지 받기](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)를 완료해야 합니다.

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>main.c 및 gulpfile.js에 기능 추가
1. 다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.

   ```bash
   cd Lesson4
   code .
   ```
2. `main.c` 파일을 연 후, 다음 함수를 blinkLED() 함수 뒤에 추가합니다.

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![함수가 추가된 main.c 파일](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. `receiveMessageCallback` 함수의 `if` 블록에 있는 기본 조건 앞에 다음 조건을 추가합니다.

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   이제 샘플 응용 프로그램이 메시지를 통해 더 많은 명령에 응답하도록 구성되었습니다. "on" 명령은 LED를 켜고 "off" 명령은 LED를 끕니다.
4. gulpfile.js file 파일을 연 다음 `sendMessage` 함수 앞에 새 함수를 추가합니다.

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![함수가 추가된 Gulpfile.js 파일](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. `sendMessage` 함수에서 `var message = buildMessage(sentMessageCount);`를 다음 코드 조각에 있는 새 줄로 바꿉니다.

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. 모든 변경 사항을 저장합니다.

### <a name="deploy-and-run-the-sample-application"></a>샘플 응용 프로그램 배포 및 실행
다음 명령을 실행하여 Pi에 샘플 응용 프로그램을 배포하고 실행합니다.

```bash
gulp deploy && gulp run
```

LED가 2초간 켜졌다가 다음 2초간 꺼지는 것을 볼 수 있습니다. 마지막 "stop" 메시지는 샘플 응용 프로그램이 실행되는 것을 막습니다.

![on 및 off 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

축하합니다. IoT Hub에서 Pi로 보내는 메시지에 대한 사용자 지정이 완료되었습니다.

### <a name="summary"></a>요약
이 선택적인 섹션은 샘플 응용 프로그램이 다른 방식으로 LED를 켜고 끄는 동작을 제어할 수 있도록 메시지를 사용자 지정하는 방법을 보여줍니다.
