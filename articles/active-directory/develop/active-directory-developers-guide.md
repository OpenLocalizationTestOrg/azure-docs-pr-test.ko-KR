---
title: "개발자를 위한 Active Directory aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory를 사용하여 Microsoft 회사 및 학교 계정에 로그인하는 방법의 개요를 제공합니다."
services: active-directory
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4dbbea6c1e0b8a70c0c36ddd1caec5658130a003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-for-developers"></a>개발자용 Azure Active Directory
Azure Active Directory는 개발자가 toosecurely 로그인 Microsoft에서 지 원하는 회사 또는 학교 계정 가진 모든 사용자 허용 하는 클라우드 id 서비스입니다.  여기에 hello 설명서 tooadd Azure AD에서 OAuth 및 OpenID Connect 업계 표준 인증 프로토콜을 사용 하 여 tooyour 응용 프로그램을 지원 하는 방법을 보여 줍니다.

| | |
| --- | --- |
|[인증 기본 사항](active-directory-authentication-scenarios.md) | Azure AD에는 소개 tooauthentication |
|[응용 프로그램 유형](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Azure AD에서 지 원하는 hello 인증 시나리오의 개요 |                                
                                                                              
## <a name="get-started"></a>시작
이러한 단계별된 설치 우리의 인증 라이브러리 toosign를 사용 하 여 Azure Active Directory 사용자에서를 진행 합니다.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![모바일 및 데스크톱 앱](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />모바일 및 데스크톱 앱</center> | [개요](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET](active-directory-devquickstarts-dotnet.md)<br /><br />[Windows](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md)<br /><br />[OAuth 2.0](active-directory-protocols-oauth-code.md) |
| <center>![Web Apps](./media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [개요](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [NodeJS](active-directory-devquickstarts-openidconnect-nodejs.md)<br /><br />[OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) |  |
| <center>![단일 페이지 앱](./media/active-directory-developers-guide/SPA.png)<br />단일 페이지 앱</center> | [개요](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![Web API](./media/active-directory-developers-guide/Web_API.png)<br />Web API</center> | [개요](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[NodeJS](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![서비스 간](./media/active-directory-developers-guide/Service_App.png)<br />서비스 간</center> | [개요](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#server-or-daemon-application-to-web-api)<br /><br />[OAuth 2.0 클라이언트 자격 증명](active-directory-protocols-oauth-service-to-service.md) |  |

## <a name="guides"></a>가이드
이러한 문서는 Azure Active Directory와 tooperform 공통 작업 하는 방법을 알려 줍니다.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[앱 등록](active-directory-integrating-applications.md)           | 어떻게 tooregister Azure AD에서 응용 프로그램 |
|[다중 테넌트 앱](active-directory-devhowto-multi-tenant-overview.md)    | 모든 microsoft에서 toosign 계정 작동 하는 방식 |
|[OAuth 및 OpenID Connect](active-directory-protocols-openid-connect-code.md)| Toosign 기능 사용자에 게 및 호출 웹 Api는 최신 인증 프로토콜을 사용 하는 방법 |
|[가이드 더 보기...](active-directory-developers-guide-index.md#guides)        |     |

## <a name="reference"></a>참조
다음 문서는 API, 프로토콜 메시지 및 Azure Active Directory에서 사용되는 용어에 대한 자세한 정보를 제공합니다.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [인증 라이브러리(ADAL)](active-directory-authentication-libraries.md)   | Hello 라이브러리 및 Azure AD에서 제공 하는 Sdk의 개요 |
| [코드 샘플](active-directory-code-samples.md)                                  | 모든 Azure AD 코드 샘플의 목록 |
| [용어](active-directory-dev-glossary.md)                                      | 이 설명서에서 사용하는 용어 및 단어의 정의 |
| [참조 자료 더 보기...](active-directory-developers-guide-index.md#reference)|     |

## <a name="help--support"></a>도움말 및 지원
이들은 hello 최상의 위치 tooget 도움말을 보려면 Azure Active Directory에서 프로젝트를 개발 합니다.

|  |  
|---|
|[Stack Overflow`azure-active-directory` 및 `adal` 태그](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)      |
|[Azure Active Directory에 대한 피드백](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)|
| [Microsoft 개발자 채팅 사용(제한된 시간 동안 무료)](http://aka.ms/devchat) |

<br />

> [!NOTE]
> Toosign에서 Microsoft 개인 계정은 필요한 경우 tooconsider hello를 사용 하 여 [Azure AD v2.0 끝점](active-directory-appmodel-v2-overview.md)합니다.  Azure AD hello v2.0 끝점은 단일 인증 시스템에 개인 Microsoft 계정 및 Microsoft 작업 계정 (Azure AD)에서 hello 통합.
