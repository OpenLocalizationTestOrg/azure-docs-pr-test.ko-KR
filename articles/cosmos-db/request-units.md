---
title: "aaaRequest 단위 및 예상 처리량-Azure Cosmos DB | Microsoft Docs"
description: "Toounderstand,이 지정 하 고 Azure Cosmos DB에서 요청 단위 요구 사항을 예측 하는 방법에 대해 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Azure Cosmos DB의 요청 단위
지금 사용 가능: Azure Cosmos DB [요청 단위 계산기](https://www.documentdb.com/capacityplanner). 자세한 내용을 보려면 [처리량 요구 예측](request-units.md#estimating-throughput-needs)을 참조하세요.

![처리량 계산기][5]

## <a name="introduction"></a>소개
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스입니다. Azure Cosmos DB와 함께 하지 않는 toorent 가상 컴퓨터, 소프트웨어를 배포 했거나 데이터베이스를 모니터링 합니다. Azure Cosmos DB은 운영 하 고 Microsoft 상위 엔지니어 toodeliver world 클래스 가용성, 성능 및 데이터 보호에서 지속적으로 모니터링 됩니다. [DocumentDB SQL](documentdb-sql-query.md)(문서), MongoDB(문서), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/)(키-값) 및 [Gremlin](https://tinkerpop.apache.org/gremlin.html)(그래프)가 모두 기본적으로 지원되므로 원하는 API를 사용하여 데이터에 액세스할 수 있습니다. Cosmos DB Azure의 hello 통화는 hello 요청 단위 (RU)입니다. RUs와 않아도 tooreserve 읽기/쓰기 용량 또는 프로 비전 CPU, 메모리 및 IOPS입니다.

Azure Cosmos DB 간단한 읽기에서 사이의 다른 작업에 다양 한 Api 지원 하며 toocomplex graph 쿼리를 씁니다. 정규화 된 수량 할당 된 모든 요청 값이 같으면 이후 **요청 단위** 계산 필요한 tooserve hello 요청의 hello 금액에 따른 합니다. 작업에 대 한 요청 단위 수가 hello 결정적 이며 hello 응답 헤더를 통해 Azure Cosmos DB에서 모든 작업에서 사용 하는 요청 단위 수를 추적할 수 있습니다. 

tooprovide 예측 가능한 성능, 필요한 tooreserve 처리량이 100 단위에서 RU 수/초입니다. 

이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.  

* 요청 단위 및 요청 요금이 무엇인가요?
* 컬렉션에 대해 요청 단위 용량을 지정하려면 어떻게 해야 하나요?
* 내 응용 프로그램에 필요한 요청 단위를 어떻게 추정할 수 있나요?
* 컬렉션의 요청 단위 용량을 초과하면 어떻게 되나요?

Azure Cosmos DB 다중 모델 데이터베이스는 때 중요 한 toonote 문서 API, graph API에 대 한 그래프/노드 및 테이블 API에 대 한 테이블/엔터티 tooa 컬렉션/문서는 이라고 합니다. 처리량이이 문서에서는 toohello 개념 컨테이너/항목의 일반화 됩니다.

## <a name="request-units-and-request-charges"></a>요청 단위 및 요청 요금
Azure Cosmos DB 하 여 신속 하 고 예측 가능한 성능을 제공 *예약* 리소스 toosatisfy 응용 프로그램의 처리량이 필요 합니다.  응용 프로그램 로드 시간에 따른 변경을 패턴에 액세스 하기 때문에 Azure Cosmos DB tooeasily 증가 허용 또는 예약 된 처리량 tooyour 사용 가능한 응용 프로그램의 hello 양을 줄입니다.

Azure Cosmos DB에서는 예약된 처리량이 초당 처리되는 요청 단위로 지정됩니다. 상상할 수 있는 요청 단위 처리량 통화로, 그에 따라 있습니다 *예약* 는 양의 초 단위로에서 사용할 수 있는 tooyour 응용 프로그램 요청 단위를 보장 합니다.  문서 작성, 쿼리 수행, 문서 업데이트 등 Azure Cosmos DB의 각 작업에서는 CPU, 메모리 및 IOPS를 사용합니다.  즉, 각 작업이 *요청 요금*을 발생시키고, 요청 요금은 *요청 단위*로 표시됩니다.  응용 프로그램의 처리량 요구 사항 함께 요청 단위 요금에 영향을 주는 hello 요인을 이해 가능한 한 효과적으로 비용으로 응용을 프로그램 toorun 있습니다 있습니다. hello 쿼리 탐색기는 쿼리는 매우 유용한 도구 tootest hello 코어 이기도합니다.

다음 비디오에서는 Aravind Ramachandran 요청 단위 및 Azure Cosmos DB와 함께 예측 가능한 성능의 설명 하는 여기서 hello를 시청 하 여 시작 하는 것이 좋습니다.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Azure Cosmos DB에서 요청 단위 용량 지정
Hello 수를 지정 하는 새 컬렉션, 테이블 또는 그래프를 시작할 때 예약 하려면 (초당 RU) 초당 요청 단위입니다. Hello 프로 비전 된 처리량에 따라, Azure Cosmos DB 할당 실제 파티션을 toohost 컬렉션 및 분할/rebalances 데이터 파티션에서 커짐에 따라 합니다.

Azure Cosmos DB 파티션 키 toobe 컬렉션은 2, 500 요청 단위를 통해 프로 비전 또는 더 높은 때을 지정 해야 합니다. 파티션 키는도 필요한 tooscale 컬렉션의 처리량 hello 향후 2, 500 요청 단위를 초과 합니다. 따라서이 가장 좋습니다 tooconfigure는 [파티션 키](partition-data.md) 초기 처리량에 관계 없이 컨테이너를 만들 때. 이기 때문에 데이터를 여러 파티션에 분할 toobe 해야할 필요한 toopick 카디널리티가 높은 (고유 값 100 toomillions) 컬렉션/테이블/그래프 및 요청 균일 하 게 하 여 확장할 있습니다 Azure Cosmos DB 수 있도록 하는 파티션 키입니다. 

> [!NOTE]
> 파티션 키는 논리적 경계이며 실제 경계가 아닙니다. 따라서 toolimit hello 고유 파티션 키 값 수가 필요 하지 않습니다. 더 나은 toohave 더 분명가 실제로 Azure Cosmos DB에 더 많은 부하 분산 옵션, 보다 키 값을 분할 합니다.

다음은 3, 000으로 컬렉션을 만들기 위한 코드 조각 사용 하 고 초당 단위 hello.NET SDK 요청:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB는 처리량의 예약 모델에서 작동합니다. 즉, 처리량 양을 hello에 대 한 요금이 청구 됩니다 *예약*적극적으로 어느 정도의 처리량 인지에 관계 없이 *사용*합니다. 응용 프로그램의 로드, 데이터 및 사용 패턴 변경 위쪽 / 아래쪽에 쉽게 확장할 수으로 Sdk 통해 예약 된 RUs 양을 hello 또는 hello를 사용 하 여 [Azure 포털](https://portal.azure.com)합니다.

각 컬렉션/테이블/그래프 매핑된 tooan `Offer` hello 프로 비전 된 처리량에 대 한 메타 데이터가 Cosmos db에서 Azure 리소스입니다. 컨테이너에 대 한 hello 해당 제안 리소스를 찾는 다음 hello 새 처리량 값으로 업데이트 하 여 할당 된 hello 처리량을 변경할 수 있습니다. 다음 컬렉션 too5의 hello 처리량을 변경 하기 위한 코드 조각으로 사용 하 고 초당 요청 단위 000 hello.NET SDK.

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Hello 처리량을 변경 하면 영향 toohello 컨테이너의 사용 가능한 시간이 있습니다. 일반적으로 hello 새롭게 예약 된 처리량은 hello 새 처리량의 응용 프로그램에 몇 초 이내 효과적입니다.

## <a name="request-unit-considerations"></a>요청 단위 고려 사항
Cosmos DB Azure 컨테이너에 대 한 요청 단위 tooreserve hello 수 예측, 경우에 변수 고려 사항에 따라 중요 한 tootake hello:

* **항목 크기**. 크기가 증가 hello 사용 된 단위 tooread 또는 hello 데이터 쓰기 늘어납니다.
* **항목 속성 개수**. 문서/노드/ntity hello 속성 수가 증가 함에 따라 증가 합니다 hello 사용 된 단위 toowrite 모든 속성의 기본 인덱싱 가정 합니다.
* **데이터 일관성**. Strong 또는 Bounded Staleness의 데이터 일관성 수준을 사용 하는 경우 추가 단위가 소비 된 tooread 항목 됩니다.
* **인덱싱된 속성**. 각 컨테이너의 인덱스 정책에 따라 기본적으로 인덱싱되는 속성이 결정됩니다. 인덱싱된 속성의 hello 수를 제한 하거나 lazy 인덱싱을 사용 하도록 설정 하 여 요청 단위 사용을 줄일 수 있습니다.
* **문서 인덱싱**. 각 항목은 자동으로 인덱싱됩니다 기본적으로 항목의 일부 하지 tooindex 선택 하는 경우 더 적은 요청 단위를 사용 합니다.
* **쿼리 패턴**. hello 복잡 한 쿼리 요청 단위의 수는 작업에 대 한 사용 되는 영향을 줍니다. 조건자의 hello 개수, hello 조건자, 프로젝션, Udf의 수와 모든 영향을 줄의 hello 비용 hello 원본 데이터 집합의 hello 크기의 특성 작업을 쿼리 합니다.
* **스크립트 사용량**.  저장된 프로시저 및 트리거는 쿼리와 마찬가지로 수행 되는 hello 작업의 hello 복잡성에 따라 요청 단위 사용 합니다. 응용 프로그램을 개발할 때는 hello 요청 충전 검사 헤더 toobetter 각 작업은 요청 단위 용량을 사용 하는 방법을 이해 합니다.

## <a name="estimating-throughput-needs"></a>필요한 처리량 예측
요청 단위는 요청 처리 비용의 정규화된 측정값입니다. 단일 요청 단위 (시스템 속성은 제외) 10 개의 고유 속성 값을 항목으로 구성 된 단일 1KB hello 처리 필요한 용량 tooread를 (통해 자체 링크 또는 id)를 나타냅니다. 요청 toocreate (삽입) 바꾸거나 hello 동일 항목을 사용 하면 추가 처리가 hello 서비스에서 삭제 및 함으로써 더 요청 단위입니다.   

> [!NOTE]
> 1 개의 요청이 단위의 hello 초기는 1KB tooa 간단한를 해당 항목에 대 한 자체 링크 또는 hello 항목의 id로 가져옵니다.
> 
> 

예를 들어 다음 요청 수를 보여 주는 표는 세 가지 다른 항목 크기 (1KB, 4KB 이며 및 64KB) 및 두 개의 서로 다른 성능 수준에서 단위 tooprovision (500 읽기/초 + 100 쓰기/초 및 500 읽기/초 + 500 쓰기/초)입니다. 세션에서 구성 된 hello 데이터 일관성 및 인덱싱 정책을 hello tooNone 설정 되었습니다.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>항목 크기</strong></p></td>
            <td valign="top"><p><strong>읽기/초</strong></p></td>
            <td valign="top"><p><strong>쓰기/초</strong></p></td>
            <td valign="top"><p><strong>요청 단위</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1,000RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3,000RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1.3) + (100 * 7) = 1,350RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1.3) + (500 * 7) = 4,150RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9,800RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29,000RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Hello 요청 단위 계산기를 사용 하 여
