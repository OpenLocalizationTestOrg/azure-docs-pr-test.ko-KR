---
title: "Azure SQL 데이터 웨어하우스에 대 한 aaaBest 사례 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에 대한 솔루션을 개발하면서 알아야 할 권장 사항 및 모범 사례입니다. 이 내용은 성공적인 개발에 도움이 됩니다."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스에 대한 모범 사례
이 문서는 Azure SQL 데이터 웨어하우스에서 tooachieve 최적의 성능을 도움이 되는 많은 유용한의 컬렉션입니다.  이 문서에 대 한 hello 개념 중 일부는 기본 쉽고 tooexplain, 기타 개념은 더 높은 수준의 및이 문서의 hello 화면 방금 스크래치 했습니다.  이 문서의 hello 목적은 toogive 때 중요 한 영역 toofocus의 기본적인 몇 가지 지침과 tooraise 인식 작성 하 여 데이터 웨어하우스 합니다.  각 섹션에는 tooa 개념과 가리킵니다 toomore 자세한 문서는 커버 hello 개념에 자세히 소개 합니다.

Azure SQL 데이터 웨어하우스를 이제 시작하는 사용자라면 이 문서가 어려울 수 있습니다.  hello 항목 hello 시퀀스는 대부분 중요 한 hello 순서입니다.  먼저 몇 가지 개념 hello에 집중 하 여 시작 하는 경우 양호한 상태 수 수 있습니다.  SQL 데이터 웨어하우스 사용에 익숙해지면 돌아와서 더 많은 개념을 살펴봅니다.  걸리지 않습니다 toomake 의미 모든 항목에 대 한 long입니다.

## <a name="reduce-cost-with-pause-and-scale"></a>일시 중지 및 규모 조정으로 비용 절감
SQL 데이터 웨어하우스의 핵심 기능이입니다. hello 기능 toopause 사용 하지 않는 경우 계산 리소스의 hello 청구를 중지 합니다.  또 다른 주요 기능은 hello 기능 tooscale 리소스입니다.  일시 중지 및 배율 hello Azure 포털 또는 PowerShell 명령을 통해 수행할 수 있습니다.  에 대해 잘 알고 이러한 기능으로 사용 중에서이 아닌 경우 데이터 웨어하우스의 hello 비용을 크게 줄일 수 있습니다.  데이터 웨어하우스에 액세스할 수 있는 수식에서 항상 하려면 tooconsider 일시 중지 하는 것이 아니라 toohello 가장 작은 크기는 DW100 줄일 수도 있습니다.

또한 [계산 리소스 일시 중지][Pause compute resources], [계산 리소스 다시 시작][Resume compute resources], [계산 리소스 크기 조정]을 참조하세요.

## <a name="drain-transactions-before-pausing-or-scaling"></a>일시 중지 또는 크기 조정 전 트랜잭션 비우기
일시 중지 하거나 SQL 데이터 웨어하우스를 확장 하는 경우 쿼리는 hello를 시작할 때 취소 hello 백그라운드 일시 중지 하거나 요청 크기를 조정 합니다.  단순 선택 쿼리를 취소 빠른 작업을 거의 영향 toohello 시간이 걸리는 toopause 나가 인스턴스 크기를 조정 합니다.  그러나 트랜잭션 hello 데이터의 데이터 또는 hello 구조를 수정 하는 쿼리를 아닐 수 toostop 신속 하 게 합니다.  **기본적으로 트랜잭션 쿼리는 전체를 완료하거나 변경 사항을 롤백해야 합니다.**  트랜잭션 쿼리에 의해 완료 된 hello 작업 롤백 길거나 hello 원래 변경 보다 더 오래 hello 쿼리 된 적용 걸릴 수 있습니다.  예를 들어 행을 삭제 했습니다 및 1 시간 동안 이미 실행 된 쿼리를 취소 하면 걸릴 수 hello 시스템 삭제 된 시간 tooinsert 백 hello 행.  일시 중지 또는 처리 중, 일시 중지 하면 트랜잭션은 또는 tootake 보일 수 있지만 크기 조정 하는 동안 확장을 실행 하는 경우 시간이 오래 일시 중지 하 고 확장 하기 때문에 롤백 toocomplete hello에 대 한 toowait 진행할 수 있습니다.

