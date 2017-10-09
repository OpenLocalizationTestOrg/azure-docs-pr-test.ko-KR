---
title: "Azure에서 Linux와 함께 Cassandra aaaRun | Microsoft Docs"
description: "Node.js 응용 프로그램에서 Azure 가상 컴퓨터의 linux 클러스터는 Cassandra toorun 방법"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Azure에서 Linux 환경의 Cassandra 실행 및 Node.js에서 Cassandra에 액세스
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) 및 [CentOS의 Spark 클러스터 및 Cassandra](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/)는 Resource Manager 템플릿을 참조하세요.

## <a name="overview"></a>개요
Microsoft Azure는 운영 체제, 응용 프로그램 서버, 메시징 미들웨어뿐 아니라 상용 및 오픈 소스 모델의 SQL 및 NoSQL 데이터베이스를 포함하는 Microsoft 및 타사 소프트웨어를 실행하는 개방형 클라우드 플랫폼입니다. Azure를 비롯한 공용 클라우드에 복원 서비스를 빌드하려면 응용 프로그램 서버 및 저장소 계층 둘 다의 신중한 계획과 세밀한 아키텍처가 필요합니다. Cassandra의 분산 저장소 아키텍처는 클러스터 오류에 대한 내결함성이 있는 고가용성 시스템 빌드에 도움이 됩니다. Cassandra는 cassandra.apache.org에서 Apache Software Foundation에 의해 유지 관리되는 클라우드 규모의 NoSQL 데이터베이스입니다. Cassandra는 Java로 작성되었으므로 Windows 및 Linux 플랫폼에서 모두 실행됩니다.

hello이이 문서는 Microsoft Azure 가상 컴퓨터와 가상 네트워크를 활용 하는 단일 및 다중 데이터 센터 클러스터로 ubuntu tooshow Cassandra 배포. hello 클러스터 배포에 최적화 된 프로덕션 작업에는이 문서의 범위를 벗어났습니다 다중 디스크 노드 구성 해야 하므로, 적절 한 링 토폴로지 디자인 및 데이터 모델링 toosupport hello 필요한 복제, 데이터 일관성, 처리량 및 고가용성 요구 사항입니다.

Docker, Chef 또는 puppet과 인프라 배포를 더 쉽게 많은 hello을 만들 수 있는 작업과 관련 된 사항을 건물 hello Cassandra 클러스터 기본 접근 방식을 tooshow 비교를 수행 하는 문서입니다.  

## <a name="hello-deployment-models"></a>hello 배포 모델
Microsoft Azure 네트워킹을 통해 hello 배포의 격리 된 개인 클러스터는 hello 액세스 제한 tooattain 세밀 하 게 세분화 된 네트워크 보안을 수 있습니다.  이 문서는 기본적인 수준 hello Cassandra 배포를 보여 주는 하는 방법에 대 한 이므로 하지 살펴볼 것에서 hello 일관성 수준 및 처리량에 대 한 hello 최적의 저장소 디자인입니다. Hello 우리의 가상 클러스터에 대 한 네트워킹 요구 사항 목록은 다음과 같습니다.

* 외부 시스템은 Azure 내부나 외부에서 Cassandra 데이터베이스에 액세스할 수 없어야 합니다.
* Cassandra 클러스터 toobe thrift 트래픽에 대 한 부하 분산 장치 뒤에
* 클러스터 가용성 향상을 위해 각 데이터 센터의 두 그룹에 Cassandra 노드를 배포해야 합니다.
* 잠글 hello 클러스터 하므로 하는 서버 팜의 응용 프로그램에 직접 액세스 toohello 데이터베이스가
* SSH 이외의 공용 네트워킹 끝점이 없어야 합니다.
* 각 Cassandra 노드에 고정된 내부 IP 주소가 필요합니다.

배포 된 tooa 단일 Azure 지역 또는 hello 작업 부하의 distributed hello 특성에 따라 toomultiple 영역의 Cassandra 수 있습니다. 다중 지역 배포 모델 사용된 tooserve 최종 사용자가 더 가깝기 때문 tooa 특정 지리 hello 통해 수 동일한 Cassandra 인프라입니다. 여러 데이터 센터에서 시작 된 쓰고 hello 데이터 tooapplications의 일관 된 뷰를 제공 하는 다중 마스터의 hello 동기화의 Cassandra의 기본 제공 노드 복제는 주의 합니다. 다중 지역 배포는 hello 보다 광범위 한 Azure 서비스 중단의 위험 완화 hello와 유용할 수 있습니다. Cassandra의 조정 가능한 일관성 및 복제 토폴로지는 응용 프로그램의 다양한 RPO 요구를 충족하는 데 유용합니다.

### <a name="single-region-deployment"></a>단일 지역 배포
단일 지역 배포 및 9 월 hello 배우게 되는 다중 지역 모델을 만드는 것부터 시작 합니다. 위에서 언급 한 hello 네트워크 보안 요구를 충족 될 수 있도록 azure 가상 네트워크 격리 사용된 toocreate 서브넷 됩니다.  Ubuntu 14.04 LTS 및 Cassandra 2.08; hello 단일 지역 배포 만들기에 설명 된 hello 프로세스 사용 그러나 hello 프로세스 수 채택된 되 toohello 다른 Linux 변형 됩니다. hello 단일 지역 배포의 시스템 특성 hello hello 다음과가 같습니다.  

