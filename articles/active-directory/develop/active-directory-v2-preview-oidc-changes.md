---
title: "Azure AD toohello v2.0 끝점 aaaChanges | Microsoft Docs"
description: "Toohello 앱 모델 v2.0 공개 미리 보기 프로토콜 수행 된 변경 내용에 대 한 설명"
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
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="a92f5-103">중요 한 업데이트 toohello v 2.0 인증 프로토콜</span><span class="sxs-lookup"><span data-stu-id="a92f5-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="a92f5-104">개발자들은 주목하세요!</span><span class="sxs-lookup"><span data-stu-id="a92f5-104">Attention developers!</span></span> <span data-ttu-id="a92f5-105">Hello를 통해 다음 2 주, 수행할 예정 몇 가지 업데이트 tooour v 2.0 인증 프로토콜 집합 의미할 수 있습니다. 주요 우리의 미리 보기 기간 중 작성 한 모든 앱에 대 한 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="a92f5-106">어떤 것이 영향을 받습니까?</span><span class="sxs-lookup"><span data-stu-id="a92f5-106">Who does this affect?</span></span>
<span data-ttu-id="a92f5-107">인증 끝점 수렴 되었습니다 toouse hello v2.0 기록 된 모든 앱</span><span class="sxs-lookup"><span data-stu-id="a92f5-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="a92f5-108">Hello v2.0 끝점에 대 한 자세한 내용은 있습니다 [여기](active-directory-appmodel-v2-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="a92f5-109">우리의 OAuth 또는 OpenID Connect 웹 middlewares 중 하나를 사용 하 여 직접 toohello v 2.0 프로토콜을 코딩 하 여 hello v2.0 끝점을 사용 하는 응용 프로그램 작성 한 또는 다른 3rd 파티 라이브러리 tooperform 인증을 사용 해야 하는 경우 프로젝트 및 확인 tootest 준비 필요한 경우 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="a92f5-110">어떤 것이 영향을 받지 않습니까?</span><span class="sxs-lookup"><span data-stu-id="a92f5-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="a92f5-111">Hello 프로덕션 Azure AD 인증 끝점에 대해 기록 된 모든 앱</span><span class="sxs-lookup"><span data-stu-id="a92f5-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="a92f5-112">이 프로토콜은 확정되었으며 어떠한 변경도 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="a92f5-113">또한 경우 앱 **만** 우리의 ADAL 라이브러리 tooperform 인증을 사용 하 여 toochange 아무 것도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="a92f5-114">ADAL은 hello 변경 된 내용에서 앱을 차폐 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="a92f5-115">Hello 변경이 합니까?</span><span class="sxs-lookup"><span data-stu-id="a92f5-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="a92f5-116">JWT 헤더에서 hello x5t 값 제거</span><span class="sxs-lookup"><span data-stu-id="a92f5-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="a92f5-117">hello v2.0 끝점이 사용 JWT 토큰을 광범위 하 게 hello 토큰에 대 한 관련 메타 데이터가 있는 헤더 매개 변수 섹션을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="a92f5-118">현재이 Jwt 중 하나의 hello 헤더를 디코딩할 다음과 같이 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="a92f5-119">Hello OpenID Connect 메타 데이터 끝점에서 검색 된 대로 hello "x5t" 및 "kid" 속성이 모두 hello 공개 키를 식별 하는 위치를 사용 하는 toovalidate hello 토큰의 서명에 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="a92f5-120">여기 진행 중인 hello 변경은 tooremove "x5t" hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="a92f5-121">동일한 메커니즘 toovalidate 토큰에 있지만 사용 해야 hello "kid" 속성 tooretrieve hello 올바른 공개 키, OpenID Connect 프로토콜에 지정 된 hello로 toouse hello를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a92f5-122">**작업: 앱 hello hello x5t 값이 있는지 여부에 종속 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="a92f5-123">profile_info 제거</span><span class="sxs-lookup"><span data-stu-id="a92f5-123">Removing profile_info</span></span>
<span data-ttu-id="a92f5-124">이전에 hello v2.0 끝점에 되었습니다 반환 base64 인코딩된 JSON 개체로 호출 하는 토큰 응답에 `profile_info`합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="a92f5-125">요청을 전송 하 여 hello v2.0 끝점에서 액세스 토큰을 요청:</span><span class="sxs-lookup"><span data-stu-id="a92f5-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="a92f5-126">hello 응답은 JSON 개체를 수행 하는 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="a92f5-127">hello `profile_info` hello 사용자 hello 앱의 표시 이름, 이름, 성, 전자 메일 주소, 식별자 및 등을 로그인에 대 한 정보가 포함 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="a92f5-128">기본적으로, hello `profile_info` 토큰 캐싱에 사용 된 및 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="a92f5-129">이제 hello 제거 `profile_info` 값-하지만 걱정 하지 마십시오 약간 다른 위치에이 정보 toodevelopers를 제공 하 고 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="a92f5-130">대신 `profile_info`, hello v2.0 끝점은 이제 반환는 `id_token` 각 토큰 응답에:</span><span class="sxs-lookup"><span data-stu-id="a92f5-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="a92f5-131">디코딩하고 hello id_token를 구문 분석할 수 있습니다 tooretrieve hello profile_info에서 받은 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="a92f5-132">hello id_token JWT JSON 웹 토큰 (), OpenID Connect로 지정 된 내용으로입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="a92f5-133">hello 이렇게 하는 것에 대 한 코드와 매우 유사 이며, 하기만 tooextract hello 중간 세그먼트 (hello 본문) hello id_token 및 base64 디코딩해야 내 tooaccess hello JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="a92f5-134">Hello를 통해 다음 2 주, 코드를 작성 해야 앱 tooretrieve hello 사용자 정보가 두 hello에서 `id_token` 또는 `profile_info`; 존재 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="a92f5-135">이런 방식으로 hello 변경 될 때 앱에서 hello 전환을 처리할 원활 하 게 수 `profile_info` 너무`id_token` 중단 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a92f5-136">**작업: 응용 프로그램의 hello hello 존재 여부에 종속 되지 않는 있는지 확인 `profile_info` 값입니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="a92f5-137">Id_token_expires_in 제거</span><span class="sxs-lookup"><span data-stu-id="a92f5-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="a92f5-138">비슷한 너무`profile_info`, hello 제거도 `id_token_expires_in` 응답에서 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="a92f5-139">Hello v2.0 끝점 반환에 대 한 값 이전에 `id_token_expires_in` authorize 응답의 예를 들어 각 id_token 응답과 함께:</span><span class="sxs-lookup"><span data-stu-id="a92f5-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="a92f5-140">반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-140">Or in a token response:</span></span>

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

