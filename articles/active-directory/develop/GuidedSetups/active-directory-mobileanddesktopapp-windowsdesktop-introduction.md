---
title: "AD aaaAzure v2 Windows 데스크톱 시작-소개 | Microsoft Docs"
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="aa989-103">Windows 바탕 화면 앱에서 hello Microsoft Graph API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="aa989-104">이 가이드에서는 네이티브 Windows Desktop .NET(XAML) 응용 프로그램이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="aa989-105">이 가이드의 hello 끝 응용 프로그램은 개인 계정 (outlook.com, live.com, 등 포함)를 사용 하 여 보호 된 API 수 toocall 수 뿐만 아니라 작업 및 모든 회사 또는 조직 Azure Active Directory에서 학교 계정.</span><span class="sxs-lookup"><span data-stu-id="aa989-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="aa989-106">이 가이드에는 Visual Studio 2015 업데이트 3 또는 Visual Studio 2017이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="aa989-107">이 프로그램이 아직 설치되어 있지 않나요?</span><span class="sxs-lookup"><span data-stu-id="aa989-107">Don’t have it?</span></span> [<span data-ttu-id="aa989-108">Visual Studio 2017 무료 다운로드</span><span class="sxs-lookup"><span data-stu-id="aa989-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="aa989-109">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="aa989-109">How this guide works</span></span>

![이 가이드의 작동 방식](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="aa989-111">이 가이드에서 만든 hello 예제 응용 프로그램에는 Windows 데스크톱 응용 프로그램 tooquery Microsoft Graph API 또는 Azure Active Directory v2 끝점에서 토큰을 수락 하는 웹 API 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="aa989-112">이 시나리오에 대 한 토큰 tooHTTP 요청 hello 권한 부여 헤더를 통해 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="aa989-113">토큰 획득 및 갱신. 이후에 hello Microsoft 인증 라이브러리 (MSAL)에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="aa989-114">보호되는 Web API에 액세스하기 위한 토큰 획득 처리</span><span class="sxs-lookup"><span data-stu-id="aa989-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="aa989-115">Hello 사용자 인증 후, hello 샘플 응용 프로그램 Microsoft Graph API 또는 Microsoft Azure Active Directory v 2를 통해 보안이 유지 되는 웹 API를 사용 하는 tooquery 일 수 있는 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="aa989-116">Api는 Microsoft Graph 필요한 tooread 예를 들어 특정 리소스에 액세스 하는 액세스 토큰 tooallow 사용자의 프로필을와 같은 사용자의 일정을 액세스 하거나 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="aa989-117">응용 프로그램 API 범위를 지정 하 여 액세스 토큰 MSAL tooaccess를 사용 하 여 이러한 리소스를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="aa989-118">이 액세스 토큰에 있으면 보호 된 리소스를 추가 된 toohello hello에 대 한 모든 호출에 대 한 HTTP 인증 헤더.</span><span class="sxs-lookup"><span data-stu-id="aa989-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="aa989-119">MSAL은 사용자를 대신해 액세스 토큰 캐싱 및 새로 고침을 관리하므로 응용 프로그램에서 이러한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa989-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="aa989-120">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="aa989-120">NuGet Packages</span></span>

<span data-ttu-id="aa989-121">이 가이드에서는 다음 NuGet 패키지 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="aa989-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="aa989-122">라이브러리</span><span class="sxs-lookup"><span data-stu-id="aa989-122">Library</span></span>|<span data-ttu-id="aa989-123">설명</span><span class="sxs-lookup"><span data-stu-id="aa989-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="aa989-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="aa989-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="aa989-125">MSAL(Microsoft 인증 라이브러리)</span><span class="sxs-lookup"><span data-stu-id="aa989-125">Microsoft Authentication Library (MSAL)</span></span>|

