---
title: "Azure AD v2.0 끝점으로 바꾸기 | Microsoft Docs"
description: "앱 모델 v2.0 공개 미리보기 프로토콜에 적용될 변경 사항에 대한 설명"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="ddb5f-103">v2.0 인증 프로토콜에 대한 중요 업데이트</span><span class="sxs-lookup"><span data-stu-id="ddb5f-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="ddb5f-104">개발자들은 주목하세요!</span><span class="sxs-lookup"><span data-stu-id="ddb5f-104">Attention developers!</span></span> <span data-ttu-id="ddb5f-105">앞으로 2주 동안 v2.0 인증 프로토콜에 대해 몇 가지 업데이트를 수행할 예정이며, 이는 미리보기 기간 동안 작성한 앱에 대해 상당한 변화를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="ddb5f-106">어떤 것이 영향을 받습니까?</span><span class="sxs-lookup"><span data-stu-id="ddb5f-106">Who does this affect?</span></span>
<span data-ttu-id="ddb5f-107">v2.0 수렴형 인증 끝점을 사용하여 작성된 모든 앱.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="ddb5f-108">v2.0 끝점에 대한 자세한 내용은 [여기](active-directory-appmodel-v2-overview.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="ddb5f-109">v2.0 프로토콜에 대해 직접 코딩하여 v2.0 끝점을 사용하거나 OpenID Connect 또는 OAuth 웹 미들웨어를 사용하거나 인증을 수행하기 위해 다른 타사 라이브러리를 사용하여 앱을 작성한 경우, 프로젝트를 테스트하고 필요하면 변경할 준비를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="ddb5f-110">어떤 것이 영향을 받지 않습니까?</span><span class="sxs-lookup"><span data-stu-id="ddb5f-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="ddb5f-111">프로덕션 Azure AD 인증 끝점에 대해 작성된 모든 앱.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="ddb5f-112">이 프로토콜은 확정되었으며 어떠한 변경도 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="ddb5f-113">또한 앱이 ADAL 라이브러리 **만** 를 사용하여 인증을 수행하는 경우 어떤 것도 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="ddb5f-114">ADAL은 앱을 변경하지 못하도록 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="ddb5f-115">변경 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ddb5f-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="ddb5f-116">JWT 헤더에서 x5t 값 제거</span><span class="sxs-lookup"><span data-stu-id="ddb5f-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="ddb5f-117">v2.0 끝점은 JWT 토큰을 광범위하게 사용하며, 토큰과 관련된 메타데이터와 헤더 매개 변수 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="ddb5f-118">현재 JWT 중 하나의 헤더를 디코딩하는 경우, 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="ddb5f-119">OpenID Connect 메타데이터 끝점에서 검색된 토큰의 서명 유효성을 검사하는 데 사용해야 하는 공개 키를 "x5t" 및 "kid"의 두 속성이 식별하는 위치.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="ddb5f-120">여기서 변경하려는 내용은 "x5t" 속성을 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="ddb5f-121">토큰 유효성을 검사하기 위해 동일한 메커니즘을 계속 사용할 수 있지만, OpenID Connect 프로토콜에 지정된 대로 올바른 공개 키를 검색하기 위해 "kid" 속성에만 의존해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ddb5f-122">**작업: 앱이 x5t 값의 존재에 종속되지 않도록 하세요.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="ddb5f-123">profile_info 제거</span><span class="sxs-lookup"><span data-stu-id="ddb5f-123">Removing profile_info</span></span>
<span data-ttu-id="ddb5f-124">이전에는 v2.0 끝점이 `profile_info`라고 하는 토큰 응답에 있는 base64 인코딩 JSON 개체를 반환해왔습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="ddb5f-125">요청을 다음에 전송하여 v2.0 끝점으로부터 액세스 토큰을 요청하는 경우</span><span class="sxs-lookup"><span data-stu-id="ddb5f-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="ddb5f-126">응답은 다음과 같은 JSON 개체처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-126">The response would look like the following JSON object:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="ddb5f-127">`profile_info` 값에는 표시 이름, 이름, 성, 전자 메일 주소, 식별자 및 등 앱에 서명한 사용자에 관한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="ddb5f-128">`profile_info` 은(는) 주로 토큰 캐싱과 표시 용도로 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="ddb5f-129">이제 `profile_info` 값이 제거되지만, 개발자에게 이 정보를 다소 다른 위치에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="ddb5f-130">`profile_info` 대신, v2.0 끝점이 각 토큰 응답에서 `id_token`을(를) 반환하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="ddb5f-131">profile_info에서 수신한 동일한 정보를 검색하는 id_token을 디코딩하고 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="ddb5f-132">id_token는 OpenID Connect에 지정된 대로 콘텐츠가 포함된 JSON 웹 토큰(JWT)입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="ddb5f-133">이를 수행하기 위한 코드는 매우 유사해야 합니다. 즉, 범위 내에서 JSON 개체를 액세스하기 위해 id_token 및 base64 디코딩의 중간 세그먼트(본문)를 추출하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="ddb5f-134">앞으로 2주 동안 `id_token` 또는 `profile_info`에 존재하는 사용자 정보를 검색하기 위해 앱을 코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="ddb5f-135">이러한 방식으로 변경할 때 앱은 중단 없이 `profile_info`에서 `id_token`(으)로의 전환을 원활하게 처리할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="ddb5f-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb5f-136">**작업: 앱이 `profile_info` 값의 존재에 종속되지 않도록 하세요.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="ddb5f-137">Id_token_expires_in 제거</span><span class="sxs-lookup"><span data-stu-id="ddb5f-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="ddb5f-138">`profile_info`와(과) 마찬가지로 응답에서 `id_token_expires_in` 매개 변수도 제거할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="ddb5f-139">이전에는 권한 부여 응답 또는 토큰 응답의 인스턴스에 대해 v2.0 끝점이 각 id_token 응답과 함께 `id_token_expires_in`에 대한 값을</span><span class="sxs-lookup"><span data-stu-id="ddb5f-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="ddb5f-140">반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-140">Or in a token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="ddb5f-141">`id_token_expires_in` 값은 id_token을 유효한 상태로 유지하는 시간(초)의 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="ddb5f-142">이제 `id_token_expires_in` 값을 완전히 제거하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="ddb5f-143">대신에 OpenID Connect 표준 `nbf` 및 `exp` 클레임을 사용하여 id_token의 유효성을 검사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="ddb5f-144">이러한 클레임에 대한 자세한 내용은 [v2.0 토큰 참조](active-directory-v2-tokens.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb5f-145">**작업: 앱이 `id_token_expires_in` 값의 존재에 종속되지 않도록 하세요.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="ddb5f-146">scope=openid에 의해 반환된 클레임 변경</span><span class="sxs-lookup"><span data-stu-id="ddb5f-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="ddb5f-147">이 변경은 영향력이 가장 큽니다. 실제로 v2.0 끝점을 사용하는 거의 모든 앱에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="ddb5f-148">많은 응용 프로그램은 다음과 같은 `openid` 범위를 사용하여 v2.0 끝점에 요청을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="ddb5f-149">현재 `openid` 범위에 대해 사용자가 동의한 경우, 앱은 결과 id_token의 사용자에 대해 다양한 정보를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="ddb5f-150">이러한 클레임에는 이름, 기본 설정된 사용자 이름, 전자 메일 주소, 개체 ID 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="ddb5f-151">이 업데이트에는 OpenID Connect 사양으로 보다 잘 확인하기 위해 `openid` 범위가 허용하는 앱의 액세스 정보를 변경할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="ddb5f-152">`openid` 범위는 앱이 id_token의 `sub` 클레임에 있는 사용자를 로그인시키고 해당 사용자에 대한 앱별 식별자만 수신할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="ddb5f-153">부여된 `openid` 범위만 있는 id_token의 클레임에는 개인 식별 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="ddb5f-154">예시 id_token 클레임은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-154">Example id_token claims are:</span></span>

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

<span data-ttu-id="ddb5f-155">앱에 있는 사용자의 개인 식별 정보(PII)를 가져오려면 앱은 사용자로부터 추가 권한을 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="ddb5f-156">이를 수행할 수 있는 OpenID Connect 사양의 두 가지의 새로운 범위 즉, `email` 및 `profile` 범위에 대한 지원을 도입할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="ddb5f-157">`email` 범위는 매우 간단합니다. 앱이 id_token의 `email` 클레임을 통해 사용자의 기본 전자 메일 주소에 액세스할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="ddb5f-158">`email` 클레임이 id_tokens에 항상 존재하지는 않을 것입니다. 사용자의 프로필에 사용할 수 있는 경우에만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="ddb5f-159">`profile` 범위는 앱이 사용자 이름, 기본 설정된 사용자 이름, 개체 ID 등 사용자에 관한 모든 기타 기본 정보에 액세스할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="ddb5f-160">이렇게 하면 최소한의 공개로 앱을 코딩할 수 있으며, 작업 수행에 필요한 정보를 사용자에게 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="ddb5f-161">현재 앱이 수신하고 있는 전체 사용자 정보 전체를 계속 가져오려는 경우, 권한 부여 요청에 세 가지 범위 모두를 포함시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="ddb5f-162">앱은 즉시 `email` 및 `profile` 범위 전송을 시작할 수 있으며, v2.0 끝점은 이러한 두 범위를 수락하고 필요에 따라 사용자로부터 권한 요청을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="ddb5f-163">그러나 `openid` 범위에 대한 해석 변경은 몇 주 동안 적용되지 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb5f-164">**작업: 앱이 사용자에 대한 정보를 요구하는 경우 `profile` 및 `email` 범위를 추가하세요.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="ddb5f-165">ADAL은 기본적으로 요청에 이러한 권한을 모두 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="ddb5f-166">발급자 후행 슬래시 제거</span><span class="sxs-lookup"><span data-stu-id="ddb5f-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="ddb5f-167">이전에는 v2.0 끝점의 토큰에 표시되는 발급자 값이 양식을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="ddb5f-168">이 양식에서 GUID는 토큰을 발급한 Azure AD 테넌트의 tenantId입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="ddb5f-169">이러한 변경 사항과 함께 발급자 값은</span><span class="sxs-lookup"><span data-stu-id="ddb5f-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="ddb5f-170">두 토큰과 OpenID Connect Discovery 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb5f-171">**작업: 앱이 발급자 유효성 검사 중 후행 슬래시가 있는 발급자 값과 없는 발급자 값 모두 수락하는지 확인하세요.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="ddb5f-172">변경한 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ddb5f-172">Why change?</span></span>
<span data-ttu-id="ddb5f-173">이러한 변경 사항을 도입하는 주된 목적은 OpenID Connect 표준 사양을 준수하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="ddb5f-174">OpenID Connect를 준수함으로써 Microsoft ID 서비스와 업계에서 다른 ID 서비스를 통합하는 과정에서 차이가 최소화되기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="ddb5f-175">개발자가 Microsoft의 차이점을 수용하기 위해 라이브러리를 변경하지 않고도 자신의 좋아하는 오픈 소스 인증 라이브러리를 사용할 수 있도록 하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="ddb5f-176">어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="ddb5f-176">What can you do?</span></span>
<span data-ttu-id="ddb5f-177">현재 위에서 설명한 모든 변경을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="ddb5f-178">다음은 즉시 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-178">You should immediately:</span></span>

1. <span data-ttu-id="ddb5f-179">**`x5t` 헤더 매개 변수의 모든 종속성을 제거합니다.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="ddb5f-180">**토큰 응답에서 `profile_info`에서 `id_token`으로의 전환을 적절하게 처리합니다.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="ddb5f-181">**`id_token_expires_in` 응답 매개 변수의 모든 종속성을 제거합니다.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="ddb5f-182">**앱에 기본 사용자 정보가 필요한 경우, `profile` 및 `email` 범위를 앱에 추가합니다.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="ddb5f-183">**토큰에 후행 슬래시가 있는 발급자 값과 없는 발급자 값을 모두 수락합니다.**</span><span class="sxs-lookup"><span data-stu-id="ddb5f-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="ddb5f-184">[v2.0 프로토콜 설명서](active-directory-v2-protocols.md) 에는 이미 이러한 변경 내용을 반영 되어 있기 때문에, 코드를 업데이트하는 데 참조로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="ddb5f-185">변경의 범위에 대해 추가 질문이 있으면 Twitter @AzureAD로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="ddb5f-186">프로토콜은 얼마나 자주 변경합니까?</span><span class="sxs-lookup"><span data-stu-id="ddb5f-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="ddb5f-187">이후 인증 프로토콜의 주요 변경을 예상하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="ddb5f-188">이러한 유형의 업데이트 과정을 너무 자주 거치지 않도록 의도적으로 이러한 변경 사항들을 하나의 릴리스로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="ddb5f-189">물론, 수렴형 v2.0 인증 서비스를 활용하도록 기능을 계속해서 추가할 것이지만, 이러한 변경 사항을 추가할 뿐 기존 코드를 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="ddb5f-190">마지막으로, 이번 미리보기 기간 동안 작업을 시도해주신데 대해 감사 말씀을 드립니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="ddb5f-191">지금까지 최초 도입자의 통찰력과 경험은 매우 소중했으며, 계속 의견 및 아이디어를 공유해주시기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="ddb5f-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="ddb5f-192">즐거운 코딩 작업이 되길 바랍니다!</span><span class="sxs-lookup"><span data-stu-id="ddb5f-192">Happy coding!</span></span>

<span data-ttu-id="ddb5f-193">Microsoft ID 부서</span><span class="sxs-lookup"><span data-stu-id="ddb5f-193">The Microsoft Identity Division</span></span>

