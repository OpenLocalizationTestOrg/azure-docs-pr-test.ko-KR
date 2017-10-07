---
title: "toolive 시간을 사용 하 여 Azure Cosmos DB에서 aaaExpire 데이터 | Microsoft Docs"
description: "Microsoft Azure Cosmos DB TTL, 된 시간이 지나면 hello 시스템에서 자동으로 제거 된 hello 기능 toohave 문서를 제공 합니다."
services: cosmos-db
documentationcenter: 
keywords: "toolive 시간"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>만료 시간 toolive 자동으로 Azure Cosmos DB 컬렉션의 데이터
응용 프로그램은 방대한 양의 데이터을 생성하고 저장할 수 있습니다. 컴퓨터에서 생성한 이벤트 데이터, 로그 및 사용자 세션 정보와 같은 이 데이터 중 일부는 한정된 기간에만 사용할 수 있습니다. Hello 데이터가 려 hello 응용 프로그램의 나머지 toohello 요구 되 면 안전 toopurge이이 데이터 이며 응용 프로그램의 hello 저장소 요구를 줄이는 합니다.

Microsoft Azure Cosmos DB "toolive 시간" 또는 TTL 시간이 지나면 hello 데이터베이스에서 자동으로 제거 된 hello 기능 toohave 문서를 제공 합니다. toolive hello 기본 시간 hello 모음 수준에서 설정 하 고 문서 단위의 되 면 사용할 수 있습니다. TTL을 컬렉션 기본값으로 설정하거나 문서 수준에서 설정하면 Cosmos DB는 마지막으로 수정된 이후 해당 기간(초) 후에 존재하는 문서를 자동으로 제거합니다.

Cosmos db에서 toolive 시간 hello 문서 마지막으로 수정 된 경우에 대 한 오프셋을 사용 합니다. toodo이이 it hello를 사용 하 여 `_ts` 모든 문서에 있는 필드입니다. hello _ts 필드에는 unix 스타일 epoch 타임 스탬프 나타내는 hello 날짜와 시간입니다. hello `_ts` 필드는 문서를 수정 될 때마다 업데이트 됩니다. 

## <a name="ttl-behavior"></a>TTL 동작
hello TTL 기능이 두 수준-hello 컬렉션 수준과 hello 문서 수준에서 TTL 속성에 의해 제어 됩니다. hello 값 초 단위로 설정 하 고 hello에서 델타로 처리 됩니다 `_ts` hello 문서에 마지막으로 수정 합니다.

1. DefaultTTL hello 컬렉션에 대 한
   
   * 누락 된 (또는 집합 toonull)에 대해 설명 하는 경우 자동으로 삭제 되지 않습니다.
   * 있는 경우 hello 값은 "-1" 및 무한 – = 기본적으로 문서 만료 안 함
   * 있는 경우 hello 값은 일부 숫자 ("n") 및 – 문서 만료 "n" 초를 마지막으로 수정한 후
2. Hello 문서에 대 한 TTL: 
   
   * 속성은 DefaultTTL가 hello 부모 컬렉션에 대해 존재 하는 경우에 적용할 수 있습니다.
   * Hello 부모 컬렉션에 대 한 hello DefaultTTL 값을 재정의합니다.

Hello 문서가 만료 되어야 하는 즉시 (`ttl`  +  `_ts` > 현재 서버 시간 =), hello 문서 "만료 됨"으로 표시 됩니다. 없음 작업이 허용 됩니다. 이러한 문서에이 시간 이후 및 hello 수행 하는 쿼리 결과에서 제외 됩니다. hello 문서 hello 시스템에 물리적으로 삭제 되 고 나중에 선택적 hello 백그라운드에서 삭제 됩니다. 모든이 게 사용 하지 않도록 [요청 단위 (RUs)](request-units.md) hello 컬렉션 예산에서 합니다.

논리 위에 hello hello 행렬 뒤에 표시할 수 있습니다:

|  | Hello 모음에 DefaultTTL 누락/not 설정 | 컬렉션에서 DefaultTTL = -1 | 컬렉션에서 DefaultTTL = "n" |
| --- |:--- |:--- |:--- |
| 문서에서 TTL 누락 |아무것도 hello 문서와 컬렉션에 TTL의 개념이 없으므로 문서 수준에서 toooverride 합니다. |이 컬렉션에서 만료되는 문서가 없습니다. |이 컬렉션에 있는 hello 문서 간격 n 경과 하면 만료 됩니다. |
| 문서에서 TTL = -1 |Hello 컬렉션을 정의 하지 않은 이후 hello 문서 수준에서 toooverride hello DefaultTTL 속성 문서 재정의할 수 있는 것입니다. 문서에 대해 TTL hello 체제별 terpreted 되지 않습니다. |이 컬렉션에서 만료되는 문서가 없습니다. |이 컬렉션에 TTL = 1 hello 문서는 만료 되지 않습니다. 다른 모든 문서는 "n" 간격 후에 만료됩니다. |
| 문서에서 TTL = n |아무것도 hello 문서 수준에서 toooverride 합니다. 문서에 대해 TTL hello 시스템에 의해 해석 되지 않은 합니다. |TTL이 된 hello 문서 = n 초에서 간격 n 후 만료 됩니다. 다른 문서는 간격 -1을 상속하며 만료되지 않습니다. |TTL이 된 hello 문서 = n 초에서 간격 n 후 만료 됩니다. 다른 문서 hello 컬렉션에서 "n" 간격을 상속 합니다. |

## <a name="configuring-ttl"></a>TTL 구성
기본적으로 시간 toolive 모든 Cosmos DB 컬렉션에서 모든 문서에는 기본적으로 비활성화 됩니다.

