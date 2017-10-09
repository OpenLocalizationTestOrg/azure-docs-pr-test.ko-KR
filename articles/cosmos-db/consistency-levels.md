---
title: "Azure Cosmos DB에서 aaaConsistency 수준 | Microsoft Docs"
description: "Azure Cosmos DB에 5 개의 일관성 수준 toohelp 균형 결과적 일관성, 가용성 및 대기 시간 장단점이 있습니다."
keywords: "최종 일관성, azure cosmos db, azure, Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Azure Cosmos DB의 튜닝 가능한 데이터 일관성 수준
모든 데이터 모델에 대해 염두 글로벌 배포 접지 hello에서 azure Cosmos DB 설계 되었습니다. 디자인 된 toooffer 짧은 대기 시간을 예측 가능한 기능을 보장 함으로써 99.99% 가용성 SLA 이며 잘 정의 된 여러 완화 일관성 모델입니다. 현재 Azure Cosmos DB는 5가지 일관성 수준(강력, 제한된 부실, 세션, 일관적인 접두사 및 최종)을 제공합니다. 

Azure Cosmos DB는 분산된 데이터베이스에서 흔히 제공하는 **강력**하고 **최종 일관성**있는 모델 외에도 신중하게 변환된 조작 가능한 3가지 일관성 모델을 제공하며 실제 사용 사례에서도 유용하다는 것이 입증되었습니다. 이 hello **부실 제한**, **세션**, 및 **일관 된 접두사** 일관성 수준입니다. 전체적으로 이러한 5 개 일관성 수준을 사용 하면 toomake 잘 내용된 간의 장단점 일관성, 가용성 및 대기 시간입니다. 

## <a name="distributed-databases-and-consistency"></a>분산된 데이터베이스 및 일관성
상업적으로 분산된 데이터베이스는 입증 가능한 잘 정의된 일관성 선택 사항을 전혀 제공하지 않는 데이터베이스와, 두 가지 극단적인 프로그래밍 가능성 선택을 제공하는 데이터베이스(강력한 일관성, 결과적 일관성) 등의 두 가지 범주에 해당합니다. 

