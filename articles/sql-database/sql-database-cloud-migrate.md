---
title: "aaaSQL 서버 데이터베이스 마이그레이션 tooAzure SQL 데이터베이스 | Microsoft Docs"
description: "대 한 SQL Server 데이터베이스 마이그레이션 tooAzure hello 클라우드의 SQL 데이터베이스에 알아봅니다. 데이터베이스 마이그레이션 도구 tootest 호환성 이전 toodatabase 마이그레이션을 사용 합니다."
keywords: "데이터베이스 마이그레이션, SQL Server 데이터베이스 마이그레이션, 데이터베이스 마이그레이션 도구, 데이터베이스 마이그레이션, SQL 데이터베이스 마이그레이션"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>SQL Server 데이터베이스 마이그레이션 tooSQL hello 클라우드의 데이터베이스
이 문서에서는 배웁니다 hello에 대 한 SQL Server 2005 또는 이후 데이터베이스 tooAzure SQL 데이터베이스에 대 한 두 가지 주요 방법입니다. hello 첫 번째 방법은 과정은 간단 하지만 기울여야 일부 hello 마이그레이션하는 동안 가능 상당한 가동 중지 시간. hello 두 번째 방법은 더 복잡 하지만 대체로 hello 마이그레이션하는 동안 가동 중지 시간을 제거 합니다.

