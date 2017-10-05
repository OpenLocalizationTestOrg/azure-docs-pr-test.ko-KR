---
title: "확장된 클라우드 데이터베이스에서 보고(수평 분할) | Microsoft Docs"
description: "데이터베이스 간 쿼리 사용 방법"
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
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="20fb5-103">확장된 클라우드 데이터베이스에서 보고(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="20fb5-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="20fb5-104">[탄력적 쿼리](sql-database-elastic-query-overview.md)를 사용하여 단일 연결 지점의 여러 Azure SQL 데이터베이스에서 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="20fb5-105">데이터베이스를 가로로 분할해야 합니다("분할됨"이라고도 함).</span><span class="sxs-lookup"><span data-stu-id="20fb5-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="20fb5-106">기존 데이터베이스를 사용하는 경우 [확장된 데이터베이스에 기존 데이터베이스 마이그레이션](sql-database-elastic-convert-to-use-elastic-tools.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="20fb5-107">쿼리에 필요한 SQL 개체를 알아보려면 [수평 분할된 데이터베이스에 쿼리](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20fb5-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="20fb5-108">Prerequisites</span></span>
<span data-ttu-id="20fb5-109">[탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)을 다운로드하고 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="20fb5-110">샘플 응용 프로그램을 사용하여 분할된 데이터베이스 맵 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="20fb5-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="20fb5-111">분할된 데이터베이스 안의 삽입된 데이터에 따라 여느 분할된 데이터 베이스와 마찬가지로 분할된 데이터 베이스 관리자를 만들수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="20fb5-112">이미 분할된 데이터가 설치되어 있는 분할된 데이터베이스가 있다면, 다음 단계들을 건너뛰고 다음 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="20fb5-113">**탄력적 데이터베이스 도구 응용 프로그램** 을 빌드하고 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="20fb5-114">[샘플 앱 다운로드 및 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)섹션에서 7단계까지 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="20fb5-115">7단계를 끝내면 다음 명령 프롬프트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![명령 프롬프트][1]
2. <span data-ttu-id="20fb5-117">명령 창에 "1"을 입력하고 **Enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="20fb5-118">이 명령은 분할된 데이터베이스 관리자를 생성 및 두 분할된 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="20fb5-119">그런 다음 "3"을 입력하고 **Enter**키를 누릅니다: 작업을 4번 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="20fb5-120">이 명령은 분할된 데이터베이스에 샘플 데이터행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="20fb5-121">[Azure Portal](https://portal.azure.com)에서 사용자의 서버 내에 다음과 같은 3개의 새 데이터베이스가 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio 확인][2]

   <span data-ttu-id="20fb5-123">이 시점에 데이터베이스 간 쿼리는 탄력적 데이터베이스 클라이언트 라이브러리를 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="20fb5-124">예를 들면, 명령창에 있는 옵션4를 이용합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="20fb5-125">다중 분할된 데이터베이스 쿼리에서 나온 결과는 항상 모든 분할된 데이터베이스의 **UNION ALL** 입니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="20fb5-126">다음 섹션에서는 분할 된 데이터베이스 간 데이터의 다양한 쿼리를 지원하는 샘플 데이터베이스 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="20fb5-127">탄력적 쿼리 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="20fb5-127">Create an elastic query database</span></span>
1. <span data-ttu-id="20fb5-128">[Azure Portal](https://portal.azure.com)을 열고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="20fb5-129">분할 된 데이터베이스를 설치한 동일 서버에서 새 Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="20fb5-130">데이터베이스 이름을"ElasticDBQuery."로 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-130">Name the database "ElasticDBQuery."</span></span>

    ![Azure 포털 및 가격 책정 계층][3]

    > [!NOTE]
    > <span data-ttu-id="20fb5-132">기존 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-132">you can use an existing database.</span></span> <span data-ttu-id="20fb5-133">그럴 경우, 사용자가 실행하고 싶은 쿼리가 포함된 분할된 데이터베이스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="20fb5-134">이 데이터베이스는 탄력적 데이터베이스 쿼리에 대한 메타데이터 개체를 만들기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="20fb5-135">데이터베이스 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="20fb5-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="20fb5-136">데이터베이스-범위 마스터 키 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="20fb5-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="20fb5-137">분할된 데이터베이스와 분할된 데이터베이스 관리자를 연결하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="20fb5-138">SQL Server Management Studio 또는 Visual Studio의 SQL Server Data Tools를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="20fb5-139">ElasticDBQuery 데이터베이스에 연결한 다음 T-SQL 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="20fb5-140">"username" 및 "password"는 [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)의 [샘플 응용 프로그램 다운로드 및 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)의 6단계에서 사용한 로그인 정보와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="20fb5-141">외부 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="20fb5-141">External data sources</span></span>
<span data-ttu-id="20fb5-142">외부 데이터 소스를 만들려면 ElasticDBQuery 데이터베이스에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="20fb5-143">탄력적 데이터베이스 도구 샘플로  분할된 데이터베이스와 관리자를 만든 경우, "CustomerIDShardMap"가 분할된 데이터베이스 맵의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="20fb5-144">그러나, 이 샘플에서 사용자 설치를 사용했다면, 응용 프로그램 내에서 분할된 데이터베이스 이름을 정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="20fb5-145">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="20fb5-145">External tables</span></span>
<span data-ttu-id="20fb5-146">ElasticDBQuery database의 명령을 실행하여 분할된 데이터베이스의 사용자 테이블과 일치하는 외부테이블을 만들수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="20fb5-147">탄력적 데이터베이스 T-SQL쿼리 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="20fb5-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="20fb5-148">외부 데이터 원본 및 외부 테이블을 정의한 후 외부 테이블을 통해 전체 T-SQL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="20fb5-149">ElasticDBQuery 데이터베이스에서 다음쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="20fb5-150">모든 분할된 데이터베이스에서 쿼리를 집계한 결과 및 다음 출력이 지정됨을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![출력 세부 정보][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="20fb5-152">탄력적 데이터베이스 쿼리 결과를 Excel로 가져오기</span><span class="sxs-lookup"><span data-stu-id="20fb5-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="20fb5-153">쿼리의 결과를 엑셀파일로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="20fb5-154">Excel 2013을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="20fb5-155">**데이터** 리본을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="20fb5-156">**기타 원본에서**을 클릭하고 **SQL Server에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![다른 원본에서 Excel 가져오기][5]
4. <span data-ttu-id="20fb5-158">**데이터 연결 마법사** 에서 서버 이름 및 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="20fb5-159">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-159">Then click **Next**.</span></span>
5. <span data-ttu-id="20fb5-160">대화 상자에서 **원하는 데이터를 포함하는 데이터베이스를 선택**하고 **ElasticDBQuery** 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="20fb5-161">목록 보기에서 **사용자**테이블을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="20fb5-162">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="20fb5-163">**데이터 가져오기** 양식에서, **통합 문서에서 원하는 데이터를 보는 방법을 선택**하고 **테이블**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="20fb5-164">다른 분할된 데이터베이스에 저장된 **Customers** 테이블의 모든 행으로 Excel 시트를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="20fb5-165">이제 Excel의 강력한 데이터 시각화 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="20fb5-166">탄력적 쿼리 데이터 베이스의 데이터 통합 도구 및 BI과 연결하기 위해 서버 이름, 데이터베이스 이름, 자격 증명과 연결 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="20fb5-167">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="20fb5-168">탄력적 쿼리 데이터베이스 및 기타 SQL Server 데이터베이스와 마찬가지로 외부 테이블 및 도구와 연결할 수 있는 SQL Server 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="20fb5-169">비용</span><span class="sxs-lookup"><span data-stu-id="20fb5-169">Cost</span></span>
<span data-ttu-id="20fb5-170">탄력적 데이터베이스 쿼리 기능을 사용 하는 것은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="20fb5-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="20fb5-171">가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20fb5-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20fb5-172">Next steps</span></span>

* <span data-ttu-id="20fb5-173">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="20fb5-174">수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="20fb5-175">수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="20fb5-176">행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="20fb5-177">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20fb5-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
