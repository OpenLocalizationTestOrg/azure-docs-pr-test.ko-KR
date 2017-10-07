---
title: "aaaAzure Cosmos DB 질문과 대답 | Microsoft Docs"
description: "Azure Cosmos DB 세계적으로 분산 된 다중 모델 데이터베이스 서비스에 대 한 질문과 대답 toofrequently를 가져옵니다. 용량, 성능 수준 및 크기 조정에 대해 알아봅니다."
keywords: "데이터베이스 질문, 질문과 대답, Documentdb, Azure, Microsoft Azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Azure Cosmos DB FAQ
## <a name="azure-cosmos-db-fundamentals"></a>Azure DB Cosmos 기본 사항
### <a name="what-is-azure-cosmos-db"></a>Azure Cosmos DB란 무엇인가요?
Azure Cosmos DB는 전역적으로 복제된 다중 모델 데이터베이스 서비스로, Microsoft Azure의 성능과 범위로 지원되는 관리 플랫폼을 통해 스키마 제약이 없는 데이터에 대해 다양한 쿼리를 제공하고, 이 hello 전원 뒷받침 되며 및 Microsoft azure에 도달 하는 관리 되는 플랫폼을 통해 얻습니다 모든. 

Azure Cosmos DB는 웹, 모바일, 게임에 대 한 hello 적합 한 솔루션 및 핵심적인 요소는 고가용성을 예측 가능한 처리량, 짧은 대기 시간, 스키마가 없는 데이터 모델 경우 IoT 응용 프로그램입니다. Azure Cosmos DB는 스키마 유연성과 다양한 인덱싱을 제공하며, 통합된 JavaScript로 다중 문서 트랜잭션도 지원합니다. 

