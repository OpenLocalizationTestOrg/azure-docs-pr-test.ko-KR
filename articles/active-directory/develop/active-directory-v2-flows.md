---
title: "hello Azure Active Directory v2.0 끝점에 대 한 aaaApp 형식 | Microsoft Docs"
description: "응용 프로그램 및 hello Azure Active Directory v2.0 끝점에서 지 원하는 시나리오 hello 형식입니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Hello Azure Active Directory v2.0 끝점에 대 한 응용 프로그램 형식
hello Azure Active Directory (Azure AD) v 2.0 끝점 인증에 대 한 지원의 업계 표준 프로토콜에 따라 모든 최신 응용 프로그램 아키텍처의 다양 한 [OAuth 2.0, OpenID Connect](active-directory-v2-protocols.md)합니다. 이 문서에서는 hello 유형의 기본 설정된 언어 또는 플랫폼에 관계 없이 Azure AD v 2.0을 사용 하 여 빌드할 수 있는 앱을 설명 합니다. hello이 문서의 정보는 하기 전에 높은 수준의 시나리오를 이해 하는 디자인 된 toohelp [hello 코드 작업 시작](active-directory-appmodel-v2-overview.md#getting-started)합니다.

> [!NOTE]
> hello v2.0 끝점은 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다. 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

## <a name="hello-basics"></a>hello 기본 사항
Hello의 hello v2.0 끝점을 사용 하 여 각 앱을 등록 해야 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com)합니다. hello 응용 프로그램 등록 프로세스는 수집 하 고 앱에 대 한 이러한 값을 할당 합니다.

* 앱을 고유하게 식별하는 **응용 프로그램 ID**
* A **리디렉션 URI** toodirect 응답 백 tooyour 응용 프로그램을 사용할 수 있는
* 다른 몇 가지 시나리오 관련 값.

자세한 내용은 자세한 방법을 너무[앱을 등록](active-directory-v2-app-registration.md)합니다.

Hello 앱 등록 되 면 hello 앱 toohello Azure AD v2.0 끝점 요청을 전송 하 여 Azure AD와 통신 합니다. 오픈 소스 프레임 워크 및 이러한 요청의 hello 세부 사항을 처리 하는 라이브러리를 제공 합니다. 있습니다 hello 옵션 tooimplement hello 인증 논리 직접 만들어 요청 toothese 끝점:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>웹 앱
웹 응용 프로그램 (.NET, PHP, Java, Ruby, Python, 노드)는 hello 브라우저를 통해 사용자 액세스를 사용할 수 있습니다 [OpenID Connect](active-directory-v2-protocols.md) 사용자 로그인에 대 한 합니다. OpenID Connect의 hello 웹 응용 프로그램 ID 토큰을 받습니다. ID 토큰은 hello 사용자의 id를 확인 하 고 클레임의 hello 형태로 hello 사용자에 대 한 정보를 제공 하는 보안 토큰:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

