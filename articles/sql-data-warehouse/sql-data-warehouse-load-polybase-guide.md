---
title: "SQL Data Warehouse의 PolyBase 사용을 위한 가이드 | Microsoft Docs"
description: "SQL 데이터 웨어하우스 시나리오에서 PolyBase를 사용하는 방법에 대한 지침 및 권장 사항입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="076cb-103">SQL 데이터 웨어하우스의 PolyBase 사용을 위한 가이드</span><span class="sxs-lookup"><span data-stu-id="076cb-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="076cb-104">이 가이드는 SQL 데이터 웨어하우스의 PolyBase를 사용하는 방법에 대한 실용적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="076cb-105">시작하려면 [PolyBase를 사용하여 데이터 로드][Load data with PolyBase] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="076cb-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="076cb-106">저장소 키 회전</span><span class="sxs-lookup"><span data-stu-id="076cb-106">Rotating storage keys</span></span>
<span data-ttu-id="076cb-107">때때로 보안을 위해 blob 저장소 액세스 키를 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="076cb-108">이 작업을 수행하는 가장 세련된 방법은 "키 회전" 라고 하는 프로세스를 따르는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="076cb-109">Blob 저장소 계정에 두 개의 저장소 키가 있는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="076cb-110">이는 다음을 전환하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-110">This is so that you can transition</span></span>

<span data-ttu-id="076cb-111">Azure 저장소 계정 키를 회전하는 것은 간단한 3단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="076cb-112">두 번째 저장소 액세스 키를 기반으로 두 번째 데이터베이스 범위가 지정된 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="076cb-113">이 새 자격 증명을 기반으로 두 번째 외부 데이터 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="076cb-114">새 외부 테이블을 끌어 놓고 새 외부 데이터 원본을 가리키는 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="076cb-115">외부 테이블을 새 외부 데이터 원본으로 모두 마이그레이션한 후에 정리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="076cb-116">첫 번째 외부 데이터 원본을 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-116">Drop first external data source</span></span>
2. <span data-ttu-id="076cb-117">기본 저장소 액세스 키를 기반으로 첫 번째 데이터베이스 범위 자격 증명을 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="076cb-118">Azure에 로그인하고 다음 번에 사용할 준비가 된 기본 액세스 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="076cb-119">Azure Blob 저장소 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="076cb-119">Query Azure blob storage data</span></span>
<span data-ttu-id="076cb-120">외부 테이블에 대한 쿼리는 관계형 테이블인 것처럼 테이블 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="076cb-121">외부 테이블에 대한 쿼리가 *"쿼리가 중단되었습니다. 외부 소스에서 읽는 동안 최대 거부 임계값에 도달했습니다."*오류로 인해 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="076cb-122">이는 외부 데이터에 *더티* 레코드가 포함되어 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="076cb-123">열의 실제 데이터 형식/개수가 외부 테이블의 열 정의와 일치하지 않거나 데이터가 지정된 외부 파일 형식에 맞지 않는 경우 데이터 레코드가 '더티'로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="076cb-124">이 문제를 해결하려면 외부 테이블 및 외부 파일 형식 정의가 올바른지, 그리고 외부 데이터가 이러한 정의를 준수하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="076cb-125">외부 데이터 레코드의 하위 집합이 더티인 경우 CREATE EXTERNAL TABLE DDL의 거부 옵션을 사용하여 쿼리에 대해 해당 레코드를 거부하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="076cb-126">Azure Blob 저장소에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="076cb-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="076cb-127">이 예제에서는 SQL 데이터 웨어하우스 데이터베이스로 Azure blob 저장소에서 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="076cb-128">직접 데이터를 저장하면 쿼리를 위한 데이터 전송 시간을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="076cb-129">Columnstore 인덱스를 사용하여 데이터를 저장하면 최대 10배까지 분석 쿼리를 위한 쿼리 성능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="076cb-130">이 예제에서는 CREATE TABLE AS SELECT 문을 사용하여 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="076cb-131">새 테이블은 쿼리에서 명명된 열을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="076cb-132">외부 테이블 정의에서 해당 열의 데이터 형식을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="076cb-133">CREATE TABLE AS SELECT는 SQL 데이터 웨어하우스의 모든 계산 노드에 병렬로 데이터를 로드하는 높은 성능의 Transact-SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="076cb-134">분석 플랫폼 시스템에는 방대한 병렬 처리(MPP) 엔진을 처음 개발했으며 이제 SQL 데이터 웨어하우스에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="076cb-135">[CREATE TABLE AS SELECT(Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="076cb-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="076cb-136">새로 로드한 데이터에 대한 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="076cb-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="076cb-137">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="076cb-138">쿼리에서 최상의 성능을 얻으려면, 데이터를 처음 로드하거나 데이터에 상당한 변화가 발생한 후에 모든 테이블의 모든 열에서 통계가 만들어지는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="076cb-139">통계에 대한 자세한 설명은 개발 항목 그룹의 [통계][Statistics] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="076cb-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="076cb-140">다음은 이 예제에 로드한 테이블에 대한 통계를 만드는 방법을 간략히 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="076cb-141">Azure Blob 저장소에 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="076cb-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="076cb-142">이 섹션은 SQL 데이터 웨어하우스에서 Azure Blob 저장소로 데이터를 내보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="076cb-143">이 예에서는 모든 계산 노드에서 병렬로 데이터를 내보내는 높은 성능의 Transact-SQL 문인 CREATE EXTERNAL TABLE AS SELECT를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="076cb-144">다음 예에서는 dbo.Weblogs 표에서 열 정의 및 데이터를 사용하여 외부 표 Weblogs2014를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="076cb-145">외부 표 정의는 SQL 데이터 웨어하우스에 저장되며 SELECT 문의 결과는 데이터 원본에서 정의한 Blob 컨테이너 아래에 있는 “/archive/log2014/” 디렉터리로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="076cb-146">데이터는 지정된 텍스트 파일 형식으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-146">The data is exported in the specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="076cb-147">사용자 로드 격리</span><span class="sxs-lookup"><span data-stu-id="076cb-147">Isolate Loading Users</span></span>
<span data-ttu-id="076cb-148">SQL DW로 데이터를 로드할 수 있는 여러 명의 사용자가 필요한 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="076cb-149">[CREATE TABLE AS SELECT(Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]는 데이터베이스의 CONTROL 권한이 필요하므로 모든 스키마에 대한 제어 액세스가 있는 여러 명의 사용자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="076cb-150">이를 제한하기 위해 DENY CONTROL 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="076cb-151">예: 데이터베이스 스키마, 부서 A에 대한 스키마_A 및 부서 B에 대한 스키마_B를 가정합니다. 데이터베이스 사용자, 사용자_A 및 사용자_B가 부서 A와 B 각각에서 PolyBase 로딩에 대한 사용자가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="076cb-152">둘 모두 데이터베이스 CONTROL 권한을 부여 받습니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="076cb-153">스키마 A와 B의 작성자는 이제 DENY를 사용하여 해당 스키마를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="076cb-154">이로 인해 사용자_A 및 사용자_B는 이제 다른 부서의 스키마에서 차단되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="076cb-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="076cb-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="076cb-155">Next steps</span></span>
<span data-ttu-id="076cb-156">SQL Data Warehouse로 데이터를 이동하는 방법에 대한 자세한 내용은 [데이터 마이그레이션 개요][data migration overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="076cb-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
