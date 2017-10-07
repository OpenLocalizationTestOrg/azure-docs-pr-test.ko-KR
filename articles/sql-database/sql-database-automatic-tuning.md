---
title: "데이터베이스-aaaSQL 자동 튜닝 | Microsoft Docs"
description: "SQL 쿼리를 분석 하는 SQL 데이터베이스 및 automaticaly toouser 작업 부하에 맞게 변경 합니다."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>자동 조정

Azure SQL 데이터베이스는 hello 데이터베이스에서 실행 되 고 자동으로 hello 워크 로드의 성능이 향상 하는 hello 쿼리를 모니터링 하는 완전히 관리 되는 데이터 서비스. Azure SQL 데이터베이스에 자동으로 조정 하 고 사용 하 여 동적으로 hello 데이터베이스 tooyour 작업 쿼리의 성능을 향상 시킬 수 있는 기본 제공 intelligence 메커니즘이 있습니다. Azure SQL 데이터베이스의 자동 튜닝 hello 쿼리의 toooptimize 성능 Azure SQL 데이터베이스에 사용할 수 있는 가장 중요 한 기능 중 하나일 수 있습니다.

Hello 단계에 대 한이 문서를 너무 참조[자동 조정 기능 사용](sql-database-automatic-tuning-enable.md) Azure 포털 hello를 사용 하 여 합니다.

## <a name="why-automatic-tuning"></a>자동 조정을 사용하는 이유는 무엇입니까?

Hello 클래식 데이터베이스 관리의 주요 작업 중 하나는 모니터링 하 고 hello 작업을 식별 하는 중요 한 SQL 쿼리, tooimprove 성능 추가 해야 하며 거의 인덱스를 사용 하는 인덱스입니다. Azure SQL 데이터베이스 제공 면밀히 살펴보고 hello 쿼리 및 인덱스 toomonitor 해야 합니다. 그러나 지속적으로 데이터베이스를 모니터링하는 것은 특히 많은 데이터베이스를 처리할 때 힘들고 지루한 작업입니다. 거 대 한 수의 데이터베이스를 관리할 수 있습니다 불가능 한 toodo 효율적으로 된 경우에 모든 사용 가능한 도구 및 Azure SQL 데이터베이스 및 Azure 포털에서 제공 하는 보고서. 를 모니터링 대신 데이터베이스를 수동으로 조정 해야 할 hello 모니터링 및 튜닝 작업 tooAzure SQL 데이터베이스의 일부를 위임 자동 튜닝 기능을 사용 하 여 합니다. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>자동 조정의 작동 방식은 무엇입니까?

Azure SQL 데이터베이스에 지속적으로 hello 워크 로드의 특성을 인식 하 고 잠재적인 문제 및 향상 된 기능을 식별 하는 지속적인 성능 모니터링 및 분석 프로세스를 있습니다.

![자동 조정 프로세스](./media/sql-database-automatic-tuning/tuning-process.png)

이 프로세스에서는 Azure SQL 데이터베이스 toodynamically 어떤 인덱스 및 계획에 작업의 성능을 향상 시킬 수 및 인덱스를 검색 하 여 tooyour 작업 부하를 조정 작업을 영향을 줍니다. 이러한 결과에 따라 자동 조정은 작업의 성능을 향상시키는 조정 작업을 적용합니다. 또한 Azure SQL 데이터베이스의 변경 내용은 자동 튜닝 tooensure 워크 로드의 성능을 향상 시키는 후 성능을 지속적으로 모니터링 합니다. 성능을 향상시키지 않은 모든 작업은 자동으로 되돌려집니다. 이 확인 프로세스는 변경 내용은 자동 튜닝 작업 hello 성능이 저하 되지 않도록 보장 하는 주요 기능입니다.

Azure SQL Database에서 사용할 수 있는 두 가지 자동 조정 측면이 있습니다.

 -  데이터베이스에 추가되어야 하는 인덱스 및 제거되어야 하는 인덱스를 식별하는 **자동 인덱스 관리**
 -  문제가 있는 계획을 식별하고 SQL 계획 성능 문제를 해결하는 **자동 계획 수정**(출시 예정, SQL Server 2017에서 이미 사용 가능)

## <a name="automatic-index-management"></a>자동 인덱스 관리

Azure SQL Database에서 인덱스 관리는 Azure SQL Database에서 작업에 대해 학습하고 데이터가 항상 최적으로 인덱싱되도록 보장하기 때문에 매우 간단합니다. 적절한 인덱스 디자인은 작업의 최적의 성능을 위해 중요하고 자동 인덱스 관리는 인덱스를 최적화하는 데 도움이 될 수 있습니다. 자동 인덱스 관리 수 중 하나 인덱싱된 올바르지 않게 데이터베이스의 성능 문제를 해결 하거나 유지 관리 하 고 hello 기존 데이터베이스 스키마에 대 한 인덱스를 향상 시키십시오. 

### <a name="why-do-you-need-index-management"></a>인덱스 관리가 필요한 이유는 무엇입니까?

