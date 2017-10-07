---
title: "다른 스키마와 클라우드 간에 aaaQuery 데이터베이스 | Microsoft Docs"
description: "어떻게 tooset 열 분할에 대 한 데이터베이스 간 쿼리를"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>여러 스키마를 사용하여 클라우드 데이터베이스에서 쿼리(미리 보기)
![다른 데이터베이스에서 테이블에 대한 쿼리][1]

수직 분할 데이터베이스는 서로 다른 데이터베이스에서 다양한 테이블 집합을 사용합니다. 즉, 해당 hello 스키마는 다른 데이터베이스에서 다릅니다. 예를 들어, 재고의 모든 테이블은 한 데이터베이스 안에 있지만 모든 회계 관련 테이블은 보조 데이터베이스에 있습니다. 

## <a name="prerequisites"></a>필수 조건
* hello 사용자가 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다. 이 사용 권한은 hello ALTER DATABASE 권한이 포함 되어 있습니다.
* ALTER ANY EXTERNAL DATA SOURCE 권한은 필요한 toorefer toohello 데이터 원본으로 사용 합니다.

## <a name="overview"></a>개요

> [!NOTE]
> 와 달리 수평 분할을 사용 하면 이러한 DDL 문은에 종속 되지 않는 hello 탄력적 데이터베이스 클라이언트 라이브러리를 통해 분할 맵 사용 하 여 데이터 계층을 정의 합니다.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [데이터베이스 범위 자격 증명 만들기](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>데이터베이스 범위 마스터 키 및 자격 증명 만들기
hello 자격 증명 hello 탄력적 쿼리 tooconnect tooyour 원격 데이터베이스에서 사용 됩니다.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> 해당 hello 확인 `<username>` 포함 하지 않습니다 **"@servername"** 접미사입니다. 
>

## <a name="create-external-data-sources"></a>외부 데이터 원본 만들기
구문

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> hello 형식 매개 변수를 너무 설정 되어 있어야**RDBMS**합니다. 
>

### <a name="example"></a>예제
hello 다음 예제에서는 외부 데이터 원본에 대 한 CREATE 문 hello hello 사용 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

현재 외부 데이터 원본의 tooretrieve hello 목록: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>외부 테이블
구문

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>예제
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

다음 예제는 hello tooretrieve hello 현재 데이터베이스에서 외부 테이블 목록을 hello 하는 방법을 보여 줍니다. 

    select * from sys.external_tables; 

### <a name="remarks"></a>설명
탄력적 쿼리 hello 기존 외부 테이블 구문 toodefine 외부 테이블 형식의 RDBMS 외부 데이터 원본을 사용 하는 확장 합니다. 수직 분할에 대 한 외부 테이블 정의에서는 hello 다음 측면을 다룹니다. 

* **스키마**: hello 외부 테이블 DDL 쿼리를 사용할 수 있는 스키마를 정의 합니다. 외부 테이블 정의에 제공 된 hello 스키마 hello hello 실제 데이터가 저장 되는 원격 데이터베이스에 있는 hello 테이블의 toomatch hello 스키마가 필요 합니다. 
* **원격 데이터베이스 참조**: hello 외부 테이블 DDL tooan 외부 데이터 원본을 참조 합니다. hello 외부 데이터 원본은 hello 논리 서버 이름 및 hello hello 실제 테이블 데이터가 저장 되는 원격 데이터베이스의 데이터베이스 이름을 지정 합니다. 

외부 데이터 소스를 사용 하 여 hello 이전 섹션에 설명 된 대로, hello 구문 toocreate 외부 테이블은 다음과 같습니다. 

hello DATA_SOURCE 절 hello 외부 테이블에 사용 되는 hello 외부 데이터 원본 (예: hello 원격 데이터베이스 수직 분할의 경우)을 정의 합니다.  

hello SCHEMA_NAME, OBJECT_NAME 절의 각각 hello 원격 데이터베이스 또는 다른 이름으로 tooa 테이블에 hello 기능 toomap hello 외부 테이블 정의 tooa 테이블 다른 스키마에 제공합니다. 원하는 toodefine 외부 테이블 tooa 카탈로그 뷰 또는 DMV-원격 데이터베이스 또는 여기서 hello 원격 테이블 이름이 이미 사용 중 로컬로 다른 상황에서 경우에 유용 합니다.  

hello 다음 DDL 문은 기존 외부 테이블 정의에서 삭제 hello 로컬 카탈로그 합니다. Hello 원격 데이터베이스는 영향을 주지 않습니다. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**CREATE/DROP 외부 테이블에 대 한 권한을**: 외부 테이블은 DDL 필요한 toorefer toohello 기본 데이터 원본에 대 한 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요 합니다.  

## <a name="security-considerations"></a>보안 고려 사항
Access toohello 외부 테이블에 있는 사용자는 자동으로 액세스할 toohello hello 외부 데이터 원본 정의에 지정 된 hello 자격 증명에서 기본 원격 테이블 수입니다. 순서 tooavoid 의도 하지 않은 권한 상승으로 hello 외부 데이터 원본의 hello 자격 증명을 통해 액세스 toohello 외부 테이블을 신중 하 게 관리 해야 합니다. 일반 SQL 사용 권한 것를 일반 테이블 처럼 사용 되는 tooGRANT 또는 REVOKE access tooan 외부 테이블을 수 있습니다.  

## <a name="example-querying-vertically-partitioned-databases"></a>예: 수직 분할된 데이터베이스 쿼리
hello 다음 쿼리는 3 방향 조인을 수행 주문 및 주문 라인에 대해 두 개의 로컬 테이블 hello 및 hello 원격 테이블 간에 고객에 대 한 합니다. 이것이 hello 탄력적 쿼리에 대 한 참조 데이터 사용 사례의 한 예: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>원격 T-SQL 실행을 위한 저장 프로시저: sp\_execute_remote
탄력적 쿼리도 toohello 분할 된 데이터베이스에 직접 액세스를 제공 하는 저장된 프로시저를 소개 합니다. hello 저장된 프로시저를 호출 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714) tooexecute 사용 되는 원격 저장된 프로시저 또는 hello 원격 데이터베이스의 T-SQL 코드 상태일 수 있습니다. Hello 매개 변수를 다음을 수행 합니다. 