미세 하 게 toohelp 고객의 처리량은 예측이 잘못 조정, 기반으로 웹이 [요청 단위 계산기](https://www.documentdb.com/capacityplanner) toohelp hello 요청 단위에 필요한 예측 등과 같은 일반적인 작업을 합니다.

* 항목 만들기(쓰기)
* 항목 읽기
* 항목 삭제
* 항목 업데이트

hello 도구에는 데이터 저장소 요구를 제공 하는 hello 샘플 항목을 기반으로 예측에 대 한 지원이 포함 되어 있습니다.

Hello 도구를 사용 하는 것은 간단 합니다.

1. 하나 이상의 대표 항목을 업로드합니다.
   
    ![항목 toohello 요청 단위 계산기를 업로드 합니다.][2]
2. tooestimate 데이터 저장소 요구 사항 hello 총 수를 입력 하려는 toostore 항목의 합니다.
3. 입력 항목 수가 hello 만들기, 읽기, 업데이트 및 삭제 작업 (초 단위 기준) 필요 합니다. 항목 업데이트 작업의 tooestimate hello 요청 단위 요금이 일반적인 필드 업데이트가 포함 된 위의 1 단계에서 hello 샘플 항목의 복사본을 업로드 합니다.  예를 들어 항목 업데이트 lastLogin 및 userVisits, 라는 두 개의 속성을 수정 일반적으로 다음 hello 샘플 항목을 복사 하기만 하는 경우 이러한 두 속성에 대 한 hello 값 업데이트 되 고 복사 하는 hello 항목을 업로드 합니다.
   
    ![Hello 요청 단위 계산기의 처리량 요구 사항을 입력합니다][3]
4. 클릭 하 여 계산 하 고 hello 결과 확인 합니다.
   
    ![요청 단위 계산기 결과][4]

> [!NOTE]
> 인덱싱된 속성의 크기와 hello 수 측면에서 크게 달라 집니다 항목 형식을 설정한 경우 다음 각 예제 업로드 *형식* 일반적인 항목 toohello의 도구를 다음 hello 결과 계산 합니다.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Hello Azure Cosmos DB 요청 충전 응답 헤더를 사용 하 여
사용자 지정 헤더를 포함 하는 hello Azure Cosmos DB 서비스에서에서 모든 응답 (`x-ms-request-charge`) hello 요청에 대 한 사용 된 hello 요청 단위를 포함 하 합니다. 이 헤더 hello Azure Cosmos DB Sdk를 통해 액세스할 수 이기도합니다. .NET SDK hello RequestCharge hello ResourceResponse 개체의 속성을입니다.  쿼리에 대 한 hello Azure 포털에서에서 Azure Cosmos DB 쿼리 탐색기 hello 실행 된 쿼리에 대 한 요청 충전 정보를 제공 합니다.

![쿼리 탐색기 hello에 RU 요금을 검사 하는 중][1]

이 점을 고려 hello 양을 응용 프로그램에 필요한 예약 된 처리량을 예측 하기 위한 한 가지 방법은 toorecord hello 요청 단위 충전 응용 프로그램에서 사용 되는 대표적인 항목에 대해 실행 되는 일반적인 작업와 관련 된 다음 매 초 마다 수행 예상 hello 작업 수를 예측 합니다.  있는지 toomeasure 되며 일반적인 쿼리 및 뿐만 아니라 Azure Cosmos DB 스크립트 사용 등.

> [!NOTE]
> 인덱싱된 속성의 크기와 hello 수 측면에서 크게 달라 집니다 항목 형식을 설정한 경우 다음 hello 적용 가능한 작업과 요청 단위 충전 각 연결 된 기록 *형식* 일반적인 항목의 합니다.
> 
> 

예:

1. 기록 hello 요청 단위 효율적인 (삽입)를 만드는 일반적인 항목입니다. 
2. 일반적인 항목을 읽을 레코드 hello 요청 단위 요금이 합니다.
3. 레코드 hello 요청 단위 효율적인 일반적인 항목을 업데이트 합니다.
4. 레코드 hello 요청 단위 요금이 청구 일반적이 고 일반적인 항목 쿼리.
5. 레코드 hello 요청 단위 효율적인 사용자 정의 스크립트 (저장된 프로시저, 트리거, 사용자 정의 함수) hello 응용 프로그램에서 활용
6. 작업의 수를 예상 하는 hello 주어진 단위를 예상 toorun 매 초 마다 hello 필요한 요청을 계산 합니다.

### <a id="GetLastRequestStatistics"></a>MongoDB API의 GetLastRequestStatistics 명령 사용
MongoDB에 대 한 API 지원 사용자 지정 명령 *getLastRequestStatistics*, 지정 된 작업에 대 한 요청 충전 hello를 검색 하기 위한 합니다.

예를 들어 hello Mongo 셸을, tooverify hello 요청 요금은 hello 작업을 실행 합니다.
```
> db.sample.find()
```

다음을 실행 하는 hello 명령 *getLastRequestStatistics*합니다.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

이 점을 고려 hello 양을 응용 프로그램에 필요한 예약 된 처리량을 예측 하기 위한 한 가지 방법은 toorecord hello 요청 단위 충전 응용 프로그램에서 사용 되는 대표적인 항목에 대해 실행 되는 일반적인 작업와 관련 된 다음 매 초 마다 수행 예상 hello 작업 수를 예측 합니다.

> [!NOTE]
> 인덱싱된 속성의 크기와 hello 수 측면에서 크게 달라 집니다 항목 형식을 설정한 경우 다음 hello 적용 가능한 작업과 요청 단위 충전 각 연결 된 기록 *형식* 일반적인 항목의 합니다.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>MongoDB API 포털 메트릭 사용
MongoDB 데이터베이스 toouse hello에 대 한 API에 대 한 요금이 청구 요청 단위의 좋은 예측 하는 가장 간단한 방법은 tooget hello [Azure 포털](https://portal.azure.com) 메트릭. Hello로 *요청 수가* 및 *요청 충전* 차트, 요청 단위를 사용 중인 각 작업은 요청 단위의 수의 예측을 얻을 수 있습니다 상대 tooone 차지 다른 합니다.

![MongoDB API 포털 메트릭][6]

## <a name="a-request-unit-estimation-example"></a>요청 단위 추정 예제
Hello ~ 1 KB 문서 다음을 고려 합니다.

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> 문서는 hello 시스템 위의 hello 문서 크기가 1KB 보다 약간 짧으므로 계산 되므로 Azure Cosmos DB에서 축소 됩니다.
> 
> 

hello 다음 표에서 대략적인 요청을이 항목에 대 한 일반적인 작업에 대 한 단위 요금이 (hello 대략적인 요청 단위 충전 hello 계정 일관성 수준이 너무 설정 된 것으로 가정 "세션" 하 고 모든 항목은 자동으로 인덱스):

| 작업 | 요청 단위 요금 |
| --- | --- |
| 항목 만들기 |~15 RU |
| 항목 읽기 |~1 RU |
| ID로 항목 쿼리 |~2.5 RU |

또한이 표에서 단위 요금이 hello 응용 프로그램에서 사용 되는 일반적인 쿼리에 대 한 대략적인 요청을 보여줍니다.

| 쿼리 | 요청 단위 요금 | 반환된 항목 수 |
| --- | --- | --- |
| ID로 음식 선택 |~2.5 RU |1 |
| 제조업체로 음식 선택 |~7 RU |7 |
| 음식 그룹으로 선택하고 무게로 주문 |~70 RU |100 |
| 음식 그룹의 상위 10개 음식 선택 |~10 RU |10 |

> [!NOTE]
> RU 요금 hello 반환 되는 항목 수에 따라 다릅니다.
> 
> 

이 정보를 통해 작업 및 쿼리 / 초 라고 생각이 제공 된 응용 프로그램 hello 수에 대 한 hello RU 요구 사항을 예상할 수 있습니다.

| 작업/쿼리 | 예상되는 초당 수 | 필요한 RU |
| --- | --- | --- |
| 항목 만들기 |10 |150 |
| 항목 읽기 |100 |100 |
| 제조업체로 음식 선택 |25 |175 |
| 음식 그룹으로 선택 |10 |700 |
| 상위 10개 선택 |15 |총 150 |

이 예에서는 필요한 평균 처리량이 1,275 RU/s로 예상됩니다.  100 가장 가까운 toohello를 반올림이 응용 프로그램의이 컬렉션에 대 한 1, 300 000RU/s를 프로 비전는 했습니다.

## <a id="RequestRateTooLarge"></a> Azure Cosmos DB에서 예약된 처리량 제한 초과
Hello 예산 비어 있으면 요청 단위 소비 초 당 속도로 계산 됨을 기억 하십시오. Hello를 초과 하는 응용 프로그램에 대 한 프로 비전 된 요청 단위는 컨테이너에 대 한 요청 수 hello 속도 hello 예약 된 수준 아래로 떨어질 때까지 toothat 컬렉션 제한 됩니다. (HTTP 상태 코드 429) RequestRateTooLargeException hello 요청 하 고 반환 hello x-ms-다시 시도-후-ms을 나타내는 헤더 hello 양의 시간 (밀리초), 사용자 hello 하기 전에 대기 해야 hello 서버 스로틀 되는 경우 종료 미리 됩니다. hello 요청을 다시 시도 합니다.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

측면 hello 서버에 지정 된 retry-after 헤더 hello.NET 클라이언트 SDK 및 LINQ 쿼리에 다음 하지 않아도이 예외와 toodeal hello 현재 버전의.NET 클라이언트 SDK hello이이 응답을 암시적으로 catch 하는 대로 hello 시간의 대부분을 사용 하는 경우 및 hello 요청을 다시 시도 횟수입니다. 계정 여러 클라이언트에서 동시에 액세스 하는, 하지 않는 한 hello 다음 재시도 성공 합니다.

누적 클라이언트가 여러 개 있는 경우 hello 기본 다시 시도 동작이 수 요구 사항을 충족 하지, 및 hello 클라이언트에서는 상태 코드 429 toohello 응용 프로그램과 함께 DocumentClientException throw hello 요청 속도 이상으로 작동 합니다. 이와 같은 경우에 다시 시도 동작이 및 응용 프로그램의 오류 처리 루틴 또는 hello hello 컨테이너에 대 한 예약 된 처리량을 증가에서 논리를 처리를 고려할 수 있습니다.

## <a id="RequestRateTooLargeAPIforMongoDB"></a> MongoDB API에서 예약된 처리량 제한 초과
Hello 속도 hello 예약 된 수준 아래로 떨어질 때까지 컬렉션에 대 한 사용자를 프로 비전 하는 hello 요청 단위를 초과 하는 응용 프로그램 제한 됩니다. 사용 하 여 hello 요청 스로틀 발생할 때 hello 백 엔드 끝납니다 여기서는 *16500* 오류 코드- *너무 많은 요청*합니다. 기본적으로 API MongoDB에 대 한 자동으로 다시 too10 시간을 반환 하기 전에 *너무 많은 요청* 오류 코드입니다. 많은 발생 하는 경우 *너무 많은 요청* 오류 코드를 응용 프로그램의 오류 처리 루틴에에서 추가 하거나 다시 시도 동작을 고려할 수 있습니다 또는 [hellohello컬렉션에대한예약된처리량을증가](set-throughput.md).

## <a name="next-steps"></a>다음 단계
toolearn Azure Cosmos DB 데이터베이스와 예약 된 처리량에 대 한 자세한이 리소스를 살펴봅니다.

* [Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/).
* [Azure Cosmos DB에서 데이터 분할](partition-data.md)

Azure Cosmos DB에 대해 자세히 toolearn hello Azure Cosmos DB 참조 [설명서](https://azure.microsoft.com/documentation/services/cosmos-db/)합니다. 

확장 및 성능 Azure Cosmos DB를 사용 하 여 테스트 시작 tooget 참조 [성능 및 배율 Azure Cosmos DB를 사용 하 여 테스트](performance-testing.md)합니다.

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
