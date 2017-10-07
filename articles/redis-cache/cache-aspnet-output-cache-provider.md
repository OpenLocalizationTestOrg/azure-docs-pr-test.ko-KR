---
title: "aaaCache ASP.NET 출력 캐시 공급자"
description: "자세한 내용은 Azure Redis Cache를 사용 하 여 toocache ASP.NET 페이지 출력 하는 방법"
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
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="16f29-103">Azure Redis Cache에 대한 ASP.NET 출력 캐시 공급자</span><span class="sxs-lookup"><span data-stu-id="16f29-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="16f29-104">hello Redis 출력 캐시 공급자는 출력 캐시 데이터에 대 한 out of process 저장소 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="16f29-105">이 데이터는 완전한 HTTP 응답(페이지 출력 캐싱)에 특별히 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="16f29-106">hello 새로운 출력 캐시 공급자 확장 지점 ASP.NET 4에 도입 된 hello 공급자는 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="16f29-107">toouse hello Redis 출력 캐시 공급자는 먼저 캐시를 구성 하 고 hello Redis 출력 캐시 공급자 NuGet 패키지를 사용 하 여 ASP.NET 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="16f29-108">이 항목에서는 응용 프로그램 toouse hello Redis 출력 캐시 공급자를 구성 하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="16f29-109">Azure Redis Cache 인스턴스 생성 및 구성에 대한 자세한 내용은 [캐시 생성하기](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16f29-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="16f29-110">Hello 캐시에 ASP.NET 페이지 출력 저장</span><span class="sxs-lookup"><span data-stu-id="16f29-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="16f29-111">tooconfigure hello Redis 캐시 세션 상태 NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램 클릭 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="16f29-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="16f29-112">실행 hello 다음 hello에서 명령을 `Package Manager Console` 창.</span><span class="sxs-lookup"><span data-stu-id="16f29-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="16f29-113">hello Redis 출력 캐시 공급자 NuGet 패키지에 hello StackExchange.Redis.StrongName 패키지에 대 한 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="16f29-114">Hello StackExchange.Redis.StrongName 패키지를 프로젝트에 없는 경우 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="16f29-115">Hello Redis 출력 캐시 공급자 NuGet 패키지에 대 한 자세한 내용은 참조 hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet 페이지.</span><span class="sxs-lookup"><span data-stu-id="16f29-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="16f29-116">또한 toohello 강력한 이름의 StackExchange.Redis.StrongName 패키지에 hello StackExchange.Redis 비-강력한 이름 버전도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="16f29-117">프로젝트 hello 비-이름 StackExchange.Redis 버전을 제거 해야를 사용 하는 경우 그렇지 않으면 하면에서 이름 충돌이 발생 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="16f29-118">이 패키지에 대한 자세한 내용은 [.NET 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16f29-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="16f29-119">hello NuGet 패키지가 다운로드 되 고 추가 하는 hello 필요한 어셈블리 참조 및 hello 섹션을 web.config 파일에 다음 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="16f29-120">이 섹션에는 ASP.NET 응용 프로그램 toouse hello Redis 출력 캐시 공급자에 대 한 hello 필요한 구성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="16f29-121">hello 주석 섹션 hello 특성 및 각 특성에 대 한 샘플 설정의 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="16f29-122">Hello 특성 hello hello Microsoft Azure 포털 내에서 캐시 블레이드의 값으로 구성 하 고 구성 필요에 따라 다른 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="16f29-123">캐시 속성에 액세스 하는 방법은 [Redis 캐시 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16f29-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="16f29-124">**호스트** – 캐시 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="16f29-125">**포트** – 비 SSL 포트 또는 hello ssl 설정에 따라 SSL 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="16f29-126">**accessKey** – hello 기본 또는 보조 키 중 하나를 사용 하 여 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="16f29-127">**ssl** – toosecure 캐시/클라이언트 통신에 ssl 사용 하려는 경우 true이 고, 그렇지 않으면 false입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="16f29-128">있는지 toospecify hello 올바른 포트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="16f29-129">hello 비 SSL 포트는 새 캐시에 대해 기본적으로 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="16f29-130">이 설정은 toouse hello SSL 포트에 대해 true를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="16f29-131">Hello 비 SSL 포트를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 hello [액세스 포트](cache-configure.md#access-ports) hello 섹션인 [캐시 구성](cache-configure.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="16f29-132">**databaseId** – 지정 된 캐시에 대 한 데이터베이스 toouse 어떤 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="16f29-133">지정 하지 않으면 hello 기본값 0이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="16f29-134">**applicationName** – `<AppName>_<SessionId>_Data`로 redis에 저장된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="16f29-135">이 명명 스키마는 여러 응용 프로그램 tooshare hello를 통해 같은 키입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="16f29-136">이 매개변수는 선택적이며 사용자가 제공하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="16f29-137">**connectionTimeoutInMilliseconds** –이 설정을 통해 toooverride hello connectTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="16f29-138">지정 하지 않으면 5000 hello 기본 connectTimeout 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="16f29-139">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16f29-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="16f29-140">**operationTimeoutInMilliseconds** –이 설정을 통해 toooverride hello syncTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="16f29-141">지정 하지 않으면 1000 hello 기본 syncTimeout 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="16f29-142">더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16f29-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="16f29-143">Toocache hello 출력 원하는 OutputCache 지시문 tooeach 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="16f29-144">Hello 이전 예제에서는 hello 60 초 동안 hello 캐시에 남아 있는 데이터 페이지를 캐시 하 고 hello 페이지의 다른 버전이 각 매개 변수 조합에 대해 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="16f29-145">Hello OutputCache 지시문에 대 한 자세한 내용은 참조 [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837)합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="16f29-146">다음이 단계를 수행 하 고 나면 응용 프로그램에 구성 된 toouse hello Redis 출력 캐시 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16f29-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16f29-147">Next steps</span></span>
<span data-ttu-id="16f29-148">체크 아웃 hello [Azure Redis Cache 용 ASP.NET 세션 상태 공급자](cache-aspnet-session-state-provider.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16f29-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