**고가용성:** hello Cassandra 노드 tootwo 가용성 집합 hello 노드는 고가용성을 위해 여러 오류 도메인 간에 분산 되어 있도록 그림 1에 배포 된 hello에 표시 된 것입니다. 각 가용성 집합으로 주석이 달려 있어야 하는 Vm은 매핑된 too2 오류 도메인입니다.  작동 중단 시간 (예:: 하드웨어나 소프트웨어 장애) hello 개념의 업그레이드 도메인 (예: 호스트 또는 게스트 OS 패치/업그레이드, 응용 프로그램 업그레이드) 하는 동안 계획 되지 않은 오류 도메인 toomanage의 Microsoft Azure 사용 하 여 hello 개념 작동 중단 시간에 예약 된 관리에 사용 됩니다. 참조 하십시오 [Azure 응용 프로그램에 대 한 고가용성 및 재해 복구](http://msdn.microsoft.com/library/dn251004.aspx) 높은 가용성을 계산 하기에 있는 오류 및 업그레이드 도메인의 hello 역할에 대 한 합니다.

![단일 지역 배포](./media/cassandra-nodejs/cassandra-linux1.png)

그림 1: 단일 지역 배포

참고는이 문서 작성 hello 시 Azure 허용 하지 않습니다 hello Vm tooa 특정 장애 도메인; 그룹의 명시적 매핑 따라서 그림 1에 표시 된 hello 배포 모델을 사용 하더라도 것이 통계적으로 할 모든 hello 가상 컴퓨터 4 개가 아니라 매핑된 tootwo 오류 도메인을 수 있습니다.

**로드 균형 조정 Thrift 트래픽:** hello 웹 서버가 안쪽 Thrift 클라이언트 라이브러리는 내부 부하 분산 장치를 통해 toohello 클러스터에 연결 합니다. 이 위해서는 hello 내부 부하 분산 장치 toohello "데이터" 서브넷을 추가 하는 hello 프로세스 (그림 1 참조) hello Cassandra 클러스터를 호스팅하는 hello 클라우드 서비스의 hello 컨텍스트에서 합니다. Hello 내부 부하 분산 장치에서 정의 되 면 각 노드는 hello 부하 분산 된 끝점 toobe 정의 된 부하 분산 장치 이름이 이전 부하 분산 된 집합의 hello 주석으로 추가 해야 합니다. 자세한 내용은 [Azure 내부 부하 분산 ](../../../load-balancer/load-balancer-internal-overview.md)을 참조하세요.

**클러스터 시드:** tooselect hello 클러스터의 시드 노드 toodiscover hello 토폴로지 통신할 초기값으로 새 노드를 hello에 대 한 대부분의 항상 사용 가능한 노드에 hello 고려해 야 합니다. 각 가용성 집합에서 한 노드 시드 노드 tooavoid 단일 오류 지점으로 지정 됩니다.

**복제 요소와 일관성 수준을:** Cassandra의 기본 제공 고가용성 및 데이터 지 속성의 특징은 hello 복제 요소 (RF-hello 클러스터에 저장 된 각 행의 복사본 개수) 및 일관성 수준 (개수 복제본 toobe hello 결과 toohello 호출자에 게 반환 하기 전에 읽기/쓰기). 복제 요소 hello 일관성 수준이 hello CRUD 쿼리를 실행 하는 동안 지정 된 반면 hello 있어 실제로 (유사한 tooa 관계형 데이터베이스) 생성 하는 동안 지정 됩니다. Cassandra 설명서를 참조 [일관성에 대 한 구성](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 일관성 세부 정보 및 쿼럼 계산에 대 한 hello 수식에 대 한 합니다.

Cassandra 두 가지 유형의 일관성 및 결과적 일관성; – 데이터 무결성 모델 지원 hello 복제 요소와 일관성 수준이 경우 hello 데이터 일관성이 됩니다 즉시 쓰기 작업이 완료 되는 것은 결국 일관 된 결정 함께 합니다. 예를 들어 지정 하면 쿼럼 hello 수가 필요한 tooattain로 작성 된 복제본 toobe 아래의 모든 일관성 수준 하는 동안 데이터 일관성을 보장 하는 hello 일관성 수준이 항상 (예: 1 개) 쿼럼 발생 결국 일관성이 데이터입니다.

3, 쿼럼 복제 요소와 위에 표시 된 hello 8 개 노드 클러스터 (2 노드는 읽기 또는 쓰기 일관성을 위해) 읽기/쓰기 일관성 수준이, hello 복제 당 1 노드는 최대 hello 응용 프로그램 시작 하기 전에 그룹에서 hello 이론적 손실이 감당할 수 있는 hello 오류를 검색 합니다. 이 모든 hello 키 공간 읽기/쓰기 요청을 분산도 가정 합니다.  hello 다음은 배포 된 hello 클러스터를 사용 하는 hello 매개 변수입니다.

단일 지역 Cassandra 클러스터 구성:

| 클러스터 매개 변수 | 값 | 설명 |
| --- | --- | --- |
| 노드 수(N) |8 |총 hello 클러스터의 노드 수 |
| 복제 계수(RF) |3 |지정된 행의 복제본 수 |
| 일관성 수준(쓰기) |QUORUM[(RF/2) +1) = 2] hello 결과 수식을 내림 hello의 |에 작성 hello 대부분 복제본 2 개 hello 응답 toohello 호출자를 전송 하기 전에 3 번째 복제본 결국 일관 된 방식으로 기록 됩니다. |
| 일관성 수준(읽기) |쿼럼 [(RF/2) + 1 = 2] hello 수식의 hello 결과 내림 |응답 toohello 호출자에 게 보내기 전에 복제본 2 개를 읽습니다. |
| 복제 전략 |NetworkTopologyStrategy자세한 내용은 Cassandra 설명서의 [데이터 복제](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) 참조 |Hello 배포 토폴로지를 이해 하 고 모든 hello 복제 하지 않는에서 중단 될 hello 동일한 복제본 노드에 배치 랙 |
| Snitch |GossipingPropertyFileSnitch 자세한 내용은 Cassandra 설명서의 [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) 를 참조 |NetworkTopologyStrategy는 경찰관 toounderstand hello 토폴로지의 개념을 사용합니다. GossipingPropertyFileSnitch 각 노드 toodata 중심과 랙 매핑에 효율적으로 제어를 제공 합니다. hello 클러스터는 다음 여러 toopropagate이이 정보가 사용합니다. 동적 IP 설정 상대 tooPropertyFileSnitch에 훨씬 더 간단입니다. |

**Cassandra 클러스터에 대한 Azure 고려 사항:** Microsoft Azure Virtual Machines 기능은 디스크 지속성을 위해 Azure Blob Storage를 사용합니다. Azure Storage는 높은 내구성을 위해 각 디스크의 복제본을 3개 저장합니다. 즉, Cassandra 테이블에 삽입 된 데이터의 각 행은 이미 복제본 3 개에 저장 하 고 따라서 데이터 일관성 이미 안전 하다는 1 hello 복제 비율 (RF) 하는 경우에 합니다. 복제 비율로 1 hello 큰 문제는 hello 응용 프로그램에서 작동 중단이 발생 한 단일 Cassandra 노드가 실패 한 경우에입니다. 그러나 Azure 패브릭 컨트롤러에 의해 인식 hello 문제 (예: 하드웨어, 소프트웨어 오류 시스템)에 대 한 노드가 다운 되는 경우 것은 프로 비전 사용 하 여 해당 위치에 새 노드는 동일한 저장소 드라이브 hello 합니다. 새 노드 tooreplace hello 이전 몇 분 정도 걸릴 수 있습니다 하나를 프로 비전 합니다.  마찬가지로 게스트 OS 변경 내용과 비슷한 계획 된 유지 관리 작업에 대 한 Cassandra 업그레이드 하 고 응용 프로그램을 변경 Azure 패브릭 컨트롤러 hello 클러스터에서 롤링 hello 노드의 업그레이드 수행 합니다.  Hello 클러스터 몇 가지 파티션에 대 한 짧은 가동 중지가 발생할 수 있으므로 및 롤링 업그레이드도 한 번에 몇 개 노드 아래로 걸릴 수 있습니다. 그러나 hello 데이터 toohello 기본 제공 Azure 저장소 중복 인해 손실 됩니다.  

시스템이 tooAzure 고가용성이 필요 하지 않은 배포에 대 한 (예: 99.9 약 변수인 해당 too8.76 시간/연도; 참조 [고가용성](http://en.wikipedia.org/wiki/High_availability) 대 한 자세한 내용은) 수 toorun RF 사용 될 수 있습니다 = 1 및 일관성 수준이 = 하나입니다.  응용 프로그램의 가용성 요구 사항이, RF = 3, 일관성 수준이 = 쿼럼 hello hello 복제본 중 하나 hello 노드 중 하나의 작동 중단이 허용 됩니다. RF = 1 기존 배포에서 인해 디스크 오류와 같은 문제 로부터 toohello 가능한 데이터 손실 (예: 온-프레미스)를 사용할 수 없습니다.   

## <a name="multi-region-deployment"></a>다중 지역 배포
Cassandra의 복제 데이터 센터 인식 및 일관성 모델 hello 없이 hello 초기 hello 다중 지역 배포와 함께 사용 하면 위에서 설명한 모든 외부 도구에 대 한 필요 합니다. 이것이 hello 기존의 관계형 데이터베이스와에서 크게 다르게 다중 마스터 쓰기에 대 한 데이터베이스 미러링에 대 한 hello 설치 매우 복잡할 수 있습니다. Cassandra 다중 지역 설정에 hello 다음을 비롯 한 hello 사용 시나리오에 도움이 될 수 있습니다.

**근접 기반 배포:** 테 넌 트 사용자의 명확한 매핑 사용 하 여 다중 테 넌 트 응용 프로그램-에-지역 hello 다중 지역 클러스터의 낮은 대기 시간이 있었습니다 될 수 있습니다. 예를 들어 학습 관리 교육 기관에 대 한 시스템에서 미국 동부 및 미국 서 부 지역 tooserve hello 해당 캠퍼스에 대 한 분산된 클러스터를 배포할 수 분석 뿐만 아니라 트랜잭션. hello 데이터 hello 시간 읽기 및 쓰기에 로컬로 일관 된 수 있으며 두 hello 영역 간에 결국 일치 될 수 있습니다. 미디어 배포, 전자 상거래와 같은 다른 예제는 없으며, 지역 관련 사용자 기반을 제공하는 모든 것이 이 배포 모델에 대한 좋은 사용 사례입니다.

**고가용성:** 중복성은 소프트웨어 및 하드웨어의 높은 가용성을 계산하는 핵심 요소이며 자세한 내용은 Microsoft Azure에서 신뢰할 수 있는 클라우드 시스템 구축을 참조하세요. Microsoft Azure에서 true 중복성을 얻기 위한 hello 신뢰할 수 있는 유일한 방법은 다중 지역 클러스터를 배포 하 여 것입니다. 액티브-패시브 또는 액티브-액티브 모드에서 응용 프로그램을 배포할 수 있습니다 및 hello 지역 중 한 다운 된 경우 Azure 트래픽 관리자 트래픽 toohello 활성 영역을 리디렉션할 수 있습니다.  Hello 단일 지역 배포 된 hello 가용성 99.9, 이면 두 지역 배포 일 수 99.9999 hello 수식으로 계산의 가용성: (1-(1-0.999) * (1-0.999)) * 100); 용지 대 한 자세한 내용은 위의 hello를 참조 하십시오.

**재해 복구:** 제대로 설계된 경우 다중 지역 Cassandra 클러스터는 치명적인 데이터 센터 중단을 견딜 수 있습니다. 하나의 영역 다운 되는 경우 hello 응용 프로그램을 배포 tooother 영역 hello 최종 사용자가 처리를 시작할 수 있습니다. 모든 다른 비즈니스 연속성 구현에서는 같은 hello 응용 프로그램 toobe hello 비동기 파이프라인의 hello 데이터에서 일부 데이터가 손실에 대 한 내결함성에 있습니다. 그러나 Cassandra는 hello 복구 일반 데이터베이스 복구 프로세스에서 사용한 hello 시간 보다 훨씬 swifter. 그림 2는 각 지역에 8 개 노드가 포함 된 hello 일반적인 다중 지역 배포 모델을 보여줍니다. 두 영역은 hello에 대 한 서로의 미러 이미지 대칭; 동일한 실제 디자인 hello 작업 유형 (트랜잭션 또는 분석 예:), RPO, RTO, 데이터 일관성 및 가용성 요구 사항에 따라 다릅니다.

![다중 지역 배포](./media/cassandra-nodejs/cassandra-linux2.png)

그림 2: 다중 지역 Cassandra 배포

### <a name="network-integration"></a>네트워크 통합
VPN 터널을 사용 하 여 서로 통신 하는 두 지역에 있는 배포 된 tooprivate 네트워크는 가상 컴퓨터의 설정 합니다. hello VPN 터널 hello 네트워크 배포 프로세스 중 사용자를 프로 비전 하는 두 개의 소프트웨어 게이트웨이 연결 합니다. 두 지역에 "웹" 및 "데이터" 서브넷; 측면에서 비슷한 네트워크 아키텍처 Azure 네트워킹 hello 필요에 따라 많은 서브넷 만들기를 허용 하 고 네트워크 보안이 필요에 따라 Acl을 적용 합니다. Hello 클러스터 토폴로지를 디자인 하는 동안 간 데이터 센터 통신 대기 시간 및 hello 경제의 영향 hello 네트워크 트래픽이 필요 toobe 것으로 간주 합니다.

### <a name="data-consistency-for-multi-data-center-deployment"></a>다중 데이터 센터 배포에 대한 데이터 일관성
배포 요구 toobe 처리량 및 가용성에 대 한 hello 클러스터 토폴로지 영향 인식 배포 됩니다. hello RF 및 일관성 수준이 필요 toobe 쿼럼 hello 방식에서 선택한 모든 hello 데이터 센터의 hello 가용성에 종속 되지 않습니다.
일관성 수준 (에 대 한 읽기 및 쓰기) 하면 해당 hello 로컬에 대 한 높은 일관성을는 LOCAL_QUORUM를 필요로 하는 시스템 읽기 및 쓰기 hello 로컬에서 충족 하는 노드 데이터는 비동기적으로 toohello 원격 데이터 센터 복제 합니다.  표 2 hello의 뒷부분에서 설명 하는 hello 다중 지역 클러스터에 대 한 세부 정보를 작성 하는 hello 구성 요약 되어 있습니다.

**두 지역 Cassandra 클러스터 구성**

| 클러스터 매개 변수 | 값 | 설명 |
| --- | --- | --- |
| 노드 수(N) |8 + 8 |총 hello 클러스터의 노드 수 |
| 복제 계수(RF) |3 |지정된 행의 복제본 수 |
| 일관성 수준(쓰기) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] hello 수식의 hello 결과 내림 |노드 2 개 쓸 toohello 첫 번째 데이터 센터 hello 추가 2 노드 쿼럼에 필요한 쓸 비동기적으로 toohello 보조 데이터 센터입니다. |
| 일관성 수준(읽기) |LOCAL_QUORUM ((RF/2) + 1) = 2 hello 수식의 hello 결과 내림 |하나의 영역;에서 읽기 요청을 충족 시킬 노드 2 개 hello 응답 백 toohello 클라이언트를 전송 하기 전에 읽습니다. |
| 복제 전략 |NetworkTopologyStrategy자세한 내용은 Cassandra 설명서의 [데이터 복제](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) 참조 |Hello 배포 토폴로지를 이해 하 고 모든 hello 복제 하지 않는에서 중단 될 hello 동일한 복제본 노드에 배치 랙 |
| Snitch |GossipingPropertyFileSnitch 자세한 내용은 Cassandra 설명서의 [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) 를 참조 |NetworkTopologyStrategy는 경찰관 toounderstand hello 토폴로지의 개념을 사용합니다. GossipingPropertyFileSnitch 각 노드 toodata 중심과 랙 매핑에 효율적으로 제어를 제공 합니다. hello 클러스터는 다음 여러 toopropagate이이 정보가 사용합니다. 동적 IP 설정 상대 tooPropertyFileSnitch에 훨씬 더 간단입니다. |

## <a name="hello-software-configuration"></a>hello 소프트웨어 구성
다음 소프트웨어 버전 hello hello 배포 하는 동안 사용 됩니다.

<table>
<tr><th>소프트웨어</th><th>원본</th><th>버전</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

이후 Oracle 라이선스, toosimplify hello 배포, 다운로드를 수행 하려면 먼저 toohello 클러스터 만드는데 hello Ubuntu 템플릿 이미지를 나중에 업로드 하기 위한 필수 소프트웨어 toohello 데스크톱 hello 모든 수동 승인의 JRE 다운로드. 배포 합니다.

Hello 로컬 컴퓨터에 다운로드 잘 알려진 디렉터리 (예: Windows에서 %TEMP%/downloads 또는 대부분의 Linux 배포판 또는 Mac에서 ~/Downloads)에 소프트웨어 위에 hello를 다운로드 합니다.

### <a name="create-ubuntu-vm"></a>UBUNTU VM 만들기
Hello 프로세스의이 단계에서를 만듭니다 Ubuntu 이미지 hello 필수 구성 요소 소프트웨어와 함께 hello 이미지 재사용 몇 개의 Cassandra 노드를 프로 비전에 있도록.  

#### <a name="step-1-generate-ssh-key-pair"></a>1단계: SSH 키 쌍 생성
Azure는 DER 또는 PEM 공개 키 시간을 프로 비전 하는 hello로 인코딩된 X509 필요 합니다. 방법에 있는 hello 지침을 사용 하 여 공개/개인 키 쌍을 생성 된 Azure에서 Linux에 SSH tooUse 합니다. Toouse putty.exe Windows 또는 Linux에 SSH 클라이언트를 계획 해야 tooconvert hello PEM 인코딩된 puttygen.exe;를 사용 하 여 RSA 개인 키 tooPPK 형식 이 대 한 hello 지침 hello 웹 페이지의 위쪽에 있습니다.

#### <a name="step-2-create-ubuntu-template-vm"></a>2단계: Ubuntu 템플릿 VM 만들기
toocreate hello 템플릿, VM에 로그인 할 hello 순서에 따라 Azure 클래식 포털을 사용 하 여 hello: 새로 만들기, 계산, 가상 컴퓨터, 갤러리, UBUNTU, Ubuntu Server 14.04 LTS를 클릭 한 다음 hello 오른쪽 화살표를 클릭 합니다. Linux VM을 확인 하는 toocreate 방법에 대해 설명 하는 자습서는 Linux 가상 컴퓨터 실행을 만듭니다.

Hello #1 "가상 컴퓨터 구성" hello 화면에 다음 정보를 입력 합니다.

<table>
<tr><th>필드 이름              </td><td>       필드 값               </td><td>         설명                </td><tr>
<tr><td>버전 릴리스 날짜    </td><td> Hello 드롭다운 목록에서 날짜 선택</td><td></td><tr>
<tr><td>가상 컴퓨터 이름    </td><td> cass-template                   </td><td> 이 hello VM의 hello 호스트 이름 </td><tr>
<tr><td>계층                     </td><td> 표준                           </td><td> Hello 기본값을 사용              </td><tr>
<tr><td>크기                     </td><td> A1                              </td><td>Hello IO 기준으로 VM 선택 hello 요구를 이 목적 hello 기본값을 그대로 둡니다. </td><tr>
<tr><td> 새 사용자 이름             </td><td> localadmin                       </td><td> "admin"은 Ubuntu 12.xx 이상에서 예약된 사용자 이름입니다.</td><tr>
<tr><td> 인증         </td><td> 확인란을 클릭합니다.                 </td><td>SSH 키를 가진 toosecure 원하면 선택 </td><tr>
<tr><td> 인증서             </td><td> hello 공개 키 인증서의 파일 이름 </td><td> 이전에 생성 된 hello 공개 키를 사용 하 여</td><tr>
<tr><td> 새 암호    </td><td> 강력한 암호 </td><td> </td><tr>
<tr><td> 암호 확인    </td><td> 강력한 암호 </td><td></td><tr>
</table>

Hello "가상 컴퓨터 구성" hello 화면 # 2에서 다음 정보를 입력 합니다.

<table>
<tr><th>필드 이름             </th><th> 필드 값                       </th><th> 설명                                 </th></tr>
<tr><td> 클라우드 서비스    </td><td> 새 클라우드 서비스 만들기    </td><td>클라우드 서비스는 가상 컴퓨터와 같은 계산 리소스의 컨테이너입니다.</td></tr>
<tr><td> 클라우드 서비스 DNS 이름    </td><td>ubuntu-template.cloudapp.net    </td><td>컴퓨터에 알 수 없는 부하 분산 장치 이름을 지정합니다.</td></tr>
<tr><td> 지역/선호도 그룹/가상 네트워크 </td><td>    미국 서부    </td><td> 웹 응용 프로그램 올 hello Cassandra 클러스터에 액세스 한 지역을 선택합니다</td></tr>
<tr><td>저장소 계정 </td><td>    기본값 사용    </td><td>사용 하 여 hello 기본 저장소 계정 또는 특정 지역에서 미리 생성된 된 저장소 계정</td></tr>
<tr><td>가용성 집합 </td><td>    없음 </td><td>    비워 둡니다.</td></tr>
<tr><td>끝점    </td><td>기본값 사용 </td><td>    Hello 기본 SSH 구성 사용 </td></tr>
</table>

오른쪽 화살표를 클릭 하 고 hello 화면 # 3에서 hello 기본값을 그대로 두고 hello "확인" 단추 toocomplete hello VM 프로 비전 프로세스를 클릭 합니다. 몇 분 후 VM 템플릿을 사용 하 여 hello 이름"ubuntu-" hello "실행 중" 상태에 있어야 합니다.

### <a name="install-hello-necessary-software"></a>Hello 필요한 소프트웨어를 설치 합니다.
#### <a name="step-1-upload-tarballs"></a>1단계: tarball 업로드
Scp 또는 pscp를 사용 하 여 복사 hello 이전에 다운로드 한 소프트웨어 너무 ~ 다운로드 디렉터리 명령 형식에 따라 hello를 사용 하 여:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Hello Cassandra 비트의 경우와 명령 위에 hello JRE도 반복 합니다.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>2 단계: hello 디렉터리 구조를 준비 하 고 hello 아카이브를 추출 합니다.
VM hello를 로그인 하 고 hello 디렉터리 구조를 만드는 하 고 소프트웨어 아래의 hello bash 스크립트를 사용 하는 슈퍼 사용자로 추출:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Vim 창에이 스크립트를 붙여 확인 되었는지 tooremove hello 캐리지 반환 ('\r ") hello 다음 명령을 사용 하 여:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>3단계: etc/profile 편집
Hello 다음 hello 끝에 추가 합니다.

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>4단계: 프로덕션 시스템용 JNA 설치
사용 하 여 hello 다음 시퀀스 명령은: hello 다음 명령은 설치 jna 3.2.7.jar 및 jna-플랫폼-3.2.7.jar too/usr/share.java 디렉터리 sudo apt-get libjna-java 설치 합니다

Cassandra 시작 스크립트에서 이러한 jar을 찾을 수 있도록 $CASS_HOME/lib 디렉터리에 바로 가기 링크를 만듭니다.

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>5단계: cassandra.yaml 구성
[우리는 조정이 hello 실제 프로 비전 하는 동안] 모든 hello 가상 컴퓨터에 필요한 각 VM tooreflect 구성에서 cassandra.yaml를 편집 합니다.

<table>
<tr><th>필드 이름   </th><th> 값  </th><th>    설명 </th></tr>
<tr><td>cluster_name </td><td>    "CustomerService"    </td><td> 배포를 반영 하는 hello 이름 사용</td></tr>
<tr><td>listen_address    </td><td>[비워 둠]    </td><td> "localhost"를 삭제합니다. </td></tr>
<tr><td>rpc_addres   </td><td>[비워 둠]    </td><td> "localhost"를 삭제합니다. </td></tr>
<tr><td>seeds    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>초기값으로 지정 된 모든 hello IP 주소 목록입니다.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> 이 사용 됩니다 hello NetworkTopologyStrateg 유추 hello 데이터 센터 및 hello VM의 hello 랙</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>6 단계: hello VM 이미지 캡처
Hello 호스트 이름 (hk cas template.cloudapp.net) 및 이전에 만든 hello SSH 개인 키를 사용 하 여 hello 가상 컴퓨터에 로그인 합니다. 참조 방식을 사용 하 여 toolog hello 명령 ssh 또는 putty.exe tooUse SSH에 대 한 Azure에서 Linux와 함께 자세히 설명 하는 방법입니다.

Hello toocapture hello 이미지 작업의 시퀀스를 따라를 실행 합니다.

##### <a name="1-deprovision"></a>1. 프로비전 해제
Hello 명령을 사용 하 여 "sudo waagent-deprovision + 사용자" tooremove 가상 컴퓨터 인스턴스 관련 정보입니다. 에 대 한 참조 [어떻게 tooCapture Linux 가상 컴퓨터를](capture-image.md) 템플릿으로 tooUse hello 이미지 캡처 프로세스에서 더 자세히 설명 합니다.

##### <a name="2-shutdown-hello-vm"></a>2: 종료 hello VM
Hello 가상 컴퓨터 선택 되었는지 확인 하 고 hello 맨 아래 명령 모음에서 hello 종료 링크를 클릭 합니다.

##### <a name="3-capture-hello-image"></a>3: hello 이미지 캡처
Hello 가상 컴퓨터 선택 되었는지 확인 하 고 hello 맨 아래 명령 모음에서 hello 캡처 링크를 클릭 합니다. Hello 다음 화면 (예: hk-cas-2-08-ub-14-04-2014071) 이미지 이름을 지정 하 고 이미지 설명 적절 한 hello "검사" 표시 toofinish hello 캡처 프로세스를 클릭 합니다.

몇 초 정도 걸립니다 및 hello 이미지 hello 이미지 갤러리의 이미지 내 이미지 섹션에서 사용할 수 있어야 합니다. hello 이미지는 성공적으로 캡처되면 hello 원본 VM을 자동으로 삭제 됩니다. 

## <a name="single-region-deployment-process"></a>단일 지역 배포 프로세스
**1 단계: hello 가상 네트워크 만들기** Azure 포털 hello에 로그인 하 고 가상 네트워크 만들기 (클래식) hello 특성으로 다음 표에 hello에 표시 된 것입니다. 참조 [hello Azure 포털을 사용 하 여 가상 네트워크 (클래식) 만들기](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello 프로세스의 자세한 단계입니다.      

<table>
<tr><th>VM 특성 이름</th><th>값</th><th>설명</th></tr>
<tr><td>이름</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>지역</td><td>미국 서부</td><td></td></tr>
<tr><td>DNS 서버</td><td>없음</td><td>DNS 서버를 사용하지 않으므로 이 특성을 무시합니다.</td></tr>
<tr><td>주소 공간</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>시작 IP</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Hello 다음 서브넷을 추가 합니다.

<table>
<tr><th>이름</th><th>시작 IP</th><th>CIDR</th><th>설명</th></tr>
<tr><td>web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Hello 웹 팜에 대 한 서브넷</td></tr>
<tr><td>데이터</td><td>10.1.2.0</td><td>/24 (251)</td><td>데이터베이스 노드 hello에 대 한 서브넷</td></tr>
</table>

데이터 및 웹 서브넷 보호할 수 있습니다 네트워크 보안 그룹을 통해 hello 검사는이 문서에 대 한 범위를 벗어났습니다.  

**가상 컴퓨터를 프로 비전 하는 2 단계:** 이전에 만든 hello 이미지를 사용 하 여 hello 클라우드의 가상 컴퓨터를 다음 hello 서버 "hk-c-svc-서" 만들어져 아래와 같이 toohello 해당 하는 서브넷 바인딩합니다.

<table>
<tr><th>컴퓨터 이름    </th><th>서브넷    </th><th>IP 주소    </th><th>가용성 집합</th><th>DC/랙</th><th>시드 여부</th></tr>
<tr><td>hk-c1-west-us    </td><td>데이터    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1 </td><td>예</td></tr>
<tr><td>hk-c2-west-us    </td><td>데이터    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1    </td><td>아니요 </td></tr>
<tr><td>hk-c3-west-us    </td><td>데이터    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>예</td></tr>
<tr><td>hk-c4-west-us    </td><td>데이터    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>아니요 </td></tr>
<tr><td>hk-c5-west-us    </td><td>데이터    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>예</td></tr>
<tr><td>hk-c6-west-us    </td><td>데이터    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>아니요 </td></tr>
<tr><td>hk-c7-west-us    </td><td>데이터    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>예</td></tr>
<tr><td>hk-c8-west-us    </td><td>데이터    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>아니요 </td></tr>
<tr><td>hk-w1-west-us    </td><td>web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>해당 없음</td></tr>
<tr><td>hk-w2-west-us    </td><td>web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>해당 없음</td></tr>
</table>

Vm의 목록 위의 hello 만들기 프로세스를 수행 하는 hello이 필요 합니다.

1. 특정 지역에 빈 클라우드 서비스를 만듭니다.
2. Hello 이전에 캡처된 이미지에서 VM을 만들고; 이전에 만든 toohello 가상 네트워크 연결 모든 hello Vm에 대해이 단계를 반복합니다
3. 내부 부하 분산 장치 toohello 클라우드 서비스를 추가 하 고 "데이터" toohello 서브넷 연결
4. 이전에 만든 각 VM에 대 한 부하 분산 된 집합을 연결 된 이전에 만든 toohello 내부 부하 분산 장치를 통해 thrift 트래픽에 대 한 부하 분산 된 끝점 추가

Azure 클래식 포털;를 사용 하 여 hello 위의 프로세스를 실행할 수 있습니다. Windows 컴퓨터 (액세스 tooa Windows 컴퓨터에 없는 경우 Azure에서 VM 사용)를 사용 하 여 자동으로 다음 PowerShell 스크립트 tooprovision hello 8 모든 Vm을 사용 합니다.

**목록 1: 가상 컴퓨터 프로비전을 위한 PowerShell 스크립트**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**3단계: 각 VM에서 Cassandra 구성**

Hello VM에 로그인 한를 hello 다음을 수행 합니다.

* $CASS_HOME/conf/cassandra-rackdc.properties는 toospecify hello 데이터 센터와 랙 속성을 편집 합니다.
  
       dc =EASTUS, rack =rack1
* 아래와 같이 cassandra.yaml tooconfigure 시드 노드를 편집 합니다.
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**4 단계: hello Vm을 시작 하 고 hello 클러스터 테스트**

(예: 홍콩-c1-서쪽-us) hello 노드 중 하나에 로그인 실행된 hello hello 클러스터의 명령 toosee hello 상태에 따라:

       nodetool –h 10.1.2.4 –p 7199 status

Hello 디스플레이 비슷한 toohello 하나 아래의 8 개 노드 클러스터에 대 한 표시 되어야 합니다.

<table>
<tr><th>가동 상태</th><th>주소    </th><th>로드    </th><th>토큰    </th><th>소유 비율 </th><th>호스트 ID    </th><th>랙</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38.0%    </td><td>Guid(제거됨)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>Guid(제거됨)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid(제거됨)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid(제거됨)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid(제거됨)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid(제거됨)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid(제거됨)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid(제거됨)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>테스트 hello 단일 지역 클러스터
다음 단계 tootest hello 클러스터 hello를 사용 합니다.

1. Hello Powershell 명령 가져오기 AzureInternalLoadbalancer commandlet을 사용 (예: hello 내부 부하 분산 장치의 IP 주소 hello 가져올  10.1.2.101)입니다. hello 명령의 hello 구문은 다음과 같습니다: AzureLoadbalancer Get-ServiceName "hk-c-svc-서쪽-us" [hello 내부 부하 분산 장치 IP 주소와 함께 hello 세부 정보가 표시 됩니다.]
2. Hello 웹 팜 (예: 홍콩-w1-서쪽-us) VM에 로그인 Putty를 사용 하 여 또는 ssh
3. $CASS_HOME/bin/cqlsh 10.1.2.101 9160을 실행합니다.
4. Hello CQL 명령을 tooverify hello 클러스터가 작동 하는 경우 다음을 사용 합니다.
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');
   
     SELECT * FROM Customers;

Hello 하나 아래와 같은 표시를 나타나야 합니다.

<table>
  <tr><th> customer_id </th><th> firstname </th><th> Lastname </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Jane </td><td> Doe </td></tr>
</table>

4 단계에서 만든 해당 hello 키 스페이스 SimpleStrategy를 사용 하 여 3 replication_factor와 note 하십시오. SimpleStrategy는 단일 데이터 세터 배포에 권장되고 NetworkTopologyStrategy는 다중 데이터 세터 배포에 권장됩니다. replication_factor가 3이면 노드 오류에 대한 내결함성이 제공됩니다.

## <a id="tworegion"> </a>다중 지역 배포 프로세스
완료 하는 hello 단일 지역 배포를 활용 하 고 hello 두 번째 영역을 설치 하기 위한 hello 동일한 프로세스를 반복 합니다. hello 주요한 차이점 hello 단일 및 다중 지역 배포는 지역 간 통신용; hello VPN 터널 설정 hello 네트워크를 통해 설치를 시작, hello Vm을 프로 비전 하 고 Cassandra를 구성 합니다.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>1 단계: hello에 hello 가상 네트워크 만들기 2 일 영역
Azure 클래식 포털 hello를 로그인 하 고 hello 표에 hello 특성 표시 된 가상 네트워크를 만듭니다. 참조 [hello Azure 클래식 포털에서에서 클라우드 전용 가상 네트워크 구성](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello 프로세스의 자세한 단계입니다.      

<table>
<tr><th>특성 이름    </th><th>값    </th><th>설명</th></tr>
<tr><td>Name    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>지역    </td><td>미국 동부</td><td></td></tr>
<tr><td>DNS 서버        </td><td></td><td>DNS 서버를 사용하지 않으므로 이 특성을 무시합니다.</td></tr>
<tr><td>지점 및 사이트 간 VPN 구성</td><td></td><td>        이 특성을 무시합니다.</td></tr>
<tr><td>사이트 간 VPN 구성</td><td></td><td>        이 특성을 무시합니다.</td></tr>
<tr><td>주소 공간    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>시작 IP    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Hello 다음 서브넷을 추가 합니다.

<table>
<tr><th>이름    </th><th>시작 IP    </th><th>CIDR    </th><th>설명</th></tr>
<tr><td>web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Hello 웹 팜에 대 한 서브넷</td></tr>
<tr><td>데이터    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>데이터베이스 노드 hello에 대 한 서브넷</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>2단계: 로컬 네트워크 만들기
Azure 가상 네트워킹에는 로컬 네트워크는 사설 클라우드 또는 다른 Azure 영역을 포함 하 여 tooa 원격 사이트에 매핑되는 프록시 주소 공간입니다. 이 프록시 주소 공간은 라우팅 네트워크 toohello 오른쪽 대상 네트워킹에 대 한 원격 게이트웨이 바인딩된 tooa입니다. 참조 [VNet tooVNet 연결 구성](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) hello에 대 한 지침은 VNET 대 VNET 연결을 설정 합니다.

다음 세부 정보는 hello 당 두 개의 로컬 네트워크를 만듭니다.

| 네트워크 이름 | VPN 게이트웨이 주소 | 주소 공간 | 설명 |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |Hello 로컬 네트워크를 만드는 동안 자리 표시자 게이트웨이 주소를 제공 합니다. hello 실제 게이트웨이 주소는 hello 게이트웨이가 생성 된 후에 채워집니다. Hello는 주소 공간 있는지와 정확히 일치 hello 해당 원격 VNET; 이 경우 hello VNET에서에서 만든 hello 미국 동부 지역입니다. |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |Hello 로컬 네트워크를 만드는 동안 자리 표시자 게이트웨이 주소를 제공 합니다. hello 실제 게이트웨이 주소는 hello 게이트웨이가 생성 된 후에 채워집니다. Hello는 주소 공간 있는지와 정확히 일치 hello 해당 원격 VNET; 이 경우 hello VNET에서에서 만든 hello 미국 서 부 지역입니다. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>3 단계: 맵 "Local" 네트워크 toohello 각 Vnet
Hello Azure 클래식 포털에서에서 각 vnet 선택를 클릭 "구성", "Connect toohello 로컬 네트워크" 확인 하 고 다음 세부 정보는 hello 당 hello 로컬 네트워크:

| 가상 네트워크 | 로컬 네트워크 |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>4단계: VNET1 및 VNET2에 게이트웨이 만들기
두 hello 가상 네트워크의 hello 대시보드에서 hello VPN 게이트웨이 프로 비전 프로세스 트리거되고 게이트웨이 만들기를 클릭 합니다. 잠시 후에는 각 가상 네트워크의 대시보드 hello 후 hello 실제 게이트웨이 주소가 표시 되어야 합니다.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Hello 각각 "게이트웨이" 주소와 5 단계: 업데이트 "Local" 네트워크
두 hello 로컬 네트워크 tooreplace hello 자리 표시자 게이트웨이 IP 주소 프로 비전의 정당한 hello hello 실제 IP 주소와 게이트웨이 편집 합니다. 다음 매핑 hello를 사용 합니다.

<table>
<tr><th>로컬 네트워크    </th><th>가상 네트워크 게이트웨이</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>hk-vnet-west-us의 게이트웨이</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>hk-vnet-east-us의 게이트웨이</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>6 단계: hello 공유 키를 업데이트 합니다.
다음 Powershell 스크립트 tooupdate hello IPSec 키 [모두 hello 게이트웨이에 사용 하 여 hello 찾았 키] 각 VPN 게이트웨이의 사용 하 여 hello: 집합 AzureVNetGatewayKey VNetName hk-vnet-동부-미국-LocalNetworkSiteName hk-lnet-map-to-west-us-에서 SharedKey D9E76BKK 집합 AzureVNetGatewayKey-VNetName hk-vnet-서쪽-미국-LocalNetworkSiteName hk-lnet-map-to-east-us-에서 SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>7 단계: hello VNET 대 VNET 연결 설정
Hello Azure 클래식 포털에서에서 모두 hello tooestablish 가상 네트워크 게이트웨이 투 게이트웨이 연결의 "대시보드" 메뉴 hello를 사용 합니다. Hello 아래쪽 도구 모음에서 hello "연결" 메뉴 항목을 사용 합니다. 몇 분 후 hello 대시보드에서 hello 연결 세부 정보를 그래픽으로 표시 되어야 합니다.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>8 단계: 영역 # 2에에서 hello 가상 컴퓨터 만들기
다음 hello 단계 같거나 hello 이미지 VHD 파일 toohello Azure 저장소 계정이 지역 # 2에 복사 하 여 지역 #1 배포에 설명 된 대로 hello Ubuntu 이미지를 만들고 hello 이미지를 만듭니다. 이 이미지를 사용 하 고 hello hk-c-svc-동부-us를 새 클라우드 서비스에 가상 컴퓨터의 목록을 다음을 만듭니다.

| 컴퓨터 이름 | 서브넷 | IP 주소 | 가용성 집합 | DC/랙 | 시드 여부 |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |데이터 |10.2.2.4 |hk-c-aset-1 |dc =EASTUS rack =rack1 |예 |
| hk-c2-east-us |데이터 |10.2.2.5 |hk-c-aset-1 |dc =EASTUS rack =rack1 |아니요 |
| hk-c3-east-us |데이터 |10.2.2.6 |hk-c-aset-1 |dc =EASTUS rack =rack2 |예 |
| hk-c5-east-us |데이터 |10.2.2.8 |hk-c-aset-2 |dc =EASTUS rack =rack3 |예 |
| hk-c6-east-us |데이터 |10.2.2.9 |hk-c-aset-2 |dc =EASTUS rack =rack3 |아니요 |
| hk-c7-east-us |데이터 |10.2.2.10 |hk-c-aset-2 |dc =EASTUS rack =rack4 |예 |
| hk-c8-east-us |데이터 |10.2.2.11 |hk-c-aset-2 |dc =EASTUS rack =rack4 |아니요 |
| hk-w1-east-us |web |10.2.1.4 |hk-w-aset-1 |해당 없음 |해당 없음 |
| hk-w2-east-us |web |10.2.1.5 |hk-w-aset-1 |해당 없음 |해당 없음 |

다음과 같은 hello 지역 #1 지침 하지만 10.2.xxx.xxx 주소 공간을 사용 합니다.

### <a name="step-9-configure-cassandra-on-each-vm"></a>9단계: 각 VM에서 Cassandra 구성
Hello VM에 로그인 한를 hello 다음을 수행 합니다.

1. 속성을 편집 $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello 데이터 센터와 랙 hello 형태로 표시: dc = EASTUS 랙 rack1 =
2. Cassandra.yaml tooconfigure 시드 노드를 편집: 초기값: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>10단계: Cassandra 시작
각 VM에 로그인 하 고 hello 다음 명령을 실행 하 여 Cassandra hello 백그라운드에서 시작: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>테스트 hello 다중 지역 클러스터
지금까지 Cassandra 각 Azure 영역의 8 개의 노드로 구성 된 배포 된 too16 노드 되었습니다. 이러한 노드는 hello 일반 클러스터 이름 및 hello 시드 노드 구성으로 인해 클러스터 동일 hello입니다. 다음 프로세스 tootest hello 클러스터 hello를 사용 합니다.

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>1 단계: PowerShell을 사용 하 여 두 hello 영역에 대 한 hello 내부 부하 분산 장치 IP 가져오기
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-west-us"
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-east-us"  
  
    Hello IP 주소를 기록해 둡니다 (예:-10.1.2.101, 동-서 10.2.2.101) 표시 합니다.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>2 단계: hello 서 부 지역에 hello 다음 hk-w1-서쪽-미국에 로그인 한 후 실행
1. $CASS_HOME/bin/cqlsh 10.1.2.101 9160을 실행합니다.
2. Hello 다음 CQL 명령을 실행 합니다.
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { 'class' : 'NetworkToplogyStrategy', 'WESTUS' : 3, 'EASTUS' : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Hello 하나 아래와 같은 표시를 나타나야 합니다.

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>3 단계 hello 동부 지역 hello 다음 hk-w1-동부-미국에 로그인 한 후 실행 합니다.:
1. $CASS_HOME/bin/cqlsh 10.2.2.101 9160 실행
2. Hello 다음 CQL 명령을 실행 합니다.
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Hello 서 부 지역에 대해 표시 되는 디스플레이 동일 hello를 표시 되어야 합니다.

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

몇 가지 더 많은 삽입을 실행 하 고 복제 된 toowest를 구하십시오 것-hello 클러스터의 일부로 주세요.

## <a name="test-cassandra-cluster-from-nodejs"></a>Node.js에서 Cassandra 클러스터 테스트
Hello "웹" 계층에서 이전에 만든 hello Linux Vm 중 하나를 사용 하 여, 이전 실행될지 간단한 Node.js 스크립트 tooread hello 앞서 삽입 한 데이터

**1단계: Node.js 및 Cassandra 클라이언트 설치**

1. Node.js 및 npm을 설치합니다.
2. npm을 사용하여 노드 패키지 "cassandra-client"를 설치합니다.
3. Hello 스크립트 hello 검색 데이터의 json 문자열 hello를 표시 하는 hello 셸 프롬프트에서 다음을 실행 합니다.
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>결론
Microsoft Azure는이 연습에서 설명으로 Microsoft 오픈 소스 소프트웨어 hello 실행 수 있도록 허용 하는 유동적인 플랫폼입니다. 항상 사용 가능한 Cassandra 클러스터 hello를 분배 hello 클러스터 노드의 여러 오류 도메인을 통해 단일 데이터 센터에 배포할 수 있습니다. 재해 증명 시스템을 위해 지역적으로 떨어진 여러 Azure 지역에 Cassandra 클러스터를 배포할 수도 있습니다. Azure와 함께 사용 하면 Cassandra hello 확장성이 높은, 항상 사용 가능한의 생성 및 재해 복구 가능한 클라우드 서비스 필요한 현재의 인터넷에서 서비스를 크기입니다.  

## <a name="references"></a>참조
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

