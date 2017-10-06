---
title: "CDN aaaAzure 규칙 엔진 기능 | Microsoft Docs"
description: "Azure CDN 규칙 엔진 일치 조건 및 기능에 대한 참조 설명서"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Azure CDN 규칙 엔진 기능
이 항목에 자세히 설명 hello 사용할 수 있는 기능에 대 한 Azure 네트워크 CDN (콘텐츠 배달)에서는 [규칙 엔진](cdn-rules-engine.md)합니다.

규칙의 세 번째 부분 hello는 hello 기능입니다. 수 있는 작업의 hello 형식을 정의 하는 기능 toohello 유형의 집합 일치 조건에 의해 식별 되는 요청을 적용 합니다.

## <a name="access"></a>Access

이러한 기능은 디자인 된 toocontrol 액세스 toocontent 있습니다.


이름 | 목적
-----|--------
액세스 거부 | 모든 요청이 403 사용 권한 없음 응답으로 거부되는지 여부를 결정합니다.
토큰 인증 | 토큰 기반 인증 적용된 tooa 요청 않을 것인지를 결정 합니다.
토큰 인증 거부 코드 | 반환 되는 tooa 사용자 요청이 거부 되는 tooToken 기반 인증 인 경우 응답의 hello 유형을 결정 합니다.
토큰 인증 URL 대/소문자 무시 | 토큰 기반 인증에서 URL 비교 시 대/소문자를 구분할지 결정합니다.
토큰 인증 매개 변수 | Hello 토큰 기반 인증 쿼리 문자열 매개 변수 이름을 바꿔야 하는지 여부를 결정 합니다.

### <a name="deny-access"></a>액세스 거부
**목적**: 모든 요청이 403 사용할 수 없음 응답으로 거부되는지 여부를 결정합니다.

값 | 결과
------|-------
사용| Hello 일치 하는 조건을 toobe 403 사용 권한 없음 응답와 함께 거부를 만족 하는 모든 요청 하면 됩니다.
사용 안 함| Hello 기본 동작을 복원합니다. hello 기본 동작은 tooallow hello 원본 toodetermine hello의 서버 유형을 반환 되는 응답입니다.

**기본 동작**: 사용 안 함

> [!TIP]
   > 이 기능은 사용할 수는 tooassociate 조건 tooblock 액세스 tooHTTP 참조 페이지 인라인 링크 tooyour 콘텐츠를 사용 하는 요청 헤더와 일치 합니다.

### <a name="token-auth"></a>토큰 인증
**목적:** 토큰 기반 인증 적용된 tooa 요청 않을 것인지를 결정 합니다.

토큰 기반 인증을 사용 하는 경우 암호화 된 토큰을 제공 하 고 해당 토큰이 지정 된 toohello 요구 사항을 준수 하는 유일한 요청 적용 됩니다.

hello 한 암호화 키를 사용 하는 tooencrypt 및 암호 해독 토큰 값이 됩니다는 기본 키와 토큰 인증 페이지의 키 백업 옵션에 의해 결정 됩니다. 암호화 키는 플랫폼에 따라 다릅니다.

값 | 결과
------|---------
사용 | 보호 hello 토큰 기반 인증을 사용 하는 콘텐츠를 요청 합니다. 유효한 토큰을 제공하고 요구 사항을 충족하는 클라이언트의 요청만 허용합니다. FTP 트랜잭션은 토큰 기반 인증에서 제외됩니다.
사용 안 함| Hello 기본 동작을 복원합니다. 기본 동작은 hello가 tooallow 토큰 기반 인증 구성 toodetermine 요청은 보안 됩니다.

**기본 동작**: 사용 안 함

###<a name="token-auth-denial-code"></a>토큰 인증 거부 코드
**목적:** 반환 되는 tooa 사용자 요청이 거부 되는 tooToken 기반 인증 인 경우 응답의 hello 유형을 결정 합니다.

hello 사용할 수 있는 응답 코드는 다음과 같습니다.

응답 코드|응답 이름|설명
----------------|-----------|--------
301|영구적으로 이동됨|이 상태 코드의 위치 헤더에 지정 된 권한이 없는 사용자가 toohello URL로 리디렉션합니다.
302|있음|이 상태 코드의 위치 헤더에 지정 된 권한이 없는 사용자가 toohello URL로 리디렉션합니다. 이 상태 코드는 hello 산업 표준 방법의 리디렉션을 수행 합니다.
307|임시 리디렉션|이 상태 코드의 위치 헤더에 지정 된 권한이 없는 사용자가 toohello URL로 리디렉션합니다.
401|권한 없음|이 상태 코드를 응답 Www-authenticate 헤더 함께 사용 하면 사용자에 게 인증 tooprompt이 있습니다.
403|사용할 수 없음|이 hello 표준 403 사용할 수 없음 상태 메시지 콘텐츠 보호 tooaccess 시도 때 권한 없는 사용자 표시 됩니다.
404|파일을 찾을 수 없음|이 상태 코드는 hello HTTP 클라이언트 hello 서버와 수 toocommunicate 있지만 hello 요청한 콘텐츠를 찾을 수 없습니다 나타냅니다.

#### <a name="url-redirection"></a>URL 리디렉션

이 기능은 구성 된 tooreturn 3xx 상태 코드 되었을 때 URL 리디렉션 tooa 사용자 지정 URL을 지원 합니다. Hello 다음 단계를 수행 하 여이 사용자 지정 URL은 지정할 수 있습니다.

1. Hello 토큰 인증 거부 코드 기능에 대 한 3xx 응답 코드를 선택 합니다.
2. 선택적 헤더 이름 옵션에서 "Location"을 선택합니다.
3. 선택적 헤더 값 옵션 toohello 필요한 URL을 설정 합니다.

URL 3xx 상태 코드를 정의 하지 않은 경우 다음 hello 3xx 상태 코드에 대 한 표준 응답 페이지가 반환할 toohello 사용자입니다.

URL 리디렉션은 3xx 응답 코드에만 적용됩니다.

선택적 헤더 값 옵션은 영숫자, 인용 부호 및 공백을 지원합니다.

#### <a name="authentication"></a>인증

이 기능은 tooan 토큰 기반 인증으로 보호 된 콘텐츠에 대 한 권한이 없는 요청에 응답할 때 hello 기능 tooinclude WWW 인증 헤더를 지원 합니다. Www-authenticate 헤더에 설정 된 경우 구성에서 너무 "기본" hello 권한이 없는 사용자 계정 자격 증명에 대 한 나타납니다.

구성 이상 hello hello 다음 단계를 수행 하 여 수행할 수 있습니다.

1. Hello 토큰 인증 거부 코드 기능에 대 한 hello 응답 코드와 "401"를 선택 합니다.
2. 선택적 헤더 이름 옵션에서 "WWW-Authenticate"를 선택합니다.
3. 선택적 헤더 값 옵션이 너무 "기본 설정 합니다."

WWW-Authenticate 헤더는 401 응답 코드에만 적용됩니다.

### <a name="token-auth-ignore-url-case"></a>토큰 인증 URL 대/소문자 무시
**목적:** 토큰 기반 인증으로 수행되는 URL 비교에서 대/소문자를 구분하는지 여부를 결정합니다.

이 기능에 의해 영향을 받는 hello 매개 변수는.

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

유효한 값은 다음과 같습니다.

값|결과
---|----
사용|토큰 기반 인증 매개 변수에 대 한 Url을 비교할 때이 지 서버 tooignore 대/소문자를 하면 됩니다.
사용 안 함|Hello 기본 동작을 복원합니다. 토큰 인증 toobe 대/소문자 구분에 대 한 URL 비교 hello 기본 동작이입니다.

**기본 동작**: 사용 안 함
 
### <a name="token-auth-parameter"></a>토큰 인증 매개 변수
**목적:** hello 토큰 기반 인증 쿼리 문자열 매개 변수 이름을 바꿔야 하는지 여부를 결정 합니다.

주요 정보:

- 값 옵션 정의 hello 쿼리 문자열 매개 변수 이름을 통해 토큰을 지정할 수 있습니다.
- 값 옵션을 너무 설정할 수 없습니다. "ec_token."
- 값 옵션만에 정의 된 해당 hello 이름이 있는지 확인 
- 유효한 URL 문자를 포함합니다.

값|결과
----|----
사용|값 옵션이 있는 토큰을 정의 해야 하는 hello 쿼리 문자열 매개 변수 이름을 정의 합니다.
사용 안 함|토큰은 hello 요청 URL에는 정의 되지 않은 쿼리 문자열 매개 변수로 지정할 수 있습니다.

**기본 동작**: 사용 안 함 토큰은 hello 요청 URL에는 정의 되지 않은 쿼리 문자열 매개 변수로 지정할 수 있습니다.

## <a name="caching"></a>구성

이러한 기능은 디자인 된 toocustomize 시기와 방법을 콘텐츠가 캐시 되 고 있습니다.

