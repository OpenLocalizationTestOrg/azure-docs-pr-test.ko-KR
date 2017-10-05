---
title: "여러 스키마를 사용하여 클라우드 데이터베이스에서 쿼리 | Microsoft Docs"
description: "수직 분할을 통해 데이터베이스 간 쿼리를 설정하는 방법"
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
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="d2792-103">여러 스키마를 사용하여 클라우드 데이터베이스에서 쿼리(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="d2792-103">Query across cloud databases with different schemas (preview)</span></span>
![다른 데이터베이스에서 테이블에 대한 쿼리][1]

<span data-ttu-id="d2792-105">수직 분할 데이터베이스는 서로 다른 데이터베이스에서 다양한 테이블 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="d2792-106">즉 스키마가 데이터베이스마다 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="d2792-107">예를 들어, 재고의 모든 테이블은 한 데이터베이스 안에 있지만 모든 회계 관련 테이블은 보조 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d2792-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2792-108">Prerequisites</span></span>
* <span data-ttu-id="d2792-109">사용자는 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="d2792-110">이 사용 권한은 ALTER DATABASE 권한에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="d2792-111">기본 데이터 원본을 참조하기 위해 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="d2792-112">개요</span><span class="sxs-lookup"><span data-stu-id="d2792-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="d2792-113">행 분할과 달리 이 DDL 문은 Elastic Database 클라이언트 라이브러리를 통한 분할 맵이 있는 데이터 계층 정의에 종속되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="d2792-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="d2792-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="d2792-115">데이터베이스 범위 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="d2792-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="d2792-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="d2792-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="d2792-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="d2792-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="d2792-118">데이터베이스 범위 마스터 키 및 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="d2792-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="d2792-119">자격 증명은 탄력적 쿼리에서 원격 데이터베이스 연결에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="d2792-120">`<username>`에 **"@servername"** 접미사가 포함되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="d2792-121">외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="d2792-121">Create external data sources</span></span>
<span data-ttu-id="d2792-122">구문</span><span class="sxs-lookup"><span data-stu-id="d2792-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="d2792-123">TYPE 매개 변수는 **RDBMS**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="d2792-124">예</span><span class="sxs-lookup"><span data-stu-id="d2792-124">Example</span></span>
<span data-ttu-id="d2792-125">다음 예제에서는 외부 데이터 원본에 대한 CREATE 문 사용을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="d2792-126">현재 외부 데이터 원본의 목록을 검색하려면:</span><span class="sxs-lookup"><span data-stu-id="d2792-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="d2792-127">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="d2792-127">External Tables</span></span>
<span data-ttu-id="d2792-128">구문</span><span class="sxs-lookup"><span data-stu-id="d2792-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="d2792-129">예제</span><span class="sxs-lookup"><span data-stu-id="d2792-129">Example</span></span>
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

<span data-ttu-id="d2792-130">다음 예제에서는 현재 데이터베이스에서 외부 테이블 목록을 검색 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="d2792-131">설명</span><span class="sxs-lookup"><span data-stu-id="d2792-131">Remarks</span></span>
<span data-ttu-id="d2792-132">탄력적 쿼리는 기존 외부 테이블 구문을 확장하여 RDBMS 형식의 외부 데이터 원본을 사용하는 외부 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="d2792-133">수직 분할에 대한 외부 테이블 정의에서는 다음과 같은 측면을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="d2792-134">**스키마**: 외부 테이블 DDL은 쿼리가 사용할 수 있는 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="d2792-135">외부 테이블 정의에서 제공한 스키마는 실제 데이터가 저장되는 원격 데이터베이스의 테이블 스키마와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="d2792-136">**원격 데이터 참조**: 외부 테이블 DDL은 외부 데이터 원본을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="d2792-137">외부 데이터 원본은 실제 테이블 데이터가 저장된 원격 데이터베이스의 논리적 서버 이름과 데이터베이스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="d2792-138">이전 섹션에서 설명한 대로 외부 데이터 소스를 사용하여 외부 테이블을 만드는 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="d2792-139">DATA_SOURCE 절은 외부 테이블에 사용하는 외부 데이터 원본(즉, 수직 분할의 경우 원격 데이터베이스)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="d2792-140">SCHEMA_NAME 및 OBJECT_NAME 절은 각각 외부 테이블 정의를 원격 데이터베이스에 있는 다른 스키마 또는 다른 이름의 테이블에 매핑하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="d2792-141">이 기능은 원격 데이터베이스에서 카탈로그 뷰나 DMV에 대해 외부 테이블을 정의하거나, 원격 테이블 이름을 이미 로컬로 사용하는 경우 등의 다른 상황에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="d2792-142">다음 DDL 문은 로컬 카탈로그에서 기존 외부 테이블 정의를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="d2792-143">원격 데이터베이스에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="d2792-144">**CREATE/DROP EXTERNAL TABLE 권한**: 기본 데이터 원본을 참조하기 위해 외부 테이블 DDL에 대한 ALTER ANY EXTERNAL DATA SOURCE 권한도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="d2792-145">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d2792-145">Security considerations</span></span>
<span data-ttu-id="d2792-146">외부 테이블에 대한 액세스 권한이 있는 사용자는 외부 데이터 원본 정의에서 제공한 자격 증명에 따라 자동으로 기본 원격 테이블에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="d2792-147">외부 데이터 원본의 자격 증명을 통해 원치 않는 권한 상승을 방지하려면 외부 테이블에 대한 액세스 관리에 주의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="d2792-148">일반 SQL 권한을 사용하여 일반 테이블에서처럼 외부 테이블에 대한 액세스를 부여하거나 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="d2792-149">예: 수직 분할된 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="d2792-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="d2792-150">다음 쿼리는 주문 및 주문 라인을 위한 2개의 로컬 테이블과 고객을 위한 원격 테이블 간의 3방향 조인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="d2792-151">탄력적 쿼리에 대한 참조 데이터 사용 사례의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-151">This is an example of the reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="d2792-152">원격 T-SQL 실행을 위한 저장 프로시저: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="d2792-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="d2792-153">또한 탄력적 쿼리는 분할된 데이터베이스에 대한 직접 액세스를 제공하기 위해 저장 프로시저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="d2792-154">저장 프로시저는 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)라고 하며, 원격 데이터베이스에서 원격 저장 프로시저 또는 T-SQL 코드를 실행하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="d2792-155">사용되는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="d2792-156">데이터 원본 이름(nvarchar): RDBMS 형식의 외부 데이터 원본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="d2792-157">쿼리(nvarchar): T-SQL 쿼리를 각 분할된 데이터베이스에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="d2792-158">매개 변수 선언(nvarchar), 선택 사항: 쿼리 매개 변수(예: sp_executesql)에 사용된 매개 변수에 대한 데이터 형식 정의가 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="d2792-159">매개 변수 값 목록, 선택 사항: 쉼표로 구분한 매개 변수 값(예: sp_executesql) 목록.</span><span class="sxs-lookup"><span data-stu-id="d2792-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="d2792-160">sp\_execute\_remote는 호출 매개 변수에 제공된 외부 데이터 원본을 사용하여 원격 데이터베이스에서 지정된 T-SQL 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="d2792-161">또한 외부 데이터 원본의 자격 증명을 사용하여 분할 맵 관리자 데이터베이스 및 원격 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="d2792-162">예제:</span><span class="sxs-lookup"><span data-stu-id="d2792-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="d2792-163">도구에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="d2792-163">Connectivity for tools</span></span>
<span data-ttu-id="d2792-164">일반 SQL Server 연결 문자열을 사용하여, 탄력적 쿼리를 사용하도록 설정되었고 외부 테이블이 정의된 SQL DB 서버의 데이터베이스에 BI 및 데이터 통합 도구를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="d2792-165">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="d2792-166">그런 다음 도구와 연결하려는 타 SQL Server 데이터베이스와 똑같이 탄력적 쿼리 데이터베이스와 외부 테이블을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="d2792-167">모범 사례</span><span class="sxs-lookup"><span data-stu-id="d2792-167">Best practices</span></span>
* <span data-ttu-id="d2792-168">SQL DB 방화벽 구성에서 Azure 서비스에 대한 액세스를 활성화하여 탄력적 쿼리 끝점 데이터베이스에 원격 데이터베이스 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="d2792-169">또한 외부 데이터 원본 종의에서 제공한 자격 증명으로 원격 데이터베이스에 로그인할 수 있고 원격 테이블에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="d2792-170">탄력적 쿼리는 원격 데이터베이스에서 대부분의 계산을 수행할 수 있는 상황에서 가장 잘 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="d2792-171">일반적으로 원격 데이터베이스에서 평가할 수 있는 선택적 필더 조건자나, 원격 데이터베이스에서 완전히 수행 가능한 조인을 통해 최고의 쿼리 성능을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="d2792-172">다른 쿼리 패턴은 원격 데이터베이스에서 대규모의 데이터 로드가 필요할 수도 있기 때문에 성능이 좋지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2792-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d2792-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2792-173">Next steps</span></span>

* <span data-ttu-id="d2792-174">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2792-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="d2792-175">수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2792-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="d2792-176">행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2792-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="d2792-177">행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2792-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="d2792-178">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2792-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
