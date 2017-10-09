---
title: "aaaAzure SQL 데이터베이스 벤치 마크 개요"
description: "이 항목에서는 Azure SQL 데이터베이스 벤치 마크를 Azure SQL 데이터베이스의 hello 성능을 측정에 사용 된 hello를 설명 합니다."
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Azure SQL 데이터베이스 벤치마크 개요
## <a name="overview"></a>개요
Microsoft Azure SQL 데이터베이스는 여러 성능 수준의 3가지 [서비스 계층](sql-database-service-tiers.md) 을 제공합니다. 각 성능 수준은 증가 집합이 자원 또는 '전원' 설계 toodeliver 높은 처리량을 제공합니다.

것이 중요 한 toobe 수 tooquantify 높아지는 데이터베이스 성능이 hello 각 성능 수준의 기능 증가가 변환 하는 방법을 합니다. 이 Microsoft 개발 했습니다 toodo hello SQL 데이터베이스 벤치 마크 ASDB (Azure). hello 모든 OLTP 작업에 기본적인 작업 조합을 수행 합니다. 각 성능 수준에서 실행 되는 데이터베이스에 대 한 hello 처리량을 측정 합니다.

hello 리소스와 각 서비스 계층과 성능 수준의 표현의 측면에서 [데이터베이스 트랜잭션 단위 (DTUs)](sql-database-what-is-a-dtu.md)합니다. Dtu를 통해 toodescribe hello 성능 수준의 상대적 용량 CPU, 메모리의 복합된 측정에 기반 하 고 읽고 쓸 각 성능 수준에서 제공 되는 속도입니다. 데이터베이스의 DTU 등급이 hello 더블링 toodoubling hello 데이터베이스 기능도를 같습니다. hello 벤치 마크를 통해 tooassess hello 영향 비례하여에서 데이터베이스 크기, 사용자 및 트랜잭션 속도 확장할 수를 크기 조정 하는 동안 실제 데이터베이스 작업을 실행 하 여 각 성능 수준에서 제공 되는 기능을 늘리면 hello 데이터베이스 성능에 toohello 리소스 toohello 데이터베이스를 제공 합니다.

트랜잭션을 시간당을 사용 하 여 hello Basic 서비스 계층의 hello 처리량 나타내어 분당 트랜잭션, 및 초당을 보다 쉽게 tooquickly 이렇게 하면 트랜잭션을 사용 하 여 hello Premium 서비스 계층을 사용 하 여 hello Standard 서비스 계층 관련 hello 각 응용 프로그램의 서비스 계층 toohello 요구 사항 성능 가능성이 있습니다.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>상관 관계 자동 연결 벤치 마크 결과 tooreal 세계 데이터베이스 성능
중요 한 toounderstand 모든 벤치 마크와 같은 해당 ASDB 되만 한정 되며 암시적 됩니다. 안녕 트랜잭션 hello 벤치 마크 응용 프로그램을 사용 하 여 수행 하는 속도 다른 응용 프로그램과 얻을 수 있는 것과 동일한 hello 되지 않습니다. hello 벤치 마크는 종류의 테이블 및 데이터 형식 범위를 포함 하는 스키마에 대해 실행 하는 다른 트랜잭션의 컬렉션을 구성 합니다. Hello 벤치 마크 연습 hello 일반적인 tooall OLTP 워크 로드는 동일한 기본 작업을 하는 동안 데이터베이스 또는 응용 프로그램의 특정 클래스를 나타내지 않습니다. hello hello 벤치 마크의 목적은 tooprovide 예상 되는 확장 또는 축소 하는 경우 성능 수준 간에 데이터베이스의 적절 한 지침 toohello 상대적인 성능입니다. 실제로, 각 데이터베이스는 크기와 복잡성이 다르고 다양하게 혼합된 워크로드를 처리할 수 있으며 각각 다른 방식으로 대응합니다. 예를 들어, IO를 많이 사용하는 응용 프로그램은 IO 임계값에 빠르게 도달할 수 있고 CPU를 많이 사용하는 응용 프로그램은 CPU 한도에 빠르게 도달할 수 있습니다. 했더라도 특정 데이터베이스가 동일한 방식으로 hello 증가 시 벤치 마크로 로드 하는 hello에 확장할 수 있습니다.

hello 벤치 마크와 해당 방법 설명 아래에 자세히 합니다.

## <a name="benchmark-summary"></a>벤치마크 요약
ASDB는 온라인 트랜잭션 처리 (OLTP) 워크 로드에서에서 가장 자주 발생 하는 기본적인 데이터베이스 작업 조합의 hello 성능을 측정 합니다. Hello 벤치 마크는 클라우드 컴퓨팅을 염두에 두고 설계, 있지만 hello 데이터베이스 스키마, 데이터 채우기 및 트랜잭션이 된 디자인 된 toobe OLTP 워크 로드에 가장 많이 사용 하는 hello 기본 요소를 광범위 하 게 반영 합니다.