이름 | 목적
-----|--------
대역폭 매개 변수 | 대역폭 제한 매개 변수(예: ec_rate 및 ec_prebuf)를 활성화할지 여부를 결정합니다.
대역폭 제한 | 이 지 서버에서 제공 하는 hello 응답에 대 한 hello 대역폭을 제한 합니다.
바이패스 캐시 | Hello 요청 우리의 캐싱 기술을 활용할 수 있는지 여부를 결정 합니다.
Cache-Control 헤더 처리 | 컨트롤은 hello에 지 서버에서 캐시 제어 헤더의 생성을 hello 외부 Max-age 기능을 활성화 하는 경우.
Cache-Key 쿼리 문자열 | Hello 캐시 키 요청과 연결 된 쿼리 문자열 매개 변수를 제외 포함 여부를 결정 합니다.
Cache-Key 다시 쓰기 | 요청과 연결 된 hello 캐시 키를 다시 작성 합니다.
전체 캐시 채우기 | 요청 결과, 에지 서버에서 캐시가 부분적으로 누락된 경우 수행할 작업을 결정합니다.
압축 파일 형식 | Hello 서버에서 압축 되도록 하는 hello 파일 형식을 정의 합니다.
기본 내부 Max-Age | Edge 서버 tooorigin 서버 캐시 유효성 재검사 hello 기본 최대 처리 기간 간격을 결정합니다.
만료 헤더 처리 | 컨트롤에 지 서버에서 Expires 헤더의 생성을 hello hello 외부 Max-age 기능을 활성화 하는 경우.
외부 Max-Age | 브라우저 tooedge 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정합니다.
강제 내부 Max-Age | Edge 서버 tooorigin 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정합니다.
H.264 지원(HTTP 점진적 다운로드) | H.264 hello 유형의 파일 형식을 사용 하는 toostream 수 있는 콘텐츠를 결정 합니다.
No-Cache 요청 부여 | 여부 HTTP 클라이언트의 캐시 없음 요청 전달 toohello 원본 서버를 결정 합니다.
원본 No-Cache 무시 | CDN이 원본 서버에서 제공되는 특정 지시문을 무시할지 여부를 결정합니다.
적절하지 않은 범위 무시 | 반환 되는 tooclients 요청 416 요청한 범위가 충분 하지 않음 상태 코드를 생성할 때 hello 응답을 결정 합니다.
내부 Max-Stale | 캐시 된 자산을 구현 될 수 있습니다 hello 정상적으로 종료 시간 이전 시간에 지 서버에서 hello에 지 서버 경우 없습니다 toorevalidate hello hello 원본 서버와 캐시 된 자산을 제어 합니다.
부분 캐시 공유 | 요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있는지 여부를 결정합니다.
캐시된 콘텐츠 사전 유효성 검사 | TTL이 만료되기 전에 캐시된 콘텐츠로 미리 유효성 재검사할 수 있는지 여부를 결정합니다.
0바이트 캐시 파일 새로 고침 | 0바이트 캐시 자산에 대한 HTTP 클라이언트 요청이 에지 서버에 의해 처리되는 방식을 결정합니다.
캐시 가능한 상태 코드 집합 | 캐시 된 콘텐츠 발생할 수 있는 상태 코드 hello 집합을 정의 합니다.
오류 시 오래된 콘텐츠 배달 | 캐시 유효성 재검사 중 또는 검색 하는 동안 hello hello 고객 원본 서버에서 콘텐츠를 요청 하면 오류가 발생할 때 배달 될 캐시 된 콘텐츠 만료 여부를 확인 합니다.
유효성 재검사 중 기한 경과 | 유효성을 다시 수행 하는 동안이 지 서버 tooserve 오래 된 클라이언트 toohello 요청자를 허용 하 여 성능이 향상 됩니다.
주석 | hello 주석 기능을 사용 하는 참고 toobe 규칙 내에 추가 합니다.

###<a name="bandwidth-parameters"></a>대역폭 매개 변수
**목적:** 대역폭 제한 매개 변수(예: ec_rate 및 ec_prebuf)를 활성화하는지 여부를 결정합니다.

대역폭 조정 매개 변수는 클라이언트의 요청에 대 한 hello 데이터 전송 속도 제한 tooa 사용자 지정 비율 여부를 결정 합니다.

값|결과
--|--
사용|Edge 서버 toohonor 대역폭을으로 요청을 수 있습니다.
사용 안 함|Edge 서버 tooignore 대역폭 매개 변수를 제한 하면 됩니다. hello 요청 (즉, 대역폭 제한) 없이 콘텐츠를 정상적으로 처리 됩니다.

**기본 동작**: 사용

###<a name="bandwidth-throttling"></a>대역폭 제한
**목적:** 스로틀 hello 우리의 지 서버에서 제공 하는 hello 응답에 대 한 대역폭입니다.

Hello 다음 옵션을 모두 정의 tooproperly 대역폭 제한 설정 해야 합니다.

옵션|설명
--|--
초당 킬로바이트|이 옵션 toohello 최대 대역폭 (k b / 초)을 사용 하는 toodeliver hello 응답 수를 설정 합니다.
Prebuf 초|이 옵션 toohello 번호는에 지 서버에서 제한 대역폭 될 때까지 대기 하는 시간 (초)을 설정 합니다. hello의이 시간 동안 무제한 대역폭의 목적은 tooprevent 미디어 플레이어에서 일지 또는 버퍼링 toobandwidth 제한 문제가 발생 합니다.

**기본 동작**: 사용 안 함

###<a name="bypass-cache"></a>바이패스 캐시
**목적:** hello 요청 우리의 캐싱 기술을 활용할 수 있는지 여부를 결정 합니다.

값|결과
--|--
사용|Hello 콘텐츠는에 지 서버에서 이전에 캐시 된 경우에 toohello 원본 서버를 통해 모든 요청 toofall을 하면 됩니다.
사용 안 함|응답 헤더에 정의 된 toohello 캐시 정책에 따라 toocache 자산에 지 서버에 발생 합니다.

**기본 동작:**

- **HTTP Large:** 사용 안 함

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Cache-Control 헤더 처리
**목적:** 외부 Max-age 기능을 활성화 하는 경우 hello에 지 서버에서 캐시 제어 헤더의 hello 생성을 제어 합니다.

이 구성 유형은 tooplace hello 외부 Max-age 및 hello 캐시 컨트롤 헤더 처리 기능에는 가장 쉬운 방법은 tooachieve hello 동일한 문에서 hello 합니다.

값|결과
--|--
덮어쓰기|해당 hello 다음 작업 수행을 확인 합니다.<br/> -Hello 원본 서버에 의해 생성 된 Cache-control 헤더를 덮어씁니다. <br/>-Hello 외부 Max-age 기능 toohello 응답에서 생성 된 Cache-control 헤더를 추가 합니다.
통과|Hello 외부 Max-age 기능에 의해 생성 된 Cache-control 헤더 toohello 응답 하지 않습니다 추가 되어 있는지 확인 합니다. <br/> Hello 원본 서버에서 생성 하는 Cache-control 헤더 toohello 최종 사용자를 통해 전달 합니다. <br/> Hello 원본 서버는 캐시 제어 헤더 다음이 옵션을 생성 하지 포함 될 수 있습니다 원인 hello 응답 헤더 toonot 캐시 컨트롤 헤더입니다.
없는 경우 추가|캐시 컨트롤 헤더 hello 원본 서버에서 수신 되지 않았습니다,이 옵션 hello 외부 Max-age 기능에 의해 생성 된 Cache-control 헤더를 추가 합니다. 이 옵션은 모든 자산에 Cache-Control 헤더를 할당하도록 하는 데 유용합니다.
제거| 이 옵션을 사용 하면 캐시 컨트롤 헤더 hello 헤더 응답과 함께 포함 되지 않습니다. 캐시 컨트롤 헤더에 이미 할당 된 경우 다음 것에서 제거 됩니다 hello 헤더 응답 합니다.

**기본 동작:** 덮어쓰기

###<a name="cache-key-query-string"></a>Cache-Key 쿼리 문자열
**목적:** cache-key에서 요청과 관련된 쿼리 문자열 매개 변수를 포함할지 또는 제외할지 여부를 결정합니다.

주요 정보:

- 쿼리 문자열 매개 변수 이름을 둘 이상 지정합니다. 각 매개 변수 이름은 단일 공백으로 구분해야 합니다.
- 이 기능은 쿼리 문자열 매개 변수를 포함 하거나 hello 캐시 키에서 제외 됩니다 있는지 여부를 결정 합니다. 각 옵션에 제공되는 추가 정보는 다음과 같습니다.

형식|설명
--|--
 포함|  지정 된 각 매개 변수에 해야 hello 캐시 키에 포함 되어야 함을 나타냅니다. 이 기능에 정의된 쿼리 문자열 매개 변수의 고유한 값을 포함하는 요청마다 고유한 cache-key가 생성됩니다. 
 모두 포함  |고유한 쿼리 문자열이 포함 된 각 요청 tooan 자산에 대 한 고유 캐시 키 만들어질 수를 나타냅니다. 이러한 유형의 구성 하므로 캐시 적중 횟수의 작은 비율을 tooa 않을 일반적으로 권장 되지 않습니다. 이렇게 하면 미치게 될 tooserve 더 많은 요청이 이후 hello 원본 서버의 hello 로드가 늘어납니다. 이 구성은 hello 캐싱 "고유-cache" 쿼리 문자열 캐싱 페이지 라고 하는 동작을 복제 합니다. 
 제외 | 해당만 hello 지정 매개 변수는 hello 캐시 키에서 제외 됩니다 나타냅니다. 다른 모든 쿼리 문자열 매개 변수는 hello 캐시 키에 포함 됩니다. 
 모두 제외  |모든 쿼리 문자열 매개 변수가 됩니다 hello 캐시 키에서 제외 되어야 함을 나타냅니다. 이 구성은 hello 기본 캐싱 쿼리 문자열 캐싱 페이지에 "표준 캐시"으로 알려진 동작을 복제 합니다. 

