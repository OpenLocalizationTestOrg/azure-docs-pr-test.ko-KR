---
title: Azure Redis Cache aaaHow tooUse | Microsoft Docs
description: "Tooimprove Azure Redis 캐시와 Azure 응용 프로그램의 성능을 hello 하는 방법에 대해 알아봅니다"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a>Azure Redis 캐시 하는 tooUse 방법
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

이 가이드에서는 알아봅니다 tooget를 사용 하 여 시작 방법을 **Azure Redis Cache**합니다. Microsoft Azure Redis Cache hello 인기 있는 오픈 소스 Redis Cache를 기반으로 합니다. 제공 tooa 안전한 전용된 Redis 캐시, Microsoft에서 관리 액세스 합니다. Azure Redis 캐시를 사용하여 만들어진 캐시는 Microsoft Azure 내의 모든 응용 프로그램에서 액세스할 수 있습니다.

Microsoft Azure Redis Cache는 hello 다음 계층에서에서 제공 됩니다.

* **기본** – 단일 노드. Too53 GB 여러 크기입니다.
* **표준** – 2노드 주/복제본. Too53 GB 여러 크기입니다. 99.9% SLA
* **프리미엄** – 두 노드 주/복제본와 시작 too10 분할 된 데이터베이스입니다. GB too530 6GB 여러 크기입니다. 모든 표준 계층 기능과 추가적인 [Redis 클러스터](cache-how-to-premium-clustering.md), [Redis 지속성](cache-how-to-premium-persistence.md) 및 [Azure Virtual Network](cache-how-to-premium-vnet.md) 지원이 포함됩니다. 99.9% SLA

각 계층은 기능과 가격이 다릅니다. 가격 책정에 대한 내용은 [캐시 가격 책정 정보][Cache Pricing Details]를 참조하세요.

이 가이드에서는 toouse hello [StackExchange.Redis] [ StackExchange.Redis] C를 사용 하 여 클라이언트\# 코드입니다. hello 가이드에서 다루는 시나리오 포함 **만들기 및 구성 캐시**, **캐시 클라이언트 구성**, 및 **추가 하 고 hello 캐시에서 개체 제거**합니다. Azure Redis Cache 사용에 대한 자세한 내용은 [다음 단계][Next Steps]를 참조하세요. ASP.NET MVC Redis 캐시와 웹 응용 프로그램 빌드 과정의 단계별 자습서를 참조 하십시오. [어떻게 toocreate Redis Cache에 웹 앱](cache-web-app-howto.md)합니다.

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Azure Redis Cache 시작
Azure Redis 캐시를 시작하기는 쉽습니다. tooget 하면 프로 비전을 시작 하 고 캐시를 구성 합니다. 다음으로 hello 캐시 액세스할 수 있도록 hello 캐시 클라이언트 구성 합니다. Hello 캐시 클라이언트를 구성한 후 작업을 시작할 수 있습니다.

* [Hello 캐시 만들기][Create hello cache]
* [Hello 캐시 클라이언트 구성][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>캐시 만들기
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess 그 뒤에 캐시는 생성
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

캐시를 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooconfigure Azure Redis Cache](cache-configure.md)합니다.

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Hello 캐시 클라이언트 구성
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

캐싱에 대 한 클라이언트 프로젝트 구성 되 면 hello 다음 캐시 작업에 대 한 섹션에에서 설명 된 hello 기술을 사용할 수 있습니다.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>캐시 작업
이 섹션의 hello 단계 tooperform 일반 캐시와 작업 하는 방법을 설명 합니다.

