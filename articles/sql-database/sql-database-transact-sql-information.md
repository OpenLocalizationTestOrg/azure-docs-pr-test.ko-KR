---
title: "T-SQL 차이점-마이그레이션-Azure SQL 데이터베이스 aaaResolving | Microsoft Docs"
description: "Azure SQL 데이터베이스에서 완전히 지원되지 않는 TRANSACT-SQL 문"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>데이터베이스 마이그레이션 tooSQL 중 TRANSACT-SQL 차이점을 해결   
때 [데이터베이스 마이그레이션](sql-database-cloud-migrate.md) SQL Server tooAzure SQL Server에서에서 검색할 수 있습니다 데이터베이스 한다는 일부 혁신 전에 hello SQL Server를 마이그레이션할 수 있습니다. 이 항목에서는 지침 tooassist 혁신 hello 모두 이러한 혁신을 수행 하 고 이유를 이유 기본 hello 이해에 필요 합니다. hello를 사용 하 여 toodetect 비 호환성 [데이터 마이그레이션 길잡이 (DMA)](https://www.microsoft.com/download/details.aspx?id=53595)합니다.

## <a name="overview"></a>개요
응용 프로그램에서 사용하는 대부분의 Transact-SQL 기능은 Microsoft SQL Server와 Azure SQL Database 모두에서 완전하게 지원됩니다. 예를 들어, 데이터 형식, 연산자, 문자열, 산술, 논리 및 커서 함수를 SQL Server와 SQL 데이터베이스에서 동일 하 게 작동와 같은 핵심 SQL 구성 요소를 hello 합니다. 그러나 DDL(데이터 정의 언어) 및 DML(데이터 조작 언어) 요소에는 몇 가지 T-SQL 차이점이 있으며 그 결과 T-SQL 문 및 쿼리가 부분적으로만 지원됩니다(이 항목의 뒷부분에서 설명).

또한 일부 기능은 및 Azure SQL 데이터베이스 이므로 전혀 지원 되지 않는 구문 hello master 데이터베이스 및 hello 운영 체제에 종속에서 tooisolate 기능이 디자인 합니다. 따라서 대부분의 서버 수준 작업이 SQL Database에 적합하지 않습니다. T-SQL 문과 옵션은 서버 수준 옵션 또는 운영 체제 구성 요소를 구성하거나 파일 시스템 구성을 지정하는 경우에 사용할 수 없습니다. 이러한 기능이 필요한 경우 SQL Database 또는 다른 Azure 기능이나 서비스에서 다른 방법으로 사용할 수 있는 적합한 대안이 있는 경우가 많습니다. 

예를 들어 고가용성은에 기본 제공 Azure 되므로 항상에 구성 필요 하지 않습니다 (하지만 재해의 hello 이벤트에서 더 빠른 복구를 위한 tooconfigure 활성 지리적 복제를 사용할 수 있습니다). 따라서 T-SQL 문을 관련 tooavailability 그룹 SQL 데이터베이스에서 지원 되지 않는 및 hello 동적 관리 뷰에 관련된 tooAlways 지원 되지 않습니다.

목록이 지원 및 SQL 데이터베이스에서 지원 되는 hello 기능에 대 한 참조 [Azure SQL 데이터베이스 기능 비교](sql-database-features.md)합니다. 이 페이지에 hello 목록 해당 지침 및 기능 항목 보완 및 Transact SQL 문에 중점을 둡니다.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>부분적으로 차이점이 있는 Transact-SQL 구문
hello 코어 DDL (데이터 정의 언어) 문을 사용할 수 있지만 일부 DDL 문이 확장 관련된 toodisk 배치 있고 지원 되지 않는 기능입니다. 

- CREATE 및 ALTER DATABASE 문에는 36개가 넘는 옵션이 있습니다. hello 문은 파일 배치, FILESTREAM, 및 tooSQL 서버에만 적용 되는 service broker 옵션을 포함 합니다. 비교 해야 데이터베이스를 만드는 T-SQL 코드를 마이그레이션하는 경우를 마이그레이션하기 전에 데이터베이스를 만들 경우 이것은 중요 하지 [CREATE DATABASE (Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/dn268335.aspx) 에 hello SQL Server 구문과 함께 [만들기 데이터베이스 (SQL Server Transact SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake 있는지 사용 하면 모든 hello 옵션이 지원 됩니다. Azure SQL 데이터베이스에 대 한 CREATE DATABASE에는 역시 서비스 목표 및 tooSQL 데이터베이스만 적용 되는 탄력적인 크기 조정 옵션입니다.
- hello CREATE 및 ALTER TABLE 문의 FILESTREAM 지원 되지 않으므로 SQL 데이터베이스에서 사용할 수 없는 FileTable 옵션이 있습니다.
- CREATE 및 ALTER login 문을 지원 하지만 SQL 데이터베이스는 모든 hello 옵션을 제공 하지 않습니다. 데이터베이스 이식성이 향상 SQL 데이터베이스를 사용 하 여이 권장 toomake 가능 하면 로그인 하는 대신 데이터베이스 사용자가 포함 되어 있습니다. 자세한 내용은 [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) 및 [데이터베이스 액세스 제어 및 권한 부여](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)를 참조하세요.

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>SQL Database에서 지원되지 않는 Transact-SQL 구문   
또한 tooTransact SQL 문이 관련된 toohello 지원 되지 않는 기능에 설명 된 [Azure SQL 데이터베이스 기능 비교](sql-database-features.md), 다음 문 및 문 그룹 hello, 지원 되지 않습니다. 따라서 데이터베이스 toobe 마이그레이션하는 경우 사용 하는 hello 다음 기능을 T-SQL tooeliminate를 다시 구성 이러한 T-SQL 기능과 문을 합니다.

- 시스템 개체의 데이터 정렬
- 연결 관련: 끝점 문, `ORIGINAL_DB_NAME`. SQL 데이터베이스는 Windows 인증을 지원 하지 않지만 hello와 유사한 Azure Active Directory 인증을 지원 합니다. 일부 인증 유형은 hello 최신 버전의 SSMS 필요로 합니다. 자세한 내용은 참조 [연결 tooSQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여](sql-database-aad-authentication.md)합니다.
- 세 개 또는 네 개의 부분으로 된 이름을 사용하여 데이터베이스 쿼리를 교차합니다. 읽기 전용 데이터베이스 간 쿼리는 [탄력적 데이터베이스 쿼리](sql-database-elastic-query-overview.md)를 통해 지원됩니다.
- 데이터베이스 간 소유권 체인, `TRUSTWORTHY` 설정
- `DATABASEPROPERTY` 대신 `DATABASEPROPERTYEX`를 사용합니다.
- `EXECUTE AS LOGIN` 대신 '사용자로 실행'을 사용합니다.
- 확장 가능 키 관리를 제외하고 암호화를 지원합니다.
- 이벤트: 이벤트, 이벤트 알림, 쿼리 알림
- 파일 배치: 구문 관련 toodatabase 파일 배치, 크기 및 Microsoft Azure에서 자동으로 관리 되는 데이터베이스 파일입니다.
- 고가용성: Microsoft Azure 계정을 통해 관리 되는 toohigh 가용성 관련 구문은 합니다. 백업, 복원, Alwayson, 데이터베이스 미러링, 로그 전달, 복구 모드에 대한 구문을 포함합니다.
- 로그 판독기: SQL 데이터베이스에서 사용할 수 없으면 hello 로그 판독기를 사용 하는 구문: 밀어넣기 복제, 변경 데이터 캡처. SQL Database는 푸시 복제 문서의 구독자가 될 수 있습니다.
- 함수: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- 전역 임시 테이블
- 하드웨어: 구문 관련 toohardware 관련 서버 설정: 메모리, 작업자 스레드 수, CPU 선호도, 추적 플래그를 지정 합니다. 대신 서비스 수준을 사용합니다.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE` 및 네 부분으로 된 이름
- .NET Framework: CLR과 SQL Server 통합
- 의미 체계 검색
- 서버 자격 증명: 대신 [데이터베이스 범위 자격 증명](https://msdn.microsoft.com/library/mt270260.aspx)을 사용합니다.
- 서버 수준 항목: 서버 역할, `IS_SRVROLEMEMBER`, `sys.login_token`입니다. 서버 수준 사용 권한의 `GRANT`, `REVOKE`, `DENY`은 사용할 수 없지만 일부는 데이터베이스 수준 사용 권한으로 대체됩니다. 몇 가지 유용한 서버 수준 DMV에는 동등한 데이터베이스 수준 DMV가 있습니다.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- `sp_configure` 옵션 및 `RECONFIGURE`입니다. [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)을 사용하면 일부 옵션은 사용 가능합니다.
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL Server 에이전트: hello SQL Server 에이전트 또는 hello MSDB 데이터베이스에 의존 하는 구문을: 경고, 운영자, 중앙 관리 서버입니다. 대신 Azure PowerShell과 같은 스크립팅을 사용합니다.
- SQL Server 감사: 대신 SQL Database 감사를 사용합니다.
- SQL Server 추적
- 추적 플래그: 항목이 되었는지 일부 추적 플래그가 toocompatibility 모드를 이동 합니다.
- TRANSACT-SQL 디버깅
- 트리거: 서버 범위 또는 로그온 트리거
- `USE`문: toochange hello 데이터베이스 컨텍스트 tooa 다른 데이터베이스를 새 연결 toohello 새 데이터베이스를 확인 해야 합니다.

## <a name="full-transact-sql-reference"></a>전체 TRANSACT-SQL 참조
TRANSACT-SQL 문법, 사용법 및 예제에 대한 자세한 내용은 SQL Server 온라인 설명서의 [TRANSACT-SQL 참조(데이터베이스 엔진)](https://msdn.microsoft.com/library/bb510741.aspx) 를 참조하세요. 

### <a name="about-hello-applies-to-tags"></a>Hello "적용 대상" 태그 정보
hello TRANSACT-SQL 참조 항목 관련된 tooSQL 현재 서버 버전 2008 toohello 포함 되어 있습니다. Hello 항목 제목 아래 아이콘 표시줄, 목록 hello 4 개의 SQL Server 플랫폼 및 적용 가능성 나타내는는 있습니다. 예를 들어 가용성 그룹은 SQL Server 2012에서 도입되었습니다. [CREATE AVAILABILTY GROUP](https://msdn.microsoft.com/library/ff878399.aspx) 항목 hello 문을에 적용 되도록 나타냅니다 **SQL Server (2012부터 시작)**합니다. tooSQL Server 2008, SQL Server 2008 R2, Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스 또는 병렬 데이터 웨어하우스 hello 문에 적용 되지 않습니다.

일부 경우에는 항목의 일반적인 주제 hello 제품에서 사용할 수 있지만 제품 간에 약간 차이가 있습니다. hello 차이점 중간점에 적절 하 게 hello 항목에 표시 됩니다. 일부 경우에는 항목의 일반적인 주제 hello 제품에서 사용할 수 있지만 제품 간에 약간 차이가 있습니다. hello 차이점 중간점에 적절 하 게 hello 항목에 표시 됩니다. 예를 들어 hello CREATE TRIGGER 항목은 SQL 데이터베이스에서 사용할 수 있습니다. 하지만 hello **모든 서버** 서버 수준 트리거에 대 한 옵션을 SQL 데이터베이스에서 서버 수준 트리거를 사용할 수 없음을 나타냅니다. 대신 데이터베이스 수준 트리거를 사용합니다.

## <a name="next-steps"></a>다음 단계

목록이 지원 및 SQL 데이터베이스에서 지원 되는 hello 기능에 대 한 참조 [Azure SQL 데이터베이스 기능 비교](sql-database-features.md)합니다. 이 페이지에 hello 목록 해당 지침 및 기능 항목 보완 및 Transact SQL 문에 중점을 둡니다.

