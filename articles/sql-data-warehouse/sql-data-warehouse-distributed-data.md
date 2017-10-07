---
title: "aaaHow distributed의 Azure SQL 데이터 웨어하우스 데이터 작동 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 테이블을 배포 하기 위한 방대한 병렬 처리 (MPP) 및 hello 옵션에 대 한 데이터를 배포 하는 방법에 대해 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>대규모 병렬 처리(MPP)에 대한 분산 데이터 및 분산 테이블
Microsoft의 대규모 병렬 처리(MPP) 시스템인 SQL Data Warehouse 및 병렬 데이터 웨어하우스의 사용자 데이터가 분산되는 원리에 대해 알아봅니다. 분산된 데이터 데이터 웨어하우스 toouse 디자인 하면 tooachieve hello 쿼리 처리 hello MPP 아키텍처의 이점을 통해 효과적으로. 몇 가지 데이터베이스 디자인 선택에 따라 쿼리 성능 향상에 상당한 영향을 미칠 수 있습니다.  

> [!NOTE]
> Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 사용 하 여 hello 같은 대규모 병렬 처리 (MPP) 디자인, 있지만 hello 기본 플랫폼으로 인해 몇 가지 차이점이 필요한 것입니다. SQL Data Warehouse는 Azure에서 실행되는 PaaS(Platform as a Service)입니다. 병렬 데이터 웨어하우스는 Windows Server에서 실행되는 온-프레미스 어플라이언스인 APS(분석 플랫폼 시스템)에서 실행됩니다.
> 
> 

## <a name="what-is-distributed-data"></a>분산 데이터란?
SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 분산된 된 데이터는 hello MPP 시스템에서 여러 위치에 저장 되어 있는 toouser 데이터 의미 합니다. 각 위치 기능 독립 저장소 및 처리 장치를 해당 부분의 hello 데이터에서 쿼리를 실행 합니다. 분산된 된 데이터는 병렬 tooachieve 높은 쿼리 성능에 근본적인 toorunning 쿼리 합니다.

toodistribute 데이터 hello 데이터 웨어하우스는 사용자 테이블 distributed tooone 위치의 각 행에 할당합니다.  해시 분산 메서드 또는 라운드 로빈 메서드를 사용하여 테이블을 분산할 수 있습니다. CREATE TABLE 문 hello에 hello 배포 방법 지정 됩니다. 

## <a name="hash-distributed-tables"></a>해시 분산 테이블
다음 다이어그램 hello 전체 (분산 되지 않은 테이블)을 가져옵니다 해시 distributed 표 형식으로 저장 하는 방법을 보여 줍니다. 결정적 함수는 각 행 toobelong tooone 배포를 할당합니다. Hello 테이블 정의에서 hello 열 중 하나의 hello 배포 열으로 지정 됩니다. hello 해시 함수는 각 행 tooa 분배 hello 배포 열 tooassign의 hello 값을 사용 합니다.

배포 열 고유성, 데이터 기울이기 hello 유형의 hello 시스템에서 실행 하는 쿼리 등의 hello 선택에 대 한 성능 고려 사항이 있습니다.

![분산 테이블](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "분산 테이블")  

* 각 행이 속한 tooone 배포 합니다.  
* 결정적 해시 알고리즘에는 각 행 tooone 배포를 할당합니다.  
* hello 다양 한 크기의 테이블에 표시 된 대로 hello 분포 테이블 행 수에 따라 다릅니다.

## <a name="round-robin-distributed-tables"></a>라운드 로빈 분산 테이블
라운드 로빈 분산된 테이블 각 행 tooa 분배를 순차적으로 할당 하 여 hello 행을 배포 합니다. 라운드 로빈 테이블로 빠른 tooload 데이터 이지만 쿼리 성능이 느려질 수 있습니다.  일반적으로 라운드 로빈 테이블 조인 hello 행 tooenable hello 쿼리 tooproduce 시간이 올바른 결과 섞는 필요 합니다.

## <a name="distributed-storage-locations-are-called-distributions"></a>분산된 저장소 위치를 분산이라고 함
분산된 각 위치를 분산이라고 부릅니다. 병렬 쿼리 실행, 각 배포 hello 데이터의 해당 부분에는 SQL 쿼리를 수행 합니다. SQL 데이터 웨어하우스 SQL 데이터베이스 toorun hello 쿼리를 사용합니다. 병렬 데이터 웨어하우스 SQL Server toorun hello 쿼리를 사용합니다. 이 공유 없는 아키텍처 디자인은 기본 tooachieving 확장 병렬 계산 합니다.

