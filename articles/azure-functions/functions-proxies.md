---
title: "Azure 함수에서 프록시와 aaaWork | Microsoft Docs"
description: "방법의 개요 toouse Azure 함수 프록시"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Azure Functions 프록시 사용(미리 보기)

> [!NOTE] 
> Azure Functions 프록시는 현재 미리 보기 상태입니다. 대금 청구 미리 보기, 하지만 표준 함수 tooproxy 실행을 적용 하는 동안 무료입니다. 자세한 내용은 [Azure Functions 가격 책정](https://azure.microsoft.com/pricing/details/functions/)을 참조하세요.

이 문서에서는 설명 어떻게 tooconfigure Azure 함수 프록시와 작동 합니다. 이 기능을 사용하면 다른 리소스에서 구현된 함수 앱에 끝점을 지정할 수 있습니다. 여전히 클라이언트에 대 한 단일 API 화면을 표시 하는 동안 여러 기능 앱 (예: 마이크로 서비스 아키텍처의 경우)에 이러한 프록시 toobreak 큰 API를 사용할 수 있습니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Azure Functions 프록시 사용

프록시는 기본적으로 사용하도록 설정되어 있지 않습니다. Hello 기능을 해제 하지만 실행 되지 것입니다 프록시를 만들 수 있습니다. tooenable 프록시 뒤 hello지 않습니다.

1. 열기 hello [Azure 포털], tooyour 함수 응용 프로그램을 이동 합니다.
2. **함수 앱 설정**을 선택합니다.
3. 스위치 **사용 Azure 함수 프록시 (미리 보기)** 너무**에**합니다.

또한 변수로 반환할 수 있습니다 여기 tooupdate hello 프록시 런타임 새 기능을 사용할 수 있게 합니다.


## <a name="create"></a>프록시 만들기

이 섹션에서는 a에서 프록시 toocreate 함수 포털 hello 하는 방법을 보여 줍니다.

1. 열기 hello [Azure 포털], tooyour 함수 응용 프로그램을 이동 합니다.
2. Hello 왼쪽된 창에서 선택 **새 프록시**합니다.
3. 프록시의 이름을 제공합니다.
4. Hello를 지정 하 여이 함수 응용 프로그램에 노출 되는 hello 끝점을 구성 **경로 템플릿을** 및 **HTTP 메서드**합니다. 이러한 매개 변수 동작에 대 한 따라 toohello 규칙 [HTTP 트리거]합니다.
5. 집합 hello **백 엔드 URL** tooanother 끝점입니다. 이러한 끝점은 다른 함수 앱의 함수이거나 다른 API일 수 있습니다. hello 값 필요 toobe 정적이 고 참조할 수 있는 [응용 프로그램 설정] 및 [hello 원래 클라이언트 요청에서 매개 변수]합니다.
6. **만들기**를 클릭합니다.

이제 프록시는 함수 앱에서 새 끝점으로 존재합니다. 클라이언트 관점에서 해당 tooan Azure 함수에서 HttpTrigger 것합니다. Hello 프록시 URL을 복사 하 고 자주 사용 하 여 HTTP 클라이언트를 테스트 하 여 새 프록시를 시도할 수 있습니다.

## <a name="modify-requests-responses"></a>요청 및 응답 수정

Azure 함수 프록시와 hello 백 엔드에서 요청 tooand 응답을 수정할 수 있습니다. 이러한 변환은 [변수 사용]에 정의된 대로 변수를 사용할 수 있습니다.

### <a name="modify-backend-request"></a>Hello 백 엔드에서 요청을 수정

기본적으로 hello 백 엔드에서 요청 hello 원래 요청 항목의 복사본으로 초기화 됩니다. 또한 toosetting hello 백 엔드 URL 변경 toohello HTTP 메서드, 헤더 및 쿼리 문자열 매개 변수를 만들 수 있습니다. hello 수정된 값 참조할 수 [응용 프로그램 설정] 및 [hello 원래 클라이언트 요청에서 매개 변수]합니다.

현재 백 엔드 요청을 수정하기 위한 포털 환경은 없습니다. toolearn tooapply proxies.json에서이 기능 확인 하려면 어떻게 해야 [requestOverrides 개체 정의]합니다.

### <a name="modify-response"></a>Hello 응답 수정

기본적으로 hello 클라이언트 응답 hello 백 엔드 응답의 복사본으로 초기화 됩니다. 변경 내용 toohello 응답 상태 코드, 이유 구문, 헤더 및 본문을 만들 수 있습니다. hello 수정된 값 참조할 수 [응용 프로그램 설정], [hello 원래 클라이언트 요청에서 매개 변수], 및 [hello 백 엔드 응답에서 매개 변수]합니다.

현재 응답을 수정하기 위한 포털 환경은 없습니다. toolearn tooapply proxies.json에서이 기능 확인 하려면 어떻게 해야 [responseOverrides 개체 정의]합니다.

## <a name="using-variables"></a>변수 사용

작업에 대 한 hello 구성 하지 않아도 toobe 정적입니다. Hello 원래 요청, hello 백 엔드 응답 또는 응용 프로그램 설정에서 toouse 변수 조건 수 있습니다.

### <a name="request-parameters"></a>요청 매개 변수 참조

Toohello 백 엔드 URL 속성을 입력으로 또는 수정 요청 및 응답의 일부로 요청 매개 변수를 사용할 수 있습니다. Hello 기본 프록시 구성에 지정 된 hello 경로 서식 파일에서 일부 매개 변수에 바인딩할 수 있으며 다른 hello 들어오는 요청의 속성에서 가져올 수 있습니다.

#### <a name="route-template-parameters"></a>경로 템플릿 매개 변수
Hello 경로 템플릿을에 사용 되는 매개 변수 이름으로 참조 되는 사용 가능한 toobe 됩니다. hello 매개 변수 이름은 중괄호 ({})에 포함 됩니다.

예를 들어, 프록시에는 경로 템플릿을 같은 경우 `/pets/{petId}`, hello 백 엔드 URL의 hello 값을 포함할 수 있습니다 `{petId}`에서 같이 `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`합니다. Hello 경로 템플릿을에 와일드 카드와 같은 종료 `/api/{*restOfPath}`, 값 hello `{restOfPath}` hello 남은 hello 들어오는 요청에서 경로 세그먼트의 문자열 표현입니다.

#### <a name="additional-request-parameters"></a>추가 요청 매개 변수
또한 toohello 라우팅할 템플릿 매개 변수, 다음 값에는 hello 구성 값에 사용할 수 있습니다.

* **{request.method}** : hello hello 원래 요청에 사용 되는 HTTP 메서드입니다.
* **{request.headers 합니다. \<HeaderName\>}**: hello 원래 요청에서 읽을 수 있는 헤더입니다. 대체  *\<HeaderName\>*  tooread hello 헤더의 hello 이름으로 합니다. Hello 헤더 hello 요청에 포함 되어 있지 않으면, hello 값 hello 빈 문자열이 됩니다.
* **{request.querystring 합니다. \<ParameterName\>}**: hello 원래 요청에서 읽을 수 있는 쿼리 문자열 매개 변수입니다. 대체  *\<ParameterName\>*  hello tooread 원하는 hello 매개 변수 이름으로 합니다. Hello 매개 변수는 hello 요청에 포함 되어 있지 않으면, hello 값 hello 빈 문자열이 됩니다.

### <a name="response-parameters"></a>백 엔드 응답 매개 변수 참조

응답 매개 변수 수정 hello 응답 toohello 클라이언트의 일부로 사용할 수 있습니다. 다음 값에는 hello 구성 값에 사용할 수 있습니다.

* **{backend.response.statusCode}** : hello hello 백 엔드 응답에 반환 되는 HTTP 상태 코드입니다.
* **{backend.response.statusReason}** : hello 백 엔드 응답에 반환 되는 HTTP hello 이유 구문입니다.
* **{backend.response.headers 합니다. \<HeaderName\>}**: hello 백 엔드 응답에서 읽을 수 있는 헤더입니다. 대체  *\<HeaderName\>*  tooread hello 헤더의 hello 이름으로 원하는 합니다. Hello 헤더 hello 요청에 포함 되어 있지 않으면, hello 값 hello 빈 문자열이 됩니다.

### <a name="use-appsettings"></a>응용 프로그램 설정 참조

참조할 수도 있습니다 [hello 함수 앱에 대해 정의 된 응용 프로그램 설정](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) hello 설정 이름은 백분율 기호 (%)로 묶어 합니다.

백 엔드 URL 예를 들어 *https://%ORDER_PROCESSING_HOST%/api/orders* "% ORDER_PROCESSING_HOST %" hello hello ORDER_PROCESSING_HOST 설정 값으로 대체 해야 합니다.

> [!TIP] 
> 배포 또는 테스트 환경이 여러 개 있는 경우 백 엔드 호스트에 대해 응용 프로그램 설정을 사용하세요. 이렇게 할 수 있습니다는 항상 통신의 대상이 해당 환경에 대 한 다시 toohello 종료 합니다.

## <a name="advanced-configuration"></a>고급 구성

구성 하는 hello 프록시 함수 응용 프로그램 디렉터리의 hello 루트에 있는 proxies.json 파일에 저장 됩니다. 수동으로이 파일을 편집 하 고 hello 중 하나를 사용 하는 경우 응용 프로그램의 일부분으로 배포할 수 [배포 방법](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) 함수를 지 원하는 합니다. hello 기능 이어야 합니다 [활성화](#enable) hello 파일 toobe 처리에 대 한 합니다. 

> [!TIP] 
> Hello 배포 방법 중 하나를 설정 하지 않은 경우 있습니다 작업할 수도 hello 포털에서 hello proxies.json 파일입니다. 선택 이동 tooyour 함수 앱 **플랫폼 기능**를 선택한 후 **응용 프로그램 서비스 편집기**합니다. 이렇게 함으로써 함수 응용 프로그램의 hello 전체 파일 구조를 볼 수 있으며 다음 변경 합니다.

Proxies.json은 명명된 프록시 및 해당 정의로 구성된 프록시 개체로 정의됩니다. 편집기에서 코드 완성을 지원하는 경우 필요에 따라 [JSON 스키마](http://json.schemastore.org/proxies)를 참조할 수 있습니다. 파일의 예는 hello 다음과 같을 수 있습니다.

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

각 프록시는 이름와 같은 *proxy1* hello 예제 앞에 있습니다. 프록시 정의 개체를 해당 하는 hello hello 다음과 같은 속성으로 정의 됩니다.

* **matchCondition**: 필요 합니다--이 프록시의 hello 실행을 트리거하는 hello 요청을 정의 하는 개체입니다. [HTTP 트리거]와 공유되는 두 가지 속성이 포함되어 있습니다.
    * _메서드_: 프록시 hello hello HTTP 메서드 배열을에 응답 합니다. 지정 하지 않으면 hello 프록시 hello 경로에 tooall HTTP 메서드에 응답 합니다.
    * _경로_: 필수-hello 경로 템플릿, Url 프록시 요청 제어 정의에 응답 합니다. HTTP 트리거와 달리 기본값이 없습니다.
* **backendUri**: hello 백 엔드 리소스 toowhich hello 요청의 hello URL 프록시 수 있어야 합니다. 이 값 hello 원래 클라이언트 요청에서 응용 프로그램 설정 및 매개 변수를 참조할 수 있습니다. 이 속성을 포함하지 않으면 Azure Functions는 HTTP 200 OK로 응답합니다.
* **requestOverrides**: 변환 toohello 백 엔드에서 요청을 정의 하는 개체입니다. [requestOverrides 개체 정의]를 참조하세요.
* **responseOverrides**: 변환 toohello 클라이언트 응답을 정의 하는 개체입니다. [responseOverrides 개체 정의]를 참조하세요.

> [!NOTE] 
> hello 경로 속성 Azure 함수 프록시 hello 함수 호스트 구성의 hello routePrefix 속성을 준수 하지 않습니다. Tooinclude /api 같은 접두사를 사용 하도록 하려는 경우에 hello 경로 속성에 포함 되어야 합니다.

### <a name="requestOverrides"></a>requestOverrides 개체 정의

hello requestOverrides 개체 정의 toohello 요청 될 때 변경 hello 백 엔드 리소스 라고 합니다. hello 개체 hello 다음과 같은 속성으로 정의 됩니다.

* **backend.request.method**: hello toocall hello 백 엔드를 사용 하는 HTTP 메서드입니다.
* **backend.request.querystring 합니다. \<ParameterName\>**: hello 호출 toohello 백 엔드에 설정 될 수 있는 쿼리 문자열 매개 변수입니다. 대체  *\<ParameterName\>*  hello tooset 원하는 hello 매개 변수 이름으로 합니다. Hello 빈 문자열이 지정 된 hello 매개 변수는 hello 백 엔드에서 요청에 포함 되지 않습니다.
* **backend.request.headers 합니다. \<HeaderName\>**: hello 호출 toohello 백 엔드에 설정 될 수 있는 헤더입니다. 대체  *\<HeaderName\>*  tooset hello 헤더의 hello 이름으로 합니다. Hello 빈 문자열을 제공 하는 경우 hello 헤더 hello 백 엔드에서 요청에 포함 되지 않습니다.

값은 hello 원래 클라이언트 요청에서 응용 프로그램 설정 및 매개 변수를 참조할 수 있습니다.

예제 구성 hello 다음과 같을 수 있습니다.

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>responseOverrides 개체 정의

hello requestOverrides 개체 정의 뒤로 toohello 클라이언트 통과 toohello 응답 적용 된 변경 합니다. hello 개체 hello 다음과 같은 속성으로 정의 됩니다.

* **response.statusCode**: hello HTTP 상태 코드 toobe toohello 클라이언트를 반환 합니다.
* **response.statusReason**: hello HTTP 이유 구 toobe toohello 클라이언트를 반환 합니다.
* **response.body**: hello 본문 toobe의 문자열 표현을 hello toohello 클라이언트를 반환 합니다.
* **response.headers 합니다. \<HeaderName\>**: hello 응답 toohello 클라이언트에 대해 설정할 수 있는 헤더입니다. 대체  *\<HeaderName\>*  tooset hello 헤더의 hello 이름으로 합니다. Hello 빈 문자열을 제공 하는 경우 hello 헤더 hello 응답에 포함 되지 않습니다.

값은 hello 백 엔드 응답에서 응용 프로그램 설정, hello 원래 클라이언트 요청에서 매개 변수 및 매개 변수를 참조할 수 있습니다.

예제 구성 hello 다음과 같을 수 있습니다.

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> 이 예제에서는 hello 본문 설정 되어 직접 하므로 아니요 `backendUri` 속성이 필요 합니다. hello 예제 모의 Api에 대 한 Azure 기능 프록시를 사용 하는 방법을 보여 줍니다.

[Azure 포털]: https://portal.azure.com
[HTTP 트리거]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[requestOverrides 개체 정의]: #requestOverrides
[responseOverrides 개체 정의]: #responseOverrides
[응용 프로그램 설정]: #use-appsettings
[변수 사용]: #using-variables
[hello 원래 클라이언트 요청에서 매개 변수]: #request-parameters
[hello 백 엔드 응답에서 매개 변수]: #response-parameters
