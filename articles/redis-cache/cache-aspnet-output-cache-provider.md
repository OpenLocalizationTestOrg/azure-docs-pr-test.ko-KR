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
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Azure Redis Cache에 대한 ASP.NET 출력 캐시 공급자
hello Redis 출력 캐시 공급자는 출력 캐시 데이터에 대 한 out of process 저장소 메커니즘입니다. 이 데이터는 완전한 HTTP 응답(페이지 출력 캐싱)에 특별히 사용됩니다. hello 새로운 출력 캐시 공급자 확장 지점 ASP.NET 4에 도입 된 hello 공급자는 연결 합니다.

toouse hello Redis 출력 캐시 공급자는 먼저 캐시를 구성 하 고 hello Redis 출력 캐시 공급자 NuGet 패키지를 사용 하 여 ASP.NET 응용 프로그램을 구성 합니다. 이 항목에서는 응용 프로그램 toouse hello Redis 출력 캐시 공급자를 구성 하는 방법에 지침을 제공 합니다. Azure Redis Cache 인스턴스 생성 및 구성에 대한 자세한 내용은 [캐시 생성하기](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)을 참조하세요.

## <a name="store-aspnet-page-output-in-hello-cache"></a>Hello 캐시에 ASP.NET 페이지 출력 저장
tooconfigure hello Redis 캐시 세션 상태 NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램 클릭 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴.

실행 hello 다음 hello에서 명령을 `Package Manager Console` 창.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

hello Redis 출력 캐시 공급자 NuGet 패키지에 hello StackExchange.Redis.StrongName 패키지에 대 한 종속성입니다. Hello StackExchange.Redis.StrongName 패키지를 프로젝트에 없는 경우 설치 됩니다. Hello Redis 출력 캐시 공급자 NuGet 패키지에 대 한 자세한 내용은 참조 hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet 페이지.

>[!NOTE]
>또한 toohello 강력한 이름의 StackExchange.Redis.StrongName 패키지에 hello StackExchange.Redis 비-강력한 이름 버전도 됩니다. 프로젝트 hello 비-이름 StackExchange.Redis 버전을 제거 해야를 사용 하는 경우 그렇지 않으면 하면에서 이름 충돌이 발생 프로젝트입니다. 이 패키지에 대한 자세한 내용은 [.NET 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)을 참조하세요.
>
>

hello NuGet 패키지가 다운로드 되 고 추가 하는 hello 필요한 어셈블리 참조 및 hello 섹션을 web.config 파일에 다음 추가 되었습니다. 이 섹션에는 ASP.NET 응용 프로그램 toouse hello Redis 출력 캐시 공급자에 대 한 hello 필요한 구성을 포함 합니다.

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

hello 주석 섹션 hello 특성 및 각 특성에 대 한 샘플 설정의 예를 제공 합니다.

Hello 특성 hello hello Microsoft Azure 포털 내에서 캐시 블레이드의 값으로 구성 하 고 구성 필요에 따라 다른 값을 hello 합니다. 캐시 속성에 액세스 하는 방법은 [Redis 캐시 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.

* **호스트** – 캐시 끝점을 지정합니다.
* **포트** – 비 SSL 포트 또는 hello ssl 설정에 따라 SSL 포트를 사용 합니다.
* **accessKey** – hello 기본 또는 보조 키 중 하나를 사용 하 여 캐시 합니다.
* **ssl** – toosecure 캐시/클라이언트 통신에 ssl 사용 하려는 경우 true이 고, 그렇지 않으면 false입니다. 있는지 toospecify hello 올바른 포트 여야 합니다.
  * hello 비 SSL 포트는 새 캐시에 대해 기본적으로 비활성화 되어 있습니다. 이 설정은 toouse hello SSL 포트에 대해 true를 지정 합니다. Hello 비 SSL 포트를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 hello [액세스 포트](cache-configure.md#access-ports) hello 섹션인 [캐시 구성](cache-configure.md) 항목입니다.
* **databaseId** – 지정 된 캐시에 대 한 데이터베이스 toouse 어떤 데이터를 출력 합니다. 지정 하지 않으면 hello 기본값 0이 사용 됩니다.
* **applicationName** – `<AppName>_<SessionId>_Data`로 redis에 저장된 키입니다. 이 명명 스키마는 여러 응용 프로그램 tooshare hello를 통해 같은 키입니다. 이 매개변수는 선택적이며 사용자가 제공하지 않으면 기본값이 사용됩니다.
* **connectionTimeoutInMilliseconds** –이 설정을 통해 toooverride hello connectTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다. 지정 하지 않으면 5000 hello 기본 connectTimeout 설정이 사용 됩니다. 더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.
* **operationTimeoutInMilliseconds** –이 설정을 통해 toooverride hello syncTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다. 지정 하지 않으면 1000 hello 기본 syncTimeout 설정이 사용 됩니다. 더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.

Toocache hello 출력 원하는 OutputCache 지시문 tooeach 페이지를 추가 합니다.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

Hello 이전 예제에서는 hello 60 초 동안 hello 캐시에 남아 있는 데이터 페이지를 캐시 하 고 hello 페이지의 다른 버전이 각 매개 변수 조합에 대해 캐시 됩니다. Hello OutputCache 지시문에 대 한 자세한 내용은 참조 [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837)합니다.

다음이 단계를 수행 하 고 나면 응용 프로그램에 구성 된 toouse hello Redis 출력 캐시 공급자입니다.

## <a name="next-steps"></a>다음 단계
체크 아웃 hello [Azure Redis Cache 용 ASP.NET 세션 상태 공급자](cache-aspnet-session-state-provider.md)합니다.

