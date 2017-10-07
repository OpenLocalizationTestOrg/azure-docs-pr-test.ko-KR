---
title: "Active Directory aaaAzure v2.0 범위, 권한 및 동의 | Microsoft Docs"
description: "범위, 권한 및 동의 포함 하 여 Azure AD hello v2.0 끝점에서 권한 부여의 설명입니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>범위, 권한 및 hello Azure Active Directory v 2.0 끝점의 동의
Azure AD(Azure Active Directory)와 통합된 앱은 사용자가 앱이 데이터에 액세스하는 방법을 제어할 수 있는 권한 부여 모델을 따릅니다. hello 권한 부여 모델의 hello v2.0 구현 업데이트 된 하 고 앱이 Azure AD와 상호 작용 해야 방법을 변경 합니다. 이 문서에서는 hello 범위, 권한 및 동의 포함 하 여이 권한 부여 모델의 기본 개념에 설명 합니다.

> [!NOTE]
> hello v2.0 끝점에는 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다. 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

## <a name="scopes-and-permissions"></a>범위 및 사용 권한
Azure AD 구현 hello [OAuth 2.0](active-directory-v2-protocols.md) 인증 프로토콜입니다. OAuth 2.0은 사용자 대신 타사 앱에서 웹에 호스트된 리소스에 액세스할 수 있도록 하는 방법입니다. Azure AD와 통합된 웹에 호스트된 리소스에는 리소스 식별자 또는 *응용 프로그램 ID URI*가 있습니다. 예를 들어 웹에 호스트된 몇 가지 Microsoft 리소스는 다음과 같습니다.

* Office 365 통합 메일 API hello:`https://outlook.office.com`
* Azure AD Graph API hello:`https://graph.windows.net`
* Microsoft Graph: `https://graph.microsoft.com`

