---
title: "보존 정책 사용 하 여 임시 테이블에서 한 aaaManage 기록 데이터 | Microsoft Docs"
description: "자세한 내용은 방법 toouse 임시 보존 정책 tookeep 기록 데이터 제어 합니다."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>재방문 주기 정책 사용하여 Temporal Tables에서 과거 데이터 관리
임시 테이블은 특히 과거 데이터를 장기간 보관할 경우 일반 테이블 보다 데이터베이스 크기를 늘릴 수 있습니다. 따라서, 기록 데이터에 대 한 보존 정책 계획 및 모든 임시 테이블의 hello 수명 주기 관리의 중요 한 측면입니다. Azure SQL Database의 임시 테이블은 이 작업을 수행하는 데 유용한 사용하기 쉬운 재방문 주기 메커니즘과 함께 제공됩니다.

임시 기록 보존 toocreate 유연한 에이징 정책은 사용자가 hello 개별 테이블 수준에서 구성할 수 있습니다. 임시 보존이 적용 하는 것은 간단: 하나의 매개 변수 toobe 테이블 스키마를 만들거나 변경 하는 동안 설정 해야 합니다.

재방문 주기 정책을 정의하고 나면 Azure SQL Database는 자동 데이터 정리에 적합한 과거 행이 있는지 정기적으로 확인하기 시작합니다. 일치 하는 행 식별 하 고 hello 기록 테이블에서 해당 제거 예약 되 고 hello 시스템에서 실행 하는 hello 백그라운드 작업에서 투명 하 게 발생 합니다. Hello 기록 테이블의 행에 대 한 나이 조건은 SYSTEM_TIME 기간 종료를 나타내는 hello 열에 따라 확인 됩니다. 보존 기간 등 설정 된 경우 toosix 정리에 대 한 적격 테이블 행 hello 다음 조건을 충족 하는 월:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

앞 예제는 hello, 것으로 가정 하는 **ValidTo** toohello SYSTEM_TIME 기간 종료 열에 해당 합니다.

## <a name="how-tooconfigure-retention-policy"></a>어떻게 tooconfigure 보존 정책을?
임시 테이블에 대 한 보존 정책을 구성 하기 전에 먼저 임시 기록 보존 설정 되어 있는지 확인 *hello 데이터베이스 수준에서*합니다.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

플래그 데이터베이스 **is_temporal_history_retention_enabled** 기본적으로 집합 tooON 이지만 사용자가 ALTER DATABASE 문을 사용 하 여 변경할 수 있습니다. 자동으로 후 tooOFF 집합은 또한 [지정 시간 복원](sql-database-recovery-using-backups.md) 작업 합니다. 프로그램 데이터베이스에 대 한 임시 기록 보존 정리 tooenable hello 문 다음 실행 합니다.

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> **is_temporal_history_retention_enabled**이 OFF가 되더라도 임시 테이블에 대한 재방문 주기는 구성할 수 있지만 그 경우 오래된 행에 대한 자동 정리는 트리거되지 않습니다.
> 
> 

보존 정책은 hello HISTORY_RETENTION_PERIOD 매개 변수 값을 지정 하 여 테이블을 만들 때 구성 됩니다.

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

Azure SQL 데이터베이스를 통해 toospecify 보존 기간이 다른 시간 단위를 사용 하 여: 일, 주, 월 및 연도입니다. HISTORY_RETENTION_PERIOD가 생략되면 재방문 주기를 INFINITE로 가정합니다. 또한 INFINITE 키워드를 명시적으로 사용할 수 있습니다.

일부 시나리오에서는 테이블을 만든 후 tooconfigure 보존을 할 수 있습니다 또는 toochange 이전에 구성 된 값입니다. 이 경우 ALTER TABLE 문을 사용합니다.

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> SYSTEM_VERSIONING tooOFF 설정 *유지 하지 않습니다* 보존 기간 값입니다. HISTORY_RETENTION_PERIOD 없이 SYSTEM_VERSIONING tooON 설정에 지정 된 명시적으로 결과 hello 무한 보존 기간입니다.
> 
> 

