---
title: "Azure AD v2 Android 시작 - 테스트 | Microsoft Docs"
description: "Android 앱이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="4017a-103">코드 테스트</span><span class="sxs-lookup"><span data-stu-id="4017a-103">Test your code</span></span>

1. <span data-ttu-id="4017a-104">장치/에뮬레이터에 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="4017a-105">테스트할 준비가 되면 Microsoft Azure Active Directory(조직 계정) 또는 Microsoft 계정(live.com, outlook.com)을 사용해 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="4017a-106">![샘플 스크린샷](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="4017a-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="4017a-107">
![로그인](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="4017a-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="4017a-108">동의</span><span class="sxs-lookup"><span data-stu-id="4017a-108">Consent</span></span>
<span data-ttu-id="4017a-109">사용자가 응용 프로그램에 처음으로 로그인하면 아래와 유사한 동의 화면이 표시됩니다. 사용자는 여기서 명시적으로 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![동의](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="4017a-111">예상 결과</span><span class="sxs-lookup"><span data-stu-id="4017a-111">Expected results</span></span>
<span data-ttu-id="4017a-112">사용자 프로필 https://graph.microsoft.com/v1.0/me를 얻는 데 사용된 Microsoft Graph API ‘me’ 끝점에 대한 호출 결과가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="4017a-113">일반적인 Microsoft Graph 끝점 목록은 이 [문서](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4017a-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="4017a-114">범위 및 위임된 권한에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="4017a-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="4017a-115">Microsoft Graph API는 `user.read` 범위가 있어야만 사용자 프로필을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="4017a-116">이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="4017a-117">일부 다른 Microsoft Graph용 API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="4017a-118">예를 들어 Microsoft Graph의 경우 사용자 일정을 나열하려면 `Calendars.Read` 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="4017a-119">응용 프로그램의 컨텍스트에서 사용자 일정에 액세스하려면 응용 프로그램 등록 정보에 `Calendars.Read` 위임 권한을 추가한 다음 `acquireTokenSilentAsync` 호출에 `Calendars.Read` 범위를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="4017a-120">범위 수를 늘리면 사용자에게 추가 동의를 요청하는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4017a-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
