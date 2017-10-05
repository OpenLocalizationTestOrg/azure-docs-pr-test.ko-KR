---
title: "모바일 앱을 사용하여 Apache Cordova에 인증 추가 | Microsoft Docs"
description: "Azure 앱 서비스에서 모바일 앱을 사용하여 Google, Facebook, Twitter, Microsoft를 비롯한 다양한 ID 공급자를 통해 Apache Cordova 앱의 사용자를 인증하는 방법을 알아봅니다."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="84bea-103">Apache Cordova 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="84bea-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="84bea-104">요약</span><span class="sxs-lookup"><span data-stu-id="84bea-104">Summary</span></span>
<span data-ttu-id="84bea-105">이 자습서에서는 지원되는 ID 공급자를 사용하여 Apache Cordova의 할 일 모음 빠른 시작 프로젝트에 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="84bea-106">이 자습서는 [Mobile Apps 시작] 자습서를 기반으로 하며 이를 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="84bea-107"><a name="register"></a>인증을 위해 앱 등록 및 앱 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="84bea-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="84bea-108">유사한 단계를 보여 주는 비디오 보기</span><span class="sxs-lookup"><span data-stu-id="84bea-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="84bea-109"><a name="permissions"></a>사용 권한을 인증된 사용자로 제한</span><span class="sxs-lookup"><span data-stu-id="84bea-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="84bea-110">이제 백 엔드에 대한 익명 액세스가 비활성화되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="84bea-111">Visual Studio에서</span><span class="sxs-lookup"><span data-stu-id="84bea-111">In Visual Studio:</span></span>

* <span data-ttu-id="84bea-112">[Mobile Apps 시작]자습서를 완료했을 때 생성된 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="84bea-113">**Google Android 에뮬레이터**에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="84bea-114">앱이 시작된 후 예기치 않은 연결 오류가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="84bea-115">다음으로 앱을 업데이트하여 모바일 앱 백 엔드에서 리소스를 요청하기 전에 사용자를 인증하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="84bea-116"><a name="add-authentication"></a>앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="84bea-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="84bea-117">**Visual Studio**에서 프로젝트를 연 다음 편집을 위해 `www/index.html` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="84bea-118">헤드 섹션에서 `Content-Security-Policy` META 태그를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="84bea-119">허용된 원본 목록에 OAuth 호스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="84bea-120">공급자</span><span class="sxs-lookup"><span data-stu-id="84bea-120">Provider</span></span> | <span data-ttu-id="84bea-121">SDK 공급자 이름</span><span class="sxs-lookup"><span data-stu-id="84bea-121">SDK Provider Name</span></span> | <span data-ttu-id="84bea-122">OAuth 호스트</span><span class="sxs-lookup"><span data-stu-id="84bea-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="84bea-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84bea-123">Azure Active Directory</span></span> | <span data-ttu-id="84bea-124">aad</span><span class="sxs-lookup"><span data-stu-id="84bea-124">aad</span></span> | <span data-ttu-id="84bea-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="84bea-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="84bea-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="84bea-126">Facebook</span></span> | <span data-ttu-id="84bea-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="84bea-127">facebook</span></span> | <span data-ttu-id="84bea-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="84bea-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="84bea-129">Google</span><span class="sxs-lookup"><span data-stu-id="84bea-129">Google</span></span> | <span data-ttu-id="84bea-130">Google</span><span class="sxs-lookup"><span data-stu-id="84bea-130">google</span></span> | <span data-ttu-id="84bea-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="84bea-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="84bea-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="84bea-132">Microsoft</span></span> | <span data-ttu-id="84bea-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="84bea-133">microsoftaccount</span></span> | <span data-ttu-id="84bea-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="84bea-134">https://login.live.com</span></span> |
   | <span data-ttu-id="84bea-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="84bea-135">Twitter</span></span> | <span data-ttu-id="84bea-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="84bea-136">twitter</span></span> | <span data-ttu-id="84bea-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="84bea-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="84bea-138">다음은 Content-Security-Policy(Azure Active Directory용으로 구현됨) 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="84bea-139">`https://login.microsoftonline.com`을 위 표의 OAuth 호스트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="84bea-140">content-security-policy 메타 태그에 대한 자세한 내용은 [Content-Security-Policy 설명서]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84bea-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="84bea-141">일부 인증 공급자에서는 적절한 모바일 장치에서 사용하는 경우 Content-Security-Policy 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="84bea-142">예를 들어 Android 장치에서 Google 인증을 사용하는 경우 Content-Security-Policy를 변경하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="84bea-143">편집을 위해 `www/js/index.js` 파일을 열고 `onDeviceReady()` 메서드를 찾아 클라이언트 생성 코드에서 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="84bea-144">이 코드는 테이블 참조를 만들고 UI를 새로 고치는 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="84bea-145">login() 메서드는 공급자를 사용하여 인증을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="84bea-146">login() 메서드는 JavaScript 프라미스를 반환하는 비동기 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="84bea-147">초기화의 나머지는 login() 메서드가 완료될 때까지 실행되지 않도록 프라미스 응답 안에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="84bea-148">방금 추가한 코드에서 `SDK_Provider_Name` 를 로그인 공급자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="84bea-149">예를 들어 Azure Active Directory의 경우 `client.login('aad')`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="84bea-150">프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-150">Run your project.</span></span>  <span data-ttu-id="84bea-151">프로젝트 초기화가 완료되면 응용 프로그램에서 선택한 인증 공급자에 대한 OAuth 로그인 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="84bea-152"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="84bea-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="84bea-153">Azure 앱 서비스의 [인증 정보] 에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="84bea-154">[푸시 알림] 을 Apache Cordova 앱에 추가하여 자습서를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="84bea-155">SDK 사용 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="84bea-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="84bea-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="84bea-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="84bea-157">[ASP.NET 서버 SDK]</span><span class="sxs-lookup"><span data-stu-id="84bea-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="84bea-158">[Node.js 서버 SDK]</span><span class="sxs-lookup"><span data-stu-id="84bea-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="84bea-159">[Mobile Apps 시작]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="84bea-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="84bea-160">[Content-Security-Policy 설명서]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="84bea-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="84bea-161">[푸시 알림]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="84bea-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="84bea-162">[인증 정보]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="84bea-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="84bea-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="84bea-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="84bea-164">[ASP.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="84bea-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="84bea-165">[Node.js 서버 SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="84bea-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
