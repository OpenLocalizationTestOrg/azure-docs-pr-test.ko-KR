---
title: "CORS와 Azure CDN aaaUsing | Microsoft Docs"
description: "Toouse Azure 콘텐츠 배달 네트워크 (CDN) toowith 크로스-원본 자원 공유 (CORS) hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="a3df1-103">CORS에서 Azure CDN 사용</span><span class="sxs-lookup"><span data-stu-id="a3df1-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="a3df1-104">CORS의 정의</span><span class="sxs-lookup"><span data-stu-id="a3df1-104">What is CORS?</span></span>
<span data-ttu-id="a3df1-105">CORS (원본 자원 공유 교차)은 다른 도메인에 있는 한 도메인 tooaccess 리소스를 실행 하는 웹 응용 프로그램을 활성화 하는 HTTP 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="a3df1-106">순서 tooreduce hello 교차 사이트 스크립팅 공격의 가능성을 모든 최신 웹 브라우저는 보안 제한을 구현 [동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="a3df1-107">이 경우 웹 페이지는 다른 도메인의 API를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="a3df1-108">CORS는 안전 하 게 tooallow 한 원본 (원본 도메인 hello) toocall Api 다른 원본에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a3df1-109">작동 방법</span><span class="sxs-lookup"><span data-stu-id="a3df1-109">How it works</span></span>
<span data-ttu-id="a3df1-110">CORS 요청에는 *간단한 요청*과 *복잡한 요청*의 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="a3df1-111">간단한 요청:</span><span class="sxs-lookup"><span data-stu-id="a3df1-111">For simple requests:</span></span>

1. <span data-ttu-id="a3df1-112">추가 함께 hello CORS 요청을 전송 하는 hello 브라우저 **원점** HTTP 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="a3df1-113">이 헤더의 hello 값은 hello 부모 페이지의 hello 조합으로 정의 된 서비스는 hello 원점 *프로토콜을* *도메인* 및 *포트입니다.*</span><span class="sxs-lookup"><span data-stu-id="a3df1-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="a3df1-114">Https://www.contoso.com에서 페이지를 시도할 때 tooaccess hello fabrikam.com 원점에 대 한 사용자의 데이터, 요청 헤더 뒤에 오는 hello 보낼 toofabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="a3df1-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="a3df1-115">hello 서버 hello 다음 중 하나를 사용 하 여 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="a3df1-116">허용되는 원본 사이트를 나타내는 응답의 **Access-Control-Allow-Origin** 헤더</span><span class="sxs-lookup"><span data-stu-id="a3df1-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="a3df1-117">예:</span><span class="sxs-lookup"><span data-stu-id="a3df1-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="a3df1-118">Hello 서버 hello 원본 헤더를 확인 한 후 hello 크로스-원본 요청을 허용 하지 않는 경우 HTTP 오류 코드 403 등</span><span class="sxs-lookup"><span data-stu-id="a3df1-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="a3df1-119">모든 원본을 허용하는 와일드카드를 사용한 **Access-Control-Allow-Origin** 헤더</span><span class="sxs-lookup"><span data-stu-id="a3df1-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="a3df1-120">복잡한 요청:</span><span class="sxs-lookup"><span data-stu-id="a3df1-120">For complex requests:</span></span>

<span data-ttu-id="a3df1-121">복잡 한 요청은 CORS 요청 여기서 hello 브라우저는 필요한 toosend는 *실행 전 요청* (즉, 예비 프로브) hello 실제 CORS 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="a3df1-122">hello 실행 전 요청 hello 서버 사용 권한 인지 묻고 hello 원래 CORS 요청을 진행할 수는 `OPTIONS` toohello 요청 동일한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="a3df1-123">CORS 흐름 및 일반적인 문제에 대 한 자세한 내용은 hello 볼 [tooCORS REST Api에 대 한 가이드](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="a3df1-124">와일드카드 또는 단일 원본 시나리오</span><span class="sxs-lookup"><span data-stu-id="a3df1-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="a3df1-125">Azure CDN에 CORS 때 hello 추가 구성 없이 자동으로 작동 합니다 **액세스 제어-허용-원본** toowildcard (*) 또는 단일 원본을 헤더가 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="a3df1-126">hello CDN가 hello 첫 번째 응답을 캐시 하 고 후속 요청은 hello를 사용 하는 동일한 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="a3df1-127">요청이 이미 수행한 toohello CDN 이전 tooCORS 원본 hello에 설정 되는 경우 toopurge 콘텐츠 끝점 콘텐츠 tooreload hello에 hello를 사용 하 여 콘텐츠 **액세스 제어-허용-원본** 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="a3df1-128">여러 원본 시나리오</span><span class="sxs-lookup"><span data-stu-id="a3df1-128">Multiple origin scenarios</span></span>
<span data-ttu-id="a3df1-129">CORS에 대해 허용 된 원본 toobe의 특정 목록 tooallow 필요한 상황이 좀 더 복잡해 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="a3df1-130">hello CDN 캐시 hello hello 문제가 발생 **액세스 제어-허용-원본** hello 첫 번째 CORS 원점에 대 한 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="a3df1-131">Hello CDN 캐시 hello 사용 될 다른 CORS 시작 후속 요청을 하면 **액세스 제어-허용-원본** 헤더와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="a3df1-132">있는 경우 여러 가지 방법으로 toocorrect이</span><span class="sxs-lookup"><span data-stu-id="a3df1-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="a3df1-133">Verizon의 Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="a3df1-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="a3df1-134">가장 좋은 방법은 tooenable hello toouse 이것이 **Verizon에서 Azure CDN Premium**, 일부를 노출 하는 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="a3df1-135">너무 해야[규칙을 만들](cdn-rules-engine.md) toocheck hello **원점** hello 요청의 헤더에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="a3df1-136">사용자 규칙은 hello 설정 유효한 원점 이면 **액세스 제어-허용-원본** hello 원점 hello 요청에 제공 된 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="a3df1-137">Hello 원점 hello에 지정 된 경우 **원점** 헤더 허용 되지 않음, 규칙 hello를 생략 해야 **액세스 제어-허용-원본** 헤더 hello 브라우저 tooreject hello 요청 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="a3df1-138">있는 경우 두 가지 방법으로 toodo이 hello 규칙 엔진</span><span class="sxs-lookup"><span data-stu-id="a3df1-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="a3df1-139">두 경우 모두 hello **액세스 제어-허용-원본** hello 파일의 원본 서버에서 헤더는 무시 됩니다 완전히, CORS 원본을 허용 하는 hello hello CDN 규칙 엔진에 완전히 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="a3df1-140">유효한 모든 원본을 포함하는 단일 정규식</span><span class="sxs-lookup"><span data-stu-id="a3df1-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="a3df1-141">이 경우에 만들게 hello 출처를 모두 포함 하는 정규식 tooallow 원하는:</span><span class="sxs-lookup"><span data-stu-id="a3df1-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="a3df1-142">**Verizon의 Azure CDN** 은 [Perl 호환 정규식](http://pcre.org/) 을 정규식에 대한 엔진으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="a3df1-143">와 같은 도구를 사용할 수 있습니다 [일반 식 101](https://regex101.com/) toovalidate 정규식입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="a3df1-144">Hello "/" 문자는 정규식의 올바른지, 그리고 이스케이프 toobe 필요 하지 않습니다, 그리고 해당 문자를 이스케이프 처리 가장 좋은 방법은 간주 되 고 일부 regex 유효성 검사기에서 예상 하는 반면 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="a3df1-145">Hello 정규식과 일치 하는 경우 규칙이 hello 대체 **액세스 제어-허용-원본** hello 요청을 보낸 hello 원점 함께 hello 원본에서 헤더 (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="a3df1-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="a3df1-146">**Access-Control-Allow-Methods**와 같은 CORS 헤더를 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![정규식을 사용하는 규칙 예제](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="a3df1-148">각 원본에 대한 요청 헤더 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-148">Request header rule for each origin.</span></span>
<span data-ttu-id="a3df1-149">대신 정규식을 만들 수 있습니다 대신 별도 각 원본에 대 한 규칙 tooallow hello를 사용 하 여 원하는 **요청 헤더 와일드 카드** [조건과 일치](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="a3df1-150">Hello 정규식 메서드를 사용 하 hello 규칙 집합 hello CORS 헤더 단독 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![정규식을 사용하지 않는 규칙 예제](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="a3df1-152">위의 hello 예제에서 사용 하 여 hello 와일드 카드 문자를 hello * hello 규칙 엔진이 toomatch 지시 HTTP 및 HTTPS입니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="a3df1-153">Azure CDN 표준</span><span class="sxs-lookup"><span data-stu-id="a3df1-153">Azure CDN Standard</span></span>
<span data-ttu-id="a3df1-154">Azure CDN 표준 프로필에서 hello hello 와일드 카드 origin 사용 하지 않고도 여러 출처에 대 한 메커니즘 tooallow toouse 파일인 hello [쿼리 문자열 캐싱](cdn-query-string.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="a3df1-155">Tooenable 쿼리 문자열 설정 hello CDN 끝점에 대 한 필요 하 고이 정보를 요청에서 허용 된 각 도메인에 대 한 고유한 쿼리 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="a3df1-156">이 작업을 수행 각 고유 쿼리 문자열에 대 한 별도 개체 캐싱을 CDN hello 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3df1-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="a3df1-157">그러나이 방법은 적합 하지 않습니다. hello의 여러 복사본에서와 동일한 파일을 CDN에 캐시 된 hello.</span><span class="sxs-lookup"><span data-stu-id="a3df1-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