<span data-ttu-id="a92f5-141">hello `id_token_expires_in` 값은 hello 수가 hello id_token은에 대 한 유효한 상태로 유지 하는 시간 (초) 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="a92f5-142">Hello 제거 이제 `id_token_expires_in` 완전히 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="a92f5-143">대신, hello OpenID Connect 표준을 사용할 수 있습니다 `nbf` 및 `exp` 는 id_token의 tooexamine hello 유효성 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="a92f5-144">Hello 참조 [v2.0 토큰 참조](active-directory-v2-tokens.md) 이러한 클레임에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a92f5-145">**작업: 응용 프로그램의 hello hello 존재 여부에 종속 되지 않는 있는지 확인 `id_token_expires_in` 값입니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="a92f5-146">범위에서 반환 된 hello 클레임 변경 openid =</span><span class="sxs-lookup"><span data-stu-id="a92f5-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="a92f5-147">이 변경 됩니다. 가장 중요 한 – hello 실제로으로 hello v2.0 끝점을 사용 하는 거의 모든 앱에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="a92f5-148">Hello를 사용 하 여 많은 응용 프로그램이 송신 요청 toohello v2.0 끝점 `openid` 같은 범위:</span><span class="sxs-lookup"><span data-stu-id="a92f5-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="a92f5-149">Hello 사용자 hello에 대 한 동의 허용 하는 경우 현재 `openid` 범위 앱 다양 한 hello 사용자에 대 한 정보 id_token으로 인해 발생 하는 hello에 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="a92f5-150">이러한 클레임에는 이름, 기본 설정된 사용자 이름, 전자 메일 주소, 개체 ID 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="a92f5-151">이 업데이트에서 변경 하 고 hello 정보는 hello `openid` 범위 hello 사양 OpenID Connect로 toobetter comform에 응용 프로그램 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="a92f5-152">hello `openid` 범위만을 통해 앱 toosign hello 사용자가 되며 hello 사용자에 대 한 응용 프로그램별 식별자 hello에 수신 `sub` hello id_token의 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="a92f5-153">id_token의 클레임만 hello로 hello `openid` 부여 범위 개인 식별 정보 보내게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="a92f5-154">예시 id_token 클레임은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="a92f5-155">Hello 사용자에 대 한 응용 프로그램에서 tooobtain 개인 식별이 가능한 정보 (PII)를 원하는 경우 응용 프로그램에 hello 사용자 로부터 toorequest 추가 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="a92f5-156">도입 새 범위 두에 대 한 지원을 hello OpenID Connect 사양-에서 hello `email` 및 `profile` 수 있게 해 주는 toodo 하므로 범위 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="a92f5-157">hello `email` 범위는 매우 단순 – hello 통해 응용 프로그램 액세스 toohello 사용자 기본 전자 메일 주소를 허용 `email` hello id_token에 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="a92f5-158">해당 hello 참고 `email` 클레임 항상 누락 될 id_tokens에-만 포함 됩니다 hello 사용자의 프로필에 사용할 수 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="a92f5-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="a92f5-159">hello `profile` ID, 개체 범위는 응용 프로그램 액세스 tooall hello 사용자-해당 이름, 기본 사용자 이름에 대 한 다른 기본 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="a92f5-160">이렇게 하면 toocode 최소 공개 방식-앱의 정보는 앱에 필요한 toodo 작업 집합에만 hello에 대 한 hello 사용자를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="a92f5-161">Hello 전체 집합이 현재 응용 프로그램을 수신 하는 사용자 정보를 가져오는 toocontinue를 원하는 경우에 권한 부여 요청에서 모든 세 가지 범위를 포함 해야:</span><span class="sxs-lookup"><span data-stu-id="a92f5-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="a92f5-162">Hello 보내는 응용 프로그램을 시작할 수 `email` 및 `profile` 범위를 즉시 인과 hello v2.0 끝점은 이러한 두 범위를 수락 하 고 필요에 따라 사용자 로부터 권한 요청을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="a92f5-163">Hello hello의 hello 해석에 변경 하는 반면 `openid` 범위 내용이 적용 되지 것입니다 몇 주 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a92f5-164">**작업: hello 추가 `profile` 및 `email` 앱 hello 사용자에 대 한 정보를 요구 하는 경우의 범위가 지정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="a92f5-165">ADAL은 기본적으로 요청에 이러한 권한을 모두 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="a92f5-166">Hello 발급자 후행 슬래시를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="a92f5-167">이전에 hello 발급자 값 hello v2.0 끝점에서 토큰에 표시 되는 데 걸린 hello 양식</span><span class="sxs-lookup"><span data-stu-id="a92f5-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="a92f5-168">여기서 hello guid hello 토큰을 발급 한 hello Azure AD 테 넌 트의 tenantId hello 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="a92f5-169">이러한 변경 내용으로 hello 발급자 값은</span><span class="sxs-lookup"><span data-stu-id="a92f5-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="a92f5-170">hello OpenID Connect 검색 문서 및 두 토큰에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a92f5-171">**작업: 앱 발급자 유효성 검사 중 hello 발급자 값 모두와 사용 하지 않는 끝에 슬래시를 수락 하 고 있는지 확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="a92f5-172">변경한 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a92f5-172">Why change?</span></span>
<span data-ttu-id="a92f5-173">이러한 변경 내용을 도입 하는 데 기본 동기 hello toobe hello OpenID Connect 표준 사양 준수입니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="a92f5-174">OpenID Connect 규격 됨으로써 toominimize 다른 id 서비스 hello 업계의 Microsoft id 서비스와 통합 차이점 하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="a92f5-175">원하는 tooenable 개발자 toouse 해당 즐겨 찾는 오픈 소스 인증 라이브러리 tooalter hello 라이브러리 tooaccommodate Microsoft 차이 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="a92f5-176">어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="a92f5-176">What can you do?</span></span>
<span data-ttu-id="a92f5-177">현재로 서 모든 위에서 설명한 hello 변경 하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="a92f5-178">다음은 즉시 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-178">You should immediately:</span></span>

