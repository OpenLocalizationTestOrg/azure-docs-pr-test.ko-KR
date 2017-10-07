---
title: "aaaAzure Active Directory 코드 예제 | Microsoft Docs"
description: "시나리오별로 구성된 Azure Active Directory 코드 샘플의 인덱스입니다."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Azure Active Directory 코드 샘플
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Microsoft Azure Active Directory (Azure AD) tooadd 인증 및 권한 부여 tooyour 웹 응용 프로그램을 사용할 수 있으며 웹 Api. 이 섹션에는 응용 프로그램에서 사용할 수 있는 코드 조각 및 있습니다 toosamples 수행 하는 방법을 보여 주는 연결 합니다. Hello 코드 샘플 페이지에서 자세한 읽기를 찾을 수 있습니다-내게 요구 사항, 설치 및 설정에 대 한 도움말 항목입니다. 및 hello 코드는 주석 처리 된 toohelp hello 임계 영역을 이해 합니다.

toounderstand hello 기본 시나리오에 대 한 각 샘플 유형의 Azure AD에 대 한 인증 시나리오를 참조 하십시오.

GitHub의 tooour 샘플 기여: [Microsoft Azure Active Directory 샘플 및 설명서](https://github.com/Azure-Samples?page=3&query=active-directory)합니다.

## <a name="web-browser-tooweb-application"></a>웹 브라우저 tooWeb 응용 프로그램
이 샘플 toowrite에 지시 하는 웹 응용 프로그램 사용자의 브라우저 toosign hello 하는 방법을 보여 tooAzure AD에서에서 해당 합니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| C#/.NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Azure AD 테 넌 트의 tooauthenticate 사용자 OpenID Connect (ASP.Net OpenID Connect OWIN 미들웨어)를 사용 합니다. |
| C#/.NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |여러 Azure AD 테 넌 트의 tooauthenticate 사용자 OpenID Connect (ASP.Net OpenID Connect OWIN 미들웨어)를 사용 하는 다중 테 넌 트.NET MVC 웹 응용 프로그램입니다. |
| C#/.NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Azure AD 테 넌 트의 Ws-federation (ASP.Net Ws-federation OWIN 미들웨어) tooauthenticate 사용자가 사용 합니다. |

## <a name="single-page-application-spa"></a>SPA(단일 페이지 응용 프로그램)
이 샘플에서는 toowrite 단일 페이지 응용 프로그램 보안 방법을 Azure AD와 보여 줍니다.  

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| JavaScript, C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |ADAL을 사용 하 여 Azure AD 및 JavaScript toosecure AngularJS 기반 단일 페이지 응용 프로그램을 위한 ASP.NET 웹 API 백 엔드로 사용 하 여 구현 합니다. |

## <a name="native-application-tooweb-api"></a>네이티브 응용 프로그램 tooWeb API
이 코드 샘플 toobuild 네이티브 클라이언트 응용 프로그램 웹 Api를 호출 하는 Azure AD에서 보호 되는 방법을 보여 줍니다. [Azure ADAL(AD 인증 라이브러리)](active-directory-authentication-libraries.md) 및 [Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)이 사용됩니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| JavaScript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Apache Cordova toobuild web API를 호출 하 고 인증을 위한 Azure AD를 사용 하는 Apache Cordova 앱에 대 한 hello ADAL 플러그 인을 사용 합니다. |
| C#/.NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Azure AD를 사용하여 보안되는 웹 API를 호출하는 .NET WPF 응용 프로그램입니다. |
| C#/.NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Azure AD를 사용하여 보안되는 웹 API를 호출하는 Windows 스토어 응용 프로그램입니다. |
| C#/.NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Azure AD를 사용하여 보안되는 다중 테넌트 웹 API를 호출하는 Windows 스토어 응용 프로그램입니다. |
| C#/.NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |네이티브 클라이언트 응용 프로그램 웹 API를 호출 하는 hello 원래 사용자 대신 토큰 tooact를 가져오고 다음 사용 하 여 다른 web API 토큰 toocall를 hello 합니다. |
| C#/.NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Azure AD로 보안되는 웹 API를 호출하는 Windows Phone 8.1용 Windows 스토어 응용 프로그램입니다. |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |인증을 위해 Azure AD를 필요로 하는 웹 API를 호출하는 iOS 응용 프로그램입니다. |
| C#/.NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |OWIN 미들웨어를 사용 하는 대신 웹 API에에서 논리 tooprocess JWT 토큰을 포함 하는 네이티브 클라이언트 응용 프로그램입니다. |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |기본 Azure AD toohello 바인딩 Xamarin 인증 라이브러리 (ADAL)에 대 한 hello Android 라이브러리입니다. |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Xamarin 바인딩 toohello 네이티브 Azure AD 인증 라이브러리 (ADAL) iOS에 대 한 합니다. |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |5개의 플랫폼을 대상으로 하며 Azure AD로 보안되는 웹 API를 호출하는 Xamarin 프로젝트입니다. |
| C#/.NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |비대화형 인증을 수행하고 Azure AD로 보안되는 웹 API를 호출하는 네이티브 응용 프로그램입니다. |

## <a name="web-application-tooweb-api"></a>웹 응용 프로그램 tooWeb API
이 코드 샘플을 사용 하는 방법을 보여 줍니다 [Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild 웹 응용 프로그램 웹 Api를 호출 하는 Azure AD로 보호 됩니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| C#/.NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Hello 로그인 한 사용자의 권한으로 web API를 호출 합니다. |
| C#/.NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Hello 응용 프로그램의 사용 권한이 있는 web API를 호출 합니다. |
| C#/.NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |사용한 권한 부여 추가 [Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan 기존 웹 응용 프로그램 웹 API를 호출할 수 있도록 합니다. |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |API 보호를 위해 Azure AD와 통합된 REST API 서비스를 설정합니다. Web API를 사용하여 Node.js 서버를 포함합니다. |
| C#/.NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |다중 테 넌 트 MVC 웹 응용 프로그램에서 Azure AD 테 넌 트 tooauthenticate 사용자 OpenID Connect (ASP.Net OpenID Connect OWIN 미들웨어)를 사용 하 여입니다. 권한 부여 코드 tooinvoke hello Graph API를 사용합니다. |

## <a name="server-or-daemon-application-tooweb-api"></a>서버 또는 데몬 응용 프로그램 tooWeb API
이 코드 샘플 toobuild는 디먼 또는 서버 응용 프로그램을 가져오는 방법을 리소스 web API에서에서 사용 하 여 보여 [Azure AD 인증 라이브러리 (ADAL)](active-directory-authentication-libraries.md) 및 [Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| C#/.NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |웹 API를 호출하는 콘솔 응용 프로그램입니다. hello 클라이언트 자격 증명에는 암호입니다. |
| C#/.NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |웹 API를 호출하는 콘솔 응용 프로그램입니다. hello 클라이언트 자격 증명에는 인증서입니다. |

## <a name="calling-azure-ad-graph-api"></a>Azure AD Graph API 호출
이 코드 샘플 toobuild 응용 프로그램 호출 하는 Azure AD Graph API tooread 디렉터리 데이터 및 쓰기 hello 하는 방법을 보여 줍니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Graph API tooaccess hello Azure AD 디렉터리 데이터를 사용 하는 웹 응용 프로그램입니다. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Graph API tooaccess hello Azure AD 디렉터리 데이터를 사용 하는 웹 응용 프로그램입니다. |
| C#/.NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Graph API tooaccess hello Azure AD 디렉터리 데이터를 사용 하는 웹 응용 프로그램입니다. |
| C#/.NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |이 콘솔 응용 프로그램 일반적인 읽기 및 쓰기 호출 toohello Graph API를 보여 줍니다. 및 tooexecute 사용자 라이선스 할당 하 고 사용자의 축소판 사진 및 링크를 업데이트 하는 방법을 보여줍니다. |
| C#/.NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Hello Graph API tooget 주기에서 hello 차등 쿼리를 사용 하는 콘솔 응용 프로그램 Azure AD 테 넌 트의 toouser 개체를 변경 합니다. |
| C#/.NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |MVC 응용 프로그램에 Graph API 쿼리 toogenerate 간단한 회사 조직도 사용합니다. |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Graph API tooregister hello는 확장 프로그램을 호출 하 고 다음 읽기, 업데이트 및 hello 확장 특성의 값을 삭제 하는 PHP 응용 프로그램입니다. |

## <a name="authorization"></a>권한 부여
샘플 표시 방식을 코드 이러한 toouse Azure AD 권한 부여에 대 한 합니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| C#/.NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Azure AD와 통합된 응용 프로그램에서 Azure Active Directory 그룹 클레임을 사용하여 RBAC(역할 기반 액세스 제어)를 수행합니다. |
| C#/.NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Azure AD와 통합된 응용 프로그램에서 Azure Active Directory 응용 프로그램 역할을 사용하여 RBAC(역할 기반 액세스 제어)를 수행합니다. |

## <a name="legacy-walkthroughs"></a>레거시 연습
다음 연습에서는 다소 오래된 기술을 사용하지만 여전히 유용할 수 있습니다.

| 언어/플랫폼 | 샘플 | 설명 |
| --- | --- | --- |
| C#/.NET |[Microsoft Azure AD 응용 프로그램의 역할 기반 및 ACL 기반 권한 부여](http://go.microsoft.com/fwlink/?LinkId=331694) |Azure AD와 통합된 응용 프로그램에서 RBAC(역할 기반 액세스 제어) 및 ACL 기반 권한 부여를 수행합니다. |
| C#/.NET |[AAL-Windows 스토어 앱 tooREST 서비스-인증](http://go.microsoft.com/fwlink/?LinkId=330605) |사용 하 여 [Azure AD 인증 라이브러리 (ADAL)](active-directory-authentication-libraries.md) (이전의 AAL) Windows 스토어 베타 tooadd 사용자 인증 기능 tooa Windows 스토어 앱에 대 한 합니다. |
| C#/.NET |[ADAL-네이티브 앱 tooREST 서비스-브라우저 대화 상자를 통해 AAD 인증](http://go.microsoft.com/fwlink/?LinkId=259814) |사용 하 여 [Azure AD 인증 라이브러리 (ADAL)](active-directory-authentication-libraries.md) tooadd 사용자 인증 기능 tooa WPF 클라이언트입니다. |
| C#/.NET |[ADAL-네이티브 앱 tooREST 서비스-브라우저 대화 상자를 통해 ACS 인증](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |사용 하 여 [Azure AD 인증 라이브러리 (ADAL)](active-directory-authentication-libraries.md) 및 [서비스 2.0 ACS (액세스 제어)](http://msdn.microsoft.com/library/azure/hh147631.aspx) tooadd 사용자 인증 기능 tooa WPF 클라이언트입니다. |
| C#/.NET |[ADAL-서버 tooServer 인증](http://go.microsoft.com/fwlink/?LinkId=259816) |사용 하 여 [Azure AD 인증 라이브러리 (ADAL)](active-directory-authentication-libraries.md) 서버 쪽 프로세스 tooan MVC4 Web API REST 서비스에서에서 toosecure 서비스를 호출 합니다. |
| C#/.NET |[추가 로그온 tooYour 웹 응용 프로그램 사용 하 여 Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |.NET 응용 프로그램 tooperform 웹 single sign on Azure AD 엔터프라이즈 디렉터리에 대해 구성 합니다. |
| C#/.NET |[Azure AD를 사용하여 다중 테넌트 웹 응용 프로그램 개발](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |여러 조직에서 Azure AD tooadd toohello single sign on 및 하나의.NET 응용 프로그램 toowork의 디렉터리 액세스 기능을 사용 합니다. |
| Java |[Azure AD Graph API용 Java 샘플 앱](http://go.microsoft.com/fwlink/?LinkId=263969) |Azure AD의 hello tooaccess 디렉터리 데이터를 Graph API를 사용 합니다. |
| PHP |[Azure AD Graph API용 PHP 샘플 앱](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Azure AD의 hello tooaccess 디렉터리 데이터를 Graph API를 사용 합니다. |
| C#/.NET |[Azure AD Graph API용 샘플 앱](http://go.microsoft.com/fwlink/?LinkID=262648) |Azure AD의 hello tooaccess 디렉터리 데이터를 Graph API를 사용 합니다. |
| C#/.NET |[Azure AD Graph 차등 쿼리용 샘플 앱](http://go.microsoft.com/fwlink/?LinkId=275398) |Azure AD 테 넌 트에 있는 hello Graph API tooget 정기적인 변경 내용 toouser 개체에 hello 차등 쿼리를 사용 합니다. |
| C#/.NET |[Azure AD에 대해 다중 테넌트 클라우드 응용 프로그램을 통합하는 샘플 앱](http://go.microsoft.com/fwlink/?LinkId=275397) |다중 테넌트 응용 프로그램을 Azure AD에 통합합니다. |
| C#/.NET |[Azure AD를 사용하여 Windows 스토어 응용 프로그램 및 REST 웹 서비스 보안](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |간단한 web API 리소스 및 Azure AD를 사용 하 여 Windows 스토어 클라이언트 응용 프로그램을 만들고 hello [Azure AD 인증 라이브러리 (ADAL)](active-directory-authentication-libraries.md)합니다. |
| C#/.NET |[Graph API tooQuery hello Azure AD를 사용 하 여](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Microsoft.NET 응용 프로그램 toouse hello Azure AD 테 넌 트 디렉터리에서 Azure AD Graph API tooaccess 데이터를 구성 합니다. |

## <a name="see-also"></a>참고 항목
##### <a name="other-resources"></a>기타 리소스
[Azure Active Directory 개발자 가이드](active-directory-developers-guide.md)

[Azure AD Graph API 개념 및 참조](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Azure AD Graph API 도우미 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
