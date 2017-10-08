---
title: "Azure SQL 데이터베이스에서 쿼리 저장소 aaaOperating"
description: "Toooperate Azure SQL 데이터베이스에서 쿼리 저장소를 hello 하는 방법에 대해 알아봅니다"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>운영 hello Azure SQL 데이터베이스에서 쿼리 저장소
Azure의 쿼리 저장소는 모든 쿼리에 대한 자세한 기록 정보를 지속적으로 수집하고 제공하는, 완전히 관리되는 데이터베이스 기능입니다. 쿼리 저장소에 대 한 유사한 tooan 비행기 비행 데이터 레코더 크게 간소화 하 쿼리 성능 문제 해결에 대 한 클라우드 둘 다 고 온-프레미스 고객으로 생각할 수 있습니다. 이 문서는 Azure의 쿼리 저장소 운영에 대한 구체적인 측면을 설명합니다. 미리 수집된 쿼리 데이터를 사용하면, 성능 문제를 신속하게 진단하고 해결할 수 있기 때문에 업무에 더 많은 시간을 집중할 수 있습니다. 

쿼리 저장소는 2015년 11월부터 Azure SQL 데이터베이스에서 [전세계적으로 사용할 수 있습니다](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) . 쿼리 저장소는 성능 분석과 같은 기능을 튜닝에 대 한 hello foundation [SQL 데이터베이스 관리자 및 성능 대시보드](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)합니다. 이 문서를 게시의 hello 시점에서 쿼리 저장소가 실행 되 고 azure에서 200, 000 개 이상의 사용자 데이터베이스에 중단 없이 몇 개월 동안와 관련 된 쿼리 정보를 수집 합니다.

> [!IMPORTANT]
> Microsoft는 모든 Azure SQL 데이터베이스 (기존 및 새)에 대 한 쿼리 저장소 활성화 hello 프로세스에 있습니다. 
> 
> 

## <a name="optimal-query-store-configuration"></a>최적인 쿼리 저장소 구성
이 섹션에서는 최적의 구성 되는 기본값을 디자인 된 tooensure 안정적으로 작업 한 hello 쿼리 저장소와 종속 기능의 같은 설명 [SQL 데이터베이스 관리자 및 성능 대시보드](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)합니다. 기본 구성은 지속적인 데이터 수집을 위해 최적화됩니다(예: OFF/READ_ONLY 상태에 소요되는 시간 최소화).

| 구성 | 설명 | 기본값 | 주석 |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |쿼리 저장소는 z 고객 데이터베이스 내부에서 사용할 수 있는 hello 데이터 공간에 대 한 hello 제한을 지정 합니다. |100 |새 데이터베이스에 적용 |
| INTERVAL_LENGTH_MINUTES |쿼리 계획에 대해 수집된 런타임 통계가 집계되고 지속되는 기간의 규모를 정의합니다. 모든 활성 쿼리 계획은 이 구성을 통해 정의된 기간에 대해 최대 하나의 행을 갖습니다. |60 |새 데이터베이스에 적용 |
| STALE_QUERY_THRESHOLD_DAYS |Hello 지속형된 런타임 통계와 비활성 쿼리의 보존 기간을 제어 하는 시간 기반 정리 정책 |30 |새 데이터베이스 및 이전 기본값을 포함하는 데이터베이스에 적용(367) |
| SIZE_BASED_CLEANUP_MODE |쿼리 저장소 데이터 크기가 hello 제한에 도달할 때 자동 데이터 정리 위치를 받는지 여부를 지정합니다 |AUTO |모든 데이터베이스에 적용 |
| QUERY_CAPTURE_MODE |모든 쿼리를 추적할지 또는 쿼리의 하위 집합만 추적할지를 지정합니다. |AUTO |모든 데이터베이스에 적용 |
| FLUSH_INTERVAL_SECONDS |Toodisk에 플러시하기 전에 캡처된 런타임 통계는 메모리에 보관 되는 최대 기간을 지정 합니다. |900 |새 데이터베이스에 적용 |
|  | | | |

> [!IMPORTANT]
> 이러한 기본값 hello (이전 중요 한 참고 참조)는 모든 Azure SQL 데이터베이스에서 쿼리 저장소 활성화의 최종 단계에서 자동으로 적용 됩니다. 이 표시등이, 이후 Azure SQL 데이터베이스 변경 하지 않으므로 고객에 의해 설정 되는 구성 값 부정적인 영향을 받기 한 기본 워크 로드 또는 hello 쿼리 저장소의 신뢰할 수 있는 작업 하지 않는 한 합니다.
> 
> 

사용자 지정 설정으로 toostay 하려는 경우 사용할 [쿼리 저장소 옵션으로 ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) toorevert 구성 toohello 이전 상태입니다. 체크 아웃 [hello 쿼리 저장소로 모범 사례](https://msdn.microsoft.com/library/mt604821.aspx) toolearn 어떻게 상위 순서의 최적 구성 매개 변수를 선택 합니다.

## <a name="next-steps"></a>다음 단계
[SQL 데이터베이스 성능 Insight](sql-database-performance.md)

## <a name="additional-resources"></a>추가 리소스
자세한 내용은 체크아웃 문서 다음 hello에 대 한:

* [데이터베이스에 대한 블랙박스](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Hello 쿼리 저장소를 사용 하 여 성능 모니터링](https://msdn.microsoft.com/library/dn817826.aspx)
* [쿼리 저장소 사용 시나리오](https://msdn.microsoft.com/library/mt614796.aspx)
* [Hello 쿼리 저장소를 사용 하 여 성능 모니터링](https://msdn.microsoft.com/library/dn817826.aspx) 

