---
title: "테이블 API aaaIntroduction tooAzure Cosmos DB | Microsoft Docs"
description: "짧은 대기 시간 사용 하 여 키 값 데이터의 쿼리 massive 볼륨이 hello 인기 OSS MongoDB Api 한 Azure Cosmos DB toostore를 사용 하는 방법을 배웁니다."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Cosmos DB 소개 tooAzure: 테이블 API

[Azure Cosmos DB](introduction.md)는 업무에 중요한 응용 프로그램에 대한 Microsoft의 전역 분산 다중 모델 데이터베이스 서비스입니다. Azure Cosmos DB에는 [턴키 글로벌 메일](distribute-data-globally.md), [처리량 및 저장소의 탄력적인 크기 조정을](partition-data.md) hello 99 번째 백분위 수 전 세계, 자리 밀리초 대기 [5 개 잘 정의 된 일관성 수준이](consistency-levels.md), 모두 만족할된 높은 가용성을 보장할 수 [업계를 주도하 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)합니다. Azure Cosmos DB [데이터를 자동으로 인덱싱됩니다](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal 스미카 및 인덱스 관리를 요구 하지 않고 있습니다. 또한 다중 모델 방식이며, 문서, 키-값, 그래프 및 열 형식 데이터 모델을 지원합니다. 

![Azure Table Storage API 및 Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Azure Cosmos DB hello 유연한 스키마, 예측 가능한 성능, 글로벌 메일 및 처리량이 높은 키-값 저장소를 필요로 하는 응용 프로그램에 대 한 테이블 (미리 보기) API 제공 합니다. 테이블 API hello 제공 hello Azure 테이블 저장소와 동일한 기능을 하지만 hello Azure Cosmos DB 엔진의 hello 혜택을 활용 합니다. 

Toouse 높은 저장소 및 처리량 요구 사항이 낮은 테이블에 대 한 Azure 테이블 저장소를 계속할 수 있습니다. Azure Cosmos DB 향후 업데이트에서 저장소 액세스에 최적화 된 테이블에 대 한 지원을 제공 하 고 기존 및 새 Azure 테이블 저장소 계정 수 없으며 tooAzure Cosmos DB 업그레이드 됩니다.

## <a name="premium-and-standard-table-apis"></a>프리미엄 및 표준 테이블 API
현재 Azure 테이블 저장소를 사용 하는 경우 이점을 tooAzure Cosmos DB "프리미엄 table" 미리 보기를 이동 하 여 다음 hello를 얻을 수 있습니다.

|  | Azure Table Storage | Azure Cosmos DB: Table Storage(미리 보기) |
| --- | --- | --- |
| 대기 시간 | 빠르지만 대기 시간에 상한 없음 | 읽기와 쓰기에 대 한 자리 밀리초 대기 시간을 기반으로 < 대기 시간이 10ms 읽고 및 < 대기 시간이 15 밀리초의 hello world 모든 차원에서의 hello 99 번째 백분위 수에 작성 |
| 처리량 | 확장성이 뛰어나지만 전용 처리량 모델 없음. 20,000작업/초의 테이블 확장 한도 | [테이블당 전용 예약된 처리량](request-units.md)으로 탁월한 확장성(SLA로 지원). 계정은 처리량에 상한이 없으며 테이블당 1000만 개 이상의 초당 작업 지원 |
| 글로벌 배포 | HA에 대해 선택적으로 읽을 수 있는 보조 읽기 지역이 하나 있는 단일 지역. 장애 조치를 시작할 수 없음 | [턴키 글로벌 메일](distribute-data-globally.md) 하나의 too30 + 지역,에 대 한 지원 [자동 및 수동 장애 조치](regional-failover.md) 언제 든 지의 hello world |
| 인덱싱 | PartitionKey 및 RowKey에 대한 기본 인덱스만 제공. 보조 인덱스 없음 | 모든 속성에 대한 자동 및 전체 인덱싱, 인덱스 관리 없음 |
| 쿼리 | 쿼리 실행 시 기본 키에 대한 인덱스를 사용하고 그렇지 않은 경우 검색합니다. | 쿼리는 빠른 쿼리 시간을 위해 속성에 대해 자동 인덱싱을 활용할 수 있습니다. Azure Cosmos DB의 데이터베이스 엔진은 집계, 지리 공간 및 정렬을 지원할 수 있습니다. |
| 일관성 | 주 지역 내에서 강력, 보조 지역에서 최종적 | [5 개의 잘 정의 된 일관성 수준이](consistency-levels.md) 가용성, 대기 시간, 처리량 및 일관성 오프 tootrade 응용 프로그램 요구 사항에 따라 |
| 가격 | 저장소 최적화  | 처리량 최적화 |
| SLA | 99.9% 가용성 | 단일 지역 및 기능 tooadd를 자세한 내에서 99.99% 가용성 가용성을 높이기 위해 지역입니다. 일반 공급에서 [업계 최고의 포괄적인 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) |

## <a name="how-tooget-started"></a>Tooget 시작 하는 방법

Hello에 Azure Cosmos DB 계정을 만드는 [Azure 포털](https://portal.azure.com), 시작 및 우리의 [.NET을 사용 하 여 테이블 API에 대 한 퀵 스타트](create-table-dotnet.md)합니다. 

## <a name="next-steps"></a>다음 단계

다음은 몇 가지 포인터 tooget 시작한입니다.
* [Hello 테이블 API를 사용 하 여.NET 응용 프로그램 빌드](create-table-dotnet.md)
* [Hello.net에서 테이블 API를 사용 하 여 개발](tutorial-develop-table-dotnet.md)
* [Hello 테이블 API를 사용 하 여 테이블 데이터를 쿼리 합니다.](tutorial-query-table.md)
* [어떻게 테이블 API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello](tutorial-global-distribution-table.md)
* [.NET용 Azure Cosmos DB 테이블 API SDK](table-sdk-dotnet.md)
