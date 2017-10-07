---
title: "Android 모바일 앱에서 aaaAdd 인증 | Microsoft Docs"
description: "Toouse 다양 한 Google, Facebook, Twitter 및 Microsoft를 비롯 한 id 공급자를 통해 Android 앱의 Azure 앱 서비스 tooauthenticate 사용자의 모바일 앱 기능을 hello 하는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="bb010-103">인증 tooyour Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="bb010-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="bb010-104">요약</span><span class="sxs-lookup"><span data-stu-id="bb010-104">Summary</span></span>
<span data-ttu-id="bb010-105">이 자습서에서는 지원 되는 id 공급자를 사용 하 여 Android에서 인증 toohello todolist 퀵 스타트 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="bb010-106">이 자습서는 hello 기반 [모바일 앱 시작] 자습서 먼저 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="bb010-107"><a name="register"></a>인증을 위한 앱 등록 및 Azure App Service 구성</span><span class="sxs-lookup"><span data-stu-id="bb010-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="bb010-108"><a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가</span><span class="sxs-lookup"><span data-stu-id="bb010-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="bb010-109">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="bb010-110">Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="bb010-111">이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체.</span><span class="sxs-lookup"><span data-stu-id="bb010-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="bb010-112">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="bb010-113">고유 tooyour 모바일 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="bb010-114">hello 서버 쪽에서 tooenable hello 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="bb010-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="bb010-115">Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="bb010-116">Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="bb010-117">Hello에 **외부 리디렉션 Url 허용**, 입력 `appname://easyauth.callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="bb010-118">hello _appname_ 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="bb010-119">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="bb010-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="bb010-120">Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="bb010-121">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-121">Click **OK**.</span></span>

5. <span data-ttu-id="bb010-122">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-122">Click **Save**.</span></span>

## <span data-ttu-id="bb010-123"><a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한</span><span class="sxs-lookup"><span data-stu-id="bb010-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="bb010-124">Android Studio에서 hello 자습서와 함께 완료 hello 프로젝트를 열고 [모바일 앱 시작]합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="bb010-125">Hello에서 **실행** 메뉴를 클릭 하 여 **응용 프로그램을 실행**, hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="bb010-126">이 예외는 hello 앱 시도 tooaccess hello 다시 인증 되지 않은 사용자로 종료 하지만 hello 때문에 발생 *TodoItem* 테이블에는 이제 인증이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="bb010-127">다음으로, 모바일 앱을 다시 종료 hello에서 리소스를 요청 하기 전에 hello 앱 tooauthenticate 사용자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="bb010-128">인증 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="bb010-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="bb010-129"><a name="cache-tokens"></a>Hello 클라이언트에서 인증 토큰을 캐시</span><span class="sxs-lookup"><span data-stu-id="bb010-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="bb010-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb010-130">Next steps</span></span>
<span data-ttu-id="bb010-131">이 기본 인증 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="bb010-132">[푸시 알림 tooyour Android 앱 추가](app-service-mobile-android-get-started-push.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="bb010-133">모바일 앱 다시 tooconfigure toouse Azure 알림 허브 toosend 푸시 알림을 종료 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="bb010-134">[Android 앱에 대해 오프라인 동기화를 사용합니다](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="bb010-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="bb010-135">오프 라인 tooadd 모바일 앱 백 엔드를 사용 하 여 tooyour 응용 프로그램을 지 원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="bb010-136">오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb010-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[모바일 앱 시작]: app-service-mobile-android-get-started.md