HTTP 규칙 엔진의 hello 전원 toocustomize hello 방식 으로를 쿼리 문자열 캐싱을 구현 되는에 있습니다. 예를 들어 특정 위치 또는 파일 형식에서만 쿼리 문자열 캐싱을 수행하도록 지정할 수 있습니다.

Tooduplicate hello 쿼리 문자열 캐싱 동작으로 "no cache" 쿼리 문자열 캐싱 페이지, 원하는 경우 해야 합니다 toocreate는 URL 쿼리 와일드 카드 일치 조건과 바이패스 캐시 기능을 포함 하는 규칙입니다. URL 쿼리 와일드 카드 일치 조건을 hello tooan 별표 (*)을 설정 해야 합니다.

#### <a name="sample-scenarios"></a>샘플 시나리오

이 기능의 샘플 사용법이 아래에 나와 있습니다. 예제 요청 및 hello에 대 한 기본 캐시 키 아래에 나와 있습니다.

- **샘플 요청:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01
- **기본 cache-key:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>포함

샘플 구성:

- **형식:** 포함
- **매개 변수:** language

이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>모두 포함

샘플 구성:

- **형식:** 모두 포함

이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>제외

샘플 구성:

- **형식:** 제외
- **매개 변수:** sessionid userid

이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>모두 제외

샘플 구성:

- **형식:** 모두 제외

이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Cache-Key 다시 쓰기
**목적:** 캡슐화 hello 요청과 연결 된 캐시 키입니다.

캐시 키가 캐시의 hello 목적을 위해 자산을 식별 하는 hello 상대 경로입니다. 즉, 서버는 캐시 된 버전의 캐시 키에 정의 된 대로 tooits 경로 따라 자산을 확인 합니다.

모두 hello 다음 옵션을 정의 하 여이 기능을 구성 합니다.

옵션|설명
--|--
원래 경로| 캐시 키를 다시 작성 됩니다 요청의 hello 상대 경로 toohello 유형을 정의 합니다. 상대 경로는 기본 경로를 선택한 다음 정규식 패턴을 정의함으로써 정의할 수 있습니다.
새 경로|Hello hello 새 캐시 키에 대 한 상대 경로 정의 합니다. 상대 경로는 기본 경로를 선택한 다음 정규식 패턴을 정의함으로써 정의할 수 있습니다. HTTP 변수의 hello 사용을 통해이 상대 경로 동적으로 생성 될 수 있습니다.
**기본 동작:** 요청의 캐시 키 hello 요청 URI에 의해 결정 됩니다.

###<a name="complete-cache-fill"></a>전체 캐시 채우기
**목적:** 요청으로 인해 에지 서버에서 부분 캐시가 누락된 경우 수행할 작업을 결정합니다.

부분 캐시 누락 tooan 완전히 다운로드 된에 지 서버 없었던 자산에 대 한 hello 캐시 상태를 설명 합니다. 자산 부분적 으로만에 지 서버에 캐시 되는, 다음 hello 해당 자산에 대 한 다음 요청이 전달 됩니다 다시 toohello 원본 서버.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
부분 캐시 누락은 일반적으로 사용자가 다운로드를 중단한 후에 발생하거나 HTTP 범위 요청을 사용하여 단독으로 요청된 자산에 대해 발생합니다. 이 기능은 큰 자산에 대 한 가장 유용한 여기서 사용자가 다운로드 되지 것입니다 일반적으로 이러한 시작 toofinish (예: 비디오) 에서입니다. 결과적으로,이 기능은 hello HTTP 많은 플랫폼에서 기본적으로 사용 됩니다. 다른 모든 플랫폼에서는 사용할 수 없습니다.

Hello 부하 고객 원본 서버를 줄여야 하 고는 고객에 게 콘텐츠를 다운로드 하는 hello 속도 높일 이후 tooleave hello 기본 구성은 hello HTTP 큰 플랫폼에 대 한이 좋습니다.

설정을 추적 되는 캐시에 toohello 방식으로 인해이 기능을 연결할 수 일치 조건을 다음 hello로: 가장자리 Cname, 리터럴 헤더를 요청, 요청 헤더 와일드 카드, URL 쿼리 리터럴 및 쿼리 와일드 카드 URL입니다.

값|결과
--|--
사용|Hello 기본 동작을 복원합니다. hello 기본 동작은 tooforce hello edge 서버 tooinitiate hello 원본 서버에서 hello 자산의 백그라운드 가져오기입니다. 그 후 hello 자산 hello 지 서버 로컬 캐시에 포함 됩니다.
사용 안 함|에 지 서버를 hello 자산에 대 한 백그라운드 가져오기를 수행할 수 없습니다. 즉, 해당 hello 다음 요청 edge 서버 toorequest 하면 해당 지역에서 해당 자산에 대 한 hello 고객 원본 서버에서 합니다.

**기본 동작**: 사용

###<a name="compress-file-types"></a>압축 파일 형식
**목적:** hello 서버에서 압축 되도록 하는 hello 파일 형식을 정의 합니다.

파일 형식은 인터넷 미디어 유형, 즉 Content-Type을 사용하여 지정할 수 있습니다. 인터넷 미디어 유형은 특정 자산 우리의 서버 tooidentify hello 파일 형식을 허용 하는 플랫폼 독립적 메타 데이터입니다. 일반적인 인터넷 미디어 유형 목록은 다음과 같습니다.

인터넷 미디어 유형|설명
--|--
텍스트/일반|일반 텍스트 파일
텍스트/html| HTML 파일
텍스트/css|CSS(스타일시트)
application/x-javascript|JavaScript
application/javascript|JavaScript
주요 정보:

- 각각 하나의 공백으로 구분하여 여러 인터넷 미디어 유형을 지정합니다. 
- 이 기능은 1MB 미만 크기의 자산만 압축합니다. 더 큰 자산은 서버에서 압축하지 않습니다.
- 이미지, 비디오 및 오디오 미디어 자산(예: JPG, MP3, MP4 등)과 같은 특정 유형의 콘텐츠는 이미 압축되어 있습니다. 이러한 유형의 자산을 추가로 압축해도 파일 크기가 크게 줄어들지는 않습니다. 따라서 이러한 유형의 자산에는 압축을 사용하지 않는 것이 좋습니다.
- 별표와 같은 와일드카드 문자는 지원되지 않습니다.
- 이 기능은 tooa 규칙을 추가 하기 전에 hello 플랫폼 toowhich이이 규칙은 적용에 대 한 압축 페이지 압축 사용 안 함 옵션 tooset 있는지 확인 합니다.

###<a name="default-internal-max-age"></a>기본 내부 Max-Age
**목적:** edge 서버 tooorigin 서버 캐시 유효성 재검사 Determines hello 기본 최대 처리 기간 간격입니다. 즉, 앞에 지 서버에 전달 하는 시간의 양을 hello는 캐시 된 자산 hello 원본 서버에 저장 된 hello 자산 일치 하는지 여부를 확인 합니다.

주요 정보:

- 이 작업은 Cache-Control 또는 Expires 헤더에 max-age 표시를 할당하지 않은 원본 서버의 응답에 대해서만 발생합니다.
- 이 작업은 캐시 가능하다고 간주되지 않는 자산에 대해서는 수행되지 않습니다.
- 이 작업에는 브라우저 tooedge 서버 캐시 revalidations 영향을 주지 않습니다. 이러한 유형의 revalidations 캐시 컨트롤에 의해 결정 됩니다 또는 Expires 헤더가 전송 toohello 브라우저 외부 Max-age 기능을 사용자 지정할 수 있습니다.
- 이 동작의 결과가 hello hello 응답 헤더 및 콘텐츠에에 지 서버에서 반환 된 hello 콘텐츠에 눈에 띄는 영향 필요는 없지만 것에 지 서버 tooyour 원본 서버에서 보낸 유효성 재검사 트래픽의 hello 금액에 영향을 미칠 수 있습니다.
- 이 기능은 다음과 같이 구성합니다.
    - 기본 내부 최대 보존 기간을 적용할 수 있는 hello 상태 코드를 선택 합니다.
    - 정수 값을 지정 하 고 다음을 선택 하는 원하는 시간 단위 (예: 초, 분, 시간 등) hello 합니다. 이 값 hello 기본 내부 최대 처리 기간 간격을 정의합니다.

- 설정 hello 시간 단위 너무 "Off"가 할당 Cache-control 또는 Expires 헤더에는 최대 기간 표시 할당 되지 않은 요청에 대 한 일의 기본 내부 최대 처리 기간 간격 합니다.
- 설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다. 
    - Edge 
    - Cname
    - 요청 헤더 리터럴
    - 요청 헤더 와일드카드
    - 요청 메서드
    - URL 쿼리 리터럴
    - URL 쿼리 와일드카드

**기본값:** 7일

###<a name="expires-header-treatment"></a>만료 헤더 처리
**목적:** 외부 Max-age 기능이 활성화 되어 있을 때에 지 서버에서 Expires 헤더의 hello 생성을 제어 합니다.

이 구성 유형은 tooplace hello 외부 Max-age 및 hello 만료 헤더 처리 기능에는 가장 쉬운 방법은 tooachieve hello 동일한 문에서 hello 합니다.

