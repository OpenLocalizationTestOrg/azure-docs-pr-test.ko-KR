---
title: "aaaHow toouse Azure 함수에서 SendGrid | Microsoft Docs"
description: "표시 방법을 toouse Azure 함수에서 SendGrid"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>어떻게 toouse Azure 함수에서 SendGrid

## <a name="sendgrid-overview"></a>SendGrid 개요

Azure 기능 지원 SendGrid 바인딩 tooenable 몇 줄만 코드 및 SendGrid 계정을 함수 toosend 전자 메일 메시지를 출력합니다.

Azure 함수에 hello SendGrid API toouse 있어야는 [SendGrid 계정을](http://SendGrid.com)합니다. 또한 SendGrid API 키가 있어야 합니다. Tooyour SendGrid 계정에에서 로그인 하 고 클릭 **설정** 다음 **API 키** toogenerate API 키입니다. 이후 단계에서 사용되므로 이 키를 사용 가능한 상태로 유지합니다.

준비 toocreate Azure 함수 응용 프로그램입니다.

## <a name="create-an-azure-function-app"></a>Azure Function 앱 만들기 

Azure Function Appls는 하나 이상의 Azure Functions에 대한 컨테이너입니다. Azure Functions는 함수일 뿐입니다. 각 Azure 함수는 동률된 tooone 트리거 hello 함수 toorun 발생 하는 이벤트입니다.
각 함수는 임의 개수의 입력 또는 출력 바인딩을 포함할 수 있습니다. 바인딩은 함수에서 사용할 수 있는 서비스입니다. SendGrid 바인딩의 경우 출력 toosend 전자 메일을 사용할 수입니다. 

1. Toohello Azure 포털에에서 로그인 하 고 [Azure 함수 응용 프로그램을 만들](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) 하거나 기존 함수 앱을 엽니다. 
2. Azure Function을 만듭니다. 수동 트리거 및 C#을 선택 하기 간단 하며 tookeep 

 ![Azure Function 만들기](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Azure Function 앱에서 사용할 SendGrid 구성

응용 프로그램 설정 toouse로 SendGrid API 키를 저장 해야 하는 함수에서. hello ApiKey 필드 실제 SendGrid API 키에는 없지만 실제 API 키를 나타내는 설정 하는 응용 프로그램 정의. 이러한 방식으로 키를 저장하면 소스 코드 제어에 체크인될 수 있는 코드 또는 파일에서 분리되므로 보안에 도움이 됩니다.

- 함수 앱의 **응용 프로그램 설정**에서 **AppSettings**를 만듭니다.

 ![Azure Function 만들기](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>SendGrid 출력 바인딩 구성

SendGrid는 Azure Function 출력 바인딩으로 사용할 수 있습니다. SendGrid toocreate 출력 바인딩:

1. Toohello 이동 **통합** hello Azure 포털의에서 hello 함수 탭 합니다.
2. 클릭 **새 출력** toocreate는 SendGrid 출력 바인딩이 있습니다.
3. Hello 입력 **API 키** 및 **메시지 매개 변수 이름** 속성입니다. 입력할 수 있는 다른 속성을 이제 hello 또는 대신 코드를 작성할 합니다. 이러한 설정은 기본값으로 사용할 수 있습니다.

 ![SendGrid 출력 바인딩 구성](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

라는 파일을 만들어 바인딩 tooa 함수 추가 **function.json** 함수의 폴더에 있습니다. 이 파일에 포함 되어 모든 동일한 정보에서에서 볼 수 있는 hello Azure 함수 hello **통합** , 탭이 포함 되지만 Json의 서식을 지정 합니다. 설정 hello **ApiKey**, **메시지**, 및 **에서** 필드 만들기 hello에 항목을 다음 hello **function.json** 파일: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

원할 경우 이 파일을 직접 수정할 수 있습니다.

생성 하 고 hello 함수 응용 프로그램 및 기능을 구성 했으므로 전자 메일 hello 코드 toosend를 작성할 수 있습니다.

## <a name="write-code-that-creates-and-sends-email"></a>전자 메일을 만들어 보내는 코드 작성

모든 hello SendGrid API 포함 hello 명령을 toocreate 필요 하 고 전자 메일을 보냅니다.  

- 코드 다음 hello로 hello 함수에서 hello 코드를 바꿉니다.

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

공지 hello에 대 한 첫 번째 줄 포함 hello ```#r``` hello SendGrid 어셈블리를 참조 하는 지시문입니다. 그 후 사용할 수 있습니다는 ```using``` 문을 toomore 쉽게 해당 네임 스페이스의 hello 개체에 액세스 합니다. Hello 코드에서의 인스턴스를 만들 ```Mail```, ```Personalization```, 및 ```Content``` hello SendGrid API에서에서 hello 전자 메일을 구성 하는 개체입니다. Hello 메시지를 반환 하는 경우 SendGrid로 전달 합니다. 

hello 함수의 서명이 포함 out 형식 매개 변수는 추가 ```Mail``` 라는 ```message```합니다. 입력 및 출력 바인딩 모두 코드에서 함수 매개 변수를 나타냅니다. 

2. 클릭 하 여 코드 테스트 **테스트** hello에 메시지를 입력 하 고 **요청 본문** 필드 hello를 클릭 한 후 **실행** 단추입니다.

 ![코드 테스트](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. 전자 메일 tooverify를 SendGrid hello 전자 메일을 보내고 있는지 확인 하십시오. 1 단계에서 toohello 주소 hello 코드를 이동 하 고 hello에서 hello 메시지 포함 **요청 본문**합니다.

## <a name="next-steps"></a>다음 단계
이 문서 toouse SendGrid 서비스 toocreate hello 및 전자 메일을 보내는 방법을 제시 합니다. 응용 프로그램에서 Azure 함수 사용에 대 한 더 toolearn hello 다음 항목을 참조 하십시오. 

- [Azure 기능에 대 한 유용한](functions-best-practices.md) Azure 함수를 만들 때 몇 가지 모범 사례 toouse를 나열 합니다.

- [Azure Functions 개발자 참조](functions-reference.md) 함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.

- [Azure Functions 테스트](functions-test-a-function.md) 함수를 테스트하는 다양한 도구와 기법을 설명합니다.