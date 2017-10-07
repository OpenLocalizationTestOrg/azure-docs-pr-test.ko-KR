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
# <a name="azure-functions-sendgrid-bindings"></a>Azure Functions SendGrid 바인딩

이 문서에서는 설명 어떻게 tooconfigure 정보와 Azure 함수에서 SendGrid 바인딩을 사용 하는 작업입니다. SendGrid를 하 여 프로그래밍 방식으로 Azure 함수 toosend 사용자 지정 전자 메일을 사용할 수 있습니다.

이 문서는 Azure Functions 개발자를 위한 참조 정보입니다. 새로운 tooAzure 함수를 사용 하는 경우 다음 리소스는 hello로 시작 합니다.

[첫 번째 Azure Function 만들기](functions-create-first-azure-function.md) 
[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) 또는 [Node](functions-reference-node.md) 개발자 참조

## <a name="functionjson-for-sendgrid-bindings"></a>SendGrid 바인딩의 function.json

Azure Functions는 SendGrid에 대해 출력 바인딩을 제공합니다. SendGrid hello 바인딩을 사용 하면 toocreate 후 전자 메일 보내기 프로그래밍 방식으로 출력 합니다. 

hello SendGrid 바인딩은 hello를 다음과 같은 속성을 지원 합니다.

- `name`: 필수-hello 요청 또는 요청 본문에 대 한 함수 코드에서 사용 하는 hello 변수 이름입니다. 반환 값이 하나만 있는 경우 이 값은 ```$return```입니다. 
- `type`: 필수-설정 해야 너무 "sendGrid."
- `direction`: 필수-"out" 너무 설정 해야
- `apiKey`: 필수-hello 함수 응용 프로그램의 응용 프로그램 설정에 저장 된 사용자의 API 키의 집합 toohello 이름 이어야 합니다.
- `to`: hello 받는 사람의 전자 메일 주소입니다.
- `from`: hello 보낸 사람의 전자 메일 주소입니다.
- `subject`: hello 전자 메일의 hello 제목입니다.
- `text`: 전자 메일 콘텐츠 hello 합니다.

**function.json**의 예제는 다음과 같습니다.

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
> Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다. 이 작업은 사용자의 중요한 정보를 보호합니다.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>SendGrid hello의 C# 예제에서는 출력 바인딩

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Hello의 노드가 예 SendGrid 출력 바인딩

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

## <a name="next-steps"></a>다음 단계
Azure Functions에 대한 다른 바인딩 및 트리거에 대한 정보는 다음을 참조하세요. 
- [Azure Functions 트리거 및 바인딩 개발자 참조](functions-triggers-bindings.md)

- [Azure 기능에 대 한 유용한](functions-best-practices.md) Azure 함수를 만들 때 몇 가지 모범 사례 toouse를 나열 합니다.

- [Azure Functions 개발자 참조](functions-reference.md) 함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.
