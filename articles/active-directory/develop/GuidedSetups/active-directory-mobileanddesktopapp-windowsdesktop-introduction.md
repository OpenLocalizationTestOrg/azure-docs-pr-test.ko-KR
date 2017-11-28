---
title: "Azure AD v2 Windows 데스크톱 시작 - 소개 | Microsoft Docs"
description: "Windows Desktop .NET(XAML) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
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
ms.openlocfilehash: 4a695c00fce4deb02261ba58ec95469746bb1486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="0ac34-103">Windows 데스크톱 앱에서 Microsoft Graph API 호출</span><span class="sxs-lookup"><span data-stu-id="0ac34-103">Call the Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="0ac34-104">이 가이드에서는 네이티브 Windows Desktop .NET(XAML) 응용 프로그램이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="0ac34-105">이 가이드를 모두 살펴보면 응용 프로그램에서 Azure Active Directory를 사용하는 모든 회사 또는 조직의 회사 및 학교 계정뿐만 아니라 개인 계정(outlook.com, live.com 등)을 사용해 보호되는 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="0ac34-106">이 가이드에는 Visual Studio 2015 업데이트 3 또는 Visual Studio 2017이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="0ac34-107">이 프로그램이 아직 설치되어 있지 않나요?</span><span class="sxs-lookup"><span data-stu-id="0ac34-107">Don’t have it?</span></span> [<span data-ttu-id="0ac34-108">Visual Studio 2017 무료 다운로드</span><span class="sxs-lookup"><span data-stu-id="0ac34-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="0ac34-109">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="0ac34-109">How this guide works</span></span>

![이 가이드의 작동 방식](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="0ac34-111">이 가이드에서 만든 샘플 응용 프로그램은 Windows 데스크톱 응용 프로그램이 Azure Active Directory v2 끝점에서 토큰을 수락하는 Microsoft Graph API 또는 Web API를 쿼리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-111">The sample application created by this guide enables a Windows Desktop Application to query Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="0ac34-112">이 시나리오에서는 토큰은 권한 부여 헤더를 통해 HTTP 요청에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-112">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="0ac34-113">토큰 획득 및 갱신은 MSAL(Microsoft 인증 라이브러리)에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-113">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="0ac34-114">보호되는 Web API에 액세스하기 위한 토큰 획득 처리</span><span class="sxs-lookup"><span data-stu-id="0ac34-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="0ac34-115">사용자 인증 후 샘플 응용 프로그램은 Microsoft Azure Active Directory v2로 보호되는 Microsoft Graph API 또는 Web API를 쿼리하는 데 사용할 수 있는 토큰을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-115">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="0ac34-116">예를 들어, 사용자의 프로필을 읽거나, 사용자의 일정에 액세스하거나, 메일을 보내기 위해 특정 리소스에 대한 액세스를 허용하려면 Microsoft Graph과 같은 API에는 액세스 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-116">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="0ac34-117">응용 프로그램에서는 MSAL을 통해 액세스 토큰을 요청하고 API 범위를 지정해 이러한 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-117">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="0ac34-118">그런 다음 액세스 토큰은 보호되는 리소스에 대한 모든 호출에 사용될 수 있도록 HTTP 인증 헤더에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-118">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="0ac34-119">MSAL은 사용자를 대신해 액세스 토큰 캐싱 및 새로 고침을 관리하므로 응용 프로그램에서 이러한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="0ac34-120">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="0ac34-120">NuGet Packages</span></span>

<span data-ttu-id="0ac34-121">이 가이드에서는 다음 NuGet 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac34-121">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="0ac34-122">라이브러리</span><span class="sxs-lookup"><span data-stu-id="0ac34-122">Library</span></span>|<span data-ttu-id="0ac34-123">설명</span><span class="sxs-lookup"><span data-stu-id="0ac34-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="0ac34-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="0ac34-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="0ac34-125">MSAL(Microsoft 인증 라이브러리)</span><span class="sxs-lookup"><span data-stu-id="0ac34-125">Microsoft Authentication Library (MSAL)</span></span>|