값|결과
--|--
덮어쓰기|해당 hello 다음 작업 수행을 확인 합니다.<br/>-Hello 원본 서버에 의해 생성 된 Expires 헤더를 덮어씁니다.<br/>-Hello 외부 Max-age 기능 toohello 응답에서 생성 된 Expires 헤더를 추가 합니다.
통과|Expires 헤더 hello 외부 Max-age 기능에 의해 생성 된 toohello 응답 하지 않습니다 추가 되어 있는지 확인 합니다. <br/> Expires 헤더 생성 하는 원본 서버 hello toohello 최종 사용자를 통해 전달 합니다. <br/>원본 서버 hello Expires 헤더로, 다음이 옵션을 생성 하지 않으므로 포함 될 수 있습니다 원인 hello 응답 헤더 toonot Expires 헤더입니다.
없는 경우 추가| Expires 헤더 hello 원본 서버에서 수신 되지 않았습니다,이 옵션 hello 외부 Max-age 기능에 의해 생성 된 Expires 헤더를 추가 합니다. 이 옵션은 모든 자산에 Expires 헤더를 할당하도록 하는 데 유용합니다.
제거| Expires 헤더 hello 헤더 응답에 포함 되는지 확인 합니다. Expires 헤더에 이미 할당 된 경우 다음 것에서 제거 됩니다 hello 헤더 응답 합니다.

**기본 동작:** 덮어쓰기

###<a name="external-max-age"></a>외부 Max-Age
**목적:** 브라우저 tooedge 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정 합니다. 즉, 새 버전의 자산을에 지 서버 hello 브라우저 전에 전달 하는 시간의 양을 확인할 수 있습니다.

이 기능을 사용 하면 캐시를 생성 합니다-제어: 최대-age 및 헤더는에 지 서버에서 만료 되 고 보내는 toohello HTTP 클라이언트입니다. 이러한 헤더는 기본적으로 hello 원본 서버에서 만든를 덮어쓰게 됩니다. 그러나 캐시 컨트롤 헤더 처리 및 헤더 처리 만료 기능 수 있습니다이 동작은 사용 되는 tooalter 수 있습니다.

주요 정보:

- 이 작업에 지 서버 tooorigin 서버 캐시 revalidations 영향을 주지 않습니다. 이러한 유형의 revalidations hello 원본 서버에서 받은 캐시-컨트롤/Expires 헤더에 의해 결정 됩니다 하 고는 기본 내부 Max-age 및 Force 내부 Max-age 기능으로 사용자 지정할 수 있습니다.
- 정수 값을 지정 하 고 hello 원하는 시간 단위 (예: 초, 분, 시간 등)를 선택 하 여이 기능을 구성 합니다.
- 이 기능은 tooa 음수 값을 설정 하면 우리의 edge 서버 toosend 캐시-제어: no-캐시 및 hello에 설정 된 만료 시간 각 응답 toohello 브라우저와 과거 합니다. HTTP 클라이언트 hello 응답을 캐시 하지 않습니다, 하지만이 설정은 edge 서버 기능 toocache hello 응답 hello 원본 서버에서 변경 되지 않습니다.
- 설정 hello 시간 단위 너무 "Off"는이 기능을 해제 합니다. Hello hello 원본 서버에 대 한 응답으로 캐시는 캐시-컨트롤/Expires 헤더 toohello 브라우저를 통해 전달 됩니다.

**기본 동작:** 끄기

###<a name="force-internal-max-age"></a>강제 내부 Max-Age
**목적:** edge 서버 tooorigin 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정 합니다. 즉, 앞에 지 서버에 전달 하는 시간의 양을 hello 캐시 된 자산 hello 원본 서버에 저장 된 hello 자산 일치 하는지 여부를 확인할 수 있습니다.

주요 정보:

- 이 기능은 Cache-control 또는 Expires 헤더는 원본 서버에서 생성 된에 정의 된 hello 최대 처리 기간 간격을 재정의 합니다.
- 이 기능은 브라우저 tooedge 서버 캐시 revalidations 영향을 주지 않습니다. 이러한 유형의 revalidations 캐시 컨트롤에 의해 결정 됩니다 또는 Expires 헤더가 toohello 브라우저를 전송 합니다.
- 이 기능에는 edge 서버 toohello 요청자에서 제공 하는 hello 응답에는 observable 효과가지 않습니다. 그러나 우리 지 서버 toohello 원본 서버에서 보낸 유효성 재검사 트래픽의 hello 금액에 영향을 미칠 수 것입니다.
- 이 기능은 다음과 같이 구성합니다.
    - 내부 최대 기간을 적용할 hello 상태 코드를 선택 합니다.
    - 정수 값을 지정 하 고 선택 하면 hello 원하는 시간 단위 (예: 초, 분, 시간 등). 이 값 hello 요청 최대 처리 기간 간격을 정의합니다.

- 설정 hello 시간 단위 너무 "Off"이이 기능이 해제 됩니다. 내부 최대 처리 기간 간격 toorequested 자산 할당 되지 않습니다. Hello 원래 머리글 캐싱 지침을 포함 하지 않으면 hello 자산 toohello 기본 내부 Max-age 기능에서 활성 설정에 따라 캐시 됩니다.
- 설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다. 
    - Edge 
    - Cname
    - 요청 헤더 리터럴
    - 요청 헤더 와일드카드
    - 요청 메서드
    - URL 쿼리 리터럴
    - URL 쿼리 와일드카드

**기본 동작:** 끄기

###<a name="h264-support-http-progressive-download"></a>H.264 지원(HTTP 점진적 다운로드)
**목적:** Determines hello 유형의 H.264 파일 형식을 사용 하는 toostream 수 있는 콘텐츠입니다.

주요 정보:

- 파일 확장명 옵션에서 허용되는 H.264 파일 이름 확장명의 공백으로 구분된 집합을 정의합니다. 파일 확장명 옵션 hello 기본 동작을 재정의 합니다. 이 옵션을 설정할 때 파일 이름 확장명을 포함하여 MP4 및 F4V 지원을 유지합니다. 
- 있는지 tooinclude 기간을 확인 하십시오. 각 파일 이름 확장명 (예:.mp4.f4v)를 지정 하는 경우.

**기본 동작:** HTTP 점진적 다운로드는 기본적으로 MP4 및 F4V 미디어를 지원합니다.

###<a name="honor-no-cache-request"></a>no-cache 요청 부여
**목적:** 여부는 HTTP 클라이언트의 캐시 없음 요청 toohello 원본 서버를 전달 됩니다 결정 합니다.

No 캐시 요청 발생 hello HTTP 클라이언트에서 캐시를 보낼 때-제어: no-캐시 및/또는 Pragma:no-hello HTTP 요청에 캐시 헤더입니다.

값|결과
--|--
사용|HTTP 클라이언트의 아니요 캐시 toobe 전달된 toohello 원본 서버를 요청 하 고 hello 원본 서버는 반환 hello 응답 헤더 및 hello 본문 hello 지 서버를 통해 백 toohello HTTP 클라이언트를 허용 합니다.
사용 안 함|Hello 기본 동작을 복원합니다. hello 기본 동작은 원본 서버에 toohello 전달을 tooprevent 아니요 캐시 요청입니다.

모든 프로덕션 트래픽에 대 한 것은 매우 tooleave 사용 하지 않도록 설정 하는 기본 상태에서이 기능을 권장 합니다. 그렇지 않은 경우 원본 서버에서 최종 사용자 웹 페이지를 새로 고칠 때 많은 아니요 캐시 요청을 실수로 트리거될 수 있습니다 보호 하지 않습니다 또는 hello에서 인기 있는 미디어 플레이어 있는 코딩 된 toosend 아니요 캐시 헤더 비디오 모든 요청에 합니다. 그럼에도 불구 하 고이 기능은 유용 tooapply toocertain 비-프로덕션 준비 수 또는 요청 시 hello 원본 서버에서 끌어온 순서 tooallow 새 콘텐츠 toobe에서 디렉터리를 테스트 합니다.

toothis 기능 인해 전달 toobe tooan 원본 서버는 TCP_Client_Refresh_Miss 허용 되는 요청에 대 한 보고 되는 hello 캐시 상태입니다. Hello 핵심 보고 모듈에서 사용할 수 있는 캐시 상태 보고서 캐시 상태에 의해 통계 정보를 제공 합니다. 이렇게 하면 tootrack hello 번호와 요청 비율을 toothis 기능 인해 tooan 원본 서버에 전달 되 고 있습니다.

**기본 동작**: 사용 안 함

###<a name="ignore-origin-no-cache"></a>원본 no-cache 무시
**목적:** 우리의 CDN은 hello 원본 서버에서 제공 하는 지시문 뒤를 무시 하는지 여부를 결정 합니다.

- Cache-Control: private
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

주요 정보:

- 공백으로 구분 된 목록이 지시문 위에 hello 무시 되는 상태 코드를 정의 하 여이 기능을 구성 합니다.
- hello이 기능에 대 한 유효한 상태 코드의 집합은: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, 및 505 합니다.
- Tooa 빈 값을 설정 하 여이 기능을 사용 하지 않도록 설정 합니다.
- 설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다. 
    - Edge 
    - Cname
    - 요청 헤더 리터럴
    - 요청 헤더 와일드카드
    - 요청 메서드
    - URL 쿼리 리터럴
    - URL 쿼리 와일드카드

