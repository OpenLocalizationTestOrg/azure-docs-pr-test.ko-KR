---
title: "Azure API 관리 제한 aaaAdvanced 요청"
description: "자세한 내용은 방법 toocreate 유연한 할당량 및 속도 제한 Azure API 관리를 사용 하 여 정책을 적용 합니다."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="94a24-103">Azure API 관리로 고급 요청 제한</span><span class="sxs-lookup"><span data-stu-id="94a24-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="94a24-104">들어오는 요청 수 toothrottle Azure API 관리의 중요 한 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-104">Being able toothrottle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="94a24-105">API 관리를 통해 전송 하거나 요청 또는 hello 총 요청/데이터 hello 속도 제어 API 공급자 tooprotect 남용에서 해당 Api 다양 한 API 제품 계층에 대 한 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-105">Either by controlling hello rate of requests or hello total requests/data transferred, API Management allows API providers tooprotect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="94a24-106">제품 기반 제한</span><span class="sxs-lookup"><span data-stu-id="94a24-106">Product based throttling</span></span>
<span data-ttu-id="94a24-107">toodate, hello 속도 제한 기능 범위 제한 toobeing tooa 특정 제품 구독 (기본적으로 키) 되어 합니다 API 관리 게시자 포털 hello에 정의 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-107">toodate, hello rate throttling capabilities have been limited toobeing scoped tooa particular Product subscription (essentially a key), defined in hello API Management publisher portal.</span></span> <span data-ttu-id="94a24-108">그러나 Hello 개발자에 게 등록 한 toouse 자신의 API에 대 한 hello API 공급자 tooapply 제한에 유용 합니다, 도움이 되지는 않습니다, 예를 들어 hello API의 개별 최종 사용자를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-108">This is useful for hello API provider tooapply limits on hello developers who have signed up toouse their API, however, it does not help, for example, in throttling individual end-users of hello API.</span></span> <span data-ttu-id="94a24-109">가 응용 프로그램 tooconsume hello 개발자의 단일 사용자에 대해 전체 할당량을 hello 있으며 다음 못하도록 hello 개발자의 다른 고객 수 toouse hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-109">It is possible that for single user of hello developer's application tooconsume hello entire quota and then prevent other customers of hello developer from being able toouse hello application.</span></span> <span data-ttu-id="94a24-110">또한 많은 양의 요청을 생성할 수 있습니다는 여러 고객 액세스 toooccasional 사용자를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-110">Also, several customers who might generate a high volume of requests may limit access toooccasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="94a24-111">사용자 지정 키 기반 제한</span><span class="sxs-lookup"><span data-stu-id="94a24-111">Custom key based throttling</span></span>
<span data-ttu-id="94a24-112">새 hello [키로 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [키로 할당량](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 정책은 훨씬 더 유연한 솔루션 tootraffic 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-112">hello new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution tootraffic control.</span></span> <span data-ttu-id="94a24-113">이러한 새 정책을 사용 하면 toodefine 식 tooidentify hello 키 사용된 tootrack 트래픽 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-113">These new policies allow you toodefine expressions tooidentify hello keys that will be used tootrack traffic usage.</span></span> <span data-ttu-id="94a24-114">첫 번째 예이 작동 하는 hello 방법은 보여 줍니다 것이 가장 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-114">hello way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="94a24-115">IP 주소 제한</span><span class="sxs-lookup"><span data-stu-id="94a24-115">IP Address throttling</span></span>
<span data-ttu-id="94a24-116">hello 다음 정책을 제한할 단일 클라이언트 IP 주소 tooonly 10 1000000 호출 하 고 매달 대역폭의 10, 000 킬로바이트 단위는 총 1 분 마다를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-116">hello following policies restrict a single client IP address tooonly 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="94a24-117">Hello 인터넷에 있는 모든 클라이언트에 고유 IP 주소를 사용 하는 경우 사용자가 사용을 제한 하는 효과적인 방법을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-117">If all clients on hello Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="94a24-118">그러나 여러 사용자가 toothem 액세스 hello 인터넷 NAT 장치를 통해 인해 단일 공용 IP 주소를 공유 한다는 가능성이 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-118">However, it is quite likely that multiple users will sharing a single public IP address due toothem accessing hello Internet via a NAT device.</span></span> <span data-ttu-id="94a24-119">Hello 인증 되지 않은 액세스를 허용 하는 Api에 대 한 그럼에도 불구 하 고 `IpAddress` hello 최상의 옵션 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-119">Despite this, for APIs that allow unauthenticated access hello `IpAddress` might be hello best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="94a24-120">사용자 ID 제한</span><span class="sxs-lookup"><span data-stu-id="94a24-120">User identity throttling</span></span>
<span data-ttu-id="94a24-121">최종 사용자가 인증된 후 해당 사용자를 고유하게 식별하는 정보를 기반으로 제한 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="94a24-122">다음이 예제에서는 hello 권한 부여 헤더를 추출, 너무 변환`JWT` 개체 및 hello 토큰 tooidentify hello 사용자의 hello 제목을 사용 하 여 hello 속도 키 제한으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-122">In this example we extract hello Authorization header, convert it too`JWT` object and use hello subject of hello token tooidentify hello user and use that as hello rate limiting key.</span></span> <span data-ttu-id="94a24-123">Hello 사용자 id hello에 저장 되어 있으면 `JWT` 하나 hello 다른 클레임으로 다음 그 자리에 값이 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-123">If hello user identity is stored in hello `JWT` as one of hello other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="94a24-124">결합된 정책</span><span class="sxs-lookup"><span data-stu-id="94a24-124">Combined policies</span></span>
<span data-ttu-id="94a24-125">새로운 정책을 조절 하는 hello hello 제한 정책을 기존 보다 더 많은 제어를 제공 하지만 여전히 값이 두 기능을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-125">Although hello new throttling policies provide more control than hello existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="94a24-126">제품 구독 키로 제한 ([구독에 의해 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [구독 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota))은 사용 수준에 따라 tooenable 충전 하 여 API의 monetizing 위한 훌륭한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way tooenable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="94a24-127">hello 더 세밀 하 게 제어할 수 toothrottle 사용자가 되는 상호 보완적인 고 방지 한 사용자의 동작 다른 hello 경험을 저하 시 키 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-127">hello finer grained control of being able toothrottle by user is complementary and prevents one user's behavior from degrading hello experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="94a24-128">클라이언트 기반 제한</span><span class="sxs-lookup"><span data-stu-id="94a24-128">Client driven throttling</span></span>
<span data-ttu-id="94a24-129">키를 제한 하는 hello를 사용 하 여 정의 되는 [정책 식을](https://msdn.microsoft.com/library/azure/dn910913.aspx), hello 제한 범위 방법을 선택 하는 hello API 공급자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-129">When hello throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is hello API provider that is choosing how hello throttling is scoped.</span></span> <span data-ttu-id="94a24-130">그러나 개발자는 경우가 평가 방법 toocontrol 자신의 고객을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-130">However, a developer might want toocontrol how they rate limit their own customers.</span></span> <span data-ttu-id="94a24-131">이 사용자 지정 헤더 tooallow hello 개발자의 클라이언트 응용 프로그램 toocommunicate hello 키 toohello API를 도입 하 여 hello API 공급자가 설정할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-131">This could be enabled by hello API provider by introducing a custom header tooallow hello developer's client application toocommunicate hello key toohello API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="94a24-132">이렇게 하면 hello 개발자의 클라이언트 응용 프로그램 toochoose 보고자 toocreate hello 속도 키를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-132">This enables hello developer's client application toochoose how they want toocreate hello rate limiting key.</span></span> <span data-ttu-id="94a24-133">약간의 클라이언트 개발자 hello 키 용도 키 toousers의 집합을 할당 하 여 자신의 급여 계층을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys toousers and rotating hello key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="94a24-134">요약</span><span class="sxs-lookup"><span data-stu-id="94a24-134">Summary</span></span>
<span data-ttu-id="94a24-135">Azure API 관리 속도 및 따옴표 tooboth 제한 보호 하 고 추가 값 tooyour API 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-135">Azure API Management provides rate and quote throttling tooboth protect and add value tooyour API service.</span></span> <span data-ttu-id="94a24-136">새로운 사용자 지정 범위 지정 규칙을 사용 하 여 정책을 조절 하는 hello 더욱 세밀 하 게 하면 덜 세분화 된 해당 정책 tooenable 제어할 고객 toobuild 더 나은 응용 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-136">hello new throttling policies with custom scoping rules allow you finer grained control over those policies tooenable your customers toobuild even better applications.</span></span> <span data-ttu-id="94a24-137">이 문서의 예제 hello 제조 속도 클라이언트 IP 주소, 사용자 id 및 클라이언트 생성 된 값과 함께 키를 제한 하 여 이러한 새 정책 사용 하 여를 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-137">hello examples in this article demonstrate hello use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="94a24-138">그러나 사용자 에이전트, URL 경로 부분, 메시지 크기와 같은 사용 될 수 있는 hello 메시지의 다른 많은 부분 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-138">However, there are many other parts of hello message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94a24-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94a24-139">Next steps</span></span>
<span data-ttu-id="94a24-140">하십시오 의견을 보내 주십시오 hello Disqus 스레드에이 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-140">Please give us your feedback in hello Disqus thread for this topic.</span></span> <span data-ttu-id="94a24-141">시나리오에서 논리적인 선택 된 다른 잠재적인 키 값에 대 한 훌륭한 toohear 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a24-141">It would be great toohear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="94a24-142">이러한 정책에 대한 동영상 개요 시청</span><span class="sxs-lookup"><span data-stu-id="94a24-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="94a24-143">Hello에 대 한 자세한 내용은 [키로 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [키로 할당량](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 이 문서에서 다루는 정책을 hello 다음 비디오를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94a24-143">For more information on hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

