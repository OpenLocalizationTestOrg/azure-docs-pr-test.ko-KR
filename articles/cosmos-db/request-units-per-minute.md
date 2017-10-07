---
title: "Azure CosmosDB: 분당 요청 단위(RU/m) | Microsoft Docs"
description: "사용 하 여 tooreduce 비용 분당 단위를 요청 하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Azure Cosmos DB의 분당 요청 단위

Azure Cosmos DB는 신속 하 고 예측 가능한 성능 및 크기 조정 응용 프로그램의 증가 함께 원활 하 게 실현 디자인 된 toohelp입니다. 초당 및 분당(RU/m) 단위 모두에서 Cosmos DB 컨테이너의 처리량을 프로비전할 수 있습니다. hello 분당 세분성에서 프로 비전 된 처리량은 사용 되는 toomanage 예기치 않은 hello 갑작스러운 작업량 증가에 초당 세분성에서 발생 합니다. 

이 문서에서는 hello 요청 단위 (RU/m) 분당 프로 비전 작동 하는 방법에 대 한 개요를 제공 합니다. hello RU/m의 프로비저닝 염두에서 목적은 tooprovide spiky 작업 부하 및 예측할 수 없는 요구 (특히 해야 할 경우 toorun 분석 운영 데이터를 기반으로) 예측 가능한 성능입니다. 고객 사용 hello 처리량 더 많은 처리량을 신속 하 게 확장할 수 있도록 프로 비전 할 toohave 주시기 바랍니다.

이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.

* 분당 요청 단위는 어떻게 작동하나요?
* 분 당 요청 단위 및 초당 요청 단위 간의 hello 차이점은 무엇입니까?
* 어떻게 tooprovision RU/m?
* 어떤 시나리오에서 분당 요청 단위를 프로비전하는 것이 좋은가요?
* 어떻게 toouse 내 비용 및 성능 메트릭을 포털 toooptimize hello?
* 어떤 종류의 요청에서 RU/m 예산을 소비할 수 있는지 정의하나요?

## <a name="provisioning-request-units-per-minute-rum"></a>분당 요청 단위(RU/m) 프로비전

Hello 두 번째 세분성 (000RU/s)에서 Azure Cosmos DB를 프로 비전 할 때 요청 처리량 해당 초 이내에 사용자를 프로 비전 하는 hello 용량을 초과 하지 않은 경우 짧은 대기 시간에 성공 하는 hello 보장을 가져옵니다. RU/m으로 해당 분 내에 요청이 성공 하는 hello 보장 적용 hello 분 hello 세분성이입니다. Toobursting 시스템 비교 얻게 되는 hello 성능을 예측할 수 및 계획 수 있는지 확인 했습니다.

작동을 프로 비전 하는 분당 hello 방법은 간단 합니다.

