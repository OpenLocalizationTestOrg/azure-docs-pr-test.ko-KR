---
title: "캐시 ASP.NET 세션 상태 제공자 | Microsoft Docs"
description: "Azure Redis Cache를 사용하여 ASP.NET 세션 상태를 저장하는 방법을 알아봅니다."
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 0f3683939ac9646565a0669e19b4c82811d621fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a><span data-ttu-id="70d79-103">Azure Redis Cache에 대한 ASP.NET 세션 상태 제공자</span><span class="sxs-lookup"><span data-stu-id="70d79-103">ASP.NET Session State Provider for Azure Redis Cache</span></span>
<span data-ttu-id="70d79-104">Azure Redis Cache는 메모리 내 또는 SQL Server 데이터베이스가 아니라 캐시에 세션 상태를 저장하는 데 사용할 수 있는 세션 상태 제공자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-104">Azure Redis Cache provides a session state provider that you can use to store your session state in a cache rather than in-memory or in a SQL Server database.</span></span> <span data-ttu-id="70d79-105">캐싱 세션 상태 제공자를 사용하려면 먼저 캐시를 구성하고 Redis Cache 세션 상태 NuGet 패키지를 사용하여 캐시용 ASP.NET 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-105">To use the caching session state provider, first configure your cache, and then configure your ASP.NET application for cache using the Redis Cache Session State NuGet package.</span></span>

