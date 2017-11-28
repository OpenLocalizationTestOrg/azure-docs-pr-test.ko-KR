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
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="db327-103">여러 스키마를 사용하여 클라우드 데이터베이스에서 쿼리(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="db327-103">Query across cloud databases with different schemas (preview)</span></span>
![다른 데이터베이스에서 테이블에 대한 쿼리][1]

<span data-ttu-id="db327-105">수직 분할 데이터베이스는 서로 다른 데이터베이스에서 다양한 테이블 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="db327-106">즉, 해당 hello 스키마는 다른 데이터베이스에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="db327-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="db327-107">예를 들어, 재고의 모든 테이블은 한 데이터베이스 안에 있지만 모든 회계 관련 테이블은 보조 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db327-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db327-108">Prerequisites</span></span>
* <span data-ttu-id="db327-109">hello 사용자가 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="db327-110">이 사용 권한은 hello ALTER DATABASE 권한이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="db327-111">ALTER ANY EXTERNAL DATA SOURCE 권한은 필요한 toorefer toohello 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="db327-112">개요</span><span class="sxs-lookup"><span data-stu-id="db327-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="db327-113">와 달리 수평 분할을 사용 하면 이러한 DDL 문은에 종속 되지 않는 hello 탄력적 데이터베이스 클라이언트 라이브러리를 통해 분할 맵 사용 하 여 데이터 계층을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="db327-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="db327-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="db327-115">데이터베이스 범위 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="db327-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="db327-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="db327-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="db327-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="db327-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="db327-118">데이터베이스 범위 마스터 키 및 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="db327-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="db327-119">hello 자격 증명 hello 탄력적 쿼리 tooconnect tooyour 원격 데이터베이스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db327-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="db327-120">해당 hello 확인 `<username>` 포함 하지 않습니다 **"@servername"** 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="db327-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="db327-121">외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="db327-121">Create external data sources</span></span>
<span data-ttu-id="db327-122">구문</span><span class="sxs-lookup"><span data-stu-id="db327-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="db327-123">hello 형식 매개 변수를 너무 설정 되어 있어야**RDBMS**합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="db327-124">예제</span><span class="sxs-lookup"><span data-stu-id="db327-124">Example</span></span>
<span data-ttu-id="db327-125">hello 다음 예제에서는 외부 데이터 원본에 대 한 CREATE 문 hello hello 사용</span><span class="sxs-lookup"><span data-stu-id="db327-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="db327-126">현재 외부 데이터 원본의 tooretrieve hello 목록:</span><span class="sxs-lookup"><span data-stu-id="db327-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="db327-127">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="db327-127">External Tables</span></span>
<span data-ttu-id="db327-128">구문</span><span class="sxs-lookup"><span data-stu-id="db327-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="db327-129">예제</span><span class="sxs-lookup"><span data-stu-id="db327-129">Example</span></span>
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

<span data-ttu-id="db327-130">다음 예제는 hello tooretrieve hello 현재 데이터베이스에서 외부 테이블 목록을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db327-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="db327-131">설명</span><span class="sxs-lookup"><span data-stu-id="db327-131">Remarks</span></span>
<span data-ttu-id="db327-132">탄력적 쿼리 hello 기존 외부 테이블 구문 toodefine 외부 테이블 형식의 RDBMS 외부 데이터 원본을 사용 하는 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="db327-133">수직 분할에 대 한 외부 테이블 정의에서는 hello 다음 측면을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="db327-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="db327-134">**스키마**: hello 외부 테이블 DDL 쿼리를 사용할 수 있는 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="db327-135">외부 테이블 정의에 제공 된 hello 스키마 hello hello 실제 데이터가 저장 되는 원격 데이터베이스에 있는 hello 테이블의 toomatch hello 스키마가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="db327-136">**원격 데이터베이스 참조**: hello 외부 테이블 DDL tooan 외부 데이터 원본을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="db327-137">hello 외부 데이터 원본은 hello 논리 서버 이름 및 hello hello 실제 테이블 데이터가 저장 되는 원격 데이터베이스의 데이터베이스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="db327-138">외부 데이터 소스를 사용 하 여 hello 이전 섹션에 설명 된 대로, hello 구문 toocreate 외부 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="db327-139">hello DATA_SOURCE 절 hello 외부 테이블에 사용 되는 hello 외부 데이터 원본 (예: hello 원격 데이터베이스 수직 분할의 경우)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="db327-140">hello SCHEMA_NAME, OBJECT_NAME 절의 각각 hello 원격 데이터베이스 또는 다른 이름으로 tooa 테이블에 hello 기능 toomap hello 외부 테이블 정의 tooa 테이블 다른 스키마에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="db327-141">원하는 toodefine 외부 테이블 tooa 카탈로그 뷰 또는 DMV-원격 데이터베이스 또는 여기서 hello 원격 테이블 이름이 이미 사용 중 로컬로 다른 상황에서 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="db327-142">hello 다음 DDL 문은 기존 외부 테이블 정의에서 삭제 hello 로컬 카탈로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="db327-143">Hello 원격 데이터베이스는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="db327-144">**CREATE/DROP 외부 테이블에 대 한 권한을**: 외부 테이블은 DDL 필요한 toorefer toohello 기본 데이터 원본에 대 한 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="db327-145">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="db327-145">Security considerations</span></span>
<span data-ttu-id="db327-146">Access toohello 외부 테이블에 있는 사용자는 자동으로 액세스할 toohello hello 외부 데이터 원본 정의에 지정 된 hello 자격 증명에서 기본 원격 테이블 수입니다.</span><span class="sxs-lookup"><span data-stu-id="db327-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="db327-147">순서 tooavoid 의도 하지 않은 권한 상승으로 hello 외부 데이터 원본의 hello 자격 증명을 통해 액세스 toohello 외부 테이블을 신중 하 게 관리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="db327-148">일반 SQL 사용 권한 것를 일반 테이블 처럼 사용 되는 tooGRANT 또는 REVOKE access tooan 외부 테이블을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="db327-149">예: 수직 분할된 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="db327-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="db327-150">hello 다음 쿼리는 3 방향 조인을 수행 주문 및 주문 라인에 대해 두 개의 로컬 테이블 hello 및 hello 원격 테이블 간에 고객에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="db327-151">이것이 hello 탄력적 쿼리에 대 한 참조 데이터 사용 사례의 한 예:</span><span class="sxs-lookup"><span data-stu-id="db327-151">This is an example of hello reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="db327-152">원격 T-SQL 실행을 위한 저장 프로시저: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="db327-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="db327-153">탄력적 쿼리도 toohello 분할 된 데이터베이스에 직접 액세스를 제공 하는 저장된 프로시저를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="db327-154">hello 저장된 프로시저를 호출 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714) tooexecute 사용 되는 원격 저장된 프로시저 또는 hello 원격 데이터베이스의 T-SQL 코드 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="db327-155">Hello 매개 변수를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="db327-156">데이터 원본 이름 (nvarchar): hello 이름 hello 유형의 RDBMS 외부 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="db327-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="db327-157">쿼리 (nvarchar): hello T-SQL 쿼리 toobe 각 분할 된 데이터베이스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="db327-158">선택적 매개 변수 선언 (nvarchar)-: hello 쿼리 매개 변수 (예: sp_executesql)에서 사용 되는 hello 매개 변수에 대 한 데이터 형식 정의 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="db327-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="db327-159">매개 변수 값 목록, 선택 사항: 쉼표로 구분한 매개 변수 값(예: sp_executesql) 목록.</span><span class="sxs-lookup"><span data-stu-id="db327-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="db327-160">hello sp\_실행\_원격 사용 하 여 hello hello 호출 매개 변수 tooexecute hello hello 원격 데이터베이스의 T-SQL 문을 들에 제공 된 외부 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="db327-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="db327-161">Hello 외부 데이터 원본 tooconnect toohello shardmap manager 데이터베이스 및 hello 원격 데이터베이스의 hello 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="db327-162">예제:</span><span class="sxs-lookup"><span data-stu-id="db327-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="db327-163">도구에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="db327-163">Connectivity for tools</span></span>
<span data-ttu-id="db327-164">일반 SQL Server 연결 문자열 tooconnect 프로그램 BI와 데이터 통합 도구 toodatabases 사용 하도록 설정 하는 탄력적 쿼리 및 외부 테이블 정의 된 hello SQL DB 서버에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="db327-165">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="db327-166">Toohello 탄력적 쿼리 데이터베이스와 다른 SQL Server 데이터베이스를 연결 하는 toowith 하는 도구와 마찬가지로 외부 테이블을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="db327-167">모범 사례</span><span class="sxs-lookup"><span data-stu-id="db327-167">Best practices</span></span>
* <span data-ttu-id="db327-168">해당 hello 탄력적 쿼리 끝점 데이터베이스에 부여 된 액세스 toohello 원격 데이터베이스는 SQL DB 방화벽 구성에 Azure 서비스에 대 한 액세스를 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="db327-169">또한 hello 외부 데이터에서 원본 정의 hello 원격 데이터베이스에 성공적으로 로그인 할 수 있으며 hello 권한 tooaccess hello 원격 테이블 제공 hello 자격 증명을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="db327-170">탄력적 쿼리 적합 쿼리에 대 한 대부분 hello 계산의 hello 원격 데이터베이스에서 수행할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="db327-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="db327-171">일반적으로 완전히 hello 원격 데이터베이스에서 수행할 수 있는 조인 또는 hello 원격 데이터베이스에 평가 될 수 있는 선택적 필터 조건자를 사용 하는 최고의 쿼리 성능을 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db327-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="db327-172">다른 쿼리 패턴 tooload 많은 양의 hello 원격 데이터베이스에서 데이터를 할 수 및 성능이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db327-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="db327-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db327-173">Next steps</span></span>

* <span data-ttu-id="db327-174">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db327-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="db327-175">수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db327-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="db327-176">행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db327-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="db327-177">행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db327-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="db327-178">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db327-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
