---
title: "캐시 ASP.NET 출력 캐시 공급자"
description: "Azure Redis Cache를 사용하여 ASP.NET 페이지 출력 캐시하는 방법을 알아봅니다."
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="f4388-103">Azure Redis Cache에 대한 ASP.NET 출력 캐시 공급자</span><span class="sxs-lookup"><span data-stu-id="f4388-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="f4388-104">Redis 출력 캐시 공급자는 출력 캐시 데이터에 대한 out-of-process 저장소 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="f4388-105">이 데이터는 완전한 HTTP 응답(페이지 출력 캐싱)에 특별히 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="f4388-106">공급자가 ASP.NET 4에 도입된 새로운 출력 캐시 공급자 확장 포인트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="f4388-107">Redis 출력 캐시 공급자를 사용 하려면 먼저 캐시를 구성하고 Redis 출력 개시 공급자 NuGet 패키지를 사용하여 사용자의 ASP.NET 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="f4388-108">이 항목에서는 Redis 출력 캐시 공급자를 사용할 수 있도록 응용 프로그램을 구성하는 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="f4388-109">Azure Redis Cache 인스턴스 생성 및 구성에 대한 자세한 내용은 [캐시 생성하기](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="f4388-110">ASP.NET 페이지 출력을 캐시에 저장</span><span class="sxs-lookup"><span data-stu-id="f4388-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="f4388-111">Redis Cache 세션 상태 NuGet 패키지를 사용하여 Visual Studio에서 클라이언트 응용 프로그램을 구성하려면 **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="f4388-112">`Package Manager Console` 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="f4388-113">Reids Output 캐시 공급자 NuGet 패키지는 StackExchange.Redis.StrongName 패키지에 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="f4388-114">StackExchange.Redis.StrongName 패키지가 프로젝트에 나타나지 않는 경우 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="f4388-115">Redis 출력 캐시 공급자 NuGet 패키지에 대한 자세한 내용은 [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet 패키지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="f4388-116">강력한 이름의 StackExchange.Redis.StrongName 패키지 외에도 StackExchange.Redis 강력하지 않은 이름의 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="f4388-117">프로젝트가 StackExchange.Redis 강력하지 않은 이름의 버전을 사용하는 경우 해당 버전을 제거해야 합니다. 그렇지 않으면 프로젝트에서 이름이 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="f4388-118">이 패키지에 대한 자세한 내용은 [.NET 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="f4388-119">NuGet 패키지에서는 필수 어셈블리 참조를 다운로드하고 추가하며 web.config 파일에 다음 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="f4388-120">이 섹션에서는 Redis 출력 캐시 공급자를 사용하기 위해 ASP.NET 응용 프로그램에 필수 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="f4388-121">주석 처리된 섹션은 특성의 예와 각 특성의 샘플 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="f4388-122">Microsoft Azure 포털의 캐시 블레이드에서 값으로 특성을 구성하고, 필요에 따라 다른 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="f4388-123">캐시 속성에 액세스 하는 방법은 [Redis 캐시 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="f4388-124">**호스트** – 캐시 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="f4388-125">**포트** – ssl 설정에 따라 비-SSL 포트 또는 SSL 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="f4388-126">**선택키** – 캐시에 적합한 기본 또는 보조 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="f4388-127">**ssl** – ssl로 캐시/클라이언트 통신을 보호하려는 경우 true가 되고, 그 외의 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="f4388-128">올바른 포트를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="f4388-129">비 SSL 포트는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="f4388-130">SSL 포트를 사용하여 설정에 대한 true를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="f4388-131">비-SSL 포트 사용 방법에 대한 자세한 내용은 [캐시 구성](cache-configure.md) 토픽의 [액세스 포트](cache-configure.md#access-ports) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="f4388-132">**databaseId** – 캐시 출력 데이터에 사용할 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="f4388-133">지정하지 않으면 기본값 0이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="f4388-134">**applicationName** – `<AppName>_<SessionId>_Data`로 redis에 저장된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="f4388-135">이 이름 지정 체계를 사용하면 여러 응용 프로그램이 동일한 키를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="f4388-136">이 매개변수는 선택적이며 사용자가 제공하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="f4388-137">**connectionTimeoutInMilliseconds** – 이 설정은 StackExchange.Redis 클라이언트의 connectTimeout 설정을 무시할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="f4388-138">지정하지 않으면 기본 connectTimeout 설정인 5000이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="f4388-139">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="f4388-140">**operationTimeoutInMilliseconds** – 이 설정은 StackExchange.Redis 클라이언트의 syncTimeout 설정을 무시할 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="f4388-141">지정하지 않으면 기본 syncTimeout 설정인 1000이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="f4388-142">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="f4388-143">출력을 캐시하고자 하는 각 페이지에 OutputCache 지시문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="f4388-144">이전 예제에서는 캐시된 페이지 데이터가 캐시에 60초 동안 머물게 되며, 각 매개 변수 조합에 따라 페이지의 다른 버전이 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="f4388-145">출력 캐시 지시문에 대한 자세한 내용은 [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="f4388-146">이 단계를 수행하면, 응용 프로그램은 Redis 출력 캐시 공급자를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4388-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4388-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4388-147">Next steps</span></span>
<span data-ttu-id="f4388-148">[Azure Redis Cache에 대한 ASP.NET 세션 상태 제공자](cache-aspnet-session-state-provider.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f4388-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