1. <span data-ttu-id="a92f5-179">**Hello에서 모든 종속성을 제거 `x5t` header 매개 변수입니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="a92f5-180">**hello 전환을 정상적으로 처리할 `profile_info` 너무`id_token` 토큰 응답에 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="a92f5-181">**Hello에서 모든 종속성을 제거 `id_token_expires_in` 응답 매개 변수입니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="a92f5-182">**Hello 추가 `profile` 및 `email` 범위 tooyour 앱 응용 프로그램에 기본 사용자 정보가 필요한 경우.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="a92f5-183">**토큰에 후행 슬래시가 있는 발급자 값과 없는 발급자 값을 모두 수락합니다.**</span><span class="sxs-lookup"><span data-stu-id="a92f5-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="a92f5-184">우리의 [v2.0 프로토콜 설명서](active-directory-v2-protocols.md) 는 이미 사용 되었으므로 업데이트 tooreflect 이러한 변경 내용을 코드를 업데이트 하는 데 대 한 참조로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="a92f5-185">Hello hello 변경 범위에 추가 질문이 있으면 언제 라도 무료 tooreach 아웃에서 Twitter에서 toous @AzureAD합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="a92f5-186">프로토콜은 얼마나 자주 변경합니까?</span><span class="sxs-lookup"><span data-stu-id="a92f5-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="a92f5-187">추가 주요 toohello 인증 프로토콜을 변경 하지 않는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="a92f5-188">의도적으로이 유형의 업데이트 프로세스를 통해 toogo 언제 든 지 곧 않아도 되도록 한 릴리스에 이러한 변경 내용을 번들로 म 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="a92f5-189">Tooadd 기능 toohello 계속 것 물론, v2.0 인증 서비스를 이용할 수 있는 수렴 형 않지만 해당 변경 내용을 누적 및 기존 코드를 중단 하지 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="a92f5-190">마지막으로, toosay 주셔서 hello 미리 보기 기간 동안 작업을 시도해 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="a92f5-191">hello insights 및 우리의 조기 채택자의 경험 되지 않은 귀중 한 지금까지 하 고 계속 해 서 tooshare 의견과 아이디어 하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a92f5-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="a92f5-192">즐거운 코딩 작업이 되길 바랍니다!</span><span class="sxs-lookup"><span data-stu-id="a92f5-192">Happy coding!</span></span>

<span data-ttu-id="a92f5-193">Microsoft Identity 나누기 hello</span><span class="sxs-lookup"><span data-stu-id="a92f5-193">hello Microsoft Identity Division</span></span>