토큰 및 클레임 hello에서 사용할 수 있는 tooan 응용 프로그램은 hello 형식 모두에 대해 학습할 수 있는 [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다.

웹 서버 응용 프로그램 hello 로그인 인증 흐름 같은 대략적인 단계를 수행합니다.

![웹앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Hello v2.0 끝점에서 수신 되는 공개 서명 키 hello ID 토큰을 확인 하 여 hello 사용자의 id를 확인할 수 있습니다. 다음 페이지 요청에 사용 되는 tooidentify hello 사용자 일 수 있는 세션 쿠키 설정 됩니다.

우리의 v 2.0에서 toosee 작업 시도 hello 웹 앱에 로그인 코드 중 하나에서이 시나리오 샘플 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.

또한 toosimple 로그인, 웹 서버 앱 tooaccess REST API와 같은 다른 웹 서비스를 필요로 할 수 있습니다. 이 경우 hello 웹 서버 응용 프로그램은에 참여 결합 된 OAuth 2.0 및 OpenID Connect 흐름 hello를 사용 하 여 [OAuth 2.0 인증 코드 흐름](active-directory-v2-protocols.md)합니다. 이 시나리오에 대한 자세한 내용은 [웹앱 및 Web API 시작](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)을 참조하세요.

## <a name="web-apis"></a>Web API
Hello v2.0 끝점 toosecure와 같은 웹 서비스 응용 프로그램의 RESTful 웹 API를 사용할 수 있습니다. ID 토큰 및 세션 쿠키는 대신 웹 API를 사용 하 여 OAuth 2.0 액세스 토큰 toosecure의 데이터 및 tooauthenticate 들어오는 요청입니다. 웹 API의 hello 호출자의 HTTP 요청을 다음과 같이 hello 인증 헤더에 액세스 토큰을 추가합니다.

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

웹 API hello hello 액세스 토큰에서 인코딩 되는 클레임에서 hello 호출자에 대 한 hello 액세스 토큰 tooverify hello API 호출자의 id 및 tooextract 정보를 사용 합니다. 토큰 및 클레임을 사용할 수 있는 tooan 앱 hello 형식 모두에 대해 toolearn 참조 hello [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다.

웹 API에 사용자가 hello 전원 tooopt 제공 하거나 권한을 라고도 노출 하 여 특정 기능이 나 데이터 옵트아웃 수 [범위](active-directory-v2-scopes.md)합니다. 호출 응용 프로그램 tooacquire 권한 tooa 범위, hello 사용자 toohello 범위는 흐름 중 동의 해야 합니다. hello v2.0 끝점 권한에 대 한 hello 사용자에 게 요청 하 고 모든 액세스 토큰에 사용 권한을 웹 API 수신 하는 hello 기록 합니다. hello 웹 API에는 각 호출에서 수신 하 고 인증 검사를 수행 hello 액세스 토큰을 확인 합니다.

Web API는 웹 서버 앱, 데스크톱 및 모바일 앱, 단일 페이지 앱, 서버 쪽 데몬 및 다른 Web API까지 포함하여 모든 유형의 앱에서 액세스 토큰을 받을 수 있습니다. hello 웹 API에 대 한 상위 수준 흐름은 다음과 같습니다.

![Web API 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toosecure OAuth2 액세스 토큰을 체크 아웃 hello 웹 API 코드를 사용 하 여 Web API에서 샘플링 하는 방법을 toolearn 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.

대부분의 경우에서 web Api는 toomake tooother 다운스트림 웹 Api를 Azure Active Directory를 통해 보안이 유지 되는 아웃 바운드 요청도 필요 합니다.  toodo, 웹 Api 활용할 수 Azure AD의 **를 대신 하 여의에서** 흐름 hello web API tooexchange 아웃 바운드 요청에 사용 되는 다른 액세스 토큰 toobe에 대 한 수신 액세스 토큰을 허용 합니다.  에 설명 된 hello v 2.0 끝점의 흐름을 대신 하 여 [여기에 대해 자세히 설명](active-directory-v2-protocols-oauth-on-behalf-of.md)합니다.

## <a name="mobile-and-native-apps"></a>모바일 및 네이티브 앱
Tooaccess 백 엔드 서비스 또는 웹 Api 데이터를 저장 하 고 사용자를 대신 하는 기능을 수행 하는 장치 설치 된 앱은 모바일 및 데스크톱 앱 필요한 경우가 많습니다. 이러한 앱 hello를 사용 하 여 로그인 및 권한 부여 tooback 간 서비스를 추가할 수 [OAuth 2.0 인증 코드 흐름](active-directory-v2-protocols-oauth-code.md)합니다.

이 흐름에서 hello 앱 hello 사용자가 로그인 할 때 hello v2.0 끝점에서 인증 코드를 받습니다. hello 권한 부여 코드 나타냅니다 hello hello 사용자가 로그인를 위해 응용 프로그램의 사용 권한 toocall 백 엔드 서비스입니다. hello 앱 OAuth 2.0 액세스 토큰 및 새로 고침 토큰에 대 한 hello 백그라운드로 hello 인증 코드를 교환할 수 있습니다. hello 앱 HTTP 요청 시에서 hello 액세스 토큰 tooauthenticate tooWeb Api를 사용 하 여 하 고 이전 액세스 토큰이 만료 되 면 hello 새로 고침 토큰 tooget 새 액세스 토큰을 사용할 수 있습니다.

![네이티브 앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>단일 페이지 앱(JavaScript)
대부분의 최신 앱에는 주로 Javascript로 작성되고 AngularJS, Ember.js, Durandal 등과 같은 프레임워크로도 작성되는 단일 페이지 앱 프런트 엔드가 있습니다. Azure AD hello v2.0 끝점 hello를 사용 하 여 이러한 응용 프로그램 지원 [OAuth 2.0 암시적 흐름](active-directory-v2-protocols-implicit.md)합니다.

이 흐름에서 hello 앱에서 hello에서 직접 토큰을 수신 v2.0 모든 서버 간 교환 하지 않고 끝점에 권한을 부여 합니다. 모든 인증 논리 및 세션 처리는 전적으로 추가 하는 페이지 리디렉션도 없이 hello JavaScript 클라이언트에서 수행 됩니다.

![암시적 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee 작업에서이 시나리오 중 하나를 시도 hello 단일 페이지 응용 프로그램 코드 샘플에서는 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.

## <a name="daemons-and-server-side-apps"></a>디먼 및 서버 쪽 앱
장기 실행 프로세스 또는 사용자와 상호 작용 없이 작동 하는 앱 tooaccess 웹 Api와 같은 리소스를 보호 하는 방법이 있어야 합니다. 이러한 응용 프로그램에서 인증 하 고 hello 응용 프로그램의 id를 사용 하 여 토큰을 가져올 수 대신 사용자의 id hello OAuth 2.0 클라이언트 자격 증명 흐름을 위임 합니다.

이 흐름에서 hello와 직접 상호 작용 hello 앱 `/token` 끝점 tooobtain 끝점:

![디먼 앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild 데몬 앱에서 hello 클라이언트 자격 증명 설명서를 참조 하십시오. 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션 또는 시도 [.NET 예제 응용 프로그램](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)합니다.
