---
title: "Azure API 관리로 고급 요청 제한"
description: "Azure API 관리로 유연한 할당량 및 속도 제한 정책을 만들고 적용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="0c621-103">Azure API 관리로 고급 요청 제한</span><span class="sxs-lookup"><span data-stu-id="0c621-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="0c621-104">들어오는 요청을 제한하는 것은 Azure API 관리의 중요한 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="0c621-105">Azure API 관리는 요청 속도 또는 전송된 총 요청/데이터를 제어하여 API 공급자가 자신의 API가 남용되지 않도록 보호하고 다양한 API 제품 계층에 대해 가치를 창출할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="0c621-106">제품 기반 제한</span><span class="sxs-lookup"><span data-stu-id="0c621-106">Product based throttling</span></span>
<span data-ttu-id="0c621-107">현재까지, 속도 제한 기능은 API 관리 게시자 포털에 정의된 특정 제품 구독(기본적으로 키)으로 범위를 제한했습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="0c621-108">이렇게 하면 API 공급자가 해당 API를 사용하기 위해 등록한 개발자에게 제한을 적용하는 데는 유용하지만 예를 들어 API의 개별 최종 사용자를 제한하는 데는 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="0c621-109">개발자 응용 프로그램의 단일 사용자가 전체 할당량을 사용한 후 개발자의 다른 고객이 해당 응용 프로그램을 사용하지 못하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="0c621-110">또한, 대용량의 요청을 생성할 수 있는 여러 고객이 간헐적 사용자에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="0c621-111">사용자 지정 키 기반 제한</span><span class="sxs-lookup"><span data-stu-id="0c621-111">Custom key based throttling</span></span>
<span data-ttu-id="0c621-112">새로운 [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 정책은 트래픽 제어에 훨씬 유연한 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="0c621-113">이 새로운 정책을 통해 트래픽 사용량을 추적하는 데 사용할 키를 식별하는 식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="0c621-114">이러한 작동 방식은 예제를 통해 가장 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="0c621-115">IP 주소 제한</span><span class="sxs-lookup"><span data-stu-id="0c621-115">IP Address throttling</span></span>
<span data-ttu-id="0c621-116">다음 정책은 단일 클라이언트 IP 주소를 1분에 10개 호출만으로 제한하고 1개월에 총 1,000,000개 호출과 10,000킬로바이트의 대역폭으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="0c621-117">인터넷의 모든 클라이언트가 고유 IP 주소를 사용한 경우 사용자별로 사용량을 제한하는 효과적인 방법일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="0c621-118">그러나 사용자는 NAT 장치를 통해 인터넷에 액세스하므로 여러 사용자가 하나의 공용 IP 주소를 공유할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="0c621-119">그럼에도 불구하고 `IpAddress` 에 대한 무단 액세스를 허용하는 API에 대해서는 최상의 옵션일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="0c621-120">사용자 ID 제한</span><span class="sxs-lookup"><span data-stu-id="0c621-120">User identity throttling</span></span>
<span data-ttu-id="0c621-121">최종 사용자가 인증된 후 해당 사용자를 고유하게 식별하는 정보를 기반으로 제한 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="0c621-122">이 예제에서는 인증 헤더를 추출하여 `JWT` 개체로 변환하고 토큰의 주체를 사용하여 사용자를 식별하고 속도 제한 키로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="0c621-123">사용자 ID가 `JWT` 에 다른 클레임 중 하나로 저장된 경우 해당 값을 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="0c621-124">결합된 정책</span><span class="sxs-lookup"><span data-stu-id="0c621-124">Combined policies</span></span>
<span data-ttu-id="0c621-125">새 제한 정책이 기존 제한 정책보다 더 많은 제어를 제공하더라도 여전히 두 기능을 결합하는 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="0c621-126">제품 구독 키로 제한([구독으로 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [구독으로 사용 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota))은 사용 수준에 따라 요금을 청구하여 API 수익화를 실현하는 뛰어난 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="0c621-127">사용자별로 제한할 수 있도록 세분화된 제어로 보완되며 한 사용자의 동작이 다른 사용자의 환경에 부정적인 영향을 주지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="0c621-128">클라이언트 기반 제한</span><span class="sxs-lookup"><span data-stu-id="0c621-128">Client driven throttling</span></span>
<span data-ttu-id="0c621-129">제한 키가 [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx)을 사용하여 정의된 경우 제한 범위를 정하는 방식을 선택하는 것은 API 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="0c621-130">그러나 개발자가 자신의 고객을 속도 제한하는 방식을 제어하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="0c621-131">API 공급자가 개발자의 클라이언트 응용 프로그램이 키를 API에 전달하도록 허용하는 사용자 지정 헤더를 도입하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="0c621-132">따라서 개발자의 클라이언트 응용 프로그램이 속도 제한 키를 만드는 방법을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="0c621-133">약간의 창의성만 발휘한다면 클라이언트 개발자는 키 집합을 사용자에 할당하고 키 사용을 회전하여 자신의 고유한 속도 계층을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="0c621-134">요약</span><span class="sxs-lookup"><span data-stu-id="0c621-134">Summary</span></span>
<span data-ttu-id="0c621-135">Azure API 관리에서는 속도 및 할당량 제한을 제공하여 API 서비스를 보호하고 가치를 더합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="0c621-136">사용자 지정 범위 규칙이 포함된 새로운 제한 정책을 통해 정책을 세밀하게 제어할 수 있으므로 고객이 훨씬 향상된 응용 프로그램을 구축할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="0c621-137">이 문서의 예제에서는 클라이언트 IP 주소, 사용자 ID 및 클라이언트에서 생성한 값으로 속도 제한 키를 제조하여 이러한 새 정책을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="0c621-138">그러나 사용자 에이전트, URL 경로 조각, 메시지 크기와 같이 사용할 수 있는 메시지의 많은 다른 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c621-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c621-139">Next steps</span></span>
<span data-ttu-id="0c621-140">이 항목에 대한 Disqus 스레드에 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="0c621-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="0c621-141">귀하의 시나리오에서 논리적으로 선택된 잠재적인 다른 키 값에 대한 의견을 환영합니다.</span><span class="sxs-lookup"><span data-stu-id="0c621-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="0c621-142">이러한 정책에 대한 동영상 개요 시청</span><span class="sxs-lookup"><span data-stu-id="0c621-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="0c621-143">이 문서에서 다루는 [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 정책에 대한 자세한 내용은 다음 동영상을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c621-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