tooreview hello 보존 정책의 현재 상태를 사용 하 여 hello 다음 쿼리 개별 테이블에 대 한 보존 기간이 hello 데이터베이스 수준에서 해당 조인 임시 보존 사용 플래그:

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>SQL Database가 오래된 행을 삭제하는 방법은?
hello 정리 프로세스는 hello 기록 테이블의 hello 인덱스 레이아웃에 따라 다릅니다. 것이 중요 한 toonotice 하 *유한 보존 정책을 구성한를 포함할 수 있습니다 (B-트리 또는 columnstore) 클러스터형된 인덱스를 가진 기록 테이블*합니다. 백그라운드 작업을 한정 된 보존 기간으로 모든 임시 테이블에 대 한 오래 된 데이터 정리 tooperform 만들어집니다.
Hello 클러스터형된 rowstore (btree) 인덱스에 대 한 정리 논리 데이터베이스 로그와 I/O 하위 시스템에 대 한 압력을 최소화 합니다. 더 작은 청크 (위쪽 too10K)의 오래 된 행을 삭제 합니다. 정리 논리를 활용 하지만 B-트리 인덱스, 보존 기간을 모뎀과 보장할 수 없는 보다 오래 된 hello 행에 대 한 삭제의 순서를 필요 합니다. 따라서 *응용 프로그램에서 정리 순서 hello에 모든 종속성을 사용 하지 않는*합니다.

