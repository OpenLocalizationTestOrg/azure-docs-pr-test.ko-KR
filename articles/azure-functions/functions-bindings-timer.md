---
title: "Azure Functions 타이머 트리거 | Microsoft Docs"
description: "Azure Functions에서 타이머 트리거를 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure 함수, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="4876c-104">Azure Functions 타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="4876c-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="4876c-105">이 문서에서는 Azure Functions에서 타이머 트리거를 구성하고 코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="4876c-106">Azure Functions에는 정의된 일정에 따라 함수 코드를 실행할 수 있는 타이머 트리거 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="4876c-107">타이머 트리거는 다중 인스턴스 확장을 지원합니다. 특정 타이머 함수의 단일 인스턴스는 모든 인스턴스에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="4876c-108">타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="4876c-108">Timer trigger</span></span>
<span data-ttu-id="4876c-109">함수에 대한 타이머 트리거는 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="4876c-110">`schedule`의 값은 이러한 6개 필드를 포함하는 [CRON 식](http://en.wikipedia.org/wiki/Cron#CRON_expression)입니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="4876c-111">온라인에서 볼 수 있는 많은 cron 식은 `{second}` 필드를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="4876c-112">그 중 하나를 복사하는 경우 추가 `{second}` 필드에 대해 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="4876c-113">특정 예제를 보려면 아래에 있는 [일정 예제](#examples)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4876c-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="4876c-114">CRON 식과 함께 사용하는 기본 표준 시간대는 UTC(협정 세계시)입니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="4876c-115">다른 표준 시간대를 기반으로 하는 CRON 식을 사용하려면 `WEBSITE_TIME_ZONE`이라는 함수 앱에 대한 새 앱 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="4876c-116">[Microsoft 표준 시간대 색인](https://msdn.microsoft.com/library/ms912391.aspx)에 나온 대로 값을 원하는 표준 시간대의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="4876c-117">예를 들어 *동부 표준시*는 UTC-05:00입니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="4876c-118">타이머 트리거를 매일 오전 10시 EST에 발생하도록 하려면 UTC 표준 시간대를 반영하는 다음과 같은 CRON 식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="4876c-119">또는 `WEBSITE_TIME_ZONE`이라는 함수 앱에 대한 새 앱 설정을 추가하고 값을 **동부 표준시**로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="4876c-120">그런 다음 오전 10시 EST에 대해 다음과 같은 CRON 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="4876c-121">일정 예제</span><span class="sxs-lookup"><span data-stu-id="4876c-121">Schedule examples</span></span>
<span data-ttu-id="4876c-122">다음은 `schedule` 속성에 사용할 수 있는 몇 가지 샘플 CRON 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="4876c-123">5분마다 한 번씩 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="4876c-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="4876c-124">1시간마다 맨 위에 한 번씩 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="4876c-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="4876c-125">2시간마다 한 번씩 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="4876c-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="4876c-126">오전 9시에서 오후 5시까지 1시간마다 한 번씩 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="4876c-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="4876c-127">매일 오전 9시 30분에 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="4876c-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="4876c-128">월요일부터 금요일까지 오전 9시 30분에 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="4876c-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="4876c-129">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="4876c-129">Trigger usage</span></span>
<span data-ttu-id="4876c-130">타이머 트리거 함수를 호출하면 [타이머 개체](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs)가 함수에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="4876c-131">다음 JSON은 타이머 개체의 예제 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-131">The following JSON is an example representation of the timer object.</span></span> 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="4876c-132">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="4876c-132">Trigger sample</span></span>
<span data-ttu-id="4876c-133">function.json의 `bindings` 배열에 다음과 같은 타이머 트리거가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4876c-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="4876c-134">타이머 개체를 읽어 실행이 지연되는지 여부를 확인하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4876c-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="4876c-135">C#</span><span class="sxs-lookup"><span data-stu-id="4876c-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="4876c-136">F#</span><span class="sxs-lookup"><span data-stu-id="4876c-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="4876c-137">Node.JS</span><span class="sxs-lookup"><span data-stu-id="4876c-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="4876c-138">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="4876c-138">Trigger sample in C#</span></span> #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="4876c-139">F#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="4876c-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="4876c-140">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="4876c-140">Trigger sample in Node.js</span></span>
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="4876c-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4876c-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

