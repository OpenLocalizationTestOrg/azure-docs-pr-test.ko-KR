---
title: "확장 클라우드 데이터베이스 (수평 분할)에 걸쳐 aaaReport | Microsoft Docs"
description: "toouse는 데이터베이스 데이터베이스 쿼리를 교차 하는 방법"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="264f3-103">확장된 클라우드 데이터베이스에서 보고(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="264f3-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="264f3-104">[탄력적 쿼리](sql-database-elastic-query-overview.md)를 사용하여 단일 연결 지점의 여러 Azure SQL 데이터베이스에서 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="264f3-105">(또한 다음 이라고 알려집니다 "분할") hello 데이터베이스를 가로로 분할 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="264f3-106">기존 데이터베이스를 설정한 경우 참조 [tooscaled 아웃 데이터베이스를 데이터베이스 마이그레이션 기존](sql-database-elastic-convert-to-use-elastic-tools.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="264f3-107">toounderstand hello SQL 개체 필요한 tooquery, 참조 [수평 분할 된 데이터베이스에 걸쳐 쿼리](sql-database-elastic-query-horizontal-partitioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="264f3-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="264f3-108">Prerequisites</span></span>
<span data-ttu-id="264f3-109">다운로드 및 실행 hello [탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="264f3-110">분할 맵 hello 샘플 응용 프로그램을 사용 하 여 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="264f3-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="264f3-111">여기에서는 만듭니다 분할 맵은 다음 데이터 삽입 hello 분할 된 데이터베이스를 여러 분할 영역 함께 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="264f3-112">Tooalready 문제가 발생 하는 경우 분할 된 데이터를 사용 하 여 분할 된 데이터베이스 설치 개, 단계를 수행 하는 hello를 건너뛰고 toohello 다음 섹션을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="264f3-113">빌드 및 실행 hello **탄력적 데이터베이스 도구 시작** 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="264f3-114">Hello 섹션에는 7 단계까지 hello 단계에 따라 [다운로드 하 고 hello 샘플 응용 프로그램을 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="264f3-115">7 단계의 hello 끝 hello 명령 프롬프트에 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![명령 프롬프트][1]
2. <span data-ttu-id="264f3-117">Hello 명령 창에서 "1"을 입력 한 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="264f3-118">Hello shard map manager 만들고 두 명의 분할 된 데이터베이스 toohello 서버에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="264f3-119">그런 다음 "3"을 입력 하 고 키를 눌러 **Enter**; hello 작업을 4 번 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="264f3-120">이 명령은 분할된 데이터베이스에 샘플 데이터행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="264f3-121">hello [Azure 포털](https://portal.azure.com) 3 개의 새 데이터베이스 서버에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio 확인][2]

   <span data-ttu-id="264f3-123">이 시점에서 데이터베이스 간 쿼리는 hello 탄력적 데이터베이스 클라이언트 라이브러리를 통해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="264f3-124">예를 들어 hello 명령 창에서 옵션 4를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="264f3-125">hello 다중 분할 된 데이터베이스 쿼리 결과 항상 한 **UNION ALL** 모든 분할 영역에서 hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="264f3-126">Hello 다음 섹션에서는 분할 영역 간에 hello 데이터의 다양 한 쿼리를 지 원하는 샘플 데이터베이스 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="264f3-127">탄력적 쿼리 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="264f3-127">Create an elastic query database</span></span>
1. <span data-ttu-id="264f3-128">열기 hello [Azure 포털](https://portal.azure.com) 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="264f3-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="264f3-129">Hello에 새 Azure SQL 데이터베이스 만들기 분할 설치와 동일한 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="264f3-130">"ElasticDBQuery" hello 데이터베이스의 이름을</span><span class="sxs-lookup"><span data-stu-id="264f3-130">Name hello database "ElasticDBQuery."</span></span>

    ![Azure 포털 및 가격 책정 계층][3]

    > [!NOTE]
    > <span data-ttu-id="264f3-132">기존 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-132">you can use an existing database.</span></span> <span data-ttu-id="264f3-133">경우 그렇게 할 수 있습니다이 아니어야 싶다는 의사를 tooexecute hello 분할 영역 중 하나에 대 한 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="264f3-134">이 데이터베이스는 hello 탄력적 데이터베이스 쿼리에 대 한 메타 데이터 개체를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="264f3-135">데이터베이스 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="264f3-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="264f3-136">데이터베이스-범위 마스터 키 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="264f3-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="264f3-137">다음은 사용 되는 tooconnect toohello 분할 맵 관리자 및 hello 분할 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="264f3-138">SQL Server Management Studio 또는 Visual Studio의 SQL Server Data Tools를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="264f3-139">TooElasticDBQuery 데이터베이스를 연결 하 고 다음 T-SQL 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="264f3-140">"username" 및 "password" 해야 수 hello 동일의 6 단계에서 사용 되는 로그인 정보로 [다운로드 하 고 hello 샘플 응용 프로그램을 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) 에 [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="264f3-141">외부 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="264f3-141">External data sources</span></span>
<span data-ttu-id="264f3-142">외부 데이터 원본, toocreate hello hello ElasticDBQuery 데이터베이스에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="264f3-143">"CustomerIDShardMap"를 만든 경우 hello 분할 맵 및 shard map manager hello 탄력적 데이터베이스 도구 샘플을 사용 하 여 hello 분할 맵 hello 이름을입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="264f3-144">그러나이 샘플에 대 한 사용자 지정 설치를 사용 하는 경우 다음 것 응용 프로그램에서 선택한 hello shard map 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="264f3-145">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="264f3-145">External tables</span></span>
<span data-ttu-id="264f3-146">Hello ElasticDBQuery 데이터베이스에서 다음 명령을 실행 하 여 hello 분할 영역에 hello Customers 테이블을 일치 하는 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="264f3-147">탄력적 데이터베이스 T-SQL쿼리 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="264f3-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="264f3-148">외부 데이터 원본 및 외부 테이블을 정의한 후 외부 테이블을 통해 전체 T-SQL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="264f3-149">Hello ElasticDBQuery 데이터베이스에서이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="264f3-150">Hello 쿼리 하는 모든 hello 분할 영역에서 결과 집계 하 고 hello 다음 출력을 제공 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![출력 세부 정보][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="264f3-152">탄력적 데이터베이스 쿼리 결과 tooExcel 가져오기</span><span class="sxs-lookup"><span data-stu-id="264f3-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="264f3-153">쿼리 tooan Excel 파일의 hello 결과를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="264f3-154">Excel 2013을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="264f3-155">Toohello 이동 **데이터** 리본.</span><span class="sxs-lookup"><span data-stu-id="264f3-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="264f3-156">**기타 원본에서**을 클릭하고 **SQL Server에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![다른 원본에서 Excel 가져오기][5]
4. <span data-ttu-id="264f3-158">Hello에 **데이터 연결 마법사** hello 서버 이름 및 로그인 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="264f3-159">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-159">Then click **Next**.</span></span>
5. <span data-ttu-id="264f3-160">Hello 대화 상자에서 **원하는 hello 데이터가 들어 있는 Select hello 데이터베이스**선택, hello **ElasticDBQuery** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="264f3-161">선택 hello **고객** hello 목록 뷰에서 테이블 마우스 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="264f3-162">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="264f3-163">Hello에 **데이터 가져오기** 양식의 **표시할 방법을 선택 tooview이이 데이터 통합 문서에서**선택, **테이블** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="264f3-164">행을 hello 모든 **고객** 다른 분할 영역에 저장 된 테이블을 채우는 hello Excel 시트입니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="264f3-165">이제 Excel의 강력한 데이터 시각화 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="264f3-166">Tooconnect BI와 데이터 통합 도구 toohello 탄력적 쿼리 데이터베이스 자격 증명 및 hello 연결 문자열을 서버 이름으로, 데이터베이스 이름에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="264f3-167">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="264f3-168">Toohello 쿼리 탄력적 데이터베이스 및 다른 SQL Server 데이터베이스와 마찬가지로 외부 테이블을 연결 하는 toowith 도구에는 SQL Server 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="264f3-169">비용</span><span class="sxs-lookup"><span data-stu-id="264f3-169">Cost</span></span>
<span data-ttu-id="264f3-170">Hello 탄력적 데이터베이스 쿼리 기능을 사용 하기 위한 추가 비용 없이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264f3-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="264f3-171">가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="264f3-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="264f3-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="264f3-172">Next steps</span></span>

* <span data-ttu-id="264f3-173">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="264f3-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="264f3-174">수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="264f3-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="264f3-175">수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="264f3-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="264f3-176">행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="264f3-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="264f3-177">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="264f3-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
