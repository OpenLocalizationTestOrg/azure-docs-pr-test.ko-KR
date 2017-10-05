---
title: "CORS에서 Azure CDN 사용 | Microsoft Docs"
description: "CORS(크로스-원본 자원 공유)와 함께 CDN(콘텐츠 배달 네트워크)을 사용하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="fe705-103">CORS에서 Azure CDN 사용</span><span class="sxs-lookup"><span data-stu-id="fe705-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="fe705-104">CORS의 정의</span><span class="sxs-lookup"><span data-stu-id="fe705-104">What is CORS?</span></span>
<span data-ttu-id="fe705-105">CORS(크로스 원본 자원 공유)는 특정 도메인에서 실행되는 웹 응용 프로그램이 다른 도메인의 자원에 액세스할 수 있도록 하는 HTTP 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="fe705-106">사이트 간 스크립팅 공격 가능성을 줄이기 위해 모든 최신 웹 브라우저는 [동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy)이라는 보안 제한을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="fe705-107">이 경우 웹 페이지는 다른 도메인의 API를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="fe705-108">CORS는 한 도메인(원본 도메인)에서 다른 도메인의 API를 호출할 수 있는 안전한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="fe705-109">작동 방법</span><span class="sxs-lookup"><span data-stu-id="fe705-109">How it works</span></span>
<span data-ttu-id="fe705-110">CORS 요청에는 *간단한 요청*과 *복잡한 요청*의 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="fe705-111">간단한 요청:</span><span class="sxs-lookup"><span data-stu-id="fe705-111">For simple requests:</span></span>

1. <span data-ttu-id="fe705-112">브라우저는 추가 **원본** HTTP 요청 헤더를 포함하여 CORS 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="fe705-113">이 헤더의 값은 부모 페이지를 제공한 원본입니다. 이 값은 *프로토콜* *도메인* 및 *포트*로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="fe705-114">https://www.contoso.com의 페이지가 fabrikam.com 원본의 사용자 데이터에 액세스하려고 하면 다음 요청 헤더가 fabrikam.com으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="fe705-115">서버는 다음으로 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="fe705-116">허용되는 원본 사이트를 나타내는 응답의 **Access-Control-Allow-Origin** 헤더</span><span class="sxs-lookup"><span data-stu-id="fe705-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="fe705-117">예:</span><span class="sxs-lookup"><span data-stu-id="fe705-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="fe705-118">서버가 원본 헤더를 확인한 후 교차 원본 요청을 허용하지 않으면 403과 같은 HTTP 오류 코드 표시</span><span class="sxs-lookup"><span data-stu-id="fe705-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="fe705-119">모든 원본을 허용하는 와일드카드를 사용한 **Access-Control-Allow-Origin** 헤더</span><span class="sxs-lookup"><span data-stu-id="fe705-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="fe705-120">복잡한 요청:</span><span class="sxs-lookup"><span data-stu-id="fe705-120">For complex requests:</span></span>

