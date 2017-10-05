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
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="9b845-104">LED 켜기 및 끄기 동작 변경</span><span class="sxs-lookup"><span data-stu-id="9b845-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9b845-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="9b845-105">What you will do</span></span>
<span data-ttu-id="9b845-106">LED의 켜기 및 끄기 동작을 변경하도록 메시지를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="9b845-107">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="9b845-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9b845-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="9b845-108">What you will learn</span></span>
<span data-ttu-id="9b845-109">추가적인 Node.js 함수를 사용하여 LED 켜기 및 끄기 동작 변경.</span><span class="sxs-lookup"><span data-stu-id="9b845-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9b845-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="9b845-110">What you need</span></span>
<span data-ttu-id="9b845-111">[Raspberry Pi에서 샘플 응용 프로그램을 실행하여 클라우드-장치 메시지 받기](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud to device messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="9b845-112">main.c 및 gulpfile.js에 기능 추가</span><span class="sxs-lookup"><span data-stu-id="9b845-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="9b845-113">다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="9b845-114">`main.c` 파일을 연 후, 다음 함수를 blinkLED() 함수 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="9b845-116">`receiveMessageCallback` 함수의 `if` 블록에 있는 기본 조건 앞에 다음 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-116">Add the following conditions before the default one in the `if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="9b845-117">이제 샘플 응용 프로그램이 메시지를 통해 더 많은 명령에 응답하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="9b845-118">"on" 명령은 LED를 켜고 "off" 명령은 LED를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="9b845-119">gulpfile.js file 파일을 연 다음 `sendMessage` 함수 앞에 새 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="9b845-121">`sendMessage` 함수에서 `var message = buildMessage(sentMessageCount);`를 다음 코드 조각에 있는 새 줄로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="9b845-122">모든 변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="9b845-123">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="9b845-123">Deploy and run the sample application</span></span>
<span data-ttu-id="9b845-124">다음 명령을 실행하여 Pi에 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="9b845-125">LED가 2초간 켜졌다가 다음 2초간 꺼지는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="9b845-126">마지막 "stop" 메시지는 샘플 응용 프로그램이 실행되는 것을 막습니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-126">The last "stop" message stops the sample application from running.</span></span>

![on 및 off 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="9b845-128">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-128">Congratulations!</span></span> <span data-ttu-id="9b845-129">IoT Hub에서 Pi로 보내는 메시지에 대한 사용자 지정이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="9b845-130">요약</span><span class="sxs-lookup"><span data-stu-id="9b845-130">Summary</span></span>
<span data-ttu-id="9b845-131">이 선택적인 섹션은 샘플 응용 프로그램이 다른 방식으로 LED를 켜고 끄는 동작을 제어할 수 있도록 메시지를 사용자 지정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b845-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>
