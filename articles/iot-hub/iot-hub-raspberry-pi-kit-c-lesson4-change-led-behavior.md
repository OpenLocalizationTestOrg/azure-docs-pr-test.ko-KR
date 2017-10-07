---
title: "Connect Raspberry Pi (C) tooAzure IoT-4 단원: 응용 프로그램 수정 | Microsoft Docs"
description: "Hello 메시지 toochange hello 켜고 동작 LED가 사용자 지정 합니다."
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
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Hello 켜고 hello LED의 동작 변경
## <a name="what-you-will-do"></a>수행할 사항
Hello 메시지 toochange hello 켜고 동작 LED가 사용자 지정 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
켜고 동작 LED가 추가 Node.js 함수 toochange hello를 사용 합니다.

## <a name="what-you-need"></a>필요한 항목
성공적으로 완료 해야 [toodevice 메시지 라스베리 Pi tooreceive 클라우드에서 샘플 응용 프로그램을 실행](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)합니다.

## <a name="add-functions-toomainc-and-gulpfilejs"></a>함수 toomain.c 및 gulpfile.js 추가
1. Hello 다음 명령을 실행 하 여 Visual Studio code에서 hello 샘플 응용 프로그램을 엽니다.

   ```bash
   cd Lesson4
   code .
   ```
2. 열기 hello `main.c` 파일을 선택한 다음 hello 함수 blinkLED() 함수 뒤에 다음을 추가 합니다.

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
3. Hello hello 기본 하기 전에 조건 다음에 오는 hello 추가 `if` hello 블록 `receiveMessageCallback` 함수:

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

   이제 메시지를 통해 hello 샘플 응용 프로그램 toorespond toomore 지침을 구성 했습니다. "명령 에" hello hello LED 설정 하 고 "off" 명령은 hello hello LED 끕니다.
4. 다음 hello 함수 앞에 새 함수를 추가 하 고 hello gulpfile.js 파일을 열고 `sendMessage`:

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
5. Hello에 `sendMessage` 함수, hello 줄 `var message = buildMessage(sentMessageCount);` hello 다음 코드 조각에에서 표시 된 hello 새 줄으로:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. 모든 hello 변경 내용을 저장 합니다.

### <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 원주율 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp deploy && gulp run
```

2 초에 대 한 hello LED 설정 및 다른 2 초에 대 한 다음 선택을 취소 나타납니다. hello 마지막 "중지" 메시지 hello 샘플 응용 프로그램의 실행을 중지합니다.

![on 및 off 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

축하합니다. TooPi IoT 허브에서 보낸 hello 메시지를 사용자 지정한 했습니다.

### <a name="summary"></a>요약
이 선택적 섹션이 toocustomize hello 샘플 응용 프로그램을 다른 방식으로 hello 켜고 hello LED의 동작을 제어할 수 있도록 메시지 하는 방법을 보여 줍니다.
