---
title: "Azure 모바일 앱의 인증 및 권한 부여 | Microsoft Docs"
description: "Azure 모바일 앱에 대한 인증/권한 부여 기능의 개념 참조 및 개요"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 92c9f91807a6b5d4fea6b504256508f805627a16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a><span data-ttu-id="6fde9-103">Azure 모바일 앱의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="6fde9-103">Authentication and Authorization in Azure Mobile Apps</span></span>
## <a name="what-is-app-service-authentication--authorization"></a><span data-ttu-id="6fde9-104">앱 서비스 인증/권한 부여란?</span><span class="sxs-lookup"><span data-stu-id="6fde9-104">What is App Service Authentication / Authorization?</span></span>
> [!NOTE]
> <span data-ttu-id="6fde9-105">이 항목은 웹, 모바일 및 API 앱을 다루는 통합된 [앱 서비스 인증/권한 부여](../app-service/app-service-authentication-overview.md) 항목으로 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-105">This topic will be migrated to a consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="6fde9-106">앱 서비스 인증/권한 부여는 응용 프로그램이 앱 백 엔드에 필요한 코드 변경 없이 사용자를 로그인할 수 있도록 만드는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-106">App Service Authentication / Authorization is a feature which allows your application to log in users with no code changes required on the app backend.</span></span> <span data-ttu-id="6fde9-107">응용 프로그램을 보호하고 사용자 단위당 데이터로 작업하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-107">It provides an easy way to protect your application and work with per-user data.</span></span>

<span data-ttu-id="6fde9-108">앱 서비스는 페더레이션된 ID를 사용하며 여기서 타사 **ID 공급자** ("IDP")는 계정을 저장하고 사용자를 인증하며 응용 프로그램은 자체 ID 대신 이 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-108">App Service uses federated identity, in which a 3rd-party **identity provider** ("IDP") stores accounts and authenticates users, and the application uses this identity instead of its own.</span></span> <span data-ttu-id="6fde9-109">App Service는 기본적으로 *Azure Active Directory*, *Facebook*, *Google*, *Microsoft 계정* 및 *Twitter*와 같은 다섯 가지 ID 공급자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-109">App Service supports five identity providers out of the box: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, and *Twitter*.</span></span> <span data-ttu-id="6fde9-110">또한 다른 ID 공급자 또는 사용자 고유의 사용자 지정 ID 솔루션을 통합하여 앱에 이 지원을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-110">You can also expand this support for your apps by integrating another identity provider or your own custom identity solution.</span></span>

<span data-ttu-id="6fde9-111">앱은 개수에 관계 없이 이러한 ID 공급자를 활용할 수 있으므로 최종 사용자에게 로그인 방법에 대한 옵션을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-111">Your app can leverage any number of these identity providers, so you can provide your end users with options for how they login.</span></span>

<span data-ttu-id="6fde9-112">지금 바로 시작하려는 경우 다음 자습서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fde9-112">If you wish to get started right away, please see one of the following tutorials:</span></span>