## <a name="schema"></a>스키마
hello 스키마가 디자인 된 toohave 충분 한 다양 하 고 복잡 toosupport 폭넓은 작업 합니다. hello 벤치 마크는 6 개 테이블로 구성 된 데이터베이스에 대해 실행 됩니다. hello 테이블 세 범주로: 고정 크기, 확장 및 증가 합니다. 2개의 고정 크기 테이블, 3개의 확장 테이블, 1개의 증가 테이블이 있습니다. 고정 크기 테이블에는 고정된 수의 행이 있습니다. 크기 조정 테이블 카디널리티가 비례 toodatabase 성능 이지만 hello 벤치 마크 하는 동안 변경 되지 않습니다. hello 테이블 증가 하 고 초기 로드 시 확장 테이블과 같이 크기가 지정 하지만 hello 카디널리티 hello 행을 삽입 / 삭제 하는 대로 hello 벤치 마크 실행 과정에서 변경 합니다.

hello 스키마에는 다양 한 데이터 형식에 정수, 숫자, 문자 및 날짜/시간입니다. hello 기본 및 보조 키를 포함 되지만 포함 외래 키는-즉, 테이블 간에 참조 무결성 제약 조건이 없으면 있습니다는 합니다.

데이터 생성 프로그램이 초기 데이터베이스 hello에 대 한 hello 데이터를 생성합니다. 정수 및 숫자 데이터는 다양한 전략으로 생성됩니다. 값이 범위에 무작위로 분포되는 경우도 있습니다. 다른 경우에는 값 집합이 임의로 변경한 tooensure 특정 배포 유지 관리 됩니다. 텍스트 필드는 가중치가 적용 된 목록이 단어 tooproduce 실제와 같은 데이터에서 생성 됩니다.

hello 데이터베이스 크기 기반으로 "배율 인수"입니다. hello 배율 (약어 SF) hello 확장 및 증가 테이블의 hello 카디널리티를 결정 합니다. 아래에 설명 된 대로 hello 섹션 사용자 및 속도 hello 데이터베이스 크기, 사용자 및 다른 비율 tooeach로 모든 크기를 조정 하는 최대 성능을 수 있습니다.

## <a name="transactions"></a>트랜잭션
hello 작업 hello 테이블 아래에 나와 있는 것 처럼 9 개 트랜잭션 유형으로 구성 됩니다. 각 트랜잭션에 특정 시스템 특징 집합을 hello 데이터베이스 엔진과 시스템 하드웨어의 디자인 된 toohighlight를 hello 다른 트랜잭션이 크게 다릅니다. 이러한 방식을 통해 다양 한 구성 요소 toooverall 성능을 보다 쉽게 tooassess hello 영향입니다. 예를 들어 "읽기 중형" hello 트랜잭션 수가 디스크에서 읽기 작업을 생성합니다.

| 트랜잭션 유형 | 설명 |
| --- | --- |
| 적은 읽기 작업 |SELECT, 메모리 내, 읽기 전용 |
| 중간 읽기 작업 |SELECT, 대부분 메모리 내, 읽기 전용 |
| 많은 읽기 작업 |SELECT, 대부분 메모리 외, 읽기 전용 |
| 적은 업데이트 작업 |UPDATE, 메모리 내, 읽기-쓰기 |
| 많은 업데이트 작업 |UPDATE, 대부분 메모리 외, 읽기-쓰기 |
| 적은 삽입 작업 |INSERT, 메모리 내, 읽기-쓰기 |
| 많은 삽입 작업 |INSERT, 대부분 메모리 외, 읽기-쓰기 |
| 삭제 |DELETE, 메모리 내 및 메모리 외 혼합, 읽기-쓰기 |
| 많은 CPU 사용 |SELECT, 메모리 내, 상대적으로 많은 CPU 부하, 읽기 전용 |

## <a name="workload-mix"></a>워크로드 혼합
트랜잭션은 다음 전체 조합의 hello로 가중치가 적용 된 분산에서 임의로 선택 됩니다. hello 전체 조합의 약 2: 1의 읽기/쓰기 비율은 있습니다.

| 트랜잭션 유형 | 혼합 비율 |
| --- | --- |
| 적은 읽기 작업 |35 |
| 중간 읽기 작업 |20 |
| 많은 읽기 작업 |5 |
| 적은 업데이트 작업 |20 |
| 많은 업데이트 작업 |3 |
| 적은 삽입 작업 |3 |
| 많은 삽입 작업 |2 |
| 삭제 |2 |
| 많은 CPU 사용 |10 |

