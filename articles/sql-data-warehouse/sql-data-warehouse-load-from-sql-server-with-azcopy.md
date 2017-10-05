---
title: "SQL Server에서 Azure SQL Data Warehouse로 데이터 로드(PolyBase) | Microsoft Docs"
description: "bcp를 사용하여 SQL Server에서 플랫 파일로 데이터를 내보내고 AZCopy를 사용하여 Azure Blob 저장소로 데이터를 가져오고, PolyBase를 사용하여 Azure SQL 데이터 웨어하우스로 데이터를 수집합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="570c8-103">SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(AZCopy)</span><span class="sxs-lookup"><span data-stu-id="570c8-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="570c8-104">SQL Server에서 Azure Blob 저장소로 데이터를 로드하려면 bcp 및 AZCopy 명령줄 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="570c8-105">그 다음 PolyBase 또는 Azure Data Factory를 사용하여 Azure SQL 데이터 웨어하우스로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="570c8-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="570c8-106">Prerequisites</span></span>
<span data-ttu-id="570c8-107">이 자습서를 단계별로 실행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="570c8-108">SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="570c8-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="570c8-109">설치된 bcp 명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="570c8-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="570c8-110">설치된 SQLCMD 명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="570c8-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="570c8-111">[Microsoft 다운로드 센터][Microsoft Download Center]에서 bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="570c8-112">SQL 데이터 웨어하우스로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="570c8-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="570c8-113">이 자습서에서는 Azure SQL 데이터 웨어하우스에서 테이블을 만들고 테이블로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="570c8-114">1단계: Azure SQL 데이터 웨어하우스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="570c8-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="570c8-115">명령 프롬프트에서 sqlcmd를 사용하여 다음 쿼리를 실행하여 인스턴스에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> <span data-ttu-id="570c8-116">SQL Data Warehouse에서 테이블을 만드는 방법과 WITH 절에서 사용 가능한 옵션에 대한 자세한 내용은 [테이블 개요][Table Overview] 또는 [CREATE TABLE 구문][CREATE TABLE syntax]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="570c8-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="570c8-117">2단계: 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="570c8-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="570c8-118">메모장을 열고 다음 데이터 줄을 새 텍스트 파일에 복사한 다음 이 파일을 로컬 임시 디렉터리 C:\Temp\DimDate2.txt에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="570c8-119">해당 bcp.exe는 UTF-8 파일 인코딩을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="570c8-120">bcp.exe 사용 시 파일에 ASCII 파일 또는 UTF-16 인코딩 파일을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="570c8-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="570c8-121">3단계: 데이터 연결 및 가져오기</span><span class="sxs-lookup"><span data-stu-id="570c8-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="570c8-122">bcp를 사용하여, 연결하고 값을 적절하게 대체하는 다음 명령을 사용하여 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="570c8-123">sqlcmd에서 다음 쿼리를 실행하여 데이터가 로드되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="570c8-124">다음 결과를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-124">This should return the following results:</span></span>