또한 [트랜잭션 이해][Understanding transactions], [트랜잭션 최적화][Optimizing transactions]도 참조하세요.

## <a name="maintain-statistics"></a>통계 유지 관리
열에서 통계를 자동으로 감지하고 만들거나 업데이트하는 SQL Server와 달리, SQL 데이터 웨어하우스에서는 통계를 수동으로 유지 관리해야 합니다.  Toochange 계획 수행 하는 동안이 미래에 대 한 것이 좋습니다 toomaintain SQL 데이터 웨어하우스 계획 hello 프로그램 통계 tooensure 이제 hello 최적화 됩니다.  hello 최적화 프로그램에서 만든 hello 계획은 사용 가능한 통계 hello 우수한 수만 있습니다.  **모든 열에 샘플링 된 통계를 만드는 쉽게 tooget으로 시작 됩니다 통계.**  상태가 동일 하 게 중요 한 tooupdate 통계 중요 한 변경이 발생 tooyour 데이터입니다.  보수적인 접근 방법 찼거나 tooupdate 통계 매일 각 로드 후 합니다.  성능 및 비용 toocreate 및 update statistics hello 간의 장단점은 항상입니다. 걸리는 너무 길어 toomaintain 모든 통계를 찾을 경우 통계가 있는 열 또는 열에 대 한 좀 더 선택적 tootry toobe 자주 업데이트 해야 하는 것이 좋습니다.  예를 들어 tooupdate 날짜 열의 경우 새 값 추가, 일일 수 있는 경우가 있습니다. **조인, GROUP by 절 및 열을 찾을 위치 hello에 사용 되는 열에 포함 된 열에서 통계를 포함 하면 것이 가장 좋습니다 hello를 얻게 됩니다.**

또한 [테이블 통계 관리][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS], [UPDATE STATISTICS][UPDATE STATISTICS]도 참조하세요.

## <a name="group-insert-statements-into-batches"></a>INSERT 문을 일괄 처리로 그룹화
INSERT 문 또는 정기적으로 다시 로드 하는 조회의 일회성 부하 tooa 작은 테이블은 같은 문 사용 하 여 요구 사항에 대해 잘 수행 될 수 있습니다 `INSERT INTO MyLookup VALUES (1, 'Type 1')`합니다.  그러나 tooload 수백 또는 수백만 행 hello 하루 종일 해야 할 경우 singleton 삽입을 방금 유지할 수 없는 발견할 수 있습니다.  대신, tooa 파일을 작성 하 고 다른 프로세스는 정기적으로 연결 되 고이 파일을 로드 하 여 프로세스를 개발 합니다.

또한 [INSERT][INSERT]도 참조하세요.

## <a name="use-polybase-tooload-and-export-data-quickly"></a>PolyBase tooload 및 내보내기 데이터를 신속 하 게 사용
SQL 데이터 웨어하우스는 Azure Data Factory, PolyBase, BCP 등의 여러 도구를 통해 데이터 로드 및 내보내기를 지원합니다.  성능이 중요하지 않은 소량의 데이터에는 어떤 도구를 사용해도 사용자 요구 사항을 충족할 수 있습니다.  그러나를 로드 하거나 많은 양의 데이터를 내보내는 또는 빠른 성능이 필요한 경우 PolyBase는 hello 가장 좋습니다.  PolyBase의 SQL 데이터 웨어하우스의 디자인 된 tooleverage hello MPP (처리 방대한 병렬) 아키텍처는 따라서를 로드 및 데이터 크기가 숫자를 다른 어떤 도구 보다 더 빠르게 내보내기.  PolyBase 로드는 CTAS 또는 INSERT INTO를 사용하여 실행할 수 있습니다.  **CTAS에는 사용 하 여 최소화 됩니다 트랜잭션 로깅 및 hello 가장 빠른 방법은 tooload 데이터.**  Azure Data Factory는 또한 PolyBase 로드를 지원합니다.  PolyBase는 Gzip 파일을 포함한 다양한 파일 형식을 지원합니다.  **toomaximize 처리량 60 개 이상의 파일 toomaximize의 병렬 처리 부하에 gzip 텍스트 파일, 나누기 파일 사용 하는 경우.**  총 처리량을 더 빠르게 하기 위해 데이터를 동시에 로드하는 것이 좋습니다.