### <a name="can-i-view-hello-distributions"></a>Hello 분포를 볼 수 있습니까?
각 배포에 배포 ID가 고 tooSQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 관련 된 시스템 뷰에 표시 됩니다. Hello 배포 ID tootroubleshoot 쿼리 성능 및 기타 문제를 사용할 수 있습니다. Hello 시스템 뷰 목록, 참조 hello [MPP 시스템 뷰](sql-data-warehouse-reference-tsql-statements.md)합니다.

## <a name="difference-between-a-distribution-and-a-compute-node"></a>분산과 계산 노드의 차이점
분포는 분산된 된 데이터를 저장 하 고 병렬 쿼리 처리에 대 한 hello 기본 단위입니다. 분산은 계산 노드로 그룹화됩니다. 각 계산 노드는 하나 이상의 분산을 추적합니다.  

* 분석 플랫폼 시스템 hello 하드웨어 아키텍처 및 확장 기능은의 중앙 구성 요소로 계산 노드를 사용합니다. 항상 해시 distributed 테이블에 대 한 hello 다이어그램에 나와 있는 것 처럼 계산 노드에 당 8 개의 배포를 사용 합니다. hello 계산 노드 수 및 배포를 따라서 hello, hello hello 기기를 구매 하는 계산 노드 수에 따라 결정 됩니다. 예를 들어 8개의 계산 노드를 구매하면 64개의 분산(계산 노드 8개 x 분산 8개/노드)을 얻게 됩니다. 
* SQL Data Warehouse는 분산의 수는 60개로 고정되어 있고 계산 노드의 수는 유연하게 결정할 수 있습니다. hello 계산 노드는 Azure 컴퓨팅 및 저장소 리소스에 구현 됩니다. hello 계산 노드 수에 따라 toohello 백 엔드 서비스 작업 hello 데이터 웨어하우스에 대 한 지정 컴퓨팅 hello 용량 (Dwu)를 변경할 수 있습니다. 계산 노드 hello 수가 변경 되 면 hello 수가 계산 노드당도 변경 됩니다. 

### <a name="can-i-view-hello-compute-nodes"></a>Hello 계산 노드를 볼 수 있습니까?
각 계산 노드가 노드 ID에 있으며 tooSQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 관련 된 시스템 뷰에서 볼 수 있습니다.  Hello node_id 열 이름이 sys.pdw_nodes로 시작 하는 시스템 뷰에서 검색 하 여 hello 계산 노드를 볼 수 있습니다. Hello 시스템 뷰 목록, 참조 hello [MPP 시스템 뷰](sql-data-warehouse-reference-tsql-statements.md)합니다.

## <a name="Replicated"></a>복제된 테이블
복제 된 테이블에는 각 계산 노드에 hello 테이블의 복사본을 저장 하는 완벽 하 게 합니다. 테이블을 복제 하기 전에 조인 또는 집계를 계산 노드 간에 hello 필요 tootransfer 데이터를 제거 합니다. Hello 때문에 복제 된 테이블은 작은 테이블으로만 각 계산 노드에 대해 추가 저장소 필요한 toostore hello 전체 테이블입니다.  

hello 다음 다이어그램에서는 각 계산 노드에 저장 된 복제 된 테이블 SQL 데이터 웨어하우스 hello 복제 된 테이블은 각 계산 노드에 대해 완전히 복사 tooa 배포 데이터베이스입니다. 병렬 데이터 웨어하우스에 대 한 hello 복제 테이블 toohello 계산 노드에 할당 된 모든 디스크에 저장 됩니다.  이 디스크 전략은 SQL Server 파일 그룹을 사용하여 구현됩니다.  

![복제 테이블](media/sql-data-warehouse-distributed-data/replicated-table.png "복제 테이블") 

## <a name="next-steps"></a>다음 단계
distributed toouse 테이블 효과적으로 참조 [SQL 데이터 웨어하우스의 테이블을 배포 합니다.](sql-data-warehouse-tables-distribute.md)  

