---
title: "aaaAuthentication 및 Azure 모바일 앱에 대 한 권한 부여 | Microsoft Docs"
description: "개념적 참조 및 간략하게 hello 인증 / 권한 부여 Azure 모바일 앱에 대 한 기능"
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
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a><span data-ttu-id="c3a83-103">Azure 모바일 앱의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c3a83-103">Authentication and Authorization in Azure Mobile Apps</span></span>
## <a name="what-is-app-service-authentication--authorization"></a><span data-ttu-id="c3a83-104">앱 서비스 인증/권한 부여란?</span><span class="sxs-lookup"><span data-stu-id="c3a83-104">What is App Service Authentication / Authorization?</span></span>
> [!NOTE]
> <span data-ttu-id="c3a83-105">이 항목에는 마이그레이션된 tooa 통합 됩니다 [응용 프로그램 서비스 인증 / 권한 부여](../app-service/app-service-authentication-overview.md) 웹, 모바일 및 API 앱에 설명 하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-105">This topic will be migrated tooa consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="c3a83-106">앱 서비스 인증 / 권한 부여는 hello 앱 백 엔드에 필요한 코드 변경 없이 사용자가 응용 프로그램 toolog 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-106">App Service Authentication / Authorization is a feature which allows your application toolog in users with no code changes required on hello app backend.</span></span> <span data-ttu-id="c3a83-107">제공을 쉽게 tooprotect 응용 프로그램 및 작업 사용자별 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-107">It provides an easy way tooprotect your application and work with per-user data.</span></span>

<span data-ttu-id="c3a83-108">응용 프로그램 서비스는 페더레이션된 id를 사용 하 여 한 타사 **id 공급자** hello 응용 프로그램에서이 id를 사용 하 여 자체 대신 및 계정을 저장 하 고 사용자를 인증 하는 "IDP (").</span><span class="sxs-lookup"><span data-stu-id="c3a83-108">App Service uses federated identity, in which a 3rd-party **identity provider** ("IDP") stores accounts and authenticates users, and hello application uses this identity instead of its own.</span></span> <span data-ttu-id="c3a83-109">응용 프로그램 서비스는 hello 초기 5 개 id 공급자 지원: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft 계정*, 및 *Twitter*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-109">App Service supports five identity providers out of hello box: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, and *Twitter*.</span></span> <span data-ttu-id="c3a83-110">또한 다른 ID 공급자 또는 사용자 고유의 사용자 지정 ID 솔루션을 통합하여 앱에 이 지원을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-110">You can also expand this support for your apps by integrating another identity provider or your own custom identity solution.</span></span>

<span data-ttu-id="c3a83-111">앱은 개수에 관계 없이 이러한 ID 공급자를 활용할 수 있으므로 최종 사용자에게 로그인 방법에 대한 옵션을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-111">Your app can leverage any number of these identity providers, so you can provide your end users with options for how they login.</span></span>

<span data-ttu-id="c3a83-112">Tooget 당장 시작 하려면 다음 자습서 hello 중 하나 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c3a83-112">If you wish tooget started right away, please see one of hello following tutorials:</span></span>

