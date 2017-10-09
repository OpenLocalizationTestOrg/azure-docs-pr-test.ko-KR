---
title: "AD aaaAzure v2 Android 시작-테스트 | Microsoft Docs"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="b7e5d-103">코드 테스트</span><span class="sxs-lookup"><span data-stu-id="b7e5d-103">Test your code</span></span>

1. <span data-ttu-id="b7e5d-104">코드 tooyour 장치/에뮬레이터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="b7e5d-105">준비 tootest 되 면 실행 하는 Microsoft Azure Active Directory (조직 계정) 또는에서 Microsoft 계정 (live.com, outlook.com) 계정 toosign를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="b7e5d-106">![샘플 스크린샷](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="b7e5d-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="b7e5d-107">
![로그인](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="b7e5d-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="b7e5d-108">동의</span><span class="sxs-lookup"><span data-stu-id="b7e5d-108">Consent</span></span>
<span data-ttu-id="b7e5d-109">hello tooyour 응용 프로그램에서 사용자가 처음으로 제공 됩니다 toohello 비슷한 아래 동의 화면으로, 어디에서 든 tooexplicitly 허용:</span><span class="sxs-lookup"><span data-stu-id="b7e5d-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![동의](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="b7e5d-111">예상 결과</span><span class="sxs-lookup"><span data-stu-id="b7e5d-111">Expected results</span></span>
<span data-ttu-id="b7e5d-112">결과가 표시 됩니다 hello 호출 tooMicrosoft Graph API의 'm e'는 끝점이 사용 tootooobtain hello 사용자 프로필-https://graph.microsoft.com/v1.0/me 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="b7e5d-113">일반적인 Microsoft Graph 끝점 목록은 이 [문서](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="b7e5d-114">범위 및 위임된 권한에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="b7e5d-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="b7e5d-115">Microsoft Graph API hello 필요 hello `user.read` tooread hello 사용자 프로필의 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="b7e5d-116">이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="b7e5d-117">일부 다른 Microsoft Graph용 API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="b7e5d-118">예를 들어 Microsoft Graph에 대해 범위를 hello `Calendars.Read` 필요한 toolist hello 사용자 일정은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="b7e5d-119">순서로 tooaccess hello 응용 프로그램의 컨텍스트에서 사용자의 일정, tooadd hello 필요한 `Calendars.Read` 위임 권한 toohello 응용 프로그램 등록 정보를 hello 추가 `Calendars.Read` 범위 toohello `acquireTokenSilentAsync` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="b7e5d-120">hello 사용자 hello 범위 수를 늘리면 추가 동의 대 한 안내가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7e5d-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
