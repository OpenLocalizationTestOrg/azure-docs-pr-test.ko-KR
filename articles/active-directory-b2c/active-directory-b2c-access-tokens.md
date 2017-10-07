---
title: "Azure Active Directory B2C: 액세스 토큰 요청 | Microsoft Docs"
description: "이 문서에서는 보여 어떻게 toosetup 클라이언트 응용 프로그램 액세스 토큰 및 합니다."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: 액세스 토큰 요청

액세스 토큰 (로 표시 된 **액세스\_토큰** hello 응답에서 Azure AD B2C) 의해 보안 되는 클라이언트가 tooaccess 리소스를 사용할 수 있는 보안 토큰의 형태는 [권한 부여 서버](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), web API와 같이 합니다. 액세스 토큰으로 표시 됩니다 [Jwt](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) hello 의도 한 리소스 서버 및 부여 된 사용 권한 toohello 서버 hello에 대 한 정보를 포함 합니다. Hello 리소스 서버를 호출할 때는 hello 액세스 토큰 hello HTTP 요청에 있어야 합니다.

이 문서에서는 방법을 tooconfigure 클라이언트 응용 프로그램 및 web API에는 tooobtain 순서는 **액세스\_토큰**합니다.

> [!NOTE]
> **Azure AD B2C에서는 Web API 체인(On-Behalf-Of)을 지원하지 않습니다.**
>
> Azure AD B2C로 보호 둘 다, 다 수의 아키텍처 toocall 해야 하는 web API를 다른 다운스트림 web API 포함 됩니다. 이 시나리오는 hello Azure AD Graph API와 같은 Microsoft 온라인 서비스를 호출 하는 웹 API 백 엔드로 있는 네이티브 클라이언트에서 일반적입니다.
>
> Hello에 대신-흐름 이라고 hello 그렇지 않으면 OAuth 2.0 JWT 전달자 자격 증명 부여를 사용 하 여이 연결 된 웹 API 시나리오를 지원할 수 있습니다. 그러나 Azure AD B2C에 hello에 대신-흐름 현재 구현 되지 않습니다.

## <a name="register-a-web-api-and-publish-permissions"></a>웹 API 등록 및 권한 게시

액세스 토큰을 요청 하기 전에 먼저 tooregister web API 및 해야 toohello 클라이언트 응용 프로그램에 부여할 수 있는 권한 (범위)을 게시 합니다.

### <a name="register-a-web-api"></a>웹 API 등록

1. Hello Azure 포털에 기능 블레이드에서 hello B2C 클릭 **응용 프로그램**합니다.
1. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
1. 입력 한 **이름** 응용 프로그램 tooconsumers 설명 하는 hello 응용 프로그램에 대 한 합니다. 예를 들어 "Contoso API"를 입력할 수 있습니다.
1. 설정/해제 hello **웹 앱 / 웹 API** 너무 전환**예**합니다.
1. Hello에 대 한 임의 값을 입력 **회신 Url**합니다. 예를 들어 `https://localhost:44316/`을 입력합니다. hello 값 API 해야를 받지 hello 토큰 Azure AD B2C에서 직접 하므로 문제가 되지 않습니다.
1. **앱 ID URI**를 입력합니다. Web API에 사용 되는 hello 식별자입니다. 예를 들어 hello 상자에 '참고'를 입력 합니다. hello **앱 ID URI** 것 `https://{tenantName}.onmicrosoft.com/notes`합니다.
1. 클릭 **만들기** tooregister 응용 프로그램입니다.
1. 방금 만든 hello 응용 프로그램을 클릭 하 고 hello 전역적으로 고유 아래로 복사 **응용 프로그램 클라이언트 ID** 하는 코드에서 사용할 합니다.

### <a name="publishing-permissions"></a>권한 게시

유사한 toopermissions 요소인 범위는 응용 프로그램은 API를 호출 하는 경우에 필요 합니다. 범위의 일부 예는 "읽기" 또는 "쓰기"입니다. 웹 또는 너무 "읽기" API에서 네이티브 응용 프로그램 한다고 가정 합니다. 앱이 Azure AD B2C을 호출 하 고 액세스 하는 토큰 요청 "읽기" 액세스 toohello 범위를 제공 합니다. Azure AD B2C tooemit 액세스 토큰에 대 한 순서로 hello 앱 toobe 권한이 너무 "읽기" hello 특정 API에서 부여 해야 합니다. toodo이 API는 먼저 toopublish hello "읽기" 범위 필요한 합니다.

1. Azure AD B2C hello 내 **응용 프로그램** 블레이드를 열고 hello 웹 API 응용 프로그램 ("Contoso API").
1. **게시된 범위**를 클릭합니다. 이 tooother 응용 프로그램에 부여할 수 있는 hello 사용 권한 (범위)를 정의 하는입니다.
1. 필요에 따라 **범위 값**을 추가합니다(예: "읽기"). 기본적으로 hello "user_impersonation" 범위를 정의 합니다. 원하는 경우 이를 무시할 수 있습니다. Hello에 hello 범위에 대 한 설명을 입력 **범위 이름** 열입니다.
1. **Save**를 클릭합니다.

> [!IMPORTANT]
> hello **범위 이름** 은 hello hello에 대 한 설명 **범위 값**합니다. Hello 범위를 사용할 때는 확인 되었는지 toouse hello **범위 값**합니다.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>네이티브 권한을 부여 하거나 웹 응용 프로그램 사용 권한 tooa 웹 API

