---
title: "Azure 기능을 사용 하 여 Azure 논리 앱에 대 한 코드 aaaCustom | Microsoft Docs"
description: "Azure Functions를 사용하여 Azure Logic Apps에 대한 사용자 지정 코드 만들기 및 실행"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Azure Functions를 통해 Logic Apps에 대한 사용자 지정 코드 추가 및 실행

C# 또는 논리 앱에서 node.js의 사용자 지정 코드 조각을 toorun Azure 기능을 통해 사용자 지정 함수를 만들 수 있습니다. 
[Azure Functions](../azure-functions/functions-overview.md)는 Microsoft Azure에서 서버 없는 계산을 제공하고 다음과 같은 태스크를 수행하는 데 유용합니다.

* 고급 서식 지정 또는 논리 앱에서 필드 계산
* 워크플로에서 계산을 수행합니다.
* C# 또는 node.js에서 지원 되는 함수로 hello 논리 앱 기능을 확장

## <a name="create-custom-functions-for-your-logic-apps"></a>Logic Apps에 대한 사용자 지정 함수 만들기

Hello에서 hello 함수 Azure 포털에는 함수를 만드는 것이 좋습니다 **제네릭 Webhook-노드** 또는 **제네릭 Webhook-C#** 템플릿. hello 결과 자동으로 채워진 서식 파일을 만들고 허용 `application/json` 논리 앱에서 합니다. 이러한 서식 파일에서 만든 함수는 자동으로 검색 및 논리 응용 프로그램 디자이너에서 hello에 표시 **내 영역에서 Azure 함수입니다.**

Hello hello에 Azure 포털에서에서 **통합** 창 함수에 대 한 서식 파일에 표시할지를 **모드** 도**Webhook** 및 **Webhook유형** 너무 설정**일반 JSON**합니다. 

Webhook 함수 요청을 수락 및 통해 hello 메서드에 전달 된 `data` 변수입니다. 와 같은 점 표기법을 사용 하 여 페이로드 hello 속성에 액세스할 수 있습니다 `data.function-name`합니다. 예를 들어 날짜 문자열에는 DateTime 값으로 변환 하는 간단한 JavaScript 함수를 다음 예제는 hello 같습니다.

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>논리 앱에서 Azure Functions 호출

해당 구독 및 toocall 논리가 응용 프로그램 디자이너에서 선택 hello 함수 toolist hello 컨테이너 클릭 hello **작업** 메뉴에서을 선택에서 **내 영역에서 Azure 함수**합니다.

Hello 함수를 선택 하 고 나면 됩니다 toospecify 입력된 페이로드 개체를 요청 합니다. 이 개체는 hello 메시지를 논리 앱 보냅니다 toohello 함수 hello를 JSON 개체 여야 합니다. 예를 들어 hello에 toopass 원하는 **마지막으로 수정한 날짜** 날짜는 Salesforce 트리거에서 hello 함수 페이로드가이 예제와 같습니다.

![마지막으로 수정한 날짜][1]

## <a name="trigger-logic-apps-from-a-function"></a>함수에서 논리 앱 트리거

함수 내에서 논리 앱을 트리거할 수 있습니다. [호출 가능 끝점인 논리 앱](logic-apps-http-endpoint.md)을 참조하세요. 수동 트리거가 있는 논리 앱을 만드는 다음에서 내부 함수를 생성 toohello 논리 앱을 전송 하는 것이 원하는 hello 페이로드를 사용한 HTTP POST toohello 수동 트리거 URL입니다.

### <a name="create-a-function-from-logic-app-designer"></a>Logic App Designer에서 함수 만들기

Node.js webhook 함수 hello 디자이너에서 만들 수도 있습니다. 먼저 **내 영역의 Azure Functions** 를 선택하고 함수에 대한 컨테이너를 선택합니다. Hello에서 toocreate 하나 컨테이너를 아직 없는 경우 해야 [Azure 함수 포털](https://functions.azure.com/signin)합니다. 그런 다음 **새로 만들기**를 선택합니다.  

toogenerate toocompute, hello 데이터를 기반으로 템플릿의 함수로 toopass를 계획 하는 hello 컨텍스트 개체를 지정 합니다. 이 개체는 JSON 개체여야 합니다. 예를 들어 hello 파일 내용에서 FTP 작업에서 전달 하는 경우 hello 컨텍스트 페이로드가이 예제와 같습니다.

![상황에 맞는 페이로드][2]

> [!NOTE]
> 이 개체를 문자열로 캐스팅 되지 않은, toohello JSON 페이로드 hello 콘텐츠 직접 추가 됩니다. 그러나 hello 개체 JSON 토큰 (즉, 문자열 또는 JSON 개체/배열은) 없는 경우 오류가 발생 합니다. toocast hello 개체를 문자열로 hello이 문서의 첫 번째 그림에 나와 있는 것 처럼 따옴표를 추가 합니다.
> 

hello 디자이너에는 다음 인라인을 만들 수는 함수 템플릿을 생성 합니다. 변수 미리 hello 함수로 toopass를 계획 하는 hello 상황에 따라 생성 됩니다.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
