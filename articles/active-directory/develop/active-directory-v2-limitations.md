---
title: "Active Directory aaaAzure v2.0 끝점 제한 사항 및 제한 사항 | Microsoft Docs"
description: "목록 hello Azure AD v2.0 끝점에 대 한 제한 사항입니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>Hello v2.0 끝점을 사용 해야 합니까?
Azure Active Directory와 통합 하는 응용 프로그램을 빌드할 때 hello v2.0 끝점 및 인증 프로토콜 요구 사항을 충족 하는지 여부를 toodecide가 필요 합니다. Azure Active Directory의 원래 끝점은 계속해서 완전히 지원되며 v2.0보다 더 많은 기능이 제공되는 측면이 있습니다. 그러나 v2.0 끝점 hello [상당한 혜택이 도입](active-directory-v2-compare.md) 개발자를 위한 합니다.

다음은 현 시점에서 개발자를 위한 간단한 권장 사항입니다.

* 응용 프로그램에서 개인 Microsoft 계정을 지원 해야 하는 경우 hello v2.0 끝점을 사용 합니다. 하지만 수행 하기 전에이 문서에서 설명 하는 hello 제한 사항을 이해 하는 확인할 수 있습니다.
* 응용 프로그램만 toosupport Microsoft 작업 및 학교 계정에 필요한 hello v2.0 끝점을 사용 하지 마십시오. 대신, tooour 참조 [Azure AD 개발자 가이드](active-directory-developers-guide.md)합니다.

시간이 지남에 따라 hello v2.0 끝점 toouse hello v2.0 끝점만 할 수 있도록 tooeliminate hello 제한 사항이 여기에 나열 된 커집니다. Hello에 그 동안이 문서는 의도 한 toohelp hello v2.0 끝점 적합 한지 여부를 결정 합니다. 이 문서 tooreflect hello의 현재 상태 hello v2.0 끝점 tooupdate를 계속 실행 됩니다. 뒤로 tooreevaluate v2.0 기능에 대 한 요구 사항을 확인 합니다.

Hello v2.0 끝점을 사용 하지 않는 기존 Azure AD 앱 있을 경우 처음부터 필요 toostart 없습니다. Hello 이후에서 우리 방법을 제공 합니다는 toouse 있습니다에 대 한 hello v2.0 끝점을 사용 하 여 기존 Azure AD 응용 프로그램.

## <a name="restrictions-on-app-types"></a>앱 형식에 대한 제한 사항
현재 hello 다음과 같은 유형의 응용 프로그램 지원 되지 않습니다 hello v2.0 끝점에서. 지원 되는 앱 형식에 대 한 참조 [hello Azure Active Directory v2.0 끝점에 대 한 응용 프로그램 형식을](active-directory-v2-flows.md)합니다.

### <a name="standalone-web-apis"></a>독립 실행형 Web API
Hello v2.0 끝점도 사용할 수 있습니다[OAuth 2.0으로 보호 되는 Web API 작성](active-directory-v2-flows.md#web-apis)합니다. 그러나 해당 Web API가 동일한 응용 프로그램 id. hello에 응용 프로그램에서 토큰을 받을 수는 다른 응용 프로그램 ID를 가진 클라이언트에서는 Web API에 액세스할 수 없습니다. 클라이언트 hello가 사용 권한을 tooyour 웹 API를 가져오거나 수 toorequest 수 없습니다.

toobuild 된 클라이언트에서 보낸 토큰을 hello 같은 응용 프로그램 ID를 허용 하는 웹 API를 확인 하려면 어떻게 toosee hello v2.0 끝점 웹 API 샘플에서는 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.

## <a name="restrictions-on-app-registrations"></a>앱 등록에 대한 제한 사항
현재 toointegrate hello v2.0 끝점을 사용 하려는 각 응용 프로그램에 대 한 응용 프로그램 등록에서에서 만들어야 hello 새 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)합니다. 기존 Azure AD 또는 Microsoft 계정 앱 hello v2.0 끝점와 호환 되지 않습니다. 응용 프로그램 등록 포털 hello 이외의 모든 포털에 등록 된 응용 프로그램 hello v2.0 끝점과 호환 되지 않습니다. Hello 이후, tooprovide 방식으로 toouse v2.0 응용 프로그램으로 기존 응용 프로그램을 계획 합니다. 현재 하지만 없는 마이그레이션 경로 hello v2.0 끝점을 사용 하는 기존 앱 toowork에 대 한 합니다.

또한 hello에서 만드는 앱 등록 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) hello 다음 제한 사항을 적용 했습니다.

