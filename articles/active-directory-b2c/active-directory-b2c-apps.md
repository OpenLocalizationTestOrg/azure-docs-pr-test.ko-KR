---
title: AD B2C aaaAzure | Microsoft Docs
description: "hello 유형의 응용 프로그램 hello Azure Active Directory B2C에에서 빌드할 수 있습니다."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: 응용 프로그램 유형
Azure AD(Azure Active Directory) B2C는 다양한 최신 앱 아키텍처의 인증을 지원합니다. Hello 업계 표준 프로토콜을 기반 모두 [OAuth 2.0](active-directory-b2c-reference-protocols.md) 또는 [OpenID Connect](active-directory-b2c-reference-protocols.md)합니다. 이 문서에는 간단 하 게 빌드할 수 있는 앱의 hello 유형에 대해 설명, hello 언어 및 플랫폼에 관계 없이 것이 좋습니다. 또한 이해 하도록 하기 전에 hello 높은 수준의 시나리오 [응용 프로그램을 빌드](active-directory-b2c-overview.md#get-started)합니다.

## <a name="hello-basics"></a>hello 기본 사항
Azure AD B2C를 사용 하는 모든 응용 프로그램에 등록 해야 프로그램 [B2C 디렉터리](active-directory-b2c-get-started.md) hello를 통해 [Azure 포털](https://portal.azure.com/)합니다. 수집 하 고 몇 가지 값 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 등록 프로세스:

* 앱을 고유하게 식별하는 **응용 프로그램 ID**
* A **리디렉션 URI** 사용된 toodirect 응답 백 tooyour 앱 일 수 있는 합니다.
* 다른 모든 시나리오 관련 값. 자세한 내용은 자세한 방법을 너무[앱을 등록](active-directory-b2c-app-registration.md)합니다.

Hello 앱을 등록 한 후 통신 Azure AD와 Azure AD toohello v2.0 끝점 요청을 전송 하 여:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

각 전송 된 요청은 AD B2C tooAzure 지정는 **정책**합니다. Azure AD의 hello 동작을 제어 하는 정책입니다. 또한 이러한 끝점 toocreate 고도로 사용자 지정 가능한 집합이 사용자 환경 사용할 수 있습니다. 공통 정책에는 등록 정책, 로그인 정책 및 프로필 편집 정책이 포함됩니다. 정책을 사용 하 여 잘 모르는 경우 읽어야 할 Azure AD B2C hello [확장 가능한 정책 프레임 워크](active-directory-b2c-reference-policies.md) 계속 하기 전에.

v2.0 끝점이 있는 모든 응용 프로그램의 hello 상호 작용 비슷한 높은 수준의 패턴을 따릅니다.

1. hello 앱 hello 사용자 toohello v2.0 끝점 tooexecute 보냅니다는 [정책](active-directory-b2c-reference-policies.md)합니다.
2. hello 사용자 hello 정책 toohello 정책 정의 따라 완료 합니다.
3. hello 앱 hello v2.0 끝점에서 일종의 보안 토큰을 받습니다.
4. hello 앱 hello 보안 보호 토큰 tooaccess 정보 또는 보호 된 리소스를 사용합니다.
5. hello 리소스 서버에 대 한 액세스를 부여할 수 있는 hello 보안 토큰 tooverify를 확인 합니다.
6. hello 앱 hello 보안 토큰을 주기적으로 새로 고쳐집니다.

<!-- TODO: Need a page for libraries toolink too-->
다음이 단계 hello 유형의 작성 하는 응용 프로그램에 따라 약간씩 다를 수 있습니다. 오픈 소스 라이브러리를 hello 세부 정보를 해결할 수 있습니다.

## <a name="web-apps"></a>웹 앱
서버에서 호스팅되며 브라우저를 통해 액세스하는 웹앱(.NET, PHP, Java, Ruby, Python, Node.js 등)의 경우 Azure AD B2C는 모든 사용자 환경에 [OpenID Connect](active-directory-b2c-reference-protocols.md) 를 지원합니다. 여기에는 로그인, 등록 및 프로필 관리가 포함됩니다. OpenID Connect의 Azure AD B2C hello 구현에서 웹 앱 인증 요청 tooAzure AD를 실행 하 여 이러한 사용자 환경을 시작 합니다. hello 요청의 hello 결과는 `id_token`합니다. 이 보안 토큰이 hello 사용자의 id를 나타냅니다. 또한 클레임의 hello 형태로 hello 사용자에 대 한 정보를 제공 합니다.

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Hello에 사용할 수 있는 tooan 앱 토큰 및 클레임 유형의 hello에 대 한 자세한 정보 [B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.

웹앱에서 [정책](active-directory-b2c-reference-policies.md) 의 각 실행에서는 이러한 수준 높은 단계를 수행합니다.

![웹앱 스윔 레인 이미지](./media/active-directory-b2c-apps/webapp.png)

유효성 검사의 hello `id_token` Azure AD에서 받은 공개 서명 키를 사용 하 여 hello 사용자 충분 한 tooverify hello id입니다. 또한 후속 페이지 요청에서 사용 되는 tooidentify hello 사용자 일 수 있는 세션 쿠키를 설정 합니다.

toosee 작업에서이 시나리오 중 하나를 시도 hello 웹 응용 프로그램 로그인 코드 샘플에서는 우리의 [섹션 시작](active-directory-b2c-overview.md#get-started)합니다.

웹 서버 응용 프로그램 추가 toofacilitating 간단한 로그인에서는 tooaccess 백 엔드 웹 서비스 할 수도 있습니다. 이 경우 hello 웹 앱 약간 다른 수행할 수 [OpenID Connect 흐름](active-directory-b2c-reference-oidc.md) 및 권한 부여 코드를 사용 하 여 토큰을 획득 하 고 새로 고침 토큰입니다. 이 시나리오는 hello 다음에 표시 된 [웹 Api 섹션](#web-apis)합니다.

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>Web API
앱의 RESTful 웹 API와 같은 Azure AD B2C toosecure 웹 서비스를 사용할 수 있습니다. 웹 Api 토큰을 사용 하 여 들어오는 HTTP 요청을 인증 하 여 OAuth 2.0 toosecure 해당 데이터를 사용할 수 있습니다. web API의 hello 호출자의 HTTP 요청 hello 인증 헤더에 토큰을 추가합니다.

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

hello 웹 API hello 토큰에서 인코딩 되는 클레임에서 hello 호출자에 대 한 hello 토큰 tooverify hello API 호출자의 id 및 tooextract 정보를 사용할 수 있습니다. Hello에 사용할 수 있는 tooan 앱 토큰 및 클레임 유형의 hello에 대 한 자세한 정보 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.

> [!NOTE]
> Azure AD B2C는 현재 고유한 잘 알려진 클라이언트에서 액세스하는 Web API만을 지원합니다. 예를 들어 전체 앱이 iOS 앱, Android 앱 및 백 엔드 Web API를 포함할 수도 있습니다. 이 아키텍처를 완전히 지원합니다. 동일한 웹 API 현재 지원 되지 않습니다를 tooaccess hello 다른 iOS 앱 같은 파트너 클라이언트를 허용 합니다. 단일 응용 프로그램 ID를 공유 해야 전체 응용 프로그램의 hello 구성 요소를 모두
>
>

Web API는 웹앱, 데스크톱 및 모바일 앱, 단일 페이지 앱, 서버 쪽 데몬 및 다른 Web API까지 포함하여 많은 유형의 클라이언트에서 토큰을 받을 수 있습니다. Web API를 호출 하는 웹 앱에 대 한 hello 전체 흐름의 예는 다음과 같습니다.

![웹앱 Web API 스윔 레인 이미지](./media/active-directory-b2c-apps/webapi.png)

hello에 대 한 읽기 권한 부여 코드, 새로 고침 토큰 및 토큰을 가져오기 위한 hello 단계에 대해 자세히 toolearn [OAuth 2.0 프로토콜](active-directory-b2c-reference-oauth-code.md)합니다.

방법을 Azure AD B2C 체크 아웃 hello 사용 하 여 웹 API toosecure 웹의 자습서에서는 API toolearn 우리의 [섹션 시작](active-directory-b2c-overview.md#get-started)합니다.

## <a name="mobile-and-native-apps"></a>모바일 및 네이티브 앱
모바일 및 데스크톱 앱 같은 장치에 설치 된 앱을 tooaccess 백 엔드 서비스 또는 사용자 대신 웹 Api 필요한 경우가 많습니다. 사용자 지정 된 id 관리 환경을 tooyour 네이티브 앱을 추가 하 고 안전 하 게 Azure AD B2C 및 hello를 사용 하 여 백 엔드 서비스를 호출할 수 [OAuth 2.0 인증 코드 흐름](active-directory-b2c-reference-oauth-code.md)합니다.  

Hello 응용 프로그램 실행이 흐름에서 [정책](active-directory-b2c-reference-policies.md) 수신는 `authorization_code` hello 사용자 hello 정책 완료 된 후에 Azure AD에서 합니다. hello `authorization_code` 나타냅니다 hello hello 사용자가 현재 로그인를 위해 응용 프로그램의 사용 권한 toocall 백 엔드 서비스입니다. hello 앱 hello를 교환할 수 있습니다 `authorization_code` 에 대 한 hello 백그라운드로 `id_token` 및 `refresh_token`합니다.  hello 앱 hello צ ְ ײ `id_token` tooauthenticate tooa 백 엔드에 web API의 HTTP 요청입니다. Hello를 사용할 수도 있습니다 `refresh_token` 새 tooget `id_token` 이전 만료 될 때입니다.

> [!NOTE]
> Azure AD B2C는 현재 토큰을 사용 하는 tooaccess 응용 프로그램 자체의 백 엔드 웹 서비스를 지원 합니다. 예를 들어 전체 앱이 iOS 앱, Android 앱 및 백 엔드 Web API를 포함할 수도 있습니다. 이 아키텍처를 완전히 지원합니다. OAuth 2.0 액세스 토큰을 사용 하 여 iOS 앱 tooaccess 파트너 웹 API를 허용 현재 지원 되지 않습니다. 단일 응용 프로그램 ID를 공유 해야 전체 응용 프로그램의 hello 구성 요소를 모두
>
>

![네이티브 앱 스윔 레인 이미지](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>현재 제한 사항
Azure AD B2C hello 유형의 앱을 다음 현재 지원 하지 않지만 hello 로드맵에 있습니다. 

### <a name="daemonsserver-side-apps"></a>디먼/서버 쪽 앱
장기 실행 프로세스를 포함 하는 또는 사용자의 hello 존재 하지 않고 작동 하는 앱 tooaccess 웹 Api와 같은 리소스를 보호 하는 방법이 있어야 합니다. 이러한 응용 프로그램 인증 하 고 hello 응용 프로그램 id (사용자의 위임 된 id 아님)를 사용 하 고 hello OAuth 2.0 클라이언트 자격 증명 흐름을 사용 하 여 토큰을 가져올 수 있습니다.

이 흐름은 Azure AD B2C에서 현재 지원되지 않습니다. 이러한 앱은 대화형 사용자 흐름이 발생한 후에만 토큰을 가져올 수 있습니다.

### <a name="web-api-chains-on-behalf-of-flow"></a>Web API 체인(On-Behalf-Of 흐름)
웹 API에 필요한 toocall 여기서 Azure AD B2C 통해 보안 되며 둘 다 다른 다운스트림 웹 API를 포함 하는 많은 아키텍처. 이 시나리오는 Web API 백 엔드를 가지고 있는 네이티브 클라이언트에서 일반적입니다. 이 다음 hello Azure AD Graph API와 같은 Microsoft 온라인 서비스를 호출합니다.

Hello OAuth 2.0 JWT 전달자 자격 증명 부여 라고도 hello에-를 대신 하 여-의 흐름을 사용 하 여이 연결 된 웹 API 시나리오를 지원할 수 있습니다.  그러나 Azure AD B2C hello에 hello에 대신-흐름 현재 구현 되지 않습니다.
