---
title: "Azure 논리 앱-HTTP 통해 모든 끝점과 aaaCommunicate | Microsoft Docs"
description: "HTTP를 통해 끝점과 통신할 수 있는 Logic Apps 만들기"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>HTTP 동작 hello로 시작

HTTP 동작 hello로 워크플로 확장 하 여 조직에 대 한 수 있으며 tooany 끝점 HTTP를 통해 통신할 수 있습니다.

다음을 수행할 수 있습니다.

* 관리하는 웹 사이트가 중단되면 활성화되는(트리거) 논리 앱 워크플로를 만듭니다.
* 통신할 끝점 tooany HTTP tooextend 워크플로 다른 서비스에 합니다.

tooget hello HTTP 작업을 사용 하 여 논리 앱에서 시작 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="use-hello-http-trigger"></a>Hello HTTP 트리거를 사용 하 여
트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다. [트리거에 대해 자세히 알아보세요.](connectors-overview.md)

다음은 시퀀스 tooset HTTP hello hello 논리가 응용 프로그램 디자이너에서에서 트리거하는 방법의 예입니다.

1. 논리 앱에 hello HTTP 트리거를 추가 합니다.
2. Toopoll hello HTTP 끝점에 대 한 hello 매개 변수를 입력 합니다.
3. 폴링 간격에 hello 되풀이 간격을 수정 합니다.

   각 검사 하는 동안 반환 되는 모든 콘텐츠로 hello 논리 앱 이제 발생 합니다.

   ![HTTP 트리거](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Hello HTTP 트리거 작동 방식

hello HTTP 트리거 되풀이 간격 호출 tooHTTP 끝점을 보냅니다. 기본적으로 300 보다 낮은 모든 HTTP 응답 코드는 논리 앱 toorun을 발생 합니다. toospecify hello 논리 앱 발생 시켜야 하는지 여부를는 hello 논리 앱 코드 보기에서 편집을 HTTP 호출 hello 후 확인 하는 조건을 추가할 수 있습니다. 다음은 상태 코드 보다 크면 또는 값이 너무 hello 반환 되 면 발생 하는 HTTP 트리거의 예`400`합니다.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Hello HTTP 트리거 매개 변수에 대 한 자세한 세부 정보는에서 사용할 수 있는 [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)합니다.

## <a name="use-hello-http-action"></a>Hello HTTP 작업을 사용 하 여

동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다. 
[작업에 대해 자세히 알아봅니다.](connectors-overview.md)

1. **다음 단계** > **동작 추가**를 선택합니다.
3. Hello 동작 검색 상자에 입력 **http** toolist hello HTTP 동작 합니다.
   
    ![Hello HTTP 작업을 선택](./media/connectors-native-http/using-action-1.png)

4. Hello HTTP 호출에 대 한 필수 매개 변수를 추가 합니다.
   
    ![전체 hello HTTP 동작](./media/connectors-native-http/using-action-2.png)

5. Hello 디자이너 도구 모음에서 클릭 **저장**합니다. 논리 앱을 저장 하 고 hello에 (활성화) 게시 동시 합니다.

## <a name="http-trigger"></a>HTTP 트리거
이 커넥터가 지 원하는 hello 트리거에 대 한 hello 세부 정보는 다음과 같습니다. HTTP 커넥터 hello에 하나의 트리거가 있습니다.

| 트리거 | 설명 |
| --- | --- |
| HTTP |HTTP 호출을 실행 하 고 hello 응답 콘텐츠를 반환 합니다. |

## <a name="http-action"></a>HTTP 동작
이 커넥터가 지 원하는 hello 동작에 대 한 hello 세부 정보는 다음과 같습니다. HTTP 커넥터 hello에 작업을 사용할 수 있습니다.

| 동작 | 설명 |
| --- | --- |
| HTTP |HTTP 호출을 실행 하 고 hello 응답 콘텐츠를 반환 합니다. |

## <a name="http-details"></a>HTTP 세부 정보
hello 다음 표에서 필요한 hello 및 hello 작업과 hello 동작을 사용 하 여 연관 된 hello 해당 하는 출력 정보에 대 한 선택적 입력된 필드.

#### <a name="http-request"></a>HTTP 요청
hello 다음은 아웃 바운드 HTTP 요청을 낮추는 hello 동작에 대 한 입력된 필드입니다.
*는 필수 필드임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| Method* |메서드 |hello HTTP 동사 toouse |
| URI* |uri |hello HTTP 요청에 대 한 hello URI |
| 헤더 |headers |HTTP 헤더 tooinclude의 JSON 개체 |
| body |body |hello HTTP 요청 본문 |
| 인증 |인증 |Hello에 대 한 세부 정보 [인증](#authentication) 섹션 |

<br>

#### <a name="output-details"></a>출력 세부 정보
hello 다음은 hello HTTP 응답에 대 한 정보를 출력 합니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| headers |object |응답 헤더 |
| 본문 |object |응답 개체 |
| 상태 코드 |int |HTTP 상태 코드 |

## <a name="authentication"></a>인증
hello 논리 앱 기능 toouse 서로 다른 유형의 HTTP 끝점에 대해 인증 있습니다. 이 인증을 사용 하 여 hello로 **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, 및  **[HTTP Webhook](connectors-native-webhook.md)**  커넥터입니다. hello 인증 유형만 구성할 수는:

* [기본 인증](#basic-authentication)
* [클라이언트 인증서 인증](#client-certificate-authentication)
* [Azure AD(Azure Active Directory) OAuth 인증](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>기본 인증

기본 인증을 위한 인증 개체를 다음 hello 필요 합니다.
*는 필수 필드임을 의미합니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| 형식* |type |인증 유형(기본 인증의 경우 `Basic` 이어야 함) |
| 사용자 이름* |username |사용자 이름 tooauthenticate |
| 암호* |암호 |암호 tooauthenticate |

> [!TIP]
> Toouse hello 정의에서 검색할 수 없는 암호 사용을 `securestring` 매개 변수 및 hello `@parameters()`  
>  [워크플로 정의 함수의](http://aka.ms/logicappdocs)합니다.

예:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>클라이언트 인증서 인증

hello 다음 인증 개체에 필요한 클라이언트 인증서 인증 합니다. *는 필수 필드임을 의미합니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| 형식* |type |인증 유형 hello (있어야 `ClientCertificate` SSL 클라이언트 인증서에 대 한) |
| PFX* |pfx |hello hello 개인 정보 교환 (PFX) 파일의 내용을 Base64 인코딩 |
| 암호* |암호 |hello 암호 tooaccess hello PFX 파일 |

> [!TIP]
> 사용할 수는 매개 변수는 hello 정의 hello 논리 앱을 저장 한 후에 읽을 수 없는 되지 않을 toouse는 `securestring` 매개 변수 및 hello `@parameters()`  
>  [워크플로 정의 함수의](http://aka.ms/logicappdocs)합니다.

예:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Azure AD OAuth 인증
Azure AD OAuth 인증을 위한 인증 개체를 다음 hello 필요 합니다. *는 필수 필드임을 의미합니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| 형식* |type |인증 유형 hello (있어야 `ActiveDirectoryOAuth` Azure AD OAuth 용) |
| 테넌트* |tenant |hello Azure AD 테 넌 트에 대 한 hello 테 넌 트 식별자 |
| 대상* |audience |권한 부여 toouse를 요청 하는 hello 리소스입니다. 예: `https://management.core.windows.net/` |
| 클라이언트 ID* |clientId |hello hello Azure AD 응용 프로그램에 대 한 클라이언트 식별자 |
| 암호* |secret |hello 토큰을 요청 하는 hello 클라이언트의 hello 암호 |

> [!TIP]
> 사용할 수는 `securestring` 매개 변수 및 hello `@parameters()` [워크플로 정의 함수의](http://aka.ms/logicappdocs) toouse 매개 변수를 저장 한 후 hello 정의에서 쉽게 읽을 수 없습니다.
> 
> 

예:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>다음 단계
이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다. 탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

