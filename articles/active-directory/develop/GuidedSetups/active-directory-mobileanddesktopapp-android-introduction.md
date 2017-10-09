---
title: "AD aaaAzure v2 Android 시작-소개 | Microsoft Docs"
description: "Android 앱이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Android 앱에서 hello Microsoft Graph API를 호출 합니다.

이 가이드에서는 네이티브 Android 응용 프로그램이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법에 대해 설명합니다.

이 가이드의 hello 끝 응용 프로그램은 개인 계정 (outlook.com, live.com, 등 포함)를 사용 하 여 보호 된 API 수 toocall 수 뿐만 아니라 작업 및 모든 회사 또는 조직 Azure Active Directory에서 학교 계정.  

### <a name="how-this-sample-works"></a>이 샘플의 작동 원리
![이 샘플의 작동 원리](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

이 가이드에서 만든 hello 샘플 여기서 Android 응용 프로그램은 Azure Active Directory v2 끝점-이 경우 Microsoft Graph API 로부터 토큰을 받는 웹 API를 사용 하는 tooquery 시나리오를 기반으로 합니다. 이 시나리오에 대 한 토큰 tooHTTP 요청 hello 권한 부여 헤더를 통해 추가 됩니다. 토큰 획득 및 갱신. 이후에 hello Microsoft 인증 라이브러리 (MSAL)에 의해 처리 됩니다.

### <a name="pre-requisites"></a>필수 조건
* 이 안내식 설정은 Android Studio를 중심으로 설명하지만 다른 Android 응용 프로그램 개발 환경에도 적용됩니다. 
* Android SDK 21 이상이 필요합니다(SDK 25 권장).
* Android용 MSAL(Microsoft 인증 라이브러리)의 이 릴리스에는 Google Chrome 또는 사용자 지정 탭을 사용하는 웹 브라우저가 필요합니다.

> 참고: Google Chrome은 Visual Studio Emulator for Android에 포함되어 있지 않습니다. Tootest 권장가 Google chrome 설치 API 25 또는 이미지와 에뮬레이터 API 21 이상 버전에서이 코드입니다.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>어떻게 toohandle 토큰 획득 tooaccess 보호 된 웹 API

Hello 사용자 인증 후, hello 샘플 응용 프로그램 Microsoft Graph API 또는 Microsoft Azure Active Directory v 2를 통해 보안이 유지 되는 웹 API를 사용 하는 tooquery 일 수 있는 토큰을 받습니다.

Api는 Microsoft Graph 필요한 tooread 예를 들어 특정 리소스에 액세스 하는 액세스 토큰 tooallow 사용자의 프로필을와 같은 사용자의 일정을 액세스 하거나 전자 메일을 보냅니다. 응용 프로그램 API 범위를 지정 하 여 액세스 토큰 MSAL tooaccess를 사용 하 여 이러한 리소스를 요청할 수 있습니다. 이 액세스 토큰에 있으면 보호 된 리소스를 추가 된 toohello hello에 대 한 모든 호출에 대 한 HTTP 인증 헤더. 

MSAL은 사용자를 대신해 액세스 토큰 캐싱 및 새로 고침을 관리하므로 응용 프로그램에서 이러한 작업을 수행할 필요가 없습니다.

### <a name="libraries"></a>라이브러리

이 가이드에서는 다음 라이브러리 hello 사용:

|라이브러리|설명|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|MSAL(Microsoft 인증 라이브러리)|
