---
title: "aaaAzure 함수 타이머 트리거 | Microsoft Docs"
description: "Azure 함수에서 toouse 타이머 트리거 하는 방법을 이해 합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="bd184-104">Azure Functions 타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="bd184-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="bd184-105">이 문서에서는 Azure 함수에서 tooconfigure 및 코드 타이머 트리거 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="bd184-106">Azure Functions에는 정의된 일정에 따라 함수 코드를 실행할 수 있는 타이머 트리거 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="bd184-107">hello 타이머 트리거 다중 인스턴스 확장을 지원합니다. 특정 타이머 함수의 단일 인스턴스는 모든 인스턴스에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="bd184-108">타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="bd184-108">Timer trigger</span></span>
<span data-ttu-id="bd184-109">hello 타이머 트리거 tooa 함수 사용 하 여 hello에 대 한 JSON 개체를 다음 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="bd184-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="bd184-110">값을 hello `schedule` 은 [CRON 식](http://en.wikipedia.org/wiki/Cron#CRON_expression) 이러한 6 개의 필드에 포함 된:</span><span class="sxs-lookup"><span data-stu-id="bd184-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="bd184-111">Hello를 생략 하는 다양 한 온라인 찾았으면 hello cron 식 `{second}` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="bd184-112">이들 중 하나에서 복사 하는 경우 해야 tooadjust hello 추가 `{second}` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="bd184-113">특정 예제를 보려면 아래에 있는 [일정 예제](#examples)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd184-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="bd184-114">hello CRON 식과 함께 사용 하는 hello 기본 표준 시간대는 utc (협정 세계시)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="bd184-115">toohave CRON 식은 다른 표준 시간대를 기반으로 명명 된 함수 앱에 대 한 새 응용 프로그램 설정 만들기 `WEBSITE_TIME_ZONE`합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="bd184-116">Hello 값 toohello 이름을 가져옵니다. hello hello에 표시 된 대로 표준 시간대를 원하는 [Microsoft 표준 시간대 색인](https://msdn.microsoft.com/library/ms912391.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="bd184-117">예를 들어 *동부 표준시*는 UTC-05:00입니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="bd184-118">toohave 타이머 오전 10시 EST 매일 사용 하 여 hello 다음 CRON 식은 UTC 표준 시간대에 대 한 계정 하에서 실행을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="bd184-119">명명 된 함수 앱에 대 한 새 응용 프로그램 설정을 추가할 수는 또는 `WEBSITE_TIME_ZONE` 너무 hello 값을 설정 하 고**동부 표준시**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="bd184-120">그런 다음 다음 CRON 식은 hello 오전 10시 EST에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="bd184-121">일정 예제</span><span class="sxs-lookup"><span data-stu-id="bd184-121">Schedule examples</span></span>
<span data-ttu-id="bd184-122">다음은 hello에 사용할 수는 CRON 식의 몇 가지 샘플이 `schedule` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="bd184-123">5 분 마다 한 번씩 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="bd184-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="bd184-124">매 시간 마다 hello 위쪽에 한 번 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="bd184-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="bd184-125">두 시간 마다 한 번씩 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="bd184-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="bd184-126">tootrigger 1 시간 마다 too5 오전 9 시에서에서 오후:</span><span class="sxs-lookup"><span data-stu-id="bd184-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="bd184-127">오전 9 시 30 매일 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="bd184-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="bd184-128">오전 9 시 30 주중 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="bd184-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="bd184-129">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="bd184-129">Trigger usage</span></span>
<span data-ttu-id="bd184-130">타이머 트리거 함수 호출 되 면 hello [타이머 개체](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) hello 함수에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="bd184-131">hello 다음 JSON 예제 표현은 hello 타이머 개체의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd184-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="bd184-132">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="bd184-132">Trigger sample</span></span>
<span data-ttu-id="bd184-133">있다고 가정 하면 다음 hello에서 타이머 트리거 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="bd184-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="bd184-134">Hello 타이머 개체 toosee 늦게 실행 되는지 여부를 읽을 수 있는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bd184-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="bd184-135">C#</span><span class="sxs-lookup"><span data-stu-id="bd184-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="bd184-136">F#</span><span class="sxs-lookup"><span data-stu-id="bd184-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="bd184-137">Node.JS</span><span class="sxs-lookup"><span data-stu-id="bd184-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="bd184-138">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="bd184-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="bd184-139">F#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="bd184-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="bd184-140">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="bd184-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="bd184-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd184-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