## <a name="enabling-ttl"></a>TTL 사용
tooenable TTL 컬렉션 또는 컬렉션 내의 hello 문서에, 컬렉션 tooeither-1 또는 0이 아닌 양수의 tooset hello DefaultTTL 속성이 필요합니다. 기본적으로 hello 컬렉션의 모든 문서 만들겠습니다 영원히 하지만 hello Cosmos DB 서비스는이 기본값을 재정의 한 문서에 대 한이 컬렉션을 모니터링 해야 hello DefaultTTL 너무 1 의미를 설정 합니다.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>컬렉션에서 기본 TTL 구성
모르는 수 tooconfigure toolive는 기본 시간 모음 수준 에서입니다. tooset hello TTL 있는 컬렉션 후에 필요한 tooprovide hello 기간 (초)을 tooexpire 나타내는 0이 아닌 양의 숫자 hello 컬렉션의 모든 문서 hello hello 문서의 타임 스탬프를 마지막으로 수정한 (`_ts`). 또는 hello 기본 너무-1, toohello 컬렉션에 삽입 하는 모든 문서가 기본적으로 무기한 만들겠습니다 의미를 설정할 수 있습니다.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>문서에서 TTL 설정
또한 컬렉션에 기본 TTL toosetting 문서 수준에서 특정 TTL를 설정할 수 있습니다. 이렇게 hello 컬렉션의 hello 기본값 보다 우선 합니다.

* tooset hello TTL tooprovide 0이 아닌 양수를 나타내는 hello 기간 (초)을 tooexpire hello 문서 hello hello 문서의 타임 스탬프를 마지막으로 수정한 후 문서에 필요한 (`_ts`).
* 문서에 다음 hello 컬렉션의 기본 hello TTL 필드가 없으면 적용 됩니다.
* Hello 모음 수준에서 TTL 하지 않으면 TTL hello 컬렉션에 다시 사용 될 때까지 hello ttl hello 문서에 대해 무시 됩니다.

Tooset 문서에 대해 TTL 만료 hello 하는 방법을 보여 주는 코드 조각은 다음과 같습니다.

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>기존 문서에서 TTL 확장
Hello 문서에 대해 쓰기 작업을 수행 하 여 문서에 대해 TTL hello를 다시 설정할 수 있습니다. 이 작업은 설정 hello `_ts` toohello 현재 시간 및 hello 카운트다운 toohello hello에 의해 설정 된 대로 만료, 문서 `ttl`, 다시 시작 됩니다. Toochange hello를 원하는 경우 `ttl` 문서를 업데이트할 수 있습니다 hello 필드 설정할 수 있는 다른 필드와 작업을 수행할 수 있습니다.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>문서에서 TTL 제거
TTL이 문서에 설정 된 경우 해당 문서 tooexpire를 더 이상 사용 하지 않으려면 다음 hello 문서를 검색, hello TTL 필드를 제거 및 교체 하는 hello 서버의 hello 문서. Hello ttl hello 문서에서 제거 되 면 hello 기본값 hello 컬렉션은 적용 됩니다. toostop 만료 문서 tooset hello TTL 값 너무-1을 사용 해야 합니다 hello 컬렉션에서 상속 되지 않습니다.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>TTL 사용 안 함
toodisable hello DefaultTTL 속성 hello 컬렉션을 삭제 해야 하는 만료 된 문서를 찾고에서 TTL 컬렉션 및 중지 hello 백그라운드에서 완전히 처리 합니다. 이 속성을 삭제 하는 것은 설정 1 너무 다릅니다. -1 너무 설정 새 문서에 추가할 toohello 컬렉션 영원히 만들겠습니다 되지만 hello 컬렉션의 특정 문서에이 재정의할 수 있습니다. Hello 컬렉션에서이 속성을 제거 의미 문서가 예상 만료 시간 이전 명시적으로 재정의 문서가 있는 경우에 합니다.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>FAQ
**TTL의 비용은 얼마인가요?**

TTL이 문서에 없는 추가 비용 toosetting 있습니다.

**얼마나 오래 걸리는 toodelete 문서 hello TTL이 가동 되 면?**

hello 문서 hello TTL, 작동 중 이며 CRUD 또는 쿼리 Api 통해 액세스할 수 없게 됩니다 되는 즉시 만료 됩니다. 

**문서에서 TTL은 RU 요금에 영향을 주나요?**

아니요, Cosmos DB에서 TTL을 통해 만료된 문서를 삭제할 경우 RU 요금에 영향을 주지 않습니다.

**Hello TTL 기능만 해당 tooentire 문서 또는 개별 문서 속성 값 만료 될?**

TTL은 toohello 전체 문서를 적용합니다. Tooexpire 원하는 hello 부분 hello tooa 별도 "연결된" 문서에 본문에서 추출 하 고 TTL을 사용 하 여 해당 추출 된 문서에 대 한 문서 후 것의 일부만 좋습니다.

**Hello TTL 기능은 특정 인덱싱 요구 사항이 있습니까?**

예. hello 컬렉션 있어야 [인덱싱 정책 집합](indexing-policies.md) tooeither Consistent 또는 Lazy입니다. 시도 tooset DefaultTTL 집합 tooNone 인덱싱을 사용 하 여 컬렉션에 이미 설정 DefaultTTL 들어 있는 컬렉션에서 인덱싱을 해제 하는 동안 tooturn 됩니다 오류가 발생 합니다.

## <a name="next-steps"></a>다음 단계
Azure Cosmos DB에 대해 자세히 toolearn toohello 서비스 참조 [ *설명서* ](https://azure.microsoft.com/documentation/services/cosmos-db/) 페이지.

