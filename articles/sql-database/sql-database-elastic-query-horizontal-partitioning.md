---
title: "확장 클라우드 데이터베이스에 걸쳐 aaaReporting | Microsoft Docs"
description: "어떻게 tooset 수평 분할에 대 한 유연한 쿼리를"
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
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="6f919-103">확장된 클라우드 데이터베이스에서 보고(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="6f919-103">Reporting across scaled-out cloud databases (preview)</span></span>
![분할된 데이터베이스에 대한 쿼리][1]

<span data-ttu-id="6f919-105">분할된 데이터베이스는 확장된 데이터 계층에 행을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="6f919-106">hello 스키마는 수평 분할이 라고도 하는 모든 참가 데이터베이스에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="6f919-107">탄력적 쿼리를 사용하여 분할된 데이터베이스의 모든 데이터베이스를 망라하는 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="6f919-108">빠른 시작은 [확장된 클라우드 데이터베이스에서 보고](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="6f919-109">비분할 데이터베이스의 경우 [여러 스키마를 사용하여 클라우드 데이터베이스에서 쿼리](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6f919-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6f919-110">Prerequisites</span></span>
* <span data-ttu-id="6f919-111">Hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 분할 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="6f919-112">[분할된 데이터베이스 맵 관리](sql-database-elastic-scale-shard-map-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="6f919-113">Hello 샘플 응용 프로그램에서 사용 하 여 또는 [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="6f919-114">참조 또는 [tooscaled 아웃 데이터베이스를 데이터베이스 마이그레이션 기존](sql-database-elastic-convert-to-use-elastic-tools.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="6f919-115">hello 사용자가 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="6f919-116">이 사용 권한은 hello ALTER DATABASE 권한이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="6f919-117">ALTER ANY EXTERNAL DATA SOURCE 권한은 필요한 toorefer toohello 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="6f919-118">개요</span><span class="sxs-lookup"><span data-stu-id="6f919-118">Overview</span></span>
<span data-ttu-id="6f919-119">이러한 문은 hello 탄력적 쿼리 데이터베이스에 분할 된 데이터 계층의 메타 데이터 표현을 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="6f919-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="6f919-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="6f919-121">데이터베이스 범위 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="6f919-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="6f919-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="6f919-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="6f919-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="6f919-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="6f919-124">1.1 데이터베이스 범위 마스터 키 및 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="6f919-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="6f919-125">hello 자격 증명 hello 탄력적 쿼리 tooconnect tooyour 원격 데이터베이스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="6f919-126">해당 hello 있는지 확인 *"\<username\>"* 포함 하지 않습니다 *"@servername"* 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="6f919-127">1.2 외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="6f919-127">1.2 Create external data sources</span></span>
<span data-ttu-id="6f919-128">구문</span><span class="sxs-lookup"><span data-stu-id="6f919-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="6f919-129">예제</span><span class="sxs-lookup"><span data-stu-id="6f919-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="6f919-130">Hello 현재 외부 데이터 원본 목록 검색:</span><span class="sxs-lookup"><span data-stu-id="6f919-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="6f919-131">hello 외부 데이터 원본에는 분할 맵을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-131">hello external data source references your shard map.</span></span> <span data-ttu-id="6f919-132">탄력적 쿼리 hello 외부 데이터 원본 및 shard map tooenumerate hello 데이터베이스 hello 데이터 계층에 참여 하는 기본 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="6f919-133">hello 동일한 자격 증명이 사용 되는 tooread hello 분할 맵은 및 tooaccess 탄력적 쿼리 hello 처리 하는 동안 hello 분할 영역에 데이터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="6f919-134">1.3 외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="6f919-134">1.3 Create external tables</span></span>
<span data-ttu-id="6f919-135">구문</span><span class="sxs-lookup"><span data-stu-id="6f919-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="6f919-136">**예제**</span><span class="sxs-lookup"><span data-stu-id="6f919-136">**Example**</span></span>

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

<span data-ttu-id="6f919-137">Hello 현재 데이터베이스에서 외부 테이블 hello 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="6f919-138">외부 테이블 toodrop:</span><span class="sxs-lookup"><span data-stu-id="6f919-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="6f919-139">설명</span><span class="sxs-lookup"><span data-stu-id="6f919-139">Remarks</span></span>
<span data-ttu-id="6f919-140">hello 데이터\_소스 절 hello 외부 테이블에 사용 되는 hello 외부 데이터 원본 (shard map)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="6f919-141">hello 스키마\_이름 및 개체\_이름 절 hello 외부 테이블 정의 tooa 테이블 다른 스키마에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="6f919-142">생략 하면 hello 원격 개체의 hello 스키마는 toobe "dbo" 하 해당 이름이 toobe 동일한 toohello 외부 테이블의 이름을 정의 하 고 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="6f919-143">원격 테이블의 이름으로 hello을 이미 수행 hello 데이터베이스 toocreate hello에 대 한 외부 테이블을 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="6f919-144">예를 들어 toodefine 외부 테이블 tooget 카탈로그 뷰에 대 한 집계 뷰를 원하는 또는 수평 확장 된 데이터에 대해 Dmv 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="6f919-145">카탈로그 뷰 및 Dmv 로컬로 존재 이미, hello 외부 테이블 정의 대 한 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="6f919-146">대신 다른 이름을 사용 하 고 hello 카탈로그 뷰를 사용 하거나 hello 스키마에서에서 DMV의 이름을 hello\_이름 및/또는 개체\_이름 절.</span><span class="sxs-lookup"><span data-stu-id="6f919-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="6f919-147">(아래의 hello 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="6f919-147">(See hello example below.)</span></span> 

<span data-ttu-id="6f919-148">hello 배포 절이이 테이블에 사용 되는 hello 데이터 분포를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="6f919-149">hello 쿼리 프로세서에서 hello 배포 절 toobuild hello 가장 효율적인 쿼리 계획에서 제공 하는 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="6f919-150">**분할 된** hello 데이터베이스 간에 데이터를 행 분할을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="6f919-151">hello 데이터 분포는 hello에 대 한 분할 키 hello **< sharding_column_name >** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="6f919-152">**복제** hello 테이블의 동일한 복사본은 각 데이터베이스에 있는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="6f919-153">것 프로그램 책임 tooensure hello 데이터베이스에 걸쳐 hello 복제본은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="6f919-154">**ROUND\_로빈** 응용 프로그램에 따라 배포 방법을 사용 하 여 해당 hello 테이블 행 분할을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="6f919-155">**데이터 계층 참조**: hello 외부 테이블 DDL tooan 외부 데이터 원본을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="6f919-156">hello 외부 데이터 원본은 데이터 계층의 모든 hello 데이터베이스 hello 정보 필요한 toolocate 있는 hello 외부 테이블을 제공 하는 분할 맵을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="6f919-157">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6f919-157">Security considerations</span></span>
<span data-ttu-id="6f919-158">Access toohello 외부 테이블에 있는 사용자는 자동으로 액세스할 toohello hello 외부 데이터 원본 정의에 지정 된 hello 자격 증명에서 기본 원격 테이블 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="6f919-159">원치 않는 hello 외부 데이터 원본의 hello 자격 증명을 통해 권한 상승을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="6f919-160">일반 테이블인 것처럼 외부 테이블에 GRANT 또는 REVOKE를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="6f919-161">외부 데이터 원본 및 외부 테이블을 정의한 후 외부 테이블을 통해 전체 T-SQL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="6f919-162">예: 수평 분할된 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="6f919-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="6f919-163">hello 다음 쿼리 웨어하우스, 주문 및 주문 라인 간에 세 방향 조인을 수행 하 고 여러 집계 및 선택적 필터를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="6f919-164">가정 (1) 가로 분할 (분할) 및 (2) 웨어하우스, 주문 및 주문 라인 hello 웨어하우스 id 열으로 분할를 hello 탄력적 쿼리 하는 hello 조인 hello 분할 영역에 배치 하 고 hello에 hello 쿼리 비용이 많이 드는 부분은 hello를 처리할 수 있습니다. 동시에 분할 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="6f919-165">원격 T-SQL 실행을 위한 저장 프로시저: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="6f919-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="6f919-166">탄력적 쿼리도 toohello 분할 된 데이터베이스에 직접 액세스를 제공 하는 저장된 프로시저를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="6f919-167">hello 저장된 프로시저를 호출 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714) tooexecute 사용 되는 원격 저장된 프로시저 또는 hello 원격 데이터베이스의 T-SQL 코드 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="6f919-168">Hello 매개 변수를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="6f919-169">데이터 원본 이름 (nvarchar): hello 이름 hello 유형의 RDBMS 외부 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="6f919-170">쿼리 (nvarchar): hello T-SQL 쿼리 toobe 각 분할 된 데이터베이스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="6f919-171">선택적 매개 변수 선언 (nvarchar)-: hello 쿼리 매개 변수 (예: sp_executesql)에서 사용 되는 hello 매개 변수에 대 한 데이터 형식 정의 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="6f919-172">매개 변수 값 목록, 선택 사항: 쉼표로 구분한 매개 변수 값(예: sp_executesql) 목록.</span><span class="sxs-lookup"><span data-stu-id="6f919-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="6f919-173">hello sp\_실행\_원격 사용 하 여 hello hello 호출 매개 변수 tooexecute hello hello 원격 데이터베이스의 T-SQL 문을 들에 제공 된 외부 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="6f919-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="6f919-174">Hello 외부 데이터 원본 tooconnect toohello shardmap manager 데이터베이스 및 hello 원격 데이터베이스의 hello 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="6f919-175">예제:</span><span class="sxs-lookup"><span data-stu-id="6f919-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="6f919-176">도구에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="6f919-176">Connectivity for tools</span></span>
<span data-ttu-id="6f919-177">일반 SQL Server 연결 문자열 tooconnect를 사용 하 여 응용 프로그램, BI 및 데이터 통합 도구 toohello 데이터베이스 외부 테이블 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="6f919-178">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="6f919-179">그런 다음 다른 SQL Server 연결 된 데이터베이스 toohello 도구를 같은 hello 탄력적 쿼리 데이터베이스를 참조 하 고 큐브인 것 처럼 로컬 테이블 도구 또는 응용 프로그램에서 외부 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="6f919-180">모범 사례</span><span class="sxs-lookup"><span data-stu-id="6f919-180">Best practices</span></span>
* <span data-ttu-id="6f919-181">해당 hello 탄력적 쿼리 끝점 데이터베이스 액세스 toohello shardmap 데이터베이스와 모든 분할 영역 hello SQL DB 방화벽을 통해 부여 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="6f919-182">유효성 검사 또는 hello 외부 테이블에 정의 된 hello 데이터 분산을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="6f919-183">실제 데이터 분포 테이블 정의에 지정 된 hello 배포와에서 다른 경우 쿼리는 예기치 않은 결과 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="6f919-184">탄력적 쿼리 현재 수행 하지 않습니다 분할 elimination hello 분할 키에 대 한 조건자를 toosafely 제외 허용 하는 경우 특정 분할 영역 처리에서.</span><span class="sxs-lookup"><span data-stu-id="6f919-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="6f919-185">탄력적 쿼리 적합 쿼리에 대 한 대부분 hello 계산의 hello 분할 된 데이터베이스에서 수행할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="6f919-186">일반적으로 얻게 hello 최고의 쿼리 성능을 평가할 수 있는 선택적 필터 조건자와 조인 또는 hello 분할 된 데이터베이스에 분할 키 모든 분할 영역에 파티션 정렬 방식으로 수행할 수 있는 hello를 통해.</span><span class="sxs-lookup"><span data-stu-id="6f919-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="6f919-187">다른 쿼리 패턴 tooload 많은 양의 데이터 hello 분할 영역 toohello 헤드 노드를 할 수 및 성능이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f919-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f919-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f919-188">Next steps</span></span>

* <span data-ttu-id="6f919-189">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="6f919-190">수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="6f919-191">수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="6f919-192">행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="6f919-193">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f919-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
