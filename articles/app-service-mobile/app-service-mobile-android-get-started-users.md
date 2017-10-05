---
title: "Mobile App을 사용하여 Android에 인증 추가 | Microsoft Docs"
description: "Azure App Service 기능의 Mobile Apps를 사용하여 Google, Facebook, Twitter, Microsoft를 비롯한 다양한 ID 공급자를 통해 Android 앱의 사용자를 인증하는 방법을 알아봅니다."
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
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="44ea7-103">Android 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="44ea7-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="44ea7-104">요약</span><span class="sxs-lookup"><span data-stu-id="44ea7-104">Summary</span></span>
<span data-ttu-id="44ea7-105">이 자습서에서는 지원되는 ID 공급자를 사용하여 Android의 할 일 모음 빠른 시작 프로젝트에 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="44ea7-106">이 자습서는 [모바일 앱 시작] 자습서를 기반으로 하며 이를 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="44ea7-107"><a name="register"></a>인증을 위한 앱 등록 및 Azure App Service 구성</span><span class="sxs-lookup"><span data-stu-id="44ea7-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="44ea7-108"><a name="redirecturl"></a>허용되는 외부 리디렉션 URL에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="44ea7-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="44ea7-109">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="44ea7-110">이를 통해 인증 시스템은 인증 프로세스가 완료되면 앱으로 다시 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="44ea7-111">이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="44ea7-112">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="44ea7-113">이 체계는 모바일 응용 프로그램에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="44ea7-114">서버 쪽에서 리디렉션을 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="44ea7-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="44ea7-115">[Azure Portal]에서 해당 App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="44ea7-116">**인증/권한 부여** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="44ea7-117">**허용되는 외부 리디렉션 URL**에서 `appname://easyauth.callback`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="44ea7-118">이 문자열의 _appname_은 모바일 응용 프로그램에 대한 URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="44ea7-119">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="44ea7-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="44ea7-120">여러 위치에서 URL 체계에 따라 모바일 응용 프로그램 코드를 조정해야 할 경우 선택한 문자열을 적어두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="44ea7-121">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-121">Click **OK**.</span></span>

5. <span data-ttu-id="44ea7-122">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-122">Click **Save**.</span></span>

## <span data-ttu-id="44ea7-123"><a name="permissions"></a>사용 권한을 인증된 사용자로 제한</span><span class="sxs-lookup"><span data-stu-id="44ea7-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="44ea7-124">Android Studio에서 [모바일 앱 시작] 자습서를 완료한 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="44ea7-125">**실행** 메뉴에서 **앱 실행**을 클릭하여 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="44ea7-126">이 예외는 앱이 인증되지 않은 사용자로 백 엔드에 액세스하려고 시도하지만 *할 일 모음* 테이블에서 이제 인증을 요구하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="44ea7-127">다음으로 앱을 업데이트하여 Mobile Apps 백 엔드에서 리소스를 요청하기 전에 사용자를 인증하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="44ea7-128">앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="44ea7-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="44ea7-129"><a name="cache-tokens"></a>클라이언트에 인증 토큰 캐시</span><span class="sxs-lookup"><span data-stu-id="44ea7-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="44ea7-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44ea7-130">Next steps</span></span>
<span data-ttu-id="44ea7-131">이 기본 인증 자습서를 완료했으므로 다음 자습서 중 하나를 계속하는 것을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="44ea7-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="44ea7-132">[Android 앱에 푸시 알림을 추가합니다](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="44ea7-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="44ea7-133">Azure Notification Hubs를 사용하는 Mobile Apps 백 엔드를 구성하여 푸시 알림을 보내는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="44ea7-134">[Android 앱에 대해 오프라인 동기화를 사용합니다](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="44ea7-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="44ea7-135">Mobile Apps 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="44ea7-136">오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ea7-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="44ea7-137">[모바일 앱 시작]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="44ea7-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>