| <span data-ttu-id="570c8-125">DateId</span><span class="sxs-lookup"><span data-stu-id="570c8-125">DateId</span></span> | <span data-ttu-id="570c8-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="570c8-126">CalendarQuarter</span></span> | <span data-ttu-id="570c8-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="570c8-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="570c8-128">20150101</span><span class="sxs-lookup"><span data-stu-id="570c8-128">20150101</span></span> |<span data-ttu-id="570c8-129">1</span><span class="sxs-lookup"><span data-stu-id="570c8-129">1</span></span> |<span data-ttu-id="570c8-130">3</span><span class="sxs-lookup"><span data-stu-id="570c8-130">3</span></span> |
| <span data-ttu-id="570c8-131">20150201</span><span class="sxs-lookup"><span data-stu-id="570c8-131">20150201</span></span> |<span data-ttu-id="570c8-132">1</span><span class="sxs-lookup"><span data-stu-id="570c8-132">1</span></span> |<span data-ttu-id="570c8-133">3</span><span class="sxs-lookup"><span data-stu-id="570c8-133">3</span></span> |
| <span data-ttu-id="570c8-134">20150301</span><span class="sxs-lookup"><span data-stu-id="570c8-134">20150301</span></span> |<span data-ttu-id="570c8-135">1</span><span class="sxs-lookup"><span data-stu-id="570c8-135">1</span></span> |<span data-ttu-id="570c8-136">3</span><span class="sxs-lookup"><span data-stu-id="570c8-136">3</span></span> |
| <span data-ttu-id="570c8-137">20150401</span><span class="sxs-lookup"><span data-stu-id="570c8-137">20150401</span></span> |<span data-ttu-id="570c8-138">2</span><span class="sxs-lookup"><span data-stu-id="570c8-138">2</span></span> |<span data-ttu-id="570c8-139">4</span><span class="sxs-lookup"><span data-stu-id="570c8-139">4</span></span> |
| <span data-ttu-id="570c8-140">20150501</span><span class="sxs-lookup"><span data-stu-id="570c8-140">20150501</span></span> |<span data-ttu-id="570c8-141">2</span><span class="sxs-lookup"><span data-stu-id="570c8-141">2</span></span> |<span data-ttu-id="570c8-142">4</span><span class="sxs-lookup"><span data-stu-id="570c8-142">4</span></span> |
| <span data-ttu-id="570c8-143">20150601</span><span class="sxs-lookup"><span data-stu-id="570c8-143">20150601</span></span> |<span data-ttu-id="570c8-144">2</span><span class="sxs-lookup"><span data-stu-id="570c8-144">2</span></span> |<span data-ttu-id="570c8-145">4</span><span class="sxs-lookup"><span data-stu-id="570c8-145">4</span></span> |
| <span data-ttu-id="570c8-146">20150701</span><span class="sxs-lookup"><span data-stu-id="570c8-146">20150701</span></span> |<span data-ttu-id="570c8-147">3</span><span class="sxs-lookup"><span data-stu-id="570c8-147">3</span></span> |<span data-ttu-id="570c8-148">1</span><span class="sxs-lookup"><span data-stu-id="570c8-148">1</span></span> |
| <span data-ttu-id="570c8-149">20150801</span><span class="sxs-lookup"><span data-stu-id="570c8-149">20150801</span></span> |<span data-ttu-id="570c8-150">3</span><span class="sxs-lookup"><span data-stu-id="570c8-150">3</span></span> |<span data-ttu-id="570c8-151">1</span><span class="sxs-lookup"><span data-stu-id="570c8-151">1</span></span> |
| <span data-ttu-id="570c8-152">20150801</span><span class="sxs-lookup"><span data-stu-id="570c8-152">20150801</span></span> |<span data-ttu-id="570c8-153">3</span><span class="sxs-lookup"><span data-stu-id="570c8-153">3</span></span> |<span data-ttu-id="570c8-154">1</span><span class="sxs-lookup"><span data-stu-id="570c8-154">1</span></span> |
| <span data-ttu-id="570c8-155">20151001</span><span class="sxs-lookup"><span data-stu-id="570c8-155">20151001</span></span> |<span data-ttu-id="570c8-156">4</span><span class="sxs-lookup"><span data-stu-id="570c8-156">4</span></span> |<span data-ttu-id="570c8-157">2</span><span class="sxs-lookup"><span data-stu-id="570c8-157">2</span></span> |
| <span data-ttu-id="570c8-158">20151101</span><span class="sxs-lookup"><span data-stu-id="570c8-158">20151101</span></span> |<span data-ttu-id="570c8-159">4</span><span class="sxs-lookup"><span data-stu-id="570c8-159">4</span></span> |<span data-ttu-id="570c8-160">2</span><span class="sxs-lookup"><span data-stu-id="570c8-160">2</span></span> |
| <span data-ttu-id="570c8-161">20151201</span><span class="sxs-lookup"><span data-stu-id="570c8-161">20151201</span></span> |<span data-ttu-id="570c8-162">4</span><span class="sxs-lookup"><span data-stu-id="570c8-162">4</span></span> |<span data-ttu-id="570c8-163">2</span><span class="sxs-lookup"><span data-stu-id="570c8-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="570c8-164">4단계: 새로 로드한 데이터에 대한 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="570c8-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="570c8-165">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="570c8-166">쿼리에서 최상의 성능을 얻으려면, 데이터를 처음 로드하거나 데이터에 상당한 변화가 발생한 후에 모든 테이블의 모든 열에서 통계가 만들어지는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="570c8-167">통계에 대한 자세한 설명은 개발 항목 그룹의 [통계][Statistics] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="570c8-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="570c8-168">다음은 이 예제에 로드한 테이블에 대한 통계를 만드는 방법을 간략히 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="570c8-169">sqlcmd 프롬프트에서 다음 CREATE STATISTICS 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="570c8-170">SQL 데이터 웨어하우스에서 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="570c8-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="570c8-171">이 자습서에서는 SQL 데이터 웨어하우스의 테이블에서 데이터 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="570c8-172">위에서 만든 데이터를 DimDate2_export.txt라는 새 데이터 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="570c8-173">1단계: 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="570c8-173">Step 1: Export the data</span></span>
<span data-ttu-id="570c8-174">bcp 유틸리티를 사용하여, 값을 적절하게 대체하는 다음 명령을 사용하여 연결하고 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="570c8-175">새 파일을 열어 데이터를 올바르게 내보냈는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="570c8-176">파일의 데이터는 아래 텍스트와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-176">The data in the file should match the text below:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="570c8-177">분산된 시스템의 특성상 데이터 순서는 SQL 데이터 웨어하우스 데이터베이스에서 동일하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="570c8-178">또 다른 옵션은 전체 테이블을 내보내는 것이 아니라 쿼리 추출을 작성하는 bcp의 **queryout** 함수를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="570c8-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="570c8-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="570c8-179">Next steps</span></span>
<span data-ttu-id="570c8-180">로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="570c8-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="570c8-181">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="570c8-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
