---
title: "Azure 관리-Microsoft 위협 모델링 도구-aaaSession | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="fdd64-103">보안 프레임: 세션 관리 | Articles</span><span class="sxs-lookup"><span data-stu-id="fdd64-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="fdd64-104">제품/서비스</span><span class="sxs-lookup"><span data-stu-id="fdd64-104">Product/Service</span></span> | <span data-ttu-id="fdd64-105">문서</span><span class="sxs-lookup"><span data-stu-id="fdd64-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="fdd64-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="fdd64-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="fdd64-107">Azure AD를 사용하는 경우에 ADAL 메서드를 사용하여 적절한 로그아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="fdd64-108">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="fdd64-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="fdd64-109">생성된 SaS 토큰에 대해 한정된 수명 사용</span><span class="sxs-lookup"><span data-stu-id="fdd64-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="fdd64-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="fdd64-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="fdd64-111">생성된 리소스 토큰에 대해 최소 토큰 수명 사용</span><span class="sxs-lookup"><span data-stu-id="fdd64-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="fdd64-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="fdd64-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="fdd64-113">ADFS를 사용하는 경우에 WsFederation 메서드를 사용하여 적절한 로그아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="fdd64-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="fdd64-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="fdd64-115">ID 서버를 사용하는 경우 적절한 로그아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="fdd64-116">**웹 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="fdd64-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="fdd64-117">HTTPS를 통해 사용할 수 있는 응용 프로그램은 보안 쿠키를 사용해야 함</span><span class="sxs-lookup"><span data-stu-id="fdd64-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="fdd64-118">모든 http 기반 응용 프로그램은 쿠키 정의에 대해서 http만을 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="fdd64-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="fdd64-119">ASP.NET 웹 페이지에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화</span><span class="sxs-lookup"><span data-stu-id="fdd64-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="fdd64-120">비활성 수명에 대한 세션 설정</span><span class="sxs-lookup"><span data-stu-id="fdd64-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="fdd64-121">Hello 응용 프로그램에서 적절 한 로그 아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="fdd64-122">**앱 API**</span><span class="sxs-lookup"><span data-stu-id="fdd64-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="fdd64-123">ASP.NET Web API에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화</span><span class="sxs-lookup"><span data-stu-id="fdd64-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="fdd64-124"><a id="logout-adal">Azure AD를 사용하는 경우에 ADAL 메서드를 사용하여 적절한 로그아웃 구현</a></span><span class="sxs-lookup"><span data-stu-id="fdd64-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="fdd64-125">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-125">Title</span></span>                   | <span data-ttu-id="fdd64-126">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-127">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-127">**Component**</span></span>               | <span data-ttu-id="fdd64-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdd64-128">Azure AD</span></span> | 
| <span data-ttu-id="fdd64-129">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-129">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-130">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-130">Build</span></span> |  
| <span data-ttu-id="fdd64-131">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-131">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-132">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-132">Generic</span></span> |
| <span data-ttu-id="fdd64-133">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-133">**Attributes**</span></span>              | <span data-ttu-id="fdd64-134">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-134">N/A</span></span>  |
| <span data-ttu-id="fdd64-135">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-135">**References**</span></span>              | <span data-ttu-id="fdd64-136">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-136">N/A</span></span>  |
| <span data-ttu-id="fdd64-137">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-137">**Steps**</span></span> | <span data-ttu-id="fdd64-138">Hello 로그 아웃 이벤트 처리기를 호출 해야 hello 응용 프로그램이 Azure AD에서 발급 하는 액세스 토큰을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="fdd64-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="fdd64-139">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="fdd64-140">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-140">Example</span></span>
<span data-ttu-id="fdd64-141">Session.Abandon() 메서드를 호출하여 사용자의 세션을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="fdd64-142">다음 메서드에서는 사용자 로그아웃의 보안 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="fdd64-143"><a id="finite-tokens"></a>생성된 SaS 토큰에 대해 한정된 수명 사용</span><span class="sxs-lookup"><span data-stu-id="fdd64-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="fdd64-144">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-144">Title</span></span>                   | <span data-ttu-id="fdd64-145">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-146">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-146">**Component**</span></span>               | <span data-ttu-id="fdd64-147">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="fdd64-147">IoT Device</span></span> | 
| <span data-ttu-id="fdd64-148">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-148">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-149">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-149">Build</span></span> |  
| <span data-ttu-id="fdd64-150">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-150">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-151">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-151">Generic</span></span> |
| <span data-ttu-id="fdd64-152">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-152">**Attributes**</span></span>              | <span data-ttu-id="fdd64-153">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-153">N/A</span></span>  |
| <span data-ttu-id="fdd64-154">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-154">**References**</span></span>              | <span data-ttu-id="fdd64-155">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-155">N/A</span></span>  |
| <span data-ttu-id="fdd64-156">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-156">**Steps**</span></span> | <span data-ttu-id="fdd64-157">IoT Hub tooAzure 인증에 대해 생성 된 SaS 토큰 유한한 만료 기간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="fdd64-158">Hello SaS 토큰 수명 tooa 최소 toolimit hello 양을 hello 토큰이 손상 된 경우에 재생 될 시간을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="fdd64-159"><a id="resource-tokens"></a>생성된 리소스 토큰에 대해 최소 토큰 수명 사용</span><span class="sxs-lookup"><span data-stu-id="fdd64-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="fdd64-160">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-160">Title</span></span>                   | <span data-ttu-id="fdd64-161">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-162">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-162">**Component**</span></span>               | <span data-ttu-id="fdd64-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="fdd64-163">Azure Document DB</span></span> | 
| <span data-ttu-id="fdd64-164">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-164">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-165">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-165">Build</span></span> |  
| <span data-ttu-id="fdd64-166">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-166">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-167">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-167">Generic</span></span> |
| <span data-ttu-id="fdd64-168">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-168">**Attributes**</span></span>              | <span data-ttu-id="fdd64-169">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-169">N/A</span></span>  |
| <span data-ttu-id="fdd64-170">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-170">**References**</span></span>              | <span data-ttu-id="fdd64-171">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-171">N/A</span></span>  |
| <span data-ttu-id="fdd64-172">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-172">**Steps**</span></span> | <span data-ttu-id="fdd64-173">리소스 토큰 tooa 필요한 최소값의 hello timespan을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="fdd64-174">리소스 토큰은 기본 1시간의 유효한 시간을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="fdd64-175"><a id="wsfederation-logout"></a>ADFS를 사용하는 경우에 WsFederation 메서드를 사용하여 적절한 로그아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="fdd64-176">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-176">Title</span></span>                   | <span data-ttu-id="fdd64-177">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-178">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-178">**Component**</span></span>               | <span data-ttu-id="fdd64-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="fdd64-179">ADFS</span></span> | 
| <span data-ttu-id="fdd64-180">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-180">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-181">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-181">Build</span></span> |  
| <span data-ttu-id="fdd64-182">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-182">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-183">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-183">Generic</span></span> |
| <span data-ttu-id="fdd64-184">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-184">**Attributes**</span></span>              | <span data-ttu-id="fdd64-185">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-185">N/A</span></span>  |
| <span data-ttu-id="fdd64-186">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-186">**References**</span></span>              | <span data-ttu-id="fdd64-187">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-187">N/A</span></span>  |
| <span data-ttu-id="fdd64-188">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-188">**Steps**</span></span> | <span data-ttu-id="fdd64-189">Hello 응용 프로그램 ad FS에서 발급 한 STS 토큰을 사용 하는 경우 아웃 hello 사용자 WSFederationAuthenticationModule.FederatedSignOut() 메서드 toolog hello 로그 아웃 이벤트 처리기에 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="fdd64-190">또한 hello 현재 세션 제거 되어야 할지, 및 hello 세션 토큰 값 다시 설정 하 고 있어 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-191">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="fdd64-192"><a id="proper-logout"></a>ID 서버를 사용하는 경우 적절한 로그아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="fdd64-193">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-193">Title</span></span>                   | <span data-ttu-id="fdd64-194">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-195">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-195">**Component**</span></span>               | <span data-ttu-id="fdd64-196">ID 서버</span><span class="sxs-lookup"><span data-stu-id="fdd64-196">Identity Server</span></span> | 
| <span data-ttu-id="fdd64-197">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-197">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-198">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-198">Build</span></span> |  
| <span data-ttu-id="fdd64-199">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-199">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-200">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-200">Generic</span></span> |
| <span data-ttu-id="fdd64-201">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-201">**Attributes**</span></span>              | <span data-ttu-id="fdd64-202">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-202">N/A</span></span>  |
| <span data-ttu-id="fdd64-203">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-203">**References**</span></span>              | [<span data-ttu-id="fdd64-204">IdentityServer3-페더레이션된 로그아웃</span><span class="sxs-lookup"><span data-stu-id="fdd64-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="fdd64-205">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-205">**Steps**</span></span> | <span data-ttu-id="fdd64-206">외부 id 공급자와 hello 기능 toofederate IdentityServer을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="fdd64-207">사용자가 업스트림 id 공급자에서 로그 오프을 사용 하는 hello 프로토콜에 따라 것 가능한 tooreceive 알림을 hello 사용자가 로그 아웃 하는 경우. IdentityServer toonotify도를 서명할 수 있으므로 여기에 클라이언트 hello 아웃 사용자 수 있습니다. Hello 구현 세부 사항에 대 한 hello references 섹션에 hello 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="fdd64-208"><a id="https-secure-cookies"></a>HTTPS를 통해 사용할 수 있는 응용 프로그램은 보안 쿠키를 사용해야 함</span><span class="sxs-lookup"><span data-stu-id="fdd64-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="fdd64-209">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-209">Title</span></span>                   | <span data-ttu-id="fdd64-210">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-211">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-211">**Component**</span></span>               | <span data-ttu-id="fdd64-212">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-212">Web Application</span></span> | 
| <span data-ttu-id="fdd64-213">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-213">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-214">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-214">Build</span></span> |  
| <span data-ttu-id="fdd64-215">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-215">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-216">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-216">Generic</span></span> |
| <span data-ttu-id="fdd64-217">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-217">**Attributes**</span></span>              | <span data-ttu-id="fdd64-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="fdd64-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="fdd64-219">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-219">**References**</span></span>              | <span data-ttu-id="fdd64-220">[httpCookies 요소(ASP.NET 설정 스키마)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure 속성](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="fdd64-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="fdd64-221">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-221">**Steps**</span></span> | <span data-ttu-id="fdd64-222">쿠키는 일반적으로 범위가 지정 된만 액세스할 수 있는 toohello 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="fdd64-223">안타깝게도, "도메인"의 hello 정의 HTTPS를 통해 생성 되는 쿠키는 HTTP를 통해 액세스할 수 있도록 hello 프로토콜을 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="fdd64-224">hello "보안" 특성은 쿠키를 hello toohello 브라우저만 사용 가능 해야 HTTPS를 통해 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="fdd64-225">HTTPS를 통해 설정 된 모든 쿠키 hello를 사용 하는지 확인 **보안** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="fdd64-226">hello 요구 사항 hello requireSSL 특성 tootrue를 설정 하 여 hello web.config 파일에 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="fdd64-227">Hello hello를 적용 하기 때문에 접근 방식을 선호는 **보안** 추가 코드 변경 내용을 hello 필요 toomake 없이 모든 현재 및 미래의 쿠키에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-228">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="fdd64-229">hello 설정은 HTTP 사용 되는 tooaccess hello 응용 프로그램은 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="fdd64-230">HTTP를 사용 하는 경우 tooaccess hello 응용 프로그램을 hello hello 응용 프로그램 hello 보안 특성과 hello 브라우저와 hello 쿠키 설정을 보내지 않으므로 해당 설정을 나누기 다시 toohello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="fdd64-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="fdd64-231">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-231">Title</span></span>                   | <span data-ttu-id="fdd64-232">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-233">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-233">**Component**</span></span>               | <span data-ttu-id="fdd64-234">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-234">Web Application</span></span> | 
| <span data-ttu-id="fdd64-235">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-235">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-236">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-236">Build</span></span> |  
| <span data-ttu-id="fdd64-237">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-237">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-238">웹 양식, MVC5</span><span class="sxs-lookup"><span data-stu-id="fdd64-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="fdd64-239">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-239">**Attributes**</span></span>              | <span data-ttu-id="fdd64-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="fdd64-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="fdd64-241">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-241">**References**</span></span>              | <span data-ttu-id="fdd64-242">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-242">N/A</span></span>  |
| <span data-ttu-id="fdd64-243">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-243">**Steps**</span></span> | <span data-ttu-id="fdd64-244">requireSSL tooTrue 설정 하 여 hello FedAuth 토큰의 보안 특성을 구성할 수 hello 웹 응용 프로그램은 신뢰 당사자 hello hello IdP는 ADFS 서버를 `system.identityModel.services` web.config의 섹션:</span><span class="sxs-lookup"><span data-stu-id="fdd64-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-245">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="fdd64-246"><a id="cookie-definition"></a>모든 http 기반 응용 프로그램은 쿠키 정의에 대해서 http만을 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="fdd64-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="fdd64-247">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-247">Title</span></span>                   | <span data-ttu-id="fdd64-248">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-249">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-249">**Component**</span></span>               | <span data-ttu-id="fdd64-250">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-250">Web Application</span></span> | 
| <span data-ttu-id="fdd64-251">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-251">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-252">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-252">Build</span></span> |  
| <span data-ttu-id="fdd64-253">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-253">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-254">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-254">Generic</span></span> |
| <span data-ttu-id="fdd64-255">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-255">**Attributes**</span></span>              | <span data-ttu-id="fdd64-256">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-256">N/A</span></span>  |
| <span data-ttu-id="fdd64-257">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-257">**References**</span></span>              | [<span data-ttu-id="fdd64-258">보안 쿠키 특성</span><span class="sxs-lookup"><span data-stu-id="fdd64-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="fdd64-259">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-259">**Steps**</span></span> | <span data-ttu-id="fdd64-260">toomitigate hello 정보 공개 위험을 교차 사이트 스크립팅 (XSS) 공격을 새 특성-httpOnly-도입된 toocookies가 있으며 모든 주요 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="fdd64-261">hello 특성 쿠키에 스크립트를 통해 액세스할 수 있는지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="fdd64-262">웹 응용 프로그램 HttpOnly 쿠키를 사용 하 여 hello 가능성 hello 쿠키에 포함 된 중요 한 정보가 스크립트를 통해 도난 및 tooan 공격자의 웹 사이트에 전송 될 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="fdd64-263">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-263">Example</span></span>
<span data-ttu-id="fdd64-264">쿠키를 사용 하는 모든 HTTP 기반 응용 프로그램은 HttpOnly 다음 web.config에서 구성을 구현 하 여 hello 쿠키 정의에 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="fdd64-265">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-265">Title</span></span>                   | <span data-ttu-id="fdd64-266">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-267">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-267">**Component**</span></span>               | <span data-ttu-id="fdd64-268">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-268">Web Application</span></span> | 
| <span data-ttu-id="fdd64-269">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-269">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-270">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-270">Build</span></span> |  
| <span data-ttu-id="fdd64-271">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-271">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-272">웹 양식</span><span class="sxs-lookup"><span data-stu-id="fdd64-272">Web Forms</span></span> |
| <span data-ttu-id="fdd64-273">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-273">**Attributes**</span></span>              | <span data-ttu-id="fdd64-274">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-274">N/A</span></span>  |
| <span data-ttu-id="fdd64-275">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-275">**References**</span></span>              | [<span data-ttu-id="fdd64-276">FormsAuthentication.RequireSSL 속성</span><span class="sxs-lookup"><span data-stu-id="fdd64-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="fdd64-277">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-277">**Steps**</span></span> | <span data-ttu-id="fdd64-278">hello RequireSSL 속성 값은 hello 구성 요소의 hello requireSSL 특성을 사용 하 여 ASP.NET 응용 프로그램에 대 한 hello 구성 파일에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="fdd64-279">지정할 수 있습니다 hello Web.config 파일에서 ASP.NET 응용 프로그램에 대 한 SSL (Secure Sockets Layer) hello requireSSL 특성을 설정 하 여 필요한 tooreturn hello 폼 인증 쿠키 toohello 서버 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-280">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-280">Example</span></span> 
<span data-ttu-id="fdd64-281">hello 다음 코드 예제에서는 hello requireSSL 특성 hello Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="fdd64-282">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-282">Title</span></span>                   | <span data-ttu-id="fdd64-283">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-284">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-284">**Component**</span></span>               | <span data-ttu-id="fdd64-285">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-285">Web Application</span></span> | 
| <span data-ttu-id="fdd64-286">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-286">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-287">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-287">Build</span></span> |  
| <span data-ttu-id="fdd64-288">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-288">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="fdd64-289">MVC5</span></span> |
| <span data-ttu-id="fdd64-290">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-290">**Attributes**</span></span>              | <span data-ttu-id="fdd64-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="fdd64-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="fdd64-292">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-292">**References**</span></span>              | [<span data-ttu-id="fdd64-293">WIF(Windows Identity Foundation) 구성 – 2부</span><span class="sxs-lookup"><span data-stu-id="fdd64-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="fdd64-294">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-294">**Steps**</span></span> | <span data-ttu-id="fdd64-295">tooset httpOnly 특성 FedAuth 쿠키, hideFromCsript 특성 값을 설정 해야 tooTrue 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="fdd64-296">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-296">Example</span></span>
<span data-ttu-id="fdd64-297">다음 구성은 hello 올바른 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="fdd64-298"><a id="csrf-asp"></a>ASP.NET 웹 페이지에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화</span><span class="sxs-lookup"><span data-stu-id="fdd64-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="fdd64-299">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-299">Title</span></span>                   | <span data-ttu-id="fdd64-300">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-301">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-301">**Component**</span></span>               | <span data-ttu-id="fdd64-302">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-302">Web Application</span></span> | 
| <span data-ttu-id="fdd64-303">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-303">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-304">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-304">Build</span></span> |  
| <span data-ttu-id="fdd64-305">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-305">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-306">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-306">Generic</span></span> |
| <span data-ttu-id="fdd64-307">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-307">**Attributes**</span></span>              | <span data-ttu-id="fdd64-308">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-308">N/A</span></span>  |
| <span data-ttu-id="fdd64-309">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-309">**References**</span></span>              | <span data-ttu-id="fdd64-310">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-310">N/A</span></span>  |
| <span data-ttu-id="fdd64-311">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-311">**Steps**</span></span> | <span data-ttu-id="fdd64-312">교차 사이트 요청 위조 (CSRF 또는 XSRF)는 hello 보안 컨텍스트에서 다른 사용자의 웹 사이트에서 설정 된 세션의 동작 하면 공격자가 수행할 수 있는 공격의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="fdd64-313">hello 목표 toomodify 또는 hello 대상된 웹 사이트는 세션 쿠키 tooauthenticate 받은 요청에서 단독으로 사용 하는 경우 콘텐츠를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="fdd64-314">공격자에 hello 사용자가 이미 로그인 취약 한 사이트를 다른 사용자의 브라우저 tooload 명령 사용 하 여 URL을 가져와이 취약점을 악용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="fdd64-315">여러 가지 방법으로 공격자가 toodo,와 같은 다른 웹 사이트를 호스트 하 여 하에서 리소스를 로드 hello 취약 한 서버 또는 가져오는 hello 사용자 tooclick 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="fdd64-316">hello 서버 추가 토큰 toohello 클라이언트 전송, 모든 향후 요청에서 해당 토큰 클라이언트 tooinclude hello 및 앞으로 모든 요청에 관련 된 toohello 현재 세션 등으로 토큰 포함 확인 필요 경우 hello 공격을 방지할 수 있습니다. hello AntiForgeryToken ASP.NET ViewState를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="fdd64-317">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-317">Title</span></span>                   | <span data-ttu-id="fdd64-318">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-319">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-319">**Component**</span></span>               | <span data-ttu-id="fdd64-320">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-320">Web Application</span></span> | 
| <span data-ttu-id="fdd64-321">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-321">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-322">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-322">Build</span></span> |  
| <span data-ttu-id="fdd64-323">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-323">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="fdd64-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="fdd64-325">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-325">**Attributes**</span></span>              | <span data-ttu-id="fdd64-326">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-326">N/A</span></span>  |
| <span data-ttu-id="fdd64-327">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-327">**References**</span></span>              | [<span data-ttu-id="fdd64-328">ASP.NET MVC 및 웹 페이지에서 XSRF/CSRF 방지</span><span class="sxs-lookup"><span data-stu-id="fdd64-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="fdd64-329">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-329">**Steps**</span></span> | <span data-ttu-id="fdd64-330">앤티 CSRF 및 ASP.NET MVC 폼에서 사용 하 여 hello `AntiForgeryToken` ; 축 자를 뷰에 대 한 도우미 메서드는 `Html.AntiForgeryToken()` hello 양식으로</span><span class="sxs-lookup"><span data-stu-id="fdd64-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-331">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="fdd64-332">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="fdd64-333">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-333">Example</span></span>
<span data-ttu-id="fdd64-334">Hello에 이와 Html.AntiForgeryToken() 제공 hello 방문자 쿠키 __RequestVerificationToken 위에 표시 된 hello 임의의 숨겨진된 값과 같은 값인 hello로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="fdd64-335">다음으로, 들어오는 폼 게시, toovalidate hello [ValidateAntiForgeryToken] 필터 toohello 대상 작업 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="fdd64-336">예:</span><span class="sxs-lookup"><span data-stu-id="fdd64-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="fdd64-337">다음을 확인하는 권한 부여 필터:</span><span class="sxs-lookup"><span data-stu-id="fdd64-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="fdd64-338">hello 들어오는 요청에 __RequestVerificationToken 라는 쿠키</span><span class="sxs-lookup"><span data-stu-id="fdd64-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="fdd64-339">hello 들어오는 요청에는 `Request.Form` __RequestVerificationToken 라는 항목</span><span class="sxs-lookup"><span data-stu-id="fdd64-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="fdd64-340">이러한 쿠키 및 `Request.Form` 가정 모든 값 일치가 잘, hello 요청은 정상적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="fdd64-341">하지만 그렇지 않으면 "필수 위조 방지 토큰을 제공하지 않았거나 올바르지 않습니다."라는 메시지와 함께 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="fdd64-342">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-342">Example</span></span>
<span data-ttu-id="fdd64-343">앤티 CSRF 및 AJAX: hello 폼 토큰 AJAX 요청 JSON 데이터를 HTML 양식 데이터가 아닌으로 보낼 수 있으므로 AJAX 요청에 대 한 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="fdd64-344">한 가지 해결 방법은 사용자 지정 HTTP 헤더에서 toosend hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="fdd64-345">hello 다음 코드 Razor 구문 toogenerate hello 토큰을 사용 하 고 hello 토큰 tooan AJAX 요청을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="fdd64-346">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-346">Example</span></span>
<span data-ttu-id="fdd64-347">Hello 요청을 처리할 때 hello 요청 헤더에서 hello 토큰을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="fdd64-348">다음 toovalidate hello 토큰 hello AntiForgery.Validate 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="fdd64-349">Validate 메서드 hello hello 토큰이 유효 하지 않은 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="fdd64-350">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-350">Title</span></span>                   | <span data-ttu-id="fdd64-351">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-352">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-352">**Component**</span></span>               | <span data-ttu-id="fdd64-353">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-353">Web Application</span></span> | 
| <span data-ttu-id="fdd64-354">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-354">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-355">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-355">Build</span></span> |  
| <span data-ttu-id="fdd64-356">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-356">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-357">웹 양식</span><span class="sxs-lookup"><span data-stu-id="fdd64-357">Web Forms</span></span> |
| <span data-ttu-id="fdd64-358">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-358">**Attributes**</span></span>              | <span data-ttu-id="fdd64-359">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-359">N/A</span></span>  |
| <span data-ttu-id="fdd64-360">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-360">**References**</span></span>              | [<span data-ttu-id="fdd64-361">Take 이점은의 ASP.NET 기본 제공 기능 tooFend 오프 웹 공격</span><span class="sxs-lookup"><span data-stu-id="fdd64-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="fdd64-362">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-362">**Steps**</span></span> | <span data-ttu-id="fdd64-363">각 사용자-사용자 ID에 대해 달라 지는 ViewStateUserKey tooa 임의 문자열을 설정 하 여 WebForm 기반 응용 프로그램에서 CSRF 공격을 완화할 수 있습니다 또는 더 잘 아직 세션 id입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="fdd64-364">다양한 기술적 및 사회적 원인으로 인해 세션 ID가 예측할 수 있고 시간이 초과하며 각 사용자에 따라 다르기 때문에 훨씬 더 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-365">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-365">Example</span></span>
<span data-ttu-id="fdd64-366">모든 페이지에 toohave 필요한 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="fdd64-367"><a id="inactivity-lifetime"></a>비활성 수명에 대한 세션 설정</span><span class="sxs-lookup"><span data-stu-id="fdd64-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="fdd64-368">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-368">Title</span></span>                   | <span data-ttu-id="fdd64-369">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-370">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-370">**Component**</span></span>               | <span data-ttu-id="fdd64-371">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-371">Web Application</span></span> | 
| <span data-ttu-id="fdd64-372">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-372">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-373">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-373">Build</span></span> |  
| <span data-ttu-id="fdd64-374">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-374">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-375">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-375">Generic</span></span> |
| <span data-ttu-id="fdd64-376">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-376">**Attributes**</span></span>              | <span data-ttu-id="fdd64-377">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-377">N/A</span></span>  |
| <span data-ttu-id="fdd64-378">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-378">**References**</span></span>              | <span data-ttu-id="fdd64-379">[HttpSessionState.Timeout 속성](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="fdd64-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="fdd64-380">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-380">**Steps**</span></span> | <span data-ttu-id="fdd64-381">세션 제한 시간 hello 사용자를 수행 하지 않는 모든 작업 웹 사이트 (웹 서버에 의해 정의 됨) 간격 동안 때 이벤트 발생을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="fdd64-382">서버 쪽에서 이벤트 hello hello 사용자 세션 too'invalid의 hello 상태 변경,' (예를 들어 "더 이상 사용 되지") 하 고 하도록 명령 hello 웹 서버 toodestroy (에 포함 된 모든 데이터가 삭제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="fdd64-383">hello 다음 코드 예제에서는 hello 시간 제한 세션 특성 too15 분 hello Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-384">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-384">Example</span></span>
<span data-ttu-id="fdd64-385">``\`XML 코드 <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="fdd64-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="fdd64-386">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-386">Title</span></span>                   | <span data-ttu-id="fdd64-387">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-388">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-388">**Component**</span></span>               | <span data-ttu-id="fdd64-389">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-389">Web Application</span></span> | 
| <span data-ttu-id="fdd64-390">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-390">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-391">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-391">Build</span></span> |  
| <span data-ttu-id="fdd64-392">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-392">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-393">웹 양식</span><span class="sxs-lookup"><span data-stu-id="fdd64-393">Web Forms</span></span> |
| <span data-ttu-id="fdd64-394">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-394">**Attributes**</span></span>              | <span data-ttu-id="fdd64-395">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-395">N/A</span></span>  |
| <span data-ttu-id="fdd64-396">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-396">**References**</span></span>              | <span data-ttu-id="fdd64-397">[인증(ASP.NET 설정 스키마)에 대한 양식 요소](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="fdd64-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="fdd64-398">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-398">**Steps**</span></span> | <span data-ttu-id="fdd64-399">Forms 인증 쿠키 시간 제한 too15 hello 분 설정</span><span class="sxs-lookup"><span data-stu-id="fdd64-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="fdd64-400">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-400">Example</span></span>
<span data-ttu-id="fdd64-401">``\`XML 코드 <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="fdd64-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="fdd64-402">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-402">Example</span></span>
<span data-ttu-id="fdd64-403">또한 SAML 클레임 토큰의 수명을 발급 ADFS too15 설정 해야 하는 hello hello 다음 hello ADFS 서버에서 powershell 명령을 실행 하 여 분:</span><span class="sxs-lookup"><span data-stu-id="fdd64-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="fdd64-404"><a id="proper-app-logout"></a>Hello 응용 프로그램에서 적절 한 로그 아웃 구현</span><span class="sxs-lookup"><span data-stu-id="fdd64-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="fdd64-405">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-405">Title</span></span>                   | <span data-ttu-id="fdd64-406">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-407">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-407">**Component**</span></span>               | <span data-ttu-id="fdd64-408">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fdd64-408">Web Application</span></span> | 
| <span data-ttu-id="fdd64-409">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-409">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-410">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-410">Build</span></span> |  
| <span data-ttu-id="fdd64-411">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-411">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-412">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-412">Generic</span></span> |
| <span data-ttu-id="fdd64-413">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-413">**Attributes**</span></span>              | <span data-ttu-id="fdd64-414">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-414">N/A</span></span>  |
| <span data-ttu-id="fdd64-415">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-415">**References**</span></span>              | <span data-ttu-id="fdd64-416">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-416">N/A</span></span>  |
| <span data-ttu-id="fdd64-417">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-417">**Steps**</span></span> | <span data-ttu-id="fdd64-418">사용자가 로그 아웃 단추가 적절 한 로그 아웃 hello 응용 프로그램에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="fdd64-419">로그아웃 시 응용 프로그램은 사용자의 세션을 삭제하고 인증 쿠키 값을 다시 설정하고 무효화하는 동시에 세션 쿠키 값을 다시 설정하고 무효화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="fdd64-420">또한 여러 세션 제한은 tooa 단일 사용자 id 인 경우 이러한 전체적으로 끝나야 hello 서버 쪽 제한 시간 또는 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="fdd64-421">마지막으로 로그아웃 기능을 모든 페이지에 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="fdd64-422"><a id="csrf-api"></a>ASP.NET Web API에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화</span><span class="sxs-lookup"><span data-stu-id="fdd64-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="fdd64-423">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-423">Title</span></span>                   | <span data-ttu-id="fdd64-424">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-425">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-425">**Component**</span></span>               | <span data-ttu-id="fdd64-426">Web API</span><span class="sxs-lookup"><span data-stu-id="fdd64-426">Web API</span></span> | 
| <span data-ttu-id="fdd64-427">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-427">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-428">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-428">Build</span></span> |  
| <span data-ttu-id="fdd64-429">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-429">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-430">일반</span><span class="sxs-lookup"><span data-stu-id="fdd64-430">Generic</span></span> |
| <span data-ttu-id="fdd64-431">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-431">**Attributes**</span></span>              | <span data-ttu-id="fdd64-432">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-432">N/A</span></span>  |
| <span data-ttu-id="fdd64-433">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-433">**References**</span></span>              | <span data-ttu-id="fdd64-434">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-434">N/A</span></span>  |
| <span data-ttu-id="fdd64-435">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-435">**Steps**</span></span> | <span data-ttu-id="fdd64-436">교차 사이트 요청 위조 (CSRF 또는 XSRF)는 hello 보안 컨텍스트에서 다른 사용자의 웹 사이트에서 설정 된 세션의 동작 하면 공격자가 수행할 수 있는 공격의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="fdd64-437">hello 목표 toomodify 또는 hello 대상된 웹 사이트는 세션 쿠키 tooauthenticate 받은 요청에서 단독으로 사용 하는 경우 콘텐츠를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="fdd64-438">공격자에 hello 사용자가 이미 로그인 취약 한 사이트를 다른 사용자의 브라우저 tooload 명령 사용 하 여 URL을 가져와이 취약점을 악용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="fdd64-439">여러 가지 방법으로 공격자가 toodo,와 같은 다른 웹 사이트를 호스트 하 여 하에서 리소스를 로드 hello 취약 한 서버 또는 가져오는 hello 사용자 tooclick 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="fdd64-440">hello 서버 추가 토큰 toohello 클라이언트 전송, 모든 향후 요청에서 해당 토큰 클라이언트 tooinclude hello 및 앞으로 모든 요청에 관련 된 toohello 현재 세션 등으로 토큰 포함 확인 필요 경우 hello 공격을 방지할 수 있습니다. hello AntiForgeryToken ASP.NET ViewState를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="fdd64-441">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-441">Title</span></span>                   | <span data-ttu-id="fdd64-442">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-443">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-443">**Component**</span></span>               | <span data-ttu-id="fdd64-444">Web API</span><span class="sxs-lookup"><span data-stu-id="fdd64-444">Web API</span></span> | 
| <span data-ttu-id="fdd64-445">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-445">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-446">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-446">Build</span></span> |  
| <span data-ttu-id="fdd64-447">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-447">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="fdd64-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="fdd64-449">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-449">**Attributes**</span></span>              | <span data-ttu-id="fdd64-450">해당 없음</span><span class="sxs-lookup"><span data-stu-id="fdd64-450">N/A</span></span>  |
| <span data-ttu-id="fdd64-451">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-451">**References**</span></span>              | [<span data-ttu-id="fdd64-452">ASP.NET Web API에서 CSRF(교차 사이트 요청 위조) 공격 방지</span><span class="sxs-lookup"><span data-stu-id="fdd64-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="fdd64-453">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-453">**Steps**</span></span> | <span data-ttu-id="fdd64-454">앤티 CSRF 및 AJAX: hello 폼 토큰 AJAX 요청 JSON 데이터를 HTML 양식 데이터가 아닌으로 보낼 수 있으므로 AJAX 요청에 대 한 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="fdd64-455">한 가지 해결 방법은 사용자 지정 HTTP 헤더에서 toosend hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="fdd64-456">hello 다음 코드 Razor 구문 toogenerate hello 토큰을 사용 하 고 hello 토큰 tooan AJAX 요청을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="fdd64-457">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="fdd64-458">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-458">Example</span></span>
<span data-ttu-id="fdd64-459">Hello 요청을 처리할 때 hello 요청 헤더에서 hello 토큰을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="fdd64-460">다음 toovalidate hello 토큰 hello AntiForgery.Validate 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="fdd64-461">Validate 메서드 hello hello 토큰이 유효 하지 않은 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="fdd64-462">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-462">Example</span></span>
<span data-ttu-id="fdd64-463">앤티 CSRF 및 ASP.NET MVC 양식-사용 하 여 hello 뷰의; AntiForgeryToken 도우미 메서드 예를 들어 hello 양식에 Html.AntiForgeryToken() 배치</span><span class="sxs-lookup"><span data-stu-id="fdd64-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="fdd64-464">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-464">Example</span></span>
<span data-ttu-id="fdd64-465">위의 hello 예제는 hello 다음과 같은 내용이 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="fdd64-466">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-466">Example</span></span>
<span data-ttu-id="fdd64-467">Hello에 이와 Html.AntiForgeryToken() 제공 hello 방문자 쿠키 __RequestVerificationToken 위에 표시 된 hello 임의의 숨겨진된 값과 같은 값인 hello로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="fdd64-468">다음으로, 들어오는 폼 게시, toovalidate hello [ValidateAntiForgeryToken] 필터 toohello 대상 작업 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="fdd64-469">예:</span><span class="sxs-lookup"><span data-stu-id="fdd64-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="fdd64-470">다음을 확인하는 권한 부여 필터:</span><span class="sxs-lookup"><span data-stu-id="fdd64-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="fdd64-471">hello 들어오는 요청에 __RequestVerificationToken 라는 쿠키</span><span class="sxs-lookup"><span data-stu-id="fdd64-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="fdd64-472">hello 들어오는 요청에는 `Request.Form` __RequestVerificationToken 라는 항목</span><span class="sxs-lookup"><span data-stu-id="fdd64-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="fdd64-473">이러한 쿠키 및 `Request.Form` 가정 모든 값 일치가 잘, hello 요청은 정상적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="fdd64-474">하지만 그렇지 않으면 "필수 위조 방지 토큰을 제공하지 않았거나 올바르지 않습니다."라는 메시지와 함께 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="fdd64-475">제목</span><span class="sxs-lookup"><span data-stu-id="fdd64-475">Title</span></span>                   | <span data-ttu-id="fdd64-476">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fdd64-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="fdd64-477">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fdd64-477">**Component**</span></span>               | <span data-ttu-id="fdd64-478">Web API</span><span class="sxs-lookup"><span data-stu-id="fdd64-478">Web API</span></span> | 
| <span data-ttu-id="fdd64-479">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-479">**SDL Phase**</span></span>               | <span data-ttu-id="fdd64-480">빌드</span><span class="sxs-lookup"><span data-stu-id="fdd64-480">Build</span></span> |  
| <span data-ttu-id="fdd64-481">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="fdd64-481">**Applicable Technologies**</span></span> | <span data-ttu-id="fdd64-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="fdd64-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="fdd64-483">**특성**</span><span class="sxs-lookup"><span data-stu-id="fdd64-483">**Attributes**</span></span>              | <span data-ttu-id="fdd64-484">ID 공급자 - ADFS, ID 공급자 - Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdd64-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="fdd64-485">**참조**</span><span class="sxs-lookup"><span data-stu-id="fdd64-485">**References**</span></span>              | [<span data-ttu-id="fdd64-486">개별 계정을 사용하는 Web API 및 ASP.NET Web API 2.2에서 로컬 로그인 보호</span><span class="sxs-lookup"><span data-stu-id="fdd64-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="fdd64-487">**단계**</span><span class="sxs-lookup"><span data-stu-id="fdd64-487">**Steps**</span></span> | <span data-ttu-id="fdd64-488">웹 API hello 보안이 설정 된 OAuth 2.0을 사용 하는 경우 다음 그에서는 전달자 토큰에서 권한 부여 요청 헤더 및 부여 액세스 toohello 요청 hello 토큰이 유효한 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="fdd64-489">브라우저는 쿠키를 기반으로 인증과 달리 hello 전달자 토큰 toorequests를 연결 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fdd64-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="fdd64-490">hello 클라이언트 해야 tooexplicitly 요청 hello 전달자 토큰 hello 요청 헤더에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="fdd64-491">따라서 ASP.NET Web API가 OAuth 2.0을 사용하여 보호되는 경우 전달자 토큰은 CSRF 공격에 대한 방어로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="fdd64-492">Hello MVC 부분의 hello 응용 프로그램에서 폼 인증 (즉, 사용 하 여 쿠키)를 사용 하는 경우 위조 방지 토큰이 hello MVC 웹 응용 프로그램에서 사용 하는 toobe note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fdd64-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="fdd64-493">예제</span><span class="sxs-lookup"><span data-stu-id="fdd64-493">Example</span></span>
<span data-ttu-id="fdd64-494">hello 웹 API에 toobe toorely 정보를 쿠키 아니라 전달자 토큰에만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd64-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="fdd64-495">구성에 따라 hello 하 여 수행할 수 있습니다 `WebApiConfig.Register` 메서드: ' ' C 형 코드 구성 합니다. SuppressDefaultHostAuthentication(); 구성 합니다. (새 HostAuthenticationFilter(OAuthDefaults.AuthenticationType)); Filters.Add</span><span class="sxs-lookup"><span data-stu-id="fdd64-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
