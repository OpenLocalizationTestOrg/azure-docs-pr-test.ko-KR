---
title: "확장된 클라우드 데이터베이스에서 보고 | Microsoft Docs"
description: "행 분할에서 탄력적 쿼리를 설정하는 방법"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 62b5bcd26aa1ed219fb38970916e0e8847ceb577
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="4200f-103">확장된 클라우드 데이터베이스에서 보고(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="4200f-103">Reporting across scaled-out cloud databases (preview)</span></span>
![분할된 데이터베이스에 대한 쿼리][1]

<span data-ttu-id="4200f-105">분할된 데이터베이스는 확장된 데이터 계층에 행을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="4200f-106">스키마는 모든 참여하는 데이터베이스에서 동일하며 이를 수평 분할이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="4200f-107">탄력적 쿼리를 사용하여 분할된 데이터베이스의 모든 데이터베이스를 망라하는 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="4200f-108">빠른 시작은 [확장된 클라우드 데이터베이스에서 보고](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="4200f-109">비분할 데이터베이스의 경우 [여러 스키마를 사용하여 클라우드 데이터베이스에서 쿼리](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4200f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4200f-110">Prerequisites</span></span>
* <span data-ttu-id="4200f-111">탄력적 데이터베이스 클라이언트 라이브러리를 사용하여 분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="4200f-112">[분할된 데이터베이스 맵 관리](sql-database-elastic-scale-shard-map-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="4200f-113">또는 [탄력적 데이터베이스 도구 시작하기](sql-database-elastic-scale-get-started.md)의 샘플 앱을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="4200f-114">또는 [기존 데이터베이스를 확장된 데이터베이스로 마이그레이션](sql-database-elastic-convert-to-use-elastic-tools.md)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="4200f-115">사용자는 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="4200f-116">이 사용 권한은 ALTER DATABASE 권한에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="4200f-117">기본 데이터 원본을 참조하기 위해 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="4200f-118">개요</span><span class="sxs-lookup"><span data-stu-id="4200f-118">Overview</span></span>
<span data-ttu-id="4200f-119">이 문은 탄력적 쿼리 데이터베이스에서 분할된 데이터 계층의 메타데이터 표현을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="4200f-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="4200f-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="4200f-121">데이터베이스 범위 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="4200f-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="4200f-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="4200f-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="4200f-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="4200f-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="4200f-124">1.1 데이터베이스 범위 마스터 키 및 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="4200f-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="4200f-125">자격 증명은 탄력적 쿼리에서 원격 데이터베이스 연결에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="4200f-126">*"\<username\>"*에 *"@servername"* 접미사가 포함되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-126">Make sure that the *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="4200f-127">1.2 외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="4200f-127">1.2 Create external data sources</span></span>
<span data-ttu-id="4200f-128">구문</span><span class="sxs-lookup"><span data-stu-id="4200f-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="4200f-129">예제</span><span class="sxs-lookup"><span data-stu-id="4200f-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="4200f-130">현재 외부 데이터 원본의 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="4200f-131">외부 데이터 원본에는 분할 맵을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-131">The external data source references your shard map.</span></span> <span data-ttu-id="4200f-132">그러면 탄력적 쿼리는 외부 데이터 원본과 기본 분할 맵을 사용하여 데이터 계층에 참여하는 데이터베이스를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="4200f-133">탄력적 쿼리를 처리하는 동안 분할 데이터베이스 맵을 읽고 분할 데이터베이스의 데이터에 액세스할 때는 동일한 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="4200f-134">1.3 외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="4200f-134">1.3 Create external tables</span></span>
<span data-ttu-id="4200f-135">구문</span><span class="sxs-lookup"><span data-stu-id="4200f-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="4200f-136">**예제**</span><span class="sxs-lookup"><span data-stu-id="4200f-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="4200f-137">현재 데이터베이스에서 외부 테이블 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="4200f-138">외부 테이블을 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="4200f-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="4200f-139">설명</span><span class="sxs-lookup"><span data-stu-id="4200f-139">Remarks</span></span>
<span data-ttu-id="4200f-140">DATA\_SOURCE 절은 외부 테이블에 사용하는 외부 데이터 원본(분할 맵)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="4200f-141">SCHEMA\_NAME 및 OBJECT\_NAME 절은 외부 테이블 정의를 다른 스키마의 테이블에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="4200f-142">생략한 경우 원격 개체의 스키마를 “dbo”라 가정하고 그 이름이 정의하는 외부 테이블 이름과 동일하다고 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="4200f-143">외부 테이블을 만들려는 데이터베이스에서 이미 원격 테이블의 이름을 가져온 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="4200f-144">수평 확장된 데이터 계층에서 DMV의 카탈로그 뷰 집계를 가져오기 위해 외부 테이블을 정의하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="4200f-145">카탈로그 뷰와 DMV는 이미 로컬로 존재하므로 외부 테이블 정의에 그 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="4200f-146">대신 다른 이름을 사용하고 SCHEMA\_NAME 및/또는 OBJECT\_NAME 절에서 카탈로그 뷰나 DMV의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="4200f-147">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-147">(See the example below.)</span></span> 

<span data-ttu-id="4200f-148">DISTRIBUTION 절은 이 테이블에 사용되는 데이터 배포를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="4200f-149">쿼리 프로세서는 가장 효율적인 쿼리 계획을 구성하기 위해 DISTRIBUTION에서 제공하는 정보를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="4200f-150">**SHARDED** 는 데이터가 데이터베이스에서 행 분할되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="4200f-151">데이터 배포의 분할 키는 **<sharding_column_name>** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="4200f-152">**REPLICATED** 는 테이블의 동일한 사본이 각 데이터베이스에 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="4200f-153">사용자가 데이터베이스 전체에서 복제본이 동일한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="4200f-154">**ROUND\_ROBIN**은 테이블이 응용 프로그램의 배포 방법에 따라 수평 분할되는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="4200f-155">**데이터 계층 참조**: 외부 테이블 DDL은 외부 데이터 원본을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="4200f-156">외부 데이터 원본은 외부 테이블에 데이터 계층의 모든 데이터베이스를 찾는 데 필요한 정보를 제공하는 분할 맵을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="4200f-157">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="4200f-157">Security considerations</span></span>
<span data-ttu-id="4200f-158">외부 테이블에 대한 액세스 권한이 있는 사용자는 외부 데이터 원본 정의에서 제공한 자격 증명에 따라 자동으로 기본 원격 테이블에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="4200f-159">외부 데이터 원본의 자격 증명을 통해 원치 않는 권한 상승을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="4200f-160">일반 테이블인 것처럼 외부 테이블에 GRANT 또는 REVOKE를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="4200f-161">외부 데이터 원본 및 외부 테이블을 정의한 후 외부 테이블을 통해 전체 T-SQL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="4200f-162">예: 수평 분할된 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="4200f-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="4200f-163">다음 쿼리는 웨어하우스, 주문 및 주문 라인 간의 3방향 조인을 수행하고 여러 집계 및 선택적인 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="4200f-164">(1) 행 분할(분할)이며 (2) 웨어하우스, 주문 및 주문 라인이 웨어하우스 ID 열로 분할되었으며, 탄력적 쿼리가 분할된 데이터베이스에서 조인을 배치할 수 있고, 분할된 데이터베이스에서 비용이 드는 쿼리 부분을 처리할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="4200f-165">원격 T-SQL 실행을 위한 저장 프로시저: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="4200f-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="4200f-166">또한 탄력적 쿼리는 분할된 데이터베이스에 대한 직접 액세스를 제공하기 위해 저장 프로시저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="4200f-167">저장 프로시저는 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)라고 하며, 원격 데이터베이스에서 원격 저장 프로시저 또는 T-SQL 코드를 실행하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="4200f-168">사용되는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="4200f-169">데이터 원본 이름(nvarchar): RDBMS 형식의 외부 데이터 원본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="4200f-170">쿼리(nvarchar): T-SQL 쿼리를 각 분할된 데이터베이스에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="4200f-171">매개 변수 선언(nvarchar), 선택 사항: 쿼리 매개 변수(예: sp_executesql)에 사용된 매개 변수에 대한 데이터 형식 정의가 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="4200f-172">매개 변수 값 목록, 선택 사항: 쉼표로 구분한 매개 변수 값(예: sp_executesql) 목록.</span><span class="sxs-lookup"><span data-stu-id="4200f-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="4200f-173">sp\_execute\_remote는 호출 매개 변수에 제공된 외부 데이터 원본을 사용하여 원격 데이터베이스에서 지정된 T-SQL 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="4200f-174">또한 외부 데이터 원본의 자격 증명을 사용하여 분할 맵 관리자 데이터베이스 및 원격 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="4200f-175">예제:</span><span class="sxs-lookup"><span data-stu-id="4200f-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="4200f-176">도구에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="4200f-176">Connectivity for tools</span></span>
<span data-ttu-id="4200f-177">일반 SQL Server 연결 문자열을 사용 하여 응용 프로그램, BI, 데이터 통합 도구를 외부 테이블 정의가 있는 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="4200f-178">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="4200f-179">그런 다음 도구에 연결된 타 SQL Server 데이터베이스 등, 탄력적 쿼리 데이터베이스를 참조하고 도구의나 응용 프로그램의 외부 테이블을 로컬 테이블처럼 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="4200f-180">모범 사례</span><span class="sxs-lookup"><span data-stu-id="4200f-180">Best practices</span></span>
* <span data-ttu-id="4200f-181">탄력적 쿼리 끝점 데이터베이스에 SQL DB 방화벽을 통한 모든 분할된 데이터베이스 및 분할 맵 데이터베이스 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="4200f-182">외부 테이블에서 정의한 데이터 배포의 유효성을 검사하거나 해당 배포를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="4200f-183">실제 데이터 배포는 테이블 정의에 지정된 배포와 다른 경우 쿼리는 예기치 않은 결과를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="4200f-184">탄력적 쿼리는 처리되는 과정에서 특정 분할된 데이터베이스가 안전하게 제외될 수 있도록 조건자 분할키가 허락할 때 분할된 데이터베이스 제거를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="4200f-185">탄력적 쿼리는 분할된 데이터베이스에서 대부분의 계산을 수행할 수 있는 상황에서 가장 잘 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="4200f-186">일반적으로 분할된 데이터베이스 에서 평가될 수 있는 선택적인 필터 조건자를 가진 최상의 쿼리성능을 얻게 되거나 모든 분할 데이터베이스에서 파티션 정렬 방식으로 수행할 수 있는 분할 키를 조인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="4200f-187">다른 쿼리 패턴은 분할된 데이터베이스에서 많은 양의 데이터를 로드해야 하기 때문에 성능이 좋지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200f-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="4200f-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4200f-188">Next steps</span></span>

* <span data-ttu-id="4200f-189">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="4200f-190">수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="4200f-191">수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="4200f-192">행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="4200f-193">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200f-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
