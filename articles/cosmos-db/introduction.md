---
title: Cosmos DB aaaIntroduction tooAzure | Microsoft Docs
description: "Azure Cosmos DB에 대해 알아봅니다. 이 전세계에 배포된 멀티모델 데이터베이스는 낮은 대기 시간, 탄력적 확장성 및 고가용성을 위해 구축되었습니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>시작 tooAzure Cosmos DB

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 멀티모델 데이터베이스입니다. Hello 단추 클릭으로 Azure Cosmos DB 있습니다 눈금 처리량 및 저장소 독립적으로 tooelastically 개수에 관계 없이 Azure의 지리적 위치입니다. 다른 데이터베이스 서비스에서는 제공하지 않는 포괄적 [Service Level Agreement(서비스 수준 약정)](https://aka.ms/acdbsla)(SLA)를 통해 처리량, 대기 시간, 가용성 및 일관성을 보장합니다.

![Azure Cosmos DB는 탄력적 확장, 낮은 대기 시간 보증, 일관성 모델 5개, 포괄적 보장 SLA를 갖춘 전세계에 배포된 데이터베이스 서비스입니다.](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Azure Cosmos DB를 활용하는 솔루션

모든 [웹, 모바일, 게임 및 응용 프로그램 IoT](use-cases.md) toohandle 대량의 읽기 및 쓰기에 필요한는 [글로벌](distribute-data-globally.md) Azure Cosmos DB에서 이익을 얻을 다양 한 데이터에 대 한 짧은 응답 시간 함께 크기 조정 [보장](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 가용성, 높은 처리량, 짧은 대기 시간 및 튜닝할 수 있는 일관성.

## <a name="key-capabilities"></a>주요 기능
전 세계적으로 분산된 데이터베이스 서비스로 Azure Cosmos DB 확장 가능한 응답성이 높은 응용 프로그램을 구축 하는 기능 toohelp 다음 hello를 제공 합니다.

* **턴키 글로벌 배포**
    * 할 수 있습니다 [데이터 배포](distribute-data-globally.md) tooany 수가 [Azure 지역](https://azure.microsoft.com/regions/), hello로 [단추 클릭](tutorial-global-distribution-documentdb.md)합니다. 이렇게 하면 tooput 수 있는 사용자가 보장 hello 가장 낮은 대기 시간을 최소화 tooyour 고객 데이터. 
    * Azure Cosmos DB를 사용 하 여 멀티 호 밍 Api, hello 앱 항상 영역 가장 가까운 hello 이며 데이터 센터에 가장 가까운 요청 toohello 송신할 위치를 알고 있습니다. 이 모든 가능한 구성 변경 없이 쓰기 지역 설정 있고, 원하는 고 hello 영역을 읽을 많은 rest 자동으로 처리 됩니다.

* **데이터 액세스 및 쿼리를 위한 다중 데이터 모델 및 주요 API**
    * Azure Cosmos DB에 고유 하 게 작성 된 hello atom 레코드 시퀀스 (ARS) 기반된 데이터 모델에는 포함 하지만 제한 되지 toodocument, 그래프, 키-값, 테이블 및 칼럼 형식 데이터 모델의 여러 데이터 모델을 지원 합니다.
    * 여러 언어에서 사용할 수 있는 Sdk와 데이터 모델을 따르는 hello에 대 한 Api 지원 됩니다.
        * [DocumentDB API](documentdb-introduction.md)
        * [MongoDB API](mongodb-introduction.md)
        * [Table API](table-introduction.md)
        * [Graph(Gremlin) API](graph-introduction.md)
        * 추가 데이터 모델 제공 예정 

* **전세계에서 필요 시 탄력적으로 처리량 및 저장소 확장**
    * 데이터베이스 처리량을 [초](request-units.md) 단위로 간편하게 확장하고 원하면 언제든 변경할 수 있습니다. 
    * 저장소 크기를 확장 [투명 하 고 자동으로](partition-data.md) toohandle 크기 요구 사항이 이제 하 고 계속 합니다.

* **응답성 높은 중요 업무용 응용 프로그램 빌드**
    * Azure Cosmos DB 종단 간 대기 시간이 짧은 hello에 99th 백분위 수 tooits 고객을 보장합니다. 
    * 일반적인 1 KB 항목 Cosmos DB 보장 읽기의 종단 간 대기 시간이 10ms 미만 및 인덱싱된 쓰기 hello 99 번째 백분위 수에 15 밀리초 미만 내 동일 hello Azure 지역입니다. hello 중앙값 대기 시간이 너무 지나치게 적으면 (아래에서 5 밀리초)입니다.

* **"Always On" 가용성 보장**
    * 단일 지역 내에서 99.99%의 가용성을 제공합니다.
    * Tooany 수의 배포 [Azure 지역](https://azure.microsoft.com/regions) 높은 가용성을 위한 합니다.
    * 데이터 무손실 보장을 통해 하나 이상의 지역에서 [오류를 시뮬레이션](regional-failover.md)합니다. 

* **전 세계적으로 분산된 응용 프로그램의 작성 hello 올바른 방법**
    * 5 개의 [일관성 모델](consistency-levels.md) 모델은 다양 한 tooNoSQL와 비슷한 방식으로 결과적 일관성 및 사이 저것 hello 모두 강력한 SQL과 유사한 일관성을 제공 합니다. 
  
* **환불 보장**
    * 데이터를 빠르게 가져오지 않는다면 환불할 수 있습니다. 
    * 가용성, 대기 시간, 처리량 및 일관성에 대한 [서비스 수준 계약](https://aka.ms/acdbsla)  

* **데이터베이스 스키마/인덱스 관리 없음**
    * 데이터베이스 스키마와 인덱스를 응용 프로그램의 스키마와 동기 상태로 유지하는 것에 대해 염려하지 않아도 됩니다. 이제 스키마 제약이 없는 것입니다. 
    * Azure Cosmos DB의 데이터베이스 엔진은 완전히 스키마를 알 수 없는 – 모든 hello 데이터 스키마 이나 인덱스 없이 수집 하 고 매우 빠른 쿼리 사용을 자동으로 인덱싱됩니다. 

* **낮은 소유 비용**
    * 5 tooten 번 [비용 효율이](https://aka.ms/cosmos-db-tco-paper) 관리 되지 않는 솔루션 보다 합니다.
    * DynamoDB보다 세 배 저렴합니다.

## <a name="capability-comparison"></a>기능 비교

Azure Cosmos DB hello 비관계형 및 관계형 데이터베이스의 가장 뛰어난 기능을 제공합니다.

| 기능 | 관계형 데이터베이스   | 비관계형(NoSQL) 데이터베이스 |    Azure Cosmos DB |
| --- | --- | --- | --- |
| 글로벌 분포 | 아니요 | 아니요 | 예, 멀티 호밍 API를 사용하여 30개 이상의 지역에서 턴키 배포|
| 수평적 확장 | 아니요 | 예 | 예, 독립적으로 저장소 및 처리량을 확장할 수 있습니다. | 
| 대기 시간 보장 | 아니요 | 예 | 예, <10ms인 읽기의 99% 및 <15 ms인 쓰기 | 
| 고가용성 | 아니요 | 예 | 예, Cosmos DB는 Always On이며 PACELC 장단점이 있고, 자동 및 수동 장애 조치 옵션을 제공합니다.|
| 데이터 모델 + API | 관계형 + SQL | 다중 모델 + OSS API | 다중 모델 + SQL + OSS API(추가 서비스 예정) |
| SLA | 예 | 아니요 | 예, 대기 시간, 처리량, 일관성, 가용성에 대한 포괄적 SLA |


## <a name="next-steps"></a>다음 단계
다음 요약 설명서를 통해 Azure Cosmos DB를 시작해 보세요.

* [Azure Cosmos DB의 DocumentDB API 시작](create-documentdb-dotnet.md)
* [Azure Cosmos DB의 MongoDB API 시작](create-mongodb-nodejs.md)
* [Azure Cosmos DB의 Graph API 시작](create-graph-dotnet.md)
* [Azure Cosmos DB의 Table API 시작](create-table-dotnet.md)
