---
title: "Active Directory 인증 라이브러리 aaaAzure | Microsoft Docs"
description: "사용 하면 클라이언트 응용 프로그램 개발자가 Azure AD 인증 라이브러리 (ADAL) hello tooeasily 사용자 toocloud 인증 또는 온-프레미스 AD (Active Directory)와 후 보안 API 호출용 액세스 토큰을 가져올 합니다."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Azure Active Directory 인증 라이브러리
hello Azure Active Directory 인증 라이브러리 (ADAL) 사용 하면 클라이언트 응용 프로그램 개발자가 tooeasily 인증 사용자 toocloud 또는 온-프레미스 Active Directory (AD) 하 고 보안 API 호출용 액세스 토큰을 가져옵니다. ADAL은 개발자가 다음과 같은 기능을 통해 더 쉽게 인증하도록 합니다.
 - 비동기 메서드 호출에 대한 지원
 - 액세스 토큰 및 새로 고침 토큰을 저장하는 구성 가능한 토큰 캐시
 - 액세스 토큰이 만료되고 새로 고침 토큰을 사용할 수 있을 때 자동 토큰 새로 고침
 - 등
 
대부분의 hello 복잡성을 처리 하 여 ADAL 비즈니스 논리에 집중할 개발자 주며 쉽게 보안에서 전문가가 아니더라도 리소스를 보호 합니다.

ADAL은 다양한 플랫폼에서 사용할 수 있습니다.

### <a name="client-libraries"></a>클라이언트 라이브러리

| 플랫폼 | 라이브러리 | 다운로드 | 소스 코드 | 샘플 | 참조
| --- | --- | --- | --- | --- | --- |
| .NET 클라이언트, Windows 스토어, UWP, Xamarin iOS 및 Android |.NET용 MSAL(미리 보기) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [데스크톱 앱](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[참조](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |JavaScript용 MSAL(미리 보기) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [단일 페이지 앱](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [참조](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |iOS용 MSAL(미리 보기) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS 앱](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [참조](https://azuread.github.io/docs/objc/) |
| Android |Android용 MSAL(미리 보기) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android 앱](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [참조](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| .NET 클라이언트, Windows 스토어, UWP, Xamarin iOS 및 Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [데스크톱 앱](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[참조](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| .NET 클라이언트, Windows 스토어, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [데스크톱 앱](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[단일 페이지 앱](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[iOS 앱](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [참조](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[hello 눈에 보는](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Android 앱](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Java 웹앱](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| 파이썬 |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>서버 라이브러리 

| 플랫폼 | 라이브러리 | 다운로드 | 소스 코드 | 샘플 | 참조
| --- | --- | --- | --- | --- | --- |
| .NET |AzureAD용 OWIN|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[MVC 앱](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OpenIDConnect용 OWIN |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[웹앱](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [앱 API](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |WS-Federation용 OWIN |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[MVC 웹앱](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |.NET 4.5용 ID 프로토콜 확장 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |.NET 4.5 JWT 핸들러 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>시나리오

ADAL을 원격 리소스에 액세스하는 클라이언트 인증에 사용할 수 있는 3가지 공통 시나리오는 다음과 같습니다.  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>장치에서 실행되는 네이티브 클라이언트 응용 프로그램의 사용자 인증 

이 시나리오에서 개발자는 WPF 클라이언트 응용 프로그램, tooaccess web API와 같이 Azure AD를 통해 보호 되는 원격 리소스를 필요로 하에 있습니다. 그는 Azure 구독, tooinvoke 다운스트림 web API를 hello 하는 방법을 알고 있으며 Azure hello 알고 AD 테 넌 트 web API 사용 하 여 hello입니다. 결과적으로, hello 인증 경험 tooADAL 완전히 위임 하거나 명시적으로 사용자 자격 증명을 처리 하 여 Azure AD와 toofacilitate ADAL 인증을 사용할 수 없었습니다. ADAL 쉽게 tooauthenticate hello 사용자를 사용 하면 하 고 Azure AD에서 액세스 토큰 및 새로 고침 토큰을 얻은 다음 hello 액세스 토큰 toomake 요청 toohello 웹 API를 사용 합니다.

인증 tooAzure AD를 사용 하 여이 시나리오를 보여 주는 코드 샘플을 보려면 [네이티브 클라이언트 WPF 응용 프로그램 tooWeb API](https://github.com/azureadsamples/nativeclient-dotnet)합니다.

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>웹 서버에서 실행되는 비밀 클라이언트 응용 프로그램 인증

이 시나리오에서 개발자는 web API와 같이 Azure AD를 통해 보호 되는 원격 리소스 tooaccess 해야 하는 서버에서 실행 중인 응용 프로그램에 있습니다. 그는 Azure를 구독, tooinvoke 다운스트림 서비스 hello 하는 방법을 알고 고 알고 hello Azure AD 테 넌 트 hello 웹 API를 사용 합니다. 결과적으로, hello 응용 프로그램의 자격 증명을 명시적으로 처리 하 여 Azure AD와 toofacilitate ADAL 인증을 사용할 수 없었습니다. ADAL에서는 Azure AD의 토큰을 쉽게 tooretrieve hello 응용 프로그램의 클라이언트 자격 증명을 사용 하 여 하 고 해당 토큰 toomake 요청 toohello web API를 사용 합니다. ADAL도 hello의 hello 수명을 관리 하는 핸들 액세스 토큰 캐시 하 고 필요에 따라 갱신 하 여입니다. 이 시나리오를 보여 주는 코드 샘플을 보려면 [데몬 콘솔 응용 프로그램 tooWeb API](https://github.com/AzureADSamples/Daemon-DotNet)합니다.

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>사용자를 대신하여 서버에서 실행되는 비밀 클라이언트 응용 프로그램 인증 

이 시나리오에서 개발자는 web API와 같이 Azure AD를 통해 보호 되는 원격 리소스 tooaccess 해야 하는 서버에서 실행 중인 응용 프로그램에 있습니다. hello 요청은 Azure AD 사용자 대신 만든 toobe도 필요 합니다. 그는 Azure를 구독, tooinvoke 다운스트림 web API를 hello 하는 방법을 알고 고 알고 hello Azure AD 테 넌 트 hello 서비스를 사용 합니다. Hello 사용자가 인증 된 toohello 웹 응용 프로그램에 모두 되 면 hello 응용 프로그램 Azure AD에서 hello 사용자에 대 한 권한 부여 코드를 가져올 수 있습니다. hello 웹 응용 프로그램 액세스 토큰 및 새로 고침 토큰 hello 권한 부여 코드와 클라이언트 자격 증명에 연결 된 Azure AD에서 hello 응용 프로그램을 사용 하 여 사용자를 대신 하 여 ADAL tooobtain를 유도할 수 있습니다. Hello 웹 응용 프로그램 hello 액세스 토큰을 소유한 되 면 hello 토큰 만료 될 때까지 hello 웹 API를 호출할 수 있습니다. Hello 토큰이 만료 되 면 hello 웹 응용 프로그램 ADAL tooget 새 액세스 토큰을 사용 하 여 이전에 받은 hello 새로 고침 토큰을 사용 하 여 수 있습니다. 이 시나리오를 보여 주는 코드 샘플을 보려면 [Native client API tooWeb tooWeb API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)합니다.

## <a name="see-also"></a>참고 항목

- [hello Azure Active Directory 개발자 가이드](active-directory-developers-guide.md)
- [Azure Active directory 인증 시나리오](active-directory-authentication-scenarios.md)
- [Azure Active Directory 코드 샘플](active-directory-code-samples.md)
