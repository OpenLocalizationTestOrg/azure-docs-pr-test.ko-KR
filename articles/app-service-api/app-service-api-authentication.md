---
title: "aaaAuthentication 및 Azure 앱 서비스에서 API 앱에 대 한 권한 부여 | Microsoft Docs"
description: "Azure 앱 서비스 API 앱에 대해 제공 하는 hello 인증 및 권한 부여 서비스를 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Azure 앱 서비스의 API 앱에 대한 인증 및 권한 부여
## <a name="overview"></a>개요
> [!NOTE]
> 이 항목에는 마이그레이션된 tooa 통합 됩니다 [응용 프로그램 서비스 인증 / 권한 부여](../app-service/app-service-authentication-overview.md) 웹, 모바일 및 API 앱에 설명 하는 항목입니다.
> 
> 

Azure App Service는 [OAuth 2.0](#oauth) 및 [OpenID Connect](#oauth)를 구현하는 기본 제공 인증 서비스를 제공합니다. 이 문서에서는 hello 서비스 및 Azure 앱 서비스에서 API 앱에 사용할 수 있는 옵션을 설명 합니다.

hello 다음 다이어그램에서는 응용 프로그램 서비스 인증의 주요 특징을 일부를 보여 줍니다.

* 들어오는 API 요청을 전처리합니다. 즉, 앱 서비스에서 지원하는 모든 언어 또는 프레임워크와 작동합니다.
* 제공 양을 인증이 작동 하기 위한 몇 가지 옵션을 원하는 toodo 사용자 코드에서.
* 최종 사용자 및 서비스 계정 인증 모두에 대해 작동합니다. 
* 여기서는 Azure Active Directory, Facebook, Google, Twitter 및 Microsoft 계정의 5가지 ID 공급자를 지원합니다.
* 그 작동 hello API 앱, 웹 앱 및 모바일 앱에 대해 동일 합니다.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>언어 알 수 없음
앱 서비스 인증 처리 요청을 모든 언어 또는 프레임 워크에서 작성 된 앱의 API는 hello 인증 기능이 작동 의미 API 앱에 도달 하기 전에 발생 합니다.  사용자 API는 ASP.NET, Java, Node.js 또는 앱 서비스에서 지원하는 모든 프레임워크를 기반으로 할 수 있습니다.

앱 서비스는 HTTP 요청의 인증 헤더 hello에에서 hello JSON 웹 토큰 (JWT)에 전달 하 고 작성 된 코드에서 모든 언어 또는 프레임 워크 정보를 얻을 수 hello 필요한 hello에서 토큰. 또한 응용 프로그램 서비스 사용 하면 보다 쉽게 toohello 가장 일반적으로 사용 되는 클레임 hello 다음과 같은 몇 가지 특수 한 헤더를 설정 하 여:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

.NET API에서 hello를 사용할 수 있습니다 `Authorize` 특성을 쉽게 작성할 수 있는 세분화 된 권한 부여의 코드에 따라 클레임.NET 클래스에 사용자에 대 한 클레임 정보가 채워집니다.

## <a name="multiple-protection-options"></a>여러 보호 옵션
앱 서비스는 익명 HTTP 요청이 API 앱에 도달하지 못하도록 하고 모든 요청을 전달하고 이를 포함하는 요청에 대한 토큰의 유효성을 검사하거나 작업 없이 모든 요청을 통과시킬 수 있습니다.

1. 인증 된 요청 tooreach만 API 앱을 허용 합니다.
   
    앱 서비스는 hello 인증 공급자에 대 한 tooa 로그온 페이지를 리디렉션합니다 익명 요청은 브라우저에서 수신 되 면 (Azure AD, Google, Twitter 등) 사용자가 선택한 합니다. 
   
    이 옵션을 사용에서 필요 없는 toowrite 인증 코드 전혀 응용 프로그램 및 권한 부여 코드 단순 하 여 hello 가장 중요 한 클레임 hello HTTP 헤더에 제공 됩니다.
2. 모든 요청 tooreach API 앱을 허용 하지만 인증 된 요청의 유효성을 검사 하 고 hello HTTP 헤더의 인증 정보를 따라 전달 합니다.
   
    이 옵션을이 선택 하면 보다 융통성 있게 익명 요청을 처리 하지만 API를 사용 하 여 익명 사용자가 tooprevent toowrite 코드가 있는 합니다. Hello 가장 인기 있는 클레임의 HTTP 요청 헤더 hello에에서 전달 되는 경우 이후 인증 코드는 비교적 간단 합니다.
3. 모든 요청 tooreach API 허용, hello 요청에 인증 정보에 대해 어떤 작업도 없습니다.
   
    이 옵션의 인증 및 권한 부여 tooyour 응용 프로그램 코드를 완전히 hello 작업을 유지합니다.

Hello에 [Azure 포털](https://portal.azure.com/), hello에서 원하는 hello 옵션을 선택 하면 **인증 / 권한 부여** 블레이드입니다.

![](./media/app-service-api-authentication/authblade.png)

옵션 1 및 2에 대 한 설정 **응용 프로그램 서비스 인증**, 및 hello **요청이 인증 되지 않은 경우 동작 tootake** 드롭다운 목록에서 선택 **로그인** 또는 **요청 허용 동작이 없습니다**합니다.  선택 하면 **로그인**, toochoose 인증 공급자도 보유 하 고 해당 공급자를 구성 합니다.

![](./media/app-service-api-authentication/actiontotake.png)

방법에 대 한 자세한 내용은 tooconfigure 인증 참조 [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다. hello 문서 tooAPI 앱 뿐 아니라 모바일 앱을 적용 하며 hello에 대 한 tooother 아티클을 다른 인증 공급자 연결 합니다.

## <a id="internal"></a> 서비스 계정 인증
앱 서비스 인증 같은 내부 시나리오 한 API 앱 tooanother API 앱에서 호출 하는 데 사용할 수 있습니다. 이 시나리오에서는 최종 사용자 자격 증명 대신, 서비스 계정에 대한 자격 증명을 사용하여 토큰을 가져옵니다. Azure Active Directory에서 서비스 계정은 *서비스 주체* 라고도 하며, 이러한 계정을 사용하는 인증을 서비스 간 시나리오라고도 합니다. 

서비스 간 시나리오에 대 한 Azure Active Directory를 사용 하 여 API 앱을 호출 하는 hello를 보호 하 고 hello API 앱을 호출할 때 AAD 서비스 주체 권한 부여 토큰을 제공 합니다. Hello 클라이언트 ID와 클라이언트 hello AAD 응용 프로그램에서에서 암호를 제공 하 여 토큰을 가져옵니다. Hello 모바일 서비스 Zumo 토큰을 처리 하기 위한 사용 되는 toobe true와 같이 필요한 된 특별 한 Azure 전용 코드가 없습니다. Hello 자습서에서 검사 하는 ASP.NET API 앱을 사용 하 여이 시나리오의 예로 [서비스 API 앱에 대 한 사용자 인증](app-service-api-dotnet-service-principal-auth.md)합니다.

앱 서비스 인증을 사용 하지 않고 toohandle 서비스 간 시나리오를 원하는 경우 클라이언트 인증서 또는 기본 인증을 사용할 수 있습니다. Azure의 클라이언트 인증서에 대 한 정보를 참조 하십시오. [어떻게 tooConfigure 웹 앱에 대 한 상호 인증 TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md)합니다. ASP.NET에서 기본 인증에 대한 자세한 내용은 [ASP.NET Web API 2에서의 인증 필터](http://www.asp.net/web-api/overview/security/authentication-filters)를 참조하세요.

앱 서비스 논리 앱 tooan API 앱에서 계정 인증 서비스는에서 설명 하는 특별 한 경우 [논리 앱과 앱 서비스에서 호스팅되는 사용자 지정 API를 사용 하 여](../logic-apps/logic-apps-custom-hosted-api.md)합니다.

## <a name="mobile-client-authentication"></a>모바일 클라이언트 인증
방법에 대 한 내용은 모바일 클라이언트 로부터의 인증 toohandle 참조 hello [모바일 앱에 대 한 인증에 대 한 설명서](../app-service-mobile/app-service-mobile-ios-get-started-users.md)합니다. 앱 서비스 인증은 hello 모바일 앱 및 API 앱 모두에 동일 합니다.

## <a name="more-information"></a>자세한 정보
인증 및 Azure 앱 서비스의 권한 부여에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.

* [앱 서비스 인증/권한 부여 확장](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (hello hello 페이지 위쪽에 다른 인증 공급자에 대 한 링크를 포함 합니다.) 

OAuth 2.0, OpenID Connect 및 JSON 웹 토큰 (JWT)에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하십시오.

* [OAuth 2.0 시작](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [소개 tooOAuth2 OpenID Connect 및 JSON 웹 토큰 (JWT)-Pluralsight 과정](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [ASP.NET에서 여러 클라이언트에 대한 RESTful API 빌드 및 보안 설정 - Pluralsight 과정(영문)](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Azure Active Directory에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.

* [Azure AD 시나리오](http://aka.ms/aadscenarios)
* [Azure AD 개발자 가이드](http://aka.ms/aaddev)
* [Azure AD 샘플](http://aka.ms/aadsamples)

## <a name="next-steps"></a>다음 단계
이 문서에서는 API 앱에 사용할 수 있는 앱 서비스의 인증 및 권한 부여 기능을 설명했습니다. hello hello를 가져올 수 있는 다음 자습서 시작 계열 표시 방법을 tooimplement [앱 서비스 API 앱에서 사용자 인증](app-service-api-dotnet-user-principal-auth.md)합니다.