또한 [데이터 로드][Load data], [PolyBase 사용 지침][Guide for using PolyBase], [Azure SQL Data Warehouse 로딩 패턴 및 전략][Azure SQL Data Warehouse loading patterns and strategies], [Azure Data Factory를 사용하여 데이터 로드][Load Data with Azure Data Factory], [Azure Data Factory를 사용하여 데이터 이동][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT], [CTAS(Create Table As Select)][Create table as select (CTAS)]도 참조하세요.

## <a name="load-then-query-external-tables"></a>외부 테이블 로드 후 쿼리
Polybase, 외부 테이블 라고도 hello 가장 빠른 방법은 tooload 데이터 일 수 동안 쿼리에 적합 하지 않습니다. SQL 데이터 웨어하우스 Polybase 테이블은 현재 Azure Blob 파일만 지원합니다. 이러한 파일에는 지원 계산 리소스가 없습니다.  결과적으로, SQL 데이터 웨어하우스가이 작업을 오프 로드할 수 없습니다 및 따라서 tootempdb 주문 tooread hello 데이터에서를 로드 하 여 hello 전체 파일을 읽을 해야 합니다.  따라서이 데이터를 쿼리 하는 여러 개의 쿼리를 사용 하도록 설정한 경우 더 나은 tooload이이 데이터를 한 번이 고 hello 로컬 테이블을 사용 하 여 쿼리를 포함 합니다.

또한 [PolyBase 사용 지침][Guide for using PolyBase]도 참조하세요.

## <a name="hash-distribute-large-tables"></a>해시 배포 대형 테이블
기본적으로 테이블은 라운드 로빈 분산됩니다.  이렇게 하면 해당 테이블을 배포 해야 하는 방법을 toodecide 필요 없이 테이블을 만들기 전에 사용자가 tooget 쉽게 합니다.  라운드 로빈 테이블은 일부 워크로드에 대해서는 잘 작동하지만 대체로 배포 열을 선택하면 성능이 훨씬 향상됩니다.  hello 때 열에 의해 배포 된 테이블은 훨씬 보다 성능이 뛰어나지만 라운드 로빈 테이블의 가장 일반적인 예는 두 큰 팩트 테이블을 조인 하는 경우.  예를 들어 order_id 하 여 배포 되는 orders 테이블을가 order_id, 의해 order_id에 orders 테이블 tooyour 트랜잭션 테이블을 조인 하면를 배포 하는 트랜잭션 테이블을이 쿼리 의미 하는 통과 쿼리는 데이터 이동 작업을 해결 합니다.  단계가 적을수록 쿼리는 빨라집니다.  데이터 이동이 적을수록 쿼리는 빨라집니다.  이 설명은 정당한 스크래치 hello 화면입니다. 분산된 테이블을 로드할 때 느려집니다에 로드 하는 대로 들어오는 데이터 hello 배포 키에 정렬 되지 않았음을 해야 합니다.  많은 링크 아래 hello 어떻게 배포 열을 선택 하면 성능을 향상 시킬 수 방법에 대 한 자세한 내용은 참조 toodefine hello CREATE TABLES 문의 WITH 절에서 분산된 테이블입니다.

또한 [테이블 개요][Table overview], [테이블 배포][Table distribution], [테이블 배포 선택][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]도 참조하세요.

