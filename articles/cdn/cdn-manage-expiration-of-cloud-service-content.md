---
title: "Azure CDN에서 웹 콘텐츠 aaaManage 만료 | Microsoft Docs"
description: "자세한 내용은 방법 Azure CDN에서 콘텐츠를 Azure 웹 앱/클라우드 서비스, ASP.NET 또는 IIS의 toomanage 만료 합니다."
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
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Azure CDN에서 Azure Web Apps/Cloud Services, ASP.NET 또는 IIS 콘텐츠의 만료 관리
> [!div class="op_single_selector"]
> * [Azure Web Apps/Cloud Services, ASP.NET 또는 IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure Storage Blob service](cdn-manage-expiration-of-blob-content.md)
> 
> 

TTL (time-to-live)이 경과할 때까지 원본 웹 서버에서 공개적으로 액세스할 수 있는 파일은 Azure CDN에 캐시될 수 있습니다.  hello TTL 따라 사용자가 hello [ *캐시 제어* 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello HTTP 응답 hello 원본 서버에서 합니다.  이 문서에서는 설명 방법을 tooset `Cache-Control` Azure 웹 앱, Azure 클라우드 서비스, ASP.NET 응용 프로그램 및는 모두 비슷하게 구성 된 인터넷 정보 서비스 사이트에 대 한 헤더입니다.

> [!TIP]
> 파일에 없는 TTL tooset를 선택할 수 있습니다.  이 경우에 Azure CDN은 기본 TTL인 7일을 자동으로 적용합니다.
> 
> Azure CDN toospeed 액세스 toofiles 및 기타 리소스를 작동 하는 방법에 대 한 자세한 내용은 참조 hello [Azure CDN 개요](cdn-overview.md)합니다.
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>구성 파일에 Cache-Control 헤더 설정
이미지와 스타일 시트 같은 정적 콘텐츠의 hello를 수정 하 여 hello 업데이트 빈도 제어할 수 있습니다 **applicationHost.config** 또는 **web.config** 웹 응용 프로그램에 대 한 파일입니다.  hello **system.webServer\staticContent\clientCache** hello 구성 파일의 요소는 hello 설정 `Cache-Control` 콘텐츠에 대 한 헤더입니다. 에 대 한 **web.config**, hello 구성 설정에 영향을 줍니다 모든 hello 폴더 및 모든 하위 폴더에서 hello 하위 수준에서 재정의 되지 않는 경우.  예를 들어 기본을 설정할 수 있습니다는 활성 시간 hello 루트 toohave 모든 정적 콘텐츠 3 일에 대 한 캐시 되지만 6 시간의 캐시 설정을 사용 하 여 콘텐츠 자세한 변수 된 하위 폴더에 있습니다.  에 대 한 **applicationHost.config**, hello 사이트의 모든 응용 프로그램은 영향을 받을 수 있지만에서 재정의할 수 있습니다 **web.config** hello 응용 프로그램의에서 파일입니다.

hello 다음 XML의 예가 나와 설정 **clientCache** toospecify a 3 일의 최대 수명:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

지정 **UseMaxAge** 추가 `Cache-Control: max-age=<nnn>` hello에 지정 된 hello 값을 기반으로 하는 헤더 toohello 응답 **CacheControlMaxAge** 특성입니다. hello hello timespan 형식이 hello에 대 한 **cacheControlMaxAge** 특성은 <days>.<hours>:<min>:<sec>합니다. Hello에 대 한 자세한 내용은 **clientCache** 노드를 참조 [클라이언트 캐시 <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)합니다.  

## <a name="setting-cache-control-headers-in-code"></a>코드에 Cache-Control 헤더 설정
ASP.NET 응용 프로그램에 대 한 여 설정할 수 있습니다 hello CDN 캐싱 동작 프로그래밍 방식으로 설정 하는 hello **HttpResponse.Cache** 속성입니다. Hello에 대 한 자세한 내용은 **HttpResponse.Cache** 속성 참조 [HttpResponse.Cache 속성](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 및 [HttpCachePolicy 클래스](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)합니다.  

너무 HttpCacheability를 설정 하 여 hello 콘텐츠도 표시 되어 있는지 확인 하려는 경우 ASP.NET에서 tooprogrammatically 응용 프로그램 콘텐츠,*공용*합니다. 또한 캐시 유효성 검사기가 설정되었는지 확인합니다. hello 캐시 유효성 검사기는 마지막으로 수정한 날짜 일 수 있습니다는 etag 값 또는 SetLastModified를 호출 하 여 설정 하는 타임 스탬프 SetETag를 호출 하 여 설정 합니다. 필요에 따라 선택 사항으로 SetExpires를 호출 하 여 캐시 만료 시간을 지정할 수도 있습니다 또는이 문서의 앞부분에서 설명한 hello 기본 캐시 추론에 의존할 수 있습니다.  

예를 들어 1 시간에 대 한 콘텐츠 toocache hello 다음을 추가 합니다.  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>다음 단계
* [Hello에 대 한 세부 정보를 읽어 **clientCache** 요소](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Hello에 대 한 설명서를 hello **HttpResponse.Cache** 속성](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Hello에 대 한 설명서를 hello **HttpCachePolicy 클래스**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)합니다.  