* 응용 프로그램 ID당 두 개의 앱 암호만 허용됩니다.
* 개인 Microsoft 계정이 있는 사용자가 등록한 앱 등록은 단일 개발자 계정으로만 보고 관리할 수 있습니다. 여러 개발자 간에 공유할 수 없습니다.  Tooshare 원하는 경우 적절 한 여러 개발자가 응용 프로그램 등록, Azure AD 계정 사용 하 여 hello 등록 포털에 로그인 하 여 hello 응용 프로그램을 만들 수 있습니다.
* Hello 리디렉션 허용 되는 URI의 hello 형식에 몇 가지 제한이 있습니다. 리디렉션 Uri에 대 한 자세한 내용은 hello 다음 섹션을 참조 하세요.

## <a name="restrictions-on-redirect-uris"></a>리디렉션 URI에 대한 제한
현재 hello 응용 프로그램 등록 포털에에서 등록 된 앱은 제한 하는 제한 된 tooa 집합 리디렉션 URI 값입니다. 웹 앱 및 서비스에 대 한 URI 체계 hello로 시작 해야 하는 리디렉션 hello `https`, 하 고 모든 리디렉션 URI 값 단일 DNS 도메인을 공유 해야 합니다. 예를 들어 다음 리디렉션 URI 중 하나가 있는 웹앱은 등록할 수 없습니다.

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

hello 등록 시스템 hello hello 기존 리디렉션 URI toohello의 DNS 이름 hello 리디렉션 URI 추가 하는 전체 DNS 이름과 비교 합니다. hello 요청 tooadd hello DNS 이름 hello 다음 조건 중 하나에 해당 하는 경우 실패 합니다.  

* hello 새 리디렉션 URI의 전체 DNS 이름 hello hello 기존 리디렉션 URI의 hello DNS 이름과 일치 하지 않습니다.
* hello 새 리디렉션 URI의 전체 DNS 이름 hello hello 기존 리디렉션 URI의 하위 도메인이 아닌 경우

예를 들어 hello 응용 프로그램에이 리디렉션 URI:

`https://login.contoso.com`

다음과 같이 tooit를 추가할 수 있습니다.

`https://login.contoso.com/new`

이 경우 hello DNS 이름과 정확히 일치합니다. 또는 다음을 수행할 수 있습니다.

`https://new.login.contoso.com`

이 경우 login.contoso.com의 tooa DNS 하위 도메인을 참조 하 합니다. Toohave 로그인 east.contoso.com과 west.contoso.com 로그인 리디렉션 Uri로 되어 있는 앱을 사용 하도록 하려는 경우이 순서로 된 리디렉션 URIs를 추가 해야 합니다.

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

두 개의 하위 도메인의 hello 되기 때문에 먼저 리디렉션 URI, 후자 hello를 추가할 수 있습니다 contoso.com입니다. 이 제한은 향후 릴리스에서 제거될 예정입니다.

tooregister hello 응용 프로그램 등록 포털에서에서 응용 프로그램에서 참조 하는 방법을 toolearn [어떻게 tooregister hello v2.0 끝점을 사용 하 여 앱](active-directory-v2-app-registration.md)합니다.

## <a name="restrictions-on-services-and-apis"></a>서비스 및 API에 대한 제한 사항
Hello 응용 프로그램 등록 포털에에서 등록 된 연결 되 고 있는 hello 목록에 모든 앱에 대 한 로그인 지원 hello v2.0 끝점 현재 [인증 흐름을 지원](active-directory-v2-flows.md)합니다. 그러나 이러한 앱은 매우 제한된 리소스 집합에 대한 OAuth 2.0 액세스 토큰만 획득할 수 있습니다. hello v2.0 끝점 문제에 대해서만 토큰에 액세스 합니다.