<span data-ttu-id="70d79-106">종종 실제 클라우드 앱에서 사용자 세션에 대한 일종의 상태를 저장을 회피하는 데 실용적이지 않지만 일부 접근 방법은 다른 항목 보다 성능 및 확장성에 더 많은 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-106">It's often not practical in a real-world cloud app to avoid storing some form of state for a user session, but some approaches impact performance and scalability more than others.</span></span> <span data-ttu-id="70d79-107">상태를 저장해야 하는 경우 가장 좋은 해결법은 상태의 크기를 작게 유지하고 쿠키에 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-107">If you have to store state, the best solution is to keep the amount of state small and store it in cookies.</span></span> <span data-ttu-id="70d79-108">이것이 어려운 경우 다음 해결법은 분산된 메모리 내 캐시에 대해 공급자로 ASP.NET 세션 상태를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-108">If that isn't feasible, the next best solution is to use ASP.NET session state with a provider for distributed, in-memory cache.</span></span> <span data-ttu-id="70d79-109">성능 및 확장성 측면에서 최악의 해결법은 데이터베이스 지원 세션 상태 제공자를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-109">The worst solution from a performance and scalability standpoint is to use a database backed session state provider.</span></span> <span data-ttu-id="70d79-110">이 항목은 Azure Redis Cache에 대해 ASP.NET 세션 상태 제공자를 사용하는 가이드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-110">This topic provides guidance on using the ASP.NET Session State Provider for Azure Redis Cache.</span></span> <span data-ttu-id="70d79-111">다른 세션 상태 옵션에 대한 내용은 [ASP.NET 세션 상태 옵션](#aspnet-session-state-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-111">For information on other session state options, see [ASP.NET Session State options](#aspnet-session-state-options).</span></span>

## <a name="store-aspnet-session-state-in-the-cache"></a><span data-ttu-id="70d79-112">캐시에 ASP.NET 세션 상태 저장</span><span class="sxs-lookup"><span data-stu-id="70d79-112">Store ASP.NET session state in the cache</span></span>
<span data-ttu-id="70d79-113">Redis Cache 세션 상태 NuGet 패키지를 사용하여 Visual Studio에서 클라이언트 응용 프로그램을 구성하려면 **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-113">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="70d79-114">`Package Manager Console` 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-114">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> <span data-ttu-id="70d79-115">프리미엄 계층에서 클러스터링 기능을 사용하는 경우 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 이상을 사용하지 않으면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-115">If you are using the clustering feature from the premium tier, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="70d79-116">2.0.1 이상 버전으로 이동하는 주요 변경 내용입니다. 자세한 내용은 [v2.0.0 주요 변경 세부 사항](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-116">Moving to 2.0.1 or higher is a breaking change; for more information, see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span> <span data-ttu-id="70d79-117">이 문서를 업데이트할 당시 이 패키지의 현재 버전은 2.2.3입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-117">At the time of this article update, the current version of this package is 2.2.3.</span></span>
> 
> 

<span data-ttu-id="70d79-118">Reids 세션 상태 제공자 NuGet 패키지는 StackExchange.Redis.StrongName 패키지에 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-118">The Redis Session State Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="70d79-119">StackExchange.Redis.StrongName 패키지가 프로젝트에 나타나지 않는 경우 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-119">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span>

>[!NOTE]
><span data-ttu-id="70d79-120">강력한 이름의 StackExchange.Redis.StrongName 패키지 외에도 StackExchange.Redis 강력하지 않은 이름의 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-120">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="70d79-121">프로젝트가 StackExchange.Redis 강력하지 않은 이름의 버전을 사용하는 경우 해당 버전을 제거해야 합니다. 그렇지 않으면 프로젝트에서 이름이 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-121">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="70d79-122">이 패키지에 대한 자세한 내용은 [.NET 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-122">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="70d79-123">NuGet 패키지에서는 필수 어셈블리 참조를 다운로드하고 추가하며 web.config 파일에 다음 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-123">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="70d79-124">이 섹션에서는 Redis Cache 세션 상태 제공자를 사용하기 위해 ASP.NET 응용 프로그램에 필수 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-124">This section contains the required configuration for your ASP.NET application to use the Redis Cache Session State Provider.</span></span>

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

<span data-ttu-id="70d79-125">주석 처리된 섹션은 특성의 예와 각 특성의 샘플 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-125">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="70d79-126">Microsoft Azure 포털의 캐시 블레이드에서 값으로 특성을 구성하고, 필요에 따라 다른 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-126">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="70d79-127">캐시 속성에 액세스 하는 방법은 [Redis 캐시 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-127">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="70d79-128">**호스트** – 캐시 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-128">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="70d79-129">**포트** – ssl 설정에 따라 비-SSL 포트 또는 SSL 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-129">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="70d79-130">**선택키** – 캐시에 적합한 기본 또는 보조 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-130">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="70d79-131">**ssl** – ssl로 캐시/클라이언트 통신을 보호하려는 경우 true가 되고, 그 외의 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-131">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="70d79-132">올바른 포트를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-132">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="70d79-133">비 SSL 포트는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-133">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="70d79-134">SSL 포트를 사용하여 설정에 대한 true를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-134">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="70d79-135">비-SSL 포트 사용 방법에 대한 자세한 내용은 [캐시 구성](cache-configure.md) 토픽의 [액세스 포트](cache-configure.md#access-ports) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-135">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="70d79-136">**throwOnError** – 오류가 있는 경우 예외를 throw하려면 true이고 작업을 자동으로 실패하게 하려면 false입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-136">**throwOnError** – true if you want an exception to be thrown if there is a failure, or false if you want the operation to fail silently.</span></span> <span data-ttu-id="70d79-137">정적 Microsoft.Web.Redis.RedisSessionStateProvider.LastException 속성을 확인하여 오류를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-137">You can check for a failure by checking the static Microsoft.Web.Redis.RedisSessionStateProvider.LastException property.</span></span> <span data-ttu-id="70d79-138">기본값은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-138">The default is true.</span></span>
* <span data-ttu-id="70d79-139">**retryTimeoutInMilliseconds** – 이 간격 동안 실패한 작업이 다시 시도되며 밀리초 단위로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-139">**retryTimeoutInMilliseconds** – Operations that fail are retried during this interval, specified in milliseconds.</span></span> <span data-ttu-id="70d79-140">처음 다시 시도는 20밀리초 후에 발생하고 다시 시도는 retryTimeoutInMilliseconds 간격이 만료될 때까지 매초 마다 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-140">The first retry occurs after 20 milliseconds, and then retries occur every second until the retryTimeoutInMilliseconds interval expires.</span></span> <span data-ttu-id="70d79-141">이 간격 후에 즉시 최종적으로 한 번 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-141">Immediately after this interval, the operation is retried one final time.</span></span> <span data-ttu-id="70d79-142">작업이 계속 실패하면 throwOnError 설정에 따라 호출자에게 예외가 다시 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-142">If the operation still fails, the exception is thrown back to the caller, depending on the throwOnError setting.</span></span> <span data-ttu-id="70d79-143">기본값은 다시 시도하지 않는다는 의미의 0입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-143">The default value is 0, which means no retries.</span></span>
* <span data-ttu-id="70d79-144">**databaseId** – 캐시 출력 데이터에 사용할 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-144">**databaseId** – Specifies which database to use for cache output data.</span></span> <span data-ttu-id="70d79-145">지정하지 않으면 기본값 0이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-145">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="70d79-146">**applicationName** – `{<Application Name>_<Session ID>}_Data`로 redis에 저장된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-146">**applicationName** – Keys are stored in redis as `{<Application Name>_<Session ID>}_Data`.</span></span> <span data-ttu-id="70d79-147">이 이름 지정 체계를 사용하면 여러 응용 프로그램에서 동일한 Redis 인스턴스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-147">This naming scheme enables multiple applications to share the same Redis instance.</span></span> <span data-ttu-id="70d79-148">이 매개변수는 선택적이며 사용자가 제공하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-148">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="70d79-149">**connectionTimeoutInMilliseconds** – 이 설정은 StackExchange.Redis 클라이언트의 connectTimeout 설정을 무시할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-149">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="70d79-150">지정하지 않으면 기본 connectTimeout 설정인 5000이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-150">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="70d79-151">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-151">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="70d79-152">**operationTimeoutInMilliseconds** – 이 설정은 StackExchange.Redis 클라이언트의 syncTimeout 설정을 무시할 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-152">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="70d79-153">지정하지 않으면 기본 syncTimeout 설정인 1000이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-153">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="70d79-154">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-154">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="70d79-155">이러한 속성에 대한 자세한 내용은 [Redis에 대한 ASP.NET 세션 상태 제공자 발표](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)에서 원래 블로그 게시물 발표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-155">For more information about these properties, see the original blog post announcement at [Announcing ASP.NET Session State Provider for Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).</span></span>

<span data-ttu-id="70d79-156">Web.config 파일에서 표준 InProc 세션 상태 제공자 섹션을 주석으로 처리하는 것을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-156">Don’t forget to comment out the standard InProc session state provider section in your web.config.</span></span>

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

<span data-ttu-id="70d79-157">이 단계를 수행하면, 응용 프로그램은 Redis Cache 섹션 상태 제공자를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-157">Once these steps are performed, your application is configured to use the Redis Cache Session State Provider.</span></span> <span data-ttu-id="70d79-158">응용 프로그램에서 세션 상태를 사용하는 경우 Azure Redis Cache 인스턴스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-158">When you use session state in your application, it is stored in an Azure Redis Cache instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70d79-159">기본값 메모리 내 ASP.NET 세션 상태 제공자에 저장될 수 있는 데이터와 달리 캐시에 저장된 데이터는 직렬화할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-159">Data stored in the cache must be serializable, unlike the data that can be stored in the default in-memory ASP.NET Session State Provider.</span></span> <span data-ttu-id="70d79-160">Redis에 세션 상태 제공자를 사용하면 세션 상태에 저장되는 데이터 형식을 직렬화할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-160">When the Session State Provider for Redis is used, be sure that the data types that are being stored in session state are serializable.</span></span>
> 
> 

## <a name="aspnet-session-state-options"></a><span data-ttu-id="70d79-161">ASP.NET 세션 상태 옵션</span><span class="sxs-lookup"><span data-stu-id="70d79-161">ASP.NET Session State options</span></span>
* <span data-ttu-id="70d79-162">메모리 내 세션 상태 제공자 - 이 공급자는 메모리에 세션 상태를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-162">In Memory Session State Provider - This provider stores the Session State in memory.</span></span> <span data-ttu-id="70d79-163">이 공급자를 사용하면 단순하고 빠르다는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-163">The benefit of using this provider is it is simple and fast.</span></span> <span data-ttu-id="70d79-164">그러나 배포되지 않는 메모리 공급자에서 사용 중인 경우 웹앱의 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-164">However you cannot scale your Web Apps if you are using in memory provider since it is not distributed.</span></span>
* <span data-ttu-id="70d79-165">SQL Server 세션 상태 제공자 - 이 공급자는 SQL Server에 세션 상태를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-165">Sql Server Session State Provider - This provider stores the Session State in Sql Server.</span></span> <span data-ttu-id="70d79-166">영구 저장소에서 세션 상태를 유지하려는 경우 이 제공자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-166">Use this provider if you want to store the Session state in persistent storage.</span></span> <span data-ttu-id="70d79-167">Web App의 크기를 조정할 수 있지만 세션에 SQL Server를 사용하면 Web App의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-167">You can scale your Web App but using Sql Server for Session has a performance impact on your Web App.</span></span>
* <span data-ttu-id="70d79-168">Redis Cache 세션 상태 제공자와 같은 배포된 메모리 내 세션 상태 제공자 - 이 공급자는 두 분야의 모든 장점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-168">Distributed In Memory Session State Provider such as Redis Cache Session State Provider - This provider gives you the best of both worlds.</span></span> <span data-ttu-id="70d79-169">Web App에는 빠르고 간단하며 확장성 있는 세션 상태 제공자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-169">Your Web App can have a simple, fast, and scalable Session State Provider.</span></span> <span data-ttu-id="70d79-170">이 제공자가 캐시에서 세션 상태를 저장하기 때문에 앱이 일시적인 네트워크 오류와 같은 분산된 메모리 내 캐시와 통신할 때 관련된 모든 특성을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-170">Because this provider stores the Session state in a Cache, your app has to take in consideration all the characteristics associated when talking to a Distributed In Memory Cache, such as transient network failures.</span></span> <span data-ttu-id="70d79-171">캐시 사용의 모범 사례는 Microsoft Patterns & Practices [Azure 클라우드 응용 프로그램 설계 및 구현 지침](https://github.com/mspnp/azure-guidance)에서 [캐싱 지침](../best-practices-caching.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-171">For best practices on using Cache, see [Caching guidance](../best-practices-caching.md) from Microsoft Patterns & Practices [Azure Cloud Application Design and Implementation Guidance](https://github.com/mspnp/azure-guidance).</span></span>

<span data-ttu-id="70d79-172">세션 상태 및 기타 모범 사례에 대한 자세한 내용은 [웹 개발 모범 사례(Azure를 사용하는 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70d79-172">For more information about session state and other best practices, see [Web Development Best Practices (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70d79-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70d79-173">Next steps</span></span>
<span data-ttu-id="70d79-174">[Azure Redis Cache에 대한 ASP.NET 출력 캐시 제공자](cache-aspnet-output-cache-provider.md)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70d79-174">Check out the [ASP.NET Output Cache Provider for Azure Redis Cache](cache-aspnet-output-cache-provider.md).</span></span>

