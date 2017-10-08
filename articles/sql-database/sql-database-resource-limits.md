---
title: "SQL 데이터베이스 리소스 제한 aaaAzure | Microsoft Docs"
description: "이 페이지에서는 Azure SQL 데이터베이스에 대한 몇 가지 일반적인 리소스 제한을 설명합니다."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Azure SQL 데이터베이스 리소스 제한
## <a name="overview"></a>개요
다른 두 가지 메커니즘을 사용 하 여 hello 리소스 사용 가능한 tooa 데이터베이스를 관리 하는 azure SQL 데이터베이스: **리소스 거 버 넌 스** 및 **제한을 적용**합니다. 이 항목에서는 리소스 관리의 다음 두 주요 영역을 설명합니다.

## <a name="resource-governance"></a>리소스 관리
Hello Basic, Standard, Premium 및 RS Premium 서비스 계층의 hello 디자인 목표 중 하나는 Azure SQL 데이터베이스 toobehave에 대 한 hello 데이터베이스가 다른 데이터베이스에서 격리 된 자체 컴퓨터에서 실행 되 고 처럼 합니다. 리소스 관리는 이러한 동작을 에뮬레이션합니다. 리소스 사용률에 도달 하면 hello 최대 사용 가능한 CPU, 메모리, 로그 I/O, 및 데이터 I/O 자원 배정 된 toohello 데이터베이스 리소스 관리 큐 쿼리 실행에 hello 집계 toohello 큐에 대기 되었을 때 쿼리 확보 하는 리소스를 할당 합니다.

으로 전용 컴퓨터에서 현재 실행 중인 쿼리, 실행 시간이 더 길어져의 모든 사용 가능한 리소스로 결과 사용 하 여 유발할 hello 클라이언트에서 명령 제한 시간입니다. 적극적인 다시 시도 논리를 응용 프로그램과 빈도가 높은 사용 하 여 hello 데이터베이스에 대 한 쿼리를 실행 하는 응용 프로그램 hello 동시 요청 한도 도달한 경우 tooexecute 새 쿼리를 시도할 때 오류 메시지를 발생할 수 있습니다.

### <a name="recommendations"></a>권장 사항:
Hello 데이터베이스의 최대 사용률 근처에 도달 하면 hello 리소스 사용률 및 쿼리의 평균 응답 시간 hello 모니터링 합니다. 쿼리 대기 시간이 높아졌을 때 일반적으로 세 가지 옵션이 있습니다.

1. 들어오는 요청 toohello 데이터베이스 tooprevent 제한 시간 및 hello 누적을 요청의 hello 수를 줄입니다.
2. 더 높은 성능 수준 toohello 데이터베이스를 할당 합니다.
3. 각 쿼리의 쿼리 tooreduce hello 리소스 사용률을 최적화 합니다. 자세한 내용은 참조 hello hello Azure SQL 데이터베이스 성능 지침 문서에 대 한 쿼리 튜닝/힌트 섹션.

## <a name="enforcement-of-limits"></a>제한 적용
CPU, 메모리, 로그 I/O 및 데이터 I/O 이외의 리소스는 제한에 도달할 때 새 요청을 거부하여 적용합니다. Hello 구성 된 최대 크기 제한, 삽입 및 업데이트 증가 하는 데이터베이스에 도달 하면 select 및 삭제 toowork 계속 하는 동안 데이터 크기 실패 합니다. 클라이언트는 수신는 [오류 메시지가](sql-database-develop-error-messages.md) 따라 hello 제한에 도달 했습니다.

예를 들어 hello tooa SQL 데이터베이스 연결 수와 hello 처리할 수 있는 동시 요청 수가 제한 됩니다. SQL 데이터베이스 연결 toohello 데이터베이스 toobe hello 수가 동시 요청 toosupport 연결 풀링을 hello 수보다 큰 있습니다. 사용할 수 있는 연결 수가 hello hello 응용 프로그램에서 쉽게 제어할 수, 하는 동안 병렬 요청 hello 수는 종종 시간 쉽다는 점 tooestimate 및 toocontrol 합니다. 특히 하는 동안 최대 부하 hello 응용 프로그램 너무 많은 요청을 보냅니다 또는 hello 데이터베이스는 리소스 한계에 도달 하 고 시작 시간이 길어져 작업자 스레드 toolonger 실행 되는 쿼리 인해 오류가 발생할 수 있습니다.