* RU/m 시간별 및 추가 tooRU/s에서 요금이 청구 됩니다. 자세한 내용은 Azure Cosmos DB [가격 책정 페이지](https://aka.ms/acdbpricing)를 방문하세요.
* RU/m은 컬렉션 수준에서 사용할 수 있습니다. Hello (Node.js, Java 또는.Net) Sdk 통해 또는 hello 포털을 통해 수행할 수 있습니다 (도 MongoDB API 작업 포함)
* 사용자를 프로 비전 하는 1, 000 RU/m 용량도 RU/m 설정 되 면, 모든 100RU/s 클라우드를 프로 비전 (hello 비율이 10 배)
* 요청 단위는 지정된 시간(초) 이내에 분당 프로비전을 초과한 경우에만 지정된 시간(초)에서 RU/m 프로비전을 사용합니다.
* 60 초 (UTC) 기간 끝을 hello 한 번, 분 프로 비전 당 hello 리필은
* RU/m은 파티션당 최대 5,000RU/s로 프로비전된 컬렉션에 대해서만 사용할 수 있습니다. 처리량 요구 사항을 확장하고 높은 수준의 파티션당 프로비전을 사용한 경우 경고 메시지가 표시됩니다.

아래에서는 구체적인 예로 고객이 100kRU/m인 10kRU/s를 프로비전합니다. 그러면 100,000RU/m인 10,000RU/s을 프로비전한 컬렉션에서 90초 동안 최대(50kRU/s) 프로비전에 대한 비용의 73%를 절약할 수 있습니다.

* 1 초: hello RU/m 예산은 100, 000에서 설정 됩니다.
* 3 초가: 두 번째 hello에 해당 하는 동안 요청 단위의 소비 된 11,010 RUs, 000RU/s 프로 비전 hello 위에 1,010 RUs 합니다. 따라서 1,010 RUs hello RU/m 예산에서 차감 됩니다. 98,990 RUs에 사용할 수 있는 hello hello RU/m 예산에 다음 57 초
* 29th 초: 급등 발생 한 해당 초 동안 (> 4x 초당 프로 비전 보다 높은) 요청 단위의 hello 소비 46,920 RUs 되었으며 합니다. 36,920 RUs 92,323 RUs (28 초) too55, 403 RUs (29th 초)에서 삭제 하는 hello RU/m 예산에서 차감 됩니다.
* 두 번째 61st: RU/m 예산 다시 too100, 000 RUs 설정 됩니다.
 
![Hello 소비를 보여주는 그래프를 Azure Cosmos DB의 프로 비전](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>RU/m을 사용하여 요청 단위 용량 지정

Hello 수를 지정 하는 Azure Cosmos DB 컬렉션을 만들 때 (초당 RU) 초당 요청 단위 hello 컬렉션에 대 한 예약 된 원하는 합니다. 분 당 tooadd RU 원하면 결정할 수 있습니다. Hello 포털 또는 hello SDK 통해이 작업을 수행할 수 있습니다. 

### <a name="through-hello-portal"></a>Hello 포털을 통해

분당 RU를 활성화 또는 비활성화하려면 컬렉션을 프로비전할 때 클릭해야 합니다. 

 ![보여 주는 스크린샷 어떻게 tooset RU/m hello Azure 포털에서](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Hello SDK 통해
먼저,이 중요 한 toonote RU/m은 다음 Sdk hello에 사용할 수만:

* .Net 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

다음은 두 번째, 30, 000 요청 단위 hello.NET SDK를 사용 하 여 분당 3000 요청 단위와 컬렉션을 만들기 위한 코드 조각이입니다.

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

다음 컬렉션 too5의 hello 처리량을 변경 하기 위한 코드 조각으로 사용 하 여 분 당 RU를 프로 비전 하지 초당 요청 단위 000 hello.NET SDK.

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>적합한 시나리오

이 섹션에서는 RU/m을 사용하기 위해 적합한 시나리오의 개요를 제공합니다.

**개발/테스트 환경:** 적합합니다. Hello 개발 단계에서 다른 작업이 있는 응용 프로그램을 테스트 하는 경우 RU/m 제공할 수 hello 유연성이이 단계에서. Hello 동안 [에뮬레이터](local-emulator.md) 좋은 무료 도구 tootest Azure Cosmos DB가 있습니다. 그러나 클라우드 환경에서 toostart 원하는 임시 성능 요구에 따라 RU/m으로 뛰어난 유연성을 해야 합니다. 처음에는 성능 요구 사항에 대해 염려하지 않고 개발하는 데 많은 시간을 투자합니다. Hello 최소 000RU/s 프로 비전부터 시작 하는 것이 좋습니다 하 고 RU/m을 사용 하도록 설정 합니다.

**예측할 수 없고 급증하는 분 단위 요구 사항:** 적합 – 비용 절감: 25-75%. RU/m이 크게 개선되었고 대부분의 프로덕션 시나리오가 해당 그룹에 속합니다. 실행 된 쿼리가 있을 경우 스파이크를 몇 번 1 분 내에 있는 IoT 작업이 있는 경우 때 시스템에서는 대량 삽입 hello에 동일한 time, spiky 처리 요구에 추가 용량이 필요 합니다. 아래의 단계별 접근 방식을 적용하여 리소스 요구 사항을 최적화하는 것이 좋습니다.

 ![5분 단위로 요청 사용을 보여 주는 그래프](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *그림 - RU 사용 벤치마크*

**편안함:** 적합 – 비용 절감: 10-20%. 경우에 따라 toohave 없으므로 걱정할 필요 하 고 잠재적인 최대치 및 제한에 대해 우려할 필요가 없습니다. 이 기능은 hello 오른쪽으로 한 드립니다. 이 경우에 RU/m을 사용하도록 설정하고 초당 프로비전을 약간 낮추는 것이 좋습니다. 이 경우는 하면 시도 하지 것입니다 toooptimize 적극적으로 사용자 프로 비전 하는 대로 위의 hello와에서 다릅니다. 오히려 사용 중인 "0 제한"에 가깝습니다.

임시 요구 사항이 중요 한 작업: 때로는 좋습니다 tooonly RU/m 예산 hello 예산 함을 알 수 있도록 액세스 adhoc 하거나 덜 중요 한 작업을 사용 하는 중요 한 작업입니다. 쉽게 hello 섹션 아래에 정의할 수 있습니다.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Hello 포털 메트릭 toooptimize 비용 및 성능을 사용 하 여

**Hello 이후 몇 주간에 처리량이 필요한 RUs 분 소비 toooptimize 모니터링 주위의 hello 콘텐츠와 개발 추가 했습니다.**

Hello 포털 메트릭을 통해 RU 대를 사용 하는 일반 RU 초 어느 정도의 시간 (분)을 볼 수 있습니다. 이러한 메트릭을 모니터링하면 프로비전을 최적화하는 데 도움이 됩니다. 

방법에 대 한 단계별 접근 방법이 권장 toouse RU/m tooyour 이점이 있습니다. 각 단계에 대해 (수도 시간, 일, 심지어 몇 주) 워크 로드의 전체 주기를 나타내는 hello RU 소비에 대해 간략하게 있어야 하면 프로 비전의 hello 사용률에 대 한 정보를 얻기 및 합니다.

이 접근 방법 hello 원칙은 아래 성능 조건에 일치 하는 지점을 프로 비전 가능한 tooa와 가까운으로 처리량 프로비저닝 toomake 것입니다. 

![5분 단위로 요청 사용을 보여 주는 그래프](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello 최적의 프로비저닝 지점 작업에 대 한 toounderstand가 필요합니다.

* 소비 패턴: 아니요, 자주 사용하지 않거나 지속적으로 급증하나요? 작은(평균 2배), 중간 또는 크게(평균 10배 이상) 급증하나요?
* 제한된 요청 백분율: 약간의 제한이 있는 경우에도 편하게 생각하나요? 그렇다면, 얼마나 그런가요? 

목표는 무엇을 식별 한 후 수 tooget 자세히 toohello 최적의 프로 비전 됩니다.

tooassist tooprovide toooptimize RU/m 소비에 따라 사용자 프로비저닝는 방법에 대 한는 전반적인 지침을 원하는 합니다. 이 지침은 tooall 종류의 워크 로드는 적용 되지 않습니다 되지만 hello 비공개 미리 보기의 정보에 따라 합니다. 자세히 알아보면 이러한 기준을 변경할 수 있습니다.

|RU/m % 사용률|RU/m의 사용률 수준|프로비전하기 위해 권장되는 작업|
|---|---|---|
|0-1%|과소 사용률|더 많은 RU/m 000RU/s tooconsume를 줄이려면|
|1-10%|정상 사용|계속 hello 동일 프로 비전 수준|
|10% 이상|과도 사용률|RU/m에서 000RU/s toorely 증가|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>작업에는 hello RU/m 예산 소비할 수 있는 선택

요청 수준에서 있습니다 수 또한 설정/해제 작업 형식에 관계 없이 RU/m 예산 tooserve hello 요청 합니다. 일반 프로 비전 된 RUs/sec 예산을 소비 되는 경우 hello 요청 hello RU/m 예산을 사용할 수 없는이 요청 제한 됩니다. RU/m 처리량 예산이 활성화된 경우 기본적으로 모든 요청은 RU/m 예산에서 처리됩니다. 

다음은 코드 조각 RU/m 예산 CRUD 및 쿼리 작업에 대 한 hello DocumentDB API를 사용 하 여 사용 하지 않도록 설정 합니다.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>다음 단계

이 문서에서는 Azure Cosmos DB에서 분할이 작동하는 방식, 분할된 컬렉션을 만드는 방법 및 응용 프로그램에 적합한 파티션 키를 선택하는 방법을 설명했습니다.

* Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행합니다. 샘플에 대해서는 [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.
* Hello로 코딩을 시작 해 [Sdk](documentdb-sdk-dotnet.md) 또는 hello [REST API](/rest/api/documentdb/)합니다.
* Azure Cosmos DB에서 [프로비전된 처리량](request-units.md)에 대한 자세한 정보 

