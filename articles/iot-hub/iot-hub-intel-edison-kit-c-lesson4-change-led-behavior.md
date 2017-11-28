---
title: "Connect Intel Edison (C) tooAzure IoT-4 단원: hello LED Blink | Microsoft Docs"
description: "Hello 메시지 toochange hello 켜고 동작 LED가 사용자 지정 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino를 사용한 LED 제어"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="0f5cb-104">Hello 켜고 hello LED의 동작 변경</span><span class="sxs-lookup"><span data-stu-id="0f5cb-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0f5cb-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="0f5cb-105">What you will do</span></span>
<span data-ttu-id="0f5cb-106">Hello 메시지 toochange hello 켜고 동작 LED가 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="0f5cb-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0f5cb-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="0f5cb-108">What you will learn</span></span>
<span data-ttu-id="0f5cb-109">켜고 동작 LED가 함수를 추가로 toochange hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0f5cb-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="0f5cb-110">What you need</span></span>
<span data-ttu-id="0f5cb-111">성공적으로 완료 해야 [toodevice 메시지 Intel Edison tooreceive 클라우드에서 샘플 응용 프로그램을 실행][receive-cloud-to-device-messages]합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="0f5cb-112">함수 toomain.c 및 gulpfile.js 추가</span><span class="sxs-lookup"><span data-stu-id="0f5cb-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="0f5cb-113">Hello 다음 명령을 실행 하 여 Visual Studio code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="0f5cb-114">열기 hello `main.c` 파일을 선택한 다음 hello 함수 blinkLED() 함수 뒤에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![함수가 추가된 main.c 파일](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. <span data-ttu-id="0f5cb-116">추가 조건 hello 하기 전에 다음 hello `else if` hello 블록 `receiveMessageCallback` 함수:</span><span class="sxs-lookup"><span data-stu-id="0f5cb-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="0f5cb-117">이제 메시지를 통해 hello 샘플 응용 프로그램 toorespond toomore 지침을 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="0f5cb-118">"명령 에" hello hello LED 설정 하 고 "off" 명령은 hello hello LED 끕니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="0f5cb-119">다음 hello 함수 앞에 새 함수를 추가 하 고 hello gulpfile.js 파일을 열고 `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="0f5cb-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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

   ![함수가 추가된 Gulpfile.js 파일][gulpfile]
5. <span data-ttu-id="0f5cb-121">Hello에 `sendMessage` 함수, hello 줄 `var message = buildMessage(sentMessageCount);` hello 다음 코드 조각에에서 표시 된 hello 새 줄으로:</span><span class="sxs-lookup"><span data-stu-id="0f5cb-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="0f5cb-122">모든 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="0f5cb-123">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="0f5cb-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="0f5cb-124">배포 및 실행 hello 샘플 응용 프로그램 Edison hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="0f5cb-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="0f5cb-125">2 초에 대 한 hello LED 설정 및 다른 2 초에 대 한 다음 선택을 취소 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="0f5cb-126">hello 마지막 "중지" 메시지 hello 샘플 응용 프로그램의 실행을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-126">hello last "stop" message stops hello sample application from running.</span></span>

![켜기 및 끄기][on-and-off]

<span data-ttu-id="0f5cb-128">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-128">Congratulations!</span></span> <span data-ttu-id="0f5cb-129">TooEdison IoT 허브에서 보낸 hello 메시지를 사용자 지정한 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="0f5cb-130">요약</span><span class="sxs-lookup"><span data-stu-id="0f5cb-130">Summary</span></span>
<span data-ttu-id="0f5cb-131">이 선택적 섹션이 toocustomize hello 샘플 응용 프로그램을 다른 방식으로 hello 켜고 hello LED의 동작을 제어할 수 있도록 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f5cb-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
