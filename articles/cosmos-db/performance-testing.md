---
title: "Azure Cosmos DB 규모 및 성능 테스트 | Microsoft Docs"
description: "Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행하는 방법을 알아봅니다."
keywords: "성능 테스트"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Azure Cosmos DB를 사용한 성능 및 규모 테스트
성능 및 규모 테스트는 응용 프로그램 개발의 핵심 단계입니다. 대부분의 응용 프로그램에서 데이터베이스 계층은 전반적인 성능 및 확장성에 큰 영향을 미치므로 성능 테스트의 주요 구성 요소입니다. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 탄력적인 규모 및 예측 가능한 성능을 위해 작성되었으므로 고성능 데이터베이스 계층을 필요로 하는 응용 프로그램에 가장 적합합니다. 

이 문서는 개발자가 자신의 Cosmos DB 작업에 대한 성능 테스트 모음을 구현하거나 Cosmos DB에서 고성능 응용 프로그램 시나리오를 평가할 때 참조로 사용됩니다. 또한 이 문서는 데이터베이스의 격리된 성능 테스트에 중점을 두지만 프로덕션 응용 프로그램에 대한 모범 사례도 제공합니다.

이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.   

* Cosmos DB의 성능 테스트를 위한 샘플 .NET 클라이언트 응용 프로그램은 어디에서 찾을 수 있나요? 
* 클라이언트 응용 프로그램에서 Cosmos DB를 사용하여 높은 처리량 수준을 달성하려면 어떻게 하나요?

코드를 시작하려면 [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)에서 프로젝트를 다운로드하세요. 

> [!NOTE]
> 이 응용 프로그램의 목표는 적은 수의 클라이언트 컴퓨터를 사용하여 Cosmos DB에서 더 나은 성능을 얻기 위한 모범 사례를 제시하는 것입니다. 제한 없이 확장할 수 있는 서비스의 최대 용량을 보여 주려는 것은 아닙니다.
> 
> 

Cosmos DB의 성능 향상을 위한 클라이언트 쪽 구성 옵션에 대한 자세한 내용은 [Azure Cosmos DB 성능 팁](performance-tips.md)을 참조하세요.

## <a name="run-the-performance-testing-application"></a>성능 테스트 응용 프로그램 실행
가장 빠른 시작 방법은 아래 단계에 설명된 대로 아래의 .NET 샘플을 컴파일하고 실행하는 것입니다. 소스 코드를 검토하고 자체 클라이언트 응용 프로그램에 대해 비슷한 구성을 구현할 수도 있습니다.

**1단계:** [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)에서 프로젝트를 다운로드하거나 GitHub 리포지토리를 분기합니다.

**2단계:** App.config에서 EndpointUrl, AuthorizationKey, CollectionThroughput 및 DocumentTemplate(옵션)에 대한 설정을 수정합니다.

> [!NOTE]
> 높은 처리량의 컬렉션을 프로비전하기 전에 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하여 컬렉션당 비용을 추정합니다. Azure Cosmos DB는 시간 단위로 저장소 및 처리량의 비용을 별도로 청구하므로 테스트 후에 Azure Cosmos DB 컬렉션을 삭제하거나 처리량을 줄여 비용을 절감할 수 있습니다.
> 
> 

**3단계:** 명령줄에서 콘솔 앱을 컴파일하고 실행합니다. 다음과 유사한 출력이 표시됩니다.

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**4단계(필요한 경우):** 도구에서 보고된 처리량(RU/s)은 컬렉션의 프로비전된 처리량과 같거나 많아야 합니다. 그렇지 않은 경우 DegreeOfParallelism을 조금씩 늘리면 제한에 도달하는 데 도움이 될 수 있습니다. 클라이언트 앱의 처리량이 안정화될 경우 같거나 다른 컴퓨터에서 앱의 여러 인스턴스를 시작하면 여러 다른 인스턴스 간에 프로비전된 제한에 도달하는 데 도움이 됩니다. 이 단계에 대해 도움이 필요한 경우 askcosmosdb@microsoft.com에 전자 메일을 보내거나 [Azure Portal](https://portal.azure.com)에서 지원 티켓을 작성하세요.

실행 중인 앱이 있는 경우 다양한 [인덱싱 정책](indexing-policies.md) 및 [일관성 수준](consistency-levels.md)을 시도하면서 처리량 및 대기 시간에 미치는 영향을 이해할 수 있습니다. 소스 코드를 검토하고 자체 테스트 제품군 또는 프로덕션 응용 프로그램에 대해 비슷한 구성을 구현할 수도 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 .NET 콘솔 앱을 사용하여 Cosmos DB로 성능 및 규모 테스트를 수행하는 방법을 살펴보았습니다. Azure Cosmos DB 사용 방법에 대한 자세한 내용은 아래 링크를 참조하세요.

* [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Azure Cosmos DB 성능 향상을 위한 클라이언트 구성 옵션](performance-tips.md)
* [Azure Cosmos DB의 서버 쪽 분할](partition-data.md)


