---
title: "AD aaaAzure v2 ASP.NET 웹 서버 시작-소개 | Microsoft Docs"
description: "OpenID Connect 표준을 사용하여 기존 웹 브라우저 기반 응용 프로그램을 사용하는 ASP.NET 솔루션에서 Microsoft 로그인 구현"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Microsoft tooan ASP.NET 웹 응용 프로그램을 사용 하 여 로그인 추가

이 가이드에서는 방법을 tooimplement으로 로그인 하는 ASP.NET MVC 솔루션을 사용 하 여 OpenID Connect를 사용 하 여 기존 웹 브라우저 기반 응용 프로그램과 Microsoft 보여 줍니다. 

이 가이드의 hello 끝 응용 프로그램 수 tooaccept 기호 개인의 기능 (outlook.com, live.com, 등 포함) 계정으로 사용 되며 학교 계정을 모든 회사 또는 조직 Azure Active Directory와 통합 합니다. 

> 이 가이드에는 Visual Studio 2015 업데이트 3 또는 Visual Studio 2017이 필요합니다.  이 프로그램이 아직 설치되어 있지 않나요?  [Visual Studio 2017 무료 다운로드](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>이 가이드의 작동 방식

![이 가이드의 작동 방식](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

이 가이드는 로그인 단추를 통해 사용자 tooauthenticate 요청 hello 시나리오 ASP.NET 웹 사이트를 사용 하는 브라우저에서 액세스 하는 위치 기반으로 합니다. 이 시나리오에서 대부분 hello 작업 toorender hello 웹 페이지의 hello 서버 쪽에서 발생 합니다.

## <a name="libraries"></a>라이브러리

이 가이드에서는 다음 라이브러리 hello 사용:

|라이브러리|설명|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|인증에 대 한 응용 프로그램 toouse OpenIdConnect 수 있도록 하는 미들웨어|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|응용 프로그램 toomaintain 사용자 세션 쿠키를 사용할 수 있도록 하는 미들웨어|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|OWIN 기반 응용 프로그램 toorun hello ASP.NET 요청 파이프라인을 사용 하 여 IIS에서 사용 하도록 설정|