**기본 동작:** 기본 동작은 지시문 위에 toohonor hello입니다.

###<a name="ignore-unsatisfiable-ranges"></a>적절하지 않은 범위 무시 
**목적:** hello 응답 반환 되는 tooclients 요청 요청한 범위가 충분 하지 않음 416 상태 코드를 생성 하는 경우를 결정 합니다.

기본적으로이 상태 코드는 바이트 범위 요청을에 지 서버에서 충족 되지 않습니다 및 If-range 요청 헤더 필드를 지정 하지 않았습니다 hello 지정 된 경우 반환 됩니다.

값|결과
-|-
사용|Edge 서버에서 요청한 범위가 충분 하지 않음 416 상태 코드로 응답 tooan 잘못 된 바이트 범위 요청을 방지합니다. 대신 서버 hello 요청한 자산 배달 하 고 200 OK hello 클라이언트로 반환 됩니다.
사용 안 함|Hello 기본 동작을 복원합니다. hello 기본 동작은 toohonor 요청한 범위가 충분 하지 않음 416 상태 코드입니다.

**기본 동작**: 사용 안 함

###<a name="internal-max-stale"></a>내부 Max-Stale
**목적:** hello에 지 서버는 없습니다 toorevalidate hello 때 캐시 된 자산에 지 서버에서 구현 될 수 있습니다 지난 hello 정상적으로 종료 시간 hello 원본 서버와 자산을 캐시 하는 기간을 제어 합니다.

일반적으로 자산 최대 처리 기간 시간이 만료 되 면 hello에 지 서버 유효성 재검사 요청 toohello 원본 서버를 전송 합니다. hello 원본 서버는 다음으로 응답 중 하나는 304 귀하에 게 hello에 지 서버 새로운 임대를 200으로 그렇지 않으면 hello 캐시 된 자산에 대해 확인 hello에 지 서버 hello 캐시 된 asset의 업데이트 된 버전 제공 수정 되지 않습니다.

Hello에 지 서버에 없습니다 tooestablish 이러한 유효성 재검사를 시도 하는 동안 hello 원본 서버와의 연결을 경우이 내부 최대 부실 기능에 지 서버 tooserve hello 지금 부실 자산 계속 수 있는지 여부와 시간, hello에 대 한 제어 다음 합니다.

Note hello 실패 한 유효성 재검사 발생 때가 아니라 hello 자산 최대 처리 기간 만료 되 면이 시간 간격은 시작 되도록 합니다. 따라서는 자산 제공 될 수 있지만 유효성 재검사 없이 hello 최대 기간은 경우 hello 시간 최대 처리 기간을 더한 최대 부실 hello 조합 하 여 지정 된 시간입니다. 예를 들어 자산에 실패 한 유효성을 다시 시도 9 시 30 분의 최대 기간 및 최대 부실 15 분에 캐시 된 경우 9시 44분 초래 최종 사용자 수신 hello 오래 된 캐시 된 자산을 9시 46분 한 실패 한 유효성을 다시 시도 초래 하는 동안 hello 최종 사용자 504 게이트웨이 시간 초과 수신 합니다.

캐시에 의해 교체 된이 기능에 대해 구성 된 모든 값-제어: 해야-유효성을 다시 검사 또는 캐시-제어: 프록시-hello 원본 서버에서 받은 헤더 다시 유효성을 검사 합니다. 이러한 헤더 중 하나는 자산의 캐시 처음 되 면 hello 원본 서버에서 수신 되 면 hello edge 서버에는 오래 된 캐시 된 자산 하지 처리 합니다. 이 경우 중이면 hello에 지 서버 hello 원점으로 수 없습니다 toorevalidate hello 자산 최대 처리 기간 간격이 만료 되 면 다음 hello에 지 서버는 반환 504 게이트웨이 시간 초과 합니다.

주요 정보:

- 이 기능은 다음과 같이 구성합니다.
    - 최대 부실 적용할 수 hello 상태 코드를 선택 합니다.
    - 정수 값을 지정 하 고 다음을 선택 하는 원하는 시간 단위 (예: 초, 분, 시간 등) hello 합니다. Hello 내부 최대-부실 적용 되는이 값을 정의 합니다.

- 설정 hello 시간 단위 너무 "Off"는이 기능을 해제 합니다. 캐시된 자산은 정상 만료 시간을 초과하여 처리되지 않습니다.
- 설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다. 
    - Edge 
    - Cname
    - 요청 헤더 리터럴
    - 요청 헤더 와일드카드
    - 요청 메서드
    - URL 쿼리 리터럴
    - URL 쿼리 와일드카드

**기본 동작:** 2분

###<a name="partial-cache-sharing"></a>부분 캐시 공유
**목적:** 요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있는지 여부를 결정합니다.

그런 다음이 부분 캐시는 hello 요청 콘텐츠가 캐시 되 고 완전 하 게 될 때까지 사용된 toofulfill 해당 콘텐츠에 대 한 새 요청을 수 있습니다.

값|결과
-|-
사용|요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있습니다.
사용 안 함|요청 캐시 된 완벽 하 게 생성할 수 버전의 hello 요청 되는 콘텐츠입니다.

**기본 동작**: 사용 안 함

###<a name="prevalidate-cached-content"></a>캐시된 콘텐츠 사전 유효성 검사
**목적:** TTL이 만료되기 전에 캐시된 콘텐츠가 초기 유효성 재검사에 적합한지 여부를 결정합니다.

Hello 이전 toohello 만료 요청 콘텐츠의 TTL는 초기 유효성 재검사 적격 됩니다 시간의 hello 크기를 정의 합니다.

주요 정보:

- 유효성 재검사 tootake 위치 hello 캐시 된 콘텐츠의 TTL이 만료 된 후 필요 "Off" hello 시간 단위로 선택 합니다. 시간은 지정하지 않아야 하며, 무시됩니다.

**기본 동작:** 끄기 유효성 재검사 hello 캐시 된 콘텐츠의 TTL이 만료 된 후 수행만 될 수 있습니다.

###<a name="refresh-zero-byte-cache-files"></a>0바이트 캐시 파일 새로 고침
**목적:** 에지 서버에서 0바이트 캐시 자산에 대한 HTTP 클라이언트 요청을 처리하는 방식을 결정합니다.

유효한 값은 다음과 같습니다.

값|결과
--|--
사용|Edge 서버 toore 인출 hello 자산 hello 원본 서버에서 발생합니다.
사용 안 함|Hello 기본 동작을 복원합니다. hello 기본 동작은 요청에 따라 올바른 캐시 자산을 tooserve입니다.
이 기능은 올바른 캐싱 및 콘텐츠 배달에는 필요하지 않지만 해결 방법으로는 유용할 수 있습니다. 예를 들어 원본 서버에서 동적 콘텐츠 생성기 toohello에 지 서버에 전송 되는 0 바이트 응답에서 실수로 발생할 수 있습니다. 이러한 유형의 응답은 일반적으로 에지 서버에서 캐시합니다. 0바이트 응답이 이러한 콘텐츠에 대해 유효한 응답이 아님을 알고 있는 경우 

신뢰할 수 없는 경우에 대 한 다음이 기능은 이러한 종류의 방지할 수 자산을 처리할 tooyour 클라이언트입니다.

**기본 동작**: 사용 안 함

###<a name="set-cacheable-status-codes"></a>캐시 가능한 상태 코드 집합
**목적:** 캐시 된 콘텐츠 발생할 수 있는 상태 코드의 hello 집합을 정의 합니다.

기본적으로 캐싱은 200 확인 응답에만 사용할 수 있습니다.

원하는 hello 상태 코드는 공백으로 구분 된 집합을 정의 합니다.

주요 정보:

- 원본 No-Cache 무시 기능도 활성화합니다. 해당 기능을 사용할 수 없으면 비 200 확인 응답이 캐시되지 않을 수 있습니다.
- hello이 기능에 대 한 유효한 상태 코드의 집합은: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, 및 505 합니다.
- 이 기능에는 200 OK 상태 코드를 생성 하는 응답에 대 한 캐싱을 사용 하는 toodisable 일 수 없습니다.

**기본 동작:** 캐싱은 200 확인 상태 코드를 생성하는 응답에만 사용할 수 있습니다.
###<a name="stale-content-delivery-on-error"></a>오류 시 오래된 콘텐츠 배달
**목적:** 

캐시 유효성 재검사 중 또는 검색 하는 동안 hello hello 고객 원본 서버에서 콘텐츠를 요청 하면 오류가 발생할 때 배달 될 캐시 된 콘텐츠 만료 여부를 확인 합니다.

값|결과
-|-
사용|오래 된 콘텐츠는 제공 toohello 요청자 연결 tooan 원본 서버는 동안 오류가 발생 하는 경우.
사용 안 함|hello 원본 서버 오류 toohello 요청자에 게를 전달 됩니다.

**기본 동작:** 사용 안 함

###<a name="stale-while-revalidate"></a>유효성 재검사 중 기한 경과
**목적:** edge 서버 tooserve 부실 콘텐츠 toohello 요청자 유효성 재검사 수행 하는 동안 허용 하 여 성능이 향상 됩니다.

주요 정보:

