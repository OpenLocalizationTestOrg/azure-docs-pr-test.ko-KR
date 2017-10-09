---
title: "AD aaaAzure v2 JS SPA 단계별 설치-소개 | Microsoft Docs"
description: "JavaScript SPA 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>JavaScript 단일 페이지 응용 프로그램 (SPA) hello Microsoft Graph API를 호출 합니다.

이 가이드에서는 개인, 작업에는 JavaScript 단일 페이지 응용 프로그램 (SPA) 수 로그인 하는 방법을 보여 줍니다. 및 학교 계정 액세스 토큰을 가져오고 hello Microsoft Graph API를 호출 또는 기타 Api 액세스 토큰에서 필요로 하는 환영 Azure Active Directory v2 끝점입니다.

### <a name="how-this-guide-works"></a>이 가이드의 작동 방식

![이 가이드에 의해 생성 된 hello 샘플 응용 프로그램의 작동 원리](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>추가 정보

이 가이드에서 만든 hello 예제 응용 프로그램에는 JavaScript SPA tooquery hello Microsoft Graph API 또는 Azure Active Directory v2 끝점에서 토큰을 수락 하는 웹 API 수 있습니다. 이 시나리오에 대 한의 액세스 토큰은 이후 로그인, 사용자 hello 권한 부여 헤더를 통해 요청 및 추가 된 tooHTTP 요청입니다. 토큰 획득 및 갱신. 이후에 hello Microsoft 인증 라이브러리 (MSAL)에서 처리 됩니다.

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>라이브러리

이 가이드에서는 다음 라이브러리 hello 사용:

|라이브러리|설명|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|JavaScript용 Microsoft 인증 라이브러리 미리 보기|

> [!NOTE]
> *msal.js* 대상 hello *Azure Active Directory v2 끝점* -에 toosign 개인, 학교 및 회사 계정을 사용 하도록 설정 하 고 토큰을 획득 합니다. hello *Azure Active Directory v2 끝점* 가 [몇 가지 제한 사항이](..\active-directory-v2-limitations.md)합니다. 회사 및 학교 계정에만 관심이 있으면 사용 하 여 *adal.js* 및 hello *V1 끝점*합니다. hello v1 및 v2 끝점 간의 toounderstand 차이점 읽을 hello [v1 v2 비교](..\active-directory-v2-compare.md)합니다.

<!--end-collapse-->
