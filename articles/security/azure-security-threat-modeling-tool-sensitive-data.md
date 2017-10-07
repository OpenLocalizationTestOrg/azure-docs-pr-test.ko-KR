---
title: "데이터-Microsoft 위협 모델링 도구-Azure aaaSensitive | Microsoft Docs"
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>보안 프레임: 중요한 데이터 | Mitigations 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **컴퓨터 신뢰 경계** | <ul><li>[중요한 정보가 포함된 경우 바이너리는 난독 처리되었는지 확인](#binaries-info)</li><li>[사용 되는 tooprotect 기밀 사용자 고유의 데이터는 암호화 EFS (파일 시스템)를 사용 하 여 하는 것이 좋습니다.](#efs-user)</li><li>[Hello 응용 프로그램 hello 파일 시스템에 저장 된 중요 한 데이터 암호화 되었는지 확인](#filesystem)</li></ul> | 
| **웹 응용 프로그램** | <ul><li>[Hello 브라우저에 중요 한 콘텐츠가 캐시 되지 않았다고 확인](#cache-browser)</li><li>[중요한 데이터가 포함된 Web App의 구성 파일의 섹션 암호화](#encrypt-data)</li><li>[중요 한 양식과 입력에 hello 자동 완성 HTML 특성을 명시적으로 해제 합니다.](#autocomplete-input)</li><li>[Hello 사용자 화면에 표시 되는 중요 한 데이터 마스크 되어 있는지 확인 하십시오.](#data-mask)</li></ul> | 
| **데이터베이스** | <ul><li>[동적 데이터 마스킹 toolimit 중요 한 데이터 노출을 아닌 권한 있는 사용자가 구현 합니다.](#dynamic-users)</li><li>[암호가 솔트된 해시 형식으로 저장되었는지 확인](#salted-hash)</li><li>[데이터베이스 열의 중요한 데이터가 암호화되었는지 확인](#db-encrypted)</li><li>[TDE(데이터베이스 수준 암호화)가 활성화되어 있는지 확인](#tde-enabled)</li><li>[데이터베이스 백업이 암호화되었는지 확인](#backup)</li></ul> | 
| **앱 API** | <ul><li>[API 브라우저의 저장소에 저장 되지 않으므로 해당 중요 한 데이터 관련 tooWeb 확인](#api-browser)</li></ul> | 
| Azure Document DB | <ul><li>[DocumentDB에 저장된 중요한 데이터 암호화](#encrypt-docdb)</li></ul> | 
| **Azure IaaS VM 신뢰 경계** | <ul><li>[가상 컴퓨터에서 사용 하는 Azure 디스크 암호화 tooencrypt 디스크 사용](#disk-vm)</li></ul> | 
| **Service Fabric 신뢰 경계** | <ul><li>[Service Fabric 응용 프로그램에서 암호 암호화](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[보안 모델링 수행 및 필요한 경우 비즈니스 단위/팀 사용](#modeling-teams)</li><li>[중요 한 엔터티에 대 한 액세스 tooshare 기능 최소화](#entities)</li><li>[Hello Dynamics CRM 공유 기능 및 보안 사례와 관련 된 hello 위험에 사용자가 기차](#good-practices)</li><li>[예외 관리에서 구성 세부 정보를 표시하는 금지된 개발 표준 규칙 포함](#exception-mgmt)</li></ul> | 
| **Azure 저장소** | <ul><li>[미사용 데이터에 대한 Azure Storage 서비스 암호화(SSE) 사용(미리 보기)](#sse-preview)</li><li>[Azure 저장소에 클라이언트 쪽 암호화 toostore 중요 한 데이터를 사용 하 여](#client-storage)</li></ul> | 
| **모바일 클라이언트** | <ul><li>[구분 또는 toophones 로컬 저장소를 작성 하는 PII 데이터 암호화](#pii-phones)</li><li>[Tooend 사용자가 배포 하기 전에 생성 된 바이너리를 난독 처리](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[집합 clientCredentialType tooCertificate 또는 Windows](#cert)</li><li>[WCF 보안 모드가 활성화되지 않음](#security)</li></ul> | 

## <a id="binaries-info"></a>중요한 정보가 포함된 경우 바이너리는 난독 처리되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 이진 파일이 영업 비밀인 뒤바뀌어서는 안되는 중요한 비즈니스 논리와 같은 중요한 정보를 포함하는 경우 난독 처리되어야 합니다. 이 toostop를 리버스 엔지니어링 어셈블리입니다. 이 목적을 위해 `CryptoObfuscator`와 같은 도구를 사용할 수 있습니다. |

## <a id="efs-user"></a>사용 되는 tooprotect 기밀 사용자 고유의 데이터는 암호화 EFS (파일 시스템)를 사용 하 여 하는 것이 좋습니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 사용 되는 tooprotect 물리적으로 액세스 toohello 컴퓨터와 악의적 사용자 기밀 사용자 고유의 데이터는 암호화 EFS (파일 시스템)를 사용 하는 것이 좋습니다. |

## <a id="filesystem"></a>Hello 응용 프로그램 hello 파일 시스템에 저장 된 중요 한 데이터 암호화 되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello 응용 프로그램 hello 파일 시스템에 저장 된 중요 한 데이터 암호화 되었는지 확인 (DPAPI 사용 예:), EFS를 적용할 수 없는 경우 |

## <a id="cache-browser"></a>Hello 브라우저에 중요 한 콘텐츠가 캐시 되지 않았다고 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, Web Forms, MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 브라우저는 캐싱 및 기록을 목적으로 정보를 저장할 수 있습니다. 이 캐시 된 파일의 Internet Explorer hello 경우에서 hello 임시 인터넷 파일 폴더와 같은 폴더에 저장 됩니다. 이 페이지 다시 이라고 hello 브라우저 캐시에서으로 표시 합니다. 중요 한 정보 (예: 해당 주소, 신용 카드 정보, 사회 보장 번호 또는 사용자 이름), 표시 된 toohello 사용자 경우이 정보 브라우저의 캐시에 저장 되며 따라서 hello 브라우저 캐시를 검사를 통해 검색할 수 또는 hello 브라우저의 "뒤로" 단추를 누르는 합니다. 너무 "아니요-store" 모든 페이지에 대 한 캐시 제어 응답 헤더 값을 설정 합니다. |

### <a name="example"></a>예제
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>예제
이 예제는 필터를 통해 구현될 수 있습니다. 다음 예제를 사용할 수 있습니다. 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>중요한 데이터가 포함된 Web App의 구성 파일의 섹션 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [방법: ASP.NET 2.0 사용 하 여 DPAPI에서 구성 섹션 암호화](https://msdn.microsoft.com/library/ff647398.aspx), [보호 되는 구성 공급자를 지정 하](https://msdn.microsoft.com/library/68ze1hb2.aspx), [tooprotect 응용 프로그램 암호를 사용 하 여 Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **단계** | 같은 hello Web.config 구성 파일, appsettings.json은 종종 toohold 중요 한 정보를 사용자 이름, 암호, 데이터베이스 연결 문자열 및 암호화 키를 포함 하는 데 사용 합니다. 이 정보를 보호 하지 않는 경우 취약 tooattackers 또는 악의적인 사용자가 계정 사용자 이름 및 암호, 데이터베이스 이름 및 서버 이름이 같은 중요 한 정보를 가져오는 응용 프로그램은 합니다. Hello 배포 형식 (azure/온-프레미스)에 based, hello DPAPI 또는 Azure 키 자격 증명 모음와 같은 서비스를 사용 하 여 구성 파일의 중요 한 섹션을 암호화 합니다. |

## <a id="autocomplete-input"></a>중요 한 양식과 입력에 hello 자동 완성 HTML 특성을 명시적으로 해제 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN: 자동 완성 특성](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [HTML에서 자동 완성 기능 사용](http://msdn.microsoft.com/library/ms533032.aspx), [HTML 삭제 취약점](http://technet.microsoft.com/security/bulletin/MS10-071), [자동 완성., 다시?!](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **단계** | hello 자동 완성 특성 켜거나 폼에서 자동 완성 가져야 할지 여부를 지정 합니다. 자동 완성에 있으면 hello 브라우저 자동으로 전체 값에 값을 기반으로 해당 hello 사용자가 입력 하기 전에. 예를 들어 폼에 새 이름 및 암호를 입력 하 고 hello 항목인 때 hello 브라우저 hello 암호를 저장 해야 하는 경우 요청 합니다. Hello 폼이 표시 하는 경우에 그 이후에 hello 이름 및 암호 자동으로 채워집니다 또는 hello 이름을 입력 한 대로 완료 됩니다. 로컬 액세스 권한이 있는 경우 공격자가 hello 브라우저 캐시에서 hello 일반 텍스트 암호를 얻을 수 있습니다. 기본적으로 자동 완성은 활성화되어 있으므로 명시적으로 비활성화되어야 합니다. |

### <a name="example"></a>예제
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Hello 사용자 화면에 표시 되는 중요 한 데이터 마스크 되어 있는지 확인 하십시오.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 예: 암호, 신용 카드 번호 SSN 등 중요 한 데이터 해야 hello 화면에 표시 될 때 숨겨질 수 있습니다. 이 hello 데이터 (예: 어깨 서핑 암호, 지원 담당자 SSN 사용자 수가 보기)에 액세스할 권한이 없는 tooprevent 담당자입니다. 이러한 데이터 요소가 일반 텍스트로 표시되지 않고 적절하게 마스킹되도록 합니다. 이 인해 toobe (예: 입력으로 허용 하는 동안 자동으로 처리. 입력 형식 = "password")와 다시 hello 화면에 표시 (예: 표시만 hello hello 신용 카드 번호의 마지막 4 자리 숫자)입니다. |

## <a id="dynamic-users"></a>동적 데이터 마스킹 toolimit 중요 한 데이터 노출을 아닌 권한 있는 사용자가 구현 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure, 온-프레미스 |
| **특성**              | SQL 버전 - V12, SQL 버전 - MsSQL2016 |
| **참조**              | [동적 데이터 마스킹](https://msdn.microsoft.com/library/mt130841) |
| **단계** | hello 동적 데이터 마스킹의 목적은 중요 한 데이터를 보는에서 toohello 데이터에 액세스 권한이 없는 사용자의 toolimit 노출을입니다. 동적 데이터 마스킹 tooprevent 데이터베이스 사용자가 직접 toohello 데이터베이스를 연결 하 고 hello 중요 한 데이터 조각을 노출 하는 과도 한 쿼리를 실행 것은 아닙니다. 동적 데이터 마스킹은 상호 보완적 tooother SQL Server 보안 기능 (감사, 암호화, 행 수준 보안...) 및 toouse 권장으로 함께이 기능 뿐만 아니라 순서 toobetter에 hello 중요 한 데이터를에서 보호 hello 데이터베이스입니다. 이 기능은 SQL Server 2016 이상 및 Azure SQL Database에서만 지원됩니다. |

## <a id="salted-hash"></a>암호가 솔트된 해시 형식으로 저장되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [.NET Crypto API를 사용하여 암호 해싱](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **단계** | 암호는 사용자 지정 사용자 저장소 데이터베이스에 저장되어야 합니다. 암호 해시는 대신 솔트 값으로 저장되어야 합니다. Hello 사용자에 대 한 hello 솔트는 항상 고유 하 고 무차별 암호 강제의 tooeliminate hello 가능성 루프 최소 작업 비율 반복 횟수 150000 hello 암호를 저장 하기 전에 b 암호화, s crypt 또는 PBKDF2 적용할 수 있는지 확인 합니다.| 

## <a id="db-encrypted"></a>데이터베이스 열의 중요한 데이터가 암호화되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | SQL 버전 - 모두 |
| **참조**              | [SQL Server에서 중요한 데이터 암호화](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [방법: SQL Server에서 데이터 열 암호화](https://msdn.microsoft.com/library/ms179331), [인증서별 암호화](https://msdn.microsoft.com/library/ms188061) |
| **단계** | 신용 카드 번호 같은 중요 한 데이터 toobe hello 데이터베이스에서 암호화에 있습니다. 열 수준 암호화를 사용 하 여 데이터를 암호화할 수 또는 hello 암호화 기능을 사용 하 여 응용 프로그램 기능별. |

## <a id="tde-enabled"></a>TDE(데이터베이스 수준 암호화)가 활성화되어 있는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [SQL Server TDE(투명한 데이터 암호화) 이해](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **단계** | 투명 한 데이터 암호화 (TDE)는 데이터베이스의 중요 한 데이터 암호화에 SQL server의 기능 및 hello는 키가 인증서를 사용 하 여 사용 되는 tooencrypt hello 데이터를 보호 합니다. 이렇게 하면 hello 키가 없는 모든 사용자가 hello 데이터를 사용 하 여 수 없습니다. 데이터를 보호 하는 TDE "있는 그대로" hello 데이터 및 로그 파일을 의미 합니다. 법, 규정 및 지침을 다양 한 업계에서 확립 된 hello 기능 toocomply를 제공 합니다. |

## <a id="backup"></a>데이터베이스 백업이 암호화되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure, 온-프레미스 |
| **특성**              | SQL 버전 - V12, SQL 버전 - MsSQL2014 |
| **참조**              | [SQL Database 백업 암호화](https://msdn.microsoft.com/library/dn449489) |
| **단계** | SQL Server에는 백업을 만드는 동안 hello 기능 tooencrypt hello 데이터가 있습니다. Hello 암호화 알고리즘 및 hello 암호기 (인증서 또는 비대칭 키)를 지정 하 여 백업을 만들 때 암호화 된 백업 파일을 만들 수 하나입니다. |

## <a id="api-browser"></a>API 브라우저의 저장소에 저장 되지 않으므로 해당 중요 한 데이터 관련 tooWeb 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC 5, MVC 6 |
| **특성**              | ID 공급자 - ADFS, ID 공급자 - Azure AD |
| **참조**              | 해당 없음  |
| **단계** | <p>특정 구현에서 중요 한 아티팩트 관련 tooWeb API의 인증 브라우저의 로컬 저장소에 저장 됩니다. 예를 들어, adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key 등과 같은 Azure AD 인증 아티팩트입니다.</p><p>이러한 아티팩트는 모두 로그아웃 또는 브라우저가 닫힌 후에도 사용할 수 있습니다. 악의적인 사용자는 액세스 toothese 아티팩트를 가져온 경우 복사가 재사용할 수 tooaccess hello 보호 리소스 (Api). 모든 중요 한 아티팩트 관련된 tooWeb API 브라우저의 저장소에 저장 되지 않은 것을 확인 합니다. 클라이언트 쪽 저장소 피할 수 없는 경우 (예: 단일 페이지 응용 프로그램 (SPA) 암시적 OpenIdConnect/OAuth 흐름을 활용 하는 로컬로 액세스 토큰 toostore 필요)으로 저장소 선택 항목을 사용 하 여 지 속성을 갖지 않습니다. 예: SessionStorage tooLocalStorage를 선호 합니다.</p>| 

### <a name="example"></a>예제
아래 JavaScript 코드 조각 hello 로컬 저장소에 인증 아티팩트를 저장 하는 사용자 지정 인증 라이브러리에서 시작 됩니다. 이렇게 구현하지 않아야 합니다. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Cosmos DB에 저장된 중요한 데이터 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Document DB | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 문서 DB에서 저장하기 전에 응용 프로그램 수준에서 중요한 데이터를 암호화하거나 Azure Storage 또는 Azure SQL과 같은 다른 저장소 솔루션에서 중요한 데이터를 저장합니다.| 

## <a id="disk-vm"></a>가상 컴퓨터에서 사용 하는 Azure 디스크 암호화 tooencrypt 디스크 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure IaaS VM 트러스트 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Azure 디스크 암호화를 사용 하 여 tooencrypt 디스크를 사용할 가상 컴퓨터](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **단계** | <p>Azure 디스크 암호화는 현재 미리 보기에 포함되어 있는 새로운 기능입니다. 이 기능은 tooencrypt hello OS 디스크 및 IaaS 가상 컴퓨터에서 사용 되는 데이터 디스크입니다. Windows hello 드라이브는 업계 표준 BitLocker 암호화 기술을 사용 하 여 암호화 됩니다. Linux 용 hello 디스크 hello DM 암호화 기술을 사용 하 여 암호화 됩니다. 이 Azure 키 자격 증명 모음 tooallow 있습니다 toocontrol와 통합 hello 디스크 암호화 키를 관리 합니다. hello Azure 디스크 암호화 솔루션에서는 hello 다음 세 고객 암호화 시나리오를 지원 합니다.</p><ul><li>Azure 키 자격 증명 모음에 저장되는 고객 암호화 VHD 파일 및 고객 제공 암호화 키에서 만든 새 IaaS VM에 대해 암호화를 사용하도록 설정합니다.</li><li>Hello Azure Marketplace에서에서 만든 새 IaaS Vm에 대 한 암호화를 사용 하도록 설정 합니다.</li><li>Azure에서 이미 실행 중인 기존 IaaS VM에 대해 암호화를 사용하도록 설정합니다.</li></ul>| 

## <a id="fabric-apps"></a>Service Fabric 응용 프로그램에서 암호 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Service Fabric 트러스트 경계 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 환경 - Azure |
| **참조**              | [Service Fabric 응용 프로그램에서 비밀 관리](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **단계** | 저장소 연결 문자열, 암호, 일반 텍스트로 처리하면 안 되는 값 등 모든 민감한 정보를 비밀로 처리할 수 있습니다. 서비스 패브릭 응용 프로그램에서 Azure 키 자격 증명 모음 toomanage 키와 암호를 사용 합니다. |

## <a id="modeling-teams"></a>보안 모델링 수행 및 필요한 경우 비즈니스 단위/팀 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 보안 모델링 수행 및 필요한 경우 비즈니스 단위/팀 사용 |

## <a id="entities"></a>중요 한 엔터티에 대 한 액세스 tooshare 기능 최소화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 중요 한 엔터티에 대 한 액세스 tooshare 기능 최소화 |

## <a id="good-practices"></a>Hello Dynamics CRM 공유 기능 및 보안 사례와 관련 된 hello 위험에 사용자가 기차

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello Dynamics CRM 공유 기능 및 보안 사례와 관련 된 hello 위험에 사용자가 기차 |

## <a id="exception-mgmt"></a>예외 관리에서 구성 세부 정보를 표시하는 금지된 개발 표준 규칙 포함

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 배포 외부의 예외 관리에서 구성 세부 정보를 표시하는 금지된 개발 표준 규칙을 포함합니다. 코드 검토 또는 정기적 검사의 일부로 이 항목을 테스트합니다.|

## <a id="sse-preview"></a>미사용 데이터에 대한 Azure Storage 서비스 암호화(SSE) 사용(미리 보기)

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | StorageType - Blob |
| **참조**              | [미사용 데이터에 대한 Azure Storage 서비스 암호화(미리 보기)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **단계** | <p>Azure 저장소 서비스 암호화 SSE ()을 미사용 데이터를 사용 하면 조직의 보안 및 규정 준수 약정 데이터 toomeet를 보호 하 고 보호 합니다. 이 기능을 Azure 저장소는 자동으로 데이터 사전 toopersisting toostorage를 암호화 하 고 이전 tooretrieval 해독 합니다. hello 암호화, 암호 해독 및 키 관리는 완전히 투명 한 toousers 합니다. SSE에는 추가 blob 및 tooblock blob만, 페이지 blob을 적용 합니다. hello 다른 유형의 데이터를 테이블, 큐 및 파일을 포함 하 여 암호화 되지 않습니다.</p><p>워크플로 암호화 및 암호 해독:</p><ul><li>hello 고객 hello 저장소 계정에서 암호화를 설정합니다.</li><li>Hello 고객 데이터 (예: PUT Blob, 배치 블록, PUT Page, 등)의 새 tooBlob 저장소;를 작성 하는 경우 모든 쓰기 hello 가장 강력한 블록 암호화 사용 가능한 중 하나는 256 비트 AES 암호화를 사용 하 여 암호화</li><li>Hello 고객이 tooaccess 데이터 (Blob 가져오기, 등), 데이터를 자동으로 해독 toohello 사용자를 반환 하기 전에</li><li>암호화를 해제 하는 경우 새로운 쓰기는 더 이상 암호화 되며 기존의 암호화 된 데이터 암호화 상태를 유지 hello 사용자가 다시 작성 합니다. 암호화를 사용 하는 동안 쓰기 tooBlob 저장소 암호화 됩니다. hello 저장소 계정에 대 한 암호화를 활성화/비활성화을 전환 하는 hello 사용자와 데이터의 hello 상태 변경 되지 않습니다.</li><li>모든 암호화 키는 Microsoft에서 저장하고 암호화하며 관리합니다.</li></ul><p>이 이번에 참고 사항, hello 암호화에 사용 되는 hello 키도 Microsoft에서 관리 됩니다. Microsoft 원래 hello 키를 생성 하 고 내부 Microsoft 정책에 의해 정의 된 대로으로 hello 키 hello 일반 회전 hello 안전한 저장소를 관리 합니다. Hello 이후, 고객은 전달 되는 hello 기능 toomanage 자신의 > 암호화 키를 고 toocustomer 관리 키에서 Microsoft 관리 키에서 마이그레이션 경로 지정 합니다.</p>| 

## <a id="client-storage"></a>Azure 저장소에 클라이언트 쪽 암호화 toostore 중요 한 데이터를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Microsoft Azure Storage에 대한 클라이언트 쪽 암호화 및 Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [자습서: Azure Key Vault를 사용하여 Microsoft Azure Storage에서 Blob 암호화 및 해독](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [Azure 암호화 확장을 사용하여 Azure Blob Storage에서 데이터 안전하게 저장](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **단계** | <p>.NET Nuget 패키지용 Azure 저장소 클라이언트 라이브러리 hello tooAzure 저장소에 업로드 하 고 toohello 클라이언트를 다운로드 하는 동안 데이터를 해독 하기 전에 클라이언트 응용 프로그램 내에서 데이터를 암호화를 지원 합니다. hello 라이브러리는 또한 저장소 계정 키 관리에 대 한 Azure 키 자격 증명 모음 통합을 지원합니다. 클라이언트 쪽 암호화의 작동 원리에 대한 간단한 설명은 다음과 같습니다.</p><ul><li>hello Azure 저장소 클라이언트 SDK는 한 번 사용 대칭 키는 콘텐츠 암호화 키 (CEK)를 생성 합니다.</li><li>고객 데이터는 이 CEK를 사용하여 암호화됩니다.</li><li>hello CEK 다음 래핑된 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화) 합니다. hello KEK 키 식별자로 식별 되 하거나 수 있습니다는 비대칭 키 쌍 또는 대칭 키 및 수 수 로컬로 관리 Azure 키 자격 증명 모음에 저장 합니다. hello 저장소 클라이언트 자체에 대 한 액세스 toohello KEK에 없습니다. 방금 주요 자격 증명 모음에서 제공 하는 hello 키 래핑 알고리즘을 호출 합니다. 고객은 toouse 래핑/래핑 해제 하려는 경우 키에 대 한 사용자 지정 공급자를 선택할 수 있습니다.</li><li>hello 암호화 된 데이터는 다음 toohello Azure 저장소 서비스에 업로드 합니다. 하위 수준 구현 세부 사항에 대 한 hello references 섹션에 hello 링크를 확인 합니다.</li></ul>|

## <a id="pii-phones"></a>구분 또는 toophones 로컬 저장소를 작성 하는 PII 데이터 암호화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 모바일 클라이언트 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, Xamarin  |
| **특성**              | 해당 없음  |
| **참조**              | [Microsoft Intune 정책을 사용하여 장치에서 설정 및 기능 관리](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [키 집합 Valet](https://components.xamarin.com/view/square.valet) |
| **단계** | <p>Hello 응용 프로그램 사용자의 PII (전자 메일, 전화 번호, 이름, 성, 환경 설정 등)와 같은 중요 한 정보를 기록 하는 경우 -모바일의 파일 시스템에 다음에 암호화 되어야 toohello 로컬 파일 시스템을 작성 하기 전에. Hello 응용 프로그램이 엔터프라이즈 응용 프로그램의 경우 다음 Windows Intune을 사용 하 여 게시 응용 프로그램의 hello 가능성을 탐색 합니다.</p>|

### <a name="example"></a>예제
다음 보안 정책 toosafeguard 중요 한 데이터와 함께 Intune는 구성할 수 있습니다. 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>예제
Hello 응용 프로그램 있지 않는 경우는 엔터프라이즈 응용 프로그램을 사용 하 여 플랫폼에서 제공 하는 키 저장소, 키 집합 toostore 암호화 키를 암호화 작업을 사용 하 여 hello 파일 시스템에 수행할 수 있습니다. 다음 코드 조각은 tooaccess xamarin을 사용 하 여 키 집합에서 키 하는 방법을 보여 줍니다. 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Tooend 사용자가 배포 하기 전에 생성 된 바이너리를 난독 처리

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 모바일 클라이언트 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [.NET에 대한 암호화 난독 처리](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **단계** | 생성 된 이진 파일 (apk 내 어셈블리)를 리버스 엔지니어링 어셈블리 난독 처리 된 toostop 이어야 합니다. 도구와 같은 `CryptoObfuscator` 이 용도로 사용할 수 있습니다. |

## <a id="cert"></a>집합 clientCredentialType tooCertificate 또는 Windows

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [강화](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | 일반 텍스트 암호는 UsernameToken를 사용 하 여 암호화 되지 않은 채널을 통해 SOAP 메시지 hello을 스니핑 할 수 있는 hello 암호 tooattackers를 노출 합니다. UsernameToken hello를 사용 하는 서비스 공급자 암호가 일반 텍스트로 전송 허용 될 수 있습니다. 일반 텍스트 암호는 암호화 되지 않은 채널을 통해 보내는 SOAP 메시지 hello을 스니핑 할 수 있는 hello 자격 증명 tooattackers를 노출할 수 있습니다. | 

### <a name="example"></a>예제
hello 다음 WCF 서비스 공급자 구성을 사용 하 여 hello UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
ClientCredentialType tooCertificate 또는 Windows를 설정 합니다. 

## <a id="security"></a>WCF 보안 모드가 활성화되지 않음

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 보안 모드 - 전송, 보안 모드 - 메시지 |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [보안 강화](https://vulncat.fortify.com/en/vulncat/index.html), [WCF 보안 CoDe Magazine의 기본 사항](http://www.codemag.com/article/0611051) |
| **단계** | 전송 또는 메시지 보안이 거부되지 않았습니다. 메시지 전송 하지 않는 경우 또는 hello 무결성 또는 기밀성이 hello 메시지의 보안을 보장할 수 없습니다 메시지를 전송 하는 응용 프로그램입니다. WCF 보안 바인딩은 tooNone 설정 되 면 전송 보안과 메시지 보안 모두 비활성화 됩니다. |

### <a name="example"></a>예제
hello 다음과 같은 구성 설정 hello 보안 모드 tooNone 합니다. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>예제
5개의 가능한 보안 모드가 있는 모든 서비스 바인딩에 대한 보안 모드는 다음과 같습니다. 
* 없음. 보안 해제. 
* 전송. 상호 인증과 메시지 보호를 위해 전송 보안 사용. 
* Message. 상호 인증과 메시지 보호를 위해 메시지 보안 사용. 
* 둘 다. 있습니다 toosupply 설정을 전송 및 메시지 수준 보안 (MSMQ만이 지원). 
* TransportWithMessageCredential. Hello 메시지 및 메시지 보호와 자격 증명이 전달 및 hello 전송 계층에서 서버 인증을 제공 합니다. 
* TransportCredentialOnly. Hello 전송 계층으로 클라이언트 자격 증명이 전달 하 고 메시지 보호 없이 적용 됩니다. 메시지의 전송 및 메시지 보안 tooprotect hello 무결성 및 기밀성을 사용 합니다. 아래 hello 구성을 hello 서비스 toouse 전송 보안 메시지 자격 증명을 지정합니다.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
