---
title: "ASP.NET 세션 상태 공급자 aaaCache | Microsoft Docs"
description: "자세한 내용은 toostore ASP.NET 세션 상태 Azure Redis Cache를 사용 하는 방법"
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
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a><span data-ttu-id="51beb-103">Azure Redis Cache에 대한 ASP.NET 세션 상태 제공자</span><span class="sxs-lookup"><span data-stu-id="51beb-103">ASP.NET Session State Provider for Azure Redis Cache</span></span>
<span data-ttu-id="51beb-104">Azure Redis 캐시 세션 상태 공급자 toostore 메모리 보다는 캐시에 세션 상태를 사용 하거나 SQL Server에서 데이터베이스 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-104">Azure Redis Cache provides a session state provider that you can use toostore your session state in a cache rather than in-memory or in a SQL Server database.</span></span> <span data-ttu-id="51beb-105">toouse 캐싱 세션 상태 공급자 hello 하 고 먼저 캐시를 구성한 다음 hello Redis 캐시 세션 상태 NuGet 패키지를 사용 하 여 캐시에 대 한 ASP.NET 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-105">toouse hello caching session state provider, first configure your cache, and then configure your ASP.NET application for cache using hello Redis Cache Session State NuGet package.</span></span>

<span data-ttu-id="51beb-106">사용자 세션에 대 한 특정 형식의 상태를 저장 하는 실제 클라우드 앱 tooavoid에 실용적이 지 종종 하지만 몇 가지 접근 방식을 성능 및 확장성을 다른 항목 보다 더 많은 영향을 줄 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-106">It's often not practical in a real-world cloud app tooavoid storing some form of state for a user session, but some approaches impact performance and scalability more than others.</span></span> <span data-ttu-id="51beb-107">Toostore 상태를 설정한 경우 hello 가장 적합 한 솔루션 tookeep hello 양의 작은 상태 및 쿠키에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-107">If you have toostore state, hello best solution is tookeep hello amount of state small and store it in cookies.</span></span> <span data-ttu-id="51beb-108">불가능, hello 다음 최상의 방법 분산, 메모리 내 캐시에 대 한 공급자와 함께 toouse ASP.NET 세션 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-108">If that isn't feasible, hello next best solution is toouse ASP.NET session state with a provider for distributed, in-memory cache.</span></span> <span data-ttu-id="51beb-109">성능 및 확장성 측면에서 좋지 hello toouse 데이터베이스 백업된 세션 상태 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-109">hello worst solution from a performance and scalability standpoint is toouse a database backed session state provider.</span></span> <span data-ttu-id="51beb-110">이 항목에서는 Azure Redis Cache 용 ASP.NET 세션 상태 공급자 hello를 사용 하 여에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-110">This topic provides guidance on using hello ASP.NET Session State Provider for Azure Redis Cache.</span></span> <span data-ttu-id="51beb-111">다른 세션 상태 옵션에 대한 내용은 [ASP.NET 세션 상태 옵션](#aspnet-session-state-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-111">For information on other session state options, see [ASP.NET Session State options](#aspnet-session-state-options).</span></span>

## <a name="store-aspnet-session-state-in-hello-cache"></a><span data-ttu-id="51beb-112">Hello 캐시에 ASP.NET 세션 상태 저장</span><span class="sxs-lookup"><span data-stu-id="51beb-112">Store ASP.NET session state in hello cache</span></span>
<span data-ttu-id="51beb-113">tooconfigure hello Redis 캐시 세션 상태 NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램 클릭 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="51beb-113">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="51beb-114">실행 hello 다음 hello에서 명령을 `Package Manager Console` 창.</span><span class="sxs-lookup"><span data-stu-id="51beb-114">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> <span data-ttu-id="51beb-115">Hello hello 프리미엄 계층에서 클러스터링 기능을 사용 하는 경우 사용 해야 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 높이 거 나 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-115">If you are using hello clustering feature from hello premium tier, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="51beb-116">Too2.0.1 이동 하거나 더 높은 것은 주요한 변경; 자세한 내용은 참조 [v2.0.0 주요 변경 내용은](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-116">Moving too2.0.1 or higher is a breaking change; for more information, see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span> <span data-ttu-id="51beb-117">이 문서 업데이트의 hello 시 hello 현재이 패키지의 버전이 2.2.3 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-117">At hello time of this article update, hello current version of this package is 2.2.3.</span></span>
> 
> 

<span data-ttu-id="51beb-118">hello Redis 세션 상태 공급자 NuGet 패키지에 hello StackExchange.Redis.StrongName 패키지에 대 한 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-118">hello Redis Session State Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="51beb-119">Hello StackExchange.Redis.StrongName 패키지를 프로젝트에 없는 경우 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-119">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span>

>[!NOTE]
><span data-ttu-id="51beb-120">또한 toohello 강력한 이름의 StackExchange.Redis.StrongName 패키지에 hello StackExchange.Redis 비-강력한 이름 버전도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-120">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="51beb-121">프로젝트 hello 비-이름 StackExchange.Redis 버전을 제거 해야를 사용 하는 경우 그렇지 않으면 하면에서 이름 충돌이 발생 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-121">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="51beb-122">이 패키지에 대한 자세한 내용은 [.NET 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-122">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="51beb-123">hello NuGet 패키지가 다운로드 되 고 추가 하는 hello 필요한 어셈블리 참조 및 hello 섹션을 web.config 파일에 다음 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-123">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="51beb-124">이 섹션에는 ASP.NET 응용 프로그램 toouse hello Redis Cache 세션 상태 공급자에 대 한 hello 필요한 구성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-124">This section contains hello required configuration for your ASP.NET application toouse hello Redis Cache Session State Provider.</span></span>

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

<span data-ttu-id="51beb-125">hello 주석 섹션 hello 특성 및 각 특성에 대 한 샘플 설정의 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-125">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="51beb-126">Hello 특성 hello hello Microsoft Azure 포털 내에서 캐시 블레이드의 값으로 구성 하 고 구성 필요에 따라 다른 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-126">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="51beb-127">캐시 속성에 액세스 하는 방법은 [Redis 캐시 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-127">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="51beb-128">**호스트** – 캐시 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-128">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="51beb-129">**포트** – 비 SSL 포트 또는 hello ssl 설정에 따라 SSL 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-129">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="51beb-130">**accessKey** – hello 기본 또는 보조 키 중 하나를 사용 하 여 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-130">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="51beb-131">**ssl** – toosecure 캐시/클라이언트 통신에 ssl 사용 하려는 경우 true이 고, 그렇지 않으면 false입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-131">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="51beb-132">있는지 toospecify hello 올바른 포트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-132">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="51beb-133">hello 비 SSL 포트는 새 캐시에 대해 기본적으로 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-133">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="51beb-134">이 설정은 toouse hello SSL 포트에 대해 true를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-134">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="51beb-135">Hello 비 SSL 포트를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 hello [액세스 포트](cache-configure.md#access-ports) hello 섹션인 [캐시 구성](cache-configure.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-135">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="51beb-136">**throwOnError** – 자동으로 hello 작업 toofail 사용 하려는 경우 오류 또는 false 발생 한 경우 throw 되는 예외 toobe 하려는 경우 true입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-136">**throwOnError** – true if you want an exception toobe thrown if there is a failure, or false if you want hello operation toofail silently.</span></span> <span data-ttu-id="51beb-137">Hello 정적 Microsoft.Web.Redis.RedisSessionStateProvider.LastException 속성을 확인 하 여 오류를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-137">You can check for a failure by checking hello static Microsoft.Web.Redis.RedisSessionStateProvider.LastException property.</span></span> <span data-ttu-id="51beb-138">hello 기본값은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-138">hello default is true.</span></span>
* <span data-ttu-id="51beb-139">**retryTimeoutInMilliseconds** – 이 간격 동안 실패한 작업이 다시 시도되며 밀리초 단위로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-139">**retryTimeoutInMilliseconds** – Operations that fail are retried during this interval, specified in milliseconds.</span></span> <span data-ttu-id="51beb-140">hello 첫 번째 다시 시도 20 밀리초 후 발생 하 고 다시 시도 hello retryTimeoutInMilliseconds 간격이 만료 될 때까지 1 초 마다 발생 하는 다음 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-140">hello first retry occurs after 20 milliseconds, and then retries occur every second until hello retryTimeoutInMilliseconds interval expires.</span></span> <span data-ttu-id="51beb-141">이 간격 후 즉시 hello 작업을 마지막으로 한 번 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-141">Immediately after this interval, hello operation is retried one final time.</span></span> <span data-ttu-id="51beb-142">Hello 작업이 계속 실패 하면 hello throwOnError 설정에 따라 toohello 호출자 hello 예외가 다시 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-142">If hello operation still fails, hello exception is thrown back toohello caller, depending on hello throwOnError setting.</span></span> <span data-ttu-id="51beb-143">hello 기본값은 0 이며 다시 시도 안 함입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-143">hello default value is 0, which means no retries.</span></span>
* <span data-ttu-id="51beb-144">**databaseId** – 어떤 데이터베이스 toouse 캐시에 대 한 출력 데이터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-144">**databaseId** – Specifies which database toouse for cache output data.</span></span> <span data-ttu-id="51beb-145">지정 하지 않으면 hello 기본값 0이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-145">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="51beb-146">**applicationName** – `{<Application Name>_<Session ID>}_Data`로 redis에 저장된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-146">**applicationName** – Keys are stored in redis as `{<Application Name>_<Session ID>}_Data`.</span></span> <span data-ttu-id="51beb-147">이 명명 스키마를 사용 하면 여러 응용 프로그램 tooshare hello Redis 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-147">This naming scheme enables multiple applications tooshare hello same Redis instance.</span></span> <span data-ttu-id="51beb-148">이 매개변수는 선택적이며 사용자가 제공하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-148">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="51beb-149">**connectionTimeoutInMilliseconds** –이 설정을 통해 toooverride hello connectTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-149">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="51beb-150">지정 하지 않으면 5000 hello 기본 connectTimeout 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-150">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="51beb-151">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-151">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="51beb-152">**operationTimeoutInMilliseconds** –이 설정을 통해 toooverride hello syncTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-152">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="51beb-153">지정 하지 않으면 1000 hello 기본 syncTimeout 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-153">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="51beb-154">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-154">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="51beb-155">이러한 속성에 대 한 자세한 내용은 참조 hello 원래 블로그 게시물 공지를 [Redis 용 ASP.NET 세션 상태 공급자 발표](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-155">For more information about these properties, see hello original blog post announcement at [Announcing ASP.NET Session State Provider for Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).</span></span>

<span data-ttu-id="51beb-156">Hello 표준 InProc 세션 상태 공급자 섹션을 web.config 파일에 toocomment를 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="51beb-156">Don’t forget toocomment out hello standard InProc session state provider section in your web.config.</span></span>

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

<span data-ttu-id="51beb-157">다음이 단계를 수행 하 고 나면 응용 프로그램에 구성 된 toouse hello Redis Cache 세션 상태 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-157">Once these steps are performed, your application is configured toouse hello Redis Cache Session State Provider.</span></span> <span data-ttu-id="51beb-158">응용 프로그램에서 세션 상태를 사용하는 경우 Azure Redis Cache 인스턴스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-158">When you use session state in your application, it is stored in an Azure Redis Cache instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51beb-159">Hello 캐시에 저장 된 데이터를 직렬화 가능 해야, hello에 저장할 수 있는 hello 데이터 달리 기본 메모리 내 ASP.NET 세션 상태 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-159">Data stored in hello cache must be serializable, unlike hello data that can be stored in hello default in-memory ASP.NET Session State Provider.</span></span> <span data-ttu-id="51beb-160">Hello Redis 용 세션 상태 공급자를 사용할 경우 세션 상태에 저장 되는 hello 데이터 형식이 되는지 직렬화 가능 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-160">When hello Session State Provider for Redis is used, be sure that hello data types that are being stored in session state are serializable.</span></span>
> 
> 

## <a name="aspnet-session-state-options"></a><span data-ttu-id="51beb-161">ASP.NET 세션 상태 옵션</span><span class="sxs-lookup"><span data-stu-id="51beb-161">ASP.NET Session State options</span></span>
* <span data-ttu-id="51beb-162">메모리 내 세션 상태 공급자-이 공급자는 메모리에 hello 세션 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-162">In Memory Session State Provider - This provider stores hello Session State in memory.</span></span> <span data-ttu-id="51beb-163">이 공급자를 사용 하 여 hello 이점은 단순 하 고 빠른입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-163">hello benefit of using this provider is it is simple and fast.</span></span> <span data-ttu-id="51beb-164">그러나 배포되지 않는 메모리 공급자에서 사용 중인 경우 웹앱의 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-164">However you cannot scale your Web Apps if you are using in memory provider since it is not distributed.</span></span>
* <span data-ttu-id="51beb-165">Sql Server 세션 상태 공급자-이 공급자는 Sql Server의 hello 세션 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-165">Sql Server Session State Provider - This provider stores hello Session State in Sql Server.</span></span> <span data-ttu-id="51beb-166">영구 저장소에서 toostore hello 세션 상태를 원하는 경우이 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-166">Use this provider if you want toostore hello Session state in persistent storage.</span></span> <span data-ttu-id="51beb-167">Web App의 크기를 조정할 수 있지만 세션에 SQL Server를 사용하면 Web App의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-167">You can scale your Web App but using Sql Server for Session has a performance impact on your Web App.</span></span>
* <span data-ttu-id="51beb-168">배포에 메모리 세션 상태 공급자 Redis Cache 세션 상태 공급자-이 공급자에서는 장점 hello 등입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-168">Distributed In Memory Session State Provider such as Redis Cache Session State Provider - This provider gives you hello best of both worlds.</span></span> <span data-ttu-id="51beb-169">Web App에는 빠르고 간단하며 확장성 있는 세션 상태 제공자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-169">Your Web App can have a simple, fast, and scalable Session State Provider.</span></span> <span data-ttu-id="51beb-170">이 공급자 저장소 hello 앱 캐시에 세션 상태 고려 사항에서 tootake 갖기 때문에 모든 hello 통하게 tooa 일시적인 네트워크 오류 등의 메모리 캐시에 분산 될 때 연결 된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-170">Because this provider stores hello Session state in a Cache, your app has tootake in consideration all hello characteristics associated when talking tooa Distributed In Memory Cache, such as transient network failures.</span></span> <span data-ttu-id="51beb-171">캐시 사용의 모범 사례는 Microsoft Patterns & Practices [Azure 클라우드 응용 프로그램 설계 및 구현 지침](https://github.com/mspnp/azure-guidance)에서 [캐싱 지침](../best-practices-caching.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-171">For best practices on using Cache, see [Caching guidance](../best-practices-caching.md) from Microsoft Patterns & Practices [Azure Cloud Application Design and Implementation Guidance](https://github.com/mspnp/azure-guidance).</span></span>

<span data-ttu-id="51beb-172">세션 상태 및 기타 모범 사례에 대한 자세한 내용은 [웹 개발 모범 사례(Azure를 사용하는 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51beb-172">For more information about session state and other best practices, see [Web Development Best Practices (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51beb-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51beb-173">Next steps</span></span>
<span data-ttu-id="51beb-174">체크 아웃 hello [Azure Redis Cache 용 ASP.NET 출력 캐시 공급자](cache-aspnet-output-cache-provider.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="51beb-174">Check out hello [ASP.NET Output Cache Provider for Azure Redis Cache](cache-aspnet-output-cache-provider.md).</span></span>

