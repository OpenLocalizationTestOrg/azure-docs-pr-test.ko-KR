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
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Azure Redis Cache에 대한 ASP.NET 세션 상태 제공자
Azure Redis 캐시 세션 상태 공급자 toostore 메모리 보다는 캐시에 세션 상태를 사용 하거나 SQL Server에서 데이터베이스 수를 제공 합니다. toouse 캐싱 세션 상태 공급자 hello 하 고 먼저 캐시를 구성한 다음 hello Redis 캐시 세션 상태 NuGet 패키지를 사용 하 여 캐시에 대 한 ASP.NET 응용 프로그램을 구성 합니다.

사용자 세션에 대 한 특정 형식의 상태를 저장 하는 실제 클라우드 앱 tooavoid에 실용적이 지 종종 하지만 몇 가지 접근 방식을 성능 및 확장성을 다른 항목 보다 더 많은 영향을 줄 합니다. Toostore 상태를 설정한 경우 hello 가장 적합 한 솔루션 tookeep hello 양의 작은 상태 및 쿠키에 저장 합니다. 불가능, hello 다음 최상의 방법 분산, 메모리 내 캐시에 대 한 공급자와 함께 toouse ASP.NET 세션 상태입니다. 성능 및 확장성 측면에서 좋지 hello toouse 데이터베이스 백업된 세션 상태 공급자입니다. 이 항목에서는 Azure Redis Cache 용 ASP.NET 세션 상태 공급자 hello를 사용 하 여에 지침을 제공 합니다. 다른 세션 상태 옵션에 대한 내용은 [ASP.NET 세션 상태 옵션](#aspnet-session-state-options)을 참조하세요.

## <a name="store-aspnet-session-state-in-hello-cache"></a>Hello 캐시에 ASP.NET 세션 상태 저장
tooconfigure hello Redis 캐시 세션 상태 NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램 클릭 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴.

실행 hello 다음 hello에서 명령을 `Package Manager Console` 창.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Hello hello 프리미엄 계층에서 클러스터링 기능을 사용 하는 경우 사용 해야 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 높이 거 나 예외를 throw 합니다. Too2.0.1 이동 하거나 더 높은 것은 주요한 변경; 자세한 내용은 참조 [v2.0.0 주요 변경 내용은](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)합니다. 이 문서 업데이트의 hello 시 hello 현재이 패키지의 버전이 2.2.3 합니다.
> 
> 

hello Redis 세션 상태 공급자 NuGet 패키지에 hello StackExchange.Redis.StrongName 패키지에 대 한 종속성입니다. Hello StackExchange.Redis.StrongName 패키지를 프로젝트에 없는 경우 설치 됩니다.

>[!NOTE]
>또한 toohello 강력한 이름의 StackExchange.Redis.StrongName 패키지에 hello StackExchange.Redis 비-강력한 이름 버전도 됩니다. 프로젝트 hello 비-이름 StackExchange.Redis 버전을 제거 해야를 사용 하는 경우 그렇지 않으면 하면에서 이름 충돌이 발생 프로젝트입니다. 이 패키지에 대한 자세한 내용은 [.NET 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)을 참조하세요.
>
>

hello NuGet 패키지가 다운로드 되 고 추가 하는 hello 필요한 어셈블리 참조 및 hello 섹션을 web.config 파일에 다음 추가 되었습니다. 이 섹션에는 ASP.NET 응용 프로그램 toouse hello Redis Cache 세션 상태 공급자에 대 한 hello 필요한 구성을 포함 합니다.

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

hello 주석 섹션 hello 특성 및 각 특성에 대 한 샘플 설정의 예를 제공 합니다.

Hello 특성 hello hello Microsoft Azure 포털 내에서 캐시 블레이드의 값으로 구성 하 고 구성 필요에 따라 다른 값을 hello 합니다. 캐시 속성에 액세스 하는 방법은 [Redis 캐시 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.

* **호스트** – 캐시 끝점을 지정합니다.
* **포트** – 비 SSL 포트 또는 hello ssl 설정에 따라 SSL 포트를 사용 합니다.
* **accessKey** – hello 기본 또는 보조 키 중 하나를 사용 하 여 캐시 합니다.
* **ssl** – toosecure 캐시/클라이언트 통신에 ssl 사용 하려는 경우 true이 고, 그렇지 않으면 false입니다. 있는지 toospecify hello 올바른 포트 여야 합니다.
  * hello 비 SSL 포트는 새 캐시에 대해 기본적으로 비활성화 되어 있습니다. 이 설정은 toouse hello SSL 포트에 대해 true를 지정 합니다. Hello 비 SSL 포트를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 hello [액세스 포트](cache-configure.md#access-ports) hello 섹션인 [캐시 구성](cache-configure.md) 항목입니다.
* **throwOnError** – 자동으로 hello 작업 toofail 사용 하려는 경우 오류 또는 false 발생 한 경우 throw 되는 예외 toobe 하려는 경우 true입니다. Hello 정적 Microsoft.Web.Redis.RedisSessionStateProvider.LastException 속성을 확인 하 여 오류를 확인할 수 있습니다. hello 기본값은 true입니다.
* **retryTimeoutInMilliseconds** – 이 간격 동안 실패한 작업이 다시 시도되며 밀리초 단위로 지정됩니다. hello 첫 번째 다시 시도 20 밀리초 후 발생 하 고 다시 시도 hello retryTimeoutInMilliseconds 간격이 만료 될 때까지 1 초 마다 발생 하는 다음 키를 누릅니다. 이 간격 후 즉시 hello 작업을 마지막으로 한 번 다시 시도 합니다. Hello 작업이 계속 실패 하면 hello throwOnError 설정에 따라 toohello 호출자 hello 예외가 다시 throw 됩니다. hello 기본값은 0 이며 다시 시도 안 함입니다.
* **databaseId** – 어떤 데이터베이스 toouse 캐시에 대 한 출력 데이터를 지정 합니다. 지정 하지 않으면 hello 기본값 0이 사용 됩니다.
* **applicationName** – `{<Application Name>_<Session ID>}_Data`로 redis에 저장된 키입니다. 이 명명 스키마를 사용 하면 여러 응용 프로그램 tooshare hello Redis 동일 합니다. 이 매개변수는 선택적이며 사용자가 제공하지 않으면 기본값이 사용됩니다.
* **connectionTimeoutInMilliseconds** –이 설정을 통해 toooverride hello connectTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다. 지정 하지 않으면 5000 hello 기본 connectTimeout 설정이 사용 됩니다. 더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.
* **operationTimeoutInMilliseconds** –이 설정을 통해 toooverride hello syncTimeout hello StackExchange.Redis 클라이언트에서 설정 합니다. 지정 하지 않으면 1000 hello 기본 syncTimeout 설정이 사용 됩니다. 더 자세한 내용은 [StackExchange.Redis 구성 모델](http://go.microsoft.com/fwlink/?LinkId=398705)을 참조하세요.

이러한 속성에 대 한 자세한 내용은 참조 hello 원래 블로그 게시물 공지를 [Redis 용 ASP.NET 세션 상태 공급자 발표](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)합니다.

Hello 표준 InProc 세션 상태 공급자 섹션을 web.config 파일에 toocomment를 잊지 마십시오.

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

다음이 단계를 수행 하 고 나면 응용 프로그램에 구성 된 toouse hello Redis Cache 세션 상태 공급자입니다. 응용 프로그램에서 세션 상태를 사용하는 경우 Azure Redis Cache 인스턴스에 저장됩니다.

> [!IMPORTANT]
> Hello 캐시에 저장 된 데이터를 직렬화 가능 해야, hello에 저장할 수 있는 hello 데이터 달리 기본 메모리 내 ASP.NET 세션 상태 공급자입니다. Hello Redis 용 세션 상태 공급자를 사용할 경우 세션 상태에 저장 되는 hello 데이터 형식이 되는지 직렬화 가능 해야 합니다.
> 
> 

## <a name="aspnet-session-state-options"></a>ASP.NET 세션 상태 옵션
* 메모리 내 세션 상태 공급자-이 공급자는 메모리에 hello 세션 상태를 저장 합니다. 이 공급자를 사용 하 여 hello 이점은 단순 하 고 빠른입니다. 그러나 배포되지 않는 메모리 공급자에서 사용 중인 경우 웹앱의 크기를 조정할 수 없습니다.
* Sql Server 세션 상태 공급자-이 공급자는 Sql Server의 hello 세션 상태를 저장 합니다. 영구 저장소에서 toostore hello 세션 상태를 원하는 경우이 공급자를 사용 합니다. Web App의 크기를 조정할 수 있지만 세션에 SQL Server를 사용하면 Web App의 성능에 영향을 줍니다.
* 배포에 메모리 세션 상태 공급자 Redis Cache 세션 상태 공급자-이 공급자에서는 장점 hello 등입니다. Web App에는 빠르고 간단하며 확장성 있는 세션 상태 제공자가 있을 수 있습니다. 이 공급자 저장소 hello 앱 캐시에 세션 상태 고려 사항에서 tootake 갖기 때문에 모든 hello 통하게 tooa 일시적인 네트워크 오류 등의 메모리 캐시에 분산 될 때 연결 된 특성입니다. 캐시 사용의 모범 사례는 Microsoft Patterns & Practices [Azure 클라우드 응용 프로그램 설계 및 구현 지침](https://github.com/mspnp/azure-guidance)에서 [캐싱 지침](../best-practices-caching.md)을 참조하세요.

세션 상태 및 기타 모범 사례에 대한 자세한 내용은 [웹 개발 모범 사례(Azure를 사용하는 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)를 참조하세요.

## <a name="next-steps"></a>다음 단계
체크 아웃 hello [Azure Redis Cache 용 ASP.NET 출력 캐시 공급자](cache-aspnet-output-cache-provider.md)합니다.