API 구성된 toopublish 범위 되 면 hello 클라이언트 응용 프로그램 toobe hello Azure 포털을 통해 해당 범위를 부여 해야 합니다.

1. Toohello 이동 **응용 프로그램** hello B2C 기능 블레이드에서 메뉴.
1. 이미 없는 클라이언트 응용 프로그램([웹앱](active-directory-b2c-app-registration.md#register-a-web-app) 또는 [네이티브 클라이언트](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app))을 등록합니다. 시작 지점으로이 가이드를 따르는 경우 tooregister 클라이언트 응용 프로그램 해야 합니다.
1. **API 액세스**를 클릭합니다.
1. **추가**를 클릭합니다.
1. 웹 API 및 hello 범위 toogrant 원하는 (권한)을 선택 합니다.
1. **확인**을 클릭합니다.

> [!NOTE]
> Azure AD B2C는 클라이언트 응용 프로그램 사용자의 동의를 묻지 않습니다. 대신, 모든 동의 admin 님 안녕하세요 위에서 설명한 hello 응용 프로그램 사이 구성 된 hello 사용 권한을 기반으로 제공 됩니다. 응용 프로그램에 대 한 권한 부여를 취소 하는 경우 모든 사용자가 이전에 수 tooacquire 된 사용 권한이 더 이상 수 toodo 수 있도록 합니다.

## <a name="requesting-a-token"></a>토큰 요청

클라이언트 응용 프로그램 hello hello에서 toospecify hello 필요한 권한이 필요로 액세스 토큰을 요청할 때 **범위** hello 요청의 매개 변수입니다. 예를 들어 toospecify hello **범위 값** hello 있는 API hello에 대 한 "읽기" **앱 ID URI** 의 `https://contoso.onmicrosoft.com/notes`, hello 범위 것 `https://contoso.onmicrosoft.com/notes/read`합니다. 다음은 권한 부여 코드 요청 toohello의 예 `/authorize` 끝점입니다.

> [!NOTE]
> 현재 사용자 지정 도메인은 액세스 토큰과 함께 지원되지 않습니다. Hello 요청 URL에서 tenantName.onmicrosoft.com 도메인을 사용 해야 합니다.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire hello 여러 권한에 동일한 요청, 단일 hello에 여러 항목을 추가할 수 있습니다 **범위** 매개 변수를 공백으로 구분 합니다. 예:

디코딩된 URL:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

인코딩된 URL:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

클라이언트 응용 프로그램에 부여된 것보다 더 많은 범위(권한)를 리소스에 대해 요청할 수 있습니다. Hello 대/소문자 이면 하나 이상의 권한 부여 되 면 hello 호출이 성공 합니다. hello 결과 **액세스\_토큰** 성공적으로 부여 된 권한만 hello로 채워진 "scp" 요구를 해야 합니다.

> [!NOTE] 
> Hello에 두 개의 다른 웹 리소스에 대 한 권한을 요청 지원 하지 않습니다 같은 요청 합니다. 이러한 종류의 요청은 실패합니다.

### <a name="special-cases"></a>특수 사례

OpenID Connect 표준 hello 몇 가지 특별 한 "범위" 값을 지정합니다. "hello 사용자의 프로필 액세스" 특별 한 범위 나타내는 hello 권한이 너무 다음 hello:

* **openid**: ID 토큰 요청
* **오프라인\_액세스**: 새로 고침 토큰을 요청합니다([인증 코드 흐름](active-directory-b2c-reference-oauth-code.md) 사용).

경우 hello `response_type` 에서 매개 변수는 `/authorize` 요청에 포함 되어 `token`, hello `scope` 매개 변수 범위 리소스를 하나 이상 포함 해야 (이외의 `openid` 및 `offline_access`) 하는 권한이 부여 됩니다. 그렇지 않으면 hello `/authorize` 요청 오류와 함께 종료 됩니다.

## <a name="hello-returned-token"></a>hello 토큰 반환

성공적으로 생성 된 **액세스\_토큰** (두 hello에서 `/authorize` 또는 `/token` 끝점), hello 다음 클레임 표시 됩니다.

| 이름 | 클레임 | 설명 |
| --- | --- | --- |
|대상 |`aud` |hello **응용 프로그램 ID** hello 단일 리소스의 hello 토큰에 대 한 액세스 권한을 부여 합니다. |
|범위 |`scp` |hello 권한이 toohello 리소스를 부여 합니다. 여러 부여된 권한은 공백으로 구분됩니다. |
|권한 있는 주체 |`azp` |hello **응용 프로그램 ID** hello 요청을 시작한 hello 클라이언트 응용 프로그램의 합니다. |

API hello를 받을 때 **액세스\_토큰**, 다음 조건을 충족 해야 [hello 토큰 유효성 검사](active-directory-b2c-reference-tokens.md) 토큰 hello tooprove 인증 하 고 hello 올바른 클레임 했습니다.

우리는 항상 열려 toofeedback 및 제안을! 이 항목에 문제가 있는 경우 게시 하세요 hello 태그를 사용 하 여 스택 오버플로에 [' azure ad b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c)합니다. 기능 요청에 대 한 추가 너무[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)합니다.

## <a name="next-steps"></a>다음 단계

* [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)를 사용하여 웹 API 빌드
* [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)를 사용하여 웹 API 빌드