## <a name="do-not-over-partition"></a>과도한 분할 피하기
데이터를 분할하면 파티션 전환 또는 파티션 제거로 스캔 최적화를 통해 데이터를 매우 효율적으로 유지 관리할 수 있지만 과도하게 분할할 경우 쿼리 속도가 느려질 수 있습니다.  SQL Server에서 제대로 작동할 수 있는 높은 세분성 파티션 전략은 SQL 데이터 웨어하우스에서는 제대로 작동하지 않을 수 있습니다.  너무 많은 분할에 보다 적은 1 백만 행이 각 파티션에 클러스터형된 columnstore 인덱스의 hello 효율성을 줄일 수 있습니다.  hello 백그라운드 SQL 데이터 웨어하우스 데이터 수로 분할 60 데이터베이스 염두에서에 둬야 파티션 수가 100 개라도 테이블을 만들 경우이 실제로 인해 6000 파티션에 있도록 합니다.  각 작업은 다르므로 tooexperiment toosee 가장 적합 한 작업 분할이 hello 최선입니다.  SQL Server에서 작업한 것보다 낮은 세분성을 고려합니다.  예를 들어 매일 분할보다는 매주 또는 매달 분할을 사용하는 것이 좋습니다.

또한 [테이블 분할][Table partitioning]도 참조하세요.

## <a name="minimize-transaction-sizes"></a>트랜잭션 크기 최소화
INSERT, UPDATE, DELETE 문은 트랜잭션에서 실행되며 실패할 경우 롤백해야 합니다.  긴 롤백에 대 한 잠재적 toominimize hello 가능 하면 항상 트랜잭션 크기를 최소화 합니다.  INSERT, UPDATE 및 DELETE 문을 부분으로 나누어 이를 수행할 수 있습니다.  예를 들어 예상 tootake 1 시간, 가능한 경우 INSERT를 사용 하도록 설정한 경우 나누고 hello 삽입 15 분 내에 각 실행 4 부분으로 구성 합니다.  CTAS에는, TRUNCATE, DROP TABLE 또는 삽입 tooempty 테이블 tooreduce 롤백 위험와 같은 특수 한의 최소 로깅을 경우 활용 합니다.  또 다른 방법은 tooeliminate 롤백 toouse 메타 데이터 작업만 파티션 데이터 관리에 대 한 전환 등입니다.  예를 들어 대신 hello order_date 2001 년 10 월에에서 있던 테이블에 DELETE 문을 toodelete 모든 행을 실행, 있습니다 수 월별 데이터를 분할 하며 다른 테이블에서 빈 파티션에 대 한 데이터를 사용 하는 hello 파티션을 외부로 전환한 다음 (ALTER를 참조 하십시오. 테이블 예제)입니다.  분할 되지 않은 테이블에 대 한 DELETE를 사용 하는 대신 tookeep 테이블에서 원하는 CTAS toowrite hello 데이터를 사용 하 여 것이 좋습니다.  경우는 CTAS에는 hello 시간과,이 훨씬 더 안전 하 게 작업 toorun 중지가 최소화 트랜잭션 로깅이 있으며 필요한 경우 신속 하 게 취소할 수 있습니다.

또한 [트랜잭션 이해][Understanding transactions], [트랜잭션 최적][Optimizing transactions], [테이블 분할][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [CTAS(Create Table As Select)][Create table as select (CTAS)]도 참조하세요.

## <a name="use-hello-smallest-possible-column-size"></a>Hello 가장 작은 가능한 열 크기를 사용 하 여
DDL을 정의할 때 데이터를 원하는 hello 가장 작은 데이터 형식을 사용 하 여 쿼리 성능이 향상 됩니다.  이것은 CHAR 및 VARCHAR 열에 대해 특히 중요합니다.  Hello 가장 긴 값 열에 있는 25 자 이면 다음 VARCHAR(25)로 열을 정의 합니다.  모든 문자 열 tooa 큰 기본 길이 정의 하지 마십시오.  또한 반드시 필요한 경우에는 열을 NVARCHAR를 사용하는 것보다 VARCHAR로 정의하세요.

또한 [테이블 개요][Table overview], [테이블 데이터 형식][Table data types], [CREATE TABLE][CREATE TABLE]도 참조하세요.

## <a name="use-temporary-heap-tables-for-transient-data"></a>임시 데이터에 대해 임시 힙 테이블 사용
일시적으로 SQL 데이터 웨어하우스에 대 한 데이터는 방문는 힙 테이블을 사용 하면 전체 프로세스를 더 빠르게 hello 알 수 있습니다.  로드 하는 경우 데이터만 toostage hello 테이블 tooheap 테이블을 로드 하는 많은 변형을 실행 하기 전에 됩니다 hello 데이터 tooa 로드 보다 훨씬 빠르게 클러스터형 columnstore 테이블.  또한 데이터 tooa 로드 임시 테이블 설정 하면 테이블 toopermanent 저장소를 로드할 때 보다 훨씬 빠르게 합니다.  임시 테이블 "#"로 시작 하며 만들어지므로, 제한 된 경우에만 작동 될 수 있습니다는 hello 세션 액세스할 수 있습니다.   힙 테이블은 CREATE TABLE의 hello WITH 절에 정의 됩니다.  임시 테이블을 사용 하는 경우 해당 임시 테이블에 대 한 toocreate 통계를 너무 기억 합니다.

또한 [임시 테이블][Temporary tables], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]도 참조하세요.

