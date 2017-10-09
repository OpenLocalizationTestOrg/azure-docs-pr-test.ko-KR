---
title: "aaaMigrate 기존 Azure 데이터 웨어하우스 toopremium 저장소 | Microsoft Docs"
description: "기존 데이터 웨어하우스 toopremium 저장소로 마이그레이션하기 위한 지침"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>데이터 웨어하우스 toopremium 저장소 마이그레이션
Azure SQL Data Warehouse는 최근에 도입된 [큰 성능 예측 가능성을 위한 Premium Storage][premium storage for greater performance predictability]입니다. Toopremium 저장소를 마이그레이션할 하는 기존 데이터 웨어하우스 표준 저장소에 현재 될 수 있습니다. 자동 마이그레이션의 이용할 수 있습니다 toocontrol 선호 하는 경우 또는 때 toomigrate (하는 과정이 가동 중지 시간이)를 할 수 있는 마이그레이션 직접 hello 합니다.

둘 이상의 데이터 웨어하우스를 사용 하는 경우 사용 하 여 hello [일정 자동 마이그레이션] [ automatic migration schedule] toodetermine 마이그레이션하면도 됩니다.

## <a name="determine-storage-type"></a>저장소 유형 결정
Hello 날짜를 수행 하기 전에 데이터 웨어하우스를 만든 경우 현재 표준 저장소를 사용 하는 것입니다.

| **지역** | **이 날짜 이전에 만든 데이터 웨어하우스** |
|:--- |:--- |
| 오스트레일리아 동부 |Premium Storage를 아직 사용할 수 없음 |
| 중국 동부 |2016년 11월 1일 |
| 중국 북부 |2016년 11월 1일 |
| 독일 중부 |2016년 11월 1일 |
| 독일 북동부 |2016년 11월 1일 |
| 인도 서부 |Premium Storage를 아직 사용할 수 없음 |
| 일본 서부 |Premium Storage를 아직 사용할 수 없음 |
| 미국 중북부 |2016년 11월 10일 |

## <a name="automatic-migration-details"></a>자동 마이그레이션 세부 정보
기본적으로 마이그레이션할 예정 데이터베이스를 해당 지역의 현지 시간으로 오전 6 시와 오후 6시 사이 hello 중 [일정 자동 마이그레이션][automatic migration schedule]합니다. Hello 마이그레이션하는 동안 기존 데이터 웨어하우스의 사용할 수 없게 됩니다 수 있습니다. hello 마이그레이션 데이터 웨어하우스 당 저장소 테라바이트 당 약 1 시간이 걸립니다. Hello 자동 마이그레이션의 한 부분에 청구 되지 됩니다.

> [!NOTE]
> Hello 마이그레이션이 완료 되 면 다시 온라인이 고 사용 가능한 데이터 웨어하우스가 됩니다.
>
>

Microsoft는 hello 단계 toocomplete hello 마이그레이션 (사용자의 모든 참여 필요 하지 않습니다) 하는 데입니다. 이 예제에서는 표준 저장소의 기존 데이터 웨어하우스의 이름이 현재 "MyDW"라고 가정합니다.

1. 너무의 이름을 "MyDW" Microsoft "MyDW_DO_NOT_USE_ [타임 스탬프]"입니다.
2. Microsoft는 "MyDW_DO_NOT_USE_[타임스탬프]"를 일시 중지합니다. 이 시간 동안 백업이 수행됩니다. 이 과정에서 문제가 발생한 경우 여러 일시 중지 및 다시 시작이 표시될 수 있습니다.
3. Microsoft "MyDW" 프리미엄 저장소에 hello 백업에서 2 단계에서 수행 되 라는 새 데이터 웨어하우스를 만듭니다. "MyDW" hello 복원이 완료 된 후까지 표시 되지 않습니다.
4. (일시 중지 된 또는 현재) "MyDW" toohello 동일한 데이터 웨어하우스 단위와 상태를 반환 hello 복원이 완료 되 면 hello 마이그레이션을 시작 하기 전에 있었던 합니다.
5. Hello 마이그레이션이 완료 된 후 Microsoft "MyDW_DO_NOT_USE_ [타임 스탬프]"를 삭제 합니다.

> [!NOTE]
> hello 다음 설정으로 이전 되지 않습니다 hello 마이그레이션의 일환으로:
>
> * Hello 데이터베이스 수준 감사 toobe 다시 활성화 해야 합니다.
> * Hello 데이터베이스 수준 방화벽 규칙 toobe 다시 추가 해야 합니다. Hello 서버 수준 방화벽 규칙의 영향을 받지 않습니다.
>
>

### <a name="automatic-migration-schedule"></a>자동 마이그레이션 일정
자동 마이그레이션 중단 일정에 따라 hello 중 오후 6시 및 오전 6시 (현지 시간 / 지역당) 간에 발생 합니다.