hello가 Azure AD와 통합 하는 모든 타사 리소스에도 마찬가지입니다. 또한 이러한 리소스가 더 작은 청크로 해당 리소스의 사용된 toodivide hello 기능 일 수 있는 사용 권한 집합이 정의할 수 있습니다. 예를 들어, [Microsoft Graph](https://graph.microsoft.io) 권한을 toodo hello 다음 작업 중 일부를 정의 했습니다.

* 사용자의 일정 읽기
* 쓰기 tooa 사용자의 일정
* 사용자로 메일 보내기

이러한 유형의 사용 권한을 정의 하 여 hello 리소스에는 해당 데이터 및 hello 데이터는 노출 하는 방법에 대 한 세분화 된 제어 합니다. 타사 앱은 앱 사용자로부터 이러한 사용 권한을 요청할 수 있습니다. hello 응용 프로그램 사용자 hello 앱 hello 사용자를 대신 하 여 작업할 수 있는 전에 hello 사용 권한을 승인 해야 합니다. Hello 리소스의 기능을 더 작은 사용 권한 집합을 청크 하 여 타사 앱 빌드된 toorequest만 hello 특정 사용 권한이 필요 하다는 tooperform 해당 기능을 수 있습니다. 응용 프로그램 사용자가 정확 하 게 응용 프로그램 사용 방법가 데이터를 알 수 있으며 hello 앱 악의적인 의도로 작동 하지 않거나 더 신뢰할 수 있습니다.

Azure AD 및 OAuth에서는 이러한 유형의 사용 권한을 *범위*라고 합니다. 참조 된 tooas 되기도 *oAuth2Permissions*합니다. 범위는 Azure AD에서 문자열 값으로 표시됩니다. 각 사용 권한에 대해 hello 범위 값은 Microsoft Graph 예에서 hello:

* `Calendar.Read`를 사용하여 사용자의 일정 읽기
* 사용 하 여 쓰기 tooa 사용자의 일정`Mail.ReadWrite`
* `Mail.Send`을 사용하여 사용자로 메일 보내기

응용 프로그램 요청 toohello v2.0 끝점 hello 범위를 지정 하 여 이러한 권한을 요청할 수 있습니다.

## <a name="openid-connect-scopes"></a>OpenID Connect 범위
OpenID Connect의 hello v2.0 구현에는 특정 리소스 tooa 적용 되지 않는 몇 가지 잘 정의 된 범위가: `openid`, `email`, `profile`, 및 `offline_access`합니다.

### <a name="openid"></a>openid
응용 프로그램 로그인 사용 하 여 수행 하는 경우 [OpenID Connect](active-directory-v2-protocols.md), hello를 요청 해야 `openid` 범위입니다. hello `openid` 범위 표시 hello 작업 계정에 "로그인" 권한이 hello 처럼 동의 페이지 및 hello "프로필 보기 및 tooapps 및 Microsoft 계정을 사용 하 여 서비스를 연결 합니다." 사용 권한으로 hello 개인 Microsoft 계정에 페이지를 승인 합니다. 이 권한이 있는 응용 프로그램에서 수신할 수 hello 사용자에 대 한 고유 식별자 hello 형태의 hello `sub` 클레임입니다. 또한 hello 앱 액세스 toohello 사용자 정보 끝점이 제공합니다. hello `openid` hello v 2.0 토큰 끝점 tooacquire ID 토큰을 응용 프로그램의 다른 구성 요소 간에 사용 되는 toosecure HTTP 호출 될 수 있는에 범위를 사용할 수 있습니다.

### <a name="email"></a>email
hello `email` hello로 범위를 사용할 수 있습니다 `openid` 범위와 그 밖에 있습니다. Hello 앱 액세스 toohello 사용자의 기본 전자 메일 주소 hello hello 형태로 제공 `email` 클레임입니다. hello `email` 전자 메일 주소는 hello 경우 항상 hello 사용자 계정과 연결 된 경우에 클레임은 토큰에 포함 되어 있습니다. Hello를 사용 하는 경우 `email` 범위를 응용 프로그램 해야 toohandle는 hello 사용 하는 경우 준비 `email` hello 토큰에 클레임 존재 하지 않는 합니다.

### <a name="profile"></a>프로필
hello `profile` hello로 범위를 사용할 수 있습니다 `openid` 범위와 그 밖에 있습니다. Hello 앱 액세스 tooa 상당한 양의 hello 사용자에 대 한 정보를 제공합니다. 액세스할 수 있는 하는 hello 정보 포함 되지만 hello 사용자 이름, 성, 기본 사용자 이름 및 개체 id입니다. 제한 되지 않습니다. 특정 사용자에 대 한 hello id_tokens 매개 변수에서 사용할 수 있는 hello 프로필 클레임의 전체 목록은 참조 hello [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다.

### <a name="offlineaccess"></a>offline_access
hello [ `offline_access` 범위](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) 오랜된 시간 동안 hello 사용자 대신 응용 프로그램 액세스 tooresources를 제공 합니다. 이 범위에는 hello 작업 계정 동의 페이지에서 "데이터에 언제 든 지 액세스" 권한을 hello 형태로 나타납니다. Hello 개인 Microsoft 계정 동의 페이지에서 "언제 든 지 정보에 액세스" 권한을 hello 대로 표시 합니다. 사용자가 hello를 승인 하는 경우 `offline_access` 범위 앱 hello v 2.0 토큰 끝점에서 새로 고침 토큰을 받을 수 있습니다. 새로 고침 토큰은 장기적으로 존재합니다. 오래된 액세스 토큰이 만료되면 앱에서 새 액세스 토큰을 가져올 수 있습니다.

앱 hello를 요청 하지 않고 `offline_access` 범위, 새로 고침 토큰을 수신 하지 않습니다. 즉, hello에서 인증 코드를 사용 하는 경우 [OAuth 2.0 인증 코드 흐름](active-directory-v2-protocols.md), hello에서 액세스 토큰을 받게 됩니다 `/token` 끝점입니다. hello 액세스 토큰은 짧은 시간 동안 유효 합니다. hello 액세스 토큰은 일반적으로 한 시간에 만료 됩니다. 이 시점에서 앱 필요한 tooredirect hello 사용자 백 toohello `/authorize` 끝점 tooget 새 권한 부여 코드입니다. 응용 프로그램에서는 hello 유형에 따라이 이동 하는 동안 tooenter 자격 증명을 다시 필요 하거나 toopermissions 다시 동의 hello 사용자.

어떻게 tooget 및 사용 하 여 새로 고침 토큰에 대 한 자세한 내용은 참조 hello [v 2.0 프로토콜 참조](active-directory-v2-protocols.md)합니다.

## <a name="requesting-individual-user-consent"></a>개별 사용자의 동의 요청
에 [OpenID Connect 또는 OAuth 2.0](active-directory-v2-protocols.md) 권한 부여 요청을 응용 프로그램 hello를 사용 하 여 필요한 hello 권한을 요청할 수 `scope` 쿼리 매개 변수입니다. 예를 들어 사용자 tooan 앱에 로그인 하면 hello 앱 hello (줄 바꿈 쉽게 읽을 수 있도록 추가)와 다음 예제와 같은 요청을 보냅니다.

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

hello `scope` 매개 변수는 hello 앱 범위 공백으로 구분 된 목록을 요청 합니다. 각 범위는 hello 범위 값 toohello 리소스 식별자 (hello 응용 프로그램 ID URI)를 추가 하 여 표시 됩니다. Hello 요청의 예제는 hello 앱 hello 사용자로 권한 tooread hello 사용자의 일정 및 메일 보내기를 프로비저닝해야합니다.

Hello v 2.0 끝점의 일치 하는 레코드에 대 한 검사 hello 사용자가 자격 증명을 입력 한 후 *사용자 동의*합니다. Hello 사용자가 동의 하지 하는 경우의 hello tooany hello v2.0 끝점 요청 hello 사용자 toogrant 전의 hello에 대 한 사용 권한을 요청한 hello 사용 권한을 요청 합니다.

![작업 계정 동의](../../media/active-directory-v2-flows/work_account_consent.png)

Hello 권한을 승인 하는 hello 사용자 hello 동의 hello 권한이 없습니다. tooconsent 다시 후속 계정 로그인에 있도록 기록 됩니다.

## <a name="requesting-consent-for-an-entire-tenant"></a>전체 테넌트에 대한 동의 요청
종종 조직 라이선스 또는 응용 프로그램에 대 한 구독을 구매 하는 경우 hello 조직이 해당 직원에 대 한 toofully 프로 비전 hello 응용 프로그램입니다. 이 과정의 일환으로, 관리자는 모든 직원을 대신 하 여 응용 프로그램 tooact hello에 대 한 동의 부여할 수 있습니다. Admin 님 안녕하세요 hello 전체 테 넌 트에 대 한 동의 허용, hello 조직의 직원 hello 응용 프로그램에 대 한 동의 페이지에 표시 되지 않습니다.

모든 사용자는 테 넌 트에서 응용 프로그램에 대 한 동의 toorequest hello 관리자 동의 끝점을 사용할 수 있습니다.

## <a name="admin-restricted-scopes"></a>관리 제한 범위
너무 hello Microsoft 에코 시스템에서 일부 높은 권한 수준의 사용 권한을 설정할 수 있습니다*관리 제한*합니다. 이러한 종류의 범위의 예로 다음 권한을 hello:

* `Directory.Read`를 사용하여 조직의 디렉터리 데이터 읽기
* 사용 하 여 데이터 tooan 조직의 디렉터리에 쓰기`Directory.ReadWrite`
* `Groups.Read.All`을 사용하여 조직의 디렉터리에서 보안 그룹 읽기

소비자 사용자 응용 프로그램 액세스 toothis 종류의 데이터를 제공할 수 있습니다, 있지만 조직 사용자가 액세스 toohello 같은 중요 한 회사 데이터 집합을 부여할 제한 됩니다. 이러한 사용 권한은 액세스 tooone 조직 사용자를 요청 하는 응용 프로그램, 경우 hello 사용자 권한이 있는 tooconsent tooyour 앱 사용 권한 없는 한다는 오류 메시지를 받습니다.

앱이 조직에 대 한 액세스 tooadmin 제한 범위를 필요한 경우 요청 해야 하는 회사 관리자에서 직접도 다음에 설명한 hello 관리자 동의 끝점을 사용 하 여 합니다.

관리자가 이러한 사용 권한을 통해 admin 님 안녕하세요 끝점 동의 부여, 경우에 동의 hello 테 넌 트의 모든 사용자에 대 한 권한이 부여 됩니다.

## <a name="using-hello-admin-consent-endpoint"></a>Hello 관리자 동의 끝점을 사용 하 여
다음 단계를 따를 경우 앱은 관리 제한 범위를 포함하여 테넌트의 모든 사용자에 대한 사용 권한을 수집할 수 있습니다. toosee hello 단계를 구현 하는 코드 샘플 참조 hello [관리 제한 범위 샘플](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2)합니다.

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Hello 응용 프로그램 등록 포털에 hello 권한 요청
1. Hello에 tooyour 응용 프로그램 이동 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 또는 [응용 프로그램을 만들](active-directory-v2-app-registration.md) च ो.
2. Hello 찾을 **Microsoft 그래프 권한** 섹션을 앱에 필요한 hello 권한을 추가 합니다.
3. 했는지 확인 하십시오 **저장** hello 앱 등록 합니다.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Tooyour 앱에서 로그인 hello 사용자 권장:
일반적으로 응용 프로그램을 빌드할 때 hello 관리자 동의 끝점을 사용 하 여, hello 앱 필요한 페이지 또는 보기는 hello 관리자 hello 앱 사용 권한을 승인할 수 있습니다. 이 페이지에는 hello 응용 프로그램의 등록 흐름의 일부가 될 수 있습니다, 그리고 이거나 hello 앱 설정의 일부를 "연결" 흐름 전용 될 수 있습니다. 대부분의 경우에서 이렇게 하면 앱 tooshow hello에 대 한 사용자가 회사 또는 학교 Microsoft 계정으로 로그인 한 후에 보기를 "연결"이 있습니다.

Hello 조직 hello 사용자 tooyour 앱에 로그인 하면 확인할 수 있습니다 toowhich admin 님 안녕하세요 tooapprove hello 필요한 사용 권한을 확인 하기 전에 속합니다. 반드시 필요하지는 않지만 조직 사용자를 위한 직관적인 환경을 만들 수 있습니다. 다음에서 toosign hello 사용자 우리의 [v2.0 프로토콜 자습서](active-directory-v2-protocols.md)합니다.

### <a name="request-hello-permissions-from-a-directory-admin"></a>디렉터리 관리자 hello 사용 권한을 요청
조직의 관리자 로부터 준비 toorequest 사용 권한이 되 면 hello 사용자 toohello v2.0 리디렉션할 수 있습니다 *관리자 동의 끝점*합니다.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| 매개 변수 | 조건 | 설명 |
| --- | --- | --- |
| tenant |필수 |hello 디렉터리 테 넌 트의 toorequest 허가 합니다. GUID 또는 친숙한 이름 형식으로 제공할 수 있습니다. |
| client_id |필수 |hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| redirect_uri |필수 |hello 저장할 hello 응답 toobe 앱 toohandle에 대 한 전송 URI을 리디렉션합니다. 또한 hello 리디렉션 hello 응용 프로그램 등록 포털에 등록 하는 Uri 중 하나에 정확히 일치 해야 합니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. Hello 페이지 또는 보기에서와 같이 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 hello 상태 tooencode 정보를 사용 합니다. |

이 시점에서 Azure AD는 테 넌 트 관리자 toosign toocomplete hello 요청에 필요합니다. 관리자에 게 요청한 hello 응용 프로그램 등록 포털에서 응용 프로그램에 대 한 사용 권한을 모두 hello tooapprove를 요청 했습니다.

#### <a name="successful-response"></a>성공적인 응답
Admin 님 안녕하세요 응용 프로그램에 대 한 hello 권한의 승인 하는 경우 hello 성공적인 응답은 다음과 같습니다.

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| 매개 변수 | 설명 |
| --- | --- | --- |
| tenant |응용 프로그램 hello 권한이 부여 hello 디렉터리 테 넌 트와 요청한 GUID 형식에서입니다. |
| state |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. hello 상태가 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전입니다. |
| admin_consent |너무 설정할**true**합니다. |

#### <a name="error-response"></a>오류 응답
Admin 님 안녕하세요 응용 프로그램에 대 한 hello 권한을 승인 하지 않습니다, hello 실패 한 경우 응답은 다음과 같습니다.

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| 매개 변수 | 설명 |
| --- | --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |오류의 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

성공적인 응답 hello 관리자 동의 끝점에서 받은 후 응용 프로그램에 요청한 hello 권한을 왔습니다. 그런 다음 원하는 hello 리소스에 대 한 토큰을 요청할 수 있습니다.

## <a name="using-permissions"></a>사용 권한 사용
Hello 사용자가 앱에 대 한 toopermissions 동의한 경우 후 응용 프로그램 권한 tooaccess 응용 프로그램의 일부 기능에서 리소스를 나타내는 액세스 토큰을 획득할 수 있습니다. 액세스 토큰 단일 리소스에 대해서만 사용할 수 있지만 해당 리소스에 대 한 응용 프로그램에 부여 하는 모든 권한에 hello 액세스 토큰 내에 인코딩되기 합니다. tooacquire 액세스 토큰을 앱에는 요청 toohello v 2.0 토큰 끝점을 다음과 같이 설정할 수 있습니다.

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

HTTP 요청 toohello 리소스에서 hello 결과 액세스 토큰을 사용할 수 있습니다. 안정적으로 응용 프로그램에 특정 작업을 적절 한 사용 권한 tooperform hello 있다고 toohello 리소스를 나타냅니다.  

OAuth 2.0 hello에 대 한 자세한 정보에 대 한 프로토콜을 마우스 tooget 액세스 토큰을 확인 하려면 어떻게 해야 hello [v2.0 끝점 프로토콜 참조](active-directory-v2-protocols.md)합니다.