## <a name="optimize-clustered-columnstore-tables"></a>클러스터형 Columnstore 테이블 최적화
클러스터형된 columnstore 인덱스는 hello Azure SQL 데이터 웨어하우스에 데이터를 저장할 수는 가장 효율적인 방법 중 하나입니다.  기본적으로 SQL 데이터 웨어하우스의 테이블은 클러스터형 ColumnStore로 만들어집니다.  tooget hello 최상의 성능을 좋은 세그먼트 양질의 columnstore 테이블에 대 한 쿼리 하는 것이 중요 합니다.  행의 메모리 사용량이 toocolumnstore 테이블 기록 되 고, columnstore 세그먼트 품질이 저하 될 수 있습니다.  세그먼트 품질은 압축된 행 그룹에 있는 행의 수로 측정할 수 있습니다.  Hello 참조 [저하 columnstore의 원인을 인덱스 품질] [ Causes of poor columnstore index quality] hello에 [인덱스 테이블] [ Table indexes] 에 대 한 단계별 지침에 대 한 기사 검색 하 고 클러스터 된 columnstore 테이블에 대 한 세그먼트 품질 개선 합니다.  고품질 columnstore 세그먼트 중요 한 요소 이기 때문에 데이터를 로드 하기 위한 hello 중간 규모 또는 대규모 리소스에는 어떤 것이 좋습니다 toouse 사용자 id는 합니다.  안녕 적은 Dwu를 사용 하면 hello 큰 hello 리소스 클래스 tooassign tooyour 사용자 로드 해야 합니다.

Columnstore 테이블 쿼리 이점을 columnstore 테이블 일반적으로 않습니다 데이터를 푸시 압축 된 columnstore 세그먼트 테이블당 1 백만 개 이상의 행이 각 SQL 데이터 웨어하우스 테이블 경험상,으로 60 테이블로 분할은 될 때까지 이후 hello 테이블 60 백만 개 이상의 행에 있습니다.  보다 작은 60 백만 행이 있는 테이블에 대 한 하지 사항이 모든 의미 toohave columnstore 인덱스.  오히려 상황을 악화시킬 수 있습니다.  또한 데이터를 분할 하는 경우 각 파티션에 있는 클러스터형된 columnstore 인덱스에서 toohave 1 백만 행 toobenefit 필요 함을 tooconsider를 원하는 됩니다.  테이블에 파티션 수가 100 개라도 경우 클러스터형된 열 저장소에서 행 toobenefit toohave 6 십억 이상 필요 합니다 (60 분포 * 파티션 수가 100 개라도 * 1 백만 행).  테이블에이 예에서 6 십억 행 수 없는 경우 hello 파티션 수를 줄이거나 힙 테이블을 대신 사용 하는 것이 좋습니다.  또한 경우 수도 있습니다 시험 toosee 가치가 보조 인덱스 있는 힙 테이블을 columnstore 테이블 보다는 더 나은 성능을 얻을 수 있습니다.  Columnstore 테이블은 보조 인덱스를 아직 지원하지 않습니다.

Columnstore 테이블을 쿼리할 때 필요한 hello 열만 선택 하는 경우 쿼리가 빠르게 실행 됩니다.  