인덱스는 일부 hello 테이블에서 데이터를 읽는 쿼리 속도 그러나 데이터를 업데이트 하는 hello 쿼리 느려질 수 있습니다. Toocarefully 필요한 toocreate 인덱스 및 tooinclude에 필요한 열 인덱스 hello 시기를 분석 합니다. 일부 인덱스는 일정 시간이 지난 후 필요하지 않을 수 있습니다. 따라서 해야 tooperiodically 식별 하 고 모든 혜택을 가져오지 않는 hello 인덱스를 삭제 합니다. 무시 하면 사용 되지 않는 인덱스 hello, 데이터를 읽는 hello 쿼리에 아무런 장점 없이 데이터를 업데이트 하는 hello 쿼리의 성능을 줄일 수는 있습니다. 사용 되지 않는 인덱스도 추가 업데이트에 불필요 한 로깅 필요 하기 때문에 hello 시스템의 전반적인 성능에 영향을 합니다.

테이블에서 데이터를 읽고 업데이트에 미치는 영향이 최소화 하는 hello 쿼리의 성능을 개선 하는 인덱스의 hello 최적 집합을 찾기 연속 및 복잡 한 분석이 필요할 수 있습니다.

기본 제공 인텔리전스 및 쿼리를 분석, 될 현재 작업 프로그램에 대 한 최적의 인덱스를 식별 하는 고급 규칙을 사용 하는 azure SQL 데이터베이스 및 hello 인덱스 제거 될 수 있습니다. Azure SQL 데이터베이스를 통해 필요한 최소한의 데이터를 읽는 hello 쿼리를 최적화 하는 인덱스, 다른 쿼리를 hello에 미치는 영향을 최소화 하는 hello와 합니다.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>어떻게 tooidentify 프로그램 데이터베이스에서 변경 된 해당 필요 toobe 인덱스?

Azure SQL Database는 인덱스 관리 프로세스를 쉽게 해줍니다. Hello 수동 작업 분석 및 모니터링 하는 인덱스의 번거로운 프로세스, 대신 Azure SQL 데이터베이스 해당 작업을 분석, 새 인덱스를 사용 하면 더 빠르게 실행 될 수 있는 hello 쿼리 식별 및 사용 되지 않거나 중복 된 인덱스를 식별 합니다. [Azure Portal에서 인덱스 찾기 권장 사항](sql-database-advisor-portal.md)에서 변경되어야 하는 인덱스의 ID에 대한 자세한 정보를 찾아보세요.

### <a name="automatic-index-management-considerations"></a>자동 인덱스 관리 고려 사항

기본 제공 규칙 hello 데이터베이스의 hello 성능을 향상 하를 발견할 경우 자동으로 인덱스를 관리 하는 Azure SQL 데이터베이스를 할당할 수도 있습니다.

작업에는 Azure SQL 데이터베이스의 toocreate 필요한 인덱스 수 리소스를 소비 하며 시간적 워크 로드 성능에 영향 필요 합니다. 작업 성능에 Azure SQL 데이터베이스에서 인덱스 생성의 toominimize hello 영향 인덱스의 관리 작업에 대해 hello 적절 한 기간을 찾습니다. Hello 데이터베이스 리소스 tooexecute 워크 로드에서 요구 하는 경우 지연 되 고 hello 데이터베이스에 충분 한 경우 시작 작업을 튜닝 hello 유지 관리 태스크에 사용할 수 있는 사용 되지 않는 리소스입니다. 자동 인덱스 관리에서 중요 한 기능 중 하나는 hello 동작을 확인 합니다. Azure SQL 데이터베이스를 만들거나 인덱스를 삭제 때 모니터링 프로세스는 hello 동작 hello 성능 향상 되었는지 작업 tooverify 프로그램의 성능을 분석 합니다. 훨씬 향상 된 기능 –를 가져올 하지 않은 경우에 hello 작업 즉시 되돌아갑니다. 이러한 방식으로 Azure SQL Database는 자동 작업이 작업 성능에 부정적인 영향을 주지 않도록 합니다. 자동 튜닝 하 여 만든 인덱스는 hello 유지 관리 작업 hello 기본 스키마에 대 한 투명 합니다. 열 이름 바꾸기 또는 삭제와 같은 스키마 변경 내용은 자동으로 만든된 인덱스의 hello 중일 경우에 차단 되지 않습니다. Azure SQL Database에서 자동으로 생성된 인덱스는 관련 테이블 또는 열이 삭제될 때 즉시 삭제됩니다.

## <a name="automatic-plan-choice-correction"></a>자동 계획 선택 수정

자동 계획 수정은 오동작하는 SQL 계획을 식별하는 SQL Server 2017 CTP2.0에 추가된 새 자동 조정 기능입니다. 이 자동 조정 옵션은 Azure SQL Database에서 곧 제공됩니다. [SQL Server 2017에서 자동 조정](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning)에서 자세한 정보를 찾아보세요.

## <a name="next-steps"></a>다음 단계

- Azure SQL 데이터베이스 및 let 자동 튜닝 자동 tooenable 튜닝 기능이 완벽 하 게 작업을 관리할 참조 [자동 조정 기능 사용](sql-database-automatic-tuning-enable.md)합니다.
- 수동 튜닝 toouse 검토할 수 있습니다 [튜닝 권장 구성을 Azure 포털에서](sql-database-advisor-portal.md) 수동으로 hello 쿼리의 성능을 개선 하는 것을 적용 합니다.