- 이 기능의 hello 동작 toohello 선택한 시간 단위에 따라 달라 집니다.
    - **시간 단위:** 시간의 길이 지정 하 고 시간 단위 (예: 초, 분, 시간 등) tooallow 부실 콘텐츠 배달을 선택 합니다. 이 유형의 설치 프로그램을 허용 배달할 수 있는 시간의 hello CDN tooextend hello 길이 콘텐츠 다음 수식을 toohello에 따라 유효성 검사를 요구 하기 전에:**TTL** + **부실 하는 동안 유효성을 다시 검사 시간** 
    - **Off:** 불완전 한 콘텐츠 구현 될 수 있습니다에 대 한 "Off" 요청 하기 전에 toorequire 유효성 재검사를 선택 합니다.
        - 기간은 적용할 수 없으므로 지정하지 않아야 하며, 무시됩니다.

**기본 동작:** 끄기 유효성 재검사 hello 콘텐츠 제공 될 수 있지만 요청 하기 전에 수행 해야 합니다.

###<a name="comment"></a>주석
**목적:** 규칙 내에서 추가 참고 toobe 허용 합니다.

규칙의 일반적인 용도로 hello tooprovide 추가 정보는 하는이 기능에 대 한 사용 되었거나, 특정 조건 또는 기능을 일치 하는 이유 toohello 규칙 추가 합니다.

주요 정보:

- 최대 150자를 지정할 수 있습니다.
- 영숫자를 사용 하는지 tooonly를 확인 합니다.
- 이 기능은 hello 규칙의 hello 동작에 영향을 주지 않습니다. 단순히 말로 tooprovide 또는 나중에 참조할 수에 대 한 정보를 제공할 수 있는 영역 hello 규칙 문제를 해결할 때 도움이 될 수 있습니다.
 
## <a name="headers"></a>헤더

이러한 기능을 디자인 된 tooadd, 수정 또는 hello 요청 또는 응답에서 헤더를 삭제 합니다.

이름 | 목적
-----|--------
Age 응답 헤더 | Age 응답 헤더 toohello 요청자에 게 전송 하는 hello 응답에 포함될지 여부를 결정 합니다.
디버그 캐시 응답 헤더 | 응답 hello 요청 된 자산에 대 한 캐시 정책을 hello에 정보를 제공 하는 hello EC-X-debug 응답 헤더에 포함 될 수 있습니다 있는지 여부를 결정 합니다.
클라이언트 요청 헤더 수정 | 요청에서 헤더를 덮어쓰기, 추가 또는 삭제합니다.
클라이언트 응답 헤더 수정 | 응답에서 헤더를 덮어쓰기, 추가 또는 삭제합니다.
클라이언트 IP 사용자 지정 헤더 설정 | 사용자 지정 요청 헤더로 hello 요청 클라이언트의 IP 주소 hello toobe 추가 toohello 요청을 허용 합니다.

###<a name="age-response-header"></a>Age 응답 헤더
**용도**: Age 응답 헤더를 보낸 응답 toohello 요청자 hello에에서 포함될지 여부를 결정 합니다.
값|결과
--|--
사용 | hello Age 응답 헤더 toohello 요청자에 게 전송 하는 hello 응답에 포함 됩니다.
사용 안 함 | hello Age 응답 헤더 toohello 요청자에 게 전송 하는 hello 응답에서 제외 됩니다.

**기본 동작**: 사용 안 함

###<a name="debug-cache-response-headers"></a>디버그 캐시 응답 헤더
**목적:** 응답 hello 요청 된 자산에 대 한 캐시 정책을 hello에 정보를 제공 하는 X-EC-디버그 응답 헤더에 포함 될 수 있습니다 있는지 여부를 결정 합니다.

디버그에서 캐시 응답 헤더 모두 hello 다음에 해당할 때 hello 응답에 포함 됩니다.

- hello 원하는 요청에서 hello 디버그 캐시 응답 헤더 기능을 사용 합니다.
- 요청 위에 hello hello 응답에 포함 되어야 디버그 캐시 응답 헤더의 hello 집합을 정의 합니다.

캐시 응답 헤더를 헤더 뒤에 오는 hello를 포함 하 여 요청할 수 있습니다 및 hello 요청에서 원하는 지시문 hello 디버그:

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**예제:**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

값|결과
-|-
사용|디버그 캐시 응답 헤더에 대한 요청에서 X-EC-Debug 헤더를 포함한 응답을 반환합니다.
사용 안 함|X-EC-디버그 응답 헤더는 hello 응답에서 제외 됩니다.

**기본 동작**: 사용 안 함

###<a name="modify-client-response-header"></a>클라이언트 응답 헤더 수정
**목적:** 각 요청에는 이를 설명하는 [요청 헤더]() 집합이 있습니다. 이 기능은 다음 중 하나를 수행할 수 있습니다.

- 뒤에 추가 또는 tooa 요청 헤더를 할당 하는 hello 값을 덮어씁니다. 지정 된 요청 헤더 hello가 없는 경우 다음이 기능은 추가 됩니다 toohello 요청.
- Hello 요청에서 요청 헤더를 삭제 합니다.

Tooan 원본 서버에 전달 된 요청에는이 기능을 통해 변경 하는 hello 반영 됩니다.

요청 헤더에 hello 다음 동작 중 하나를 수행할 수 있습니다.

옵션|설명|예
-|-|-
추가|hello는 toend hello 기존 요청 헤더 값의 값이 추가 되 지정 합니다.|**요청 헤더 값(클라이언트):** Value1 <br/> **요청 헤더 값(HTTP 규칙 엔진):** Value2 <br/>**새 요청 헤더 값:** Value1Value2
덮어쓰기|값을 지정 하는 hello 요청 헤더 값 집합 toohello 됩니다.|**요청 헤더 값(클라이언트):** Value1 <br/>**요청 헤더 값(HTTP 규칙 엔진):** Value2 <br/>**새 요청 헤더 값:** Value2 <br/>
삭제|Hello 지정 된 요청 헤더를 삭제합니다.|**요청 헤더 값(클라이언트):** Value1 <br/> **클라이언트 요청 헤더 구성 수정:** Delete hello 요청 헤더에 있습니다. <br/>**결과:** hello를 지정 된 요청 헤더 toohello 원본 서버에 전달 되지 것입니다.

주요 정보:

- Name 옵션에 지정 된 hello 값 hello 원하는 요청 헤더에 대 한 정확 하 게 일치 인지 확인 합니다.
- 대/소문자가 헤더를 식별 하는 데 hello 목적을 위해 계정에 작성 되지 않습니다. 예를 들어 모든 변형 된 캐시 제어 헤더 이름 다음 hello 사용된 tooidentify를 지정할 수 있으며 해당:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- 있는지 tooonly 헤더 이름을 지정할 때 영숫자 문자, 대시 또는 밑줄만 사용 하 여 확인 합니다.
- 헤더는 삭제를 tooan 원본 서버는에 지 서버에서 전달 되지 것입니다.
- hello 다음 헤더 예약 되어 있으므로이 기능을 통해 수정할 수 없습니다.
    - forwarded
    - host
    - via
    - Warning
    - x-forwarded-for
    - "x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.

###<a name="modify-client-response-header"></a>클라이언트 응답 헤더 수정
각 응답에는 이를 설명하는 [응답 헤더]() 집합이 있습니다. 이 기능은 다음 중 하나를 수행할 수 있습니다.

- 뒤에 추가 또는 tooa 응답 헤더를 할당 하는 hello 값을 덮어씁니다. Hello 지정 된 요청 헤더가 없는 경우 다음이 기능은 됩니다 추가 toohello 응답 합니다.
- Hello 응답에서 응답 헤더를 삭제 합니다.

기본적으로 응답 헤더 값은 원본 서버 및 에지 서버에서 정의합니다.

응답 헤더에서 동작을 수행 하는 hello 중 하나를 수행할 수 있습니다.

옵션|설명|예
-|-|-
추가|hello는 toend hello 기존 요청 헤더 값의 값이 추가 되 지정 합니다.|**응답 헤더 값(클라이언트):** Value1 <br/> **응답 헤더 값(HTTP 규칙 엔진):** Value2 <br/>**새 응답 헤더 값:** Value1Value2
덮어쓰기|값을 지정 하는 hello 요청 헤더 값 집합 toohello 됩니다.|**응답 헤더 값(클라이언트):** Value1 <br/>**응답 헤더 값(HTTP 규칙 엔진):** Value2 <br/>**새 응답 헤더 값:** Value2 <br/>
삭제|Hello 지정 된 요청 헤더를 삭제합니다.|**요청 헤더 값(클라이언트):** Value1 <br/> **클라이언트 요청 헤더 구성 수정:** Delete hello 응답 헤더에 있습니다. <br/>**결과:** hello를 지정 된 응답 헤더 toohello 요청자에 게 전달 되지 것입니다.

주요 정보:

- Name 옵션에 지정 된 hello 값 hello 원하는 응답 헤더에 대 한 정확 하 게 일치 인지 확인 합니다. 
- 대/소문자가 헤더를 식별 하는 데 hello 목적을 위해 계정에 작성 되지 않습니다. 예를 들어 모든 변형 된 캐시 제어 헤더 이름 다음 hello 사용된 tooidentify를 지정할 수 있으며 해당:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- 헤더는 삭제를 toohello 요청자에 게 전달 되지 것입니다.
- hello 다음 헤더 예약 되어 있으므로이 기능을 통해 수정할 수 없습니다.
    - accept-encoding
    - age
    - connection
    - content-encoding
    - content-length
    - content-range
    - date
    - server
    - trailer
    - transfer-encoding
    - 업그레이드
    - vary
    - via
    - Warning
    - "x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.