또한 [테이블 인덱스][Table indexes], [Columnstore 인덱스 가이드][Columnstore indexes guide], [Columnstore 인덱스 다시 빌드][Rebuilding columnstore indexes]도 참조하세요.

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>더 큰 클래스 tooimprove 쿼리 성능 리소스를 사용 하 여
SQL 데이터 웨어하우스 방식으로 tooallocate 메모리 tooqueries로 리소스 그룹을 사용합니다.  모든 사용자는 hello 초기 toohello 작은 리소스 클래스 분포는 메모리의 메가바이트 수 있게 하는 할당 됩니다.  항상 있으므로 60 배포와 각 배포 100MB를 할당은 6000 MB 또는 6GB 바로 아래 시스템 넓은 hello 총 메모리의 최소를 제공 됩니다.  더 큰 메모리 할당에서 큰 조인 또는 로드 tooclustered columnstore 테이블을 같은 특정 쿼리를 제공 합니다.  순수 검색과 같은 일부 쿼리에는 어떤 이점도 보이지 않습니다.  Hello 긍 적 적인 측면에서 더 큰 리소스 클래스를 사용 하 여 영향을 동시성, tootake 할 수도이를 모든 사용자가 tooa 큰 리소스 클래스를 이동 하기 전에 고려 됩니다.

또한 [동시성 및 워크로드 관리][Concurrency and workload management]도 참조하세요.

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>리소스 클래스입니다. 더 작은 tooIncrease 동시성을 사용 하 여
사용자 쿼리 toohave 오래 지연 스 러 하는 것을 인식 하는 경우 사용자가 더 큰 리소스 클래스에서 실행 되 고 다른 쿼리 tooqueue를 일으키는 동시성 슬롯을 많이 사용 하는 합니다.  toosee 사용자 쿼리 대기 중인 경우 실행 `SELECT * FROM sys.dm_pdw_waits` toosee 경우 모든 행이 반환 됩니다.

또한 [동시성 및 워크로드 관리][Concurrency and workload management], [sys.dm_pdw_waits][sys.dm_pdw_waits]도 참조하세요.

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Toomonitor Dmv를 사용 하 고 쿼리를 최적화
SQL 데이터 웨어하우스 사용된 toomonitor 쿼리 실행 될 수 있는 몇 가지 Dmv에 있습니다.  다음 문서를 모니터링 하는 hello toolook 실행 중인 hello 세부 정보를 쿼리 하는 방법에 대 한 단계별 지침 안내 합니다.  이러한 Dmv에서 tooquickly 찾기 쿼리 hello 레이블 옵션을 사용 하 여 쿼리를 수 있습니다.

또한 [DMV를 사용하여 워크로드 모니터링][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]도 참조하세요.

## <a name="other-resources"></a>기타 리소스
또한 일반적인 문제 및 해결 방법에 대해서는 [문제 해결][Troubleshooting] 문서를 참조하세요.

원하는 내용을 대 한이 문서의 찾지 못한 경우 hello "검색 문서에 대 한" hello 왼쪽에서의이 페이지 toosearch 모든 hello Azure SQL 데이터 웨어하우스 문서를 사용해 보세요.  hello [Azure SQL 데이터 웨어하우스 MSDN 포럼] [ Azure SQL Data Warehouse MSDN Forum] 있습니다 tooask 질문 tooother 사용자 및 toohello SQL 데이터 웨어하우스 제품 그룹에 대 한 지점으로 만드는 되었습니다.  우리는 답변을 다른 사용자 또는 우리 기준이 포럼 tooensure 적극적으로 모니터링 합니다.  스택 오버플로 대 한 질문 tooask을 원할 경우 해야는 [Azure SQL 데이터 웨어하우스 스택 오버플로 포럼][Azure SQL Data Warehouse Stack Overflow Forum]합니다.

마지막으로, 사용 마십시오 hello [Azure SQL 데이터 웨어하우스 피드백] [ Azure SQL Data Warehouse Feedback] toomake 기능 요청 페이지.  요청을 추가하거나 다른 요청에 투표를 하면 기능의 순위를 지정하는 데 도움이 됩니다.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[계산 리소스 크기 조정]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