* hello 토큰을 요청한 hello 응용 프로그램입니다. 여러 가지 구성 요소 또는 계층의 hello 논리 앱이 구성 된 경우 앱 자체에 대 한 액세스 토큰을 획득할 수 있습니다. toosee이이 시나리오에서 작업을 체크 아웃 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 자습서입니다.
* hello Outlook 메일, 일정 및 연락처 REST Api는 모두 https://outlook.office.com에 있습니다. toolearn toowrite 이러한 Api에 액세스 하는 응용 프로그램 참조 hello [Office 시작](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) 자습서입니다.
* Microsoft Graph API. 에 대 한 자세한 내용은 [Microsoft Graph](https://graph.microsoft.io) hello이 데이터를 사용할 수 있는 tooyou 합니다.

현재 다른 서비스는 지원되지 않습니다. 더 많은 Microsoft 온라인 서비스를 추가할 hello 미래 또한 toosupport 사용자 고유의 사용자가 작성 한 Web Api 및 서비스에 대 한 합니다.

## <a name="restrictions-on-libraries-and-sdks"></a>라이브러리 및 SDK에 대한 제한 사항
현재 hello v2.0 끝점에 대 한 라이브러리 지원이 제한 됩니다. 프로덕션 응용 프로그램에서 toouse hello v2.0 끝점을 사용 하도록 하려는 경우 같은 옵션이 있습니다.

* 웹 응용 프로그램을 작성 하는 경우 Microsoft 일반적으로 사용 가능한 서버 쪽 미들웨어 tooperform 로그인 및 토큰 유효성 검사를 안전 하 게 사용할 수 있습니다. 여기에 ASP.NET 및 hello Node.js Passport 플러그 인에 대 한 hello ID 열린 연결 OWIN 미들웨어를 포함 됩니다. Microsoft 미들웨어를 사용하는 코드 샘플은 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션을 참조하세요.
* 데스크톱 또는 모바일 응용 프로그램을 작성하는 경우 미리 보기 MSAL(Microsoft 인증 라이브러리) 중 하나를 사용할 수 있습니다.  안전 toouse 이므로 프로덕션에서 지 원하는 미리 보기에서 이러한 라이브러리는 프로덕션 응용 프로그램에서 해당 합니다. 미리 보기 및 사용 가능한 라이브러리에서 hello hello 약관 hello에 대 한 자세한 읽을 수 우리의 [인증 라이브러리 참조](active-directory-v2-libraries.md)합니다.
* Microsoft 라이브러리에서 포함 하지 않는 플랫폼에 대 한 직접 보내고 응용 프로그램 코드에서 프로토콜 메시지를 받아서 hello v2.0 끝점과 통합할 수 있습니다. v2.0 OAuth 및 OpenID Connect 프로토콜 hello [명시적으로 문서화](active-directory-v2-protocols.md) toohelp 이러한 통합을 수행 합니다.
* 마지막으로 hello v2.0 끝점과 오픈 소스 열 ID 연결 하 고 OAuth 라이브러리 toointegrate를 사용할 수 있습니다. hello v2.0 프로토콜은 주요 변경 내용 없이 다양 한 프로토콜 오픈 소스 라이브러리와 호환 되어야 합니다. 이러한 종류의 라이브러리 hello 가용성 언어 및 플랫폼에 따라 다릅니다. hello [Open ID 연결](http://openid.net/connect/) 및 [OAuth 2.0](http://oauth.net/2/) 웹 사이트는 인기 있는 구현의 목록을 유지 관리 합니다. 자세한 내용은 참조 [Azure Active Directory v2.0 및 인증 라이브러리](active-directory-v2-libraries.md), 및 오픈 소스 클라이언트 라이브러리 및 샘플 hello v2.0 끝점과 테스트 된 hello 목록입니다.

## <a name="restrictions-on-protocols"></a>프로토콜에 대한 제한 사항
SAML 또는 Ws-federation; hello v2.0 끝점 지원 하지 않습니다. 또한 Open ID 연결 및 OAuth 2.0만 지원합니다.  Hello v2.0 끝점에 OAuth 프로토콜의 모든 기능과 특징이 통합 되었습니다. 현재는 이러한 프로토콜 기능 및 기능 *사용할 수 없는* hello v2.0 끝점에서:

* ID 발급 된 토큰은 hello v2.0 끝점이 포함 되지 않습니다는 `email` hello 사용자 tooview의 사용 권한이 자신의 전자 메일을 획득 하는 경우에 hello 사용자에 대 한 클레임입니다.
* hello OpenID 연결 사용자 정보 끝점이 hello v2.0 끝점에서 구현 되지 않았습니다. 그러나,이 끝점에서 발생 잠재적으로 하는 모든 사용자 프로필 데이터는 hello Microsoft Graph에서에서 사용할 수 있는 `/me` 끝점입니다.
* hello v2.0 끝점 ID 토큰에서 역할 또는 그룹 클레임 발급을 지원 하지 않습니다.
* hello [OAuth 2.0 리소스 소유자 암호 자격 증명 부여](https://tools.ietf.org/html/rfc6749#section-4.3) hello v2.0 끝점에서 지원 되지 않습니다.

추가 하 여, 모든 형태의 hello SAML 또는 Ws-federation 프로토콜 hello v2.0 끝점 지원 하지 않습니다.

toobetter 자세히 읽고 hello v2.0 끝점에서 지 원하는 프로토콜 기능의 hello 범위 이해 우리의 [OpenID Connect 및 OAuth 2.0 프로토콜 참조](active-directory-v2-protocols.md)합니다.

## <a name="restrictions-for-work-and-school-accounts"></a>회사 및 학교 계정에 대한 제한 사항
Windows 응용 프로그램에서 Active Directory 인증 라이브러리 (ADAL)를 사용한 경우 활용 hello SAML Security Assertion Markup Language ()에 대 한 어설션 권한 부여를 사용 하 여 Windows 통합된 인증을 수행 했습니다 수 있습니다. 이 권한 부여를 통해 페더레이션된 Azure AD 테넌트의 사용자는 자격 증명을 입력하지 않고도 해당 온-프레미스 Active Directory 인스턴스로 자동으로 인증할 수 있습니다. 현재 hello SAML 어설션이 grant hello v2.0 끝점에서 지원 되지 않습니다.
