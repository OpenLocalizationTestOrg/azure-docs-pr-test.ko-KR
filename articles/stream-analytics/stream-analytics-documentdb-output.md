---
title: "스트림 분석에 대 한 aaaJSON 출력 | Microsoft Docs"
description: "비구조화된 JSON 데이터에 대한 데이터 보관 및 짧은 대기 시간 쿼리를 위해 Stream Analytics에서 JSON 출력의 대상을 Azure Cosmos DB로 지정할 수 있는 방법을 알아봅니다."
keywords: "JSON 출력"
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Stream Analytics에서 JSON 출력의 대상을 Azure Cosmos DB로 지정
비구조화된 JSON 데이터에 대한 데이터 보관 및 짧은 대기 시간 쿼리를 사용하기 위해 Stream Analytics에서 JSON 출력의 대상을 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)로 지정할 수 있습니다. 이 문서에서는 이 구성을 구현하기 위한 몇 가지 모범 사례를 설명합니다.

Cosmos DB에 익숙하지 않은 사용자, 살펴보세요 [Azure Cosmos DB 학습 경로](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget 시작 합니다. 

참고: Mongo DB API 기반 Cosmos DB 컬렉션은 현재 지원되지 않습니다. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>출력 대상으로서 Cosmos DB의 기본 사항
hello Azure Cosmos DB 출력 스트림 분석에서 쓰기를 스트림을 여 Cosmos DB 커넥터가 컬렉션으로 JSON 출력으로 결과 처리를 수 있습니다. 스트림 분석에서에서 만들지 않습니다 컬렉션 데이터베이스 대신 필요 toocreate을 선행 합니다. Cosmos DB 컬렉션의 hello 청구 비용 투명 tooyou 있고 일관성과 직접 사용 하 여 컬렉션의 용량 hello hello 성능을 조정할 수 있도록 않도록 이것이 [Cosmos DB Api](https://msdn.microsoft.com/library/azure/dn781481.aspx)합니다. 스트리밍 작업 toologically 별도 당 하나의 Cosmos DB 데이터베이스를 사용 하는 스트리밍 작업에 대 한 사용자 컬렉션을 좋습니다.

Hello Cosmos DB 컬렉션 옵션 중 일부는 다음과 같습니다.

## <a name="tune-consistency-availability-and-latency"></a>일관성, 가용성 및 대기 시간 조정
toomatch 응용 프로그램 요구 사항, Cosmos DB 있습니다 toofine 조정 hello 데이터베이스 및 컬렉션 및 확인 척도로 상대적 일관성, 가용성 및 대기 시간. 시나리오에서 읽기 및 쓰기 대기 시간에 대해 필요로 하는 읽기 일관성 수준에 따라 데이터베이스 계정에 대한 일관성 수준을 선택할 수 있습니다. 또한 기본적으로 Cosmos DB 인덱싱을 사용할 수 있도록 동기 각 CRUD 작업 tooyour 컬렉션에 있습니다. 이 다른 유용한 옵션 toocontrol hello Cosmos DB의 성능을 읽기/쓰기입니다. 이 항목에 자세한 내용은 hello 검토 [프로그램 데이터베이스 및 쿼리 일관성 수준 변경](../documentdb/documentdb-consistency-levels.md) 문서.

## <a name="upserts-from-stream-analytics"></a>Stream Analytics에서 Upsert
스트림 분석 통합 Cosmos DB와 함께 지정된 된 문서 ID 열에 따라 Cosmos DB 컬렉션에 tooinsert 또는 업데이트 레코드를 허용 합니다. 참조 된 tooas 이기도 한 *Upsert*합니다.

스트림 분석에서 tooa 문서 ID가 충돌 인해 삽입이 실패 하면 업데이트가 수행만 됩니다 한 낙관적 Upsert 방법을 사용 합니다. 이 업데이트 부분 업데이트가 toohello 문서에 새 속성 또는 기존 속성을 증분 방식으로 수행 교체의 추가 예: 수 있으므로 패치라고, 스트림 분석에서 수행 됩니다. Note hello 속성의 값 배열에서 JSON 문서에서에서 변경 작업으로 인해 덮어쓸 가져오는 hello 전체 배열, 즉, hello 배열 병합 되지 않습니다.

## <a name="data-partitioning-in-cosmos-db"></a>Cosmos DB의 데이터 분할
Cosmos DB [컬렉션 분할](../cosmos-db/partition-data.md) hello 데이터를 분할 하기 위한 방법을 권장 됩니다. 

단일 Cosmos DB 컬렉션에 대 한 스트림 분석 여전히 있습니다 toopartition을 hello 쿼리 패턴와 응용 프로그램의 성능 요구에 따라 데이터. 각 컬렉션 수 too10GB 데이터 (최대)이 고 현재 구성 방법은 tooscale 없습니다는를 포함 (또는 오버플로) 컬렉션입니다. 를 확장에 대 한 스트림 분석 하면 지정 된 접두사가 포함 된 toowrite toomultiple 컬렉션 (사용 정보를 아래 참조). 스트림 분석 일관 된 hello를 사용 하 여 [해시 파티션 확인자](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) hello 사용자에 따라 전략 PartitionKey 열 toopartition 해당 출력 레코드를 제공 합니다. hello hello 스트리밍 작업의 시작 시간에 접두사를 제공 하는 hello 사용 하 여 컬렉션으로 사용 됩니다 hello 출력 파티션 수 toowhich hello 작업 tooin 병렬 씁니다 (Cosmos DB 컬렉션 = 출력 파티션을). 삽입만 수행하는 지연 인덱싱을 사용하는 단일 컬렉션의 경우 약 0.4MB/초의 쓰기 처리량을 예상할 수 있습니다. 여러 컬렉션을 사용 하 여 증가 된 용량 및 있습니다 tooachieve 더 높은 처리량을 허용할 수 있습니다.

향후 hello에 tooincrease hello 파티션 수를 가져오려는 경우 toostop을 새로운 컬렉션 변환한 다음 hello 스트림 분석 작업을 다시 시작 하 고 기존 컬렉션에서 repartition hello 데이터 작업을 할 수 있습니다. PartitionResolver를 사용하고 샘플 코드와 함께 다시 분할하는 방법에 대한 자세한 내용은 후속 게시물에서 다룰 예정입니다. hello 문서 [분할과 Cosmos DB에 크기 조정](../documentdb/documentdb-partition-data.md) 도이 세부 정보를 제공 합니다.

## <a name="cosmos-db-settings-for-json-output"></a>JSON 출력에 대한 Cosmos DB 설정
Cosmos DB를 Stream Analytics의 출력으로 만들면 아래와 같은 정보를 묻는 메시지가 생성됩니다. 이 섹션에서는 hello 속성 정의 대해 설명 합니다.

분할된 컬렉션 | 여러 “단일 파티션” 컬렉션
---|---
![documentdb Stream Analytics 출력 화면](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![documentdb Stream Analytics 출력 화면](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> hello **여러 "단일 파티션" 컬렉션** 시나리오는 파티션 키가 필요 하 고 지원 되는 구성 합니다. 

* **출력 별칭** – ASA 쿼리에서이 출력 하는 별칭 toorefer  
* **계정 이름** – hello 이름 또는 끝점 URI hello Cosmos DB 계정입니다.  
* **계정 키** – hello Cosmos DB 계정에 대 한 hello 공유 액세스 키입니다.  
* **데이터베이스** – hello Cosmos DB 데이터베이스 이름입니다.  
* **컬렉션 이름 패턴** – hello 컬렉션 이름 또는 hello 컬렉션 toobe 사용에 대 한 해당 패턴입니다. hello 컬렉션 이름 형식은 파티션은 0부터 시작 하는 여기서 hello 선택적 {partition} 토큰을 사용 하 여 생성할 수 있습니다. 다음은 유효한 입력 샘플입니다.  
  1\) MyCollection – "MyCollection"이라는 이름의 컬렉션이 있어야 합니다.  
  2\) MyCollection{partition} – "MyCollection0”, “MyCollection1”, “MyCollection2” 등의 컬렉션이 있어야 합니다.  
* **파티션 키** – 선택 사항. 컬렉션 이름 패턴에 {parition} 토큰을 사용하는 경우에만 필요합니다. 출력 컬렉션 간에 분할에 대 한 출력 toospecify hello 키를 사용 하는 이벤트에 대 한 hello 필드의 hello 이름입니다. 단일 컬렉션 출력의 경우 임의의 출력 열(예: PartitionId)이 사용될 수 있습니다.  
* **문서 ID** – 선택 사항입니다. 출력 이벤트의 hello 필드의 hello 이름을 사용 하는 삽입 또는 업데이트 작업은 기반으로 toospecify hello 기본 키입니다.  
