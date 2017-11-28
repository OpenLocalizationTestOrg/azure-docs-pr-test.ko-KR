---
title: "Azure 앱 서비스에서 Azure Redis 캐시와 aaaSession 상태"
description: "Toouse hello Azure 캐시 서비스 toosupport ASP.NET 세션 상태 캐싱 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="27359-103">Azure 앱 서비스에서 Azure Redis 캐시를 사용하는 세션 상태</span><span class="sxs-lookup"><span data-stu-id="27359-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="27359-104">이 항목에서는 toouse Azure Redis 캐시 서비스 세션 상태에 대 한 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="27359-105">ASP.NET 웹 응용 프로그램 세션 상태를 사용 하는 외부 세션 상태 공급자 (hello Redis 캐시 서비스 또는 SQL Server 세션 상태 공급자) tooconfigure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="27359-106">세션 상태를 사용 하 고 외부 공급자를 사용 하지 않는 경우에 웹 응용 프로그램의 제한 된 tooone 인스턴스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27359-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="27359-107">hello Redis 캐시 서비스는 hello 빠르고 간편한 tooenable입니다.</span><span class="sxs-lookup"><span data-stu-id="27359-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="27359-108"><a id="createcache"></a>Hello 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="27359-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="27359-109">에 따라 [이러한 방향은](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="27359-110"><a id="configureproject"></a>Hello RedisSessionStateProvider NuGet 패키지 tooyour 웹 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="27359-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="27359-111">Hello NuGet 설치 `RedisSessionStateProvider` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="27359-112">사용 하 여 hello 다음 명령은 hello 패키지 관리자 콘솔에서 tooinstall (**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**):</span><span class="sxs-lookup"><span data-stu-id="27359-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="27359-113">tooinstall **도구** > **NuGet 패키지 관리자** > **덩어리 패키지를 솔루션에 대 한 관리**, 검색할 `RedisSessionStateProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="27359-114">자세한 내용은 참조 hello [NuGet RedisSessionStateProvider 페이지](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) 및 [hello 캐시 클라이언트 구성](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet)합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="27359-115"><a id="configurewebconfig"></a>Hello Web.Config 파일 수정</span><span class="sxs-lookup"><span data-stu-id="27359-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="27359-116">Hello에 스텁 항목을 추가 하는 hello NuGet 패키지를 toomaking 어셈블리 캐시에 대 한 참조 하는 또한 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="27359-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="27359-117">열기 hello *web.config* hello hello 및 **sessionState** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="27359-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="27359-118">Hello 값을 입력 `host`, `accessKey`, `port` (SSL 포트 hello 6380 이어야 함)을 설정 하 고 `SSL` 너무`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="27359-119">Hello에서 이러한 값을 가져올 수 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715) 블레이드 캐시 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="27359-120">자세한 내용은 참조 [toohello 캐시 연결](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache)합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="27359-121">Hello 비 SSL 포트 새 캐시에 대해 기본적으로 해제 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="27359-122">Hello 비 SSL 포트를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 hello [액세스 포트](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) hello 섹션인 [Azure Redis Cache에서 캐시 구성](https://msdn.microsoft.com/library/azure/dn793612.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="27359-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="27359-123">hello 다음 태그를 보여 줍니다 hello 변경 toohello *web.config* 파일이, 특히 hello 변경 너무*포트*, *호스트*, accessKey * 및 *ssl*.</span><span class="sxs-lookup"><span data-stu-id="27359-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <span data-ttu-id="27359-124"><a id="usesessionobject"></a>Hello 세션 개체를 사용 하 여 코드에서</span><span class="sxs-lookup"><span data-stu-id="27359-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="27359-125">hello 최종 단계 toobegin hello 세션 개체를 사용 하 여 ASP.NET 코드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="27359-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="27359-126">Hello를 사용 하 여 개체 toosession 상태를 추가한 **Session.Add** 메서드.</span><span class="sxs-lookup"><span data-stu-id="27359-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="27359-127">이 메서드는 hello 세션 상태 캐시의 키-값 쌍 toostore 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="27359-128">hello 코드 다음 세션 상태에서이 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="27359-129">웹 앱의 hello Redis Cache toocache 개체를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27359-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="27359-130">자세한 내용은 [Azure Redis 캐시를 사용한 MVC 동영상 앱(15분)](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27359-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="27359-131">방법에 대 한 자세한 내용은 toouse ASP.NET 세션 상태 참조 [ASP.NET 세션 상태 개요][ASP.NET Session State Overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="27359-132">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="27359-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="27359-133">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27359-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="27359-134">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="27359-134">What's changed</span></span>
* <span data-ttu-id="27359-135">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="27359-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="27359-136">*작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="27359-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

