---
title: "Azure CDN에서 웹 콘텐츠의 만료 관리 | Microsoft Docs"
description: "Azure CDN에서 Azure Web Apps/Cloud Services, ASP.NET 또는 IIS 콘텐츠의 만료를 관리하는 방법을 알아봅니다."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="e36f5-103">Azure CDN에서 Azure Web Apps/Cloud Services, ASP.NET 또는 IIS 콘텐츠의 만료 관리</span><span class="sxs-lookup"><span data-stu-id="e36f5-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e36f5-104">Azure Web Apps/Cloud Services, ASP.NET 또는 IIS</span><span class="sxs-lookup"><span data-stu-id="e36f5-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="e36f5-105">Azure Storage Blob service</span><span class="sxs-lookup"><span data-stu-id="e36f5-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="e36f5-106">TTL (time-to-live)이 경과할 때까지 원본 웹 서버에서 공개적으로 액세스할 수 있는 파일은 Azure CDN에 캐시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="e36f5-107">TTL은 원본 서버의 HTTP 응답에 있는 [*Cache-Control* 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)에 기반하여 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="e36f5-108">이 문서에서는 Azure Web Apps, Azure Cloud Services, ASP.NET 응용 프로그램 및 IIS (Internet Information Services) 사이트에 대한 `Cache-Control` 헤더를 설정하는 방법을 설명하며, 이 헤더들은 모두 비슷하게 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="e36f5-109">파일에 TTL을 설정하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="e36f5-110">이 경우에 Azure CDN은 기본 TTL인 7일을 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="e36f5-111">파일과 다른 리소스에 대한 액세스 속도를 높이기 위해 Azure CDN이 작동하는 방법에 대한 자세한 내용은 [Azure CDN 개요](cdn-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e36f5-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="e36f5-112">구성 파일에 Cache-Control 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="e36f5-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="e36f5-113">이미지, 스타일 시트 등 정적 콘텐츠에 대해서는 웹 응용 프로그램의 **applicationHost.config** 또는 **web.config** 파일을 수정함으로써 업데이트 빈도를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="e36f5-114">구성 파일의 **system.webServer\staticContent\clientCache** 요소에는 콘텐츠에 대한 `Cache-Control` 헤더가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="e36f5-115">**web.config**의 구성 설정은 하위 폴더 수준에서 재정의된 경우를 제외하고는 폴더 및 그 하위 폴더의 모든 항목에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="e36f5-116">예를 들어 루트에서 모든 정적 콘텐츠가 3일간 캐시되지만 캐시 설정이 6시간인 추가 변수 콘텐츠가 포함된 하위 폴더가 있도록 기본 TTL(Time-To-Live)을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="e36f5-117">**applicationHost.config** 파일은 사이트의 모든 응용 프로그램에 영향을 주지만, 응용 프로그램의 **web.config** 파일에서 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="e36f5-118">다음 XML은 최대 기간을 3일로 지정하는 **clientCache** 설정 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e36f5-119">**UseMaxAge**를 지정하면 **CacheControlMaxAge** 특성에 지정된 값에 따라 `Cache-Control: max-age=<nnn>` 헤더를 응답에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="e36f5-120">**cacheControlMaxAge** 특성에 대한 시간 범위의 형식은 <days>.<hours>:<min>:<sec>입니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="e36f5-121">**clientCache** 노드에 대한 자세한 내용은 [클라이언트 캐시<clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e36f5-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="e36f5-122">코드에 Cache-Control 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="e36f5-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="e36f5-123">ASP.NET 응용 프로그램의 경우 **HttpResponse.Cache** 속성을 설정하면 CDN 캐싱 동작을 프로그래밍 방식으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="e36f5-124">**HttpResponse.Cache** 속성에 대한 자세한 내용은 [HttpResponse.Cache 속성](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 및 [HttpCachePolicy 클래스](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e36f5-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="e36f5-125">ASP.NET의 응용 프로그램 콘텐츠를 프로그래밍 방식으로 캐시하려면 HttpCacheability를 *Public*으로 설정하여 캐시 가능한 콘텐츠로 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="e36f5-126">또한 캐시 유효성 검사기가 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="e36f5-127">캐시 유효성 검사기는 SetLastModified를 호출하여 설정된 마지막으로 수정한 날짜 타임스탬프 또는 SetETag를 호출하여 설정된 etag 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="e36f5-128">필요에 따라, SetExpires를 호출하여 캐시 만료 시간을 지정하거나 이 문서의 앞부분에서 설명한 기본 캐시 추론을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="e36f5-129">예를 들어 1시간 동안의 콘텐츠를 캐시하려면 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e36f5-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="e36f5-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e36f5-130">Next Steps</span></span>
* [<span data-ttu-id="e36f5-131">**clientCache** 요소에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="e36f5-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="e36f5-132">**HttpResponse.Cache** 속성에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="e36f5-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="e36f5-133">[**HttpCachePolicy 클래스**에 대한 자세한 내용](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)</span><span class="sxs-lookup"><span data-stu-id="e36f5-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