###<a name="set-client-ip-custom-header"></a>클라이언트 IP 사용자 지정 헤더 설정
**목적:** IP 주소 toohello 요청 하 여 hello 요청 하는 클라이언트를 식별 하는 사용자 지정 헤더를 추가 합니다.

헤더 이름 옵션에는 hello 클라이언트의 IP 주소를 저장할 hello 사용자 지정 요청 헤더의 hello 이름을 정의 합니다.

이 기능을 사용 하는 고객 원본 서버 toofind 클라이언트 IP 주소는 사용자 지정 요청 헤더를 통해 아웃 합니다. Hello 요청을 캐시에서 서비스 하는 경우 원본 서버 hello hello 클라이언트의 IP 주소의 알림을 받지 못합니다. 따라서 이 기능은 캐시되지 않는 ADN 또는 자산과 함께 사용하는 것이 좋습니다.

해당 hello 지정 된 헤더 이름이 hello 다음 중 하나라도 일치 하지 않습니다 확인 하십시오.

- 표준 요청 헤더 이름 - 표준 헤더 이름 목록은 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)에 있습니다.
- 예약된 헤더 이름
    - forwarded-for
    - host
    - vary
    - via
    - Warning
    - x-forwarded-for
    - "x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.
 
## <a name="logs"></a>로그

이러한 기능은 원시 로그 파일에 저장 된 디자인 된 toocustomize hello 데이터에 설명 합니다.

이름 | 목적
-----|--------
사용자 지정 로그 필드 1 | Hello 형식과 원시 로그 파일의 사용자 지정 로그 필드 toohello 할당할 수 있는 hello 내용을 결정 합니다.
로그 쿼리 문자열 | 쿼리 문자열 hello URL 액세스 로그에 함께 저장 하는지 여부를 결정 합니다.

###<a name="custom-log-field-1"></a>사용자 지정 로그 필드 1
**목적:** hello 형식과 원시 로그 파일의 사용자 지정 로그 필드 toohello 할당할 수 있는 hello 내용을 결정 합니다.

이 사용자 정의 필드 뒤에 있는 주요 목적은 hello는 tooallow toodetermine 요청 및 응답 헤더 값을 로그 파일에 저장 됩니다.

기본적으로 사용자 지정 로그 필드 hello 라고 "x-ec_custom-1". 그러나이 필드의 hello 이름을 사용자 지정할 수에서 [원시 로그 설정 페이지]()합니다.

hello toospecify 요청 및 응답 헤더를 사용 해야 하는 서식 지정 아래 정의 되어 있습니다.

헤더 형식|형식|예
-|-|-
요청 헤더|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
응답 헤더|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

주요 정보:

- 사용자 지정 로그 필드는 헤더 필드와 일반 텍스트의 조합을 포함할 수 있습니다.
- 이 필드에 유효한 문자는 hello 다음: 영숫자 (즉, 0-9, a-z 및 A-z), 콜론, 세미콜론, 아포스트로피, 쉼표, 마침표, 밑줄, 등호, 괄호, 대괄호, 대시와 공백의 합니다. hello 백분율 기호와 중괄호만 허용 됩니다 때 toospecify 헤더 필드를 사용 합니다.
- 각 지정 된 헤더 필드에 대 한 hello 맞춤법 hello 원하는 요청/응답 헤더 이름이 일치 해야 합니다.
- Toospecify 원하는 경우 여러 헤더 이면 것이 좋습니다를 사용 하는 구분 기호 tooindicate 각 헤더입니다. 예를 들어 각 헤더에 약어를 사용할 수 있습니다. 샘플 구문은 다음과 같습니다.
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**기본값:** -

###<a name="log-query-string"></a>로그 쿼리 문자열
**목적:** 쿼리 문자열 hello URL 액세스 로그에 함께 저장 하는지 여부를 결정 합니다.

값|결과
-|-
사용|Url 액세스 로그에 기록할 때 쿼리 문자열의 hello 저장소를 수 있습니다. URL에 쿼리 문자열이 없으면 이 옵션이 적용되지 않습니다.
사용 안 함|Hello 기본 동작을 복원합니다. hello 기본 동작은 Url 액세스 로그에 기록할 때 tooignore 쿼리 문자열입니다.

**기본 동작**: 사용 안 함

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>원본

이러한 기능은 디자인 된 toocontrol hello CDN 원본 서버와 통신 하는 방법에 대해 설명 합니다.

이름 | 목적
-----|--------
최대 연결 유지 요청 | 닫 혔 기 전에 hello 유지 연결에 대 한 요청의 최대 수를 정의 합니다.
프록시 특별 헤더 | Hello에 지 서버 tooan 원본 서버에서 전달 하는 CDN에 관련 된 요청 헤더 집합을 정의 합니다.


###<a name="maximum-keep-alive-requests"></a>최대 연결 유지 요청
**목적:** 연결이 닫히기 전에 hello 유지 연결에 대 한 요청의 최대 수를 정의 합니다.

Hello 요청 tooa 낮은 값의 최대 수를 설정 하는 것이 좋습니다 및 성능이 저하 될 수 있습니다.

주요 정보:

- 이 값은 0을 포함한 양의 정수로 지정합니다.
- 지정 된 hello에 쉼표 또는 마침표를 포함 하지 마십시오 값입니다.

**기본값:** 10,000개 요청

###<a name="proxy-special-headers"></a>프록시 특별 헤더
**목적:** hello 집합 정의 [CDN에 관련 된 요청 헤더]() 는 지 서버 tooan 원본 서버에서 전달 됩니다.

주요 정보:

- 이 기능에 정의 된 각 특정 CDN 요청 헤더 tooan 원본 서버에 전달 됩니다.
- 이 목록에서 제거 하 여 원본 서버에 tooan 전달을 특정 CDN 요청 헤더를 방지 합니다.

**기본 동작:** 모든 [CDN에 관련 된 요청 헤더]() toohello 원본 서버에 전달 됩니다.

## <a name="specialty"></a>특별 사항

이러한 기능은 고급 사용자만 사용해야 하는 고급 기능을 제공합니다.

이름 | 목적
-----|--------
캐시 가능한 HTTP 메서드 | Hello 네트워크에 캐시 될 수 있는 추가 HTTP 메서드 집합을 결정 합니다.
캐시 가능한 요청 본문 크기 | POST 응답을 캐시할 수 있는지 여부를 확인 하기 위한 hello 임계값을 정의 합니다.

###<a name="cacheable-http-methods"></a>캐시 가능한 HTTP 메서드
**목적:** hello 네트워크에 캐시 될 수 있는 추가 HTTP 메서드 집합을 결정 합니다.

주요 정보:

- 이 기능은 GET 응답을 항상 캐시해야 한다고 가정합니다. 결과적으로, hello GET HTTP 메서드 설정이 기능이 포함 되지 않아야 합니다.
- 이 기능은 hello POST HTTP 메서드를 지원합니다. 이 기능을 :POST로 설정하여 POST 응답 캐싱을 활성화합니다. 
- 기본적으로 본문이 14Kb 미만인 요청만 캐시됩니다. Hello 최대 요청 본문 크기를 설정 하려면 캐시 가능한 요청 본문 크기 기능을 사용 합니다.

**기본 동작:** GET 응답만 캐시됩니다.

###<a name="cacheable-request-body-size"></a>캐시 가능한 요청 본문 크기

**목적:** POST 응답을 캐시할 수 있는지 여부를 확인 하기 위한 hello 임계값을 정의 합니다.

이 임계값은 최대 요청 본문 크기를 지정하여 결정됩니다. 더 큰 요청 본문을 포함한 요청은 캐시되지 않습니다.

주요 정보:

- POST 응답이 캐싱에 적합한 경우에만 이 기능을 적용할 수 있습니다. Hello 캐시 가능한 HTTP 메서드에 기능을 사용 하 여 POST 요청 캐싱을 사용 하도록 설정 합니다.
- hello 요청 본문에 대 한에 사용 됩니다.
    - x-www-form-urlencoded 값
    - 고유한 cache-key 보장
- 최대 요청 본문 크기를 크게 정의하면 데이터 전달 성능에 영향을 줄 수 있습니다.
    - **권장되는 값:** 14Kb
    - **최소값:** 1Kb

**기본 동작:** 14Kb
 
## <a name="url"></a>URL

이러한 기능을 통해 요청 toobe 리디렉션되거나 tooa 다른 URL을 다시 작성 합니다.

이름 | 목적
-----|--------
리디렉션 추적 | 요청 고객 원본 서버에서 반환 되는 hello 위치 헤더에 정의 된 리디렉션된 toohello hostname 수 있는지 여부를 결정 합니다.
URL 리디렉션 | Hello 위치 헤더를 통해 요청을 리디렉션합니다.
URL 다시 쓰기  | Hello 요청 URL을 다시 작성합니다.

###<a name="follow-redirects"></a>리디렉션 추적
**목적:** 요청 하는 고객 원본 서버에서 반환 되는 위치 헤더에 정의 된 리디렉션된 toohello hostname이 될 수 있는지 여부를 결정 합니다.

주요 정보:

- 요청에 리디렉션된 tooedge CNAMEs toohello 해당 하는 수만 있습니다 동일한 플랫폼입니다.