데이터베이스 질문, 응답 및 배포 하 고이 서비스를 사용 하는 지침 참조 hello [Azure Cosmos DB 설명서 페이지](https://azure.microsoft.com/documentation/services/cosmos-db/)합니다.

### <a name="what-happened-toodocumentdb"></a>발생 했습니다 tooDocumentDB 무엇입니까?
DocumentDB API hello Azure Cosmos DB에 대 한 hello 지원 Api와 데이터 모델 중 하나입니다. 또한 Azure Cosmos DB는 Graph API(미리 보기), Table API(미리 보기) 및 MongoDB API를 통해 사용자를 지원합니다. 자세한 내용은 [DocumentDB 고객의 질문](#moving-to-cosmos-db)을 참조하세요.

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Hello Azure 포털에서에서 toomy DocumentDB 계정 가져오기
Hello Azure 포털에서에서 왼쪽 창의 hello hello Azure Cosmos DB 아이콘을 클릭 합니다. DocumentDB 계정을 전에 설치한 경우 Azure Cosmos DB 계정을 없는 변경 tooyour 결제 해야 합니다.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Azure Cosmos DB에 대 한 hello 일반적인 사용 사례는 무엇입니까?
Azure Cosmos DB 새 웹, 모바일, 게임에 대 한 적합 한 선택 이며 여기서 자동 배율, 예측 가능한 성능, 밀리초 응답 시간의 순서 빠르며 스키마 없는 데이터에 대해 기능 tooquery hello IoT 응용 프로그램 중요 합니다. Azure Cosmos DB는 경우가 많으므로 toorapid 개발 및 응용 프로그램 데이터 모델의 hello 연속 반복을 지원 합니다. 사용자 생성 콘텐츠 및 데이터를 관리하는 응용 프로그램은 [Azure Cosmos DB의 일반적인 사용 사례](use-cases.md)입니다. 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Azure Cosmos DB는 어떻게 예측 가능한 성능을 제공하나요?
A [요청 단위](request-units.md) (RU) hello Azure Cosmos DB에서 처리량을 측정 한 것입니다. 1-RU 처리량의 hello는 1KB 문서의 GET toohello 처리량을 해당합니다. Azure Cosmos db에서 읽기, 쓰기, SQL 쿼리 및 저장된 프로시저 실행을 비롯 한 모든 작업 hello 필요한 처리량 toocomplete hello 작업에 따라 결정적 RU 값으로 포함 합니다. CPU, IO 및 메모리와 이 각각이 응용 프로그램 처리량에 미치는 영향을 고려하는 대신 단일 RU 측정값 측면에서 고려할 수 있습니다.

초당 RU 처리량 면에서 프로비전된 처리량으로 각 Azure Cosmos DB 컨테이너를 예약할 수 있습니다. 모든 규모의 응용 프로그램에 대 한 개별 요청 toomeasure RU 값을 벤치 마크 수 있으며 모든 요청에 대해 컨테이너 toohandle hello 총 요청 단위를 프로 비전 할 수 있습니다. 수직 확장 하거나 응용 프로그램 evolve의 hello 요구 사항으로 컨테이너의 처리량을 줄일 수 있습니다. 요청 단위에 대 한 자세한 내용은 및 도움말에 대 한 참조 필요한 컨테이너를 결정 하 [처리 요구 사항을 추정](request-units.md#estimating-throughput-needs) hello 시도 [처리량 계산기](https://www.documentdb.com/capacityplanner)합니다. hello 용어 *컨테이너* 여기 toorefers tooa DocumentDB API 컬렉션, Graph API 그래프, MongoDB API 컬렉션 및 테이블 API 테이블을 참조 합니다. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Azure Cosmos DB에서는 키/값, 열 형식, 문서 및 그래프와 같은 다양한 데이터 모델을 어떻게 지원하나요?

키/값 (table), 열, 형식 및 해당 Azure Cosmos DB 디자인 hello ARS (원소, 레코드 및 순서)으로 인해 기본적으로 지원 되는 모든 모델은 그래프 데이터를 기반 합니다. 원소, 레코드 및 시퀀스 매핑된 쉽고 예상 toovarious 데이터 모델을 수 있습니다. 모델의 하위 집합에 대 한 Api hello 사용할 수 있는 지금 바로 (DocumentDB, MongoDB, 테이블 및 그래프 Api) 되며 미래 hello 다른 특정 tooadditional 데이터 모델에서 사용할 수 있습니다.

Azure Cosmos DB는 스키마 알 수 없는 인덱싱 엔진이 자동으로 스키마 이나 hello 개발자 로부터 보조 인덱스 없이 수집 하는 모든 hello 데이터 인덱싱 가능 합니다. hello 엔진 hello 인덱스 및 쿼리 처리 하위 시스템에서 hello 저장소 레이아웃을 분리 하기 위한 논리적 인덱스 레이아웃 (반전, 열, 트리)의 집합에 의존 합니다. Cosmos DB도 hello 기능 toosupport 유선 프로토콜 및 Api의 집합을 확장할 수 있는 방식으로 개이고에서 변환 효율적으로 toohello 핵심 데이터 모델 (1) 및 hello 논리적 인덱스 레이아웃 (2) 있어서 고유 하 게 여러 데이터 모델을 고유 하 게 지원할 수 .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure Cosmos DB는 HIPAA 규격인가요?
예, Azure Cosmos DB는 HIPAA 규격입니다. HIPAA 공개 및 개별적으로 식별이 가능한 상태 정보 보호에 hello에 대 한 요구 사항을 사용 하 여 설정 합니다. 자세한 내용은 참조 hello [Microsoft 보안 센터](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA)합니다.

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Cosmos DB Azure의 hello 저장소 제한 사항은 무엇입니까?
없는 제한 toohello 총 데이터 양이 컨테이너 Azure Cosmos DB에 저장할 수 있는 방법이 있습니다.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Cosmos DB Azure의 hello 처리량이 제한 사항은 무엇입니까?
다음이 컨테이너는 Azure Cosmos DB에서 지원할 수 있는 처리량 없습니다 제한 toohello 총 용량입니다. 핵심 아이디어 hello 되기 toodistribute 작업 균등 하 게 파티션 키의 충분히 큰 수입니다.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Azure Cosmos DB 비용은 얼마인가요?
자세한 내용은 참조 toohello [가격 정보는 Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/) 페이지. Azure DB Cosmos 사용 요금 hello 각 컨테이너에 대 한 처리량을 프로 비전 하 고 hello 컨테이너, 온라인 상태 였던 hello 컨테이너의 개수 제한은 프로 비전 된 hello 시간 수가에 의해 결정 됩니다. hello 용어 *컨테이너* 여기 toohello DocumentDB API 컬렉션, Graph API 그래프, MongoDB API 컬렉션 및 테이블 API 테이블을 참조 합니다. 

### <a name="is-a-free-account-available"></a>무료 계정을 사용할 수 있나요?
새 tooAzure 인 경우에 등록할 수 있습니다는 [Azure 무료 계정을](https://azure.microsoft.com/free/), 30 일 이내를 제공 하는 및와 신용 tootry 모든 Azure 서비스 hello 합니다. Visual Studio 구독을 보유 하는 경우에 자격이 있으며 [무료 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse 모든 Azure 서비스에 있습니다. 

Hello를 사용할 수도 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toodevelop 및 테스트 응용 프로그램을 로컬로 대 한 무료, Azure 구독을 만들지 않고 합니다. Hello Azure Cosmos DB 에뮬레이터에서에서 응용 프로그램 작동 방식을 만족 스 러 우면 toousing hello 클라우드에서 Azure Cosmos DB 계정을 전환할 수 있습니다.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Azure Cosmos DB 추가 도움말은 어떻게 구할 수 있나요?
모든 도움이 필요 하면 교류할에 toous [스택 오버플로](http://stackoverflow.com/questions/tagged/azure-cosmosdb) 또는 hello [MSDN 포럼](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), 또는 일대일 채팅 hello Azure Cosmos DB 엔지니어링 팀에 너무 메일을 전송 하 여 예약[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Azure Cosmos DB 설정
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Azure Cosmos DB에는 어떻게 등록하나요?
Azure Cosmos DB hello Azure 포털에서에서 제공 됩니다. 먼저 Azure 구독에 등록합니다. 등록 했으면, 후 DocumentDB API를 추가할 수 있습니다, Graph API (미리 보기), 테이블 API (미리 보기) 또는 MongoDB API tooyour Azure 구독 계정.

### <a name="what-is-a-master-key"></a>마스터 키란 무엇인가요?
마스터 키가 보안 토큰 tooaccess 계정에 대 한 모든 리소스입니다. Hello 키와 개인 hello 데이터베이스 계정에 읽기 및 쓰기 액세스 tooall 리소스를 제공 합니다. 마스터 키를 배포할 때 주의하세요. hello 주 마스터 키와 보조 마스터 키 hello에서 사용할 수 있는 **키** hello의 블레이드에서 [Azure 포털][azure-portal]합니다. 키에 대한 자세한 내용은 [액세스 키 보기, 복사 및 다시 생성](manage-account.md#keys)을 참조하세요.

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>PreferredLocations로 설정할 수 있는 hello 지역 이란? 
tooany hello Azure의 hello PreferredLocations 값을 설정할 수 있습니다 영역 Cosmos DB를 사용할 수 있습니다. 사용 가능한 영역 목록은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>가 있는 hello world hello Azure 데이터 센터를 통해 데이터를 분산 때 알고 있어야 합니까? 
Azure Cosmos DB 있으면 모든 Azure 지역에 걸쳐에 지정 된 hello로 [Azure 지역](https://azure.microsoft.com/regions/) 페이지. Hello 핵심 서비스 이기 때문에 모든 새 데이터 센터는 Azure Cosmos DB 현재 상태를 있습니다. 

지역을 설정할 때 Azure Cosmos DB는 국가 및 정부 클라우드를 따른다는 점을 염두에 두어야 합니다. 즉, 국가 지역에 계정을 만든 경우 해당 국가 지역 외부로 복제할 수 없습니다. 마찬가지로 외부 계정에서 다른 국가 위치로 복제할 수 없습니다. 

## <a name="develop-against-hello-documentdb-api"></a>Hello DocumentDB API에 대해 개발

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>DocumentDB API hello에 대 한 개발을 시작 하는 방법
Microsoft DocumentDB API는 hello에서 사용할 수 있는 [Azure 포털][azure-portal]합니다. 먼저 Azure 구독에 등록해야 합니다. Azure 구독에 등록 되 면 DocumentDB API 컨테이너 tooyour Azure 구독을 추가할 수 있습니다. Azure Cosmos DB 계정 추가에 대한 지침은 [Azure Cosmos DB 데이터베이스 계정 만들기](create-documentdb-dotnet.md#create-account)를 참조하세요. DocumentDB 계정을 hello 이전에 설치한 경우 Azure Cosmos DB 계정을 해야 합니다. 

[SDK](documentdb-sdk-dotnet.md) 는 .NET, Python, Node.js, JavaScript 및 Java용으로 제공됩니다. 개발자가 hello 사용할 수도 [RESTful HTTP Api](/rest/api/documentdb/) toointeract 다양 한 플랫폼 및 언어의 Azure Cosmos DB 자원으로 합니다.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>일부 즉시 사용 가능한 샘플 tooget 쉽게 액세스할 수 있습니까?
DocumentDB API hello에 대 한 샘플 [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), 및 [Python](documentdb-python-samples.md) Sdk는 GitHub에서 사용할 수 있습니다.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>DocumentDB API 데이터베이스 지원 스키마 없는 데이터 hello 합니까?
예, hello DocumentDB API에는 스키마 정의 또는 힌트 없이 응용 프로그램 toostore 임의 JSON 문서 수 있습니다. 데이터는 hello Azure Cosmos DB SQL 쿼리 인터페이스를 통해 쿼리에 즉시 사용할 수 있습니다.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>DocumentDB API hello를 ACID 트랜잭션을 지원 합니까?
예, hello DocumentDB API에는 JavaScript 저장 프로시저와 트리거도 표시 하는 문서 간 트랜잭션을 지원 합니다. 트랜잭션은 ACID "전체 또는 nothing," 의미 체계를 사용 하 여 실행 하 고 각 컬렉션 내에서 단일 파티션에 tooa 범위가 지정 되며 다른 동시에 실행 되는 코드 및 사용자 요청에서 격리 합니다. JavaScript 응용 프로그램 코드의 hello 서버 쪽 실행을 통해 예외가 hello 전체 트랜잭션이 롤백됩니다. 트랜잭션에 대한 자세한 내용은 [데이터베이스 프로그램 트랜잭션](programming.md#database-program-transactions)을 참조하세요.

### <a name="what-is-a-collection"></a>컬렉션이란 무엇인가요?
컬렉션은 문서 및 관련 JavaScript 응용 프로그램 논리의 그룹입니다. 컬렉션은 청구 가능 엔터티에 hello [비용](performance-levels.md) 저장소를 사용 하 고 hello 처리량에 따라 결정 됩니다. 하나 이상의 파티션을 또는 서버에 걸쳐 있는 컬렉션과 toohandle 확장할 수 저장소나 처리량 거의 무제한 볼륨입니다.

컬렉션은 hello Azure Cosmos DB에 대 한 청구 엔터티도입니다. 각 컬렉션으로 시간당 청구 됩니다 하 고 hello 프로 비전 된 처리량에 따라 저장소 공간을 사용 합니다. 자세한 내용은 [Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/)을 참조하세요. 

### <a name="how-do-i-create-a-database"></a>데이터베이스를 어떻게 만드나요?
Hello를 사용 하 여 데이터베이스를 만들 수 있습니다 [Azure 포털](https://portal.azure.com)에 설명 된 대로 [컬렉션을 추가할](create-documentdb-dotnet.md#create-collection), hello 중 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md), 또는 hello [RESTApi](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>사용자 및 사용 권한을 어떻게 설정하나요?
Hello 중 하나를 사용 하 여 사용자 및 사용 권한을 만들 수 있습니다 [Cosmos DB API Sdk](documentdb-sdk-dotnet.md) 또는 hello [REST Api](/rest/api/documentdb/)합니다.  

### <a name="does-hello-documentdb-api-support-sql"></a>DocumentDB API hello SQL을 지원 합니까?
hello SQL 쿼리 언어의 SQL에서 지원 되는 hello 쿼리 기능에는 향상 된 하위 집합입니다. hello Azure Cosmos DB SQL 쿼리 언어는 풍부한 계층적 및 관계형 연산자와 JavaScript 기반, 사용자 정의 함수 (Udf)를 통해 확장성을 제공합니다. Hello Azure Cosmos DB 자동 인덱싱 기술을 Cosmos DB Azure의 hello SQL 쿼리 언어에서 사용 되는 레이블이 지정 된 노드와 트리로의 JSON 문서를 모델링 하기 위한 JSON 문법 수 있습니다. SQL 문법을 사용 하는 방법에 대 한 정보를 참조 hello [QueryDocumentDB] [ query] 문서.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Hello DocumentDB API 지원 SQL 집계 함수를 합니까?
hello DocumentDB API는 집계 함수를 통해 모든 규모에 낮은 대기 시간 집계를 지원 `COUNT`, `MIN`, `MAX`, `AVG`, 및 `SUM` hello SQL 문법을 통해 합니다. 자세한 내용은 [집계 함수](documentdb-sql-query.md#Aggregates)를 참조하세요.

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>DocumentDB API hello 동시성을 제공 하는 어떻게 합니까?
hello DocumentDB API HTTP 엔터티 태그 또는 Etag를 통해 낙관적 동시성 제어 (OCC)를 지원합니다. 모든 DocumentDB API 리소스에는 ETag 및 문서 업데이트 될 때마다 hello ETag hello 서버에 설정 합니다. hello ETag 헤더 및 hello 현재 값은 모든 응답 메시지에 포함 됩니다. Etag는 리소스를 업데이트 해야 하는지 여부를 hello If-match 헤더 tooallow hello 서버 toodecide와 사용할 수 있습니다. hello If-match 값은 hello ETag 값 toobe 여부를 검사 합니다. ETag 값 hello hello 서버 ETag 값과 일치 하면 hello 리소스 업데이트 됩니다. Hello 서버 hello ETag가 이제을 사용 하 여 hello 작업을 거부는 "HTTP 412 실패 전제 조건" 응답 코드입니다. 클라이언트 hello 다음 다시 인출 hello 리소스 tooacquire hello 현재 ETag 값 hello 리소스에 대 한 합니다. 또한 Etag는 사용 하 여 hello None-If-match 헤더 toodetermine 필요한 리소스를 다시 가져와 여부.

.net을 사용 하 여 hello toouse 낙관적 동시성 [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) 클래스입니다. .NET 샘플을 보려면 [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) GitHub에 hello DocumentManagement 샘플에 있습니다.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>트랜잭션을 hello DocumentDB API에에서 수행 하려면 어떻게 해야 합니까?
DocumentDB API hello JavaScript 저장 프로시저 및 트리거를 통한 트랜잭션 통합 언어를 지원합니다. 스크립트 내의 모든 데이터베이스 작업은 스냅숏이 격리된 상태에서 실행됩니다. 단일 파티션 컬렉션 인 경우 hello 실행은 toohello 범위가 지정 된 컬렉션입니다. Hello 실행은 hello로 범위가 지정 된 toodocuments hello 컬렉션 분할 된 경우 hello 컬렉션 내에서 동일한 파티션 키 값입니다. Hello 문서 버전 (ETags)에 대 한 스냅숏은 hello hello 트랜잭션 시작 시 수행할 이며 hello 스크립트에 성공한 경우에 커밋됩니다. Hello JavaScript 오류가 throw 되 면 hello 트랜잭션이 롤백됩니다. 자세한 내용은 [Azure Cosmos DB에 대한 서버 쪽 JavaScript 프로그래밍](programming.md)을 참조하세요.

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Cosmos DB에 문서를 어떻게 일괄 삽입할 수 있나요?
다음 두 가지 방법 중 하나로 Azure Cosmos DB에 문서를 대량 삽입할 수 있습니다.

* 에 설명 된 대로 hello 데이터 마이그레이션 도구 [Azure Cosmos DB에 대 한 데이터베이스 마이그레이션 도구](import-data.md)합니다.
* [Azure Cosmos DB에 대한 서버 쪽 JavaScript 프로그래밍](programming.md)에 설명된 대로 저장 프로시저를 사용합니다.

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>리소스 링크 캐싱 hello DocumentDB API 지원 합니까?
예, Azure Cosmos DB는 RESTful 서비스이므로 리소스 링크가 제한되며 캐시될 수 있습니다. DocumentDB API 클라이언트 있는 리소스 형식의 문서 또는 컬렉션에 대해 읽기에 대 한 "None-If-match" 헤더를 지정할 수 있으며 다음 hello 서버 버전이 변경 된 후 해당 로컬 복사본을 업데이트 됩니다.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>DocumentDB API의 로컬 인스턴스를 사용할 수 있나요?
예. hello [Azure Cosmos DB 에뮬레이터](local-emulator.md) hello Cosmos DB 서비스의 충실도 높은 재현 에뮬레이션을 제공 합니다. 기능 동일한 tooAzure Cosmos DB에 만들고 쿼리 JSON 문서에 대 한 지원을 비롯 하 여 프로 비전을 지원 하 고 저장 프로시저와 트리거의 컬렉션을 확장 하 고 실행 합니다. 개발 하 고 및 hello Azure Cosmos DB 에뮬레이터를 사용 하 여 응용 프로그램을 테스트 하 고, 단일 구성을 Azure Cosmos DB에 대 한 toohello 연결 끝점을 변경 하 여 tooAzure 세계적인 규모에 배포할 수 있습니다.

## <a name="develop-against-hello-api-for-mongodb"></a>MongoDB에 대 한 hello API에 대해 개발
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>MongoDB에 대 한 Azure Cosmos DB API hello 이란?
hello MongoDB에 대 한 Azure Cosmos DB API에는 응용 프로그램 tooeasily 가능 하며 기존, 커뮤니티에서 지 원하는 Apache MongoDB Api 및 드라이버를 사용 하 여 hello 네이티브 Azure Cosmos DB 데이터베이스 엔진과 투명 하 게 통신 하는 호환성 계층입니다. 개발자는 기존 MongoDB 도구 체인 및 기술 toobuild 응용 프로그램을 Azure Cosmos DB 활용 하기 위해 이제 사용할 합니다. Hello의 고유한 기능 Azure Cosmos DB 자동 인덱싱을, 백업 유지 관리, 재정적으로 백업 된 서비스 수준 계약 (Sla)을 포함 개발자 합니다.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>MongoDB 데이터베이스에 대 한 API toomy를 연결 하는 방법
MongoDB toohello 스타일러스가 toohead에 대 한 가장 빠른 방법은 tooconnect toohello Azure Cosmos DB API hello [Azure 포털](https://portal.azure.com)합니다. Hello 왼쪽된 탐색 메뉴에서을 클릭 하 고 tooyour 계정 이동 **빠른 시작**합니다. 빠른 시작 hello 가장 좋은 방법은 tooget 코드 조각 tooconnect tooyour 데이터베이스입니다. 

Azure Cosmos DB에는 엄격한 보안 요구 사항과 표준이 적용됩니다. Azure DB Cosmos 계정 인증과 SSL 통해 안전한 통신을 요구, 있는지 toouse TLSv1.2 기울여야 합니다.

자세한 내용은 참조 [tooyour API MongoDB 데이터베이스에 대 한 연결](connect-mongodb-account.md)합니다.

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>MongoDB 데이터베이스용 API에 대한 추가 오류 코드가 있나요?
또한 toohello 일반적인 MongoDB 오류 코드, hello MongoDB API에는 자체 특정 오류 코드:


| 오류               | 코드  | 설명  | 해결 방법  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | 사용 된 요청 단위 hello 총 수 hello 컬렉션에 대 한 hello 프로 비전된 요청 단위 비율을 초과한 및 조절 되었습니다. | Hello 처리량 hello Azure 포털에서에서 hello 컬렉션의 크기 조정 또는 다시 시도 하십시오. |
| ExceededMemoryLimit | 16501 | 다중 테 넌 트 서비스인 hello 작업이 hello 클라이언트의 메모리 할당을 초과 했습니다. | 더 제한적인 쿼리 조건을 통해 hello 작업의 hello 범위를 줄이거나 hello에서 지원에 문의 [Azure 포털](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다. <br><br>예: *&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Hello 테이블 API (미리 보기)를 사용 하 여 개발

### <a name="terms"></a>용어 
hello Azure Cosmos DB: 테이블 API (미리 보기)에서 빌드 2017 발표 테이블 지원에 대 한 Azure Cosmos db toohello 프리미엄 기능을 참조 합니다. 

hello 표준 SDK 테이블인 hello 기존 Azure 저장소 SDK입니다. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Hello 새 테이블 API (미리 보기) 기능을 사용 하려면 어떻게 해야 합니까? 
hello Azure Cosmos DB 테이블 API는 hello에서 사용할 수 있는 [Azure 포털][azure-portal]합니다. 먼저 Azure 구독에 등록해야 합니다. 등록 하 한 후 Azure Cosmos DB 테이블 API 계정 tooyour Azure 구독을 추가할 수 있으며 테이블 tooyour 계정을 추가 합니다. 

Hello 미리 보기 기간 중 때 [Sdk](../cosmos-db/table-sdk-dotnet.md) 는 사용할 수 있으며.NET 시작할 수 있는 hello를 완료 하 여 [테이블 API](../cosmos-db/create-table-dotnet.md) 빠른 시작 문서입니다.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>새 SDK toouse hello 테이블 API (미리 보기)가 필요 합니까? 
예, hello [Windows Azure 저장소 프리미엄 테이블 (미리 보기) SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) NuGet에서 확인할 수 있습니다. 추가 정보는 hello [Azure Cosmos DB 테이블.NET API: 릴리스 정보 및 다운로드](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) 페이지. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Hello SDK 또는 버그에 대 한 피드백을 제공 하는 어떻게 하나요?
Hello 같은 방법으로 다음 중 하나에 사용자 의견을 공유할 수 있습니다.

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [MSDN 포럼](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Hello 연결 문자열 싶습니다 toouse tooconnect toohello 테이블 API (미리 보기) 이란?
hello 연결 문자열은:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Hello Azure 포털의에서 hello 키 페이지에서 연결 문자열 hello를 얻을 수 있습니다. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Hello 새 테이블 API (미리 보기)에서 hello 요청 옵션에 대 한 hello 구성 설정을 재정의 하려면 어떻게 해야 합니까?
구성 설정에 대한 자세한 내용은 [Azure Cosmos DB 기능](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)을 참조하세요. Tooapp.config hello 클라이언트 응용 프로그램의 hello appSettings 섹션에 추가 하 여 hello 설정을 변경할 수 있습니다.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Hello 기존 표준 테이블 SDK를 사용 하는 고객에 대 한 변경 사항이 있습니까?
없음. Hello 기존 표준 테이블 SDK를 사용 하는 기존 또는 새 고객에 대 한 변경이 없습니다. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Hello 테이블 API (검토)로 사용 하기 위해 Azure Cosmos DB에 저장 되어 있는 테이블 데이터를 보려면 어떻게 해야 합니까? 
Hello Azure 포털 toobrowse hello 데이터를 사용할 수 있습니다. 또한 테이블 API (미리 보기) 코드 hello 또는 hello 다음 응답에 언급 된 hello 도구를 사용할 수 있습니다. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>도구를 사용할 수 있는 테이블 API (미리 보기) hello? 
Hello Azure 탐색기 (0.8.9)의 이전 버전을 사용할 수 있습니다.

Hello 유연성 tootake 이전에 지정 된 hello 형식에서 연결 문자열을 지원할 수 있는 도구 hello 새 테이블 API (미리 보기). 테이블 도구 목록이 hello에 제공 [Azure 저장소 클라이언트 도구](../storage/common/storage-explorers.md) 페이지. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell 또는 Azure CLI 작동 hello 새 테이블 API (미리 보기) 하나요?
테이블 API (미리 보기)에 대 한 PowerShell 및 Azure CLI tooadd 지원을 계획입니다. 

### <a name="is-hello-concurrency-on-operations-controlled"></a>Hello 동시성 제어 작업에는?
예, 낙관적 동시성 hello 사용 하 여 hello ETag 메커니즘을 통해 제공 됩니다. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>지원 되는 hello OData 쿼리 모델 엔터티에 대 한? 
예, hello 테이블 API (미리 보기)는 OData 쿼리 및 LINQ 쿼리를 지원합니다. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>에 연결할 수 있습니까 toohello 표준 Azure 테이블 및 hello 새로운 프리미엄 테이블 API (미리 보기)에 병렬 hello 동일한 응용 프로그램? 
예, 각 가리키는 CloudTableClient hello의 두 개별 인스턴스를 만들어 연결할 수 있습니다 tooits hello 연결 문자열을 통해 URI를 소유 합니다.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>기존 Azure 테이블 저장소 응용 프로그램 toothis 새 제품을 마이그레이션하는 방법
tootake 활용 하 여 기존 테이블 저장소 데이터 연락처에서 새 테이블 API 제공 hello [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com)합니다. 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>이 서비스에 대 한 hello 로드맵 란 무엇이 고 다른 표준 테이블 API 기능 때 제공 하 시겠습니까?
Ga에 있습니다. 방향으로 계속 진행 하면서 SAS 토큰, ServiceContext, 통계, 클라이언트 쪽 암호화, 분석 및 기타 기능에 대 한 tooadd 지원 계획 [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)에서 의견을 제공할 수 있습니다. 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>예를 들어 시작 하 여는 경우이 서비스에 대해 수행 하는 hello 저장소 크기의 확장은 어떻게  *n*  g B 데이터 및 데이터의 크기가 계속 커집니다 too1 TB 시간이 지남에 따라? 
Azure Cosmos DB 디자인 된 tooprovide는 hello 수평적 확장 사용을 통해 무제한 저장 합니다. hello 서비스 모니터링 하 고 효과적으로 저장소를 늘릴 수 있습니다. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Hello 테이블 API (미리 보기) 기능을 모니터링 하려면 어떻게 해야 합니까?
Hello 테이블 API (미리 보기)를 사용할 수 있습니다 **메트릭** 창 toomonitor 요청 및 저장소 사용 합니다. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>필요한 hello 처리량을 계산 하는 방법
Hello 용량 평가기 toocalculate hello hello 작업에 대 한 필요한 TableThroughput를 사용할 수 있습니다. 자세한 내용은 [요청 단위 및 데이터 저장소 예측](https://www.documentdb.com/capacityplanner)을 참조하세요. 일반적으로 운영을 위한 hello 번호를 제공를 JSON으로 엔터티를 나타낼 수 있습니다. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>사용할 수 있습니까 hello 새 테이블 (미리 보기) hello 에뮬레이터를 사용 하 여 로컬로 SDK API?
예를 사용할 수 있습니다 사용할 때 로컬 에뮬레이터 hello와 함께 테이블 API (미리 보기) hello hello 새 SDK입니다. toodownload 새 에뮬레이터를 너무 이동[로컬 개발 및 테스트에 사용 하 여 hello Azure Cosmos DB 에뮬레이터](local-emulator.md)합니다. app.config에서 StorageConnectionString 값 hello toobe 항목이 필요합니다.

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>기존 응용 프로그램 hello 테이블 API (미리 보기)로 작동할 수 있습니까? 
hello hello의 노출 영역에는 새 테이블 API (미리 보기) hello Azure 표준 테이블 hello에서 SDK 만들기, 삭제, 업데이트 및 쿼리 작업 hello.NET API에서에서 기존 호환 됩니다. 파티션 키와 행 키 테이블 API (미리 보기) hello 필요 하기 때문에 행 키가 있는지 확인 합니다. Tooadd 자세한 SDK 지원 GA이 서비스 제공의 방향으로 계속 진행 하면서도 계획입니다.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>필요한 toomigrate 내 기존 Azure 테이블 기반 응용 프로그램 toohello toouse hello 테이블 API (미리 보기) 기능 하지 않을 경우 새 SDK?
아니요, 어떤 종류의 중단도 없이 기존 표준 테이블 자산을 만들고 사용할 수 있습니다. 그러나 hello 새 테이블 API (미리 보기)를 사용 하지 않는 경우 hello 자동 인덱스, hello 추가 일관성 옵션 또는 글로벌 배포에서 얻을 수 없는 있습니다. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Hello 데이터의 복제 Azure의 여러 지역에 걸쳐 hello 프리미엄 테이블 API (미리 보기)에 추가 하려면 어떻게 해야 합니까?
Hello Cosmos DB Azure 포털을 사용 하려면 [전역 복제 설정을](tutorial-global-distribution-documentdb.md#portal) 응용 프로그램에 적합 한 tooadd 영역입니다. 전 세계적으로 분산된 응용 프로그램 toodevelop도 응용 프로그램 hello PreferredLocation 정보 집합 toohello 로컬 지역의 짧은 읽기 대기 시간을 제공 하는 데에 추가 해야 합니다. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Hello 계정 hello 프리미엄 테이블 API (미리 보기)에 대 한 hello 주 쓰기 영역을 변경 하려면 어떻게 해야 합니까?
Hello Azure Cosmos DB 전역 복제 포털 창 tooadd 영역을 사용할 수 있으며 다음 toohello 필요한 영역 장애 조치할 수 있습니다. 지침은 [다중 지역 Azure Cosmos DB 계정을 사용하여 개발](regional-failover.md)을 참조하세요. 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>데이터 분산 시 대기 시간을 단축하려면 기본 읽기 하위 지역을 어떻게 구성해야 하나요? 
toohelp hello 로컬 위치에서 읽을 hello PreferredLocation 키를 사용 하 여 hello app.config 파일에 있습니다. 기존 응용 프로그램에 대 한 테이블 API (미리 보기) hello LocationMode 설정 된 경우 오류를 throw 합니다. Hello 프리미엄 테이블 API (미리 보기) hello app.config 파일에서이 정보를 선택 하기 때문에 해당 코드를 제거 합니다. 자세한 내용은 [Azure Cosmos DB 기능](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)을 참조하세요.

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Hello 테이블 API (미리 보기)의 일관성 수준에 대 한 생각 하는 방법 
Azure Cosmos DB는 일관성, 가용성 및 대기 시간 간을 매우 논리적으로 절충합니다. Azure Cosmos DB hello 테이블 수준에서 hello 오른쪽 일관성 모델을 선택 하 고 hello 데이터를 쿼리 하는 동안 개별 요청을 만들 수 있도록 tooTable API (미리 보기) 개발자에 게 일관성 수준 5 개를 제공 합니다. 클라이언트가 연결되면 일관성 수준을 지정할 수 있습니다. Hello hello TableConsistencyLevel 키 값에 대 한 hello app.config 설정을 통해 hello 수준을 변경할 수 있습니다. 

hello 테이블 API (미리 보기) 대기 시간이 짧은 읽고 "읽을 직접 쓰기" hello 기본값으로 세션 일관성을 제공 합니다. 자세한 내용은 [ 일관성 수준](consistency-levels.md)을 참조하세요. 

기본적으로 Azure 테이블 저장소 영역 내에서 강력한 일관성 및 hello 보조 위치에 차례로 Eventual 일관성을 제공합니다. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Azure Cosmos DB는 표준 테이블보다 더 많은 일관성 수준을 제공하나요?
예, toobenefit hello에서 Azure Cosmos DB의 특성을 배포 하는 방법에 대 한 정보를 참조 [일관성 수준](consistency-levels.md)합니다. Hello 일관성 수준에 대 한 보장을 제공 하기 때문에 신뢰도는 사용할 수 있습니다. 자세한 내용은 [Azure Cosmos DB 기능](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)을 참조하세요.

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>글로벌 배포를 사용 하는 경우 tooreplicate hello 데이터 기간 시간이 걸리나요?
म hello 영속적 영역의 데이터 hello 로컬 커밋을 몇 시간 (밀리초)에 즉시 hello 데이터 tooother 영역. 이 복제만 hello 데이터 센터의 hello 왕복 시간 (RTT)에 종속 됩니다. Cosmos DB Azure의 hello 글로벌 메일 기능에 대 한 더 toolearn 참조 [Azure Cosmos DB: Azure에서 세계적으로 분산 된 데이터베이스 서비스](distribute-data-globally.md)합니다.

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Hello 읽기 요청 일관성 수준이 변경할 수 있습니까?
Azure Cosmos DB와 함께 hello 테이블) (on hello 일관성 수준이 hello 컨테이너 수준에서 설정할 수 있습니다. Hello SDK를 사용 하 여 TableConsistencyLevel 키 hello app.config 파일에 대 한 hello 값을 제공 하 여 hello 수준을 변경할 수 있습니다. hello 가능한 값은: Strong, Bounded Staleness, 세션, 일관 된 접두사 및 차례로 Eventual입니다. 자세한 내용은 [Azure Cosmos DB의 조정 가능한 데이터 일관성 수준](consistency-levels.md)을 참조하세요. hello 주요 개념은 없습니다에 설정 하는 hello 요청 일관성 수준 hello 테이블에 대 한 hello 설정 보다 더입니다. 예를 들어 강력한에 차례로 Eventual hello 테이블에 대 한 hello 일관성 수준 및 hello 요청 일관성 수준을 설정할 수 없습니다. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>어떻게 hello 프리미엄 테이블 API (미리 보기) 계정 처리 장애 조치 지역 작동이 중지 된 경우? 
hello 프리미엄 테이블 API (미리 보기) Cosmos DB Azure의 hello 세계적으로 분산 된 플랫폼에서 차용 합니다. 응용 프로그램 데이터 센터 작동 중단을 허용할 수 있는 tooensure hello Cosmos DB Azure 포털에서 hello 계정에 대 한 더 많은 영역을 하나 이상 사용 하도록 설정 [다중 지역 Azure Cosmos DB 계정을 사용 하 여 개발](regional-failover.md)합니다. Hello 포털을 사용 하 여 hello 영역의 hello 우선 순위를 설정할 수 있습니다 [다중 지역 Azure Cosmos DB 계정을 사용 하 여 개발](regional-failover.md)합니다. 

여기서 장애 조치 우선 순위를 제공 하는 tooby 장애 조치할 수 것을 제어 하 고 hello 계정에 대해 원하는 만큼 영역을 추가할 수 있습니다. 물론 toouse hello 데이터베이스 해야 응용 프로그램 tooprovide 너무 합니다. 이렇게 하면 고객에게 가동 중지 시간이 발생하지 않습니다. hello 클라이언트 SDK은 자동으로 이동 합니다. 즉, hello 영역 다운 되어 자동으로 장애 조치 toohello 새 영역을 검색할 수 있습니다.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>백업에 사용 하도록 설정 하는 hello 프리미엄 테이블 API (미리 보기)?
예, hello 프리미엄 테이블 API (미리 보기)에서 차용 백업에 대 한 Azure Cosmos DB의 hello 플랫폼입니다. 백업은 자동으로 수행됩니다. 자세한 내용은 [Azure Cosmos DB로 자동 온라인 백업 및 복원](online-backup-and-restore.md)을 참조하세요.

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hello 테이블 API (미리 보기)는 기본적으로 엔터티의 모든 특성 인덱스?
예, 기본적으로 엔터티의 모든 특성이 인덱싱됩니다. 자세한 내용은 [Azure Cosmos DB: 인덱싱 정책](indexing-policies.md)을 참조하세요. 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>이 의미 있지 않음 toocreate 여러 인덱스 toosatisfy hello 쿼리? 
예, Azure Cosmos DB에서는 스키마 정의 없이 모든 특성에 대한 자동 인덱싱을 제공합니다. 이 자동화 개발자 toofocus hello 응용 프로그램 대신 인덱스 생성 및 관리를 해제합니다. 자세한 내용은 [Azure Cosmos DB: 인덱싱 정책](indexing-policies.md)을 참조하세요.

### <a name="can-i-change-hello-indexing-policy"></a>Hello 인덱싱 정책을 변경할 수 있나요?
예, hello 인덱스 정의 제공 하 여 hello 인덱싱 정책을 변경할 수 있습니다. 자세한 내용은 [Azure Cosmos DB 기능](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)을 참조하세요. Tooproperly 필요한 인코딩 및 이스케이프 hello 설정 합니다. 

Json 형식의 hello app.config 파일에 문자열:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>플랫폼으로 서 azure Cosmos DB 정렬, 집계, 계층 및 기타 기능 등의 기능이 toohave 많은 것 같습니다. 에서는 이러한 기능 toohello 테이블 API을 추가할 수 있습니까? 
미리 보기에서 hello 테이블 API 제공 hello 같은 Azure 테이블 저장소와 기능을 쿼리 합니다. 또한 Azure Cosmos DB는 정렬, 집계, 지리 공간적 쿼리, 계층 구조 및 다양한 기본 제공 함수도 지원합니다. 에서는 이후 서비스 업데이트에 hello 테이블 API에에서 추가 된 기능을 제공 합니다. 자세한 내용은 [Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리](../documentdb/documentdb-sql-query.md)를 참조하세요.
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Hello 테이블 API (미리 보기)에 대 한 TableThroughput을 때 변경 해야 합니까?
Hello 다음 조건 중 하나에 적용 되는 시간 TableThroughput를 변경 해야 합니다.
* 추출, 변환 및 데이터를 로드 (ETL)를 수행 하는 짧은 시간 안에 tooupload 많은 데이터를 원하는 / 합니다. 
* 더 많은 처리량 hello 백 엔드에 hello 컨테이너에서 필요합니다. 예를 들어 hello 프로 비전 된 처리량 보다 더 사용 하는 hello 처리량은 및 제한에 이르기는 하면 참조 합니다. 자세한 내용은 [Azure Cosmos DB 컨테이너에 대한 처리량 설정](set-throughput.md)을 참조하세요.

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>확장 하거나 테이블 API (미리 보기) 테이블의 hello 처리량을 줄일 수 있습니까? 
예, hello Cosmos DB Azure 포털의 배율 창 tooscale hello 처리량을 사용할 수 있습니다. 자세한 내용은 [처리량 설정](set-throughput.md)을 참조하세요.

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>새로 프로비전된 테이블에 대해 기본 TableThroughput이 설정되나요?
예, app.config 통해 TableThroughput hello를 재정의 하지 않으면 Azure Cosmos DB에서 미리 생성된 된 컨테이너를 사용 하지 마십시오 하는 경우 hello 서비스 400의 처리량으로 테이블을 만듭니다.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>이 가격 hello 표준 테이블 API의 기존 고객에 대 한 변경 사항을 있나요?
없음. 기존 표준 Table API 고객에 대한 가격에는 변동 사항이 없습니다. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Hello 테이블 API (미리 보기)에 대 한 hello 가격을 계산 하는 방법 
hello 가격 hello TableThroughput 할당에 따라 달라 집니다. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Hello의 테이블에 있는 테이블 API (미리 보기)를 제공 하는 조정을 처리 하는 방법 
Hello 요청 속도 hello 기본 컨테이너에 대 한 hello 프로 비전 된 처리량의 hello 용량을 초과 하면 오류를 얻게 됩니다 및 hello SDK hello 재시도 정책을 적용 하 여 hello 호출을 다시 시도 됩니다.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>PartitionKey 및 RowKey tootake 활용 Cosmos DB Azure의 hello 프리미엄 테이블 API (미리 보기) 기능 외에도 처리량 toochoose 필요한 이유는 무엇입니까?
Azure Cosmos DB hello app.config 파일에서 제공 하지 않을 경우 컨테이너에 대해 기본 처리량을 설정 합니다. 

Azure Cosmos DB는 작업에 대한 상한을 사용하여 성능 및 대기 시간을 보장합니다. 이 수준의 보증 경우가 hello 엔진 hello 테 넌 트의 작업에 거 버 넌 스를 적용할 수 있습니다. 얻게 hello hello 플랫폼이이 용량을 예약 하 고 작업 성공을 보장 하기 때문에 처리량 및 대기 시간을 보장 하도록 TableThroughput를 설정 합니다. 

처리량 사양 hello를 사용 하 여 탄력적으로 응용 프로그램의 hello 계절성에서 toobenefit 변경, hello 처리량 요구를 충족 하 수 비용을 절감 합니다.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Toostore hello 데이터만 비용을 지불 하 고 거의 쿼리 때문에 azure 저장소 SDK를 부담이 해제 되었습니다. 새 Azure Cosmos DB 제공 hello 단일 거래를 수행 하거나 아무 것도 저장 하지 I 하는 경우에 me 충전 toobe 것 같습니다. 설명해 주실 수 있나요?

Azure Cosmos DB는 디자인 된 toobe 가용성, 대기 시간 및 처리량에 대 한 보장 세계적으로 분산 된 SLA 기반 시스템입니다. Azure Cosmos DB에서 처리량을 예약 하면 보장 됩니다, 다른 시스템의 처리량 hello와 달리. Azure Cosmos DB는 보조 인덱스 및 글로벌 배포와 같이 고객이 요청할 수 있는 추가 기능을 제공합니다. Hello 미리 보기 기간 중 처리량 액세스에 최적화 된 모델을 제공 하 고 결국 계획 저장소 액세스에 최적화 된 모델 toomeet tooprovide 고객의 요구 합니다. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Table Storage에 데이터를 수집할 때 파티션이 가득 찼음을 나타내는 "할당량 가득 참" 알림을 받은 적이 없는데, 테이블 API (미리 보기) hello로 않습니다 메시지가이 나타납니다. 이 제공는 me 제한 되 고 toochange me를 강제 적용 하면 기존 응용 프로그램 무엇입니까?

Azure Cosmos DB는 SLA 기반 시스템으로, 대기 시간, 처리량, 가용성 및 일관성을 보장할 뿐만 아니라 무제한 확장을 제공합니다. 최고의 성능 보장 tooensure 데이터 크기 및 인덱스 관리 및 확장할 있는지 확인 합니다. hello 10GB hello 수의 엔터티 또는 파티션 키에 따라 항목 제한은 tooensure 뛰어난 조회 및 쿼리 성능을 제공 합니다. 응용 프로그램이 Azure 저장소에도 잘 확장할 수 있는 tooensure, 좋습니다 있습니다 *하지* 한 파티션에 있는 모든 정보를 저장 하 고 쿼리 하는 것으로 핫 파티션을 만듭니다. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>PartitionKey 및 RowKey와 계속 필요 하므로 새 테이블 API (미리 보기) hello? 
예. Hello 테이블 API (미리 보기)의 노출 영역 hello hello 테이블 저장소 SDK의 유사한 toothat 이기 때문에 hello 파티션 키는 효율적인 방법을 toodistribute hello 데이터를 제공 합니다. hello 행 키는 해당 파티션 내에서 고유 합니다. 와 같이 null 일 수 없습니다 및 행 키 요구 toobe 있는 hello 표준 SDK hello 합니다. RowKey hello 길이 255 바이트가 고 PartitionKey의 hello 길이 100 바이트 (곧 toobe 증가 too1 KB)입니다. 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Hello 테이블 API (미리 보기)에 대 한 hello 오류 메시지는 무엇입니까?
이 미리 보기 hello 표준 테이블과 호환 이기 때문에 hello 오류 대부분 toohello 오류 hello 표준 테이블에서 매핑됩니다. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>이유 않는 가져오기 제한 되는 테이블 중 한 번에 하나씩 테이블 API (미리 보기) hello toocreate 많은 하려고 하면
Azure Cosmos DB는 SLA 기반 시스템으로, 대기 시간, 처리량, 가용성 및 일관성을 보장하며, 프로 비전 된 시스템 이기 때문에 리소스 tooguarantee 이러한 요구 사항을 보유 합니다. 테이블 만들기의 hello 빠른 속도로 감지 되 고 제한 합니다. 조회 테이블 만들기의 hello 속도로 분 당 5 보다 tooless 절감 하는 것이 좋습니다. 해당 hello 테이블 API (미리 보기)는 프로 비전 된 시스템 기억 합니다. hello 순간 프로 비전 할에 대 한 toopay 시작 됩니다. 

## <a name="develop-against-hello-graph-api-preview"></a>Hello Graph API (미리 보기)에 대해 개발
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Graph API (미리 보기) tooAzure Cosmos DB의 hello 기능을 적용할 수 있는 방법
Graph API (미리 보기)는 확장 라이브러리 tooapply hello 기능을 사용할 수 있습니다. 이 라이브러리를 Microsoft Azure Graph라고 하며 NuGet에서 사용할 수 있습니다. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Hello Gremlin 그래프 탐색 언어를 지 원하는 것 같습니다. 계획 입니까 tooadd 자세한 형태의 쿼리?
예, tooadd 다른 메커니즘 이후 hello에서 쿼리에 대 한 계획입니다. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Hello 새 Graph API (미리 보기) 기능을 사용 하려면 어떻게 해야 합니까? 
tooget 시작 됨, 완료 hello [Graph API](../cosmos-db/create-graph-dotnet.md) 빠른 시작 문서입니다.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>DocumentDB 고객의 질문
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Cosmos DB tooAzure 이유 이동 하 시겠습니까? 

Azure Cosmos DB은 hello 전 세계적으로 분산된를 규모에 클라우드 데이터베이스의 다음 큰 제품입니다. DocumentDB 고객으로 서 해야 액세스 toohello 혁신적인 시스템 및 Azure Cosmos DB에서 제공 하는 기능입니다.

Azure Cosmos DB "프로젝트 Florence" 2010 tooaddress hello 불만 사항에서 Microsoft 내부 대규모 응용 프로그램을 빌드하는 개발자가 직면로 시작 합니다. hello 챌린지 전 세계적으로 분산된 응용 프로그램 구축 되지 않으므로 고유 tooMicrosoft 변경이 기술의 hello 1 세대 tooAzure 개발자 2015에서에서 사용할 수 있는 Azure DocumentDB의 hello 형태로. 

그 이후로, 새로운 기능이 추가되었으며 중요한 새 기능이 도입되었습니다. Azure Cosmos DB hello 결과입니다. 이 릴리스에서는 DocumentDB 고객(데이터 포함)이 자동으로 그리고 원활하게 Azure Cosmos DB 고객이 됩니다. 이러한 기능은 hello 핵심 데이터베이스 엔진으로 글로벌 메일, 탄력적 확장성 및 업계를 주도하 고 포괄적인 Sla hello 영역의 됩니다. 특히, 모든 인기 있는 데이터 모델, 형식 시스템 및 Azure Cosmos DB의 Api toohello 기본 데이터 모델 hello Azure Cosmos DB 데이터베이스 엔진 tooefficiently 맵 발전 했습니다 했습니다. 

hello이 작업의 현재 개발자 연결 요청은 hello 새로운 지원에 대 한 [Gremlin](../cosmos-db/graph-introduction.md) 및 [테이블 저장소 Api](../cosmos-db/table-introduction.md)합니다. 및 정당한 hello 시작입니다. 계획 tooadd 다른 인기 Api 및 최신 데이터 모델 시간 성능 및 저장소 위치 세계적인 규모의 더 많은 고급 기능에 따라입니다. 

해당 hello DocumentDB 아웃 중요 toopoint는 [SQL 언어](../documentdb/documentdb-sql-query.md) 는 결코 hello 중 하나만 많은 Api 해당 hello 기본 Azure Cosmos DB 지원할 수 있습니다. 을 Azure Cosmos DB와 같은 완전히 관리 되는 서비스를 사용 하는 개발자에 대 한 hello 인터페이스 toohello 서비스는 hello hello 서비스에 의해 노출 되는 Api입니다. 기존 DocumentDB 고객에 대해 실제로 변경되는 사항은 아무 것도 없습니다. Azure Cosmos DB에서 동일한 SQL 해당 DocumentDB API에서 제공 하는 hello 정확 하 게 얻을 수 있습니다. 및 지금 (및 이후 hello)를 이전에 액세스할 수 없는 다른 기능에 액세스할 수 있습니다 

다른 징후 지속적인된 작업의 처리량 및 저장소의 확장성을 전역 및 탄력적인 확장 hello foundation입니다. 개선 되었습니다 몇 가지 근본적인 toohello 글로벌 메일 하위 시스템입니다. Hello 등의 많은 개발자 연결 기능이 것 hello 일관 된 접두사 일관성 모델을 총 5 개의 잘 정의 된 일관성 모델. 기술이 발전하면서 더 많은 흥미로운 기능을 출시할 예정입니다. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>수행할 작업 내 DocumentDB 리소스에 Azure Cosmos DB toorun를 계속 toodo tooensure 필요 합니까?

필요한 toomake 변경 없이 전혀 합니다. DocumentDB 리소스는 이제 Azure Cosmos DB 리소스 및이 이동이 발생 했을 때 hello 서비스의 중단 없이 했습니다.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>변경 내용을 수행할 toomake Azure Cosmos DB와 함께 내 앱 toowork 필요 합니까?

변경 내용을 toomake 없습니다 있습니다. 클래스, 네임스페이스 및 NuGet 패키지 이름은 변경되지 않습니다. 늘 그렇듯이 Sdk toodate tootake 활용 hello 최신 기능 및 향상 된 기능을 유지 하는 것이 좋습니다. 

### <a name="whats-changed-in-hello-azure-portal"></a>Hello Azure 포털에서에서 변경 된 기능

DocumentDB는 더 이상 Azure 서비스로 hello 포털에 나타납니다. 그 자리에 hello 다음 이미지에에서 표시 된 것과 같이 새 Azure Cosmos DB 아이콘이입니다. 모든 컬렉션은 이전과 마찬가지로 사용할 수 있으며 처리량을 조정하고 일관성 수준을 변경하며 SLA를 모니터링할 수 있습니다. 데이터 탐색기 (미리 보기)의 hello 기능이 향상 되었습니다. 있습니다 수 이제 보기 및 문서를 편집, 만들기 및 쿼리를 실행 하면 및 작업 저장된 프로시저, 트리거 및 UDF 한 페이지에서 hello 다음 이미지에에서 나와 있는 것 처럼: 

![hello Azure Cosmos DB 컬렉션 블레이드](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>변경 내용을 toopricing 있습니까?

아니요, Azure Cosmos db 앱이 실행의 hello 비용 hello 전과 동일 동일 합니다.

### <a name="are-there-changes-toohello-slas"></a>사항이 변경 toohello Sla 있습니까?

아니요, 가용성에 대 한 Sla를 hello, 일관성, 대기 시간 및 처리량은 변경 되지 않습니다 및 hello 포털에 표시 됩니다. 자세한 내용은 [Azure Cosmos DB에 대한 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/)를 참조하세요.
   
![샘플 데이터를 사용한 Todo 앱](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
