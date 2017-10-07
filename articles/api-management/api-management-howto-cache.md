---
title: "Azure API 관리에서 tooimprove 성능 캐싱 aaaAdd | Microsoft Docs"
description: "Tooimprove hello 대기 시간, 대역폭 소비 및 웹 서비스 API 관리 서비스 호출에 대 한 로드 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Azure API 관리에서 캐싱 tooimprove 성능을 추가합니다
응답 캐싱을 위해 API 관리의 작업을 구성할 수 있습니다. 응답 캐싱은 그다지 사용되지 않는 데이터에 대한 API 대기 시간, 대역폭 사용량 및 웹 서비스 부하를 상당히 줄일 수 있습니다.

이 가이드에서는 tooadd 응답 API에 대 한 캐싱 및 hello 샘플 에코 API 작업에 대 한 정책을 구성 합니다. Hello 작업 동작의 개발자 포털 tooverify 캐싱 hello에서 호출할 수 있습니다.

> [!NOTE]
> 정책 식을 사용하여 키별 캐싱 항목에 대한 자세한 내용은 [Azure API 관리에서 사용자 지정 캐싱](api-management-sample-cache-by-key.md)을 참조하세요.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 가이드의 단계를 다음 hello를 먼저 API 관리 서비스 인스턴스를 사용 하 여 API와 구성 된 제품 있어야 합니다. API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.

## <a name="configure-caching"> </a>캐싱을 위해 작업 구성
이 단계에서는 hello 캐싱 hello의 설정을 검토 하 **가져올 리소스 (캐시 됨)** hello 샘플 에코 API의 작동 합니다.

> [!NOTE]
> 각 API 관리 서비스 인스턴스를 사용 하는 tooexperiment 및 API 관리에 대 한 자세한 내용은 수 있는 에코 API와 미리 구성 된 제공 됩니다. 자세한 내용은 [Azure API Management 시작][Get started with Azure API Management]을 참조하세요.
> 
> 

시작 tooget 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서. API 관리 게시자 포털 toohello 이동합니다.

![게시자 포털][api-management-management-console]

클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **에코 API**합니다.

![Echo API][api-management-echo-api]

Hello 클릭 **작업** 탭을 클릭 한 다음 hello **가져올 리소스 (캐시 됨)** hello에서 작업 **작업** 목록입니다.

![Echo API 작업][api-management-echo-api-operations]

Hello 클릭 **캐싱** 탭 tooview hello 캐싱이 작업에 대 한 설정입니다.

![캐싱 탭][api-management-caching-tab]

작업의 경우 선택 hello tooenable 캐싱 **사용** 확인란 합니다. 이 예제에서는 캐싱이 사용됩니다.

Hello hello 값에 따라 각 작업 응답은 입력 **쿼리 문자열 매개 변수에 따라 다름** 및 **Vary 헤더에 의해** 필드입니다. 쿼리 문자열 매개 변수 또는 헤더에 따라 여러 응답 toocache 하려는 경우에이 두 필드에 구성할 수 있습니다.

**기간** hello 캐시 된 응답의 hello 만료 간격을 지정 합니다. 이 예제에서는 hello 간격은 **3600** (초)를 해당 tooone 시간입니다.

첫 번째 요청 toohello hello이 예제에서 구성을 캐싱 hello를 사용 하 여 **가져올 리소스 (캐시 됨)** 작업이 hello 백 엔드 서비스에서 응답을 반환 합니다. 이 응답 캐시 됩니다, 키가 지정 된 hello 지정 된 헤더 및 쿼리 문자열 매개 변수입니다. Toohello 작업 매개 변수를 일치 하는 hello 갖습니다 후속 호출 hello 캐시 기간 간격이 만료 될 때까지 반환 된 응답을 캐시 합니다.

## <a name="caching-policies"></a>검토 hello 캐싱 정책
이 단계에서는 hello 캐싱 hello에 대 한 설정을 검토 **가져올 리소스 (캐시 됨)** hello 샘플 에코 API의 작동 합니다.