* 데이터 원본 이름 (nvarchar): hello 이름 hello 유형의 RDBMS 외부 데이터 원본입니다. 
* 쿼리 (nvarchar): hello T-SQL 쿼리 toobe 각 분할 된 데이터베이스에서 실행 합니다. 
* 선택적 매개 변수 선언 (nvarchar)-: hello 쿼리 매개 변수 (예: sp_executesql)에서 사용 되는 hello 매개 변수에 대 한 데이터 형식 정의 포함 하는 문자열입니다. 
* 매개 변수 값 목록, 선택 사항: 쉼표로 구분한 매개 변수 값(예: sp_executesql) 목록.

hello sp\_실행\_원격 사용 하 여 hello hello 호출 매개 변수 tooexecute hello hello 원격 데이터베이스의 T-SQL 문을 들에 제공 된 외부 데이터 원본. Hello 외부 데이터 원본 tooconnect toohello shardmap manager 데이터베이스 및 hello 원격 데이터베이스의 hello 자격 증명을 사용합니다.  

예제: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a>도구에 대한 연결
일반 SQL Server 연결 문자열 tooconnect 프로그램 BI와 데이터 통합 도구 toodatabases 사용 하도록 설정 하는 탄력적 쿼리 및 외부 테이블 정의 된 hello SQL DB 서버에 사용할 수 있습니다. SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다. Toohello 탄력적 쿼리 데이터베이스와 다른 SQL Server 데이터베이스를 연결 하는 toowith 하는 도구와 마찬가지로 외부 테이블을 참조 합니다. 

## <a name="best-practices"></a>모범 사례
* 해당 hello 탄력적 쿼리 끝점 데이터베이스에 부여 된 액세스 toohello 원격 데이터베이스는 SQL DB 방화벽 구성에 Azure 서비스에 대 한 액세스를 사용 하 여 확인 합니다. 또한 hello 외부 데이터에서 원본 정의 hello 원격 데이터베이스에 성공적으로 로그인 할 수 있으며 hello 권한 tooaccess hello 원격 테이블 제공 hello 자격 증명을 확인 합니다.  
* 탄력적 쿼리 적합 쿼리에 대 한 대부분 hello 계산의 hello 원격 데이터베이스에서 수행할 수 있는 합니다. 일반적으로 완전히 hello 원격 데이터베이스에서 수행할 수 있는 조인 또는 hello 원격 데이터베이스에 평가 될 수 있는 선택적 필터 조건자를 사용 하는 최고의 쿼리 성능을 hello를 가져옵니다. 다른 쿼리 패턴 tooload 많은 양의 hello 원격 데이터베이스에서 데이터를 할 수 및 성능이 떨어질 수 있습니다. 

## <a name="next-steps"></a>다음 단계

* 탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.
* 수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.
* 행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.
* 행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.
* 단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
