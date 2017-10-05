---
title: "Azure AD v2 Windows 데스크톱 시작 - 테스트 | Microsoft Docs"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="57585-103">코드 테스트</span><span class="sxs-lookup"><span data-stu-id="57585-103">Test your code</span></span>

<span data-ttu-id="57585-104">응용 프로그램을 테스트하려면 `F5` 키를 눌러 Visual Studio에서 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="57585-105">아래와 같이 주 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57585-105">Your Main Window should appear:</span></span>

![샘플 스크린샷](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="57585-107">테스트할 준비가 되면 *Microsoft Graph API 호출*을 클릭하고 Microsoft Azure Active Directory(조직 계정) 또는 Microsoft 계정(live.com, outlook.com)을 사용해 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="57585-108">처음인 경우 로그인하라는 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57585-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![로그인](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="57585-110">동의</span><span class="sxs-lookup"><span data-stu-id="57585-110">Consent</span></span>
<span data-ttu-id="57585-111">응용 프로그램에 처음으로 로그인하면 아래와 유사한 동의 화면이 표시됩니다. 여기서 명시적으로 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![동의 화면](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="57585-113">예상 결과</span><span class="sxs-lookup"><span data-stu-id="57585-113">Expected results</span></span>
<span data-ttu-id="57585-114">[API 호출 결과] 화면에 Microsoft Graph API 호출에서 반환된 사용자 프로필 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57585-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="57585-115">[토큰 정보] 상자에 `AcquireTokenAsync` 또는 `AcquireTokenSilentAsync`를 통해 획득한 토큰에 대한 기본 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57585-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="57585-116">속성</span><span class="sxs-lookup"><span data-stu-id="57585-116">Property</span></span>  |<span data-ttu-id="57585-117">형식</span><span class="sxs-lookup"><span data-stu-id="57585-117">Format</span></span>  |<span data-ttu-id="57585-118">설명</span><span class="sxs-lookup"><span data-stu-id="57585-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="57585-119">이름</span><span class="sxs-lookup"><span data-stu-id="57585-119">Name</span></span> | <span data-ttu-id="57585-120">{User Full name}</span><span class="sxs-lookup"><span data-stu-id="57585-120">{User Full name}</span></span> |<span data-ttu-id="57585-121">사용자의 이름과 성</span><span class="sxs-lookup"><span data-stu-id="57585-121">The user’s first and last name</span></span>|
|<span data-ttu-id="57585-122">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="57585-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="57585-123">사용자를 식별하는 데 사용하는 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="57585-123">The username used to identify the user</span></span>|
|<span data-ttu-id="57585-124">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="57585-124">Token Expires</span></span> |<span data-ttu-id="57585-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="57585-125">{DateTime}</span></span>         |<span data-ttu-id="57585-126">토큰이 만료되는 시간.</span><span class="sxs-lookup"><span data-stu-id="57585-126">The time on which the token expires.</span></span> <span data-ttu-id="57585-127">MSAL에서는 필요한 경우 토큰을 갱신해 만료 날짜를 자동으로 연장합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="57585-128">액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="57585-128">Access token</span></span> |<span data-ttu-id="57585-129">{String}</span><span class="sxs-lookup"><span data-stu-id="57585-129">{String}</span></span>         |<span data-ttu-id="57585-130">인증 헤더가 필요한 HTTP 요청으로 전송될 토큰 문자열</span><span class="sxs-lookup"><span data-stu-id="57585-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="57585-131">범위 및 위임된 권한에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="57585-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="57585-132">사용자 프로필을 읽으려면 Graph API에는 `user.read` 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="57585-133">이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="57585-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="57585-134">일부 다른 Graph API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="57585-135">예를 들어 Graph의 경우 사용자 일정을 나열하려면 `Calendars.Read`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="57585-136">응용 프로그램의 컨텍스트에서 사용자 일정에 액세스하려면 `Calendars.Read` 위임 응용 프로그램 등록 정보를 추가한 다음 `AcquireTokenAsync` 호출에 `Calendars.Read`를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57585-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="57585-137">범위 수를 늘리면 사용자에게 추가 동의를 요청하는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57585-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



