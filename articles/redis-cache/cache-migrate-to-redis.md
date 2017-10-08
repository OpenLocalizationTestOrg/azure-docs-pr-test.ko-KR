---
title: "Azure 관리 캐시 서비스 응용 프로그램 tooRedis-aaaMigrate | Microsoft Docs"
description: "자세한 내용은 방법 toomigrate 관리 캐시 서비스 및 역할 내 캐시 응용 프로그램 tooAzure Redis 캐시"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>관리 캐시 서비스 tooAzure Redis Cache에서 마이그레이션
Azure 관리 캐시 서비스 tooAzure Redis Cache를 사용 하는 응용 프로그램을 마이그레이션하는 캐싱 응용 프로그램에 사용 되는 hello 관리 캐시 서비스 기능에 따라 최소한의 변경 tooyour 응용 프로그램으로 수행할 수 있습니다. Hello Api는 hello 정확히 동일한은 유사 하 고, 관리 캐시 서비스 tooaccess 캐시를 사용 하는 기존 코드의 대부분 최소한의 변경으로 다시 사용할 수입니다. 이 항목 변경 내역을 보여 toomake hello 필요한 구성 및 응용 프로그램 toomigrate 관리 캐시 서비스 응용 프로그램 toouse Azure Redis 캐시 하 고 Azure Redis Cache의 hello 기능의 일부만 사용 하는 tooimplement hello 기능 수 있는 방법을 보여 줍니다. 관리 캐시 서비스 캐시 합니다.

>[!NOTE]
>Managed Cache Service와 In-Role Cache는 2016년 11월 30일에 [사용 중지](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)되었습니다. 원하는 toomigrate tooAzure Redis 캐시 모든 역할 내 캐시의 배포를 설정한 경우이 문서의 hello 단계를 따르면 됩니다.

## <a name="migration-steps"></a>마이그레이션 단계
단계를 수행 하는 hello 필요한 toomigrate 관리 캐시 서비스 응용 프로그램 toouse Azure Redis 캐시 됩니다.

* 관리 캐시 서비스 기능 tooAzure Redis Cache 매핑
* 캐시 제품 선택
* 캐시 만들기
* Hello 캐시 클라이언트 구성
  * Hello 관리 캐시 서비스 구성 제거
  * Hello StackExchange.Redis NuGet 패키지를 사용 하 여 캐시 클라이언트 구성
* 관리된 캐시 서비스 코드 마이그레이션
  * Hello ConnectionMultiplexer 클래스를 사용 하 여 toohello 캐시를 연결 합니다.
  * 기본 데이터 형식 hello 캐시에 액세스
  * Hello 캐시에서.NET 개체 사용
* ASP.NET 세션 상태 및 출력 tooAzure Redis 캐시 캐싱 마이그레이션 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>관리 캐시 서비스 기능 tooAzure Redis Cache 매핑
Azure 관리된 캐시 서비스 및 Azure Redis Cache는 유사하지만 다른 방법으로 해당 기능 일부를 구현합니다. 이 섹션의 몇 가지 hello 차이점에 설명 하 고 Azure Redis Cache에 관리 캐시 서비스의 hello 기능 구현에 대 한 지침을 제공 합니다.

