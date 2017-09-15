---
title: "Azure AD v2 ASP.NET 웹 서버 시작 - 소개 | Microsoft Docs"
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
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="6dc53-103">ASP.NET 웹앱에 Microsoft에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="6dc53-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="6dc53-104">이 가이드에서는 OpenID Connect를 사용하는 브라우저 기반 응용 프로그램에서 ASP.NET MVC 솔루션을 사용하여 Microsoft에 로그인을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="6dc53-105">이 가이드를 모두 살펴보면 응용 프로그램에서 Azure Active Directory와 통합된 모든 회사 또는 조직의 회사 및 학교 계정뿐만 아니라 개인 계정(outlook.com, live.com 등)의 로그인을 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="6dc53-106">이 가이드에는 Visual Studio 2015 업데이트 3 또는 Visual Studio 2017이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="6dc53-107">이 프로그램이 아직 설치되어 있지 않나요?</span><span class="sxs-lookup"><span data-stu-id="6dc53-107">Don’t have it?</span></span>  [<span data-ttu-id="6dc53-108">Visual Studio 2017 무료 다운로드</span><span class="sxs-lookup"><span data-stu-id="6dc53-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="6dc53-109">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="6dc53-109">How this guide works</span></span>

![이 가이드의 작동 방식](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="6dc53-111">이 가이드는 브라우저가 ASP.NET 웹 사이트에 액세스하여 사용자에게 로그인 단추를 통해 인증하도록 요청하는 시나리오를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="6dc53-112">이 시나리오에서는 웹 페이지를 렌더링하는 작업의 대부분이 서버 쪽에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="6dc53-113">라이브러리</span><span class="sxs-lookup"><span data-stu-id="6dc53-113">Libraries</span></span>

<span data-ttu-id="6dc53-114">이 가이드에서는 다음 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="6dc53-115">라이브러리</span><span class="sxs-lookup"><span data-stu-id="6dc53-115">Library</span></span>|<span data-ttu-id="6dc53-116">설명</span><span class="sxs-lookup"><span data-stu-id="6dc53-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="6dc53-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="6dc53-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="6dc53-118">응용 프로그램이 인증에 OpenIdConnect를 사용할 수 있게 해주는 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc53-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="6dc53-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="6dc53-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="6dc53-120">응용 프로그램이 쿠키를 사용하여 사용자 세션을 유지하도록 하는 미들웨어</span><span class="sxs-lookup"><span data-stu-id="6dc53-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="6dc53-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="6dc53-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="6dc53-122">OWIN 기반 응용 프로그램이 ASP.NET 요청 파이프라인을 사용하여 IIS에서 실행되도록 함</span><span class="sxs-lookup"><span data-stu-id="6dc53-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

