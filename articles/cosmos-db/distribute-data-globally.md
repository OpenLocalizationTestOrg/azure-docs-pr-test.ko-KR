---
title: "Azure Cosmos DB를 사용 하 여 전역적으로 aaaDistribute 데이터 | Microsoft Docs"
description: "전 세계적으로 배포된 다중 모델 데이터베이스 서비스인, Azure Cosmos DB에서 글로벌 데이터베이스를 사용한 전 세계적 지역에서 복제, 장애 조치(Failover), 데이터 복구에 대해 알아봅니다."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>어떻게 Azure Cosmos DB를 사용 하 여 전역적으로 toodistribute 데이터
Azure는 어디에나 존재합니다. 전 세계 30개 이상의 지역에서 사용되며 계속해서 확장 중입니다. 전 세계의 현재 상태, Azure에서는 tooits 개발자 differentiated hello 기능 중 하나 되며 기능 toobuild hello, 배포 및 세계적으로 분산 된 응용 프로그램을 쉽게 관리 

[Azure Cosmos DB](../cosmos-db/introduction.md)는 업무에 중요한 응용 프로그램에 대한 Microsoft의 전역 분산 다중 모델 데이터베이스 서비스입니다. Azure Cosmos DB 턴키 글로벌 배포에는 [처리량 및 저장소의 탄력적인 크기 조정을](../cosmos-db/partition-data.md) hello 99 번째 백분위 수 전 세계, 자리 밀리초 대기 [5 개의 잘 정의 된 일관성 수준 ](consistency-levels.md), 모두 만족할된 높은 가용성을 보장할 수 [업계를 주도하 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)합니다. Azure Cosmos DB [데이터를 자동으로 인덱싱됩니다](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal 스미카 및 인덱스 관리를 요구 하지 않고 있습니다. 또한 다중 모델 방식이며, 문서, 키-값, 그래프 및 열 형식 데이터 모델을 지원합니다. 클라우드에서 생성 서비스로 Azure Cosmos DB 접지 hello에서 다중 테 넌 트 및 글로벌 배포와 함께 신중 하 게 엔지니어링 됩니다.

**단일 Azure Cosmos DB 컬렉션을 분할하여 여러 Azure 하위 지역에 분산**

![Azure Cosmos DB 컬렉션을 분할하여 세 하위 지역에 분산](./media/distribute-data-globally/global-apps.png)

우리가 Azure Cosmos DB를 개발하면서 알게 된 사실은 전역 분산을 나중에 추가할 수 없다는 것입니다. 전역 분산은 "단일 사이트" 데이터베이스 시스템 위에 "추가"할 수 없습니다. 세계적으로 분산 된 데이터베이스에서 제공 하는 hello 기능을 벗어날는 기존의 지리적 재해 복구 (GEO-DR) 제공한 "단일 사이트" 데이터베이스. 지역 재해 복구를 제공하는 단일 사이트 데이터베이스는 전역에 분산되는 데이터베이스의 엄격한 하위 집합입니다. 

Azure Cosmos DB 턴키 글로벌 분포 필요 없이 toobuild가 자신의 복제 스 캐 폴딩 hello 람다 패턴 중 하나를 사용 하 여 (예를 들어 [AWS DynamoDB 복제](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) hello 데이터베이스 로그를 통해 또는 여러 지역에 걸쳐 "double 쓰기"를 수행합니다. 이러한 접근 방식을 불가능 한 tooensure 정확성 이므로 이러한 접근 방식을 권장를 사운드 Sla를 제공 마십시오 했습니다. 

이 문서에서는 Azure Cosmos DB의 전역 분산 기능의 개요를 설명합니다. 또한 Azure Cosmos DB 독특한 접근 방식을 tooproviding 설명 포괄적인 Sla 합니다. 

## <a id="EnableGlobalDistribution"></a>턴키 전역 분산 활성화
Azure Cosmos DB hello 다음과 같은 장점이 기능 tooenable 있습니다 tooeasily 지구 크기 조정 응용 프로그램을 작성 합니다. 이러한 기능은 공급자 기반 hello Azure Cosmos DB 리소스를 통해 사용할 수 있는 [REST Api](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) hello Azure 포털 뿐만 아니라 합니다.

### <a id="RegionalPresence"></a>어느 지역에나 존재 
Azure는 [새 하위 지역](https://azure.microsoft.com/regions/)을 온라인으로 연결하여 지리적 존재 영역을 지속적으로 늘려가고 있습니다. Azure Cosmos DB는 기본적으로 모든 새 Azure 하위 지역에 제공됩니다. 이렇게 하면 있습니다 tooassociate Azure Cosmos DB 데이터베이스 계정 사용 하 여 지리적 위치 영역으로 Azure hello 비즈니스에 대 한 새 영역을 엽니다.

**Azure Cosmos DB는 기본적으로 모든 새 Azure 하위 지역에 제공됩니다**.

![Azure Cosmos DB는 모든 새 Azure 하위 지역에 제공됩니다.](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>개수 제한 없이 지역을 원하는 만큼 Azure Cosmos DB 데이터베이스 계정에 연결
Azure Cosmos DB tooassociate을 사용 하면 Azure Cosmos DB와 함께 Azure 지역 개수에 관계 없이 데이터베이스 계정. 지 오 펜싱 제한을 (예: 중국, 독일) 외부에서 hello Azure Cosmos DB 데이터베이스 계정에 연결 될 수 있는 지역 수에 제한이 없습니다. 다음 그림 hello 25 Azure 지역에서 데이터베이스에 구성 된 계정이 toospan를 보여 줍니다.  

**25개 Azure 지역을 아우르는 테넌트의 Azure Cosmos DB 데이터베이스 계정**

![25개 Azure 지역을 아우르는 Azure Cosmos DB 데이터베이스 계정](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>정책 기반 지역 펜스
Azure Cosmos DB는 디자인 된 toohave 정책 기반의 지 오 펜싱 기능입니다. 지 오 펜싱은 중요 한 구성 요소일 tooensure 데이터 거 버 넌 스 및 규정 준수 제한 되어 있으며 특정 지역의 사용자 계정과 연결 되지 않을 수 있습니다. 지 오 펜싱의 예 (여기 않음에 제한 되지 않은), 글로벌 메일 toohello 영역 (예를 들어 중국 및 독일) 통치 클라우드 내에서 또는 정부 세금 경계 (예를 들어 오스트레일리아) 내에서 범위를 지정 합니다. Azure 구독의 hello 메타 데이터를 사용 하 여 hello 정책 제어 됩니다.

### <a id="DynamicallyAddRegions"></a>동적으로 지역 추가 및 제거
Azure Cosmos DB 있습니다 tooadd (연결) 또는 제거 (분리) 어느 시점에서 영역 tooyour 데이터베이스 계정 (참조 [위 그림](#UnlimitedRegionsPerAccount)). 여러 파티션에 병렬로 데이터를 복제에 의해 Azure Cosmos DB 새 영역 온라인 상태가 되 면 Azure Cosmos DB를 사용할 수 있는지 30 분 내에서 아무 곳 이나 too100 TBs 구성에 대 한 hello world 확인 합니다. 

### <a id="FailoverPriorities"></a>장애 조치(Failover) 우선 순위
국가별 장애 조치 다중 지역 가동 중단, Azure Cosmos DB 없을 때의 정확한 시퀀스 toocontrol 하면 tooassociate hello 우선 순위 toovarious 영역 hello 데이터베이스 계정에 연결 된 (hello 다음 그림 참조). Azure Cosmos DB hello 자동 장애 조치 순서 지정한 hello 우선 순위 순서로 발생 하는지 확인 합니다. 지역별 장애 조치(Failover)에 대한 자세한 내용은 [비즈니스 연속성을 위한 Azure Cosmos DB의 자동 지역별 장애 조치(Failover)](regional-failover.md)를 참조하세요.

**Azure Cosmos DB의 테 넌 트 데이터베이스 계정에 연결 된 영역에 대 한 hello 장애 조치 우선 순위 순서 (오른쪽 창)을 구성할 수 있습니다.**

![Azure Cosmos DB를 사용하여 장애 조치(Failover) 우선 순위 구성](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>지역을 동적으로 "오프라인"으로 전환
Azure Cosmos DB tootake를 데이터베이스는 특정 지역에서 오프 라인 계정 및 다시 온라인 상태로 나중에 있습니다. 오프 라인으로 표시 적극적으로 복제에 참여 하지 않는 영역과 hello 장애 조치 시퀀스의 일부가 아닙니다. 이렇게 하면 잠재적으로 위험한 롤아웃하기 tooyour 응용 프로그램을 업그레이드 하기 전에 영역을 읽은 hello 중 하나에 좋은 데이터베이스 이미지를 마지막으로 toofreeze hello 있습니다.

### <a id="ConsistencyLevels"></a>전역적으로 복제된 데이터베이스에 대해 잘 정의된 여러 일관성 모델
Azure Cosmos DB는 SLA를 통해 지원되는 [잘 정의된 여러 일관성 수준](consistency-levels.md)을 노출합니다. Hello 작업/시나리오에 따라 (hello 옵션의 사용 가능한 목록)에서 특정 일관성 모델을 선택할 수 있습니다. 

### <a id="TunableConsistency"></a>전역적으로 복제된 데이터베이스에 대한 튜닝 가능한 일관성
Azure Cosmos DB tooprogrammatically 재정의 있으며 런타임 시 요청 별로 hello 기본 일관성 선택 완화 합니다. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>동적으로 구성 가능한 읽기 및 쓰기 지역
Azure Cosmos DB "읽기", "쓰기" 또는 "읽기/쓰기" 지역에 대 한 tooconfigure hello 영역 (데이터베이스에 연결 된 hello)를 사용 합니다. 

### <a id="ElasticallyScaleThroughput"></a>Azure 지역에 걸쳐 처리량을 탄력적으로 확장
프로그래밍 방식으로 처리량을 프로비전하여 Azure Cosmos DB 컬렉션을 탄력적으로 확장할 수 있습니다. hello 처리량은 적용 된 tooall hello 영역 hello 컬렉션에 배포 됩니다.

### <a id="GeoLocalReadsAndWrites"></a>지역 로컬 읽기 및 쓰기
세계적으로 분산 된 데이터베이스의 주요 이점은 hello toooffer 대기 시간이 짧은 toohello 데이터에 액세스 하는 hello world에서 아무 곳 이나 점입니다. Azure Cosmos DB는 다양한 데이터베이스 작업에 P99의 짧은 대기 시간을 보장합니다. 모든 읽기는 가장 가까운 로컬 읽기 지역의 라우트된 toohello 되도록 조정 합니다. tooserve 읽기 요청을 읽고 hello 발급 hello 쿼럼 로컬 toohello 영역 사용 됩니다. hello 마찬가지 toohello 쓰기입니다. 쓰기만 다 수의 복제본 지 속력 있게 커밋된 후 hello 쓰기 로컬로 하지 않고 원격 복제본 tooacknowledge hello 쓰기 중에 제어 된 체크 인 되 고 승인 됩니다. Cosmos DB Azure의 hello 복제 프로토콜 다르게 말해서 hello 읽기 및 쓰기 쿼럼은 항상 로컬 toohello 읽기 쓰고 지역 각각에 hello 요청이 실행 되는 hello 이라는 가정에서 작동 합니다.

### <a id="ManualFailover"></a>수동으로 지역 장애 조치(Failover) 시작
Cosmos DB azure의 hello 데이터베이스 계정 toovalidate hello tootrigger hello 장애 조치를 허용 *tooend 종료* hello 데이터베이스) (넘어 hello 전체 응용 프로그램의 가용성 속성입니다. 안전 hello 둘 다 hello 오류 검색 및 리더 투표가의 liveness 속성 보장 되므로 Azure Cosmos DB 보장 *0 데이터 손실* 테 넌 트에서 시작한 수동 장애 조치 작업에 대 한 합니다.

### <a id="AutomaticFailover"></a>자동 장애 조치(Failover)
Azure Cosmos DB는 하나 이상의 하위 지역에서 가동 중단이 발생하는 경우 자동 장애 조치(Failover)를 지원합니다. 지역 장애 조치(Failover) 동안 Azure Cosmos DB는 읽기 대기 시간, 작동 시간 가용성, 일관성 및 처리량 SLA를 유지합니다. Azure Cosmos DB 자동 장애 조치 작업 toocomplete hello 기간에 상한 값을 제공합니다. Hello 지역 가동 중단 하는 동안 잠재적 데이터 손실의 hello 창입니다.

### <a id="GranularFailover"></a>다양한 세분성의 장애 조치(Failover) 설계
현재 자동 hello 및 수동 장애 조치 기능 hello 세분성 hello 데이터베이스 계정으로 노출 됩니다. 내부적으로 Azure Cosmos DB는 디자인 된 toooffer *자동* 세밀 데이터베이스, 컬렉션 또는 심지어 파티션을 (키의 범위를 소유 하는 컬렉션)의 장애 조치 합니다. 

### <a id="MultiHomingAPIs"></a>Azure Cosmos DB의 멀티 호밍 API
Azure Cosmos DB toointeract 된 있습니다 중 하나를 사용 하 여 hello 데이터베이스 논리 (영역을 알 수 없는) 또는 실제 (지역별) 끝점입니다. 논리 끝점을 사용 하면 한 hello 응용 프로그램 수 투명 하 게 장애 조치의 경우 다중 홈입니다. hello 후자, 실제 끝점, 세분화 된 제어 toohello 응용 프로그램 tooredirect를 읽고 쓰는 toospecific 영역을 제공 합니다.

Tooconfigure hello에 대 한 기본 설정을 읽는 방법에 대 한 정보를 찾을 수 있습니다 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md), [Graph API](../cosmos-db/tutorial-global-distribution-graph.md), [테이블 API](../cosmos-db/tutorial-global-distribution-table.md), 및 [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)에 문서를 연결 합니다.

### <a id="TransparentSchemaMigration"></a>투명하고 일관적인 데이터베이스 스키마 및 인덱스 마이그레이션 
Azure Cosmos DB는 [스키마에 구애받지 않습니다](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). 데이터베이스 엔진의 hello 고유한 디자인 tooautomatically에서 허용 하 고 동기적으로 모든 스키마 나 보조 인덱스를 사용 하지 않고도 수집 hello 데이터의 모든 인덱스. 이렇게 하면 있습니다 tooiterate 전 세계적으로 분산된 응용 프로그램 신속 하 게 조정 하는 스키마 변경의 다중 단계 응용 프로그램 출시 또는 데이터베이스 스키마 및 인덱스 마이그레이션에 대 한 걱정 없이 합니다. Azure Cosmos DB의 성능 또는 가용성 저하에 명시적으로 사용자가 수행한 모든 변경 내용을 tooindexing 정책을 발생 하지 않습니다을 보장 합니다.  

### <a id="ComprehensiveSLAs"></a>포괄적인 SLA(고가용성 그 이상)
전 세계적으로 분산된 데이터베이스 서비스로 Azure Cosmos DB 제공에 대 한 잘 정의 된 SLA **데이터 손실**, **가용성**, **P99 지연**, **처리량**  및 **일관성** hello 데이터베이스와 관련 된 지역 hello 수에 관계 없이 전체 hello 데이터베이스에 대 한 합니다.  

## <a id="LatencyGuarantees"></a>대기 시간 보장
Azure Cosmos DB와 같은 세계적으로 분산 된 데이터베이스 서비스의 hello 주요 이점은 toooffer 대기 시간이 짧은 tooyour 데이터에 액세스 하는 hello world에서 아무 곳 이나 점입니다. Azure Cosmos DB는 다양한 데이터베이스 작업에 P99의 짧은 대기 시간을 보장합니다. Azure Cosmos DB를 사용 하는 hello 복제 프로토콜은 해당 hello 데이터베이스 작업 (이상적으로 모두 읽기 및 쓰기)는 항상 hello hello 클라이언트의 로컬 toothat 영역에서에서 수행 됩니다. Azure Cosmos DB SLA에 대 한 P99를 포함 하는 hello 대기 시간에 읽기, 쓰기 인덱싱된 (동기)와 다양 한 요청 및 응답 크기에 대 한 쿼리 합니다. 쓰기에 대 한 대기 시간 보장 hello hello 로컬 데이터 센터 내에서 영구 과반수 쿼럼 커밋 포함 됩니다.

### <a id="LatencyAndConsistency"></a>대기 시간과 일관성의 관계 
Toosynchronously 복제 hello 쓰기는 세계적으로 분산 된 서비스 toooffer 강력한 일관성 설치 전 세계적으로 분산을 위해 필요한 또는 동기 지역 간 읽기 – 밝은 테마와 hello 광역 네트워크 안정성 제어의 hello 속도 수행 합니다. 강력한 일관성 높은 대기 시간이 및 데이터베이스 작업의 가용성이 낮아질 발생 합니다. 따라서 낮은 대기 P99 및 99.99 가용성을 보장 하는 순서 toooffer에 hello 서비스는 비동기 복제를 사용 해야 합니다. 이에 턴 필요 hello 서비스도 제공 해야 [잘 정의 된, 상대적으로 느 일관성 choice(s)](consistency-levels.md) 강력한 보다 약 – (toooffer 낮은 대기 시간 및 가용성 보장) 이상적 "결과적" 일관성 (보다 더 강력 하 고 toooffer는 직관적인 프로그래밍 모델)입니다.

Azure Cosmos DB 하면 읽기 작업이 보호 됩니다 필요한 toocontact 복제본 간에 여러 영역 toodeliver hello 특정 일관성 수준 보장 합니다. 마찬가지로, 하 한 쓰기 작업이 차단 되지 않도록 가져올 hello 데이터가 (즉, 쓰기는 비동기적으로 복제 지역에 걸쳐) 모든 hello 지역에 걸쳐 복제 되는 동안 확인 합니다. 다중 지역 데이터베이스 계정의 경우 여러 완화된 일관성 수준이 제공됩니다. 

### <a id="LatencyAndAvailability"></a>대기 시간과 가용성의 관계 
대기 시간 및 가용성은 hello의 hello 두 변 동일한 동전 합니다. 안정 상태 및 가용성, 오류 hello 면에서 hello 작업의 대기 시간에 설명 합니다. Hello 응용 프로그램 관점에서 볼 때 느린 실행 중인 데이터베이스 작업을 사용할 수 있는 데이터베이스와 구분 되지 않습니다. 

toodistinguish 대기 시간이 긴 일으키고, Azure Cosmos DB에서 다양 한 데이터베이스 작업의 대기 시간에 절대 상한 값을 제공합니다. Hello 데이터베이스 작업 hello 상한 toocomplete 보다 더 오래 걸리면, Azure Cosmos DB 시간 초과 오류를 반환 합니다. hello Azure Cosmos DB 가용성 SLA 사용 하면 해당 hello 시간 제한을 hello 가용성 SLA에 따라 계산 됩니다. 

### <a id="LatencyAndThroughput"></a>대기 시간과 처리량의 관계
Azure Cosmos DB는 사용자가 대기 시간과 처리량 사이에서 선택을 고민하게 만들지 않습니다. 두 P99 지연에 대 한 hello SLA를 적용 하 고 프로 비전 하는 hello 처리량을 제공 합니다. 

## <a id="ConsistencyGuarantees"></a>일관성 보증
Hello 하는 동안 [강력한 일관성 모델](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) 표준은 hello "gold" 면에서 (정상 상태)에 대 한 대기 시간이 길어진다는 hello steep 가격 및 가용성 (실패의 hello 면)에서 손실의 프로그래밍 기능, 합니다. 

Cosmos DB azure에 복제 된 데이터의 일관성에 대 한 잘 정의 된 프로그래밍 모델 tooyou tooreason을 제공합니다. tooenable 있습니다 toobuild 멀티홈 응용 프로그램의 순서, Azure Cosmos DB에 의해 노출 hello 일관성 모델은 설계 된 toobe 영역에 적용할 수 및 hello 읽기 및 쓰기 제공 되는 위치에서 hello 지역에 종속 되지 합니다. 

Azure Cosmos DB 일관성 SLA는 100% 읽기 요청 (hello 기본 일관성 수준이 데이터베이스 계정 hello에 또는 hello 재정의 값 hello 요청에서 사용자가 요청 하는 hello 일관성 수준에 대 한 hello 일관성 보장 맞는지 보장 ). 읽기 요청 hello 일관성 수준에 연결 된 모든 hello 일관성 보증이 충족 하는 경우 충족 toohave hello 일관성 SLA 간주 됩니다. hello 다음 표에서가 캡처합니다 Azure Cosmos DB에서 제공 하는 toospecific 일관성 수준에 해당 하는 hello 일관성 보증이.

**Azure Cosmos DB의 특정 일관성 수준과 연결된 일관성 보장**

<table>
    <tr>
        <td><strong>일관성 수준</strong></td>
        <td><strong>일관성 특성</strong></td>
        <td><strong>SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">세션</td>
        <td>사용자 고유의 쓰기 읽기</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>단조 읽기</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>일관적인 접두사</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">제한된 부실</td>
        <td>단조 읽기(지역 내)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>일관적인 접두사</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>부실 제한 &lt; K,T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>일관적인 접두사</td>
        <td>일관적인 접두사</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>강력</td>
        <td>선형화 가능</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>일관성과 가용성의 관계
hello [impossibility 결과](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) 의 hello [CAP 정리](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) 실제로 사용할 수 있는 hello 시스템 tooremain과 오류의 hello 면 제공 linearizable 일관성 수 있다는 것을 증명 합니다. hello 데이터베이스 서비스 toobe 선택 해야 CP 시스템 hello AP 시스템을 취소 하는 동안 가용성 linearizable 일관성을 위해 취소 CP 또는 AP- [linearizable 일관성](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) 가용성 대체 합니다. Azure Cosmos DB hello를 위반 하지 공식적으로 하므로 CP 시스템 일관성 수준이 요청 합니다. 그러나 실제로 일관성은 아닙니다. 전체 또는 아무 것도 제안 linearizable 및 결과적 일관성 사이의 일관성 스펙트럼 hello와 함께 여러 잘 정의 된 일관성 모델이 있습니다. Azure Cosmos DB에서 테스트해 보았습니다 tooidentify 일관성 모델 현실 세계 적용 가능성 및는 직관적인 프로그래밍 모델을 사용 하 여 완화 hello 중 몇 가지 있습니다. Azure Cosmos DB와 함께 99.99 가용성 SLA를 제공 하 여 hello 일관성 가용성 장단점 탐색 [여러 완화 아직 잘 정의 된 일관성 수준이](consistency-levels.md)합니다. 

### <a id="ConsistencyAndAvailability"></a>일관성과 대기 시간의 관계
Daniel Abadi 교수는 [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)라고 하는 보다 포괄적인 CAP 변형을 제안했으며, 이 변형 역시 안정적인 상태에서 대기 시간과 일관성의 균형을 고려합니다. 된다고 알리는 안정 상태에서 일관성 및 대기 시간 사이의 hello 데이터베이스 시스템 선택 해야 합니다. 여러 상대적으로 느 일관성 모델에서 (뒷받침 되며 비동기 복제 및 로컬 읽기, 쓰기 쿼럼), Azure Cosmos DB를 수행 하면 모든 읽기 및 쓰기 하 로컬 toohello 읽기 각각 영역을 씁니다.  이렇게 하면 hello 일관성 수준에 대 한 hello 영역 내에서 Azure Cosmos DB toooffer 짧은 대기 시간을 보장 합니다.  

### <a id="ConsistencyAndThroughput"></a>일관성과 처리량의 관계
Hello 선택 했는지에 따라 특정 일관성 모델의 hello 구현 하므로 [쿼럼 유형을](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), hello 처리량도 일관성 hello 선택에 따라 다릅니다. 예를 들어, Azure Cosmos DB에서 hello으로 강력 하 게 일관 된 읽기 처리량은 결국 일관 된 읽기의 약 절반 toothat 합니다. 
 
**Azure Cosmos DB에서 특정 일관성 수준에 대한 읽기 용량의 관계**

![일관성과 처리량 간의 관계](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>처리량 보장 
Azure Cosmos DB 있습니다 tooscale 처리량 (으로, 저장소), 탄력적으로 hello 수요에 따라 서로 다른 영역에서. 

**단일 Azure Cosmos DB 컬렉션을 분할(세 개의 분할된 데이터베이스에 걸쳐)하여 세 Azure 지역에 분산**

![Azure Cosmos DB가 컬렉션을 분산 및 분할](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Azure Cosmos DB 컬렉션은 두 차원을 사용하여, 즉 하위 지역 내에서 그런 다음 하위 지역에 걸쳐 분산됩니다. 방법은 다음과 같습니다. 

* 단일 하위 지역 내에서 Azure Cosmos DB 컬렉션은 리소스 파티션의 측면에서 확장됩니다. 각 리소스 파티션은 키 집합을 관리하며 복제본 집합 간에 상태 시스템을 복제하여 강력한 일관성과 높은 가용성을 유지합니다. Azure Cosmos DB는 완전히 관리 되는 리소스 시스템 리소스 파티션을 부하의 시스템 할당 된 리소스 tooit의 hello 예산에 대 한 처리량을 제공 하는 일을 담당 합니다. hello Azure Cosmos DB 컬렉션의 크기 조정을 완전히 투명 하 게은 Azure Cosmos DB hello 리소스 파티션을 관리 하 고 분할 하 고 필요에 따라 병합 됩니다. 
* 그런 다음 각 hello 리소스 파티션에 여러 지역에 걸쳐 배포 합니다. 소유 하는 리소스 파티션을 다양 한 지역 양식 파티션 집합에서 키의 동일한 집합 hello (참조 [위 그림](#ThroughputGuarantees)).  파티션 집합 내의 리소스 파티션을 조정 된 여러 영역 간에 hello 상태 컴퓨터 복제를 사용 합니다. Hello 일관성 수준 구성에 따라 다른 토폴로지 (예를 들어 별모양, 데이지 체인, 트리 등)를 사용 하 여 동적으로 파티션 집합 내의 리소스 파티션은 hello 구성 됩니다. 

응답성이 높은 파티션 관리, 부하 분산 및 엄격한 리소스 거 버 넌 스를 통해 Azure Cosmos DB 있습니다 tooelastically 배율 처리량을 Azure Cosmos DB 컬렉션에 여러 Azure 지역에 걸쳐. 컬렉션에서 변경 처리량 Azure Cosmos DB hello 절대에 대 한 상한 요청 toochange hello 처리량에 대 한 대기 시간을 보장 하는 다른 데이터베이스 작업과 함께 같은 Azure Cosmos DB-는 런타임 작업은 됩니다. 예를 들어, 다음 그림 hello 고객의 컬렉션 hello 수요에 탄력적으로 프로 비전 된 처리량 (두 영역 간 1m-10 분 요청/초에서까지).
 
**처리량이 탄력적으로 프로비전된(초당 1M-10M개 요청) 고객의 컬렉션**

![Azure Cosmos DB가 처리량을 탄력적으로 프로비전](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>처리량과 일관성의 관계 
[일관성과 처리량의 관계](#ConsistencyAndThroughput)와 똑같습니다.

### <a id="ThroughputAndAvailability"></a>처리량과 가용성의 관계
Azure Cosmos DB hello 변경 될 때 toohello 처리량 toomaintain 가용성을 계속 합니다. Azure Cosmos DB 파티션을 (예를 들어 분할, 병합, 복제 작업)를 투명 하 게 관리 하 고 있는지 hello 작업 저하가 그만큼 성능이 나 가용성, 탄력적으로 hello 응용 프로그램 증가 하거나 처리량은 감소 하는 동안 되도록 합니다. 

## <a id="AvailabilityGuarantees"></a>가용성 보장
Azure Cosmos DB 제공 99.99% 가동 시간 가용성 SLA 각 hello에 대 한 데이터 및 제어 평면 작업 합니다. 앞서 설명했듯이, Azure Cosmos DB의 가용성 보장에는 모든 데이터 및 제어 평면 작업에 대한 대기 시간에 제공되는 절대 상한값이 포함됩니다. hello 가용성 보장 확고 되며 지역 또는 지역 간 지리적 거리가 hello 수로 변경 되지 않습니다. 가용성 보장은 수동 및 자동 장애 조치(failover)를 통해 적용됩니다. Cosmos DB azure 응용 프로그램 논리 끝점에 대해 작동할 수 하 고 장애 조치 시 hello 요청 toohello 새 영역 경로 투명 하 게 설정할 수 있도록 하는 투명 한 멀티 호 밍 Api를 제공 합니다. 다르게 put, 응용 프로그램에서 toobe 국가별 장애 조치 시 다시 배포 하지 않아도 되 고 hello 가용성 Sla 유지 됩니다.

### <a id="AvailabilityAndConsistency"></a>가용성과 일관성, 대기 시간 및 처리량의 관계
가용성과 일관성, 대기 시간 및 처리량 사이의 관계는 [가용성과 일관성의 관계](#ConsistencyAndAvailability), [대기 시간과 가용성의 관계](#LatencyAndAvailability) 및 [처리량과 가용성의 관계](#ThroughputAndAvailability)에 설명되어 있습니다. 

## <a id="GuaranteesAgainstDataLoss"></a>"데이터 손실"에 대한 보장 및 시스템 동작
Azure Cosmos DB에서 (컬렉션의) 각 파티션은 10-20개 이상의 오류 도메인에 분산된 여러 복제본을 통해 높은 가용성이 유지됩니다. 모든 쓰기 동기적으로 처리 하 고 지 속력 있게 커밋된 복제본의 과반수 쿼럼을 기준으로 toohello 클라이언트를 승인 하기 전에. 비동기 복제는 여러 지역에 분산된 파티션 간의 조정을 통해 적용됩니다. Azure Cosmos DB는 테넌트가 시작하는 수동 장애 조치(failover)에 대한 데이터 무손실을 보장합니다. 자동 장애 조치 중 Azure Cosmos DB 구성 hello 상한이 hello 데이터 손실 기간에 해당 SLA의 일부로 확인 간격을 제한 보장 합니다.

## <a id="CustomerFacingSLAMetrics"></a>고객을 위한 SLA 메트릭
Azure Cosmos DB을 투명 하 게 hello 처리량, 대기 시간, 일관성 및 가용성 메트릭을 표시합니다. 이러한 메트릭은 hello Azure 포털 (다음 그림 참조)를 통해 및 프로그래밍 방식으로 액세스할 수 있습니다. 또한 Azure Application Insights를 사용하여 다양한 임계값에 대한 경고를 설정할 수 있습니다.
 
**투명 하 게 사용할 수 있는 tooeach 테 넌 트를 일관성, 대기 시간, 처리량 및 가용성 메트릭은**

![Azure Cosmos DB 고객에게 표시되는 SLA 메트릭](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>다음 단계
* 사용 하 여 Azure Cosmos DB 계정에서 전역 복제 tooimplement hello Azure 포털에서 참조 [tooperform Azure Cosmos DB 글로벌 데이터베이스 복제를 사용 하 여 Azure 포털을 hello 하는 방법을](tutorial-global-distribution-documentdb.md)합니다.
* toolearn 방법에 대 한 Azure Cosmos DB와 함께 tooimplement 다중 마스터 아키텍처 참조 [다중 마스터 데이터베이스 아키텍처를 Azure Cosmos DB](multi-region-writers.md)합니다.
* 에 대해 더 알아봅니다 toolearn Azure Cosmos DB에서 자동 및 수동 장애 조치 작동 방법 참조 [Azure Cosmos DB에서 국가별 장애 조치](regional-failover.md)합니다.

## <a id="References"></a>참조
1. Eric Brewer. [Towards Robust Distributed Systems](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Eric Brewer. [단면 12 년 후 – hello 규칙 변경 방법](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer&#39;s Conjecture and Feasibility of Consistent, Available, Partition Tolerant Web Services](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf)
4. Daniel Abadi. [Consistency Tradeoffs in Modern Distributed Database Systems Design](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)
5. Martin Kleppmann. [Please stop calling databases CP or AP](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)
6. Peter Bailis et al. [Probabilistic Bounded Staleness (PBS) for Practical Partial Quorums](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
7. Naor and Wool. [Load, Capacity and Availability in Quorum Systems](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf)
8. Herlihy and Wing. [Lineralizability: A correctness condition for concurrent objects](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)
9. [Azure Cosmos DB SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
