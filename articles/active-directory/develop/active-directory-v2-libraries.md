---
title: "aaaAzure Active Directory v2.0 인증 라이브러리 | Microsoft Docs"
description: "호환 되는 클라이언트 라이브러리 및 서버 미들웨어 라이브러리 및 관련된 라이브러리, 소스 및 hello Azure Active Directory v2.0 끝점에 대 한 샘플 링크 합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Azure Active Directory v2.0 인증 라이브러리
hello Azure Active Directory (Azure AD) v 2.0 끝점 hello 업계 표준 OAuth 2.0 및 OpenID Connect 1.0 프로토콜을 지원합니다. Hello v2.0 끝점과 Microsoft 및 기타 조직에서 다양 한 라이브러리를 사용할 수 있습니다.

Hello v2.0 끝점을 사용 하는 응용 프로그램을 빌드할 때 같은 수명 주기 SDL (Security Development) 방법론을 팔 로우 하는 프로토콜 도메인 전문가 의해 작성 된 라이브러리를 사용 하는 것이 좋습니다 [Microsoft뒤에오는단일hello] [Microsoft-SDL]. Hello 프로토콜에 대 한 코드 toohand 지원 하려는 경우 SDL 방법에 따라 및 각 프로토콜에 대 한 hello 표준 사양에 toohello 보안 고려 사항 확인을 해야 하는 것이 좋습니다.

## <a name="types-of-libraries"></a>라이브러리 유형
Azure AD v2.0은 두 가지 유형의 라이브러리를 사용할 수 있습니다.

* **클라이언트 라이브러리** 네이티브 클라이언트 및 서버 클라이언트 라이브러리 tooget 액세스 토큰을 사용 하 여 Microsoft Graph 같은 리소스를 호출 합니다.
* **서버 미들웨어 라이브러리** 웹앱은 사용자 로그인에 서버 미들웨어 라이브러리를 사용합니다. 웹 Api의 다른 서버 또는 네이티브 클라이언트에서 보낸 서버 미들웨어 라이브러리 toovalidate 토큰을 사용 합니다.

## <a name="library-support"></a>라이브러리 지원
중요 한 tooknow 되기 hello v2.0 끝점을 사용 하는 경우 표준 호환 되는 모든 라이브러리를 선택할 수 있습니다, 때문에 여기서 toogo 지원 합니다. 문제 및 라이브러리 코드에서 기능 요청에 대 한 hello 라이브러리 소유자에 게 문의 합니다. 문제 및 hello 서비스 측 프로토콜 구현에서 기능 요청에 대 한 Microsoft에 문의 하십시오.

라이브러리는 두 지원 범주로 제공됩니다.

* **Microsoft 지원** Microsoft는 이러한 라이브러리에 대한 수정 사항을 제공하고 이러한 라이브러리에 대한 보안 개발 수명 주기 실사를 마쳤습니다.
* **호환 가능** Microsoft가 기본 시나리오에서 이러한 라이브러리를 테스트 하 고 hello v2.0 끝점과 작동 하는지 확인 합니다. Microsoft는 이러한 라이브러리에 대한 수정 사항을 제공하지 않으며 이러한 라이브러리의 검토를 완료하지 않았습니다. 문제 및 기능 요청 toohello 방향이 지정 된 라이브러리의 오픈 소스 프로젝트 여야 합니다.

목록이 hello v2.0 끝점을 사용 하는 라이브러리에 대 한 hello이이 문서의 다음 섹션을 참조 하세요.


## <a name="microsoft-supported-client-libraries"></a>Microsoft 지원 클라이언트 라이브러리

> [!IMPORTANT]
> hello MSAL 미리 보기 라이브러리는 프로덕션 환경에서 사용 하기에 적합 합니다. 제공이 현재 프로덕션 라이브러리 (ADAL)를 수행 하는 것 처럼 이러한 라이브러리에 대 한 동일한 프로덕션 수준 지원을 hello 합니다. Hello 미리 보기 기간 동안 변경 내용을 toohello MSAL API를 내부 캐시 형식으로 만듭니다 수 있습니다 하 고 다른 메커니즘을 사용할 수 있는 예 고 없이이 라이브러리의 버그 수정 또는 향상 된 기능이 함께 tootake 필요한 키를 누릅니다. 이러한 변경은 응용 프로그램에 영향을 줄 수 있습니다. 예를 들어, toohello 캐시 형식을 변경 합니다. 요구 하는 등 이러한에 toosign 다시 사용자에 게 영향을 줄 수 있습니다. API 변경 하면 tooupdate 코드가 필요할 수 있습니다. Hello 일반 공급 릴리스는 해야 tooupdate toohello 일반 공급 버전 6 개월 이내에 게 제공 했습니다 미리 보기를 사용 하 여 작성 된 응용 프로그램으로 라이브러리의 버전을 사용할 수 없습니다.

| 플랫폼 | 라이브러리 | 다운로드 | 소스 코드 | 샘플 | 참조
| --- | --- | --- | --- | --- | --- |
| .NET 클라이언트, Windows 스토어, UWP, Xamarin iOS 및 Android | MSAL .NET(미리 보기) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [데스크톱 앱](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js(미리 보기) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [단일 페이지 앱](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS, macOS | MSAL(미리 보기) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS 앱](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL(미리 보기) | [hello 눈에 보는](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android 앱](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Microsoft 지원 서버 미들웨어 라이브러리

| 플랫폼 | 라이브러리 | 다운로드 | 소스 코드 | 샘플 | 참조
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | OWIN OpenID Connect 미들웨어 |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[MVC 앱](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | AzureAD용 OWIN OAuth Bearer 미들웨어 |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | .NET 4.5 JWT 핸들러 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | ASP.NET OpenID Connect 미들웨어 |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[ASP.Net 보안(GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[MVC 앱](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | ASP.NET OAuth Bearer 미들웨어 |[Microsoft.AspNetCore.Authentication.OAuth(NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[ASP.Net 보안(GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | .NET Core JWT 핸들러  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [웹앱](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>호환 가능한 클라이언트 라이브러리
| 플랫폼 | 라이브러리 이름 | 테스트 버전 | 소스 코드 | 샘플 |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[네이티브 앱 샘플](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[네이티브 앱 샘플](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>호환 가능한 서버 미들웨어 라이브러리
| 플랫폼 | 라이브러리 이름 | 테스트 버전 | 소스 코드 | 샘플 |
|:---:|:---:|:---:|:---:|:---:|
| 자바 | [Scribe Java scribejava](https://github.com/scribejava/scribejava) | [버전 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [PHP 리그 oauth2 클라이언트 hello](https://github.com/thephpleague/oauth2-client) | [버전 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python-Flask |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |[웹앱](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>관련 콘텐츠
Azure AD hello v2.0 끝점에 대 한 자세한 내용은 참조 hello [Azure AD 응용 프로그램 모델 v2.0 개요][AAD-App-Model-V2-Overview]합니다.

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