값|결과
-|-
사용|요청을 리디렉션할 수 있습니다.
사용 안 함|요청을 리디렉션하지 않습니다.

**기본 동작**: 사용 안 함
###<a name="url-redirect"></a>URL 리디렉션
**목적:** Location 헤더를 통해 요청을 리디렉션합니다.

이 기능의 hello 구성 hello 다음 옵션을 설정 하는 사항이 필요 합니다.

옵션|설명
-|-
코드|Toohello 요청자에 게 반환 되는 hello 응답 코드를 선택 합니다.
원본 및 패턴| 이러한 설정은 트리로 이동 될 수 있는 요청 hello 형식을 식별 하는 요청 URI 패턴을 정의 합니다. URL의 기준에 따라 hello 둘 모두를 충족 하는 유일한 요청이 리디렉션됩니다. <br/> <br/> **원본:**(또는 콘텐츠 액세스 지점) 원본 서버를 식별하는 상대 경로를 선택합니다. 이것이 hello "/XXXX/" 섹션 및 끝점 이름입니다. <br/> **원본(패턴):** 상대 경로로 요청을 식별하는 패턴을 정의해야 합니다. 이 정규식 패턴 hello 이전에 콘텐츠 액세스 지점 (위 참조)를 선택한 후 바로 시작 하는 경로 정의 해야 합니다. <br/> -있는지 확인 하십시오 (즉, 소스 및 패턴) hello 요청 URI 조건 위에 정의 된는이 기능에 대해 정의 된 모든 일치 조건을 충돌 하지 않습니다. <br/> -있는지 toospecify 패턴을 확인 합니다. Hello 패턴으로 빈 값을 사용 하 여 요청 toohello 서버의 루트 폴더에 hello 선택한 원본 (예: http://cdn.mydomain.com/)만 일치 합니다.
대상| Hello URL은 정의 요청 위에 toowhich hello를 이동 합니다. <br/> 다음을 사용하여 이 URL을 동적으로 구성합니다. <br/> - 정규식 패턴 <br/>- HTTP 변수 <br/> $를 사용 하 여 hello 대상 패턴에 캡처되며, hello 소스 패턴에서 hello 값으로 대체 _n_  여기서  _n_  캡처되는 hello 순서에 따라 값을 식별 합니다. 예를 들어 $1 hello $2 hello 두 번째 값을 나타내는 동안 hello 소스 패턴에서 캡처되는 첫 번째 값을 나타냅니다. <br/> 
이 뛰어납니다 toouse 절대 URL을 권장 합니다. 상대 URL의 hello 사용 CDN Url tooan 잘못 된 경로 리디렉션할 수 있습니다.

**샘플 시나리오**

이 예제에서는 보여 줍니다 tooredirect 가장자리 toothis 확인 되는 CNAME URL의 CDN URL 기본 방법: http://marketing.azureedge.net/brochures

기본 가장자리 CNAME URL 리디렉션된 toothis 됩니다 요청을 한 정하는: http://cdn.mydomain.com/resources

이 URL 리디렉션 같은 구성이 hello를 통해 수행할 수 있습니다.![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**주요 정보:**

- hello URL 리디렉션 기능 정의 hello 요청 리디렉션될 Url입니다. 따라서 추가적인 일치 조건이 필요하지 않습니다. Hello 일치 조건을 "Always"로 정의 되지만 해당 지점 toohello "브로슈어" hello "마케팅" 고객 원본에 대 한 폴더 리디렉션 됨 권한만 요청 합니다. 
- 일치 하는 모든 요청에 리디렉션된 toohello 가장자리 CNAME URL 대상 옵션에서 정의 됩니다. 
    - 샘플 시나리오 #1: 
        - 샘플 요청(CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf 
        - 요청 URL(리디렉션 이후): http://cdn.mydomain.com/resources/widgets.pdf  
    - 샘플 시나리오 2: 
        - 샘플 요청(에지 CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf 
        - 요청 URL(리디렉션 이후): http://cdn.mydomain.com/resources/widgets.pdf 샘플 시나리오
    - 샘플 시나리오 #3: 
        - 샘플 요청(에지 CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - 요청 URL(리디렉션 이후):: http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- hello 요청 체계 (% {scheme}) 변수는 대상 옵션에서 활용 했습니다. 이렇게 하면 해당 hello 요청 체계 리디렉션 후 변경 되지 않습니다.
- hello 요청에서 캡처된 hello URL 세그먼트는 "$1."를 통해 추가 된 toohello 새 URL
 
###<a name="url-rewrite"></a>URL 다시 쓰기
**목적:** hello 요청 URL을 다시 작성 합니다.

주요 정보:

- 이 기능의 hello 구성 hello 다음 옵션을 설정 하는 사항이 필요 합니다.

옵션|설명
-|-
 원본 및 패턴 | 이러한 설정은 다시 작성 하는 요청의 hello 형식을 식별 하는 요청 URI 패턴을 정의 합니다. URL의 기준에 따라 hello 둘 모두를 충족 하는 유일한 요청 다시 작성 됩니다. <br/>     - **원본(또는 콘텐츠 액세스 지점):** 원본 서버를 식별하는 상대 경로를 선택합니다. 이것이 hello "/XXXX/" 섹션 및 끝점 이름입니다. <br/> - **원본(패턴):** 상대 경로로 요청을 식별하는 패턴을 정의해야 합니다. 이 정규식 패턴 hello 이전에 콘텐츠 액세스 지점 (위 참조)를 선택한 후 바로 시작 하는 경로 정의 해야 합니다. <br/> Hello 요청 URI 조건 (예: 소스 및 패턴) 위에 정의 된이 기능에 대해 정의 된 hello 일치 조건 중 하나라도와 충돌 하지 있는지 확인 합니다. 있는지 toospecify 패턴을 확인 합니다. Hello 패턴으로 빈 값을 사용 하 여 요청 toohello 서버의 루트 폴더에 hello 선택한 원본 (예: http://cdn.mydomain.com/)만 일치 합니다. 
 대상  |Hello 상대 URL을 정의 하 여 요청 위에 toowhich hello를 다시 작성 됩니다. <br/>    1. 원본 서버를 식별하는 콘텐츠 액세스 지점 선택 <br/>    2. 다음을 사용하여 상대 경로 정의 <br/>        - 정규식 패턴 <br/>        - HTTP 변수 <br/> <br/> $를 사용 하 여 hello 대상 패턴에 캡처되며, hello 소스 패턴에서 hello 값으로 대체 _n_  여기서  _n_  캡처되는 hello 순서에 따라 값을 식별 합니다. 예를 들어 $1 hello $2 hello 두 번째 값을 나타내는 동안 hello 소스 패턴에서 캡처되는 첫 번째 값을 나타냅니다. 
 이 기능 edge 서버 toorewrite hello URL을 기존의 리디렉션을 수행 하지 않고 있습니다. 즉, 해당 hello 요청자 hello hello를 다시 작성 URL에 요청 하는 경우 같은 응답 코드를 받게 됩니다.

**샘플 시나리오 1**

이 예제에서는 보여 줍니다 tooredirect 가장자리 toothis 확인 되는 CNAME URL의 CDN URL 기본 방법: http://marketing.azureedge.net/brochures/

기본 가장자리 CNAME URL 리디렉션된 toothis 됩니다 요청을 한 정하는: http://MyOrigin.azureedge.net/resources/

이 URL 리디렉션 같은 구성이 hello를 통해 수행할 수 있습니다.![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**샘플 시나리오 2**

이 예에서 보여 드리겠습니다 방법을 tooredirect 정규식을 사용 하는 대문자 toolowercase에서 CNAME URL 형성 합니다.

이 URL 리디렉션 같은 구성이 hello를 통해 수행할 수 있습니다.![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**주요 정보:**

- hello URL 재작성 기능 hello을 정의 하는 다시 작성 하는 Url을 요청 합니다. 따라서 추가적인 일치 조건이 필요하지 않습니다. Hello 일치 조건을 "Always"로 정의 되지만 해당 지점 toohello "브로슈어" hello "마케팅" 고객 원본에 대 한 폴더를 다시 작성 됩니다 권한만 요청 합니다.

- hello 요청에서 캡처된 hello URL 세그먼트는 "$1."를 통해 추가 된 toohello 새 URL



###<a name="compatibility"></a>호환성

이 기능이 적용 된 tooa 요청 수 전에 충족 해야 하는 조건과 일치 하는 것을 포함 합니다. 충돌 하는 조건에 맞는를 순서 tooprevent 설정,이 기능은 일치 조건을 다음 hello와 호환 되지 않습니다.

- AS 숫자
- CDN 원본
- 클라이언트 IP 주소
- 고객 원본
- 요청 스키마
- URL 경로 디렉터리
- URL 경로 확장
- URL 경로 파일 이름
- URL 경로 리터럴
- URL 경로 Regex
- URL 경로 와일드카드
- URL 쿼리 리터럴
- URL 쿼리 매개 변수
- URL 쿼리 Regex
- URL 쿼리 와일드카드


## <a name="next-steps"></a>다음 단계
* [규칙 엔진 참조](cdn-rules-engine-reference.md)
* [규칙 엔진 조건식](cdn-rules-engine-reference-conditional-expressions.md)
* [규칙 엔진 일치 조건](cdn-rules-engine-reference-match-conditions.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)
* [Azure CDN 개요](cdn-overview.md)
