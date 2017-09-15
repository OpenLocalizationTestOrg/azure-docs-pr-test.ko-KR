---
title: "Azure AD v2 JS SPA 단계별 설치 - 소개 | Microsoft Docs"
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
ms.openlocfilehash: 3d195d0d67f8f82c9450ffd93767917698addee3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="85ec3-103">JavaScript SPA(단일 페이지 응용 프로그램)에서 Microsoft Graph API 호출</span><span class="sxs-lookup"><span data-stu-id="85ec3-103">Call the Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="85ec3-104">이 가이드에서는 JavaScript SPA(단일 페이지 응용 프로그램)가 개인, 회사 및 학교 계정으로 로그인하고, 액세스 토큰을 얻고, Microsoft Graph API 또는 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 기타 API를 호출할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="85ec3-105">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="85ec3-105">How this guide works</span></span>

![이 가이드에서 생성된 샘플 앱의 작동 원리](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="85ec3-107">추가 정보</span><span class="sxs-lookup"><span data-stu-id="85ec3-107">More Information</span></span>

<span data-ttu-id="85ec3-108">이 가이드에서 만든 샘플 응용 프로그램은 JavaScript SPA가 Azure Active Directory v2 끝점에서 토큰을 수락하는 Microsoft Graph API 또는 Web API를 쿼리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-108">The sample application created by this guide enables a JavaScript SPA to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="85ec3-109">이 시나리오에서는 사용자가 로그인한 후에 액세스 토큰이 요청되고 권한 부여 헤더를 통해 HTTP 요청에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-109">For this scenario, after a user signs-in, an access token is requested and added to HTTP requests via the authorization header.</span></span> <span data-ttu-id="85ec3-110">토큰 획득 및 갱신은 MSAL(Microsoft 인증 라이브러리)에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-110">Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="85ec3-111">라이브러리</span><span class="sxs-lookup"><span data-stu-id="85ec3-111">Libraries</span></span>

<span data-ttu-id="85ec3-112">이 가이드에서는 다음 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-112">This guide uses the following library:</span></span>

|<span data-ttu-id="85ec3-113">라이브러리</span><span class="sxs-lookup"><span data-stu-id="85ec3-113">Library</span></span>|<span data-ttu-id="85ec3-114">설명</span><span class="sxs-lookup"><span data-stu-id="85ec3-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="85ec3-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="85ec3-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="85ec3-116">JavaScript용 Microsoft 인증 라이브러리 미리 보기</span><span class="sxs-lookup"><span data-stu-id="85ec3-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="85ec3-117">*msal.js*는 *Azure Active Directory v2 끝점*을 대상으로 하며 이를 통해 개인, 학교 및 회사 계정으로 로그인하여 토큰을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-117">*msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens.</span></span> <span data-ttu-id="85ec3-118">*Azure Active Directory v2 끝점*에는 [몇 가지 제한 사항](..\active-directory-v2-limitations.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-118">The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="85ec3-119">학교 및 회사 계정에만 관심이 있는 경우 *adal.js* 및 *V1 끝점*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85ec3-119">If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*.</span></span> <span data-ttu-id="85ec3-120">v1 및 v2 끝점 간의 차이점을 이해하려면 [v1-v2 비교](..\active-directory-v2-compare.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="85ec3-120">To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
