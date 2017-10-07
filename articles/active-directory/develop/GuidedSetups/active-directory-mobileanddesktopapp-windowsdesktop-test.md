---
title: "AD aaaAzure v2 Windows 데스크톱 시작-테스트 | Microsoft Docs"
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="b4896-103">코드 테스트</span><span class="sxs-lookup"><span data-stu-id="b4896-103">Test your code</span></span>

<span data-ttu-id="b4896-104">순서로 tootest 키를 눌러 응용 프로그램 `F5` toorun Visual Studio에서 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b4896-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="b4896-105">아래와 같이 주 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-105">Your Main Window should appear:</span></span>

![샘플 스크린샷](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="b4896-107">준비 tootest 완료 했으면 클릭 *Microsoft Graph API 호출* 하 고 실행 하는 Microsoft Azure Active Directory (조직 계정)에서 Microsoft 계정 (live.com, outlook.com) 계정 toosign 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="b4896-108">그 hello 처음으로, 요청에 사용자 toosign 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![로그인](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="b4896-110">동의</span><span class="sxs-lookup"><span data-stu-id="b4896-110">Consent</span></span>
<span data-ttu-id="b4896-111">hello tooyour 응용 프로그램에 로그인 하는 처음으로 있습니다 나타납니다 toohello 비슷한 아래 동의 화면, tooexplicitly에 동의 해야 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b4896-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![동의 화면](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="b4896-113">예상 결과</span><span class="sxs-lookup"><span data-stu-id="b4896-113">Expected results</span></span>
<span data-ttu-id="b4896-114">Hello API 호출 결과 화면 hello Microsoft Graph API 호출에서 반환 된 사용자 프로필 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="b4896-115">또한 표시를 통해 확보 하는 hello 토큰에 대 한 기본 정보 `AcquireTokenAsync` 또는 `AcquireTokenSilentAsync` hello 토큰 정보 상자에서:</span><span class="sxs-lookup"><span data-stu-id="b4896-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="b4896-116">속성</span><span class="sxs-lookup"><span data-stu-id="b4896-116">Property</span></span>  |<span data-ttu-id="b4896-117">형식</span><span class="sxs-lookup"><span data-stu-id="b4896-117">Format</span></span>  |<span data-ttu-id="b4896-118">설명</span><span class="sxs-lookup"><span data-stu-id="b4896-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="b4896-119">이름</span><span class="sxs-lookup"><span data-stu-id="b4896-119">Name</span></span> | <span data-ttu-id="b4896-120">{User Full name}</span><span class="sxs-lookup"><span data-stu-id="b4896-120">{User Full name}</span></span> |<span data-ttu-id="b4896-121">hello 사용자 ् य ा च े ं</span><span class="sxs-lookup"><span data-stu-id="b4896-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="b4896-122">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="b4896-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="b4896-123">tooidentify hello 사용자를 사용 하는 hello 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="b4896-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="b4896-124">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="b4896-124">Token Expires</span></span> |<span data-ttu-id="b4896-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="b4896-125">{DateTime}</span></span>         |<span data-ttu-id="b4896-126">토큰이 만료 되는 hello에 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-126">hello time on which hello token expires.</span></span> <span data-ttu-id="b4896-127">MSAL 필요한 경우 hello 토큰을 갱신 하 여 사용자에 대 한 hello 만료 날짜를 확장 하면</span><span class="sxs-lookup"><span data-stu-id="b4896-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="b4896-128">액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="b4896-128">Access token</span></span> |<span data-ttu-id="b4896-129">{String}</span><span class="sxs-lookup"><span data-stu-id="b4896-129">{String}</span></span>         |<span data-ttu-id="b4896-130">토큰 문자열 hello tooHTTP 요청 권한 부여 헤더를 필요로 하는 전송 하는 전송</span><span class="sxs-lookup"><span data-stu-id="b4896-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="b4896-131">범위 및 위임된 권한에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="b4896-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="b4896-132">Graph API 필요 hello `user.read` tooread 사용자 프로필의 범위.</span><span class="sxs-lookup"><span data-stu-id="b4896-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="b4896-133">이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="b4896-134">일부 다른 Graph API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="b4896-135">그래프에 대 한 예를 들어 `Calendars.Read` 필요한 toolist 사용자 일정은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="b4896-136">순서로 tooaccess hello 응용 프로그램의 컨텍스트에서 사용자의 일정, tooadd 필요한 `Calendars.Read` 응용 프로그램 등록 정보를 위임 하 고 다음 추가 `Calendars.Read` toohello `AcquireTokenAsync` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="b4896-137">Hello 범위 수를 늘리면 추가 동의 대 한 메시지가 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4896-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



