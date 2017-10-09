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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="933c8-103">Microsoft tooan ASP.NET 웹 응용 프로그램을 사용 하 여 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="933c8-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="933c8-104">이 가이드에서는 방법을 tooimplement으로 로그인 하는 ASP.NET MVC 솔루션을 사용 하 여 OpenID Connect를 사용 하 여 기존 웹 브라우저 기반 응용 프로그램과 Microsoft 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="933c8-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="933c8-105">이 가이드의 hello 끝 응용 프로그램 수 tooaccept 기호 개인의 기능 (outlook.com, live.com, 등 포함) 계정으로 사용 되며 학교 계정을 모든 회사 또는 조직 Azure Active Directory와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="933c8-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="933c8-106">이 가이드에는 Visual Studio 2015 업데이트 3 또는 Visual Studio 2017이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="933c8-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="933c8-107">이 프로그램이 아직 설치되어 있지 않나요?</span><span class="sxs-lookup"><span data-stu-id="933c8-107">Don’t have it?</span></span>  [<span data-ttu-id="933c8-108">Visual Studio 2017 무료 다운로드</span><span class="sxs-lookup"><span data-stu-id="933c8-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="933c8-109">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="933c8-109">How this guide works</span></span>

![이 가이드의 작동 방식](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="933c8-111">이 가이드는 로그인 단추를 통해 사용자 tooauthenticate 요청 hello 시나리오 ASP.NET 웹 사이트를 사용 하는 브라우저에서 액세스 하는 위치 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="933c8-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="933c8-112">이 시나리오에서 대부분 hello 작업 toorender hello 웹 페이지의 hello 서버 쪽에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="933c8-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="933c8-113">라이브러리</span><span class="sxs-lookup"><span data-stu-id="933c8-113">Libraries</span></span>

<span data-ttu-id="933c8-114">이 가이드에서는 다음 라이브러리 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="933c8-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="933c8-115">라이브러리</span><span class="sxs-lookup"><span data-stu-id="933c8-115">Library</span></span>|<span data-ttu-id="933c8-116">설명</span><span class="sxs-lookup"><span data-stu-id="933c8-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="933c8-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="933c8-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="933c8-118">인증에 대 한 응용 프로그램 toouse OpenIdConnect 수 있도록 하는 미들웨어</span><span class="sxs-lookup"><span data-stu-id="933c8-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="933c8-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="933c8-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="933c8-120">응용 프로그램 toomaintain 사용자 세션 쿠키를 사용할 수 있도록 하는 미들웨어</span><span class="sxs-lookup"><span data-stu-id="933c8-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="933c8-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="933c8-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="933c8-122">OWIN 기반 응용 프로그램 toorun hello ASP.NET 요청 파이프라인을 사용 하 여 IIS에서 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="933c8-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