hello hello clustered columnstore에 대 한 정리 작업을 제거 전체 [행 그룹](https://msdn.microsoft.com/library/gg492088.aspx) 한 번에 (일반적으로 포함 되어 각 행의 1 백만), 높은 속도로 기록 데이터가 생성 되는 경우에 특히 매우 효율적인를 합니다.

![클러스터형 columnstore 재방문 주기](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

클러스터형 columnstore 인덱스는 뛰어난 데이터 압축 및 효율적인 재방문 주기 정리를 자랑하기 때문에 워크로드가 빠른 시간 내에 대량의 과거 데이터를 생성하는 시나리오인 경우 완벽한 선택입니다. 해당 패턴은 변경 내용 추적 및 감사, 추세 분석 또는 IoT 데이터 수집에 대해 [임시 테이블을 사용하는 집약적 트랜잭션 처리 워크로드](https://msdn.microsoft.com/library/mt631669.aspx)에 일반적입니다.

## <a name="index-considerations"></a>인덱스 고려 사항
rowstore 클러스터형된 인덱스가 있는 테이블에 대 한 hello 정리 태스크는 인덱스 toostart hello 열 해당 hello 종료가 SYSTEM_TIME 기간이 필요합니다. 이러한 인덱스가 없는 경우 한정된 재방문 주기 기간을 구성할 수 없습니다.

*Msg 13765, 수준 16, 상태 1 <br> </br> temporalstagetestdb.dbo.WebsiteUserInfo' 시스템 버전 임시 테이블'에서 실패 유한 보존 기간 설정 hello 기록 테이블 ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' 필요한 클러스터형된 인덱스가 포함 되지 않습니다. 클러스터형된 columnstore 또는 SYSTEM_TIME 끝과 일치 하는 hello 열으로 시작 하는 B-트리 인덱스를 만드는 것이 좋습니다 hello 기록 테이블에서 기간입니다.*

이미 Azure SQL 데이터베이스에서 만든 기본 기록 테이블 hello toonotice에 보존 정책에 대 한 호환 되는 인덱스는 클러스터형 유용 합니다. 한정 된 보존 기간 설정 된 테이블에서 해당 인덱스 tooremove를 시도 하면 다음 오류가 hello로 작업이 실패 합니다.

*Msg 13766, 수준 16, 상태 1 <br> </br> 오래 된 데이터의 자동 정리에 사용 되는 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' hello 클러스터형된 인덱스를 삭제할 수 없습니다. 이 인덱스 toodrop 필요한 경우 hello 해당 시스템 버전 임시 테이블에서 설정 HISTORY_RETENTION_PERIOD tooINFINITE를 것이 좋습니다.*

오름차순 (hello end 기간 열에 순서 대로)는 항상 hello hello SYSTEM_ 독점적으로 hello 기록 테이블을 채울 때 hello에 기록 행이 삽입 hello 클러스터형된 columnstore 인덱스에는 정리 최적으로 작동 VERSIONIOING 메커니즘입니다. 기간 열 (수도 있음 hello 경우 기존 기록 데이터를 마이그레이션하는 경우)의 끝으로 hello 기록 테이블의 행은 정렬 되지 다시 만들어야 tooachieve 최적 정렬 제대로 되 B-트리 rowstore 인덱스를 기반으로 클러스터형된 columnstore 인덱스 성능을 제공 합니다.

정렬 자연스럽 게 hello 시스템 버전 관리 작업에 의해 적용 된 hello 행 그룹에 변경 될 수 있으므로 hello 유한 보존 기간으로 hello 기록 테이블에서 클러스터형된 columnstore 인덱스를 다시 작성 하지 마십시오. Hello 기록 테이블에서 클러스터형된 columnstore 인덱스 toorebuild 필요한 않은 경우 일반 데이터 정리에 필요한 hello 행 그룹의 순서를 유지 하면서 규격 B-트리 인덱스를 기반으로 다시 생성 하 여 만듭니다. hello 보장된 데이터 순서 없이 열 인덱스 클러스터링 기존 기록 테이블을 임시 테이블을 만들면 같은 방법을 수행 해야 합니다.

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

한정 된 보존 기간을 hello 클러스터형된 columnstore 인덱스가 있는 hello 기록 테이블에 대해 구성 된 경우 해당 테이블에 추가 비클러스터형 btree 인덱스를 만들 수 없습니다.

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

다음 오류가 hello로 문 위의 시도 tooexecute는 실패 합니다.

*Msg 13772, Level 16, State 1 <br></br> 임시 기록 테이블인 'WebsiteUserInfoHistory'에는 한정된 재방문 주기 기간 및 클러스터형 columnstore 인덱스가 정의되어 있기 때문에 비클러스터형 인덱스를 생성할 수 없습니다.*

## <a name="querying-tables-with-retention-policy"></a>재방문 주기 정책을 사용한 테이블 쿼리
Hello 임시 테이블에서 모든 쿼리가 자동으로 hello 정리 작업에서 오래 된 행을 삭제할 수 하기 때문에 무한 보존 정책, tooavoid 예측할 수 없는 결과 일치 하지 않는 결과 비교 하는 기록 행을 필터링 *시간 및 특정 시점 임의의 순서가*합니다.

hello 다음 다음과 같은 순서로 hello 쿼리 계획에 대 한 단순 쿼리

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

tooend 기간 열 (ValidTo)의 hello (강조 표시) hello 기록 테이블에서 데이터 Clustered Index Scan 연산자에 적용 하는 hello 쿼리 계획에 추가 필터를 포함 합니다. 이 예는 한 달 재방문 주기 기간이 WebsiteUserInfo 테이블에 설정되었다고 가정합니다.

![재방문 주기 쿼리 필터](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

그러나 기록 테이블을 직접 쿼리한다면 지정된 재방문 주기 기간보다 오래된 행을 볼 수도 있을테지만 쿼리 결과가 반복되리라는 보장은 없습니다. hello 다음 다음과 같은 순서로 hello 쿼리에 대 한 쿼리 실행 계획 hello 기록 테이블에 추가 필터를 적용 하지 않고

![재방문 주기 필터를 사용하지 않은 기록 쿼리](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

일관되지 않거나 예측할 수 없는 결과가 나올 수도 있기 때문에 재방문 주기 기간을 초과하여 기록 테이블을 읽는 비즈니스 논리에 의존하지 마십시오. 임시 테이블에 있는 데이터를 분석하려면 FOR SYSTEM_TIME 절을 사용한 임시 쿼리를 하는 것이 좋습니다.

## <a name="point-in-time-restore-considerations"></a>특정 시점 복원 고려 사항
하 여 새 데이터베이스를 만들 때 [기존 데이터베이스 tooa 특정 지정 시간으로 복원](sql-database-recovery-using-backups.md), 있기 임시 보존 hello 데이터베이스 수준에서 사용할 수 없습니다. (**is_temporal_history_retention_enabled** 플래그가 설정 tooOFF). 이 기능을 통해 tooexamine tooquery 도달 하기 전에 행 오래 된 하는 관계 없이 복원 시 모든 기록 행은 제거 하면 해당 합니다. 도 사용할 수 있습니다*구성 된 보존 기간 이후에도 기록 데이터를 검사*합니다.

임시 테이블의 재방문 주기가 1 MONTH로 지정되었다고 가정해 봅시다. Premium 서비스 계층에서 데이터베이스를 만든 경우에 hello 과거 인하면에서 too35 일을 hello 데이터베이스 상태와 데이터베이스 복사본 수 toocreate 것입니다. 효과적으로 수 있게 해 주는 사용자 들 두 일이 넘으면 hello 기록 테이블을 직접 쿼리하여 tooanalyze 기록 행.

Tooactivate 임시 보존 정리 하려는 경우 hello Transact SQL 문 지정 시간 복원은 후 다음을 실행 합니다.

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>다음 단계
응용 프로그램에서 임시 테이블 toouse 체크 아웃 방법을 toolearn [Azure SQL 데이터베이스에서 임시 테이블 시작](sql-database-temporal-tables.md)합니다.

방문 Channel 9 toohear는 [실제 고객 구현 임시 성공 스토리](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) 및 조사식은 [임시 데모 라이브](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)합니다.

Temporal Tables에 관한 자세한 내용은 [MSDN 설명서](https://msdn.microsoft.com/library/dn935015.aspx)를 참조하세요.

