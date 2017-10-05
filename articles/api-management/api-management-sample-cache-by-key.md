---
title: "Azure API 관리의 사용자 지정 캐싱"
description: "Azure API 관리에서 키로 항목을 캐시하는 방법을 알아봅니다"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="51255-103">Azure API 관리의 사용자 지정 캐싱</span><span class="sxs-lookup"><span data-stu-id="51255-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="51255-104">Azure API 관리 서비스에서는 리소스 URL을 키로 사용하는 [HTTP 응답 캐싱](api-management-howto-cache.md) 에 대한 기본 제공 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="51255-105">`vary-by` 속성을 사용하여 요청 헤더에서 키를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="51255-106">전체 HTTP 응답(즉, 표현)을 캐싱하는 데 유용하지만 때때로 표현의 일부를 캐싱하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="51255-107">새 [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) 및 [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) 정책은 임의의 정책 정의 내에서 데이터를 저장하고 검색하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="51255-108">이제 외부 서비스에서 나오는 응답을 캐시할 수 있기 때문에 이 기능은 이전에 도입된 [보내기 요청](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 정책에 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="51255-109">아키텍처</span><span class="sxs-lookup"><span data-stu-id="51255-109">Architecture</span></span>
<span data-ttu-id="51255-110">API 관리 서비스는 테넌트 단위 공유 데이터 캐시를 사용하므로 여러 단위까지 확장되어 동일하게 캐시된 데이터에 대한 액세스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="51255-111">그러나 다중 하위 지역 배포로 작업할 때 각 지역 내에 독립적인 캐시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="51255-112">이로 인해 일부 정보가 유일한 원본인 경우 소스 캐시를 데이터 저장소로 처리하지 않는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="51255-113">이렇게 하고 이후 다중 지역 배포를 활용하기로 결정한 경우 출장 중인 사용자와 고객은 캐시된 데이터에 액세스를 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="51255-114">부분 캐싱</span><span class="sxs-lookup"><span data-stu-id="51255-114">Fragment caching</span></span>
<span data-ttu-id="51255-115">반환되는 응답이 결정하는 비용이 높고 적절한 시간에 대해 원래 상태를 유지하는 데이터의 일부를 포함하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="51255-116">예를 들어 항공 예약, 비행 상태 등과 관련된 정보를 제공하는 항공사에서 작성한 서비스를 고려하는 것이 좋습니다. 사용자가 항공사 포인트 프로그램의 멤버인 경우 항공사는 현재 상태와 누적 주행 거리에 관련된 정보를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="51255-117">이 사용자 관련 정보는 다른 시스템에 저장될 수 있지만 비행 상태 및 예약에 대한 반환된 응답에 포함하는 것이 바람직할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="51255-118">이렇게 하려면 조각 캐싱이라는 프로세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="51255-119">기본 표시는 사용자 관련 정보를 삽입할 위치를 나타내는 일종의 토큰을 사용하여 원본 서버에서 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="51255-120">백 엔드 API에서 다음과 같은 JSON 응답을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-120">Consider the following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="51255-121">그리고 다음과 같은 `/userprofile/{userid}` 에 있는 보조 리소스도 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="51255-122">포함할 적절한 사용자 정보를 확인하기 위해 최종 사용자가 누구인지를 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="51255-123">이 메커니즘은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="51255-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="51255-124">예를 들어 `JWT` 토큰의 `Subject` 클레임을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="51255-125">이 `enduserid` 값을 나중에 사용할 컨텍스트 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="51255-126">다음 단계는 이전 요청이 사용자 정보를 검색하고 캐시에 저장했는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="51255-127">이렇게 하려면 `cache-lookup-value` 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="51255-128">키 값에 해당하는 캐시에 항목이 없는 경우 어떤 `userprofile` 컨텍스트 변수도 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="51255-129">`choose` 제어 흐름 정책을 사용하여 조회가 성공했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="51255-130">`userprofile` 컨텍스트 변수가 존재하지 않으면 찾아오기 위해 HTTP 요청을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="51255-131">`enduserid` 를 사용하여 사용자 프로필 리소스에 URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="51255-132">응답을 하면 응답에서 본문 텍스트를 가져오고 컨텍스트 변수에 다시 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="51255-133">이 HTTP 요청을 다시 하지 않으려면 동일한 사용자가 다른 요청을 할 때 사용자 프로필을 캐시에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="51255-134">원래 검색하려고 시도하는 동일한 키를 사용하여 캐시에 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="51255-135">값을 저장하도록 선택한 기간은 정보 변경 주기 및 사용자의 오래된 정보 허용치에 기반해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="51255-136">캐시에서 검색하는 작업이 여전히 out-of-process 네트워크 요청이며 잠재적으로 수십 밀리초를 요청에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="51255-137">사용자 프로필 정보를 확인하는 작업이 여러 백 엔드에서 데이터베이스 쿼리 또는 집계 정보를 수행해야 하기 때문에 훨씬 많은 시간이 걸릴 때 혜택이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="51255-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="51255-138">프로세스의 마지막 단계는 사용자 프로필 정보를 사용하여 반환된 응답을 업데이트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="51255-139">나는 토큰의 일부로 인용 부호를 포함하도록 선택하여 대체가 발생하지 않더라도 여전히 응답은 유효한 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="51255-140">주로 디버깅을 쉽게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51255-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="51255-141">이러한 모든 단계를 함께 결합하면 최종 결과는 다음과 같은 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="51255-142">이 캐싱 방법은 주로 HTML가 서버 쪽에서 구성되는 웹 사이트에서 사용되므로 단일 페이지로 렌더링될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="51255-143">그러나 클라이언트가 클라이언트 쪽 HTTP 캐싱을 수행할 수 없는 API에서 유용할 수 있고 또는 클라이언트에서 해당 역할을 넣지 않는 것이 바람직할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="51255-144">같은 종류의 조각 캐싱은 Redis caching 서버를 사용하여 백 엔드 웹 서버에서 수행될 수도 있지만 API 관리 서비스를 사용하여 이 작업을 수행하면  캐시된 조각이 기본 응답이 아닌 다른 백 엔드에서 생성될 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="51255-145">투명한 버전 관리</span><span class="sxs-lookup"><span data-stu-id="51255-145">Transparent versioning</span></span>
<span data-ttu-id="51255-146">API의 여러 다른 구현 버전이 한 번에 지원되는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="51255-147">개발, 테스트, 프로덕션 등과 같은 다른 환경을 지원하거나 API의 이전 버전을 지원하여 최신 버전으로 마이그레이션할 API 소비자에게 시간을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="51255-148">클라이언트 개발자가 URL을 `/v1/customers`에서 `/v2/customers`로 변경하도록 하는 대신 이를 처리하는 한 가지 방법이 있습니다. 즉, 현재 적절한 백 엔드 URL을 사용하고 호출하려는 API 버전인 소비자의 프로필 데이터를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="51255-149">특정 클라이언트에 대한 호출에 올바른 백 엔드 URL를 결정하기 위해 일부 구성 데이터를 쿼리하는 것이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="51255-150">이 구성 데이터를 캐시하여 이 조회를 수행하는 성능 저하를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="51255-151">첫 번째 단계는 원하는 버전을 구성하는 데 사용되는 식별자를 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="51255-152">이 예제에서는 제품 구독 키에 버전을 연결하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="51255-153">캐시 조회를 수행하여 이미 원하는 클라이언트 버전을 검색했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="51255-154">그런 다음 캐시에 있지 않은지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="51255-155">찾지 못한 경우 이동하여 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="51255-156">응답에서 응답 본문 텍스트를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="51255-157">나중에 사용할 캐시에 다시 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="51255-158">마지막으로 백 엔드 URL을 업데이트하여 클라이언트가 원하는 서비스의 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="51255-159">전체 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="51255-160">클라이언트가 클라이언트를 업데이트하고 다시 배포할 필요 없이 백 엔드 버전에 액세스하도록 투명하게 제어하도록 API 소비자를 사용하도록 설정하는 것이 많은 API 버전 관리 문제를 해결하는 세련된 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="51255-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="51255-161">테넌트 격리</span><span class="sxs-lookup"><span data-stu-id="51255-161">Tenant Isolation</span></span>
<span data-ttu-id="51255-162">더 큰 다중 테넌트 배포에서 일부 회사는 백 엔드 하드웨어의 고유한 배포에 테넌트의 별도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51255-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="51255-163">백 엔드에서 발생하는 하드웨어 문제로 영향을 받는 고객의 수를 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="51255-164">또한 새로운 소프트웨어 버전을 단계에서 롤아웃할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="51255-165">이상적으로 이 백 엔드 아키텍처는 API 소비자에게 투명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="51255-166">API 키 단위 구성 상태를 사용하여 백 엔드 URL을 조작하는 동일한 기법을 기반으로 하기 때문에 투명한 버전 관리에 비슷한 방식으로 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="51255-167">각 구독 키에 대한 기본 설정된 API 버전을 반환하는 대신 할당된 하드웨어 그룹에 테넌트를 연결하는 식별자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="51255-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="51255-168">적절한 백 엔드 URL을 생성하는 데 해당 식별자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="51255-169">요약</span><span class="sxs-lookup"><span data-stu-id="51255-169">Summary</span></span>
<span data-ttu-id="51255-170">모든 종류의 데이터를 저장하기 위해 Azure API 관리 캐시를 사용하면 인바운드 요청이 처리되는 방식에 영향을 줄 수 있는 구성 데이터에 대해 효율적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="51255-171">또한 백 엔드 API에서 반환된 응답을 강화할 수 있는 데이터 조각을 저장하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51255-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51255-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51255-172">Next steps</span></span>
<span data-ttu-id="51255-173">사용자를 위해 이러한 정책을 사용하는 다른 시나리오 또는 달성하려 하지만 현재 사용할 수 있다고 생각하지 않는 시나리오가 있다면 이 항목에 대한 Disqus 스레드에 의견을 보내 주십시오.</span><span class="sxs-lookup"><span data-stu-id="51255-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