| 관리된 캐시 서비스 기능 | 관리된 캐시 서비스 지원 | Azure Redis Cache 지원 |
| --- | --- | --- |
| 이름이 지정된 캐시 |기본 캐시가 구성 되어 있으며 hello 표준 및 프리미엄 캐시 기능, 추가 toonine 명명 된 캐시 수 구성할 수 필요 합니다. |Azure Redis cache에 사용 되는 tooimplement 유사한 기능 toonamed 캐시 될 수 있는 (기본값 16) 데이터베이스의 구성 가능한 번호가 없습니다. 자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases) 및 [기본 Redis 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요. |
| 고가용성 |Hello 표준 및 프리미엄 캐시 기능에 대 한 hello 캐시의 항목에 대 한 고가용성을 제공합니다. 항목이 tooa 오류로 인해 손실 된 경우 hello 캐시의 hello 항목의 백업 복사본을 사용할 수 있습니다. 보조 캐시 toohello 내용이 동기적으로 씁니다. |Hello 표준 및 프리미엄 캐시 기능에서 (각 분할 프리미엄 캐시에서 a가 주/복제본)는 2 개 노드 기본/복제본 구성을 포함 하는 고가용성 ´ ù. 쓰기 toohello 복제본이 비동기적으로 수행 됩니다. 자세한 내용은 [Azure Redis Cache 가격 책정](https://azure.microsoft.com/pricing/details/cache/)을 참조하세요. |
| 알림 |명명된 된 캐시에서 클라이언트가 tooreceive 비동기 알림을 때 다양 한 캐시 작업이 발생할 수 있습니다. |클라이언트 응용 프로그램이 Redis pub/sub를 사용할 수 또는 [키 스페이스 알림에서](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve 유사한 기능 toonotifications 합니다. |
| 로컬 캐시 |매우 빠른 액세스에 대 한 hello 클라이언트에서 캐시 된 개체의 복사본을 로컬로 저장합니다. |클라이언트 응용 프로그램 사전 또는 유사한 데이터 구조를 사용 하 여이 기능 tooimplement이 필요 합니다. |
| 제거 정책 |없음 또는 LRU입니다. hello 기본 정책은 LRU입니다. |Azure Redis Cache 지원 제거 정책에 따라 hello: volatile lru, lru allkeys, volatile 임의 allkeys 임의 volatile ttl, noeviction 합니다. hello 기본 정책은 lru volatile입니다. 자세한 내용은 [기본 Redis 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요. |
| 만료 정책 |hello 기본 만료 정책은 절대 이며 hello 기본 만료 간격은 10 분입니다. 또한 슬라이딩 및 없음 정책을 사용할 수 있습니다. |기본적으로 hello 캐시에서 항목이 만료 되지 않고, 않지만 캐시 집합 오버 로드를 사용 하 여 쓰기 단위로 만료를 구성할 수 있습니다. 자세한 내용은 참조 [hello 캐시에서 개체를 추가 및 검색 하 고](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache)합니다. |
| 지역 및 태깅 |지역은 캐시된 항목에 대한 하위 그룹입니다. 또한 영역은 태그 라는 추가 설명 문자열로 된 캐시 된 항목의 hello 주석을 지원 합니다. 영역은 해당 지역에서 태그가 지정된 된 항목에 대 한 hello 기능 tooperform 검색 작업을 지원합니다. 영역 내에서 모든 항목이 hello 캐시 클러스터의 단일 노드 내에 배치 됩니다. |Redis cache 이루어지며 단일 노드의 (Redis 클러스터를 사용 하지 않으면) 관리 캐시 서비스 영역의 개념이 hello 적용 되지 않습니다. 검색 지원 및 와일드 카드 연산 redis는 설명 태그 hello 키 이름 내에 포함할 수 고 tooretrieve hello 항목을 나중에 사용 되는 키를 검색할 때 합니다. Redis를 사용하는 태그 지정 솔루션을 구현하는 예는 [Redis로 태그를 지정하는 캐시 구현](http://stackify.com/implementing-cache-tagging-redis/)을 참조하세요. |
| 직렬화 |관리 되는 캐시는 NetDataContractSerializer, BinaryFormatter 및 사용자 지정 serializer의 hello 사용을 지원합니다. hello 기본값은 NetDataContractSerializer입니다. |hello hello 클라이언트 응용 프로그램 tooserialize.NET 개체의 toohello 클라이언트 응용 프로그램 개발자를 hello serializer의 hello choice가 있는 hello 캐시에 추가 하기 전에 합니다. 자세한 내용 및 예제 코드에 대 한 참조 [hello 캐시에서.NET 개체 사용](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)합니다. |
| 캐시 에뮬레이터 |관리되는 캐시는 로컬 캐시 에뮬레이터를 제공합니다. |Azure Redis Cache는 에뮬레이터 필요는 없지만 할 수 있습니다 [redis server.exe의 hello MSOpenTech 빌드를 로컬로 실행](cache-faq.md#cache-emulator) tooprovide 에뮬레이터 경험 합니다. |

## <a name="choose-a-cache-offering"></a>캐시 제품 선택
Microsoft Azure Redis Cache는 hello 다음 계층에서에서 제공 됩니다.

* **기본** – 단일 노드. Too53 GB 여러 크기입니다.
* **표준** – 2노드 주/복제본. Too53 GB 여러 크기입니다. 99.9% SLA
* **프리미엄** – 두 노드 주/복제본와 시작 too10 분할 된 데이터베이스입니다. GB too530 6GB 여러 크기입니다. 모든 표준 계층 기능과 추가적인 [Redis 클러스터](cache-how-to-premium-clustering.md), [Redis 지속성](cache-how-to-premium-persistence.md) 및 [Azure Virtual Network](cache-how-to-premium-vnet.md) 지원이 포함됩니다. 99.9% SLA

각 계층은 기능과 가격이 다릅니다. hello 기능 나와이 가이드의 뒷부분에 나오는 한 가격 책정에 대 한 자세한 내용은 참조 하십시오. [캐시 가격 정보](https://azure.microsoft.com/pricing/details/cache/)합니다.

마이그레이션에 대 한 시작 지점을 이전 처럼 관리 캐시 서비스 캐시의 hello 크기와 일치 하는 toopick hello 크기가 고 응용 프로그램의 hello 요구 사항에 따라 위나 아래로 이동을 확장 합니다. Hello 오른쪽 Azure Redis 캐시 제공 량을 선택에 대 한 자세한 지침을 참조 하십시오. [어떤 Redis 캐시 기능 및 크기 사용 해야 합니까?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)합니다.

## <a name="create-a-cache"></a>캐시 만들기
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Hello 캐시 클라이언트 구성
Hello 캐시가 만들어지고 구성 되 면 hello 다음 단계는 tooremove hello 관리 캐시 서비스 구성 및이 hello를 추가 하는 캐시 클라이언트 hello 캐시에 액세스할 수 있도록 hello Azure Redis 캐시 구성 및 참조를 추가 합니다.

* Hello 관리 캐시 서비스 구성 제거
* Hello StackExchange.Redis NuGet 패키지를 사용 하 여 캐시 클라이언트 구성

### <a name="remove-hello-managed-cache-service-configuration"></a>Hello 관리 캐시 서비스 구성 제거
Hello 하기 전에 클라이언트 응용 프로그램이 Azure Redis Cache를 hello 기존 관리 캐시 서비스 구성에 대 한 구성 수 및 hello 관리 캐시 서비스 NuGet 패키지를 제거 하 여 어셈블리 참조를 제거 해야 합니다.

toouninstall hello 관리 캐시 서비스 NuGet 패키지에서 hello 클라이언트 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **NuGet 패키지 관리**합니다. 선택 hello **설치 된 패키지** 노드와 형식 W**indowsAzure.Caching** hello에 검색 상자 패키지를 설치 합니다. 선택 **Windows** **Azure 캐시** (또는 **Windows** **Azure Caching** hello NuGet 패키지의 hello 버전에 따라), 클릭 **제거**, 클릭 하 고 **닫기**합니다.

![Azure 관리된 캐시 서비스 NuGet 패키지 제거](./media/cache-migrate-to-redis/IC757666.jpg)

Hello 관리 캐시 서비스 NuGet 패키지 제거 hello app.config 또는 web.config hello 클라이언트 응용 프로그램의 hello 관리 캐시 서비스 어셈블리와 hello 관리 캐시 서비스 항목을 제거 합니다. 일부 사용자 지정 된 설정을 hello NuGet 패키지를 제거할 때 제거 되지 않을 수 있습니다, 때문에 web.config 또는 app.config를 열고 확인 요소 다음 해당 hello 완전히 제거 됩니다.

해당 hello 확인 `dataCacheClients` hello에서 항목이 제거 되 `configSections` 요소입니다. Hello 전체를 제거 하지 마십시오 `configSections` 요소; 방금 제거 hello `dataCacheClients` 항목을 제공 합니다.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

해당 hello 확인 `dataCacheClients` 섹션이 제거 됩니다. hello `dataCacheClients` 섹션에는 다음 예제와 비슷한 toohello 됩니다.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Hello 관리 캐시 서비스 구성 제거 되 면 hello 다음 섹션에에서 설명 된 대로 hello 캐시 클라이언트를 구성할 수 있습니다.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Hello StackExchange.Redis NuGet 패키지를 사용 하 여 캐시 클라이언트 구성
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>관리된 캐시 서비스 코드 마이그레이션
hello StackExchange.Redis 캐시 클라이언트에 대 한 hello API와 비슷한 toohello 관리 캐시 서비스입니다. 이 섹션에서는 hello 차이점에 대 한 개요를 제공 합니다.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Hello ConnectionMultiplexer 클래스를 사용 하 여 toohello 캐시를 연결 합니다.
관리 캐시 서비스에서 연결 toohello 캐시 hello에 의해 처리 된 `DataCacheFactory` 및 `DataCache` 클래스입니다. Azure Redis Cache에서 hello 하 여 이러한 연결을 관리 `ConnectionMultiplexer` 클래스입니다.

Hello 다음 추가 tooaccess hello 캐시 하려는 모든 파일의 문 toohello top 사용 합니다.

```c#
using StackExchange.Redis
```

이 네임 스페이스 해결 되지 않으면 수에 설명 된 대로 hello StackExchange.Redis NuGet 패키지를 추가 해야 [hello 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)합니다.

> [!NOTE]
> Note hello StackExchange.Redis 클라이언트에.NET Framework 4 이상이 필요 합니다.
> 
> 

tooconnect tooan Azure Redis Cache 인스턴스 호출 hello 정적 `ConnectionMultiplexer.Connect` 메서드와 hello 끝점과 키를 전달 합니다. 한 가지 방법은 toosharing는 `ConnectionMultiplexer` 응용 프로그램에서 인스턴스가 toohave 비슷한 toohello 다음 예제에서는 연결 된 인스턴스를 반환 하는 정적 속성입니다. 스레드로부터 안전한 방식으로 tooinitialize 연결 하나만 제공 `ConnectionMultiplexer` 인스턴스. 이 예에서 `abortConnect` 연결 toohello 캐시 설정 되지 않으며 경우에 hello 호출은 성공 합니다 즉 집합 toofalse 됩니다. 주요 기능 중 하나 `ConnectionMultiplexer` 를 복원할 수는 자동으로 연결 toohello 캐시 hello 네트워크 문제 또는 다른 원인이 해결 되 면 됩니다.

```c#
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
```

hello 캐시 끝점, 키 및 포트에서에서 얻을 수 있습니다 hello **Redis Cache** 블레이드 캐시 인스턴스에 대 한 합니다. 자세한 내용은 [Redis Cache 속성](cache-configure.md#properties)을 참조하세요.

Hello 연결이 설정 되 면 별 참조 toohello Redis cache 데이터베이스 호출 hello `ConnectionMultiplexer.GetDatabase` 메서드. hello에서 반환 된 hello 개체 `GetDatabase` 메서드 경량의 통과 개체 이며 저장 toobe 필요는 없습니다.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

hello StackExchange.Redis 클라이언트 hello를 사용 하 여 `RedisKey` 및 `RedisValue` 형식에 액세스 하 고 hello 캐시에 항목을 저장 합니다. 이러한 형식은 문자열을 포함하여 가장 기본적인 언어 형식에 매핑되며 직접 사용되는 경우가 드뭅니다. Redis를 포함 하는 메서드를 사용 합니다 hello 형식을 직접 사용 하지 않을 수 있습니다 하는 동안 문자열 hello 가장 기본적인 종류의 Redis 값 이며 및 많은 종류의 직렬화 된 이진 스트림을 포함 하 여 데이터를 포함할 수 있습니다 및 `String` hello 이름에서. 대부분의 기본 데이터 형식에 대 한 저장 한 hello를 사용 하 여 hello 캐시에서 항목을 검색 `StringSet` 및 `StringGet` 메서드 컬렉션 또는 기타 Redis 데이터 형식을 hello 캐시에 저장 하지 않는 한 합니다. 

`StringSet`및 `StringGet` 매우 유사한 toohello 관리 캐시 서비스는 `Put` 및 `Get` 한 가지 큰 메서드를 설정 하 고 hello 캐시로.NET 개체를 가져오려면 먼저 serialize 해야 것 먼저 된 차이입니다. 

호출할 때 `StringGet`hello 개체가 있는 경우 반환 되는, 및 표시 되지 않는 경우 null이 반환 됩니다. 이 경우 hello 값 hello 원하는 데이터 원본에서 검색할 수 있으며 다음에 사용에 대 한 hello 캐시에 저장. 이 hello 캐시 배제 패턴 이라고 합니다.

hello 캐시를 사용 하 여 hello에 있는 항목의 toospecify hello 만료 `TimeSpan` 의 매개 변수 `StringSet`합니다.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Azure Redis Cache는 .NET 개체 및 기본 데이터 형식으로 작업할 수 있지만 .NET 개체를 캐시하려면 먼저 직렬화해야 합니다. Hello 응용 프로그램 개발자의 hello 책임입니다. 유연성 hello 개발자 hello serializer의 hello 선택에 있습니다. 자세한 내용 및 예제 코드에 대 한 참조 [hello 캐시에서.NET 개체 사용](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)합니다.

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>ASP.NET 세션 상태 및 출력 tooAzure Redis 캐시 캐싱 마이그레이션
Azure Redis Cache에는 ASP.NET 세션 상태 및 페이지 출력 캐싱 모두에 공급자가 있습니다. toomigrate hello 관리 캐시 서비스 버전의 이러한 공급자를 사용 하 여 응용 프로그램을 먼저 제거 web.config에서 기존 섹션 hello 고 hello Azure Redis Cache 버전의 hello 공급자를 구성 합니다. 사용 하는 방법은 Azure Redis 캐시 ASP.NET 공급자 hello, 참조 [Azure Redis Cache 용 ASP.NET 세션 상태 공급자](cache-aspnet-session-state-provider.md) 및 [Azure Redis Cache 용 ASP.NET 출력 캐시 공급자](cache-aspnet-output-cache-provider.md)합니다.

## <a name="next-steps"></a>다음 단계
Hello 탐색 [Azure Redis Cache 설명서](https://azure.microsoft.com/documentation/services/cache/) 자습서, 샘플, 비디오, 등에.

