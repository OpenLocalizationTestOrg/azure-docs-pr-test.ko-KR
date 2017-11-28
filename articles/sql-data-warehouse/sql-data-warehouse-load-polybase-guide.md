---
title: "PolyBase를 사용 하 여 SQL 데이터 웨어하우스에 대 한 aaaGuide | Microsoft Docs"
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
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="ad9c6-103">SQL 데이터 웨어하우스의 PolyBase 사용을 위한 가이드</span><span class="sxs-lookup"><span data-stu-id="ad9c6-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="ad9c6-104">이 가이드는 SQL 데이터 웨어하우스의 PolyBase를 사용하는 방법에 대한 실용적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="ad9c6-105">시작 tooget 참조 hello [PolyBase 사용 하 여 데이터 로드] [ Load data with PolyBase] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="ad9c6-106">저장소 키 회전</span><span class="sxs-lookup"><span data-stu-id="ad9c6-106">Rotating storage keys</span></span>
<span data-ttu-id="ad9c6-107">시간 tootime에서 toochange hello 액세스 키 tooyour blob 저장소를 보안상의 이유로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="ad9c6-108">이 작업은 toofollow 프로세스를 "hello 키 회전" 라고 하는 뛰어난 방식으로 tooperform을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="ad9c6-109">Blob 저장소 계정에 두 개의 저장소 키가 있는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="ad9c6-110">이는 다음을 전환하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-110">This is so that you can transition</span></span>

<span data-ttu-id="ad9c6-111">Azure 저장소 계정 키를 회전하는 것은 간단한 3단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="ad9c6-112">Hello 보조 저장소 액세스 키에 따라 두 번째 데이터베이스 범위 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="ad9c6-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="ad9c6-113">이 새 자격 증명을 기반으로 두 번째 외부 데이터 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="ad9c6-114">삭제 하 고 toohello 새 외부 데이터 원본을 가리키는 hello 외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="ad9c6-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="ad9c6-115">다음을 수행할 수 있습니다 모든 외부 테이블 toohello 새 외부 데이터 원본의 마이그레이션한 hello 작업을 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="ad9c6-116">첫 번째 외부 데이터 원본을 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-116">Drop first external data source</span></span>
2. <span data-ttu-id="ad9c6-117">첫 번째 데이터베이스를 삭제 범위 hello 기본 저장소 액세스 키에 따라 자격 증명</span><span class="sxs-lookup"><span data-stu-id="ad9c6-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="ad9c6-118">Azure에 로그인 하 고 번 hello에 대 한 준비 hello 기본 액세스 키를 다시 생성</span><span class="sxs-lookup"><span data-stu-id="ad9c6-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="ad9c6-119">Azure Blob 저장소 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="ad9c6-119">Query Azure blob storage data</span></span>
<span data-ttu-id="ad9c6-120">외부 테이블에 대 한 쿼리를 관계형 테이블 인 것 처럼 hello 테이블 이름을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="ad9c6-121">외부 테이블에 대 한 쿼리는 hello 오류와 함께 실패할 수 있습니다 *"쿼리가 중단-외부 원본에서 읽는 동안 hello 최대 거부 임계값에 도달 했습니다"*합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="ad9c6-122">이는 외부 데이터에 *더티* 레코드가 포함되어 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="ad9c6-123">데이터 레코드 hello 실제 데이터 형식/열 수가 hello 외부 테이블의 열 정의 hello 일치 하지 않는 경우 또는 hello 데이터가 toohello 지정 된 외부 파일 형식에 맞지 않습니다 경우 '더티'으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="ad9c6-124">toofix이, 외부 테이블 및 외부 파일 형식 정의 정확 하 고 toothese 정의 준수 하려면 외부 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="ad9c6-125">외부 데이터 레코드의 하위 집합을 변경 하는 경우 선택할 수 있습니다 tooreject 이러한 레코드 쿼리에 대 한 외부 테이블 DDL 만들기의 hello 거부 옵션을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="ad9c6-126">Azure Blob 저장소에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="ad9c6-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="ad9c6-127">이 예제에서는 Azure blob 저장소 tooSQL 데이터 웨어하우스 데이터베이스에서 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="ad9c6-128">쿼리에 대 한 데이터 전송 시간이 hello 제거 직접 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="ad9c6-129">Columnstore 인덱스를 사용 하 여 데이터 저장 too10x 구성 하 여 분석 쿼리에 대 한 쿼리 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="ad9c6-130">이 예제는 hello CREATE TABLE AS SELECT 문이 tooload 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="ad9c6-131">새 테이블 hello hello 쿼리에서 명명 된 hello 열을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="ad9c6-132">Hello 외부 테이블 정의에서 해당 열의 데이터 형식을 hello를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="ad9c6-133">CREATE TABLE AS SELECT는 성능이 병렬 tooall hello에 hello 데이터를 로드 하는 TRANSACT-SQL 문을의 계산 노드 SQL 데이터 웨어하우스입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="ad9c6-134">분석 플랫폼 시스템에 hello 방대한 병렬 처리 (MPP) 엔진에 대 한 원래 개발 된 하 고 SQL 데이터 웨어하우스에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

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

