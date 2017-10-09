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
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="c82b0-103">JavaScript 단일 페이지 응용 프로그램 (SPA) hello Microsoft Graph API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="c82b0-104">이 가이드에서는 개인, 작업에는 JavaScript 단일 페이지 응용 프로그램 (SPA) 수 로그인 하는 방법을 보여 줍니다. 및 학교 계정 액세스 토큰을 가져오고 hello Microsoft Graph API를 호출 또는 기타 Api 액세스 토큰에서 필요로 하는 환영 Azure Active Directory v2 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="c82b0-105">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="c82b0-105">How this guide works</span></span>

![이 가이드에 의해 생성 된 hello 샘플 응용 프로그램의 작동 원리](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="c82b0-107">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c82b0-107">More Information</span></span>

<span data-ttu-id="c82b0-108">이 가이드에서 만든 hello 예제 응용 프로그램에는 JavaScript SPA tooquery hello Microsoft Graph API 또는 Azure Active Directory v2 끝점에서 토큰을 수락 하는 웹 API 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="c82b0-109">이 시나리오에 대 한의 액세스 토큰은 이후 로그인, 사용자 hello 권한 부여 헤더를 통해 요청 및 추가 된 tooHTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="c82b0-110">토큰 획득 및 갱신. 이후에 hello Microsoft 인증 라이브러리 (MSAL)에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="c82b0-111">라이브러리</span><span class="sxs-lookup"><span data-stu-id="c82b0-111">Libraries</span></span>

<span data-ttu-id="c82b0-112">이 가이드에서는 다음 라이브러리 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="c82b0-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="c82b0-113">라이브러리</span><span class="sxs-lookup"><span data-stu-id="c82b0-113">Library</span></span>|<span data-ttu-id="c82b0-114">설명</span><span class="sxs-lookup"><span data-stu-id="c82b0-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="c82b0-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="c82b0-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="c82b0-116">JavaScript용 Microsoft 인증 라이브러리 미리 보기</span><span class="sxs-lookup"><span data-stu-id="c82b0-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="c82b0-117">*msal.js* 대상 hello *Azure Active Directory v2 끝점* -에 toosign 개인, 학교 및 회사 계정을 사용 하도록 설정 하 고 토큰을 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="c82b0-118">hello *Azure Active Directory v2 끝점* 가 [몇 가지 제한 사항이](..\active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="c82b0-119">회사 및 학교 계정에만 관심이 있으면 사용 하 여 *adal.js* 및 hello *V1 끝점*합니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="c82b0-120">hello v1 및 v2 끝점 간의 toounderstand 차이점 읽을 hello [v1 v2 비교](..\active-directory-v2-compare.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c82b0-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