* <span data-ttu-id="c3a83-113">[인증 tooyour iOS 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-113">[Add authentication tooyour iOS app]</span></span>
* <span data-ttu-id="c3a83-114">[인증 tooyour Xamarin.iOS 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-114">[Add authentication tooyour Xamarin.iOS app]</span></span>
* <span data-ttu-id="c3a83-115">[인증 tooyour Xamarin.Android 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-115">[Add authentication tooyour Xamarin.Android app]</span></span>
* <span data-ttu-id="c3a83-116">[인증 tooyour Windows 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-116">[Add Authentication tooyour Windows app]</span></span>

## <a name="how-authentication-works"></a><span data-ttu-id="c3a83-117">인증 작동 방법</span><span class="sxs-lookup"><span data-stu-id="c3a83-117">How authentication works</span></span>
<span data-ttu-id="c3a83-118">순서 tooauthenticate hello id 공급자 중 하나를 사용 하 여에서 먼저 응용 프로그램에 대 한 tooconfigure hello identity provider tooknow를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-118">In order tooauthenticate using one of hello identity providers, you first need tooconfigure hello identity provider tooknow about your application.</span></span> <span data-ttu-id="c3a83-119">hello id 공급자는 다음 Id 및 제공 백 toohello 응용 프로그램을 제공 하는 비밀 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-119">hello identity provider will then provide you with IDs and secrets that you provide back toohello application.</span></span> <span data-ttu-id="c3a83-120">이 hello 트러스트 관계를 완료 하 고 앱 서비스 toovalidate 제공 된 id tooit를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-120">This completes hello trust relationship and allows App Service toovalidate identities provided tooit.</span></span>

<span data-ttu-id="c3a83-121">이러한 단계는 hello 다음 항목에서에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-121">These steps are detailed in hello following topics:</span></span>

* <span data-ttu-id="c3a83-122">[어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-122">[How tooconfigure your app toouse Azure Active Directory login]</span></span>
* <span data-ttu-id="c3a83-123">[어떻게 tooconfigure 앱 toouse Facebook 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-123">[How tooconfigure your app toouse Facebook login]</span></span>
* <span data-ttu-id="c3a83-124">[어떻게 tooconfigure 앱 toouse Google 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-124">[How tooconfigure your app toouse Google login]</span></span>
* <span data-ttu-id="c3a83-125">[어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-125">[How tooconfigure your app toouse Microsoft Account login]</span></span>
* <span data-ttu-id="c3a83-126">[어떻게 tooconfigure 앱 toouse Twitter 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-126">[How tooconfigure your app toouse Twitter login]</span></span>

<span data-ttu-id="c3a83-127">모든 hello 백 엔드에 구성 되 면 프로그램 클라이언트 toolog에서 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-127">Once everything is configured on hello backend, you can modify your client toolog in.</span></span> <span data-ttu-id="c3a83-128">두 가지 접근 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-128">There are two approaches here:</span></span>

* <span data-ttu-id="c3a83-129">클라이언트 SDK hello 모바일 앱을 통해 코드의 한 줄을 사용 하 여 사용자가에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-129">Using a single line of code, let hello Mobile Apps client SDK sign in users.</span></span>
* <span data-ttu-id="c3a83-130">지정한 id 공급자 tooestablish id가 게시 한 SDK를 활용와 관련 된 액세스 tooApp 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-130">Leverage an SDK published by a given identity provider tooestablish identity and then gain access tooApp Service.</span></span>

> [!TIP]
> <span data-ttu-id="c3a83-131">대부분의 응용 프로그램 보다 네이티브 느낌 로그인 환경 및 tooleverage 새로 고침 지원 및 기타 공급자별 혜택 공급자 SDK tooget 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-131">Most applications should use a provider SDK tooget a more native-feeling login experience and tooleverage refresh support and other provider-specific benefits.</span></span>
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a><span data-ttu-id="c3a83-132">공급자 SDK 없이 인증 작동 방법</span><span class="sxs-lookup"><span data-stu-id="c3a83-132">How authentication without a provider SDK works</span></span>
<span data-ttu-id="c3a83-133">공급자 SDK tooset 지 수에 대 한 모바일 앱 tooperform hello 로그인을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-133">If you do not wish tooset up a provider SDK, you can allow Mobile Apps tooperform hello login for you.</span></span> <span data-ttu-id="c3a83-134">hello 모바일 앱 클라이언트 SDK를 선택 하 고 완전 hello에 대 한 로그인의 웹 보기 toohello 공급자를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-134">hello Mobile Apps client SDK will open a web view toohello provider of your choosing and complete hello sign in.</span></span> <span data-ttu-id="c3a83-135">블로그 및 포럼 나타납니다에 경우에 따라이 tooas hello "서버 흐름" 또는 "서버에서 제어 흐름" hello 서버 이후 hello 로그인을 관리 하는 및 참조 hello 클라이언트 SDK hello 공급자 토큰이 오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-135">Occasionally on blogs and forums you will see this referred tooas hello "server flow" or "server-directed flow" since hello server is managing hello login, and hello client SDK never receives hello provider token.</span></span>

<span data-ttu-id="c3a83-136">hello 코드에는 각 플랫폼에 대 한 hello 인증 자습서에서이 흐름 설명 toostart가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-136">hello code needed toostart this flow is covered in hello authentication tutorial for each platform.</span></span> <span data-ttu-id="c3a83-137">Hello 흐름의 hello 끝 hello 클라이언트 SDK는 앱 서비스 토큰 않았으며 hello 토큰은 자동으로 연결 된 tooall 요청 toohello 백 엔드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-137">At hello end of hello flow, hello client SDK has an App Service token, and hello token is automatically attached tooall requests toohello backend.</span></span>

### <a name="how-authentication-with-a-provider-sdk-works"></a><span data-ttu-id="c3a83-138">공급자 SDK를 통한 인증 작동 방법</span><span class="sxs-lookup"><span data-stu-id="c3a83-138">How authentication with a provider SDK works</span></span>
<span data-ttu-id="c3a83-139">Hello 로그인 경험 toointeract hello 플랫폼에서 실행 되 고 OS hello 앱와 보다 긴밀 하 게 허용 하는 공급자 SDK 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-139">Working with a provider SDK allows hello log-in experience toointeract more tightly with hello platform OS hello app is running on.</span></span> <span data-ttu-id="c3a83-140">또한 이렇게 하면 공급자 토큰과 훨씬 더 쉽게 tooconsume graph Api를 사용 하면 있으며 hello 사용자 환경을 사용자 지정 하는 hello 클라이언트에 대 한 사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-140">This also gives you a provider token and some user information on hello client, which makes it much easier tooconsume graph APIs and customize hello user experience.</span></span> <span data-ttu-id="c3a83-141">경우에 따라 블로그 및 포럼에 표시이 참조 tooas hello "클라이언트 흐름" 또는 "클라이언트에서 제어 흐름" 코드 이후 hello 클라이언트 hello 로그인을 처리 하는 되 고 hello 클라이언트 코드는 액세스 tooa 공급자 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-141">Occasionally on blogs and forums you will see this referred tooas hello "client flow" or "client-directed flow" since code on hello client is handling hello login, and hello client code has access tooa provider token.</span></span>

<span data-ttu-id="c3a83-142">공급자 토큰을 가져온 후 toobe tooApp 서비스 유효성 검사를 위해 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-142">Once a provider token is obtained, it needs toobe sent tooApp Service for validation.</span></span> <span data-ttu-id="c3a83-143">Hello 흐름의 hello 끝 hello 클라이언트 SDK는 앱 서비스 토큰 않았으며 hello 토큰은 자동으로 연결 된 tooall 요청 toohello 백 엔드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-143">At hello end of hello flow, hello client SDK has an App Service token, and hello token is automatically attached tooall requests toohello backend.</span></span> <span data-ttu-id="c3a83-144">또한 hello 개발자는 선택 하는 경우 참조 toohello 공급자 토큰을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-144">hello developer can also keep a reference toohello provider token if they so choose.</span></span>

## <a name="how-authorization-works"></a><span data-ttu-id="c3a83-145">권한 부여 작동 원리</span><span class="sxs-lookup"><span data-stu-id="c3a83-145">How authorization works</span></span>
<span data-ttu-id="c3a83-146">앱 서비스 인증 / 권한 부여를 위한 여러 가지 노출 **요청이 인증 되지 않은 경우 동작 tootake**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-146">App Service Authentication / Authorization exposes several choices for **Action tootake when request is not authenticated**.</span></span> <span data-ttu-id="c3a83-147">코드를 지정 된 요청을 받으면 전에 포함할 수 앱 서비스 검사 toosee hello 요청이 인증 되 면 있으며 그렇지 않은 경우를 거부 하 고 다시 시도 하기 전에 toohave hello 사용자 로그인을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-147">Before your code receives a given request, you can have App Service check toosee if hello request is authenticated and if not, reject it and attempt toohave hello user log in before trying again.</span></span>

<span data-ttu-id="c3a83-148">한 가지 옵션은 인증 되지 않은 toohave 요청 tooone hello id 공급자의 리디렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-148">One option is toohave unauthenticated requests redirect tooone of hello identity providers.</span></span> <span data-ttu-id="c3a83-149">웹 브라우저에서이 실제로 걸립니다 hello 사용자 tooa 새 페이지.</span><span class="sxs-lookup"><span data-stu-id="c3a83-149">In a web browser, this would actually take hello user tooa new page.</span></span> <span data-ttu-id="c3a83-150">그러나 모바일 클라이언트는 이러한 방식으로 리디렉션할 수 없고 인증되지 않은 응답은 HTTP *401 권한 없는* 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-150">However, your mobile client cannot be redirected in this way, and unauthenticated responses will receive an HTTP *401 Unauthorized* response.</span></span> <span data-ttu-id="c3a83-151">Hello 첫 번째 요청 하면 클라이언트는 항상 toohello 로그인 끝점 이어야 하 고 만들 수 있습니다이 점을 고려 tooany 다른 Api를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-151">Given this, hello first request your client makes should always be toohello login endpoint, and then you can make calls tooany other APIs.</span></span> <span data-ttu-id="c3a83-152">로그인 하기 전에 다른 API toocall 시도 하면 클라이언트에 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-152">If you attempt toocall another API before logging in, your client will receive an error.</span></span>

<span data-ttu-id="c3a83-153">보다 세부적인 toohave를 원하는 경우 인증을 요구 하는 끝점을 통해 컨트롤을 선택할 수 있습니다 "동작 안 함 (요청을 허용 합니다.)" 인증 되지 않은 요청에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-153">If you wish toohave more granular control over which endpoints require authentication, you can also pick "No action (allow request)" for unauthenticated requests.</span></span> <span data-ttu-id="c3a83-154">모든 인증 결정이 경우에 지연 된 tooyour 응용 프로그램 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-154">In this case, all authentication decisions are deferred tooyour application code.</span></span> <span data-ttu-id="c3a83-155">또한이 방법을 통해 사용자 지정 권한 부여 규칙에 따라 tooallow 액세스 toospecific 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-155">This also allows you tooallow access toospecific users based on custom authorization rules.</span></span>

## <a name="documentation"></a><span data-ttu-id="c3a83-156">설명서</span><span class="sxs-lookup"><span data-stu-id="c3a83-156">Documentation</span></span>
<span data-ttu-id="c3a83-157">자습서 표시 방법을 따르는 hello tooadd 인증 tooyour 모바일 클라이언트 응용 프로그램 서비스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c3a83-157">hello following tutorials show how tooadd authentication tooyour mobile clients using App Service:</span></span>

* <span data-ttu-id="c3a83-158">[인증 tooyour iOS 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-158">[Add authentication tooyour iOS app]</span></span>
* <span data-ttu-id="c3a83-159">[인증 tooyour Xamarin.iOS 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-159">[Add authentication tooyour Xamarin.iOS app]</span></span>
* <span data-ttu-id="c3a83-160">[인증 tooyour Xamarin.Android 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-160">[Add authentication tooyour Xamarin.Android app]</span></span>
* <span data-ttu-id="c3a83-161">[인증 tooyour Windows 앱 추가]</span><span class="sxs-lookup"><span data-stu-id="c3a83-161">[Add Authentication tooyour Windows app]</span></span>

<span data-ttu-id="c3a83-162">자습서 표시 방법을 따르는 hello tooconfigure 앱 서비스 tooleverage 서로 다른 인증 공급자:</span><span class="sxs-lookup"><span data-stu-id="c3a83-162">hello following tutorials show how tooconfigure App Service tooleverage different authentication providers:</span></span>

* <span data-ttu-id="c3a83-163">[어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-163">[How tooconfigure your app toouse Azure Active Directory login]</span></span>
* <span data-ttu-id="c3a83-164">[어떻게 tooconfigure 앱 toouse Facebook 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-164">[How tooconfigure your app toouse Facebook login]</span></span>
* <span data-ttu-id="c3a83-165">[어떻게 tooconfigure 앱 toouse Google 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-165">[How tooconfigure your app toouse Google login]</span></span>
* <span data-ttu-id="c3a83-166">[어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-166">[How tooconfigure your app toouse Microsoft Account login]</span></span>
* <span data-ttu-id="c3a83-167">[어떻게 tooconfigure 앱 toouse Twitter 로그인]</span><span class="sxs-lookup"><span data-stu-id="c3a83-167">[How tooconfigure your app toouse Twitter login]</span></span>

<span data-ttu-id="c3a83-168">원하는 경우 toouse id 시스템 이외의 hello도 활용할 수는 여기에서 제공 된 하 게 hello [미리 보기를 사용자 지정 인증 지원 hello.NET 서버 SDK에서에서](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a83-168">If you wish toouse an identity system other than hello ones provided here, you can also leverage hello [preview custom authentication support in hello .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).</span></span>

[인증 tooyour iOS 앱 추가]: app-service-mobile-ios-get-started-users.md
[인증 tooyour Xamarin.iOS 앱 추가]: app-service-mobile-xamarin-ios-get-started-users.md
[인증 tooyour Xamarin.Android 앱 추가]: app-service-mobile-xamarin-android-get-started-users.md
[인증 tooyour Windows 앱 추가]: app-service-mobile-windows-store-dotnet-get-started-users.md

[어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인]: app-service-mobile-how-to-configure-active-directory-authentication.md
[어떻게 tooconfigure 앱 toouse Facebook 로그인]: app-service-mobile-how-to-configure-facebook-authentication.md
[어떻게 tooconfigure 앱 toouse Google 로그인]: app-service-mobile-how-to-configure-google-authentication.md
[어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인]: app-service-mobile-how-to-configure-microsoft-authentication.md
[어떻게 tooconfigure 앱 toouse Twitter 로그인]: app-service-mobile-how-to-configure-twitter-authentication.md