<span data-ttu-id="fe705-121">복잡한 요청은 실제 CORS 요청을 전송하기 전에 브라우저가 *실행 전 요청*(즉, 예비 프로브)을 전송해야 하는 CORS 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="fe705-122">실행 전 요청은 원래 CORS 요청을 진행할 수 있고 동일한 URL에 대한 `OPTIONS` 요청인 경우에 서버 승인을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="fe705-123">CORS 흐름 및 일반적인 문제에 대한 자세한 내용은 [REST API에 대한 CORS 가이드](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe705-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="fe705-124">와일드카드 또는 단일 원본 시나리오</span><span class="sxs-lookup"><span data-stu-id="fe705-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="fe705-125">Azure CDN의 CORS는 **Access-Control-Allow-Origin** 헤더가 와일드카드(*) 또는 단일 원본으로 설정될 때 추가 구성 없이 자동으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="fe705-126">CDN은 첫 번째 응답을 캐시하며 후속 요청은 동일한 헤더를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="fe705-127">원본에 대해 설정된 CORS 이전에 CDN에 대해 이미 요청이 수행된 경우 끝점 콘텐츠의 콘텐츠를 제거하여 **Access-Control-Allow-Origin** 헤더가 있는 콘텐츠를 다시 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="fe705-128">여러 원본 시나리오</span><span class="sxs-lookup"><span data-stu-id="fe705-128">Multiple origin scenarios</span></span>
<span data-ttu-id="fe705-129">특정 목록의 원본이 CORS에 대해 허용되도록 해야 할 경우 문제가 좀 더 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="fe705-130">CDN이 첫 번째 CORS 원본에 대해 **Access-Control-Allow-Origin** 헤더를 캐시할 때 이러한 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="fe705-131">다른 CORS 원본이 후속 요청을 수행하면 CDN은 캐시된 **Access-Control-Allow-Origin** 를 제공하며 이 경우 일치하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="fe705-132">이를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="fe705-133">Verizon의 Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="fe705-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="fe705-134">이 기능을 사용하도록 설정하는 가장 좋은 방법은 일부 고급 기능을 제공하는 **Verizon의 Azure CDN Premium**을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="fe705-135">요청의 [Origin](cdn-rules-engine.md) 헤더를 확인하는 **규칙을 만들어야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="fe705-136">유효한 원본인 경우 규칙은 요청에 제공된 원본을 사용하여 **Access-Control-Allow-Origin** 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="fe705-137">**Origin** 헤더에 지정된 원본이 허용되지 않을 경우 규칙은 **Access-Control-Allow-Origin** 헤더를 생략하며 이로 인해 브라우저가 요청을 거부하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="fe705-138">규칙 엔진을 사용하여 이러한 작업을 수행하는 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="fe705-139">두 경우 모두 파일 원본 서버의 **Access-Control-Allow-Origin** 헤더가 완전히 무시되고 CDN의 규칙 엔진이 허용되는 CORS 원본을 완전하게 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="fe705-140">유효한 모든 원본을 포함하는 단일 정규식</span><span class="sxs-lookup"><span data-stu-id="fe705-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="fe705-141">이 경우 허용하려는 모든 원본을 포함하는 정규식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="fe705-142">**Verizon의 Azure CDN** 은 [Perl 호환 정규식](http://pcre.org/) 을 정규식에 대한 엔진으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="fe705-143">[Regular Expressions 101](https://regex101.com/) 과 같은 도구를 사용하여 정규식이 유효한지 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="fe705-144">"/" 문자는 정규식에서 유효하며 이스케이프할 필요가 없지만 일부 정규식 유효성 검사기에서는 이 문자의 이스케이프를 모범 사례로 간주하고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="fe705-145">정규식이 일치하는 경우 규칙은 원본의 **Access-Control-Allow-Origin** 헤더(있는 경우)를 요청을 전송한 원본으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="fe705-146">**Access-Control-Allow-Methods**와 같은 CORS 헤더를 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![정규식을 사용하는 규칙 예제](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="fe705-148">각 원본에 대한 요청 헤더 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-148">Request header rule for each origin.</span></span>
<span data-ttu-id="fe705-149">정규식을 사용하는 대신, **요청 헤더 와일드카드** [일치 조건](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1)을 사용하여 허용하려는 각 원본에 대해 별도의 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="fe705-150">정규식 방법을 사용할 때처럼 규칙 엔진은 단독으로 CORS 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![정규식을 사용하지 않는 규칙 예제](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="fe705-152">위 예제에서 와일드카드 문자 *가 사용되었으므로 규칙 엔진은 HTTP 및 HTTPS를 둘 다 일치 항목으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="fe705-153">Azure CDN 표준</span><span class="sxs-lookup"><span data-stu-id="fe705-153">Azure CDN Standard</span></span>
<span data-ttu-id="fe705-154">Azure CDN 표준 프로필에서 와일드카드 원본을 사용하지 않고 여러 원본에 대해 허용되는 유일한 메커니즘은 [쿼리 문자열 캐싱](cdn-query-string.md)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="fe705-155">CDN 끝점에 대해 쿼리 문자열 설정을 사용하도록 지정하고 허용된 각 도메인의 요청에 대해 고유한 쿼리 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="fe705-156">이렇게 하면 CDN은 고유한 각 쿼리 문자열에 대해 별도의 개체를 캐싱합니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="fe705-157">그렇지만 이 방법은 동일한 파일의 여러 복사본이 CDN에 캐시되므로 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe705-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

