---
title: "Azure 함수를 사용 하는 서버가 없는 API aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure 함수를 사용 하는 서버가 없는 API"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Azure Functions를 사용하여 서버 없는 API 만들기

이 자습서에 설명 합니다 방법을 Azure 함수 사용 하면 toobuild 고도로 확장 가능한 Api입니다. Azure 함수는 다양 한 언어로, Node.JS, C# 등을 포함 하 여 끝점의 기본 제공 HTTP 트리거 및 쉽게 tooauthor 하도록 하는 바인딩 컬렉션 함께 제공 됩니다. 이 자습서에서는 API 디자인에 HTTP 트리거 toohandle 특정 작업을 사용자 지정 하면 합니다. 또한 Azure Functions 프록시와 통합하고 모의 API를 설정하여 API를 확장할 준비를 진행합니다. 이 모든는 리소스 확장에 대 한 tooworry 없는-API 논리에만 집중할 수 있도록 hello 함수 서버가 없는 계산 환경을 기반으로 수행 됩니다.

## <a name="prerequisites"></a>필수 조건 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

이 자습서의 나머지 부분 hello에 대 한 hello 결과 함수가 사용 됩니다.

### <a name="sign-in-tooazure"></a>TooAzure에 로그인

Azure 포털 hello를 엽니다. toodo이 너무 로그인[https://portal.azure.com](https://portal.azure.com) Azure 계정.

## <a name="customize-your-http-function"></a>HTTP 함수 사용자 지정

기본적으로 HTTP 트리거 함수는 구성 된 tooaccept 모든 HTTP 메서드입니다. Hello 폼의 기본 URL은 또한 `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`합니다. 다음 hello 퀵 스타트를 따른 경우 `<funcname>` "HttpTriggerJS1" 같은 내용이 보일 것입니다. 이 섹션에서는 hello에 대 한 함수 toorespond만 tooGET 요청을 수정 합니다 `/api/hello` 대신 라우팅합니다. 

Hello Azure 포털에서에서 tooyour 함수를 이동 합니다. 선택 **통합** 왼쪽 탐색 hello에 있습니다.

![HTTP 함수 사용자 지정](./media/functions-create-serverless-api/customizing-http.png)

Hello 테이블에 지정 된 HTTP 트리거 설정을 사용 합니다.

| 필드 | 샘플 값 | 설명 |
|---|---|---|
| 허용된 HTTP 메서드 | 선택된 메서드 | HTTP 메서드를 사용 하는 tooinvoke 수 판단한이 함수 |
| 선택한 HTTP 메서드 | GET | 통해 선택 된 HTTP 메서드 toobe만 tooinvoke를이 함수 사용 |
| 경로 템플릿 | /hello | 경로 사용 되는 tooinvoke 결정이 함수 |

Hello 포함 되지 않은 `/api` 이 전역 설정에 의해 처리 되므로 hello 경로 서식 파일의 경로 접두사를 기반 합니다.

**Save**를 클릭합니다.

[Azure Functions HTTP 및 웹후크 바인딩](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint)에서 HTTP 함수 사용자 지정에 대해 자세히 알아보세요.

### <a name="test-your-api"></a>API 테스트

다음으로 테스트 함수 toosee hello 새 API 화면을 사용 합니다.

왼쪽 탐색 hello에 hello 함수 이름을 클릭 하 여 뒤로 toohello 개발 페이지를 이동 합니다.

클릭 **함수 URL을 가져올** hello URL을 복사 합니다. Hello를 사용 하도록 표시 되어야 `/api/hello` 이제 라우팅합니다.

새 브라우저 탭 또는 기본 REST 클라이언트 hello URL을 복사 합니다. 브라우저는 기본적으로 GET을 사용합니다.

Hello 함수를 실행 하 고 작동 하는지 확인 합니다. 쿼리 문자열 toosatisfy hello 빠른 시작 코드와 tooprovide hello "name" 매개 변수를 할 수 있습니다.

다른 HTTP 메서드에 tooconfirm hello 함수 실행 되지 않도록 있는 hello 끝점 호출을 시도할 수 있습니다. 이 경우 toouse cURL, 우체부, 또는 Fiddler와 같은 REST 클라이언트에 필요 합니다.

## <a name="proxies-overview"></a>프록시 개요

Hello 다음 섹션에서 프록시를 통해 API를 노출할 합니다. Azure 함수 프록시는 tooforward 요청 tooother 리소스 수 있는 미리 보기 기능입니다. HTTP 트리거가 있는 것과 마찬가지로 HTTP 끝점을 정의 하지만 URL tooa 원격 구현으로 지정 하면 해당 끝점에서 호출 될 때 코드 tooexecute를 작성 하는 대신 합니다. 이렇게 하면 클라이언트 tooconsume에 대 한 쉬운 단일 API 화면에 여러 API 원본 toocompose 있습니다. Toobuild microservices로 API를 하려는 경우 특히 유용 합니다.

프록시는와 같은 tooany HTTP 리소스를 가리킬 수 있습니다.
- Azure 기능 
- [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)의 API 앱
- [Linux의 App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)에 있는 Docker 컨테이너
- 기타 호스트된 API

프록시에 대해 자세히 toolearn 참조 [Azure 함수 프록시 (미리 보기) 작업]합니다.

## <a name="create-your-first-proxy"></a>첫 번째 프록시 만들기

이 섹션에서는 새 프록시 사용으로 만들어 프런트 엔드 tooyour 전체 API입니다. 

### <a name="setting-up-hello-frontend-environment"></a>Hello 프런트 엔드 환경 설정

 ° ט hello 너무[함수 앱 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate 새 함수 응용 프로그램 프록시 만들 됩니다. 이 새 응용 프로그램 역할을 수행 hello 프런트 엔드 우리의 API에 대 한 하며 이전에 편집 중이 던 hello 함수 앱 백 엔드 역할을 수행 합니다.

Tooyour 새 프런트 엔드 함수 앱 hello 포털에서 이동 합니다.

**설정**을 선택합니다. 다음 설정/해제 **사용 Azure 함수 프록시 (미리 보기)** 너무 "On"입니다.

**플랫폼 설정**을 선택하고 **응용 프로그램 설정**을 선택합니다.

너무 아래로 스크롤하여**앱 설정** "HELLO_HOST" 키를 가진 새 설정을 만들어야 합니다. 와 같은 백 엔드 함수 응용 프로그램의 해당 값 toohello 호스트 설정 `<YourApp>.azurewebsites.net`합니다. HTTP 기능을 테스트할 때 앞에서 복사한 hello URL의 일부입니다. Hello 구성 나중에이 설정을 참조할 수 있습니다.

> [!NOTE] 
> 응용 프로그램 설정은 hello 프록시에 대 한 환경 하드 코드 된 종속성 hello 호스트 구성 tooprevent에 권장 됩니다. 응용 프로그램 설정을 사용 하 여 있음을 나타내고 hello 프록시 구성을 환경 간에 이동할 수 hello 환경 관련 응용 프로그램 설정이 적용 됩니다.

**Save**를 클릭합니다.

### <a name="creating-a-proxy-on-hello-frontend"></a>Hello 프런트 엔드에는 프록시를 만들고

Hello 포털에서 뒤로 tooyour 프런트 엔드 함수 응용 프로그램을 이동 합니다.

Hello 왼쪽 탐색 hello '+' 다음 더하기 기호를 너무 클릭 "프록시 (미리 보기)"입니다.

![프록시 만들기](./media/functions-create-serverless-api/creating-proxy.png)

Hello 테이블에 지정 된 프록시 설정을 사용 합니다.

| 필드 | 샘플 값 | 설명 |
|---|---|---|
| 이름 | HelloProxy | 관리에 대해서만 사용되는 이름 |
| 경로 템플릿 | /api/hello | 경로 사용 되는 tooinvoke 결정이 프록시 |
| 백 엔드 URL | https://%HELLO_HOST%/api/hello | Hello 끝점 toowhich hello 요청 프록시 되어야 지정 |

프록시 hello를 제공 하지 않는 `/api` 기본 경로 접두사와 hello 경로 템플릿을에 포함 해야이 합니다.

hello `%HELLO_HOST%` 구문 앞에서 만든 hello 응용 프로그램 설정을 참조 합니다. hello 확인 URL은 tooyour 원래 함수를 가리킵니다.

**만들기**를 클릭합니다.

새 프록시 hello 프록시 URL을 복사 하 고 테스트 hello 브라우저 또는에서 자주 사용 하 여 HTTP 클라이언트와 여 볼 수 있습니다.

## <a name="create-a-mock-api"></a>모의 API 만들기

다음으로, 솔루션에 대 한 프록시 toocreate 모의 API를 사용 합니다. 이렇게 하면 클라이언트 개발 tooprogress 완전히 구현 하는 hello 백 엔드 몰라도 됩니다. 개발의 뒷부분에 나오는이 논리를 지원 하는 새 함수 앱을 만들고 프록시 tooit 리디렉션할 수 있습니다.

toocreate이 API의 모의 알림, 새 프록시 hello를 사용 하 여이 시간 만듭니다 [응용 프로그램 서비스 편집기](https://github.com/projectkudu/kudu/wiki/App-Service-Editor)합니다. 시작 tooget hello 포털에서 tooyour 함수 응용 프로그램을 이동 합니다. **플랫폼 기능**을 선택하고 **App Service 편집기**를 찾습니다. 이 클릭 하면 새 탭에서 응용 프로그램 서비스 편집기 hello를 열립니다.

선택 `proxies.json` 왼쪽 탐색 hello에 있습니다. 모든 프록시에 대 한 hello 구성을 저장 하는 hello 파일입니다. Hello 중 하나를 사용 하는 경우 [배포 방법 함수](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment),이 hello 파일을 소스 제어에 유지 됩니다. 이 파일에 대해 자세히 toolearn 참조 [프록시 고급 구성](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration)합니다.

따랐다면 지금까지, 프로그램 proxies.json hello 다음과 같이 표시 됩니다.

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

다음으로 모의 API를 추가합니다. Proxies.json 파일을 hello 다음 코드로 바꿉니다.

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

이 새 프록시 "GetUserByName" hello backendUri 속성 없이 추가합니다. 다른 리소스를 호출 하는 대신 응답 재정의 사용 하 여 프록시에서 hello 기본 응답을 수정 합니다. 요청 및 응답 재정의를 백 엔드 URL과 함께 사용할 수도 있습니다. 프록싱 tooa 레거시 시스템 해야 toomodify 헤더, 쿼리 매개 변수, 등 toolearn 요청 및 응답 재정의 대 한 자세한를 참조 하는 경우 특히 유용 [요청과 응답을 프록시 수정](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses)합니다.

호출 hello 여 모의 API 테스트 `/api/users/{username}` 브라우저 또는 자주 사용 하 여 REST 클라이언트를 사용 하 여 끝점입니다. 수 있는지 tooreplace _{username}_ 사용자 이름을 나타내는 문자열 값을 사용 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 방법에 대해 배웠습니다 toobuild 및 Azure 기능에는 API를 사용자 지정 합니다. 또한 어떻게 toobring 여러 Api를 포함 하 여 mocks, 함께 통합된 API 화면으로 배웠습니다. 이러한 기술을 toobuild Api의 복잡성에 관계 없이 아웃을 사용할 수 있는데, 서버가 없는 hello에서 실행 하는 동안 모든 Azure 기능에서 제공 하는 모델을 계산 합니다.

hello 다음 참조 도움이 될 추가 API를 개발 하는 경우:

- [Azure Functions HTTP 및 웹후크 바인딩](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [Azure 함수 프록시 (미리 보기) 작업]
- [Azure Functions API 문서화(미리 보기)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Azure 함수 프록시 (미리 보기) 작업]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