## <a name="users-and-pacing"></a>사용자 및 속도
hello 벤치 마크의 작업 수의 동시 사용자의 연결 toosimulate hello 동작의 집합을 통해 트랜잭션을 전송 하는 도구에서 생성 됩니다. 모두 hello 연결과 트랜잭션은 컴퓨터에서 생성 되 면 하지만 편의상 언급할 toothese 연결을 "사용자" 모든 사용자가 수행할 hello 각 사용자의 다른 모든 사용자와 독립적으로 작동 하지만 동일한 단계 주기를 아래에 나와 있습니다.

1. 데이터베이스에 연결합니다.
2. 신호를 받은 tooexit 될 때까지 반복 합니다.
   * (가중치가 적용된 분포에서) 무작위로 트랜잭션을 선택합니다.
   * 선택한 hello 트랜잭션과 hello 응답 시간을 측정을 수행 합니다.
   * 속도 지연을 기다립니다.
3. Hello 데이터베이스 연결을 닫습니다.
4. 끝내기를 클릭합니다.

속도 지연 시간 (단계 2 c) hello를 임의로 선택 하지만 1.0 초 평균 분포 크기가 합니다. 따라서 각 사용자는 평균적으로 1초당 최대 1개의 트랜잭션을 생성할 수 있습니다.

## <a name="scaling-rules"></a>확장 규칙
사용자 수가 hello hello 데이터베이스 크기 (배율 단위)에 의해 결정 됩니다. 5개의 배율 단위당 1명의 사용자가 있습니다. 속도 지연 hello, 때문에 한 명의 사용자에서 초당 트랜잭션을 최대 하나만 평균 생성할 수 있습니다.

예를 들어, 배율이 500(SF=500)인 데이터베이스는 사용자가 100명이며 최대 100TPS의 속도를 달성할 수 있습니다. 더 높은 TPS 속도 toodrive 더 많은 사용자와 더 큰 데이터베이스가 필요합니다.

hello 표에서 hello 실제로 각 서비스 계층과 성능 수준에 대해 지 원하는 사용자 수를 보여 줍니다.

| 서비스 계층(성능 수준) | 사용자 | 데이터베이스 크기 |
| --- | --- | --- |
| Basic |5 |720MB |
| Standard(S0) |10 |1 GB |
| Standard(S1) |20 |2.1GB |
| Standard(S2) |50 |7.1GB |
| Premium(P1) |100 |14 GB |
| Premium(P2) |200 |28GB |
| Premium(P6/P3) |800 |114GB |

## <a name="measurement-duration"></a>측정 기간
유효한 벤치마크를 실행하려면 한 시간 이상의 안정적 측정 기간이 필요합니다.

## <a name="metrics"></a>메트릭
hello 키 hello 벤치 마크에 메트릭은 처리량과 응답 시간입니다.

* 처리량은 벤치 마크 hello에에서 hello 필수 성능 측정값입니다. 처리량은 모든 트랜잭션 유형을 세는 단위 시간당 트랜잭션 수로 보고됩니다.
* 응답 시간은 성능 예측 가능성에 대한 측정값입니다. hello 응답 시간 제약 조건은 서비스 클래스 일수록 아래와 같이 보다 엄격한 응답 시간 요구 사항을, 일수록 클래스와 다릅니다.

| 서비스 클래스 | 처리량 측정 | 응답 시간 요구 사항 |
| --- | --- | --- |
| Premium |초당 트랜잭션 수 |0.5초에서 95 백분위수 |
| Standard |분당 트랜잭션 수 |1.0초에서 90 백분위수 |
| Basic |시간당 트랜잭션 수 |2.0초에서 80 백분위수 |

## <a name="conclusion"></a>결론
Azure SQL 데이터베이스 벤치 마크 hello hello hello 사용 가능한 서비스 계층 및 성능 수준 범위에서 실행 되는 Azure SQL 데이터베이스의 상대 성능을 측정 합니다. hello는 온라인 트랜잭션 처리 (OLTP) 워크 로드에서에서 가장 자주 발생 하는 기본적인 데이터베이스 작업 조합을 수행 합니다. Hello 벤치 마크가만 CPU 속도, 메모리 크기 및 IOPS 등 각 수준에서 제공 하는 hello 리소스를 나열 하 여 hello 성능 수준 변경이 처리량에 대 한 보다 의미 있는 hello 영향을 평가 하는 제공 실제 성능을 측정 하므로 . Hello 이후에서 계속 tooevolve hello 벤치 마크 toobroaden 해당 범위 하 고 제공 된 hello 데이터를 확장 합니다.

## <a name="resources"></a>리소스
[소개 tooSQL 데이터베이스](sql-database-technical-overview.md)

[서비스 계층 및 성능 수준](sql-database-service-tiers.md)

[단일 데이터베이스의 성능 지침](sql-database-performance-guidance.md)
