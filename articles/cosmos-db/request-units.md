---
title: "요청 단위 및 예상 처리량 - Azure Cosmos DB | Microsoft Docs"
description: "Azure Cosmos DB의 요청 단위 요구 사항을 이해, 지정 및 예측하는 방법을 알아봅니다."
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
ms.date: 11/02/2017
ms.author: mimig
ms.openlocfilehash: c7aadb4e535ed221f882f251324b6d4e633c2d5e
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="request-units-in-azure-cosmos-db"></a>Azure Cosmos DB의 요청 단위
지금 사용 가능: Azure Cosmos DB [요청 단위 계산기](https://www.documentdb.com/capacityplanner). 자세한 내용을 보려면 [처리량 요구 예측](request-units.md#estimating-throughput-needs)을 참조하세요.

![처리량 계산기][5]

## <a name="introduction"></a>소개
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스입니다. Azure Cosmos DB를 사용하면 가상 머신을 임대하거나, 소프트웨어를 배포하거나, 데이터베이스를 모니터링할 필요가 없습니다. 세계적 수준의 가용성, 성능 및 데이터 보호를 제공하기 위해 Microsoft의 최고 엔지니어가 Azure Cosmos DB를 작동하고 지속적으로 모니터링합니다. 원하는 API를 사용하여 데이터에 액세스할 수 있습니다. [SQL API](documentdb-introduction.md), [MongoDB API](mongodb-introduction.md), [Table API](table-introduction.md) 및 [Graph API](graph-introduction.md)를 통한 Gremlin 데이터 액세스가 모두 기본적으로 지원됩니다. Azure Cosmos DB의 통화는 RU(요청 단위)입니다. RU를 사용하면 읽기/쓰기 용량을 예약하거나 CPU, 메모리 및 IOPS를 프로비전할 필요가 없습니다.

Azure Cosmos DB는 단순한 읽기 및 쓰기부터 복잡한 그래프 쿼리에 이르기까지 다양한 작업에서 많은 API를 지원합니다. 모든 요청 값이 같지 않으므로 요청을 처리하는 데 필요한 계산의 양에 기반하여 정규화된 양의 **요청 단위**가 할당됩니다. 작업에 대한 요청 단위 수는 결정적이며 응답 헤더를 통해 Azure Cosmos DB의 모든 작업에 사용된 요청 단위 수를 추적할 수 있습니다. 

예측 가능한 성능을 제공하려면 100 RU/초 단위로 처리량을 예약해야 합니다. 

이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.  

* 요청 단위 및 요청 요금이 무엇인가요?
* 컬렉션에 대해 요청 단위 용량을 지정하려면 어떻게 해야 하나요?
* 내 응용 프로그램에 필요한 요청 단위를 어떻게 추정할 수 있나요?
* 컬렉션의 요청 단위 용량을 초과하면 어떻게 되나요?

Azure Cosmos DB는 다중 모델 데이터베이스이므로 이 문서에서는 문서 API의 경우 컬렉션/문서를, Graph API의 경우 그래프/노드를, 테이블 API의 경우 테이블/엔터티를 가합니다. 이 문서에서는 컨테이너로서의 컬렉션, 그래프 또는 테이블 개념과 항목으로서의 문서, 노드 또는 엔터티의 개념에 대해 설명합니다.

## <a name="request-units-and-request-charges"></a>요청 단위 및 요청 요금
Azure Cosmos DB는 응용 프로그램의 처리량 수요를 충족하도록 리소스를 *예약*하여 신속하고 예측 가능한 성능을 제공합니다.  시간이 지나면 응용 프로그램 로드 및 액세스 패턴이 변하는데, Azure Cosmos DB를 사용하면 응용 프로그램에 제공되는 예약된 처리량을 간편하게 늘리거나 줄일 수 있습니다.

Azure Cosmos DB에서는 예약된 처리량이 초당 처리되는 요청 단위로 지정됩니다. 요청 단위란 응용 프로그램에 보장되는 초당 요청 단위의 양을 *예약* 할 수 있는 처리량 통화라고 생각하시면 됩니다.  문서 작성, 쿼리 수행, 문서 업데이트 등 Azure Cosmos DB의 각 작업에서는 CPU, 메모리 및 IOPS를 사용합니다.  즉, 각 작업이 *요청 요금*을 발생시키고, 요청 요금은 *요청 단위*로 표시됩니다.  응용 프로그램의 처리량 요구 사항과 함께 요청 단위 요금에 영향을 주는 요소를 이해하면 응용 프로그램을 최대한 경제적으로 실행할 수 있습니다. 쿼리 탐색기는 쿼리의 핵심을 테스트하는 데 유용한 도구이기도 합니다.

먼저 Aravind Ramachandran이 Azure Cosmos DB의 요청 단위 및 예측 가능한 성능을 설명하는 다음 동영상을 보는 것이 좋습니다.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Azure Cosmos DB에서 요청 단위 용량 지정
새 컬렉션, 테이블 또는 그래프를 시작할 때 예약하려는 초당 요청 단위 수(초당 RU)를 지정합니다. 프로비전된 처리량에 따라 Azure Cosmos DB는 컬렉션을 호스트하는 실제 파티션을 할당하고 확장됨에 따라 파티션에서 데이터를 분할/균형 조정합니다.

Azure Cosmos DB 컨테이너를 고정 또는 무제한으로 만들 수 있습니다. 고정 크기 컨테이너는 최대 제한 10GB 및 10,000RU/s 처리량을 설정할 수 있습니다. 무제한 컨테이너를 만들려면 최소 1,000RU/s 처리량과 [파티션 키](partition-data.md)를 지정해야 합니다. 데이터는 여러 파티션에 분할되어야 하므로 카디널리티가 높은(백~수백만 개의 고유 값) 파티션 키를 선택해야 합니다. 고유 값이 많은 파티션 키를 선택하면 컬렉션/테이블/그래프 및 요청이 Azure Cosmos DB에서 균일하게 확장될 수 있습니다. 

> [!NOTE]
> 파티션 키는 논리적 경계이며 실제 경계가 아닙니다. 따라서 특정 파티션 키 값의 수를 제한할 필요가 없습니다. 사실 Azure Cosmos DB에 더 많은 부하 분산 옵션이 있으므로 고유 파티션 키 값이 적은 것보다 많은 것이 더 좋습니다.

.NET SDK를 사용하여 초당 3,000 요청 단위로 컬렉션을 만들기 위한 코드 조각은 다음과 같습니다.

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB는 처리량의 예약 모델에서 작동합니다. 즉, 활발하게 *사용된* 처리량에 관계없이 *예약된* 처리량에 따라 요금이 청구됩니다. 응용 프로그램의 부하, 데이터 및 사용 패턴이 변하면 그에 따라 SDK를 통해 또는 [Azure Portal](https://portal.azure.com)을 사용하여 예약된 RU 양을 간단하게 늘리거나 줄일 수 있습니다.

각 컬렉션/테이블/그래프는 프로비전된 처리량에 대한 메타데이터가 있는 Azure Cosmos DB의 `Offer` 리소스에 매핑됩니다. 컨테이너에 해당하는 제품 리소스를 조회한 다음 새 처리량 값으로 업데이트하여 할당된 처리량을 변경할 수 있습니다. 다음 코드 조각에서는 .NET SDK를 사용하여 컬렉션 처리량을 5,000RU/s로 변경합니다.

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

처리량을 변경할 때 컨테이너의 가용성에는 영향을 주지 않습니다. 일반적으로 새로 예약된 처리량은 새 처리량의 응용 프로그램에서 몇 초 이내에 유효합니다.

## <a name="request-unit-considerations"></a>요청 단위 고려 사항
Azure Cosmos DB 컨테이너에 대해 예약할 요청 단위 수를 추정하는 경우 다음 변수를 고려해야 합니다.

* **항목 크기**. 크기가 증가할수록 데이터를 읽거나 쓰는 데 사용되는 단위도 증가합니다.
* **항목 속성 개수**. 모든 속성의 기본 인덱싱을 가정할 경우 속성 수가 증가할수록 문서/노드/엔터티를 쓰는 데 사용되는 단위가 증가합니다.
* **데이터 일관성**. 강력 또는 제한된 부실 데이터 일관성 수준을 사용하는 경우 항목을 읽는 데 추가 단위가 사용됩니다.
* **인덱싱된 속성**. 각 컨테이너의 인덱스 정책에 따라 기본적으로 인덱싱되는 속성이 결정됩니다. 인덱싱되는 속성 수를 제한하거나 지연 인덱싱을 사용하면 요청 단위 사용을 줄일 수 있습니다.
* **문서 인덱싱**. 기본적으로 각 항목은 자동으로 인덱싱됩니다. 일부 항목을 인덱싱하지 않도록 선택하면 더 적은 요청 단위를 사용합니다.
* **쿼리 패턴**. 쿼리의 복잡성은 작업에 사용되는 요청 단위의 양에 영향을 줍니다. 조건자의 수, 조건자의 특성, 프로젝션, UDF 수 및 원본 데이터 집합의 크기는 모두 쿼리 작업의 비용에 영향을 줍니다.
* **스크립트 사용량**.  쿼리와 마찬가지로, 저장된 프로시저 및 트리거는 수행하는 작업의 복잡성에 따라 요청 단위를 사용합니다. 응용 프로그램을 개발하면서 요청 요금 헤더를 검사하면 각 작업이 요청 단위 용량을 어떻게 사용하는지 파악하는 데 도움이 됩니다.

## <a name="estimating-throughput-needs"></a>필요한 처리량 예측
요청 단위는 요청 처리 비용의 정규화된 측정값입니다. 단일 요청 단위는 10개의 고유한 속성 값(시스템 속성 제외)으로 구성된 1KB 항목 하나를 읽는 데(self 링크 또는 ID를 통해) 필요한 처리 용량을 나타냅니다. 동일한 항목을 생성(삽입), 대체 또는 삭제하는 요청은 서비스에서 추가 처리를 사용하므로 더 많은 요청 단위가 사용됩니다.   

> [!NOTE]
> 1KB 항목에 대한 요청 단위 1개의 기준은 항목의 self 링크 또는 ID에 의한 간단한 GET에 해당합니다.
> 
> 

예를 들어 다음 표에는 세 가지 항목 크기(1KB, 4KB 및 64KB)와 두 가지 다른 성능(500읽기/초 + 100쓰기/초 및 500읽기/초 +500 쓰기/초)에서 프로비전할 요청 단위가 나와 있습니다. 데이터 일관성은 세션에서 구성되었으며 인덱싱 정책은 None으로 설정되었습니다.

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

### <a name="use-the-request-unit-calculator"></a>요청 단위 계산기를 사용합니다.
고객이 해당 처리량 예측을 미세 조정하도록 도우려면 다음을 포함한 일반적인 작업에 대한 요청 단위 요구 사항을 예측하는 웹 기반 [요청 단위 계산기](https://www.documentdb.com/capacityplanner)를 사용합니다.

* 항목 만들기(쓰기)
* 항목 읽기
* 항목 삭제
* 항목 업데이트

이 도구에는 제공한 샘플 항목을 기반으로 하여 데이터 저장소 필요를 예측하는 지원이 포함됩니다.

도구를 사용하는 것은 간단합니다.

1. 하나 이상의 대표 항목을 업로드합니다.
   
    ![요청 단위 계산기에 항목 업로드][2]
2. 데이터 저장소 요구 사항을 예측하려면 저장할 항목의 총수를 입력합니다.
3. 항목 수를 입력하여 필요한 작업을 만들고 읽고 업데이트하고 삭제합니다(초 단위별로). 항목 업데이트 작업의 요청 단위 요금을 예측하려면 일반적인 필드 업데이트가 포함된 위의 1단계에서 샘플 항목의 복사본을 업로드합니다.  예를 들어 항목 업데이트가 일반적으로 lastLogin 및 userVisits라는 두 가지 속성을 수정하는 경우 샘플 항목을 복사하고 해당 두 가지 속성의 값을 업데이트한 다음 복사된 항목을 업로드합니다.
   
    ![요청 단위 계산기에 처리량 요구 입력][3]
4. 결과를 계산하고 검토하도록 클릭합니다.
   
    ![요청 단위 계산기 결과][4]

> [!NOTE]
> 인덱싱된 속성과 크기 및 개수가 완전히 다른 항목 유형이 있는 경우 일반 항목의 각 *유형*을 도구에 업로드한 다음 결과를 계산합니다.
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a>Azure Cosmos DB 요청 요금 응답 헤더 사용
Azure Cosmos DB 서비스의 모든 응답에는 요청에 사용된 요청 단위가 포함된 사용자 지정 헤더(`x-ms-request-charge`)가 포함되어 있습니다. 이 헤더는 Azure Cosmos DB SDK를 통해 액세스할 수도 있습니다. .NET SDK에서 RequestCharge는 ResourceResponse 개체의 속성입니다.  쿼리의 경우 Azure Portal의 Azure Cosmos DB 쿼리 탐색기는 실행된 쿼리에 대한 요청 요금 정보를 제공합니다.

![쿼리 탐색기에서 RU 요금을 검사하는 중][1]

이 점을 염두에 두고, 응용 프로그램에 필요한 예약된 처리량을 예측하는 한 가지 방법은 응용 프로그램에서 사용하는 대표적인 항목에 대해 실행되는 일반 작업과 연결된 요청 단위 요금을 기록한 다음, 예상되는 초당 수행되는 작업 수를 추정하는 것입니다.  일반 쿼리 및 Azure Cosmos DB 스크립트 사용량도 측정하여 포함해야 합니다.

> [!NOTE]
> 인덱싱된 속성과 크기 및 개수가 완전히 다른 항목 유형이 있는 경우에는 일반 항목의 각 *유형*과 연결된 적용 가능한 작업 요청 단위 요금을 기록합니다.
> 
> 

예: 

1. 일반 항목을 만드는(삽입하는) 요청 단위 요금을 기록합니다. 
2. 일반 항목을 읽는 요청 단위 요금을 기록합니다.
3. 일반 항목을 업데이트하는 요청 단위 요금을 기록합니다.
4. 일반적이고 공통적인 항목 쿼리의 요청 단위 요금을 기록합니다.
5. 응용 프로그램에서 활용하는 모든 사용자 지정 스크립트(저장된 프로시저, 트리거, 사용자 정의 함수)의 요청 단위 요금을 기록합니다.
6. 예상되는 초당 작업 수를 고려하여 필요한 요청 단위를 계산합니다.

## <a id="GetLastRequestStatistics"></a>MongoDB API의 GetLastRequestStatistics 명령 사용
MongoDB API는 지정된 작업에 대한 요청 비용을 검색하는 데 사용자 지정 명령인 *getLastRequestStatistics*를 지원합니다.

예를 들어 Mongo Shell에서 요청 비용을 확인할 작업을 실행합니다.
```
> db.sample.find()
```

다음으로 *getLastRequestStatistics* 명령을 실행합니다.
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

이 점을 염두에 두고, 응용 프로그램에 필요한 예약된 처리량을 예측하는 한 가지 방법은 응용 프로그램에서 사용하는 대표적인 항목에 대해 실행되는 일반 작업과 연결된 요청 단위 요금을 기록한 다음, 예상되는 초당 수행되는 작업 수를 추정하는 것입니다.

> [!NOTE]
> 인덱싱된 속성과 크기 및 개수가 완전히 다른 항목 유형이 있는 경우에는 일반 항목의 각 *유형*과 연결된 적용 가능한 작업 요청 단위 요금을 기록합니다.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>MongoDB API 포털 메트릭 사용
MongoDB API 데이터베이스에 대한 요청 단위 요금을 적절히 추정하는 가장 간단한 방법은 [Azure Portal](https://portal.azure.com) 메트릭을 사용하는 것입니다. *요청 수* 및 *요청 요금* 차트에서 각 작업에서 사용하는 요청 단위 수와 서로 상대적으로 사용하는 요청 단위 수를 추정할 수 있습니다.

![MongoDB API 포털 메트릭][6]

## <a name="a-request-unit-estimation-example"></a>요청 단위 추정 예제
다음과 같은 1KB보다 작은 문서를 가정하겠습니다.

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
> 문서가 Azure Cosmos DB에서 축소되기 때문에 위에서 시스템이 계산한 문서 크기는 1KB보다 약간 작습니다.
> 
> 

다음 표에서는 이 항목의 일반 작업에 대한 대략적인 요청 단위 요금을 보여 줍니다(대략적인 요청 단위 요금은 계정 일관성 수준이 "세션"으로 설정되어 있고 모든 항목이 자동으로 인덱싱되는 것으로 가정).

| 작업 | 요청 단위 요금 |
| --- | --- |
| 항목 만들기 |~15 RU |
| 항목 읽기 |~1 RU |
| ID로 항목 쿼리 |~2.5 RU |

이 테이블은 응용 프로그램에 사용되는 일반 쿼리의 대략적인 요청 단위 요금도 보여 줍니다.

| 쿼리 | 요청 단위 요금 | 반환된 항목 수 |
| --- | --- | --- |
| ID로 음식 선택 |~2.5 RU |1 |
| 제조업체로 음식 선택 |~7 RU |7 |
| 음식 그룹으로 선택하고 무게로 주문 |~70 RU |100 |
| 음식 그룹의 상위 10개 음식 선택 |~10 RU |10 |

> [!NOTE]
> RU 요금은 반환되는 항목 수에 따라 다릅니다.
> 
> 

이 정보를 통해, 예상되는 초당 작업 및 쿼리 수에 따라 이 응용 프로그램에 필요한 RU를 예측할 수 있습니다.

| 작업/쿼리 | 예상되는 초당 수 | 필요한 RU |
| --- | --- | --- |
| 항목 만들기 |10 |150 |
| 항목 읽기 |100 |100 |
| 제조업체로 음식 선택 |25 |175 |
| 음식 그룹으로 선택 |10 |700 |
| 상위 10개 선택 |15 |총 150 |

이 예에서는 필요한 평균 처리량이 1,275 RU/s로 예상됩니다.  가장 가까운 100자리 숫자로 반올림하면 이 응용 프로그램의 컬렉션에 1,300 RU/s를 프로비전하면 됩니다.

## <a id="RequestRateTooLarge"></a> Azure Cosmos DB에서 예약된 처리량 제한 초과
요청 단위 소비는 예산이 비어 있는 경우 초당 비율로 평가된다는 점을 기억하세요. 컨테이너에서 프로비전된 요청 단위 속도를 초과하는 응용 프로그램의 경우 비율이 예약된 수준 이하로 떨어질 때까지 해당 컬렉션에 대한 요청이 제한됩니다. 제한이 발생하면 서버에서 RequestRateTooLargeException(HTTP 상태 코드 429)를 사용하여 선제적으로 요청을 종료하고, 사용자가 요청을 다시 시도할 수 있을 때까지 기다려야 하는 시간을 밀리초 단위로 표시하는 x-ms-retry-after-ms 헤더를 반환합니다.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

.NET 클라이언트 SDK 및 LINQ 쿼리를 사용하는 경우에는 거의 대부분 이 예외를 처리할 필요가 없습니다. .NET 클라이언트 SDK 최신 버전이 이 응답을 암시적으로 catch하고, 서버에서 지정한 retry-after 헤더를 준수하고, 요청을 다시 시도하기 때문입니다. 동시에 여러 클라이언트가 계정에 액세스하지만 않으면 다음 재시도가 성공할 것입니다.

여러 클라이언트가 누적적으로 요청 속도를 초과하여 작동하는 경우에는 기본 재시도 동작으로 충분하지 않을 수 있으며, 클라이언트가 응용 프로그램에 상태 코드 429와 함께 DocumentClientException을 throw합니다. 이 경우 응용 프로그램의 오류 처리 루틴에서 재시도 동작 및 논리를 처리하는 방법 또는 컨테이너에 대해 예약된 처리량을 늘리는 방법을 고려해 볼 수 있습니다.

## <a id="RequestRateTooLargeAPIforMongoDB"></a> MongoDB API에서 예약된 처리량 제한 초과
컬렉션에서 프로비전된 요청 단위를 초과하는 응용 프로그램의 경우 비율이 예약된 수준 이하로 떨어질 때까지 제한됩니다. 제한이 발생하면 백 엔드는 *16500* 오류 코드 - *너무 많은 요청*으로 요청을 먼저 종료합니다. 기본적으로 MongoDB API는 *너무 많은 요청* 오류 코드를 반환되기까지 최대 10번 자동으로 재시도합니다. *너무 많은 요청* 오류 코드가 자주 발생하면 응용 프로그램의 오류 처리 루틴에서 재시도 동작을 추가하거나 [컬렉션에 대해 예약된 처리량을 늘리는 방법](set-throughput.md)을 고려해 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계
Azure Cosmos DB 데이터베이스의 예약된 처리량에 대한 자세한 내용은 다음 리소스를 참조하세요.

* [Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/).
* [Azure Cosmos DB에서 데이터 분할](partition-data.md)

Azure Cosmos DB에 대한 자세한 내용은 Azure Cosmos DB [설명서](https://azure.microsoft.com/documentation/services/cosmos-db/)를 참조하세요. 

Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 시작하려면 [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
