---
title: "AD aaaAzure v2 iOS 시작-소개 | Microsoft Docs"
description: "iOS(Swift) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="7b9ac-103">IOS 앱에서 hello Microsoft Graph API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="7b9ac-104">이 가이드는 방법을 보여 주는 기본 iOS 응용 프로그램 (Swift) 수 액세스 토큰 가져오기 hello Microsoft Graph API 또는 Azure Active Directory v2 끝점에서 액세스 토큰을 필요로 하는 다른 Api를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="7b9ac-105">이 가이드의 hello 끝 응용 프로그램은 개인 계정 (outlook.com, live.com, 등 포함)를 사용 하 여 보호 된 API 수 toocall 수 뿐만 아니라 작업 및 모든 회사 또는 조직 Azure Active Directory에서 학교 계정.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="7b9ac-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7b9ac-106">Pre-requisites</span></span>
> - <span data-ttu-id="7b9ac-107">이 가이드에는 XCode 8.x가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="7b9ac-108">[여기에서](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode 다운로드 URL") XCode를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="7b9ac-109">패키지 관리를 위한 [Carthage](https://github.com/Carthage/Carthage)</span><span class="sxs-lookup"><span data-stu-id="7b9ac-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="7b9ac-110">이 가이드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="7b9ac-110">How this guide works</span></span>

![이 가이드의 작동 방식](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="7b9ac-112">이 가이드에서 만든 hello 예제 응용 프로그램에는 iOS 응용 프로그램 tooquery hello Microsoft Graph API 또는 Azure Active Directory v2 끝점에서 토큰을 수락 하는 웹 API 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="7b9ac-113">이 시나리오에 대 한 토큰 tooHTTP 요청 hello 권한 부여 헤더를 통해 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="7b9ac-114">토큰 획득 및 갱신. 이후에 hello Microsoft 인증 라이브러리 (MSAL)에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="7b9ac-115">보호되는 Web API에 액세스하기 위한 토큰 획득 처리</span><span class="sxs-lookup"><span data-stu-id="7b9ac-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="7b9ac-116">Hello 사용자 인증 후, hello 샘플 응용 프로그램 사용된 tooquery hello Microsoft Graph API 또는 웹 API v2 Microsoft Azure Active Directory로 보호 될 수 있는 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="7b9ac-117">Api는 Microsoft Graph 필요한 tooread 예를 들어 특정 리소스에 액세스 하는 액세스 토큰 tooallow 사용자의 프로필을와 같은 사용자의 일정을 액세스 하거나 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="7b9ac-118">응용 프로그램에서는 API 범위를 지정하여 MSAL을 통해 액세스 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="7b9ac-119">이 액세스 토큰에 있으면 보호 된 리소스를 추가 된 toohello hello에 대 한 모든 호출에 대 한 HTTP 인증 헤더.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="7b9ac-120">MSAL은 사용자를 대신해 액세스 토큰 캐싱 및 새로 고침을 관리하므로 응용 프로그램에서 이러한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b9ac-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="7b9ac-121">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="7b9ac-121">NuGet packages</span></span>

<span data-ttu-id="7b9ac-122">이 가이드에서는 다음 NuGet 패키지 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="7b9ac-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="7b9ac-123">라이브러리</span><span class="sxs-lookup"><span data-stu-id="7b9ac-123">Library</span></span>|<span data-ttu-id="7b9ac-124">설명</span><span class="sxs-lookup"><span data-stu-id="7b9ac-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="7b9ac-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="7b9ac-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="7b9ac-126">iOS용 Microsoft 인증 라이브러리 미리 보기</span><span class="sxs-lookup"><span data-stu-id="7b9ac-126">Microsoft Authentication Library Preview for iOS</span></span>|

