---
title: "개요 - Azure AD B2C | Microsoft Docs"
description: "Azure Active Directory B2C를 사용하여 소비자 지향 응용 프로그램 개발"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure AD B2C: 등록 및 로그인에 대해 걱정할 필요 없이 앱에 초점 맞추기

Azure AD B2C는 웹 및 모바일 응용 프로그램을 위한 클라우드 ID 관리 솔루션입니다. Id의 수백만 toohundreds 크기가 조정 되는 항상 사용 가능한 글로벌 서비스는 엔터프라이즈급 보안 플랫폼에 기반하여 Azure AD B2C는 응용 프로그램, 비즈니스 및 고객을 보호합니다.

Azure AD B2C는 최소 구성으로 응용 프로그램 tooauthenticate를 수 있습니다.

* **소셜 계정**(예: Facebook, Google, LinkedIn 등)
* **엔터프라이즈 계정**(OpenID Connect 또는 SAML 등의 개방형 표준 프로토콜 사용)
* **로컬 계정**(이메일 주소 및 암호 또는 사용자 이름 및 암호)

## <a name="get-started"></a>시작

먼저에 설명 된 hello 단계를 사용 하 여 자신의 테 넌 트를 가져올 [Azure AD B2C 테 넌 트 만들기](active-directory-b2c-get-started.md)합니다.

그 다음, 응용 프로그램 개발 시나리오를 선택합니다.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![모바일 및 데스크톱 앱](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />모바일 및 데스크톱 앱</center> | [개요](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Web Apps](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [개요](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.JS](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![단일 페이지 앱](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />단일 페이지 앱</center> | [개요](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![Web API](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />Web API</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [.NET Web API 호출](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>새로운 기능

나중에 변경 내용 toohello Azure Active Directory B2C에 대 한 toolearn 자주 다시 여기를 선택 합니다. 또한 @AzureAD를 사용하여 업데이트에 대해 트윗합니다.

* "기본 제공 정책" (일반 공급) hello 너무 또한 ["사용자 지정 정책"](active-directory-b2c-overview-custom.md) 이제 기능은 공개 미리 보기에서 사용할 수 있습니다.  사용자 지정 정책은 hello 컴퍼지션 identity 경험에 대 한 제어 해야 하는 identity 전문가 위한 사용 됩니다.
* hello [액세스 토큰](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) 이제 기능은 공개 미리 보기에서 사용할 수 있습니다.
* [유럽 기반 Azure AD B2C의 일반 공급](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/) 디렉터리를 발표했습니다.
* 증가하는 [Github의 코드 샘플](https://github.com/Azure-Samples?q=b2c) 라이브러리를 확인해 보세요.

## <a name="how-tooarticles"></a>Tooarticles 방법

자세한 내용은 방법 toouse 특정 Azure Active Directory B2C 기능:

* 소비자 지향 응용 프로그램에서 사용하기 위해 [Facebook](active-directory-b2c-setup-fb-app.md), [Google +](active-directory-b2c-setup-goog-app.md), [Microsoft 계정](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) 및 [LinkedIn](active-directory-b2c-setup-li-app.md) 계정을 구성합니다.
* [소비자에 대 한 사용자 지정 특성 toocollect 정보를 사용 하 여](active-directory-b2c-reference-custom-attr.md)합니다.
* [소비자 지향 응용 프로그램에서 Azure Multi-Factor Authentication을 사용합니다](active-directory-b2c-reference-mfa.md).
* [소비자를 위해 셀프 서비스 암호 재설정을 설정합니다](active-directory-b2c-reference-sspr.md).
* [등록의 hello 모양과 느낌을 사용자 지정, 서명, 시작 및 다른 소비자 용 페이지](active-directory-b2c-reference-ui-customization.md) Azure Active Directory B2C에서 제공 하는 합니다.
* [사용 하 여 hello Azure Active Directory 그래프 API tooprogrammatically 만들기, 읽기, 업데이트 및 삭제 소비자](active-directory-b2c-devquickstarts-graph-dotnet.md) Azure Active Directory B2C 테 넌 트에 있습니다.

## <a name="next-steps"></a>다음 단계

이러한 링크는 심층에서 hello 서비스를 탐색 하는 데 유용 합니다.

* Hello 참조 [가격 정보를 Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/)합니다.
* Azure Active Directory B2C에 대한 [코드 샘플](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c)을 검토합니다. 
* 스택 오버플로에 hello를 사용 하 여 도움말을 보려면 [azure ad-b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) 태그입니다.
* 사용 하 여 의견을 보내주십시오 [사용자 음성](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), toohear 원하는!
* 검토 hello [Azure AD B2C 프로토콜 참조](active-directory-b2c-reference-protocols.md)합니다.
* 검토 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.
* 읽기 hello [Azure Active Directory B2C Faq](active-directory-b2c-faqs.md)합니다.
* [Azure Active Directory B2C에 대한 파일 지원 요청](active-directory-b2c-support.md)

## <a name="get-security-updates-for-our-products"></a>당사 제품에 대한 보안 업데이트 가져오기

보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.