두 경우 모두 tooensure 해야 해당 hello 원본 데이터베이스는 hello를 사용 하 여 Azure SQL 데이터베이스와 호환 [데이터 마이그레이션 길잡이 (DMA)](https://www.microsoft.com/download/details.aspx?id=53595)합니다. SQL 데이터베이스 v 12에 근접 하 고 [기능 패리티](sql-database-features.md) 문제 관련된 tooserver 수준 및 데이터베이스 간 작업 이외의 SQL Server를 사용 합니다. 데이터베이스 및 응용 프로그램을 사용 하는 [지원 되지 않는 함수 또는 부분적으로 지원](sql-database-transact-sql-information.md) 일부 필요 [toofix 혁신 이러한 비 호환성](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) 전에 hello SQL Server 데이터베이스를 마이그레이션할 수 있습니다.

> [!NOTE]
> Microsoft Access, Sybase, MySQL Oracle 및 DB2 tooAzure SQL 데이터베이스를 포함 하 여 SQL Server 이외 데이터베이스 참조 toomigrate [SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/)합니다.
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Hello 마이그레이션하는 동안 가동 중지 시간을 사용 하 여 방법 1: 마이그레이션

 약간의 가동 중지 시간이 허용되거나 나중에 마이그레이션할 수 있도록 프로덕션 데이터베이스의 테스트 마이그레이션을 수행하려면 이 방법을 사용하세요. 자습서를 보려면 [SQL Server 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)을 참조하세요.

hello 다음 목록에이 메서드를 사용 하 여 SQL Server 데이터베이스 마이그레이션에 대 한 일반적인 워크플로에 hello 있습니다.

  ![VSSSDT 마이그레이션 다이어그램](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. 최신 버전의 hello를 사용 하 여 호환성을 위해 hello 데이터베이스 평가 [데이터 마이그레이션 길잡이 (DMA)](https://www.microsoft.com/download/details.aspx?id=53595)합니다.
2. Transact-SQL 스크립트와 같은 필요한 수정 프로그램을 준비합니다.
3. Hello 원본 데이터베이스의 트랜잭션 측면에서 일관 된 복사-마이그레이션 및 확인 변경 되지 않습니다 추가 되 고 toohello 원본 데이터베이스 (또는 hello 마이그레이션을 완료 한 후에 수동으로 이러한 변경 내용을 적용할 수 있습니다). 많은 메서드 tooquiesce 클라이언트 연결 toocreating 사용 하지 않음으로써 얻게 데이터베이스는 한 [데이터베이스 스냅숏을](https://msdn.microsoft.com/library/ms175876.aspx)합니다.
4. Hello Transact SQL 스크립트 tooapply hello 수정 toohello 데이터베이스 복사본을 배포 합니다.
5. [내보내기](sql-database-export.md) 데이터베이스 복사본 tooa hello 합니다. 로컬 드라이브에 BACPAC 파일입니다.
6. [가져오기](sql-database-import.md) hello 합니다. 여러 BACPAC를 사용 하 여 새 Azure SQL 데이터베이스로 BACPAC 파일 hello 도구 최상의 성능을 위해 권장 되는 SQLPackage.exe와 도구를 가져옵니다.

### <a name="optimizing-data-transfer-performance-during-migration"></a>마이그레이션하는 동안 데이터 전송 성능 최적화 

다음 목록 hello hello 가져오기 프로세스 동안 최상의 성능을 위해 권장 사항을 포함 되어 있습니다.

* 예산 toomaximize hello 전송 성능의 허용 하는지 hello 가장 높은 서비스 수준 및 성능 계층을 선택 합니다. Hello 마이그레이션을 toosave money 완료 한 후 확장할 수 있습니다. 
* 사이의 hello 거리를 최소화 하면 됩니다. BACPAC 파일 및 hello 대상 데이터 센터
* 마이그레이션하는 동안 자동 통계 사용 안 함
* 파티션 테이블 및 인덱스
* 인덱싱된 뷰를 삭제하고 완료된 후 다시 만들기
* 기록 데이터를 거의 쿼리 tooanother 데이터베이스를 제거 하 고이 기록 데이터 tooa 별도 Azure SQL 데이터베이스를 마이그레이션하십시오. 그러면 [탄력적 쿼리](sql-database-elastic-query-overview.md)를 사용하여 이 기록 데이터를 쿼리할 수 있습니다.

### <a name="optimize-performance-after-hello-migration-completes"></a>Hello 마이그레이션을 완료 한 후 성능 최적화

[통계 업데이트](https://msdn.microsoft.com/library/ms187348.aspx) hello 마이그레이션이 완료 된 후 전체 검색으로 합니다.

## <a name="method-2-use-transactional-replication"></a>방법 2: 트랜잭션 복제 사용

여유가 없는 tooremove SQL Server 데이터베이스에서 프로덕션 hello 마이그레이션 진행 되는 동안, 경우에 마이그레이션 솔루션으로 SQL Server 트랜잭션 복제를 사용할 수 있습니다. 이 메서드를 소스 데이터베이스 hello 해야 toouse 충족 hello [트랜잭션 복제에 대 한 요구 사항](https://msdn.microsoft.com/library/mt589530.aspx) 와 Azure SQL 데이터베이스에 대 한 호환 되어야 합니다. AlwaysOn을 사용한 SQL 복제에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 복제 구성(SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server)을 참조하세요.

toouse이이 솔루션에서는 Azure SQL 데이터베이스도 구성한 toomigrate 한다고 구독자 toohello SQL Server 인스턴스를 합니다. hello 트랜잭션 복제 배포자가 데이터를 동기화 hello 데이터베이스 toobe 동기화 (hello 게시자)에서 새 트랜잭션을 계속 발생 합니다. 

트랜잭션 복제와 함께 모든 변경 내용 tooyour 데이터 또는 스키마에에서 표시 Azure SQL 데이터베이스. Hello 동기화가 완료 되 면 준비 toomigrate는 응용 프로그램 toopoint의 hello 연결 문자열을 변경 하 tooyour Azure SQL 데이터베이스입니다. 트랜잭션 복제 드레이닝하 왼쪽 변경 되 면 원본 데이터베이스와 응용 프로그램에서 tooAzure DB 가리킵니다, 그리고 트랜잭션 복제를 제거할 수 있습니다. Azure SQL 데이터베이스는 현재 프로덕션 시스템입니다.

 ![SeedCloudTR 다이어그램](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> 트랜잭션 복제 toomigrate 원본 데이터베이스의 하위 집합을 사용할 수도 있습니다. hello 게시 tooAzure SQL 데이터베이스를 복제 하는 복제 되 고 hello 데이터베이스의 hello 테이블의 제한 tooa 하위 집합을 수 있습니다. 복제 중인 각 테이블에 대 한 hello 데이터 hello 행의 하위 집합 tooa 및/또는 hello 열의 하위 집합을 제한할 수 있습니다.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>마이그레이션 tooSQL 트랜잭션 복제 워크플로 사용 하 여 데이터베이스

> [!IMPORTANT]
> 사용 하 여 hello 최신 버전의 SQL Server Management Studio tooremain Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다. 이전 버전의 SQL Server Management Studio는 SQL 데이터베이스를 구독자로 설정할 수 없습니다. [SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. 배포 설정
   -  [SSMS(SQL Server Management Studio) 사용](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [TRANSACT-SQL 사용](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. 게시물 만들기
   -  [SSMS(SQL Server Management Studio) 사용](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [TRANSACT-SQL 사용](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. 구독 만들기
   -  [SSMS(SQL Server Management Studio) 사용](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [TRANSACT-SQL 사용](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>몇 가지 팁과 마이그레이션하기 위한 차이점 tooSQL 데이터베이스

1. 로컬 배포자 사용 
   - 이렇게 하면 hello 서버의 성능에 영향을 합니다. 
   - Hello 성능에 영향을 허용 하지 않는 경우 다른 서버를 사용할 수 있지만 관리 및 관리 복잡해 지므로 합니다.
2. 충분히 큰 toohold 모든 테이블의 BCP는 스냅숏 폴더, 선택한 확인 되었는지 hello 폴더를 선택 하는 경우 원하는 tooreplicate 합니다. 
3. 스냅숏 생성 잠금 완료 될 때까지 연결 된 테이블을 hello, 따라서 스냅숏의 적절 하 게 예약 합니다. 
4. 푸시 구독만 Azure SQL Database에서 지원됩니다. Hello 원본 데이터베이스에서 구독자만 추가할 수 있습니다.

## <a name="resolving-database-migration-compatibility-issues"></a>데이터베이스 마이그레이션 호환성 문제 해결
호환성 문제를 모두 hello 버전의 SQL Server에서 마이그레이션하는 hello 데이터베이스의 hello 원본 데이터베이스와 hello 복잡성에 따라, 발생할 수 있는 광범위 한 가지가 있습니다. 이전 버전의 SQL Server에는 보다 많은 호환성 문제가 있습니다. 다음 리소스는 hello를 사용 하 여, 또한 tooa 대상 선택 하면 검색 엔진을 사용 하 여 인터넷 검색:

* [Azure SQL 데이터베이스에서 지원되지 않는 하는 SQL Server 데이터베이스 기능](sql-database-transact-sql-information.md)
* [SQL Server 2016에서 사용이 중단된 데이터베이스 엔진 기능](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [SQL Server 2014에서 사용이 중단된 데이터베이스 엔진 기능](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [SQL Server 2012에서 사용이 중단된 데이터베이스 엔진 기능](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [SQL Server 2008 R2에서 사용이 중단된 데이터베이스 엔진 기능](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [SQL Server 2005에서 사용이 중단된 데이터베이스 엔진 기능](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

또한 인터넷 hello 및 hello를 사용 하 여 이러한 리소스를 사용 하 여 toosearching [MSDN SQL Server 커뮤니티 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) 또는 [StackOverflow](http://stackoverflow.com/)합니다.

## <a name="next-steps"></a>다음 단계
* 스크립트 사용 하 여 hello hello Azure SQL EMEA 엔지니어 블로그 너무[마이그레이션하는 동안 tempdb 사용을 모니터링](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/)합니다.
* 스크립트 사용 하 여 hello hello Azure SQL EMEA 엔지니어 블로그 너무[마이그레이션이 진행 되는 동안 데이터베이스의 트랜잭션 로그 공간을 hello 모니터링](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0)합니다.
* SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.
* 마이그레이션 후 UTC 시간 사용에 대 한 정보를 참조 하십시오. [현지 표준 시간대에 대 한 수정 hello 기본 표준 시간대](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/)합니다.
* 마이그레이션 후 데이터베이스의 hello 기본 언어를 변경 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 toochange hello Azure SQL 데이터베이스의 기본 언어](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/)합니다.


