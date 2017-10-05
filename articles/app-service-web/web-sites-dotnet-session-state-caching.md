---
title: "Azure 앱 서비스에서 Azure Redis 캐시를 사용하는 세션 상태"
description: "Azure 캐시 서비스를 사용하여 ASP.NET 세션 상태 캐싱을 지원하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="f32f7-103">Azure 앱 서비스에서 Azure Redis 캐시를 사용하는 세션 상태</span><span class="sxs-lookup"><span data-stu-id="f32f7-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="f32f7-104">이 항목에서는 세션 상태에 Azure Redis 캐시 서비스를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="f32f7-105">ASP.NET 웹 앱에서 세션 상태를 사용하는 경우 외부 세션 상태 공급자(Redis 캐시 서비스 또는 SQL Server 세션 상태 공급자)를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="f32f7-106">세션 상태를 사용하는 경우 외부 공급자를 사용하지 않으면 웹 앱의 인스턴스가 하나로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="f32f7-107">Redis 캐시 서비스는 가장 빠르고 간편하게 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="f32f7-108"><a id="createcache"></a>캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="f32f7-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="f32f7-109">캐시를 만들려면 [다음 지침](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache)을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f32f7-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="f32f7-110"><a id="configureproject"></a>웹앱에 RedisSessionStateProvider NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="f32f7-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="f32f7-111">NuGet `RedisSessionStateProvider` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="f32f7-112">다음 명령을 사용하여 패키지 관리자 콘솔에서 설치합니다(**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**):</span><span class="sxs-lookup"><span data-stu-id="f32f7-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="f32f7-113">**도구** > **NuGet 패키지 관리자** > **솔루션의 NuGet 패키지 관리**에서 설치하려면 `RedisSessionStateProvider`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="f32f7-114">자세한 내용은 [NuGet RedisSessionStateProvider 페이지](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) 및 [캐시 클라이언트 구성](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f32f7-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="f32f7-115"><a id="configurewebconfig"></a>Web.Config 파일 수정</span><span class="sxs-lookup"><span data-stu-id="f32f7-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="f32f7-116">NuGet 패키지는 캐시에 대한 어셈블리 참조를 만들 뿐 아니라 *web.config* 파일에 스텁 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="f32f7-117">*web.config* 를 열고 **sessionState** 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="f32f7-118">`host`, `accessKey`, `port`(SSL 포트는 6380이어야 함) 값을 입력하고 `SSL`를 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="f32f7-119">이러한 값은 캐시 인스턴스에 대한 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715) 블레이드에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="f32f7-120">자세한 내용은 [캐시에 연결](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f32f7-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="f32f7-121">비 SSL 포트는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="f32f7-122">비-SSL 포트 사용 방법에 대한 자세한 내용은 [Azure Redis Cache에서 캐시 구성](https://msdn.microsoft.com/library/azure/dn793612.aspx) 토픽의 [액세스 포트](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f32f7-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="f32f7-123">변경 내용을 표시 하는 다음 태그는 *web.config* 파일을 변경 하려면 특별히 *포트*, *호스트*, accessKey * 및 *ssl* .</span><span class="sxs-lookup"><span data-stu-id="f32f7-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="f32f7-124"><a id="usesessionobject"></a> 코드에서 Session 개체 사용</span><span class="sxs-lookup"><span data-stu-id="f32f7-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="f32f7-125">마지막 단계는 ASP.NET 코드에서 Session 개체 사용을 시작하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="f32f7-126">**Session.Add** 메서드를 사용하여 세션 상태에 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="f32f7-127">이 메서드는 키-값 쌍을 사용하여 세션 상태 캐시에 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="f32f7-128">다음 코드를 사용하면 세션 상태에서 이 값이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="f32f7-129">Redis 캐시를 사용하여 웹 앱에서 개체를 캐시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="f32f7-130">자세한 내용은 [Azure Redis 캐시를 사용한 MVC 동영상 앱(15분)](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f32f7-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="f32f7-131">ASP.NET 세션 상태 사용 방법에 대한 자세한 내용은 [ASP.NET 세션 상태 개요][ASP.NET Session State Overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f32f7-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="f32f7-132">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f32f7-133">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f32f7-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f32f7-134">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="f32f7-134">What's changed</span></span>
* <span data-ttu-id="f32f7-135">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f32f7-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="f32f7-136">*작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="f32f7-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

