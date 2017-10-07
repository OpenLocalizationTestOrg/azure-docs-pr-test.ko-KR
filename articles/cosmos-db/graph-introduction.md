---
title: "소개 tooAzure Cosmos DB Graph Api | Microsoft Docs"
description: "Apache TinkerPop의 hello hello Gremlin 그래프 쿼리 언어를 사용 하 여 짧은 대기 시간으로 Azure Cosmos DB toostore, 쿼리 및 트래버스 massive 그래프를 사용할 수는 방법에 대해 알아봅니다."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Cosmos DB 소개 tooAzure: Graph API

[Azure Cosmos DB](introduction.md) 세계적으로 분산 된 다중 모델 데이터베이스 서비스로, Microsoft에서 중요 응용 프로그램에 대 한 hello 됩니다. Azure Cosmos DB에는 [턴키 글로벌 메일](distribute-data-globally.md), [처리량 및 저장소의 탄력적인 크기 조정을](partition-data.md) hello 99 번째 백분위 수 전 세계, 자리 밀리초 대기 [5 개 잘 정의 된 일관성 수준이](consistency-levels.md), 모두에서 지 원하는 고가용성을 보장할 수 [업계를 주도하 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)합니다. Azure Cosmos DB [데이터를 자동으로 인덱싱됩니다](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal 스미카 및 인덱스 관리를 요구 하지 않고 있습니다. 또한 다중 모델 방식이며, 문서, 키-값, 그래프 및 열 형식 데이터 모델을 지원합니다.

![Gremlin, 그래프 및 Azure Cosmos DB](./media/graph-introduction/graph-gremlin.png)

hello Azure Cosmos DB Graph API를 제공합니다.

- 그래프 모델링
- 순회 API
- 턴키 전역 배포
- 10ms 미만 읽기 대기 시간이 15 밀리초 미만에 hello 99 번째 백분위 수와 처리량 및 저장소의 탄력적인 크기 조정
- 인스턴트 쿼리 가용성을 활용한 자동 인덱싱
- 튜닝 가능한 일관성 수준
- 99.99% 가용성을 포함한 포괄적인 SLA

Azure Cosmos DB tooquery hello를 사용할 수 있습니다 [Apache TinkerPop](http://tinkerpop.apache.org) 그래프 탐색 언어 [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), 또는 다른 TinkerPop 호환 그래프 시스템 like [Apache Spark GraphX](spark-connector-graph.md).

이 문서는 hello Azure Cosmos DB Graph API의 개요를 제공 하 고 방법을 사용할 수 있습니다 toostore massive 그래프 가장자리와 꼭지점의 수십 억을 설명 합니다. 밀리초 대기 시간으로 hello 그래프를 쿼리 하 고 hello 그래프 구조 및 스키마에 따라 쉽게 발전할 수 있습니다.

## <a name="graph-database"></a>그래프 데이터베이스
데이터는 hello 현실 세계에 표시 된 대로 자연스럽 게 연결 되어 있습니다. 기존의 데이터 모델링은 엔터티에 중점을 둡니다. 대부분의 응용 프로그램에 대 한 이기도 필요 toomodel 또는 toomodel 엔터티와 관계 모두 자연스럽 게 합니다.

[그래프](http://mathworld.wolfram.com/Graph.html)는 [꼭짓점](http://mathworld.wolfram.com/GraphVertex.html) 및 [에지](http://mathworld.wolfram.com/GraphEdge.html)로 구성된 구조입니다. 꼭짓점 및 에지는 둘 다 임의 개수의 속성을 포함할 수 있습니다. 꼭짓점은 사람, 장소, 이벤트 등의 개별 개체를 나타냅니다. 에지는 꼭짓점 간의 관계를 나타냅니다. 예를 들어, 한 사용자가 다른 사용자를 알고 있으며, 이벤트에 관계되어 있고, 최근 한 위치에 있었을 수 있습니다. 속성은 hello 꼭지점 및 가장자리에 대 한 정보를 표현합니다. 예제 속성에는 이름, 사용 기간 및 에지가 있는 꼭짓점이 있습니다. 이 꼭짓점에는 타임스탬프 및/또는 가중치가 있습니다. 공식적으로 이 모델을 [속성 그래프](http://tinkerpop.apache.org/docs/current/reference/#intro)라고 합니다. Azure Cosmos DB hello 속성 그래프 모델을 지원합니다.

예를 들어 hello 다음 샘플 사용자, 모바일 장치, 취미, 및 운영 체제 간의 그래프 표시 관계입니다.

![사람, 장치 및 관심 분야를 보여 주는 샘플 데이터베이스](./media/graph-introduction/sample-graph.png)

그래프는 유용한 toounderstand 다양 한 범위의 과학, 기술 및 비즈니스에서 데이터 집합입니다. 그래프 데이터베이스를 사용하면 자연스럽고 효율적으로 그래프를 모델링하고 저장할 수 있으므로 다양한 시나리오에 유용합니다. 그래프 데이터베이스는 일반적으로 NoSQL 데이터베이스입니다. 사용 사례에 주로 스키마 유연성과 신속한 반복이 필요하기 때문입니다.

그래프는 새롭고 강력한 데이터 모델링 기법을 제공합니다. 하지만이 사실을 자체적으로 충분 한 이유 toouse 그래프 데이터베이스는 아닙니다. 그래프 순회와 관련된 여러 사용 사례 및 패턴에서 그래프는 전형적인 SQL 및 NoSQL 데이터베이스에 비해 훨씬 높은 성능을 발휘합니다. 이러한 성능 차이는 친구의 친구 같은 둘 이상의 관계를 트래버스할 때 더욱 증폭됩니다.

깊이 우선 검색, 너비 우선 검색 및 Dijkstra의 알고리즘, 소셜 네트워킹, 콘텐츠 관리, 지리 공간와 같은 다양 한 도메인의 toosolve 문제와 같은 그래프 알고리즘과 그래프 데이터베이스를 제공 하는 hello 빠른 탐색을 결합할 수 있습니다. 및 권장 사항입니다.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Azure Cosmos DB를 사용한 광범위한 규모의 그래프
Azure Cosmos DB는 글로벌 메일, 저장소 및 처리량, 자동 인덱싱 및 쿼리, 튜닝할 수 있는 일관성 수준 및 hello TinkerPop 표준에 대 한 지원의 크기 조정 탄력적에서 제공 하는 완전히 관리 되는 그래프 데이터베이스입니다.  

![Azure Cosmos DB 그래프 아키텍처](./media/graph-introduction/cosmosdb-graph-architecture.png)

Azure Cosmos DB hello 다음 differentiated 비교 했을 때 기능 제공 hello 시장에서 tooother 그래프 데이터베이스:

* 탄력적으로 확장 가능한 처리량 및 저장소

 Hello에 대 한 실제 정보 그래프는 단일 서버 hello 용량 이상 tooscale가 필요합니다. Azure Cosmos DB를 사용하면 여러 서버에 걸쳐 원활하게 그래프를 확장할 수 있습니다. 또한 액세스 패턴을 독립적으로 기반으로 하 여 그래프의 hello 처리량을 늘릴 수 있습니다. Azure Cosmos DB 지원 toovirtually 확장할 수 있는 그래프 데이터베이스 프로 비전 된 처리량 및 무제한 저장소 크기입니다.

* 다중 지역 복제

 Cosmos DB azure 계정과 연결 된 한 여 그래프 데이터 tooall 영역을 투명 하 게 복제 합니다. 게시는 toodevelop 필요한 응용 프로그램을 대 한 전역 액세스 toodata 수 있습니다. 일관성, 가용성 및 성능 및 해당 보장의 hello 영역에는 각각 장단점이 있습니다. Azure Cosmos DB는 multi-homing API를 통해 투명한 지역 장애 조치(failover)를 제공합니다. Hello 전세계 처리량 및 저장소를 탄력적으로 확장할 수 있습니다.

* 익숙한 Gremlin 구문을 통한 빠른 쿼리 및 순회

 다른 유형의 꼭짓점 및 에지를 저장하고 익숙한 Gremlin 구문을 통해 이러한 문서를 쿼리합니다. Azure Cosmos DB에서 높은 동시, 잠금 해제, 구조적 로그 인덱싱 기술을 tooautomatically 인덱스를 모든 콘텐츠를 사용합니다. 이 기능을 사용 하면 다양 한 실시간 쿼리 및 toospecify 스키마 힌트, 보조 인덱스 또는 뷰 탐색 hello 없이 필요 합니다. [Gremlin을 사용한 그래프 쿼리](gremlin-support.md)에서 자세한 내용을 참조하세요.

* 완전히 관리

 Azure Cosmos DB hello 필요 toomanage 데이터베이스 및 컴퓨터 리소스를 제거합니다. 완전히 관리 되는 Microsoft Azure 서비스로 toomanage 가상 컴퓨터를 필요 하지 않습니다, 그리고 배포 및 소프트웨어 구성, 배율, 관리 또는 복잡 한 데이터 계층 업그레이드를 처리 합니다. 모든 그래프가 자동으로 백업되고 지역적 실패로부터 보호됩니다. 필요 시 쉽게 Azure Cosmos DB 계정을 추가하고 용량을 프로비전할 수 있으므로 데이터베이스 작동 및 관리 대신 응용 프로그램에 집중할 수 있습니다.

* 자동 인덱싱

 기본적으로 Azure Cosmos DB 자동으로 hello 그래프에서 노드 및 가장자리 내에서 모든 hello 속성 인덱스 예상 되거나 않는 스키마 또는 보조 인덱스의 만들기 필요 합니다.

* Apache TinkerPop과의 호환성

 기본적으로 azure Cosmos DB hello 오픈 소스 Apache TinkerPop 표준을 지원 하 고 TinkerPop 사용 그래프의 다른 시스템으로 통합 될 수 있습니다. 따라서 Titan 또는 Neo4j 등의 다른 그래프 데이터베이스에서 쉽게 마이그레이션하거나, [Apache Spark GraphX](spark-connector-graph.md) 같은 그래프 분석 프레임워크에서 Azure Cosmos DB를 사용할 수 있습니다.

* 튜닝 가능한 일관성 수준

 5 개의 잘 정의 된 일관성 수준이 tooachieve 최적의 절충 지점을 일관성과 성능 사이의 선택 합니다. 쿼리 및 읽기 작업에 대해 Azure Cosmos DB는 강력, 제한된 부실, 세션, 일관된 접두사, 최종의 5가지 일관성 수준을 제공합니다. 이러한 세부적인, 잘 정의 된 일관성 수준 toomake 사운드 장단점 일관성, 가용성 및 대기 시간을 허용 합니다. 자세한 내용을 알아보세요 [toomaximize 가용성 및 DocumentDB의 성능 수준 일관성을 사용 하 여](consistency-levels.md)합니다.

Azure Cosmos DB도 צ ְ ײ 문서 및 graph와 같은 여러 모델 내 동일한 컨테이너/데이터베이스 hello 합니다. 문서와 함께 문서 컬렉션 toostore 그래프 데이터를 사용할 수 있습니다. 두 SQL 쿼리를 사용 하 여 JSON을 통해 및 Gremlin 쿼리 tooquery hello 그래프와 동일한 데이터입니다.

## <a name="getting-started"></a>시작
Hello Azure CLI (명령줄 인터페이스), Azure Powershell을 사용 하거나 Azure 포털 그래프 API toocreate Azure Cosmos DB 계정에 대 한 지원과 함께 hello 수 있습니다. 계정을 만든 후 hello Azure 포털에서는 서비스 끝점 같은 `https://<youraccount>.graphs.azure.com`, Gremlin에 대 한 WebSocket 프런트 엔드를 제공 하는 합니다. Hello 같은 프로그램 TinkerPop 호환 도구를 구성할 수 있습니다 [Gremin 콘솔](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), Java, Node.js 또는 모든 Gremlin 클라이언트 드라이버에서 tooconnect toothis 끝점 및 빌드 응용 프로그램입니다.

hello 아래 표에 나와 Gremlin 드라이버 인기 있는 Azure Cosmos DB에 대해 사용할 수 있습니다.

| 다운로드 | 문서화 |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.JS](https://www.npmjs.com/package/gremlin) |[Github의 Gremlin-JavaScript](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin 콘솔](https://tinkerpop.apache.org/downloads.html) |[TinkerPop 문서](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Cosmos DB azure.NET 라이브러리 hello 위에 Gremlin 확장 메서드를 제공 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md) NuGet을 통해. 이 라이브러리는 "프로세스" Gremlin 서버 제공 tooconnect를 사용할 수 있는 직접 tooDocumentDB 데이터 파티션을 합니다.

| 다운로드 | 문서화 |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Hello를 사용 하 여 [Azure Cosmos DB 에뮬레이터](local-emulator.md), Graph API toodevelop hello를 사용 하 고 Azure 구독을 만들거나 모든 비용이 발생 하지 않고 로컬로 테스트할 수 있습니다. Hello 에뮬레이터에서에서 응용 프로그램 작동 방식을 만족 스 러 우면 toousing hello 클라우드에서 Azure Cosmos DB 계정을 전환할 수 있습니다.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Azure Cosmos DB 그래프 지원에 대한 시나리오
Azure Cosmos DB 그래프 지원을 사용할 수 있는 몇 가지 시나리오는 다음과 같습니다.

* 소셜 네트워크

 고객 및 다른 사람과의 상호 작용에 대한 데이터를 조합하여 개인 설정된 환경을 개발하거나, 고객 행동을 예측하거나, 관심 영역이 비슷한 다른 사람과 연결해줄 수 있습니다. Azure Cosmos DB 사용된 toomanage 소셜 네트워크 되어 고객 기본 설정 및 데이터를 추적 합니다.

* 추천 엔진

 이 시나리오는 hello 소매 업계에 주로 사용 됩니다. 제품, 사용자 및 사용자 상호 작용(예: 항목 구입, 검색, 등급 지정)에 대한 정보를 조합하여 사용자 지정된 추천을 작성할 수 있습니다. 짧은 대기 시간, 유연한 배율과 네이티브 hello Azure Cosmos DB 그래프 지 원하는 것이 이러한 상호 작용을 모델링에 적합 합니다.

* 지리 공간적

 통신, 업무 및 여행 계획에 많은 응용 프로그램 영역 내에서 필요한 위치 toofind 필요 하거나 두 위치 간에 hello 최적/가장 짧은 경로 찾습니다. Azure Cosmos DB는 이러한 문제를 자연스럽게 해결합니다.

* 사물 인터넷

 Hello 네트워크 및 그래프로 모델링 IoT 장치 간의 연결을 사용 하 여 장치 및 자산 상태 hello 보다 잘 이해 빌드하고 어떻게 hello 네트워크의 한 부분에 있는 변경 수에 영향을 줄 다른 부분에 알아봅니다.

## <a name="next-steps"></a>다음 단계
toolearn Azure Cosmos DB에서 graph 지원에 대 한 참조.

* Hello로 시작 [Azure Cosmos DB 그래프 자습서](create-graph-dotnet.md)합니다.
* 너무 방법에 대 한 자세한 내용은[쿼리 그래프는 Gremlin를 사용 하 여 Azure Cosmos DB](gremlin-support.md)합니다.
