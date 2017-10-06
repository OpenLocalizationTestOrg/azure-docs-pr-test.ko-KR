---
title: 'Azure Cosmos DB: DocumentDB API | Microsoft Docs'
description: "SQL 및 JavaScript를 사용 하 여 짧은 대기 시간으로 Azure Cosmos DB toostore 및 쿼리 엄청난 양의 JSON 문서를 사용 하는 방법을 알아봅니다."
keywords: "json 데이터베이스, 문서 데이터베이스"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Cosmos DB 소개 tooAzure: DocumentDB API

[Azure Cosmos DB](introduction.md)는 업무에 중요한 응용 프로그램에 대한 Microsoft의 전역 분산 다중 모델 데이터베이스 서비스입니다. Azure Cosmos DB에는 [턴키 글로벌 메일](distribute-data-globally.md), [처리량 및 저장소의 탄력적인 크기 조정을](partition-data.md) hello 99 번째 백분위 수 전 세계, 자리 밀리초 대기 [5 개 잘 정의 된 일관성 수준이](consistency-levels.md), 모두 만족할된 높은 가용성을 보장할 수 [업계를 주도하 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)합니다. Azure Cosmos DB [데이터를 자동으로 인덱싱됩니다](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal 스미카 및 인덱스 관리를 요구 하지 않고 있습니다. 또한 다중 모델 방식이며, 문서, 키-값, 그래프 및 열 형식 데이터 모델을 지원합니다. 

![Azure DocumentDB API](./media/documentdb-introduction/cosmosdb-documentdb.png) 

DocumentDB API hello로 Azure Cosmos DB 제공 rich 및 친숙 한 [SQL 쿼리 기능](documentdb-sql-query.md) 스키마 없는 JSON 데이터에 대해 일치 하는 낮은 대기 시간이 있습니다. 이 문서에서는 hello Azure Cosmos DB DocumentDB API 및 JSON 데이터의 toostore 대규모 볼륨을 사용, 대기 시간 (밀리초)의 순서 내에서를 쿼리 하는 방법을 hello 스키마에 따라 쉽게 발전할 개요를 제공 합니다. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Azure Cosmos DB는 어떤 기능 및 주요 기능을 제공하나요?
Hello DocumentDB API를 통해 azure Cosmos DB hello를 주요 기능 및 혜택을 제공 합니다.

* **탄력적으로 확장 가능한 처리량 및 저장소:** 쉽게 확장 하거나 JSON 데이터베이스 toomeet 아래로 응용 프로그램을 확장 해야 합니다. 데이터는 예측 가능한 낮은 대기 시간을 위해 SSD(반도체 드라이브)에 저장됩니다. Azure Cosmos DB toovirtually 확장할 수 있는 컬렉션 호출 된 JSON 데이터를 저장할 컨테이너를 지원 프로 비전 된 처리량 및 무제한 저장소 크기입니다. 응용 프로그램 증가에 따라 탄력적으로 Azure Cosmos DB를 확장하고 원활하게 예측 가능한 성능을 얻을 수 있습니다. 


* **다중 지역 복제:** Azure Cosmos DB toodevelop 응용 프로그램에서 제공 하는 동안 전역 액세스 toodata를 필요로 하는 사용 하면 Azure Cosmos DB 계정과 관련 한 사용자 데이터 tooall 영역을 투명 하 게 복제 일관성, 가용성 및 해당 보장 모두와 함께 성능 간 균형입니다. Azure Cosmos DB hello 전세계 멀티 호 밍 Api hello 기능 tooelastically 배율 처리량 및 저장소 지역 투명 한 장애 조치를 제공합니다. [Azure Cosmos DB로 데이터를 글로벌 배포](distribute-data-globally.md)에서 자세히 알아봅니다.

* **익숙한 SQL 구문을 사용한 임시 쿼리:** 다른 형식의 JSON 문서를 저장하고 익숙한 SQL 구문을 통해 해당 문서를 쿼리합니다. Azure Cosmos DB는 무료 높은 동시 잠금을 사용 하 여, 로그 인덱싱 기술을 tooautomatically 인덱스를 모든 문서 콘텐츠 구조입니다. 이 통해 hello 필요 toospecify 스키마 힌트, 보조 인덱스 또는 뷰 없이 다양 한 실시간으로 쿼리 합니다. [Azure Cosmos DB 쿼리](documentdb-sql-query.md)에서 자세히 알아보세요. 
* **JavaScript hello 데이터베이스 내에 실행:** 저장된 프로시저, 트리거 및 표준 JavaScript를 사용 하 여 사용자 정의 함수 (Udf)으로 응용 프로그램 논리를 표현 합니다. 따라서 응용 프로그램 논리 toooperate 데이터에 대해 hello 응용 프로그램 및 hello 데이터베이스 스키마 사이 불일치가 hello에 대 한 걱정 하지 않고 있습니다. DocumentDB API hello hello 데이터베이스 엔진 내에서 직접 JavaScript 응용 프로그램 논리의 전체 트랜잭션 실행을 제공합니다. JavaScript의 hello 긴밀 한 통합에는 격리 된 트랜잭션으로 삽입, 바꾸기, 삭제 및 JavaScript 프로그램 내에서 선택 작업의 hello 실행할을 수 있습니다. [DocumentDB 서버 쪽 프로그래밍](programming.md)에서 자세히 알아보세요.

* **튜닝할 수 있는 일관성 수준:** 5에서 Select 일관성 수준 tooachieve 일관성과 성능 간에 최적의 균형을 잘 정의 합니다. 쿼리 및 읽기 작업에 대해 Azure Cosmos DB는 강력, 제한된 부실, 세션, 일관된 접두사, 최종의 5가지 일관성 수준을 제공합니다. 이러한 세부적인, 잘 정의 된 일관성 수준 toomake 사운드 간의 장단점 일관성, 가용성 및 대기 시간을 허용 합니다. 자세한 내용을 알아보세요 [toomaximize 가용성 및 성능 수준 일관성을 사용 하 여](consistency-levels.md)합니다.

* **완전히 관리:** hello 필요 toomanage 데이터베이스 및 컴퓨터 리소스를 제거 합니다. 완전히 관리 되는 Microsoft Azure 서비스와 toomanage 가상 컴퓨터를 필요 하지 않습니다, 그리고 배포 및 소프트웨어 구성, 배율, 관리 또는 복잡 한 데이터 계층 업그레이드를 처리 합니다. 모든 데이터베이스가 자동으로 백업되고 지역적 실패로부터 보호됩니다. 쉽게 Azure Cosmos DB 계정을 추가 하 고 운영 하 고 데이터베이스를 관리 하는 대신 응용 프로그램에 toofocus 허용, 필요에 따라 용량을 프로 비전 수 있습니다. 

* **의도적인 개방성:** 기존 기술과 도구를 사용하여 신속하게 시작합니다. DocumentDB API는 간단 하 고 편리한, 해야 tooadopt 새로운 도구 되거나 않는 toocustom 확장 tooJSON 또는 JavaScript 준수 hello에 대 한 프로그래밍입니다. 모든 CRUD, 쿼리 및 간단한 RESTful HTTP 인터페이스를 통해 처리 되는 JavaScript를 포함 하 여 hello 데이터베이스 기능에 액세스할 수 있습니다. hello DocumentDB API는 높은 값을 기반으로 데이터베이스 기능을 제공 하는 동안 기존 형식, 언어 및 표준을 포함 합니다.

* **자동 인덱싱을:** 기본적으로 Azure Cosmos DB 자동으로 hello 데이터베이스에서 모든 hello 문서 인덱스 예상 되거나 않는 스키마 또는 보조 인덱스의 만들기 필요 합니다. 원하지 않습니까 tooindex 모든? 걱정하지 마세요. [JSON 파일에서 경로를 옵트아웃](indexing-policies.md)할 수 있습니다.

* **변경 피드 지원:** 변경 피드는 수정 된 hello 순서로 프로그램 Azure Cosmos DB 컬렉션 내에서 문서 정렬 된 목록을 제공 합니다. 이 피드 수정 toodata 주문 tooreplicate 데이터에서에 대 한 사용된 toolisten 수, API 호출을 트리거할 하거나 업데이트에 스트림 처리를 수행할 수 있습니다. 변경 피드는 자동으로 사용 하도록 설정 하 고 쉬운 toouse: [피드 변경에 대해 자세히 알아보려면](https://docs.microsoft.com/azure/cosmos-db/change-feed)합니다. 

## <a name="data-management"></a>Hello DocumentDB API를 사용 하 여 데이터는 어떻게 관리 해야 할까요?
hello DocumentDB API는 잘 정의 된 데이터베이스 리소스를 통해 JSON 데이터를 관리 하는 데 도움이 됩니다. 이러한 리소스는 고가용성을 위해 복제되며 논리적 URI로 고유한 주소 지정이 가능합니다. hello DocumentDB API는 단순한 HTTP 기반 RESTful 프로그래밍 모델에 대 한 모든 리소스를 제공 합니다. 


hello Azure Cosmos DB 데이터베이스 계정은 tooAzure Cosmos DB에 액세스할 수 있게 해 주는 고유한 네임 스페이스입니다. Azure 구독을 사용 하면 데이터베이스 계정을 만들 수 있습니다, 전에 있어야 tooa 다양 한 Azure 서비스에 액세스 합니다. 

Azure Cosmos DB 내의 모든 리소스는 JSON 문서로 모델링되고 저장됩니다. 리소스는 메타데이터가 포함된 JSON 문서인 항목과 항목 컬렉션인 피드로 관리됩니다. 항목 집합은 해당 피드 내에 포함됩니다.

아래 hello 이미지 hello Azure Cosmos DB 리소스 간의 hello 관계를 보여 줍니다.

![hello Azure Cosmos DB에서 리소스 간의 계층 관계][1] 

데이터베이스 계정은 각각 여러 컬렉션을 포함하는 데이터베이스 집합으로 구성되고, 각 컬렉션에는 저장 프로시저, 트리거, UDF, 문서 및 관련 첨부 파일이 포함될 수 있습니다. 데이터베이스 연관 된 사용 권한 tooaccess의 집합을 가진 사용자가 다양 한 다른 컬렉션, 저장된 프로시저, 트리거, Udf, 문서 또는 첨부 파일입니다. 데이터베이스, 사용자, 사용 권한 및 컬렉션은 잘 알려진 스키마가 있는 시스템 정의 리소스인 반면 문서, 저장 프로시저, 트리거, UDF 및 첨부 파일에는 임의의 사용자 정의 JSON 콘텐츠가 포함됩니다.  

> [!NOTE]
> 도구 중 하나를 사용 하 여 hello Azure DocumentDB 또는 tooprovision, 모니터링 및 계정 hello Azure 리소스 관리 REST API를 통해 만든 관리 hello DocumentDB API를 이전에 Azure DocumentDB 서비스 hello로 사용할 수 있으므로 계속할 수 있습니다 또는 Azure Cosmos DB 리소스 이름입니다. म hello 이름 같은 의미로 참조할 때 사용할 toohello Azure DocumentDB Api입니다. 

## <a name="develop"></a>Hello DocumentDB API를 사용 하 여 앱을 개발할 수는 방법

Azure Cosmos DB hello HTTP/HTTPS 요청을 만들 수는 모든 언어에서 호출 될 수 있는 REST Api를 통해 리소스를 노출 합니다. 또한 hello DocumentDB API에 대 한 몇 가지 인기 있는 언어에 대 한 프로그래밍 라이브러리를 제공합니다. hello 클라이언트 라이브러리 API hello 주소 캐싱, 예외 관리, 자동 다시 시도 및 등과 같은 세부 정보를 처리 하 여 작업의 여러 측면을 간소화 합니다. 라이브러리는 hello에 대 한 현재 사용할 수 있는 언어 및 플랫폼에 따라:  

| 다운로드 | 설명서 |
| --- | --- |
| [.NET SDK](http://go.microsoft.com/fwlink/?LinkID=402989) |[.NET 라이브러리](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Node.js SDK](http://go.microsoft.com/fwlink/?LinkID=402990) |[Node.js 라이브러리](http://azure.github.io/azure-documentdb-node/) |
| [Java SDK](http://go.microsoft.com/fwlink/?LinkID=402380) |[Java 라이브러리](/java/api/com.microsoft.azure.documentdb) |
| [JavaScript SDK](http://go.microsoft.com/fwlink/?LinkID=402991) |[JavaScript 라이브러리](http://azure.github.io/azure-documentdb-js/) |
| 해당 없음 |[서버 쪽 JavaScript SDK](http://azure.github.io/azure-documentdb-js-server/) |
| [Python SDK](https://pypi.python.org/pypi/pydocumentdb) |[Python 라이브러리](http://azure.github.io/azure-documentdb-python/) |
| 해당 없음 | [MongoDB용 API](mongodb-introduction.md)


Hello를 사용 하 여 [Azure Cosmos DB 에뮬레이터](local-emulator.md)를 개발 하 고 Azure 구독을 만들거나 모든 비용이 발생 하지 않고 hello DocumentDB API를 사용 하 여 로컬로 응용 프로그램을 테스트할 수 있습니다. Hello 에뮬레이터에서 응용 프로그램이 작동 방식을 만족 스 러 우면 toousing hello 클라우드에서 Azure Cosmos DB 계정을 전환할 수 있습니다.

Basic 외 만들기, 읽기, 업데이트 및 삭제 작업의 경우 JSON 문서를 검색 하는 서버 쪽 JavaScript 응용 프로그램 논리의 트랜잭션 실행에서 지 원하는 서식 있는 SQL 쿼리 인터페이스를 제공 하는 DocumentDB API hello 합니다. hello 쿼리 및 스크립트 실행 인터페이스 모든 플랫폼 라이브러리를 통해 사용할 수 있는으로 hello REST Api입니다. 

### <a name="sql-query"></a>SQL 쿼리
hello DocumentDB API 문서를 쿼리는 hello에 있는 SQL 언어를 사용 하 여 JavaScript 형식 지원 시스템 및 관계, 계층, 공간 쿼리를 지 원하는 식입니다. hello DocumentDB 쿼리 언어는는 간단 하면서도 강력한 인터페이스 tooquery JSON 문서입니다. hello 언어는 ANSI SQL 문법의 하위 집합을 지원 하 고 JavaScript 개체, 배열, 개체 생성 및 함수 호출의 긴밀 한 통합을 추가 합니다. DocumentDB API hello hello 개발자 로부터 모든 명시적 스키마 나 인덱싱 힌트 없이 모델의 쿼리를 제공합니다.

사용자 정의 함수 (Udf) hello DocumentDB API로 등록 하 고 hello 문법 toosupport 사용자 지정 응용 프로그램 논리를 확장 함으로써 SQL 쿼리의 일부로 참조 수 있습니다. 이러한 Udf JavaScript 프로그램으로 작성 되 고 hello 데이터베이스 내에서 실행 됩니다. 

.NET 개발자를 위한 DocumentDB API hello [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) 또한 LINQ 쿼리 공급자를 제공 합니다. 

### <a name="transactions-and-javascript-execution"></a>트랜잭션 및 JavaScript 실행
DocumentDB API hello 완전히 JavaScript로 작성 된 명명 된 프로그램으로 toowrite 응용 프로그램 논리를 허용 합니다. 이러한 컬렉션에 대해 등록 된 프로그램과 hello 문서는 지정 된 컬렉션 내에서 데이터베이스 작업을 실행할 수 있습니다. 트리거, 저장 프로시저 또는 사용자 정의 함수로 실행하기 위해 JavaScript를 등록할 수 있습니다. 트리거 및 저장된 프로시저 수 만들기, 읽기, 업데이트, 및 쓰기 액세스 toohello 컬렉션 없이 hello 쿼리 실행 논리의 일부로 사용자 정의 함수를 실행 하는 반면 문서를 삭제 합니다.

JavaScript 실행 hello Cosmos DB 내 hello 개념 TRANSACT-SQL에 대 한 최신 대체 값으로 JavaScript와 관계형 데이터베이스 시스템에서 지 원하는 다음에 모델링 됩니다. 모든 JavaScript 논리는 스냅숏 격리를 사용하여 앰비언트 ACID 트랜잭션 내에서 실행됩니다. 실행의 hello 과정 JavaScript 예외를 throw 하는 hello에는 다음 전체 트랜잭션이 hello 중단 됩니다.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Azure Cosmos DB에 온라인 과정이 있나요?

예, Azure DocumentDB에 [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) 과정이 있습니다. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>다음 단계
Azure 계정이 있나요? 그러면 계정을 만들고 Cosmos DB를 시작하는 과정을 안내하는 [빠른 시작](../cosmos-db/create-documentdb-dotnet.md)을 따라 Azure Cosmos DB를 시작할 수 있습니다.

[1]: ./media/documentdb-introduction/json-database-resources1.png

