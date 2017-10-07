---
title: "aaaMonitor 하 고 Azure SQL 데이터베이스-성능 향상 | Microsoft Docs"
description: "Azure SQL 데이터베이스 성능을 제공 하는 hello 도구 toohelp 현재 쿼리 성능을 향상 시킬 수 있는 영역을 식별 합니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>성능 모니터링 및 향상
Azure SQL Database는 데이터베이스의 잠재적 문제를 파악하고 지능형 튜닝 작업 및 권장 사항을 제공하여 워크로드 성능을 높일 수 있는 작업을 권장합니다.

tooreview 데이터베이스 성능, 사용 하 여 hello **성능** hello 개요 페이지에서 타일 또는 너무 아래로 이동 "지원 + 문제 해결" 섹션:

   ![성능 보기](./media/sql-database-performance/entries.png)

Hello "지원 + 문제 해결" 섹션의 다음 페이지 hello를 사용할 수 있습니다.


1. [성능 개요](#performance-overview) toomonitor 데이터베이스 성능. 
2. [성능 권장 사항](#performance-recommendations) 워크 로드의 성능을 향상 시킬 수 있는 toofind 성능 권장 사항입니다.
3. [Query Performance Insight](#query-performance-insight) toofind 상위 리소스 소비 쿼리 합니다.
4. [자동 튜닝](#automatic-tuning) toolet Azure SQL 데이터베이스는 데이터베이스를 자동으로 최적화 합니다.

## <a name="performance-overview"></a>성능 개요
이 보기에서는 데이터베이스 성능에 대한 요약을 제공하여 성능 튜닝 및 문제 해결에 도움이 됩니다. 

![성능](./media/sql-database-performance/performance.png)

* hello **권장 사항을** 는 튜닝 권장 구성 데이터베이스에 대 한 분석을 제공 하는 타일 (상위 3 개 권장 사항을 표시 되어 있는 경우 더 많은). 클릭 하면이 타일 이동 너무**[성능 권장 사항](#performance-recommendations)**합니다. 
* hello **활동 튜닝** 타일은 진행 중인 작업과 데이터베이스에 대 한 작업을 튜닝 작업을 튜닝의 hello 기록을를 쉽게 확인할 수 있도록, 완료 된 hello에 대 한 요약을 제공 합니다. 이 타일을 클릭 하면 toohello 전체 데이터베이스에 대 한 기록 보기가 튜닝 이동 합니다.
* hello **자동 조정** 타일 표시 hello [자동 조정 구성을](sql-database-automatic-tuning-enable.md) (튜닝 옵션을 자동으로 적용 된 tooyour 데이터베이스) 데이터베이스에 대 한 합니다. 이 타일을 클릭 하면 hello 자동화 구성 대화 상자를 엽니다.
* hello **데이터베이스 쿼리에** 타일 표시 hello hello 쿼리 성능 (전체 DTU 사용량 및 상위 리소스 소비 쿼리) 데이터베이스에 대 한 요약입니다. 클릭 하면이 타일 이동 너무**[Query Performance Insight](#query-performance-insight)**합니다.

## <a name="performance-recommendations"></a>성능 권장 사항
이 페이지는 데이터베이스의 성능을 향상시킬 수 있는 지능형 [튜닝 권장 사항](sql-database-advisor.md)을 제공합니다. 다음 권장 사항 유형의으로 hello이이 페이지에 표시 됩니다.

* 인덱스 toocreate 또는 삭제를 권장 합니다.
* Hello 데이터베이스에서 스키마 문제가 식별 되었을 때 권장 사항입니다.
* 쿼리가 매개 변수화된 쿼리에서 이점을 얻을 수 있는 경우 권장 사항.

![성능](./media/sql-database-performance/recommendations.png)

또한 지난 hello에 적용 되었던 작업이 튜닝의 전체 기록을 찾을 수 있습니다.

자세한 내용은 방법 toofind apply 성능 권장 사항에 [찾아 성능 권장 사항 적용](sql-database-advisor-portal.md) 문서.

## <a name="automatic-tuning"></a>자동 조정
Azure SQL Database는 자동으로 [성능 권장 사항](sql-database-advisor.md)을 적용하여 데이터베이스 성능을 튜닝할 수 있습니다. toolearn 더 읽기 [자동 튜닝 문서](sql-database-automatic-tuning.md)합니다. 읽기, tooenable [어떻게 tooenable 자동 튜닝](sql-database-automatic-tuning-enable.md)합니다.

## <a name="query-performance-insight"></a>Query Performance Insight
[Query Performance Insight](sql-database-query-performance.md) 있습니다 toospend 제공 하 여 데이터베이스 성능 문제 해결 시간이 줄어듭니다.

* 데이터베이스 리소스(DTU) 사용에 대한 보다 자세한 정보를 확인합니다. 
* hello 상위 CPU 소비 쿼리 성능 향상된을 위해 조정 될 수 있음. 
* 쿼리의 hello 세부 정보로 다운 기능 toodrill를 hello 합니다. 

  ![성능 대시보드](./media/sql-database-query-performance/performance.png)

Hello 문서의이 페이지에 대 한 자세한 내용을 보려면  **[어떻게 toouse Query Performance Insight](sql-database-query-performance.md)**합니다.

## <a name="additional-resources"></a>추가 리소스
* [단일 데이터베이스의 Azure SQL 데이터베이스 성능 지침](sql-database-performance-guidance.md)
* [탄력적 풀을 사용해야 하는 경우](sql-database-elastic-pool-guidance.md)