* [Toohello 캐시를 연결 합니다.][Connect toohello cache]
* [추가 하 고 hello 캐시에서 개체를 검색 합니다.][Add and retrieve objects from hello cache]
* [Hello 캐시에서.NET 개체 사용](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Toohello 캐시를 연결 합니다.
tooprogrammatically 작업 참조 toohello 캐시는 캐시를 사용 해야 합니다. Hello toohello 위쪽 원하는 toouse hello StackExchange.Redis 클라이언트 tooaccess Azure Redis Cache 모든 파일의 다음을 추가 합니다.

    using StackExchange.Redis;

> [!NOTE]
> hello StackExchange.Redis 클라이언트에.NET Framework 4 이상이 필요합니다.
> 
> 

Azure Redis Cache hello에서 관리 하는 연결 toohello hello `ConnectionMultiplexer` 클래스입니다. 이 클래스는 공유 되지 않아야 하 고 클라이언트 응용 프로그램 전반에 걸쳐 다시 하며 toobe 작업 별로 만들 필요는 없습니다. 

tooconnect tooan Azure Redis Cache의 연결 된 인스턴스를 반환 될 `ConnectionMultiplexer`, 정적 호출 hello `Connect` 메서드와 hello 전달 캐시 끝점 및 키입니다. Hello hello password 매개 변수도 Azure 포털에서에서 생성 된 hello 키를 사용 합니다.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> 경고: 소스 코드에 자격 증명을 저장해서는 안 됩니다. tookeep이 샘플 단순 하 고 여기서 설명으로 hello 소스 코드에서. 참조 [방법을 응용 프로그램 문자열 및 연결 문자열 작업] [ How Application Strings and Connection Strings Work] 방법에 대 한 내용은 toostore 자격 증명입니다.
> 
> 

SSL toouse 않으려면 설정 하거나 `ssl=false` hello를 생략 하거나 `ssl` 매개 변수입니다.

> [!NOTE]
> hello 비 SSL 포트는 새 캐시에 대해 기본적으로 비활성화 되어 있습니다. Hello 비 SSL 포트를 사용 하도록 설정 하면 지침은 [액세스 포트](cache-configure.md#access-ports)합니다.
> 
> 

한 가지 방법은 toosharing는 `ConnectionMultiplexer` 응용 프로그램에서 인스턴스가 toohave 비슷한 toohello 다음 예제에서는 연결 된 인스턴스를 반환 하는 정적 속성입니다. 이 방법은 제공 스레드로부터 안전한 방식으로 tooinitialize 연결 하나만 `ConnectionMultiplexer` 인스턴스. 다음 예에서 `abortConnect` hello 호출이 연결 toohello Azure Redis Cache 설정 되지 않으며 경우에 성공 하는 집합 toofalse 됩니다. 주요 기능 중 하나 `ConnectionMultiplexer` 는 자동으로 복원 연결 toohello 캐시 hello 네트워크 문제 또는 다른 원인이 해결 되 면 됩니다.

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

고급 연결 구성 옵션에 대한 자세한 내용은 [StackExchange.Redis 구성 모델][StackExchange.Redis configuration model](영문)을 참조하세요.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Hello 연결이 설정 되 면 별 참조 toohello redis cache 데이터베이스 호출 hello `ConnectionMultiplexer.GetDatabase` 메서드. hello에서 반환 된 hello 개체 `GetDatabase` 메서드 경량의 통과 개체 이며 저장 toobe 필요는 없습니다.

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

Azure Redis cache Redis 캐시 내에서 사용 되는 toologically 별도 hello 데이터 일 수 있는 (기본값 16) 데이터베이스의 구성 가능한 번호가 없습니다. 자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases) 및 [기본 Redis 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요.

Tooconnect tooan Azure Redis Cache 인스턴스 및 참조 toohello 반환 데이터베이스에서 캐시 방법을 파악 했으므로 hello 캐시 작업에서 살펴보겠습니다.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>추가 하 고 hello 캐시에서 개체를 검색 합니다.
항목에 저장 하 고 hello를 사용 하 여 캐시에서 검색할 수 `StringSet` 및 `StringGet` 메서드.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Redis 저장소 Redis 문자열 하지만 이러한 문자열 대부분의 데이터에는 다양 한 유형의 hello 캐시에 개체를.NET 저장할 때 사용할 수 있는 serialize 된 이진 데이터를 포함 한 데이터를 포함 될 수 있습니다.

호출할 때 `StringGet`, hello 개체가 있는 경우 반환 되는, 존재 하지 않는 경우 `null` 반환 됩니다. 경우 `null` 반환 되 면 hello 원하는 데이터 원본에서 hello 값을 검색 하 및 이후 사용에 대 한 hello 캐시에 저장할 수 있습니다. 이 사용 패턴 hello 캐시 배제 패턴 이라고 합니다.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

사용할 수도 있습니다 `RedisValue`hello 다음 예제에에서 나온 것 처럼 합니다. `RedisValue`는 정수 데이터 형식을 작업하기 위한 암시적 연산자를 갖고 있으며, 캐시된 항목의 값으로 `null`이 예상되는 경우에 유용하게 사용할 수 있습니다.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


hello 캐시를 사용 하 여 hello에 있는 항목의 toospecify hello 만료 `TimeSpan` 의 매개 변수 `StringSet`합니다.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Hello 캐시에서.NET 개체 사용
Azure Redis Cache는 .NET 개체 및 기본 데이터 유형을 캐시할 수 있지만 .NET 개체를 캐시하려면 먼저 직렬화해야 합니다. 이.NET 개체 serialization hello 응용 프로그램 개발자의 책임 hello 있으며 hello serializer의 hello 선택에 hello 개발자 유연성을 제공 합니다.

하나의 간단한 방법을 tooserialize 개체는 toouse hello `JsonConvert` 의 serialization 메서드 [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) JSON에서 tooand serialize 합니다. hello 다음 보여 주는 예제는 get 및 set를 사용 하는 `Employee` 개체 인스턴스입니다.

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a>다음 단계
Hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure Redis Cache에 대 한 자세한를 수행 합니다.

* 체크 아웃 hello Azure Redis Cache 용 ASP.NET 공급자입니다.
  * [Azure Redis 세션 상태 공급자](cache-aspnet-session-state-provider.md)
  * [Azure Redis Cache ASP.NET 출력 캐시 공급자](cache-aspnet-output-cache-provider.md)
* [캐시 진단을 사용 하도록 설정](cache-how-to-monitor.md#enable-cache-diagnostics) 할 수 있도록 [모니터](cache-how-to-monitor.md) hello 캐시의 상태입니다. Hello 수도 hello Azure 포털에서 메트릭을 볼 수 있습니다 [다운로드 하 여 검토](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 선택한 hello 도구를 사용 하 게 합니다.
* 체크 아웃 hello [StackExchange.Redis 캐시 클라이언트 설명서][StackExchange.Redis cache client documentation]합니다.
  * Azure Redis Cache는 다양한 Redis 클라이언트와 개발 언어에서 액세스할 수 있습니다. 자세한 내용은 [http://redis.io/clients][http://redis.io/clients]를 참조하세요.
* Redsmin 및 Redis Desktop Manager와 같은 타사 서비스 및 도구와 함께 Azure Redis Cache를 사용할 수도 있습니다.
  * Redsmin에 대 한 자세한 내용은 참조 [어떻게 tooretrieve Azure Redis 연결 문자열을 사용 하 여 Redsmin와][How tooretrieve an Azure Redis connection string and use it with Redsmin]합니다.
  * [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)를 사용하여 GUI가 포함된 Azure Redis Cache의 데이터에 액세스하고 해당 데이터를 검사합니다.
* Hello 참조 [redis] [ redis] 설명서 및 읽기에 대 한 [redis 데이터 형식을] [ redis data types] 및 [15 분 소개 데이터 형식 tooRedis][a fifteen minute introduction tooRedis data types]합니다.

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