## <a name="service-tiers-and-performance-levels"></a>서비스 계층 및 성능 수준
단일 데이터베이스 및 탄력적 풀 모두에 대한 서비스 계층과 성능 수준이 있습니다.

### <a name="single-databases"></a>단일 데이터베이스
단일 데이터베이스에 대 한 데이터베이스의 hello 제한 hello 데이터베이스 서비스 계층과 성능 수준에 따라 정의 됩니다. 다음 표에서 hello 다양 한 성능 수준에서 데이터베이스를 Basic, Standard, Premium 및 프리미엄 RS의 hello 특성을 설명 합니다.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> P11 및 P15 성능 수준을 사용 하는 고객의 추가 요금 없이 포함된 저장소 too4 TB를 차지할 수 있습니다. 이 4TB 옵션은 hello 다음 영역에서에서 찾을 수 없습니다: 미국 East2, 미국 서 부, 미국 정부 기관용 버지니아, 서 부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 중앙 캐나다 및 캐나다 동부 합니다.
>

### <a name="elastic-pools"></a>탄력적 풀
[탄력적 풀](sql-database-elastic-pool.md) hello 풀의 데이터베이스 간에 리소스를 공유 합니다. 다음 표에서 hello Basic, Standard, Premium 및 프리미엄 RS 탄력적 풀의 hello 특성을 설명 합니다.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Hello 이전 표에 나열 된 각 리소스의 확장 된 정의 참조의 hello 설명 [서비스 계층 기능 및 제한](sql-database-performance-guidance.md#service-tier-capabilities-and-limits)합니다. 서비스 계층에 대한 개요는 [Azure SQL 데이터베이스 서비스 계층 및 성능 수준](sql-database-service-tiers.md)을 참조하세요.

## <a name="other-sql-database-limits"></a>기타 SQL 데이터베이스 제한
| 영역 | 제한 | 설명 |
| --- | --- | --- |
| 구독당 자동화된 내보내기를 사용하는 데이터베이스 |10 |자동화 된 내보내기 SQL 데이터베이스를 백업 하기 위한 사용자 지정 일정 toocreate를 허용 합니다. 이 기능은 미리 보기 hello 2017 년 3 월 1에 종료 됩니다.  |
| 서버당 데이터베이스 |Too5000를 |Too5000를 데이터베이스 서버 사용자별로 허용 됩니다. |
| 서버당 DTU |45000 |독립 실행형 데이터베이스 및 탄력적 풀을 프로비전하는 데 서버당 45,000개의 DTU가 허용됩니다. 독립 실행형 데이터베이스 및 서버 당 허용 되는 풀의 총 hello hello 서버 Dtu 수로만 제한 됩니다.  

> [!IMPORTANT]
> Azure SQL Database 자동화된 내보내기는 현재 미리 보기이며 및 2017년 3월 1일에 사용이 중지됩니다. 2016 년 12 월 1 일 시작 더 이상 됩니다 모든 SQL 데이터베이스에서 수 tooconfigure 자동화 된 내보내기. 모든 기존 자동화 된 내보내기 작업 toowork 2017 년 3 월 1 일 때까지 계속 합니다. 2016 년 12 월 1 일 후 사용할 수 있습니다 [장기 백업 보존](sql-database-long-term-retention.md) 또는 [Azure 자동화](../automation/automation-intro.md) tooarchive SQL 데이터베이스를 정기적으로 사용자가 선택한 tooa 일정에 따라 주기적으로 PowerShell을 사용 합니다. 예제 스크립트에 대 한 hello를 다운로드할 수 있습니다 [샘플 GitHub에서 스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)합니다.
>


## <a name="resources"></a>리소스
[Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)

[Azure SQL 데이터베이스 서비스 계층 및 성능 수준](sql-database-service-tiers.md)

[SQL 데이터베이스 클라이언트 프로그램에 대한 오류 메시지](sql-database-develop-error-messages.md)
