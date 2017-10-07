---
title: "aaaCross-원본 자원 공유 (CORS) 지원 | Microsoft Docs"
description: "자세한 내용은 tooenable CORS hello Microsoft Azure 저장소 서비스에 대 한 지원 되는 방법입니다."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Hello Azure 저장소 서비스에 대 한 크로스-원본 자원 공유 (CORS) 지원
Hello Azure 저장소 서비스 버전 2013-08-15부터 hello Blob, 테이블, 큐 및 파일 서비스에 대 한 크로스-원본 자원 공유 (CORS)를 지원 합니다. CORS는 한 도메인 tooaccess 리소스 다른 도메인에서 실행 되는 웹 응용 프로그램을 활성화 하는 HTTP 기능입니다. 웹 브라우저는 보안 제한을 구현 [동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy) ; 다른 도메인에는 Api 호출에서 웹 페이지에 맞지 않는 CORS를 안전 하 게 tooallow 한 도메인 (hello 원본 도메인) toocall 다른 도메인의 Api를 제공합니다. Hello 참조 [CORS 사양](http://www.w3.org/TR/cors/) CORS에 대 한 자세한 내용은 합니다.

설정할 수 있습니다 CORS 규칙 개별적으로 각 hello에 대 한 저장소 서비스를 호출 하 여 [Blob 서비스 속성 설정](https://msdn.microsoft.com/library/hh452235.aspx), [큐 서비스 속성 설정](https://msdn.microsoft.com/library/hh452232.aspx), 및 [설정 테이블 서비스 속성](https://msdn.microsoft.com/library/hh452240.aspx). Hello 서비스에 대 한 hello CORS 규칙을 설정한 후 다음 제대로 인증 된 요청 hello 서비스에 대해 다른 도메인에서 수행 됩니다 평가 toodetermine toohello 지정한 규칙에 따라 허용 합니다.

> [!NOTE]
> CORS는 인증 메커니즘이 아닙니다. CORS를 사용하도록 설정한 상태에서 저장소 리소스에 대해 수행하는 모든 요청은 적절한 인증 서명을 포함하거나 공용 자원에 대한 요청이어야 합니다.
> 
> 

## <a name="understanding-cors-requests"></a>CORS 요청 이해
원본 도메인의 CORS 요청은 두 가지 개별 요청으로 구성될 수 있습니다.

* 실행 전 요청을 hello 서비스에 의해 적용 된 hello CORS 제한 사항을 쿼리 하는 합니다. hello 실행 전 요청은 필요한 hello 요청 메서드를 한 [간편 하 게](http://www.w3.org/TR/cors/), GET, HEAD 또는 POST를 의미 합니다.
* hello에 대 한 hello 실제 요청 리소스를 권장 합니다.

### <a name="preflight-request"></a>실행 전 요청
hello 실행 전 요청 쿼리 hello hello 계정 소유자가 hello 저장소 서비스에 대해 설정한 CORS 제한 합니다. hello 웹 브라우저 (또는 다른 사용자 에이전트) hello 요청 헤더 포함 된 OPTIONS 요청을 보냅니다 메서드 및 원본 도메인이 있습니다. hello 저장소 서비스는 원본 도메인을 지정, 메서드를 요청 하는 CORS 규칙의 미리 구성 된 집합에 따라 의도 한 hello 작업을 평가 하 고, 저장소 리소스에 대 한 실제 요청에서 요청 헤더를 지정할 수 있습니다.

Hello 서비스에 대해 CORS가 사용 하는 경우 hello 실행 전 요청과 일치 하는 CORS 규칙이 있는 hello 서비스는 상태 코드 200 (정상)를 사용 하 여 응답 하 고 hello에 대 한 응답 hello 필요한 Access-control 헤더를 포함 합니다.

Hello 서비스에 대해 CORS가 사용 되지 않거나 hello 실행 전 요청과 일치 하는 CORS 규칙이 없는 경우 hello 서비스는 상태 코드 403 (금지 됨)으로 응답 합니다.

OPTIONS 요청에 포함 되어 있지 않습니다 hello hello 필요한 CORS 헤더 (Origin hello 및 액세스 제어-요청 방법 헤더), hello 서비스는 상태 코드 400 (잘못 된 요청)와 함께 응답 합니다.

Hello 서비스 (Blob, 큐 및 테이블)에 대해 실행 전 요청 되 고 hello 대해서가 아니라 리소스를 요청 합니다. hello 계정 소유자는 CORS 요청 toosucceed hello에 대 한 순서 대로 hello 계정 서비스 속성의 일부분으로 활성화 되어 있어야 합니다.

### <a name="actual-request"></a>실제 요청
Hello 실행 전 요청이 승인 되 면 hello 응답이 반환 됩니다 hello 브라우저 hello hello 저장소 리소스에 대 한 실제 요청을 디스패치 됩니다. 실행 전 요청이 거부 되 면 hello 즉시 hello 브라우저는 hello 실제 요청을 거부 합니다.

hello 실제 요청 hello 저장소 서비스에 대 한 일반 요청으로 처리 됩니다. hello hello Origin 헤더가 있으면 나타내고 hello 요청은 CORS 요청 hello 서비스는 hello 일치 CORS 규칙을 확인 합니다. 일치 하는 항목이 hello Access-control 헤더가 추가 된 toohello 응답은 고 뒤로 toohello 클라이언트 전송. 일치 하는 항목이 없으면 hello CORS Access-control 헤더가 반환 되지 않습니다.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Hello Azure 저장소 서비스에 CORS 사용
CORS 규칙은 hello 서비스 수준에서 설정 tooenable 필요 하거나 각 서비스 (Blob, 큐 및 테이블)에 대해 CORS를 사용 하지 않도록 설정 되므로 별도로 합니다. 기본적으로 CORS는 각 서비스에 대해 사용하지 않도록 설정됩니다. 버전 2013-08-15를 사용 하 여 tooset hello 적절 한 서비스 속성을 필요한 CORS tooenable 이상을 CORS 규칙 toohello 서비스 속성을 추가 합니다. 자세한 방법에 대 한 내용은 tooenable 서비스와 하십시오 tooset CORS 규칙 방식에 대 한 CORS를 사용 하지 않도록 설정 하거나 너무 참조[Blob 서비스 속성 설정](https://msdn.microsoft.com/library/hh452235.aspx), [큐 서비스 속성 설정](https://msdn.microsoft.com/library/hh452232.aspx), 및 [테이블 설정 서비스 속성](https://msdn.microsoft.com/library/hh452240.aspx)합니다.

서비스 속성 설정 작업을 통해 지정한 단일 CORS 규칙의 샘플은 다음과 같습니다.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

다음은 hello CORS 규칙에 포함 된 각 요소에 대 한 설명입니다.

* **AllowedOrigins**: toomake 허용 되는 hello 원본 도메인 hello 저장소에 대 한 요청 CORS를 통해 서비스입니다. hello 원본 도메인은 어떤 hello 요청이 시작 hello 도메인입니다. Note hello 원점 hello 사용자 에이전트가 보냅니다 toohello 서비스는 hello 원점 정확 하 게 대/소문자 구분 일치 되도록 합니다. Hello 와일드 카드 문자를 사용할 수도 있습니다 ' *' tooallow CORS 통해 모든 원본 도메인 toomake 요청 합니다. 위의 hello 예제에서 도메인을 hello [http://www.contoso.com](http://www.contoso.com) 및 [http://www.fabrikam.com](http://www.fabrikam.com) CORS를 사용 하 여 hello 서비스에 대 한 요청을 만들 수 있습니다.
* **AllowedMethods**: hello 메서드 (HTTP 요청 동사) 해당 hello 원본 도메인이 CORS 요청에 사용할 수 있습니다. Hello 위의 예에서 PUT 및 GET 요청만 허용 됩니다.
* **AllowedHeaders**: hello 요청 헤더는 hello 원본 도메인이 hello CORS 요청에서 지정할 수 있습니다. Hello 위의 예에서 x-ms-메타 데이터, x-ms-메타-대상 및 x ms-메타 abc로 시작 하는 모든 메타 데이터 헤더가 허용 됩니다. 해당 hello 와일드 카드 문자 ' *' hello로 시작 되는 헤더 접두사를 사용할 수 지정 했음을 나타냅니다.
* **ExposedHeaders**: hello hello 응답 toohello CORS 요청에서 전송 및 hello 브라우저 toohello 요청 발급자에 의해 노출 될 수 있는 응답 헤더입니다. Hello 예제 hello 브라우저 위에 지시 tooexpose 메타-ms x-으로 시작 되는 헤더입니다.
* **MaxAgeInSeconds**: hello 걸리는 최대 시간은 브라우저 hello 실행 전 OPTIONS 요청을 캐시 해야 합니다.

hello Azure 저장소 서비스에 지원 헤더 모두 hello **AllowedHeaders** 및 **ExposedHeaders** 요소입니다. 헤더의 범주 tooallow 공통 접두사 toothat 범주를 지정할 수 있습니다. 예를 들어 접두사 헤더로 *x-ms-meta*를 지정하면 x-ms-meta로 시작하는 모든 헤더와 일치하는 규칙이 설정됩니다.

다음과 같은 제한을 hello tooCORS 규칙을 적용 합니다.

* 저장소 서비스 (Blob, 테이블 및 큐) 당 CORS 규칙 toofive를 지정할 수 있습니다.
* hello 모든 CORS 규칙 설정의 hello 요청에서 XML 태그를 제외 하 고 최대 크기는 2KB를 초과할 수 없습니다.
* 허용 된 헤더, 노출 된 헤더 또는 허용 되는 원본 hello 길이 256 자를 넘지 않아야 합니다.
* 허용되는 헤더와 표시되는 헤더는 다음 헤더 중 하나일 수 있습니다.
  * 여기서 hello 정확한 헤더 이름이 제공 된 리터럴 헤더와 같은 **x-ms-메타 처리**합니다. Hello 요청에 최대 64 개의 리터럴 헤더를 지정할 수 있습니다.
  * 여기서 hello 헤더의 제공 된 접두사와 같은 헤더 접두사가 **x ms-메타 데이터*** 합니다. 이런이 방식으로 접두사를 지정 허용 하거나 접두사를 지정 하는 hello로 시작 하는 헤더가 노출 합니다. Hello 요청에 최대 2 개의 접두사 헤더를 지정할 수 있습니다.
* hello에 지정 된 메서드 (또는 HTTP 동사) hello **AllowedMethods** 요소에는 Azure 저장소 서비스 Api에서 지 원하는 toohello 방법을 따라야 합니다. 지원되는 메서드는 DELETE, GET, HEAD, MERGE, POST, OPTIONS, PUT입니다.

## <a name="understanding-cors-rule-evaluation-logic"></a>CORS 규칙 평가 논리 이해
저장소 서비스는 실행 전 또는 실제 요청을 받으면 hello 적절 한 Set Service Properties 작업을 통해 hello 서비스에 대해 설정한 hello CORS 규칙에 따라 해당 요청을 평가 합니다. CORS 규칙 hello Set Service Properties 작업의 hello 요청 본문에 설정 된 hello 순서로 평가 됩니다.

다음과 같이 CORS 규칙을 평가합니다.

1. Hello 요청의 원본 도메인이 hello hello에 나열 된 hello 도메인에 대해 검사 먼저 **AllowedOrigins** 요소입니다. Hello 원본 도메인이 hello 목록에 포함 되어 있거나 모든 도메인이 hello 와일드 카드 문자로 허용 되는 경우 ' *', 다음 규칙 평가가 계속 됩니다. Hello 원본 도메인을 지정 하지 않은 경우 hello 요청이 실패 합니다.
2. Hello에 나열 된 hello 방법에 대해 hello 요청의 hello 메서드 (또는 HTTP 동사)를 확인 하는 다음으로, **AllowedMethods** 요소입니다. Hello 메서드 hello 목록에 포함 되어, 규칙 평가가 계속 진행 합니다. 그렇지 않은 경우 hello 요청이 실패 합니다.
3. Hello 요청에는 원본 도메인 및 메서드의 규칙과 일치 하는 경우 해당 규칙은 선택한 tooprocess hello 요청 하 고 더 이상 규칙이 평가 됩니다. 하지만 Hello 요청이 성공할 수 있습니다 hello 요청에 지정 된 모든 헤더가 검사할지 hello에 나열 된 hello 헤더 **AllowedHeaders** 요소입니다. 보낸 hello 헤더에 헤더를 허용 하는 hello 일치 하지 않으면 hello 요청이 실패 합니다.

Hello 규칙, hello 순서 대로 hello 요청 본문에 처리 되므로 최적의 지정 하는 hello 있는 가장 제한적인 규칙을 준수 tooorigins 먼저 hello 목록에서 먼저 평가 되도록 것이 좋습니다. 규칙을 덜 제한적인 규칙 tooallow 예를 들어 hello 목록의 hello 끝에-모든 원본을 지정 합니다.

### <a name="example--cors-rules-evaluation"></a>예제 - CORS 규칙 평가
hello 다음 예제에서는 hello 저장소 서비스에 대 한 작업 tooset CORS 규칙에 대 한 일부 요청 본문 참조 [Blob 서비스 속성 설정](https://msdn.microsoft.com/library/hh452235.aspx), [큐 서비스 속성 설정](https://msdn.microsoft.com/library/hh452232.aspx), 및 [테이블 서비스 속성 설정](https://msdn.microsoft.com/library/hh452240.aspx) hello 요청 생성에 대 한 내용은 합니다.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

다음으로 CORS 요청을 수행 하는 hello를 고려해 야 합니다.

| 요청 |  |  | 응답 |  |
| --- | --- | --- | --- | --- |
| **메서드** |**원본** |**요청 헤더** |**일치하는 규칙** |**결과** |
| **PUT** |http://www.contoso.com |x-ms-blob-콘텐츠-유형 |첫 번째 규칙 |성공 |
| **GET** |http://www.contoso.com |x-ms-blob-콘텐츠-유형 |두 번째 규칙 |성공 |
| **GET** |http://www.contoso.com |x-ms-client-request-id |두 번째 규칙 |실패 |

hello 첫 번째 요청 hello 첫 번째 규칙과 일치 – hello 원본 도메인 원본을 허용 하는 hello와 일치 합니다. hello 메서드 메서드를 허용 하는 hello 하 고, hello 헤더 hello 허용-헤더와 일치 하 고 하므로 성공 합니다.

두 번째 요청 hello hello 메서드 메서드를 허용 하는 hello와 일치 하지 않으므로 hello 첫 번째 규칙을 일치 하지 않습니다. 하지만 하므로 성공 hello 두 번째 규칙을 일치, 않습니다.

hello 세 번째 요청 있으므로 더 이상 규칙이 평가 됩니다은 원본 도메인과 메서드를 hello 두 번째 규칙과 일치 합니다. 그러나 hello *x-ms-클라이언트-request-id 헤더* hello 팩트는 hello 세 번째 규칙의 의미 체계 hello 허용 것 것 toosucceed 불구 하 고 hello 요청 실패 hello 두 번째 규칙에서 허용 되지 않습니다.

> [!NOTE]
> 이 예제는 더 제한적인 속성 전에 덜 제한적인 규칙을 표시 하지만 일반적 hello 최상의 방법은 toolist hello에 대 한 가장 제한적인 규칙이 먼저입니다.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Hello Vary 헤더가 설정 되는 방법을 이해
hello *Vary* 헤더는 hello 서버 tooprocess hello 요청 하 여 선택한 hello 조건에 대 한 hello 브라우저나 사용자 에이전트에 알려주는 요청 헤더 필드의 집합으로 구성 된 표준 HTTP/1.1 헤더입니다. hello *Vary* 헤더 hello 응답을 캐시 해야 하는 방법을 프록시, 브라우저 및 Cdn toodetermine를 사용 하 여 캐시에 주로 사용 됩니다. 자세한 내용은 hello에 대 한 hello 사양을 참조 [Vary 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)합니다.

Hello 브라우저 또는 다른 사용자 에이전트에서 CORS 요청의 hello 응답을 캐시, hello 원본 도메인이 origin을 허용 하는 hello로 캐시 됩니다. 두 번째 경우 도메인 문제 hello 캐시가 활성화 된 동안 저장소 리소스에 대 한 동일한 요청 hello, hello 사용자 에이전트 hello 캐시 된 원본 도메인을 검색 합니다. 두 번째 도메인 hello 않았다면 성공 했을 hello 요청이 실패 하므로 hello 캐시 된 도메인을 일치 하지 않습니다. 경우에 따라 Azure 저장소 설정 하는 hello Vary 헤더가 너무**원점** tooinstruct hello 사용자 에이전트 toosend hello 후속 CORS 요청 toohello 서비스는 도메인이 hello에서 다른 요청 hello 원점 캐시 될 때입니다.

Hello를 설정 하는 azure 저장소 *Vary* 헤더 너무**원점** 비활성화 hello에 실제 GET/HEAD 요청에 대 한:

* Hello와 정확히 일치 하는 원본 hello 요청 원본 CORS 규칙에 의해 정의 된 허용 하는 경우. 정확히 일치 toobe hello CORS 규칙 와일드 카드를 포함 하지 않은 ' * ' 문자입니다.
* 없는 규칙이 일치 하는 hello 요청 원본과 있지만 hello 저장소 서비스에 대해 CORS가 사용 합니다.

Hello 경우 GET/HEAD 요청이 모든 원본을 허용 하는 CORS 규칙이 일치 하는 hello 응답은 모든 원본이 허용 하 고 hello 사용자 에이전트 캐시 hello 캐시가 활성화 된 동안 모든 원본 도메인의 후속 요청 하면 나타냅니다.

GET/HEAD 이외의 메서드를 사용 하는 요청에 대 한 hello 저장소 서비스는 설정 되지 않았음을 hello Vary 헤더 응답 toothese 메서드 사용자 에이전트에서 캐시 되지 않으므로 이후 note 합니다.

hello 다음 표에 Azure 방법과 저장소 hello에 이전에 따라 tooGET/HEAD 요청 설명의 경우 응답 합니다.

| 요청 | 계정 설정 및 규칙 평가 결과 |  |  | 응답 |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **요청한 Origin 헤더 유무** |**이 서비스에 대한 CORS 규칙 지정 여부** |**모든 원본(*)을 허용하는 일치 규칙 유무** |**원본이 정확하게 일치하는지 확인하는 일치 규칙 유무** |**응답에 Vary 헤더 집합 tooOrigin 포함 됩니다.** |**응답의 Access-Control-Allowed-Origin 유무:"*"** |**응답의 Access-Control-Exposed-Headers 유무** |
| 아니요 |아니요 |아니요 |아니요 |아니요 |아니요 |아니요 |
| 아니요 |예 |아니요 |아니요 |예 |아니요 |아니요 |
| 아니요 |예 |예 |아니요 |아니요 |예 |예 |
| 예 |아니요 |아니요 |아니요 |아니요 |아니요 |아니요 |
| 예 |예 |아니요 |예 |예 |아니요 |예 |
| 예 |예 |아니요 |아니요 |예 |아니요 |아니요 |
| 예 |예 |예 |아니요 |아니요 |예 |예 |

## <a name="billing-for-cors-requests"></a>CORS 요청에 대한 청구
성공적인 실행 전 요청 사용자 계정에 대 한 hello 저장소 서비스에 대 한 CORS를 사용 하는 경우 청구 됩니다 (호출 하 여 [Blob 서비스 속성 설정](https://msdn.microsoft.com/library/hh452235.aspx), [큐 서비스 속성 설정](https://msdn.microsoft.com/library/hh452232.aspx), 또는 [ 테이블 서비스 속성 설정](https://msdn.microsoft.com/library/hh452240.aspx)). toominimize 요금 hello를 설정 해 보세요. **MaxAgeInSeconds** hello 사용자 에이전트 캐시 hello 요청 하 여 CORS 요소 규칙 tooa 큰 값입니다.

실행 전 요청이 실패하면 요금이 청구되지 않습니다.

## <a name="next-steps"></a>다음 단계
[Blob 서비스 속성 설정](https://msdn.microsoft.com/library/hh452235.aspx)

[큐 서비스 속성 설정](https://msdn.microsoft.com/library/hh452232.aspx)

[테이블 서비스 속성 설정](https://msdn.microsoft.com/library/hh452240.aspx)

[W3C 교차 원본 자원 공유 사양](http://www.w3.org/TR/cors/)

