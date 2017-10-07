---
title: "키 값 저장소 – 비용 개요로 Cosmos DB aaaAzure | Microsoft Docs"
description: "키 값 저장소로 Azure Cosmos DB를 사용 하 여 hello 낮은 비용에 알아봅니다."
keywords: "키 값 저장소"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>키 값 저장소로서의 Azure Cosmos DB – 비용 개요

Azure Cosmos DB는 대규모의 고가용성 응용 프로그램을 쉽게 빌드하기 위한 전역으로 분산된 다중 모델 데이터베이스 서비스입니다. 기본적으로 Azure Cosmos DB 효율적으로 수집 하는 모든 hello 데이터를 자동으로 인덱싱됩니다. 이를 통해 모든 종류의 데이터에 대해 빠르고 일관된 [SQL](documentdb-sql-query.md)(및 [JavaScript](programming.md)) 쿼리가 가능해집니다. 

이 문서는 간단한 쓰기를 위해 Azure Cosmos DB의 hello 비용에 설명 하 고 키/값 저장소로 사용 될 때 읽기 작업 합니다. 쓰기 작업에는 문서의 삽입, 바꾸기, 삭제 및 upsert가 포함됩니다. 99.99% 가용성을 보장 하는 것 외에도 Azure Cosmos DB 제공 보장 < 읽기에 대 한 대기 시간이 10ms 및 < (인덱싱된) hello에 대 한 대기 시간이 15 밀리초 hello 99 번째 백분위 수에 각각 기록 합니다. 

## <a name="why-we-use-request-units-rus"></a>RU(요청 단위)를 사용하는 이유

Azure DB Cosmos 성능 hello 양을 기반 프로 비전 된 [요청 단위](request-units.md) (RU) hello 파티션에 대 한 합니다. 두 번째 세분성에 있고 RUs/sec 및 RUs/min 구입한 hello를 프로 비전 ([toobe 시간별 청구 hello와 혼동된 하지](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs는 hello 프로 비전 hello 응용 프로그램에 필요한 처리량을 간소화 하는 통화로 고려 되어야 합니다. 고객을 구별 toothink 읽기 및 쓰기 용량 단위 필요는 없습니다. RUs의 hello 단일 동시성 모델 읽기와 쓰기 간의 tooshare hello를 프로 비전 된 용량 효율성을 만듭니다. 이 프로 비전 된 용량이 모델 hello 서비스 tooprovide를 예측 가능 하 고 일관 된 처리량, 짧은 대기 시간 및 고가용성을 보장할 수 있습니다. 마지막으로, RU toomodel 처리량 사용 하는 각 프로 비전 된 RU에도 정의 된 리소스 (메모리, 코어). 초당 RU는 IOPS만이 아닙니다.

전 세계적으로 분산된 데이터베이스 시스템으로 Cosmos DB 추가 toohigh 가용성의 대기 시간, 처리량 및 일관성에 SLA를 제공 하는 Azure 서비스만을 hello 됩니다. 프로 비전 하는 hello 처리량은 적용 된 tooeach Cosmos DB 데이터베이스 계정에 연결 된 hello 지역입니다. 읽기에 대 한 Cosmos DB 제공 잘 정의 된 여러 [일관성 수준](consistency-levels.md) 에서 toochoose에 대 한 합니다. 

hello 다음 표에 나와 hello RUs 필요한 tooperform 읽기 수 및 1KB에서 100KBs의 문서 크기에 따라 트랜잭션을 기록 합니다.

|항목 크기|1 읽기|1 쓰기|
|-------------|------|-------|
|1KB|1RU|5RU|
|100KB|10RU|50RU|

## <a name="cost-of-reads-and-writes"></a>읽기 및 쓰기의 비용

1, 000 RU/sec를 프로 비전 하면 too3.6m RU/시간 금액이 고 $0.08 hello 시간 (미국 hello와 유럽에서 일)에 대 한 비용이 듭니다. 1KB 크기 문서에서는 프로비전된 처리량을 사용해서 3.6m 읽기 또는 0.72m 쓰기(초당 3.6m RU/5)를 사용할 수 있음을 의미합니다. 정규화 된 toomillion 읽기 및 쓰기, hello 비용 $0.022 /m 읽기 수 ($0.08 3.6 /) 및 $0.111/m 쓰기 ($0.08 0.72 /). hello 당 비용 백만 hello 테이블 아래에 나와 있는 것 처럼 최소화 됩니다.

|항목 크기|1m 읽기|1m 쓰기|
|-------------|-------|--------|
|1KB|$0.022|$0.111|
|100KB|$0.222|$1.111|


대부분의 hello 기본 blob 또는 백만 읽기 트랜잭션 및 $5 백만 쓰기 트랜잭션당 당 개체 저장소 서비스 요금이 $0.40 합니다. 최적으로 사용 하는 경우 Cosmos DB too98 %1KB 트랜잭션 위해 이러한 다른 솔루션 보다 더 적게 듭니다 될 수 있습니다.

## <a name="next-steps"></a>다음 단계

Azure Cosmos DB 리소스 프로비저닝 최적화에 대한 새 문서를 계속 확인하세요. 에 가능한 toouse 느껴집니다 그 동안 hello 우리의 [RU 계산기](https://www.documentdb.com/capacityplanner)합니다.