* <span data-ttu-id="6fde9-113">[iOS 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-113">[Add authentication to your iOS app]</span></span>
* <span data-ttu-id="6fde9-114">[Xamarin.iOS 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-114">[Add authentication to your Xamarin.iOS app]</span></span>
* <span data-ttu-id="6fde9-115">[Xamarin Android 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-115">[Add authentication to your Xamarin.Android app]</span></span>
* <span data-ttu-id="6fde9-116">[Windows 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-116">[Add Authentication to your Windows app]</span></span>

## <a name="how-authentication-works"></a><span data-ttu-id="6fde9-117">인증 작동 방법</span><span class="sxs-lookup"><span data-stu-id="6fde9-117">How authentication works</span></span>
<span data-ttu-id="6fde9-118">ID 공급자 중 하나를 사용하여 인증하려면 먼저 ID 공급자를 구성하여 응용 프로그램에 대해 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-118">In order to authenticate using one of the identity providers, you first need to configure the identity provider to know about your application.</span></span> <span data-ttu-id="6fde9-119">그러면 ID 공급자는 응용 프로그램에 다시 제공하는 ID 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-119">The identity provider will then provide you with IDs and secrets that you provide back to the application.</span></span> <span data-ttu-id="6fde9-120">트러스트 관계를 완료하고 앱 서비스가 제공된 ID의 유효성을 검사하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-120">This completes the trust relationship and allows App Service to validate identities provided to it.</span></span>

<span data-ttu-id="6fde9-121">이러한 단계는 다음 항목에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-121">These steps are detailed in the following topics:</span></span>

* <span data-ttu-id="6fde9-122">[Azure Active Directory 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-122">[How to configure your app to use Azure Active Directory login]</span></span>
* <span data-ttu-id="6fde9-123">[Facebook 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-123">[How to configure your app to use Facebook login]</span></span>
* <span data-ttu-id="6fde9-124">[Google 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-124">[How to configure your app to use Google login]</span></span>
* <span data-ttu-id="6fde9-125">[Microsoft 계정 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-125">[How to configure your app to use Microsoft Account login]</span></span>
* <span data-ttu-id="6fde9-126">[Twitter 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-126">[How to configure your app to use Twitter login]</span></span>

<span data-ttu-id="6fde9-127">모든 것이 백 엔드에서 구성되면 클라이언트를 수정하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-127">Once everything is configured on the backend, you can modify your client to log in.</span></span> <span data-ttu-id="6fde9-128">두 가지 접근 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-128">There are two approaches here:</span></span>

* <span data-ttu-id="6fde9-129">한 줄의 코드를 사용하여 모바일 앱 클라이언트 SDK가 사용자를 로그인하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-129">Using a single line of code, let the Mobile Apps client SDK sign in users.</span></span>
* <span data-ttu-id="6fde9-130">지정된 ID 공급자를 통해 게시된 SDK를 활용하여 ID를 설정한 다음 앱 서비스에 액세스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-130">Leverage an SDK published by a given identity provider to establish identity and then gain access to App Service.</span></span>

> [!TIP]
> <span data-ttu-id="6fde9-131">많은 응용 프로그램은 공급자 SDK를 사용하여 더 원시적인 로그인 환경을 가져오고 새로 고침 지원 및 기타 공급자별 혜택을 활용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-131">Most applications should use a provider SDK to get a more native-feeling login experience and to leverage refresh support and other provider-specific benefits.</span></span>
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a><span data-ttu-id="6fde9-132">공급자 SDK 없이 인증 작동 방법</span><span class="sxs-lookup"><span data-stu-id="6fde9-132">How authentication without a provider SDK works</span></span>
<span data-ttu-id="6fde9-133">공급자 SDK 설정하지 않으려는 경우 모바일 앱이 로그인을 실행하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-133">If you do not wish to set up a provider SDK, you can allow Mobile Apps to perform the login for you.</span></span> <span data-ttu-id="6fde9-134">모바일 앱 클라이언트 SDK는 선택한 공급자에게 웹 보기를 열고 로그인을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-134">The Mobile Apps client SDK will open a web view to the provider of your choosing and complete the sign in.</span></span> <span data-ttu-id="6fde9-135">서버가 로그인을 관리하고 클라이언트 SDK가 공급자 토큰을 받지 않기 때문에 경우에 따라 블로그 및 포럼에 "서버 흐름" 또는 "서버에서 제어된 흐름"이라는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-135">Occasionally on blogs and forums you will see this referred to as the "server flow" or "server-directed flow" since the server is managing the login, and the client SDK never receives the provider token.</span></span>

<span data-ttu-id="6fde9-136">이 흐름을 시작하는 데 필요한 코드는 각 플랫폼에 대한 인증 자습서에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-136">The code needed to start this flow is covered in the authentication tutorial for each platform.</span></span> <span data-ttu-id="6fde9-137">흐름의 끝에서 클라이언트 SDK에는 앱 서비스 토큰이 있고 토큰은 백 엔드에 대한 모든 요청에 자동으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-137">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span></span>

### <a name="how-authentication-with-a-provider-sdk-works"></a><span data-ttu-id="6fde9-138">공급자 SDK를 통한 인증 작동 방법</span><span class="sxs-lookup"><span data-stu-id="6fde9-138">How authentication with a provider SDK works</span></span>
<span data-ttu-id="6fde9-139">공급자 SDK로 작업하면 로그인 환경이 앱을 실행하는 플랫폼 OS와 더 밀접하게 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-139">Working with a provider SDK allows the log-in experience to interact more tightly with the platform OS the app is running on.</span></span> <span data-ttu-id="6fde9-140">또한 이렇게 하면 클라이언트의 공급자 토큰 및 사용자 정보를 가져오며 이는 Graph API를 사용하고 사용자 환경을 사용자 지정하는 작업을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-140">This also gives you a provider token and some user information on the client, which makes it much easier to consume graph APIs and customize the user experience.</span></span> <span data-ttu-id="6fde9-141">클라이언트의 코드가 로그인을 처리하고 클라이언트 코드가 공급자 토큰에 대한 액세스를 갖기 때문에 경우에 따라 블로그 및 포럼에서 "클라이언트 흐름" 또는 "클라이언트에서 제어된 흐름"이라는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-141">Occasionally on blogs and forums you will see this referred to as the "client flow" or "client-directed flow" since code on the client is handling the login, and the client code has access to a provider token.</span></span>

<span data-ttu-id="6fde9-142">공급자 토큰을 가져오면 유효성 검사에 대한 앱 서비스에 전송되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-142">Once a provider token is obtained, it needs to be sent to App Service for validation.</span></span> <span data-ttu-id="6fde9-143">흐름의 끝에서 클라이언트 SDK에는 앱 서비스 토큰이 있고 토큰은 백 엔드에 대한 모든 요청에 자동으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-143">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span></span> <span data-ttu-id="6fde9-144">또한 선택하는 경우 개발자는 공급자 토큰에 대한 참조를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-144">The developer can also keep a reference to the provider token if they so choose.</span></span>

## <a name="how-authorization-works"></a><span data-ttu-id="6fde9-145">권한 부여 작동 원리</span><span class="sxs-lookup"><span data-stu-id="6fde9-145">How authorization works</span></span>
<span data-ttu-id="6fde9-146">앱 서비스 인증/권한 부여는 **요청이 인증되지 않을 때 수행할 동작**에 대한 여러 가지 선택을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-146">App Service Authentication / Authorization exposes several choices for **Action to take when request is not authenticated**.</span></span> <span data-ttu-id="6fde9-147">코드가 지정된 요청을 받기 전에 앱 서비스가 요청이 인증되지를 확인하도록 하고 그렇지 않은 경우 거부하고 다시 시도하기 전에 사용자가 로그인을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-147">Before your code receives a given request, you can have App Service check to see if the request is authenticated and if not, reject it and attempt to have the user log in before trying again.</span></span>

<span data-ttu-id="6fde9-148">한 가지 옵션은 ID 공급자 중 하나로 인증되지 않은 요청을 리디렉션하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-148">One option is to have unauthenticated requests redirect to one of the identity providers.</span></span> <span data-ttu-id="6fde9-149">웹 브라우저에서 사용자를 새 페이지에 실제로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-149">In a web browser, this would actually take the user to a new page.</span></span> <span data-ttu-id="6fde9-150">그러나 모바일 클라이언트는 이러한 방식으로 리디렉션할 수 없고 인증되지 않은 응답은 HTTP *401 권한 없는* 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-150">However, your mobile client cannot be redirected in this way, and unauthenticated responses will receive an HTTP *401 Unauthorized* response.</span></span> <span data-ttu-id="6fde9-151">이 점을 고려하면 클라이언트가 만든 첫 번째 요청은 로그인 끝점에 항상 위치해야 하고 사용자가 다른 API 호출을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-151">Given this, the first request your client makes should always be to the login endpoint, and then you can make calls to any other APIs.</span></span> <span data-ttu-id="6fde9-152">로그인하기 전에 다른 API를 호출하려면 클라이언트에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-152">If you attempt to call another API before logging in, your client will receive an error.</span></span>

<span data-ttu-id="6fde9-153">또한 어떤 끝점이 인증을 요구하는지에 대해 보다 세부적으로 제어하려는 경우 인증되지 않은 요청에 대한 "작업 없음(요청 허용)"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-153">If you wish to have more granular control over which endpoints require authentication, you can also pick "No action (allow request)" for unauthenticated requests.</span></span> <span data-ttu-id="6fde9-154">이 경우에 모든 인증 결정은 응용 프로그램 코드에 연기됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-154">In this case, all authentication decisions are deferred to your application code.</span></span> <span data-ttu-id="6fde9-155">또한 사용자 지정 권한 부여 규칙에 기반하여 특정 사용자에 대한 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-155">This also allows you to allow access to specific users based on custom authorization rules.</span></span>

## <a name="documentation"></a><span data-ttu-id="6fde9-156">설명서</span><span class="sxs-lookup"><span data-stu-id="6fde9-156">Documentation</span></span>
<span data-ttu-id="6fde9-157">다음 자습서는 앱 서비스를 사용하여 모바일 클라이언트에 인증을 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-157">The following tutorials show how to add authentication to your mobile clients using App Service:</span></span>

* <span data-ttu-id="6fde9-158">[iOS 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-158">[Add authentication to your iOS app]</span></span>
* <span data-ttu-id="6fde9-159">[Xamarin.iOS 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-159">[Add authentication to your Xamarin.iOS app]</span></span>
* <span data-ttu-id="6fde9-160">[Xamarin Android 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-160">[Add authentication to your Xamarin.Android app]</span></span>
* <span data-ttu-id="6fde9-161">[Windows 앱에 인증 추가]</span><span class="sxs-lookup"><span data-stu-id="6fde9-161">[Add Authentication to your Windows app]</span></span>

<span data-ttu-id="6fde9-162">다음 자습서에서는 앱 서비스를 구성하여 다른 인증 공급자를 활용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-162">The following tutorials show how to configure App Service to leverage different authentication providers:</span></span>

* <span data-ttu-id="6fde9-163">[Azure Active Directory 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-163">[How to configure your app to use Azure Active Directory login]</span></span>
* <span data-ttu-id="6fde9-164">[Facebook 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-164">[How to configure your app to use Facebook login]</span></span>
* <span data-ttu-id="6fde9-165">[Google 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-165">[How to configure your app to use Google login]</span></span>
* <span data-ttu-id="6fde9-166">[Microsoft 계정 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-166">[How to configure your app to use Microsoft Account login]</span></span>
* <span data-ttu-id="6fde9-167">[Twitter 로그인을 사용하도록 앱을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="6fde9-167">[How to configure your app to use Twitter login]</span></span>

<span data-ttu-id="6fde9-168">여기에 제공된 것 이외의 ID 시스템을 사용하려는 경우 [.NET 서버 SDK에서 사용자 지정 인증 지원 미리 보기](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth)를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fde9-168">If you wish to use an identity system other than the ones provided here, you can also leverage the [preview custom authentication support in the .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).</span></span>

<span data-ttu-id="6fde9-169">[iOS 앱에 인증 추가]: app-service-mobile-ios-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-169">[Add authentication to your iOS app]: app-service-mobile-ios-get-started-users.md</span></span>
<span data-ttu-id="6fde9-170">[Xamarin.iOS 앱에 인증 추가]: app-service-mobile-xamarin-ios-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-170">[Add authentication to your Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started-users.md</span></span>
<span data-ttu-id="6fde9-171">[Xamarin Android 앱에 인증 추가]: app-service-mobile-xamarin-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-171">[Add authentication to your Xamarin.Android app]: app-service-mobile-xamarin-android-get-started-users.md</span></span>
<span data-ttu-id="6fde9-172">[Windows 앱에 인증 추가]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-172">[Add Authentication to your Windows app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>

<span data-ttu-id="6fde9-173">[Azure Active Directory 로그인을 사용하도록 앱을 구성하는 방법]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-173">[How to configure your app to use Azure Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="6fde9-174">[Facebook 로그인을 사용하도록 앱을 구성하는 방법]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-174">[How to configure your app to use Facebook login]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="6fde9-175">[Google 로그인을 사용하도록 앱을 구성하는 방법]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-175">[How to configure your app to use Google login]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="6fde9-176">[Microsoft 계정 로그인을 사용하도록 앱을 구성하는 방법]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-176">[How to configure your app to use Microsoft Account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="6fde9-177">[Twitter 로그인을 사용하도록 앱을 구성하는 방법]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="6fde9-177">[How to configure your app to use Twitter login]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