| **지역** | **예상된 시작 날짜** | **예상된 종료 날짜** |
|:--- |:--- |:--- |
| 오스트레일리아 동부 |아직 결정되지 않음 |아직 결정되지 않음 |
| 중국 동부 |2017년 1월 9일 |2017년 1월 13일 |
| 중국 북부 |2017년 1월 9일 |2017년 1월 13일 |
| 독일 중부 |2017년 1월 9일 |2017년 1월 13일 |
| 독일 북동부 |2017년 1월 9일 |2017년 1월 13일 |
| 인도 서부 |아직 결정되지 않음 |아직 결정되지 않음 |
| 일본 서부 |아직 결정되지 않음 |아직 결정되지 않음 |
| 미국 중북부 |2017년 1월 9일 |2017년 1월 13일 |

## <a name="self-migration-toopremium-storage"></a>자동 마이그레이션 toopremium 저장소
작동 중단 시간이 발생 한 경우 toocontrol를 원하는 경우 hello 나오는 단계 toomigrate 기존 데이터 웨어하우스 표준 저장소 toopremium 저장소에 사용할 수 있습니다. 이 옵션을 선택 하는 경우에 해당 지역에서 hello 자동 마이그레이션을 시작 하기 전에 hello 자체 마이그레이션을 완료 해야 합니다. 이렇게 하면 hello 자동 마이그레이션 충돌의 위험을 방지 하는 (toohello 참조 [일정 자동 마이그레이션][automatic migration schedule]).

### <a name="self-migration-instructions"></a>자체 마이그레이션 지침
데이터 웨어하우스 직접 hello 백업 및 복원 기능 toomigrate 합니다. hello 복원의 hello 마이그레이션 부분이 예상된 tootake 데이터 웨어하우스 당 저장소 테라바이트 당 약 1 시간입니다. 마이그레이션이 완료 된 후 이름과 같은 이름을 tookeep hello 원한다 면 hello에 따라 [마이그레이션하는 동안 단계 toorename][steps toorename during migration]합니다.

1. 데이터 웨어하우스를 [일시 중지][Pause]합니다. 자동 백업이 사용됩니다.
2. 가장 최근의 스냅숏에서 [복원][Restore]합니다.
3. 표준 저장소의 기존 데이터 웨어하우스를 삭제합니다. **Toodo을이 단계가 실패 하는 경우 데이터 웨어하우스 모두에 대 한 청구 됩니다.**

> [!NOTE]
> hello 다음 설정으로 이전 되지 않습니다 hello 마이그레이션의 일환으로:
>
> * Hello 데이터베이스 수준 감사 toobe 다시 활성화 해야 합니다.
> * Hello 데이터베이스 수준 방화벽 규칙 toobe 다시 추가 해야 합니다. Hello 서버 수준 방화벽 규칙의 영향을 받지 않습니다.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>마이그레이션 중 데이터 웨어하우스의 이름 바꾸기(선택 사항)
두 데이터베이스를 동일한 논리 서버가 하 여야 하는 hello hello 동일한 이름입니다. SQL 데이터 웨어하우스는 이제 hello 기능 toorename 데이터 웨어하우스를 지원합니다.

이 예제에서는 표준 저장소의 기존 데이터 웨어하우스의 이름이 현재 "MyDW"라고 가정합니다.

1. "MyDW" hello 다음 ALTER DATABASE 명령을 사용 하 여 이름을 바꿉니다. (이 예제에서는 합니다 이름을 바꾸지 "MyDW_BeforeMigration.")  이 명령은 모든 기존 트랜잭션을 중지 하 고 hello master 데이터베이스 toosucceed에서 수행 되어야 합니다.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. "MyDW_BeforeMigration"을 [일시 중지][Pause]합니다. 자동 백업이 사용됩니다.
3. [복원] [ Restore] 가장 최근 스냅숏의 hello 이름으로 새 데이터베이스에서 toobe (예: "MyDW")이 사용 됩니다.
4. "MyDW_BeforeMigration"을 삭제합니다. **Toodo을이 단계가 실패 하는 경우 데이터 웨어하우스 모두에 대 한 청구 됩니다.**


## <a name="next-steps"></a>다음 단계
데이터 웨어하우스의 hello 기본 아키텍처에서 데이터베이스 blob 파일의 횟수가 증가 레이블에도, hello로 toopremium 저장소를 변경 합니다. 이러한 변경의 toomaximize hello 성능 이점을 hello 다음 스크립트를 사용 하 여 클러스터형된 columnstore 인덱스 다시 작성 합니다. hello 스크립트는 기존 데이터 toohello 추가 blob 중 일부를 강제 적용 하 여 작동 합니다. 조치를 취하지 테이블에 더 많은 데이터를 로드 하는 대로 hello 데이터 시간에 따라 재배포할 자연스럽 게 됩니다.

**필수 조건:**

- hello 데이터 웨어하우스를 실행할지 (1, 000 데이터 웨어하우스 단위 포함) 이상 (참조 [배율 계산 능력이][scale compute power]).
- hello hello 스크립트를 실행 하는 사용자에에서 있어야 hello [mediumrc 역할] [ mediumrc role] 이상. 사용자 toothis 역할 tooadd hello 다음을 실행 합니다.````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

데이터 웨어하우스와 문제가 발생 하는 경우 [지원 티켓을 만드세요] [ create a support ticket] hello 가능한 원인으로 "마이그레이션 toopremium storage"를 참조 합니다.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