이전 부담 응용 프로그램 개발자가 복제 프로토콜의 세부 사항을 구현 하는 hello 및 일관성, 가용성, 대기 시간 및 처리량 사이의 toomake 어려운 균형에서 예상 하 합니다. 후자의 hello hello 두 가지 극단적인 예측 중 하나는 압력 toochoose를 넣습니다. Hello 다양 한 연구 및 50 개 이상의 일관성 모델에 대 한 제안, 불구 하 고 hello 분산된 데이터베이스 커뮤니티가 않았습니다 초과 강력 하 고 결과적 일관성 수 toocommercialize 일관성 수준. Cosmos DB를 사용 하면 개발자 toochoose hello 일관성 스펙트럼 – 강력한 함께 5 개의 잘 정의 된 일관성 모델 간의 제한 부실, [세션](http://dl.acm.org/citation.cfm?id=383631), 일관 된 접두사 및 최종 합니다. 

![(상대적으로 느) 일관성 모델 toochoose에서 정의 된 여러 azure Cosmos DB 제공](./media/consistency-levels/five-consistency-levels.png)

다음 표에서 hello 각 일관성 수준에서 제공 하는 hello 특정 보증을 보여 줍니다.
 
**일관성 수준 및 보증**

| 일관성 수준 | 보증 |
| --- | --- |
| 강력 | 선형화 가능성 |
| 제한된 부실 | 일관적인 접두사 k 접두사 또는 t 간격을 통해 쓰기 뒤 읽기 지연 |
| 세션   | 일관적인 접두사 단조 읽기, 단조 쓰기, 쓰기 읽기, 읽기 뒤 쓰기 |
| 일관적인 접두사 | 반환 된 업데이트는 간격 없이 모든 hello 업데이트의 일부 접두사 |
| 최종  | 순서 외 읽기 |

Hello 기본 일관성 수준이 Cosmos DB 계정에 (을 구성한 나중에 특정 읽기 요청에서 hello 일관성을 재정의). 내부적으로 hello 기본 일관성 수준이 toodata 지역으로 확장 될 수 있는 hello 파티션 집합 내에서 적용 됩니다. 테넌트의 약 73%는 세션 일관성을 사용하고 20%는 제한된 부실을 선호합니다. 고객의 약 3%는 처음에 다양한 일관성 수준을 실험한 후 응용 프로그램에 맞는 특정 일관성을 선택하는 것으로 확인되었습니다. 또한 테넌트의 2%만이 요청에 따라 일관성 수준을 재정의하는 것으로 확인되었습니다. 

Cosmos DB에서 세션, 일관적인 접두사 및 최종 일관성에서의 읽기는 강력 또는 제한된 부실 일관성에서의 읽기보다 2배 저렴합니다. Cosmos DB는 가용성, 처리량 및 대기 시간과 함께 일관성 보장을 포함하여 업계 최고 수준의 포괄적인 99.99% SLA를 제공합니다. 채택는 [linearizability 검사기](http://dl.acm.org/citation.cfm?id=1806634), 우리의 서비스 원격 분석에 대해 지속적으로 작동 하 고 공개적으로 모든 일관성 위반 tooyou를 보고 합니다. 에 대 한 부실, 모니터링 및 보고에서 위반 된 걸린 것, t 범위를 제한 합니다. 모든 5 개의 상대적으로 느 일관성 수준에 대해도 hello를 보고할 [확률적 bounded 부실 메트릭을](http://dl.acm.org/citation.cfm?id=2212359) 직접 tooyou 합니다.  

## <a name="scope-of-consistency"></a>일관성 범위
일관성의 hello 세분성은 범위 지정 된 tooa 단일 사용자 요청입니다. 쓰기 요청을 tooan insert, replace, upsert, 해당 또는 트랜잭션이 삭제 될 수 있습니다. 쓰기와 마찬가지로 읽기/쿼리 트랜잭션 범위가 지정 된 tooa 단일 사용자 요청도입니다. 결과 집합, 여러 개의 파티션이 스패닝 hello 사용자 큰를 통해 필요한 toopaginate 있을 수 있지만 각 읽기 트랜잭션 범위가 지정 된 tooa 단일 페이지가 고은 단일 파티션 내에서 제공.

## <a name="consistency-levels"></a>일관성 수준
Cosmos DB 계정으로 기본 일관성 수준이 tooall 컬렉션 (또는 데이터베이스)에 적용 되는 데이터베이스 계정에 구성할 수 있습니다. 기본적으로 모든 읽기 및 실행 hello에 대 한 쿼리가 사용자 정의 리소스 hello 기본 일관성 수준이 데이터베이스 계정 hello에 명시 된를 사용 합니다. 특정 읽기/쿼리 hello 일관성 수준이 완화 하면 지원 되는 Api를 각각 hello를 사용 하 여 요청 합니다. 5 가지 방법으로이 섹션에 설명 된 대로 지우기 기능 손실을 절충 특정 일관성은 및 성능을 제공 하는 hello Azure Cosmos DB 복제 프로토콜에서 지원 되는 일관성 수준입니다.

**강력**: 

* 강력한 일관성은 제공 된 [linearizability](https://aphyr.com/posts/313-strong-consistency-models) 보장 hello로 항목의 보장 된 tooreturn hello 가장 최신 버전을 읽습니다. 
* 강력한 일관성은 복제본의 과반수 쿼럼 hello가 지 속력 있게 커밋된 후 쓰기를 볼 수만 있는지 보장 합니다. 쓰기는 하거나 동기적으로 지 속력 있게 커밋된 hello 기본 및 보조 데이터베이스의 hello 쿼럼 둘 다로 또는 중단 됩니다. Hello 과반수 쿼럼 읽기에서 읽기를 승인할 항상, 클라이언트 수 커밋되지 않은 또는 부분 쓰기를 확인할 수 없습니다 및 tooread hello 최신 승인 된 쓰기를 항상 보장 됩니다. 
* 구성 된 toouse 강력한 일관성 있는 azure Cosmos DB 계정을 Azure Cosmos DB 계정으로 여러 Azure 지역을 연결할 수 없습니다. 
* 읽기 작업의 비용 hello (의 측면에서 [요청 단위](request-units.md) 사용) 강력한 일관성과 함께 세션 보다 높은 하 고 최종, 하지만 bounded 부실으로 hello 동일 합니다.

**제한된 부실** 

* Bounded 부실 일관성 보장 hello 읽기 쓰기 뒤 최대 지연 될 수 있습니다 *K* 버전 또는 항목의 접두사 또는 *t* 시간 간격입니다. 
* 따라서 부실 바인딩 선택 "부실" hello 구성할 수 있습니다 두 가지 방법으로: 버전 번호 *K* hello 쓰기 및 hello 시간 간격의 데이터로 hello 읽기 지연 hello 항목의 *t* 
* 부실 제공 총 글로벌 제외 하 고 내에서 순서 대로 "부실 창입니다." hello 제한 hello 단조 보장 내부 및 외부 "부실 창입니다." hello 영역 내에 있는 읽기 
* 제한된 부실은 세션이나 최종 일관성보다 강력한 일관성 보증을 제공합니다. 전 세계적으로 분산 응용 프로그램의 경우 여기서 toohave 강력한 일관성 있지만 99.99% 가용성 및 짧은 대기 시간을 원하는 시나리오에 대 한 경계 부실을 사용 하는 것이 좋습니다. 
* 제한된 부실로 구성된 Azure Cosmos DB 계정은 Azure Cosmos DB 계정이 있는 모든 Azure 지역과 연결할 수 있습니다. 
* 읽기 작업 (측면에서 사용 된 Ru)의 비용으로 hello bounded 부실 세션과 결과적 일관성 보다 높습니다. 하지만 강력한 일관성으로 hello 동일 합니다.

**세션**: 

* 강력 하 고 bounded 부실 일관성 수준에서 제공 hello 전역 일관성 모델과 달리 세션 일관성은 범위 지정 된 tooa 클라이언트 세션입니다. 
* 세션 일관성은 단조 읽기, 단조 쓰기, 사용자 고유 쓰기 읽기(RYW)를 보증하므로 장치 또는 사용자 세션이 관련된 모든 시나리오에 이상적입니다. 
* 최대 읽기 처리량 및 hello 가장 낮은 대기 시간 쓰기 및 읽기를 제공 하는 동시 및 세션 일관성은 세션에 대 한 예측 가능한 일관성을 제공 합니다. 
* 세션 일관성으로 구성된 Azure Cosmos DB 계정은 Azure Cosmos DB 계정이 있는 모든 Azure 지역과 연결할 수 있습니다. 
* 세션 일관성 수준이 강력한 및 bounded 부실 미만 이지만 이상 결과적 일관성은 읽기 작업 (측면에서 사용 된 Ru)의 비용 hello

<a id="consistent-prefix"></a>
**일관적인 접두사**: 

* 일관 된 접두사는 더 이상 쓰기 없는 경우, hello 그룹 내 복제본 hello 결국 수렴 되도록 합니다. 
* 일관적인 접두사는 읽기가 잘못된 쓰기를 볼 수 없도록 보장합니다. 쓰기 hello 순서에서 수행 된 경우 `A, B, C`, 클라이언트에 게 표시 하거나 다음 `A`, `A,B`, 또는 `A,B,C`, 되지 순서가 같은 하지만 `A,C` 또는 `B,A,C`합니다.
* 일관적인 접두사로 구성된 Azure Cosmos DB 계정은 Azure Cosmos DB 계정이 있는 모든 Azure 지역과 연결할 수 있습니다. 

**최종**: 

* 결과적 일관성은 더 이상 쓰기 없는 경우, hello 그룹 내 복제본 hello 결국 수렴 되도록 합니다. 
* 결과적 일관성은 일관성 hello 약한 형태 클라이언트가 이전에 본 적이 hello 것 보다 오래 된 hello 값을 얻을 수 있습니다.
* 결과적 일관성 hello 약한 일관성 읽었지만 결과가 제공 읽기 및 쓰기 모두에 대 한 대기 시간이 가장 짧은 hello를 제공 합니다.
* 최종 일관성으로 구성된 Azure Cosmos DB 계정은 Azure Cosmos DB 계정이 있는 모든 Azure 지역과 연결할 수 있습니다. 
* 읽기 작업 (측면에서 사용 된 Ru)의 비용 hello hello 결과적 일관성 수준은 hello 모든 hello Azure Cosmos DB 일관성 수준 중 가장 낮은 값입니다.

## <a name="configuring-hello-default-consistency-level"></a>Hello 기본 일관성 수준 구성
1. Hello에 [Azure 포털](https://portal.azure.com/)Jumpbar hello에서 클릭 **Azure Cosmos DB**합니다.
2. Hello에 **Azure Cosmos DB** 블레이드, 선택 hello 데이터베이스 계정 toomodify 합니다.
3. Hello 계정 블레이드에서 클릭 **일관성 기본**합니다.
4. Hello에 **기본 일관성** 블레이드, 새 일관성 수준 선택 hello 및 클릭 **저장**합니다.
   
    ![Hello 설정 아이콘 및 기본 일관성 항목 강조 표시 하는 스크린 샷](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>쿼리에 대한 일관성 수준
기본적으로 사용자 정의 리소스에 대 한 hello 일관성 수준이 쿼리에 hello 같은 hello 일관성 수준에 대 한 읽기 작업이 있습니다. 기본적으로 hello 인덱스는 각 삽입, 교체, 또는 항목 toohello Cosmos DB 컨테이너의 삭제에 동기적으로 업데이트 됩니다. Hello 쿼리 toohonor hello와 동일한 일관성 수준 가리킨 읽기가 사용 하도록이 설정 합니다. Azure Cosmos DB 쓰기가 최적화 하 고 쓰기, 동기 인덱스 유지 관리 및 일관 된 쿼리를 처리할 지속적인된 볼륨을 지 원하는, 구성할 수 있습니다 컬렉션 tooupdate 특정 해당 인덱스를 지연 합니다. Lazy 인덱싱을 추가 hello 쓰기 성능 증폭에 적합 하며 대량 수집 시나리오 작업은 주로 읽기 많은 경우.  

| 인덱싱 모드 | 읽기 | 쿼리 |
| --- | --- | --- |
| 일관성(기본값) |강력, 제한된 부실, 세션, 일관적인 접두사 또는 최종에서 선택 |강력, 제한된 부실, 세션 또는 최종에서 선택 |
| 지연 |강력, 제한된 부실, 세션, 일관적인 접두사 또는 최종에서 선택 |최종 |
| 없음 |강력, 제한된 부실, 세션, 일관적인 접두사 또는 최종에서 선택 |해당 없음 |

읽기 요청 각 API에 특정 쿼리 요청의 hello 일관성 수준을 낮출 수 있습니다.

## <a name="next-steps"></a>다음 단계
원하는 경우 toodo 더 장단점 및 일관성 수준에 대 한 읽기, 리소스 다음 hello를 좋습니다.

* Doug Terry. 야구(비디오)를 통해 복제된 데이터 일관성을 설명합니다.   
  [https://www.youtube.com/watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. 야구를 통해 복제된 데이터 일관성을 설명합니다.   
  [http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. 약하게 일관된 복제 데이터에 대한 세션 보장입니다.   
  [http://dl.acm.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. 최신 분산 데이터베이스 시스템 디자인의 일관성 장단점: hello 스토리의 일부만 한도 ".   
  [http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica. 실용적인 부분 쿼럼에 대한 PBS(확률적 제한된 부실)입니다.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. 최종 일관성 - 재고되었습니다.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.html](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor, Avishai 울, hello 부하, 용량 및 쿼럼 가용성 시스템, 컴퓨팅, v.27 n.2, p.423 447, 1998 년 4 월에 SIAM 저널
  [http://epubs.siam.org/doi/abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi로 Tan, 줄 위로:는 완전 하 고 자동 linearizability 검사 하는 프로그래밍 언어 디자인 및 구현, 2010 년 6 월 10 05에 우선, hello 2010 ACM SIGPLAN 회의의 절차 캐나다 [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* 제한 부실 실용적인 부분 쿼럼, hello VLDB (영 특), v.5 n.8, p.776 787, 2012 년 4 월의 절차에 대해 Peter Bailis, Shivaram Venkataraman, Michael J. 프랭클린, 있습니다 M. Hellerstein 이온 Stoica [http:// dl.acm.org/citation.cfm?id=2212359](http://dl.acm.org/citation.cfm?id=2212359)
