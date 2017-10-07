---
title: "aaaAzure 함수 SendGrid 바인딩 | Microsoft Docs"
description: "Azure Functions SendGrid 바인딩 참조"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="1c257-103">Azure Functions SendGrid 바인딩</span><span class="sxs-lookup"><span data-stu-id="1c257-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="1c257-104">이 문서에서는 설명 어떻게 tooconfigure 정보와 Azure 함수에서 SendGrid 바인딩을 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="1c257-105">SendGrid를 하 여 프로그래밍 방식으로 Azure 함수 toosend 사용자 지정 전자 메일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="1c257-106">이 문서는 Azure Functions 개발자를 위한 참조 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="1c257-107">새로운 tooAzure 함수를 사용 하는 경우 다음 리소스는 hello로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="1c257-108">[첫 번째 Azure Function 만들기](functions-create-first-azure-function.md)</span><span class="sxs-lookup"><span data-stu-id="1c257-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="1c257-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) 또는 [Node](functions-reference-node.md) 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="1c257-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="1c257-110">SendGrid 바인딩의 function.json</span><span class="sxs-lookup"><span data-stu-id="1c257-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="1c257-111">Azure Functions는 SendGrid에 대해 출력 바인딩을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="1c257-112">SendGrid hello 바인딩을 사용 하면 toocreate 후 전자 메일 보내기 프로그래밍 방식으로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="1c257-113">hello SendGrid 바인딩은 hello를 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="1c257-114">`name`: 필수-hello 요청 또는 요청 본문에 대 한 함수 코드에서 사용 하는 hello 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="1c257-115">반환 값이 하나만 있는 경우 이 값은 ```$return```입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="1c257-116">`type`: 필수-설정 해야 너무 "sendGrid."</span><span class="sxs-lookup"><span data-stu-id="1c257-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="1c257-117">`direction`: 필수-"out" 너무 설정 해야</span><span class="sxs-lookup"><span data-stu-id="1c257-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="1c257-118">`apiKey`: 필수-hello 함수 응용 프로그램의 응용 프로그램 설정에 저장 된 사용자의 API 키의 집합 toohello 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="1c257-119">`to`: hello 받는 사람의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="1c257-120">`from`: hello 보낸 사람의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="1c257-121">`subject`: hello 전자 메일의 hello 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="1c257-122">`text`: 전자 메일 콘텐츠 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-122">`text` : hello email content.</span></span>

<span data-ttu-id="1c257-123">**function.json**의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-123">Example of **function.json**:</span></span>

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="1c257-124">Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="1c257-125">이 작업은 사용자의 중요한 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="1c257-126">SendGrid hello의 C# 예제에서는 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="1c257-126">C# example of hello SendGrid output binding</span></span>

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="1c257-127">Hello의 노드가 예 SendGrid 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="1c257-127">Node example of hello SendGrid output binding</span></span>

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a><span data-ttu-id="1c257-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c257-128">Next steps</span></span>
<span data-ttu-id="1c257-129">Azure Functions에 대한 다른 바인딩 및 트리거에 대한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c257-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="1c257-130">Azure Functions 트리거 및 바인딩 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="1c257-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="1c257-131">[Azure 기능에 대 한 유용한](functions-best-practices.md) Azure 함수를 만들 때 몇 가지 모범 사례 toouse를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="1c257-132">[Azure Functions 개발자 참조](functions-reference.md) 함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="1c257-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
