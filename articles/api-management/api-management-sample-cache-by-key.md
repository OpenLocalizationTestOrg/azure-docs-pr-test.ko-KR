---
title: "Azure API 관리에서 aaaCustom 캐싱"
description: "Azure API 관리에서 키로 toocache 항목 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="adbf0-103">Azure API 관리의 사용자 지정 캐싱</span><span class="sxs-lookup"><span data-stu-id="adbf0-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="adbf0-104">Azure API 관리 서비스에서 기본적으로 지원 [HTTP 응답 캐시](api-management-howto-cache.md) hello 키로 hello 리소스 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="adbf0-105">hello 키를 수정할 수 hello를 사용 하 여 요청 헤더에 의해 `vary-by` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="adbf0-106">이 전체 HTTP 응답 (즉, 표현)을 캐시 하는 데 유용 하지만 유용한 toojust 캐시 표현의 일부 경우에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="adbf0-107">새 hello [캐시에서 조회 값](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) 및 [캐시 저장소의 값](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) 정책은 정책 정의 내에서 데이터의 임의 부분 toostore 및 검색 하 고 hello 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="adbf0-108">이 기능은 값 toohello 이전에 도입 된 추가 [보내기 요청](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 정책 되므로 이제 외부 서비스에서 응답을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="adbf0-109">아키텍처</span><span class="sxs-lookup"><span data-stu-id="adbf0-109">Architecture</span></span>
<span data-ttu-id="adbf0-110">API 관리 서비스는 여전히 액세스 toohello toomultiple 단위를 확장 시 받아볼 있도록 공유 당-테 넌 트 데이터 캐시를 사용 데이터를 캐시 하는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="adbf0-111">그러나 다중 지역 배포와 함께 작업 하는 경우 각 hello 지역 내에서 독립적인 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="adbf0-112">기한 toothis, 것이 중요 toonot 경우 hello 유일한 소스 정보 중 일부에 대 한 데이터 저장소로 hello 캐시를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="adbf0-113">나중에 tootake 활용 hello 다중 지역 배포를 결정 하는 경우 이동 하는 사용자가 사용 하는 고객 액세스 toothat 캐시 데이터가 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="adbf0-114">부분 캐싱</span><span class="sxs-lookup"><span data-stu-id="adbf0-114">Fragment caching</span></span>
<span data-ttu-id="adbf0-115">특정 되 고 반환 된 응답에 포함 된 경우 비용이 많이 드는 toodetermine를 이며 아직 적절 한 시간에 대 한 새을 유지 하는 데이터의 일부 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="adbf0-116">예를 들어 항공 예약, 비행 상태 등과 관련된 정보를 제공하는 항공사에서 작성한 서비스를 고려하는 것이 좋습니다. Hello 사용자 hello airlines 포인트 프로그램의 멤버인 경우 것도 갖게 tootheir 현재 상태 및 누적 주행 거리와 관련 된 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="adbf0-117">이 사용자 관련 정보를 다른 시스템에 저장 될 수 있지만 바람직한 tooinclude 비행 상태 및 예약에 대 한 응답에서 반환 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="adbf0-118">이렇게 하려면 조각 캐싱이라는 프로세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="adbf0-119">hello 기본 표현에서에서 반환할 수 여기서 hello 사용자 관련 정보는 삽입 toobe 토큰 tooindicate의 몇 가지 종류에 사용 하는 hello 원본 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="adbf0-120">Hello을 백 엔드 API에서에서 JSON 응답을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="adbf0-121">그리고 다음과 같은 `/userprofile/{userid}` 에 있는 보조 리소스도 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="adbf0-122">순서 toodetermine hello 적절 한 사용자 정보 tooinclude tooidentify hello 최종 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="adbf0-123">이 메커니즘은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="adbf0-124">예를 들어 hello를 사용 하 고 `Subject` 의 청구는 `JWT` 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="adbf0-125">이 `enduserid` 값을 나중에 사용할 컨텍스트 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="adbf0-126">hello 다음 단계는 이전 요청 이미 hello 사용자 정보를 검색 하 고 hello 캐시에 저장 된 경우 toodetermine입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="adbf0-127">이 사용 하 여 hello `cache-lookup-value` 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="adbf0-128">No 다음 toohello 키 값을 해당 하는 hello 캐시에 항목이 없을 경우 `userprofile` 컨텍스트 변수가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="adbf0-129">Hello를 사용 하 여 hello 조회의 hello 성공을 확인 `choose` 흐름 정책을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="adbf0-130">경우 hello `userprofile` 컨텍스트 변수가 존재 하지 않으면 다음 진행 중인 toohave toomake HTTP 요청 tooretrieve 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="adbf0-131">사용 하 여 hello `enduserid` tooconstruct hello URL toohello 사용자 프로필 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="adbf0-132">Hello 응답, 상태 hello 응답에서 본문 텍스트 hello 끌어오기 하 고 상황에 맞는 변수로 저장 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="adbf0-133">tooavoid us toomake이 HTTP 요청이 있는지 다시 hello 동일한 사용자가 다른 요청 하는 경우, 저장할 수 hello 사용자 프로필 hello 캐시에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="adbf0-134">Hello 값 tooretrieve 원래 시도 म hello 정확히 동일한 키를 사용 하 여 hello 캐시에 저장 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="adbf0-135">hello toostore hello 값 선택 된 기간에 따라 얼마나 자주 hello 정보 변경와 어떻게 허용 사용자가 tooout의 날짜 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="adbf0-136">중요 한 toorealize hello 캐시에서 검색 아직 이라고 out of process, 네트워크 요청 이며 잠재적으로 밀리초 toohello 요청 수만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="adbf0-137">hello 이점 기한 tooneeding toodo 데이터베이스 쿼리 또는 집계 정보를 여러 백 엔드 보다 훨씬 오래 걸리면 결정 hello 사용자 프로필 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="adbf0-138">hello hello 프로세스의 마지막 단계는 tooupdate hello 우리의 사용자 프로필 정보로 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="adbf0-139">선택 tooinclude hello 따옴표 hello 토큰의 일부로 hello 응답을 여전히 유효한 JSON hello 바꾸기 발생 하지 않는 경우에 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="adbf0-140">이 디버깅을 보다 쉽게 toomake 주로 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="adbf0-141">이러한 모든 단계를 함께 결합 되 면 hello 그 결과 다음과 같은 hello 하나를 수행 하는 정책이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
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

<span data-ttu-id="adbf0-142">이 캐싱 방법은 주로 웹 사이트에서 한 페이지로 렌더링 될 수 있도록 hello 서버 쪽에서 HTML 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="adbf0-143">그러나 것도 유용할 수 있습니다에 클라이언트가 클라이언트를 수행할 수 없습니다 Api HTTP 캐시 하거나 것이 바람직합니다 하지 tooput hello 클라이언트에서 이러한 일 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="adbf0-144">그러나 API 관리 서비스 tooperform hello를 사용 하 여이 작업은 유용 hello 보다 다른 백 엔드가에서 캐시 된 hello 조각이 생성 되는 경우, 부분 캐싱이 동일한 유형의 서버 캐싱을 Redis를 사용 하 여 hello 백 엔드 웹 서버에서 수행할 수 있습니다. 기본 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="adbf0-145">투명한 버전 관리</span><span class="sxs-lookup"><span data-stu-id="adbf0-145">Transparent versioning</span></span>
<span data-ttu-id="adbf0-146">한 번에 지원 되는 API toobe의 여러 다른 구현 버전에 대 한 일반적인이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="adbf0-147">아마도 개발, 테스트, 프로덕션 등과 같은, toosupport 서로 다른 환경 또는 toosupport 이전 버전의 hello API toogive 시간 API 소비자 toomigrate toonewer 버전에는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="adbf0-148">대신이 클라이언트 개발자 toochange hello Url에서 요구할 때의 한 가지 방법은 toohandling `/v1/customers` 너무`/v2/customers` hello 소비자의 프로필 데이터 toostore hello API의 버전 있어입니다 현재 toouse 원하는 hello를 적절 한 호출 백 엔드 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="adbf0-149">이 필요한 tooquery 순서 toodetermine hello 올바른 백 엔드 URL toocall 특정 클라이언트, 일부 구성 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="adbf0-150">이 구성 데이터를 캐시 하 여에서는이 조회 작업을 수행 하는 hello 성능 저하를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="adbf0-151">hello 첫 번째 단계는 toodetermine hello 식별자 tooconfigure hello 원하는 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="adbf0-152">이 예제에서는 tooassociate hello 버전 toohello 제품 구독 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="adbf0-153">그런 다음 캐시 조회 toosee hello 원하는 클라이언트 버전이 이미 검색 한 경우 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="adbf0-154">그런 다음 hello 캐시에서 발견 되지 않은 되는 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="adbf0-155">찾지 못한 경우 이동하여 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="adbf0-156">Hello 응답에서 hello 응답 본문 텍스트를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="adbf0-157">나중에 사용할 hello 캐시에 다시 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="adbf0-158">및 hello 백 엔드 URL tooselect hello 버전의 hello 클라이언트에서 원하는 hello 서비스를 마지막으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="adbf0-159">hello 완전히 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
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

<span data-ttu-id="adbf0-160">백 엔드 버전 tooupdate 및 재배포 클라이언트 필요 없이 클라이언트에서 액세스 되는 API 소비자 tootransparently 제어를 사용 하는 것은 많은 API 버전 관리 문제를 해결할 수 있는 세련 된 솔루션.</span><span class="sxs-lookup"><span data-stu-id="adbf0-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="adbf0-161">테넌트 격리</span><span class="sxs-lookup"><span data-stu-id="adbf0-161">Tenant Isolation</span></span>
<span data-ttu-id="adbf0-162">더 큰 다중 테넌트 배포에서 일부 회사는 백 엔드 하드웨어의 고유한 배포에 테넌트의 별도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="adbf0-163">이 hello hello 백 엔드에는 하드웨어 문제로 인해 영향을 받을 고객 수를 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="adbf0-164">또한 단계에서 제공 하는 새 소프트웨어 버전 toobe를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="adbf0-165">이 백 엔드 아키텍처 투명 tooAPI 소비자 여야 가장 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="adbf0-166">Hello을 기반으로 하므로 비슷한 방식으로 tootransparent 버전 관리에서 수행할 수 있습니다 API 키 당 구성 상태를 사용 하 여 hello 백 엔드 URL을 조작 하는 동일한 기법입니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="adbf0-167">각 구독 키에 대 한 hello API의 기본 버전을 반환 하는 대신 테 넌 트 할당 toohello 하드웨어 그룹을 연결 하는 식별자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="adbf0-168">해당 식별자에 사용 되는 tooconstruct hello 적절 한 백 엔드 URL 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="adbf0-169">요약</span><span class="sxs-lookup"><span data-stu-id="adbf0-169">Summary</span></span>
<span data-ttu-id="adbf0-170">hello 자유 toouse hello 모든 종류의 데이터를 저장 하기 위한 Azure API 관리 캐시 통해 효율적으로 액세스 tooconfiguration 데이터가 인바운드 요청 처리 hello 방식을 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="adbf0-171">백 엔드 API에서에서 반환 된 응답을 강화할 수 toostore 사용 되는 데이터 조각을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adbf0-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="adbf0-172">Next steps</span></span>
<span data-ttu-id="adbf0-173">하십시오 의견을 보내 주십시오 Disqus 스레드 hello에이 항목에 대 한 경우, 이러한 정책을 사용 하도록 설정한 또는 tooachieve ु 시나리오 있을 경우 되지만 같지 않으면 다른 시나리오는 현재는 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbf0-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