Hello에 대 한 작업에 대 한 캐싱 설정을 구성한 경우 **캐싱** 캐싱 탭 hello 작업에 대 한 정책을 추가 됩니다. 이러한 정책은 확인 및 hello 정책 편집기에서 편집할 수 있습니다.

클릭 **정책** hello에서 **API 관리** hello 왼쪽과 선택한 후에 메뉴 **에코 API (캐시 됨) 하는 리소스 가져오기 /** hello에서 **작업**드롭 다운 목록입니다.

![정책 범위 작업][api-management-operation-dropdown]

그러면이 작업에 대 한 hello 정책 hello 정책 편집기에 표시 됩니다.

![API 관리 정책 편집기][api-management-policy-editor]

이 작업에 대 한 hello 정책 정의 된 hello를 사용 하 여 검토 하는 hello 캐싱 구성을 정의 하는 hello 정책을 포함 **캐싱** hello 이전 단계에서 탭 합니다.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> 캐싱 정책을 hello 정책 편집기에서 변경 내용을 toohello hello에 반영 됩니다 **캐싱** 탭의 작업을 반대로 합니다.
> 
> 

## <a name="test-operation"></a>작업 호출 및 hello 캐싱을 테스트
toosee hello 동작에서 캐싱에서는 작업을 호출할 수 hello hello 개발자 포털에서 합니다. 클릭 **개발자 포털** hello 맨 위 오른쪽 메뉴에 있습니다.

![개발자 포털][api-management-developer-portal-menu]

클릭 **Api** 에 최상위 메뉴 hello 선택한 후 **에코 API**합니다.

![Echo API][api-management-apis-echo-api]

> 구성 하는 하나의 API가 있는 경우 표시 tooyour 계정 Api를 클릭 한 다음 이동 직접 해당 API에 대 한 toohello 작업.
> 
> 

선택 hello **가져올 리소스 (캐시 됨)** 작업과 클릭 **콘솔을 열고**합니다.

![콘솔 시작][api-management-open-console]

hello 콘솔 hello 개발자 포털에서 직접 tooinvoke 작업을 허용 합니다.

![콘솔][api-management-console]

Hello에 대 한 기본값을 유지 **param1** 및 **매개 변수 2가**합니다.

선택 hello hello에서 원하는 키 **구독 키** 드롭 다운 목록입니다. 계정에 구독이 하나만 있는 경우 이미 선택되어 있습니다.

입력 **sampleheader:value1** hello에 **요청 헤더** 입력란.

클릭 **HTTP Get** hello 메모 응답 헤더를 확인 합니다.

입력 **sampleheader:value2** hello에 **요청 헤더** 텍스트 상자 및 클릭 **HTTP Get**합니다.

해당 hello 값을 기록해 둡니다 **sampleheader** 여전히 **value1** hello에 대 한 응답입니다. 일부 다른 값을 사용 하 고는 hello hello 첫 번째 호출에서 캐시 된 응답이 반환 됩니다.

입력 **25** hello에 **매개 변수 2가** 필드를 선택한 다음 클릭 **HTTP Get**합니다.

해당 hello 값을 기록해 둡니다 **sampleheader** hello에 대 한 응답은 이제 **value2**합니다. Hello 작업 결과 쿼리 문자열에 따라 키가 지정 된, 때문에 hello 이전 캐시 된 응답이 반환 되지 않았습니다.

## <a name="next-steps"> </a>다음 단계
* 캐싱 정책에 대 한 자세한 내용은 참조 [캐싱 정책을] [ Caching policies] hello에 [API 관리 정책 참조][API Management policy reference]합니다.
* 정책 식을 사용하여 키별 캐싱 항목에 대한 자세한 내용은 [Azure API 관리에서 사용자 지정 캐싱](api-management-sample-cache-by-key.md)을 참조하세요.

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
