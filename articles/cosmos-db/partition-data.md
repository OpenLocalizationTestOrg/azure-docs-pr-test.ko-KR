---
title: "aaaPartitioning Azure Cosmos DB에서 가로 크기를 조정 | Microsoft Docs"
description: "Azure Cosmos DB에서 분할 방법을 작동에 대 한 어떻게 tooconfigure 분할 및 파티션 키, 그리고 toopick 오른쪽 hello 파티션 키에 대 한 응용 프로그램에 대해 알아봅니다."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>어떻게 toopartition와 Azure Cosmos DB에서 소수 자릿수

[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 있습니다 달성 신속 하 고 예측 가능한 성능 및 확장성 원활 하 게 응용 프로그램과 함께 커짐에 따라 글로벌 분산, 다중-모델 데이터베이스 설계 된 서비스 toohelp 됩니다. 이 문서에서는 분할은 모든 hello 데이터에 대 한 Azure Cosmos DB에서 모델 및 Azure Cosmos DB 컨테이너 tooeffectively 크기 조정 응용 프로그램 구성할 수 있는 방법을 설명 방법의 개요를 제공 합니다.

Scott Hanselman과 Azure Cosmos DB 수석 엔지니어링 관리자 Shireesh Thota가 진행하는 이 Azure Friday 비디오에서는 분할 및 파티션 키에 대해서도 다룹니다.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Azure Cosmos DB에서 분할
Azure Cosmos DB에서는 규모에 상관없이 밀리초 단위의 응답 시간 순으로 스키마 없는 데이터를 저장하고 쿼리할 수 있습니다. Cosmos DB는 **컬렉션(문서의 경우), 그래프 및 표**라는 데이터 저장용 컨테이너를 제공합니다. 컨테이너는 하나 이상의 물리적 파티션 또는 서버에 걸쳐 있을 수 있는 논리적 리소스입니다. 파티션 수가 hello Cosmos db hello 저장소 크기와 hello hello 컨테이너의 프로 비전 된 처리량에 따라 결정 됩니다. Cosmos DB의 모든 파티션은 고정된 양의 SSD 지원 저장소에 연결되며, 고가용성을 위해 복제됩니다. 파티션 관리 Azure Cosmos DB에서 관리 하는 완벽 하 게 하 고 toowrite 복잡 한 코드가 있는 또는 파티션을 관리 하지 않는 합니다. Cosmos DB 컨테이너는 처리량 및 저장소 면에서 제한되지 않습니다. 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

분할은 투명 tooyour 응용 프로그램입니다. Cosmos DB 빠른 읽기 및 쓰기, 쿼리, 트랜잭션 논리, 일관성 수준 및 메서드/Api tooa 단일 컨테이너 리소스를 통해 세분화 된 액세스 제어를 지원합니다. hello 파티션 간에 데이터를 배포 및 쿼리 요청 toohello 올바른 파티션 라우팅 서비스 핸들입니다. 

분할은 어떻게 작동하나요? 각 항목에는 파티션 키 및 행 키가 있어서 항목을 고유하게 식별해야 합니다. 파티션 키는 데이터에 대한 논리적 분할의 역할을 하고 파티션 간에 데이터를 배포하는 자연 경계를 가진 Cosmos DB를 제공합니다. 간단히 말해, Azure Cosmos DB에서 분할의 작동 방식은 다음과 같습니다.

* `T` 요청/초 처리량으로 Cosmos DB 컨테이너를 프로비전합니다.
* Hello 백그라운드 Cosmos DB 프로 비전 파티션에 필요한 tooserve `T` 요청/초입니다. 경우 `T` 파티션당 hello 최대 처리량 보다 높은 `t`, Cosmos DB 프로 비전 한 다음 `N`  =  `T/t` 파티션
* Cosmos DB 공간 할당 하는 hello 키 파티션 키 해시 균등 하 게 hello에서 `N` 파티션을 합니다. 따라서 각 파티션(실제 파티션)은 1-N 파티션 키 값(논리 파티션)을 호스팅합니다.
* 때 실제 파티션을 `p` 저장소 한도 Cosmos DB 원활 하 게 분할 하는 정도 `p` 두 개의 새 파티션으로 `p1` 및 `p2` 하 고이 배포의 hello tooroughly 절반 hello 키 tooeach 해당 값 파티션입니다. 이 작업을 분할은 보이지 않는 tooyour 응용 프로그램입니다.
* 마찬가지로, 보다 높은 처리량을 제공 하는 하면 `t*N` 하나 이상의 파티션 toosupport hello 더 높은 처리량을 분할 하는 처리량, Cosmos DB

파티션 키에 대 한 hello 의미 hello 표 다음에 표시 된 것과 같이 각 API의 약간 다른 toomatch hello 의미 체계를 있습니다.

| API | Partition Key | Row Key |
| --- | --- | --- |
| DocumentDB | custom partition key path | fixed `id` | 
| MongoDB | custom shard key  | fixed `_id` | 
| 그래프 | custom partition key property | fixed `id` | 
| 테이블 | fixed `PartitionKey` | fixed `RowKey` | 

Cosmos DB는 해시 기반 분할을 사용합니다. 항목을 작성 하는 경우 Cosmos DB hello 파티션 키 값을 해시 및 사용 하 여 hello 해시 결과 toodetermine 어떤 파티션 toostore hello 항목입니다. Cosmos DB 저장소 인 모든 항목에 동일한 파티션 키 hello hello 동일한 실제 파티션을 합니다. hello 선택 hello 파티션 키에는 디자인 타임에 toomake 한지 중요 한 결정 됩니다. 다양한 범위의 값과 균일한 액세스 패턴을 가진 속성 이름을 선택해야 합니다.

> [!NOTE]
> 모범 사례 toohave 많은 고유 값 (단위: 100 1000s 최소한)를 사용 하 여 파티션 키 이며
>

Azure Cosmos DB 컨테이너를 "고정" 또는 "무제한"으로 만들 수 있습니다. 고정 크기 컨테이너는 최대 제한 10GB 및 10,000RU/s 처리량을 설정할 수 있습니다. 일부 Api는 고정 크기의 컨테이너에 대 한 hello 파티션 키 toobe 생략 허용 합니다. 무제한으로 컨테이너 toocreate 2500 000RU/s의 최소 처리량을 지정 해야 합니다.

## <a name="partitioning-and-provisioned-throughput"></a>분할 및 프로비전된 처리량
Cosmos DB는 예측 가능한 성능을 위해 설계되었습니다. 컨테이너를 만들 때 **RU/m의 잠재적인 기능으로 초당 [요청 단위](request-units.md)(RU)** 측면에서 처리량을 예약합니다. 각 요청은 요청 단위 요금이 비례 toohello 양의 CPU, 메모리 및 IO hello 작업에 의해 소비와 같은 시스템 리소스를 할당 합니다. 세션 일관성에 따라 1KB 문서를 읽을 경우 1RU(요청 단위)가 소비됩니다. 읽기는 1 hello 항목 수에 관계 없이 RU hello에서 실행 되는 동시 요청 수가 hello 또는 저장 된 같은 시간입니다. 더 큰 항목 hello 크기에 따라 더 높은 요청 단위를 해야합니다. 엔터티가 hello 크기를 알고 있으며 읽기 횟수가 hello toosupport 응용 프로그램에 필요한, hello 정확한 양을 응용 프로그램의 요구 사항을 읽이 필요한 처리량을 제공할 수 있습니다. 

> [!NOTE]
> hello 컨테이너의 tooachieve hello의 전체 처리량을 선택 해야 tooevenly 수 있는 파티션 키 일부 고유 파티션 키 값 사이 요청을 배포 합니다.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Hello Azure Cosmos DB Api 사용
Hello Azure 포털 또는 Azure CLI toocreate 컨테이너를 사용할 수 있으며 언제 든 지를 확장할 수 있습니다. 이 섹션에서는 어떻게 toocreate 컨테이너 hello 처리량과 파티션 키 정의의 hello 각 지원 되는 Api를 지정 합니다.

### <a name="documentdb-api"></a>DocumentDB API
다음 예제는 hello 사용 하 여 컨테이너 (컬렉션) toocreate DocumentDB API hello 하는 방법을 보여 줍니다. [DocumentDB API를 사용하여 분할](partition-data.md)에서 자세한 내용을 볼 수 있습니다.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Hello를 사용 하 여 항목 (문서)를 읽을 수 `GET` 메서드 hello REST API 또는 사용 하 여 `ReadDocumentAsync` hello Sdk 중 하나에 있습니다.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB API
Hello MongoDB API, 임의의 도구, 드라이버 또는 SDK를 통해 분할 된 컬렉션을 만들 수 있습니다. 이 예에서는 hello 컬렉션 만들기에 대 한 hello Mongo 셸을 사용 합니다.

Mongo 셸을 hello:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
결과:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>테이블 API

테이블 API hello로 응용 프로그램에 대 한 hello appSettings 구성에서 테이블에 대 한 hello 처리량을 지정합니다.

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

그런 다음 hello Azure 테이블 저장소 SDK를 사용 하 여 테이블을 만들면 됩니다. hello 파티션 키 hello로 암시적으로 생성 되어 `PartitionKey` 값입니다. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

다음 코드 조각 hello를 사용 하 여 단일 엔터티를 검색할 수 있습니다.

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
참조 [hello 테이블 API로 개발](tutorial-develop-table-dotnet.md) 내용을 확인 합니다.

### <a name="graph-api"></a>그래프 API

Graph API hello로 hello Azure 포털 또는 CLI toocreate 컨테이너를 사용 해야 합니다. 또는 Azure Cosmos DB 다중 모델 이므로 다른 모델 toocreate hello 중 하나를 사용 하 고 그래프 컨테이너를 확장할 수 있습니다.

모든 꼭 짓 점 또는 가장자리 Gremlin에 hello 파티션 키 및 id를 사용 하 여 읽을 수 있습니다. 예를 들어 hello 파티션 키 및 "Seattle" hello 행 키로 영역 ("미국")와 그래프를 구문 다음 hello를 사용 하 여 꼭지점을 찾을 수 있습니다.

```
g.V(['USA', 'Seattle'])
```

가장자리와 동일 하지만, hello 파티션 키와 행 키를 사용 하 여 가장자리를 참조할 수 있습니다.

```
g.E(['USA', 'I5'])
```

자세한 내용은 [Cosmos DB에 대한 Gremlin 지원](gremlin-support.md)을 참조하세요.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>분할 디자인
Azure Cosmos DB와 함께 효과적으로 tooscale, 해야 toopick 파티션 키 컨테이너를 만들 때. 파티션 키를 선택하는 두 가지 주요 고려 사항이 있습니다.

* **쿼리 및 트랜잭션에 대해 경계**: 선택 하는 파티션 키를 조정 해야 hello 필요 tooenable hello 사용 요구 사항이 toodistribute hello에 대 한 트랜잭션 엔터티에서 여러 파티션 키 tooensure는 확장 가능한 솔루션입니다. 최대 hello를 설정할 수 있습니다이 있지만 모든 항목에 대 한 파티션 키를 동일한 솔루션의 hello 확장성이 제한 될 수 있습니다. 다른 한편으로을 hello에 확장성이 높은 것 이지만으로 인해에서 저장된 프로시저 및 트리거를 통해 교차 문서 트랜잭션을 사용 하는 각 항목에 대 한 고유 파티션 키를 할당할 수 있습니다. 이상적인 파티션 키가 수 있게 해 주는 toouse 효율적인 쿼리 및 충분 한 카디널리티가 하나 tooensure 솔루션은 확장 가능 합니다. 
* **저장소 및 성능 병목 현상이 없습니다**: 것이 중요 toopick 수 있도록 하는 속성에 다양 한 고유 값에 분산 toobe 씁니다. 동일한 파티션 키 단일 파티션의 hello 처리량을 초과할 수 없습니다 들어오고 정체 되 toohello를 요청 합니다. 따라서 것이 중요 한 toopick "핫 스폿을" 응용 프로그램 내에서 발생 하지 않는 파티션 키입니다. 모든 hello 데이터 이후에 파티션 내에서 단일 파티션 키를 저장 해야 합니다는 반드시 대용량의 hello에 대 한 데이터를 포함 하는 tooavoid 파티션 키 값입니다. 

몇 가지 실제 시나리오 및 적절한 파티션 키를 각각 살펴보겠습니다.
* 사용자 프로필 백엔드를 구현 하는 경우 hello 사용자 ID가 파티션 키에 적합 합니다.
* IoT 데이터(예: 장치 상태)를 저장하는 경우 장치 ID를 파티션 키로 선택하는 것이 좋습니다.
* 시계열 데이터를 기록 하기 위한 Azure Cosmos DB를 사용할 경우 다음 호스트 이름이 hello 또는 프로세스 ID는 파티션 키에 대 한 좋은 선택 합니다.
* Hello 테 넌 트 ID는 다중 테 넌 트 아키텍처 있을 경우 파티션 키에 적합 합니다.

몇 가지 사용 사례 IoT 및 사용자 프로필, hello 파티션 키와 같은 수 있습니다 (문서 키) id로 hello 동일 합니다. Hello 시계열 데이터와 같은 다른 hello id와 다른 파티션 키를 할 수 있습니다.

### <a name="partitioning-and-loggingtime-series-data"></a>분할 및 로깅/시계열 데이터
Cosmos db hello 일반적인 사용 사례 중 하나는 로깅 및 원격 분석 합니다. 중요 한 toopick 파티션 키가 tooread/쓰기 방대한 양의 데이터를 할 수 있으므로. 읽기 및 쓰기 속도 및 종류의 쿼리 toorun 예상 사항에 따라 hello 선택 합니다. 다음 방법에 대 한 몇 가지 팁은 toochoose 파티션 키입니다.

* 사용 사례의 작은 비율 포함 되는 경우의 파티션 키가 있는 좋은 방법으로 날짜 hello timestamp에 대 한 롤업을 사용 하 여 다음를 타임 스탬프 및 다른 필터의 범위를 기준으로 시간과 필요 tooquery 오랜 기간 동안 누적 씁니다. 그러면 있습니다 tooquery 모든 hello 데이터에 대해 단일 파티션의 날짜에 대 한 합니다. 
* 일반적으로 워크로드에 쓰기 작업이 많은 경우 Cosmos DB가 다양한 파티션에 쓰기를 균등하게 분산할 수 있도록 타임스탬프에 기반하지 않는 파티션 키를 사용해야 합니다. 여기서 높은 카디널리티의 호스트 이름, 프로세스 ID, 작업 ID 또는 다른 속성을 선택하는 것이 좋습니다. 
* 세 번째 방법에는 하이브리드 하나 있는 각 일/월에 대해 하나씩 여러 컨테이너가 하 고 hello 파티션 키가 호스트 이름 처럼 세부적인 속성입니다. 예를 들어 hello 현재 달에 대 한 hello 컨테이너 프로 비전 된 처리량이 높은 읽기와 쓰기 사용 되므로으로 이전 달 뿐만 이후 처리량이 낮아질 반면,이 hello 기간에 따라 다른 처리량을 설정할 수 있는 hello 혜택 읽기만 사용 합니다.

### <a name="partitioning-and-multi-tenancy"></a>분할 및 다중 테넌트
Cosmos DB를 사용하여 다중 테넌트 응용 프로그램을 구현하는 경우 테넌트당 하나의 파티션 키 및 테넌트당 하나의 컨테이너라는 두 가지 인기 있는 패턴이 있습니다. Hello 장점 및 단점 각각에 대해 다음과 같습니다.

* 테넌트당 하나의 파티션 키: 이 모델에서는 테넌트가 단일 컨테이너 내에 함께 배치됩니다. 그러나 단일 파티션 내의 항목에 대한 쿼리 및 삽입을 단일 파티션에 대해 수행할 수 있습니다. 또한 테넌트 내의 모든 항목에서 트랜잭션 논리를 구현할 수 있습니다. 다중 테넌트는 컨테이너를 공유하기 때문에 각 테넌트에 대한 추가 헤드룸을 프로비전하는 대신 테넌트에 대한 리소스를 풀링하여 저장소 및 처리량을 단일 컨테이너 내에 저장할 수 있습니다. hello 단점은 테 넌 트 당 성능 격리는입니다. 테 넌 트에 대 한 toohello 전체 컨테이너 대상으로 vs 증가 적용 하는 성능/처리량 증가 됩니다.
* 테넌트당 하나의 컨테이너: 각 테넌트에 고유한 컨테이너가 있습니다. 이 모델에서는 테넌트당 성능을 예약할 수 있습니다. Cosmos DB의 새로운 프로비전 가격 책정 모델을 사용하는 이 모델은 몇몇 테넌트가 있는 다중 테넌트 응용 프로그램에 보다 비용 효율적입니다.

또한 collocates 작은 테 넌 트 및 테 넌 트 tootheir 자체 더 큰 컨테이너 마이그레이션합니다는 조합/계층화 된 접근 방식을 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요를 제공했습니다. 

* [Azure Cosmos DB에서 프로비전된 처리량](request-units.md)에 대한 자세한 정보
* [Azure Cosmos DB에서 글로벌 배포](distribute-data-globally.md)에 대한 자세한 정보