<span data-ttu-id="ad9c6-135">[CREATE TABLE AS SELECT(Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="ad9c6-136">새로 로드한 데이터에 대한 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="ad9c6-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="ad9c6-137">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="ad9c6-138">순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 통계 hello 첫 번째 로드 한 후 모든 테이블의 모든 열에 만들 수 또는 hello 데이터에서 발생 된 모든 주요 부분을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="ad9c6-139">통계에 대 한 자세한 내용은 참조 hello [통계] [ Statistics] hello 개발 그룹 항목의 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="ad9c6-140">다음은이 예에서 테이블 hello에 대 한 toocreate 통계 로드 하는 방법에 대 한 빠른 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="ad9c6-141">데이터 tooAzure blob 저장소 내보내기</span><span class="sxs-lookup"><span data-stu-id="ad9c6-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="ad9c6-142">이 섹션에서는 어떻게 tooexport 데이터로 SQL 데이터 웨어하우스 tooAzure blob 저장소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="ad9c6-143">이 예에서는 CREATE EXTERNAL TABLE AS SELECT는 항상 고성능 TRANSACT-SQL 문을 tooexport hello 데이터 인 모든 hello 계산 노드에서 동시에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="ad9c6-144">hello 다음 예제에서는 열 정 및 데이터 dbo에서 사용 하 여 외부 테이블 Weblogs2014 웹 로그 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="ad9c6-145">hello 외부 테이블 정의 SQL 데이터 웨어하우스에 저장 되 고 hello hello SELECT 문의 결과 내보낸된 toohello hello 데이터 원본에 의해 지정 된 hello blob 컨테이너 아래에 "/ / log2014/보관" 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="ad9c6-146">hello 데이터 hello 지정 된 텍스트 파일 형식으로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-146">hello data is exported in hello specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="ad9c6-147">사용자 로드 격리</span><span class="sxs-lookup"><span data-stu-id="ad9c6-147">Isolate Loading Users</span></span>
<span data-ttu-id="ad9c6-148">있습니다 필요 toohave SQL DW로 데이터를 로드할 수 있는 여러 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="ad9c6-149">때문에 hello [CREATE TABLE AS SELECT (Transact SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] 제어 권한이 필요한 hello 데이터베이스의 하면 결국 액세스 제어로 여러 명의 사용자와 모든 스키마를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="ad9c6-150">toolimit이 hello 거부 제어 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="ad9c6-151">예: 데이터베이스 스키마, 부서 A에 대한 스키마_A 및 부서 B에 대한 스키마_B를 가정합니다. 데이터베이스 사용자, 사용자_A 및 사용자_B가 부서 A와 B 각각에서 PolyBase 로딩에 대한 사용자가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="ad9c6-152">둘 모두 데이터베이스 CONTROL 권한을 부여 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="ad9c6-153">A와 B 거부를 사용 하 여 해당 스키마를 이제 잠근 스키마의 hello 작성자:</span><span class="sxs-lookup"><span data-stu-id="ad9c6-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="ad9c6-154">이 user_A 및 user_B 해야 이제 잠길 수 hello에서 다른 부서 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="ad9c6-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad9c6-155">Next steps</span></span>
<span data-ttu-id="ad9c6-156">이동 데이터 tooSQL 데이터 웨어하우스에 대 한 자세한 정보는 toolearn 참조 hello [데이터 마이그레이션 개요][data migration overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="ad9c6-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

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
