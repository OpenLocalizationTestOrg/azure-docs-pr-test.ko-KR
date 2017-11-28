---
title: "aaaAzure 함수 Twilio 바인딩 | Microsoft Docs"
description: "이해 어떻게 Azure 함수로 toouse Twilio 바인딩."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="ef56a-104">Azure 함수에서 SMS 메시지를 보낼 hello를 사용 하 여 Twilio 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="ef56a-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ef56a-105">이 문서에서는 설명 어떻게 Azure 함수로 Twilio 바인딩 tooconfigure 및 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="ef56a-106">Azure 기능 지원 Twilio 출력 바인딩 tooenable 몇 줄의 코드로 함수 toosend SMS 텍스트 메시지와 [Twilio](https://www.twilio.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="ef56a-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="ef56a-107">hello에 대 한 function.json Twilio 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="ef56a-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="ef56a-108">hello function.json 파일 hello를 다음과 같은 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="ef56a-109">`name`: Hello Twilio SMS 문자 메시지에 대 한 함수 코드에서 사용 되는 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="ef56a-110">`type`: 너무 설정 되어 있어야*"twilioSms"*합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="ef56a-111">`accountSid`: Twilio 계정 Sid를 보유 하는 응용 프로그램 설정의 toohello 이름이이 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="ef56a-112">`authToken`: Twilio 인증 토큰을 보유 하는 응용 프로그램 설정의 toohello 이름이이 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="ef56a-113">`to`:이 값은 hello SMS 텍스트에 전송 된 toohello 전화 번호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="ef56a-114">`from`:이 값은 hello SMS 텍스트 보내지는 toohello 전화 번호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="ef56a-115">`direction`: 너무 설정 되어 있어야*"out"*합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="ef56a-116">`body`:이 값 함수에 대 한 코드 hello에서 동적으로 tooset 필요 하지 않으면 사용 되는 toohard 코드 hello SMS 문자 메시지를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="ef56a-117">예제 function.json:</span><span class="sxs-lookup"><span data-stu-id="ef56a-117">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="ef56a-118">Twilio 출력 바인딩이 포함된 C# 큐 트리거 예제</span><span class="sxs-lookup"><span data-stu-id="ef56a-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="ef56a-119">동기</span><span class="sxs-lookup"><span data-stu-id="ef56a-119">Synchronous</span></span>
<span data-ttu-id="ef56a-120">Azure 저장소 큐 트리거는이 동기 예제 코드를 벗어난 사용 하 여 매개 변수 toosend 텍스트 메시지 tooa 고객 주문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="ef56a-121">비동기</span><span class="sxs-lookup"><span data-stu-id="ef56a-121">Asynchronous</span></span>
<span data-ttu-id="ef56a-122">이 비동기 예제 코드는 Azure 저장소 큐 트리거에 대 한 텍스트 메시지 tooa 고객에 게 주문을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="ef56a-123">Twilio 출력 바인딩이 포함된 Node.js 큐 트리거 예제</span><span class="sxs-lookup"><span data-stu-id="ef56a-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="ef56a-124">Node.js 예제 텍스트 메시지 tooa 고객에 게 주문을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef56a-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ef56a-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef56a-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

