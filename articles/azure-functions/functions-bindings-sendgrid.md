---
title: "Azure Functions SendGrid 바인딩 | Microsoft Docs"
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
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="8a2bf-103">Azure Functions SendGrid 바인딩</span><span class="sxs-lookup"><span data-stu-id="8a2bf-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="8a2bf-104">이 문서에서는 Azure Functions에서 SendGrid 바인딩을 구성하고 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="8a2bf-105">SendGrid에서 Azure Functions를 사용하여 프로그래밍 방식으로 사용자 지정된 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="8a2bf-106">이 문서는 Azure Functions 개발자를 위한 참조 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="8a2bf-107">Azure Functions를 처음 접하는 경우 다음 리소스부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="8a2bf-108">[첫 번째 Azure Function 만들기](functions-create-first-azure-function.md)</span><span class="sxs-lookup"><span data-stu-id="8a2bf-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="8a2bf-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) 또는 [Node](functions-reference-node.md) 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="8a2bf-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="8a2bf-110">SendGrid 바인딩의 function.json</span><span class="sxs-lookup"><span data-stu-id="8a2bf-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="8a2bf-111">Azure Functions는 SendGrid에 대해 출력 바인딩을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="8a2bf-112">SendGrid 출력 바인딩을 사용하면 프로그래밍 방식으로 전자 메일을 만들고 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="8a2bf-113">SendGrid 바인딩에서 지원하는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="8a2bf-114">`name`: 필수 - 요청 또는 요청 본문의 함수 코드에 사용되는 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="8a2bf-115">반환 값이 하나만 있는 경우 이 값은 ```$return```입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="8a2bf-116">`type`: 필수 - "SendGrid"로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="8a2bf-117">`direction`: 필수 - "out"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="8a2bf-118">`apiKey`: 필수 - 함수 앱의 앱 설정에 저장된 API 키의 이름으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="8a2bf-119">`to`: 수신자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="8a2bf-120">`from`: 발신자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="8a2bf-121">`subject`: 메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="8a2bf-122">`text`: 전자 메일 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-122">`text` : the email content.</span></span>

<span data-ttu-id="8a2bf-123">**function.json**의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="8a2bf-124">Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="8a2bf-125">이 작업은 사용자의 중요한 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="8a2bf-126">SendGrid 출력 바인딩의 C# 예제</span><span class="sxs-lookup"><span data-stu-id="8a2bf-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="8a2bf-127">SendGrid 출력 바인딩의 Node 예제</span><span class="sxs-lookup"><span data-stu-id="8a2bf-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8a2bf-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a2bf-128">Next steps</span></span>
<span data-ttu-id="8a2bf-129">Azure Functions에 대한 다른 바인딩 및 트리거에 대한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="8a2bf-130">Azure Functions 트리거 및 바인딩 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="8a2bf-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="8a2bf-131">[Azure Functions에 대한 모범 사례](functions-best-practices.md) Azure Functions를 만들 때 사용할 몇 가지 모범 사례를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="8a2bf-132">[Azure Functions 개발자 참조](functions-reference.md) 함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="8a2bf-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
