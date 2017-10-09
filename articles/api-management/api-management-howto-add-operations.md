---
title: "Azure API 관리에서 aaaHow tooadd operations tooan API | Microsoft Docs"
description: "자세한 내용은 방법 Azure API 관리에서 tooadd 작업 tooan API입니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>어떻게 Azure API 관리에서 tooadd 작업 tooan API
API 관리에서 API를 사용하려면 먼저 작업을 추가해야 합니다. 표시 방법 안내이 tooadd 및 API 관리에서 다양 한 유형의 작업 tooan API 구성 합니다.

## <a name="add-operation"> </a>작업 추가
작업 추가 되 고 hello 게시자 포털에서 tooan API를 구성 합니다. tooaccess 게시자 포털을 클릭 하 여 hello **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.

![게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

Select hello hello 게시자 포털 및 선택 hello의 API를 원하는 **작업** 탭 합니다. 

![작업][api-management-operations]

클릭 **Add 작업** tooadd 새 작업을 합니다. hello **새 작업** 표시 되 고 hello **서명** 탭이 기본적으로 선택 됩니다.

![작업 추가][api-management-add-operation]

Hello 지정 **HTTP 동사** hello 드롭 다운 목록에서 선택 하 여 합니다.

![HTTP 메서드][api-management-http-method]

<a name="url-template"></a>

하나 이상의 URL 경로 세그먼트 및 0 개 이상의 쿼리 문자열 매개 변수 구성 된 URL 조각에 입력 하 여 hello URL 템플릿을 정의 합니다. hello URL 템플릿, hello API의 기준 URL 추가 toohello 단일 HTTP 작업을 식별합니다. 여기에는 둥근 괄호로 식별되는 하나 이상의 명명된 변수 부분을 포함할 수 있습니다. 이러한 변수를 템플릿 매개 변수 라고 부분과 hello 요청이 hello API 관리 플랫폼에 의해 처리 되 면 hello 요청 URL에서 추출 된 값을 동적으로 할당 됩니다.

> hello URL 템플릿 와일드 카드 패턴을 포함할 수 있습니다. 예를 들어 지정 `/*` 은 앞으로 다시 해당 HTTP 메서드 toohello에 대 한 모든 요청 서비스를 종료 합니다.

![URL 템플릿][api-management-url-template]

<a name="rewrite-url-template"></a>

원하는 경우 지정 hello **URL 재작성 템플릿**합니다. 이 toouse hello 표준 URL 템플릿 프런트 엔드 hello에서 들어오는 요청을 처리 하기 위해, toohello에 따라 변환 된 URL 통해 hello 백 엔드를 호출 하는 동안 서식 파일을 다시 작성 해야 합니다. Hello 재작성 템플릿에서 hello URL 템플릿에서 템플릿 매개 변수를 사용 해야 합니다. hello 다음 예제 content-type 인코딩되어 hello 이전 예제에서 hello 웹 서비스에 대 한 경로 세그먼트 API hello URL 템플릿을 사용 하 여 API 관리 플랫폼 hello를 통해 게시 하는 hello에서 쿼리 매개 변수로 제공 될 수 있습니다.

![URL 템플릿 다시 쓰기][api-management-url-template-rewrite]

호출자에 게 toohello 작업 hello 형식을 사용 합니다 `/customers?customerid=ALFKI` 너무 매핑할 수는`/Customers('ALFKI')` hello 백 엔드 서비스를 호출할 때입니다.

**디스플레이** 이름 및 **설명** hello 작업에 대 한 설명을 제공 하 고 사용 되는 tooprovide 설명서 toohello 개발자 hello 개발자 포털에서이 API를 사용 하는 합니다.

![설명][api-management-description]

hello에 일반 텍스트 또는 HTML로 지정할 수 hello 작업 설명 **설명** 입력란.

## <a name="operation-caching"> </a>작업 캐싱
응답 캐시 낮추고 대역폭 소비 hello API 소비자의 체감 대기 시간이 줄어들고 hello HTTP 웹 서비스 구현에 감소 hello 부하 hello API. 

tooeasily 신속 하 게 선택 hello hello 작업용 캐싱을 사용 하도록 설정 하 고 **캐싱** 탭 하 고 hello 확인 **사용** 확인란을 선택 합니다.

![구성][api-management-caching-tab]

**기간** hello 작업 응답 hello 캐시에 남아 있는 hello 하는 동안 시간을 지정 합니다. hello 기본값은 3600 초 또는 1 시간입니다.

캐시 키에는 응답에 걸리는 toodifferentiate를 사용 하는 이므로 tooeach 다양 한 캐시 키에 해당 하는 hello 응답 자체 별도 캐시 된 값을 가져옵니다. 필요에 따라 특정 쿼리 문자열 매개 변수 및/또는 hello에 캐시 키 값을 계산에 사용 된 HTTP 헤더 toobe 입력 **쿼리 문자열 매개 변수에 따라 다름** 및 **Vary 헤더에 의해** 텍스트 상자에 각각 있습니다. 없음 지정, 전체 요청 URL 및 때 다음 HTTP 헤더 값에는 hello ´  ְ 캐시 키 생성: **Accept** 및 **Accept-charset**합니다.

> 캐싱 및 캐싱 정책에 대 한 자세한 내용은 참조 하십시오. [Azure API 관리에서 toocache이 작업을 수행 하는 방법을][How toocache operation results in Azure API Management]합니다.
> 
> 

## <a name="request-parameters"> </a>요청 매개 변수
작업 매개 변수는 hello 매개 변수 탭에서 관리 됩니다. Hello에 지정 된 매개 변수 **URL 템플릿** hello에 **서명** 탭 자동으로 추가 되 고 hello URL 템플릿을 편집 해야만 변경할 수 있습니다. 추가 매개 변수는 수동으로 입력할 수 있습니다.

tooadd 새 쿼리 매개 변수를 클릭 하 여 **쿼리 매개 변수 추가** hello 다음 정보를 입력 합니다.

* **이름** - 매개 변수 이름입니다.
* **설명** -한 간단한 설명 (선택 사항) hello 매개 변수입니다.
* **형식** -매개 변수 유형, hello 드롭다운 목록에서 선택 합니다.
* **값** -toothis 매개 변수를 지정할 수 있는 값입니다. Hello 값 중 하나로 표시할 수 있습니다 기본값으로 (선택 사항).
* **필요한** -hello 확인란을 선택 하 여 필수 hello 매개 변수를 확인 합니다. 

![요청 매개 변수][api-management-request-parameters]

## <a name="request-body"> </a>요청 본문
Hello 작업을 허용 하는 경우 (예:: PUT, POST) 하며 지원 되는 표현 형식 (예:: json, XML)는 본문에서 모든 hello의 예를 제공할 수 있습니다. 

> hello 요청 본문에 설명 용 으로만 사용 되 고 유효성이 검사 되지 않습니다.
> 
> 

요청 본문 tooenter 전환 toohello **본문** 탭 합니다.

클릭 **추가 표현**원하는 콘텐츠 형식 이름 (예: 응용 프로그램/json)을 입력 하기 시작 hello 드롭다운 목록에서에서 선택 하 고 붙여넣기 hello hello 텍스트 상자에 hello 선택한 형식의 요청 본문 예제에서는 필요 합니다. 

![요청 본문][api-management-request-body]

추가 toorepresentations에서 지정할 수도 있습니다 hello에 선택적인 텍스트 설명 **설명** 입력란.

## <a name="responses"> </a>응답
Hello 작업이 생성 될 수 있는 모든 상태 코드에 대 한 응답의 좋습니다 tooprovide 예 이며 각 상태 코드는 응답 본문 예제를 여러 개 있을 수 있습니다, 그리고 지원 되는 각 hello에 대 한 콘텐츠 형식입니다. 

응답을 tooadd 클릭 **추가** hello 원하는 상태 코드를 입력 합니다. 이 예제에서는 hello 상태 코드는 **200 확인**합니다. Hello 코드 hello 드롭다운 목록에서 표시 되 면 선택한 hello 응답 코드는 생성 되 고 추가 된 tooyour 작업 합니다.

![응답 코드][api-management-response-code]

클릭 **추가 표현**hello 원하는 콘텐츠 형식 이름 (예: 응용 프로그램/json)을 입력 하기 시작 하 고 다음 선택 hello에서 드롭 다운 합니다.

![본문 콘텐츠 형식][api-management-response-body-content-type]

Hello 선택한 형식의 응답 본문 예제에서는 hello hello 텍스트 상자에 붙여 넣습니다. 

![응답 본문][api-management-response-body]

원하는 경우 hello에 선택적으로 설명을 추가 **설명** 입력란.

Hello 작업이 구성 되 면 클릭 **저장**합니다.

## <a name="next-steps"> </a>다음 단계
Hello 작업 tooan API에 추가 되 면 hello 다음 단계는 tooassociate hello API는 제품을 포함 하 고 개발자가 해당 작업을 호출할 수 있도록 게시 합니다.

* [어떻게 toocreate 및 제품 게시][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
