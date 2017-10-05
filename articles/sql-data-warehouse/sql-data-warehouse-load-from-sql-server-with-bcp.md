---
title: "SQL Server에서 Azure SQL Data Warehouse로 데이터 로드(bcp) | Microsoft Docs"
description: "데이터의 크기가 작으면, bcp를 사용하여 SQL Server의 데이터를 플랫 파일로 내보내고 Azure SQL 데이터 웨어하우스로 데이터를 직접 가져옵니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: dae7b5f7456f4ec0daf60d55f9c38b780896ff83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="1d302-103">SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(플랫 파일)</span><span class="sxs-lookup"><span data-stu-id="1d302-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d302-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="1d302-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="1d302-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1d302-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="1d302-106">bcp</span><span class="sxs-lookup"><span data-stu-id="1d302-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="1d302-107">소규모 데이터 집합의 경우, bcp 명령줄 유틸리티를 사용하여 SQL Server에서 데이터를 내보낸 다음 Azure SQL 데이터 웨어하우스로 데이터를 직접 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="1d302-108">이 자습서에서는 bcp를 사용하여:</span><span class="sxs-lookup"><span data-stu-id="1d302-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="1d302-109">bcp out 명령을 사용하여 SQL Server의 테이블을 내보냅니다.(또는 간단한 샘플 파일을 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="1d302-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="1d302-110">플랫 파일의 테이블을 SQL 데이터 웨어하우스로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="1d302-111">로드한 데이터에 대한 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="1d302-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1d302-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="1d302-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1d302-113">Prerequisites</span></span>
<span data-ttu-id="1d302-114">이 자습서를 단계별로 실행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="1d302-115">SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="1d302-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="1d302-116">설치된 bcp 명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="1d302-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="1d302-117">설치된 sqlcmd 명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="1d302-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="1d302-118">[Microsoft 다운로드 센터][Microsoft Download Center]에서 bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="1d302-119">ASCII 또는 UTF-16 형식 데이터</span><span class="sxs-lookup"><span data-stu-id="1d302-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="1d302-120">사용자의 데이터로 이 자습서를 수행하는 경우에는, bcp가 UTF-8을 지원하지 않으므로, 데이터에 ASCII 또는 UTF-16 인코딩을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="1d302-121">PolyBase는 UTF-8을 지원하지만 아직 UTF-16은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="1d302-122">bcp를 PolyBase와 결합하려면 데이터를 SQL Server에서 내보낸 후 UTF-8로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="1d302-123">1. 대상 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1d302-123">1. Create a destination table</span></span>
<span data-ttu-id="1d302-124">SQL 데이터 웨어하우스에 로드에 대한 대상 테이블이 될 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="1d302-125">테이블의 열은 데이터 파일의 각 행에 있는 데이터와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="1d302-126">테이블을 만들려면, 명령 프롬프트를 열고 sqlcmd.exe를 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="1d302-127">2. 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1d302-127">2. Create a source data file</span></span>
<span data-ttu-id="1d302-128">메모장을 열고 다음 데이터 줄을 새 텍스트 파일에 복사한 다음 이 파일을 로컬 임시 디렉터리 C:\Temp\DimDate2.txt에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="1d302-129">이 데이터는 ASCII 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="1d302-130">(선택 사항) SQL Server 데이터베이스에서 사용자의 데이터를 내보내려면, 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="1d302-131">TableName, ServerName, DatabaseName, Username 및 Password를 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="1d302-132">3. 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="1d302-132">3. Load the data</span></span>
<span data-ttu-id="1d302-133">데이터를 로드하려면, 명령 프롬프트를 열고 Server Name, Database name, Username 및 Password 값을 사용자의 정보로 바꿔서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="1d302-134">이 명령을 사용하여 데이터가 제대로 로드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="1d302-135">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-135">The results should look like this:</span></span>

| <span data-ttu-id="1d302-136">DateId</span><span class="sxs-lookup"><span data-stu-id="1d302-136">DateId</span></span> | <span data-ttu-id="1d302-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="1d302-137">CalendarQuarter</span></span> | <span data-ttu-id="1d302-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="1d302-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1d302-139">20150101</span><span class="sxs-lookup"><span data-stu-id="1d302-139">20150101</span></span> |<span data-ttu-id="1d302-140">1</span><span class="sxs-lookup"><span data-stu-id="1d302-140">1</span></span> |<span data-ttu-id="1d302-141">3</span><span class="sxs-lookup"><span data-stu-id="1d302-141">3</span></span> |
| <span data-ttu-id="1d302-142">20150201</span><span class="sxs-lookup"><span data-stu-id="1d302-142">20150201</span></span> |<span data-ttu-id="1d302-143">1</span><span class="sxs-lookup"><span data-stu-id="1d302-143">1</span></span> |<span data-ttu-id="1d302-144">3</span><span class="sxs-lookup"><span data-stu-id="1d302-144">3</span></span> |
| <span data-ttu-id="1d302-145">20150301</span><span class="sxs-lookup"><span data-stu-id="1d302-145">20150301</span></span> |<span data-ttu-id="1d302-146">1</span><span class="sxs-lookup"><span data-stu-id="1d302-146">1</span></span> |<span data-ttu-id="1d302-147">3</span><span class="sxs-lookup"><span data-stu-id="1d302-147">3</span></span> |
| <span data-ttu-id="1d302-148">20150401</span><span class="sxs-lookup"><span data-stu-id="1d302-148">20150401</span></span> |<span data-ttu-id="1d302-149">2</span><span class="sxs-lookup"><span data-stu-id="1d302-149">2</span></span> |<span data-ttu-id="1d302-150">4</span><span class="sxs-lookup"><span data-stu-id="1d302-150">4</span></span> |
| <span data-ttu-id="1d302-151">20150501</span><span class="sxs-lookup"><span data-stu-id="1d302-151">20150501</span></span> |<span data-ttu-id="1d302-152">2</span><span class="sxs-lookup"><span data-stu-id="1d302-152">2</span></span> |<span data-ttu-id="1d302-153">4</span><span class="sxs-lookup"><span data-stu-id="1d302-153">4</span></span> |
| <span data-ttu-id="1d302-154">20150601</span><span class="sxs-lookup"><span data-stu-id="1d302-154">20150601</span></span> |<span data-ttu-id="1d302-155">2</span><span class="sxs-lookup"><span data-stu-id="1d302-155">2</span></span> |<span data-ttu-id="1d302-156">4</span><span class="sxs-lookup"><span data-stu-id="1d302-156">4</span></span> |
| <span data-ttu-id="1d302-157">20150701</span><span class="sxs-lookup"><span data-stu-id="1d302-157">20150701</span></span> |<span data-ttu-id="1d302-158">3</span><span class="sxs-lookup"><span data-stu-id="1d302-158">3</span></span> |<span data-ttu-id="1d302-159">1</span><span class="sxs-lookup"><span data-stu-id="1d302-159">1</span></span> |
| <span data-ttu-id="1d302-160">20150801</span><span class="sxs-lookup"><span data-stu-id="1d302-160">20150801</span></span> |<span data-ttu-id="1d302-161">3</span><span class="sxs-lookup"><span data-stu-id="1d302-161">3</span></span> |<span data-ttu-id="1d302-162">1</span><span class="sxs-lookup"><span data-stu-id="1d302-162">1</span></span> |
| <span data-ttu-id="1d302-163">20150801</span><span class="sxs-lookup"><span data-stu-id="1d302-163">20150801</span></span> |<span data-ttu-id="1d302-164">3</span><span class="sxs-lookup"><span data-stu-id="1d302-164">3</span></span> |<span data-ttu-id="1d302-165">1</span><span class="sxs-lookup"><span data-stu-id="1d302-165">1</span></span> |
| <span data-ttu-id="1d302-166">20151001</span><span class="sxs-lookup"><span data-stu-id="1d302-166">20151001</span></span> |<span data-ttu-id="1d302-167">4</span><span class="sxs-lookup"><span data-stu-id="1d302-167">4</span></span> |<span data-ttu-id="1d302-168">2</span><span class="sxs-lookup"><span data-stu-id="1d302-168">2</span></span> |
| <span data-ttu-id="1d302-169">20151101</span><span class="sxs-lookup"><span data-stu-id="1d302-169">20151101</span></span> |<span data-ttu-id="1d302-170">4</span><span class="sxs-lookup"><span data-stu-id="1d302-170">4</span></span> |<span data-ttu-id="1d302-171">2</span><span class="sxs-lookup"><span data-stu-id="1d302-171">2</span></span> |
| <span data-ttu-id="1d302-172">20151201</span><span class="sxs-lookup"><span data-stu-id="1d302-172">20151201</span></span> |<span data-ttu-id="1d302-173">4</span><span class="sxs-lookup"><span data-stu-id="1d302-173">4</span></span> |<span data-ttu-id="1d302-174">2</span><span class="sxs-lookup"><span data-stu-id="1d302-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="1d302-175">4. 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="1d302-175">4. Create statistics</span></span>
<span data-ttu-id="1d302-176">SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="1d302-177">최고의 쿼리 성능을 얻으려면, 데이터를 처음 로드하거나 데이터 내에 상당한 변화가 생긴 후에, 모든 테이블의 모든 열에서 통계를 만드는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="1d302-178">통계에 대한 자세한 설명은 [통계][Statistics]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d302-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="1d302-179">다음 명령을 실행하여 새로 로드한 테이블에 대한 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="1d302-180">5. SQL 데이터 웨어하우스에서 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="1d302-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="1d302-181">재미를 위해 방금 SQL 데이터 웨어하우스에서 로드한 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="1d302-182">내보내는 명령은 SQL Server에서 내보내는 것과 똑같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="1d302-183">하지만, 결과에는 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-183">However, there is a difference in the results.</span></span> <span data-ttu-id="1d302-184">데이터가 SQL 데이터 웨어하우스 내의 분산된 위치에 저장되기 때문에, 데이터를 내보내면 각 계산 노드는 데이터를 출력 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="1d302-185">출력 파일에 포함된 데이터 순서는 입력 파일의 데이터 순서와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="1d302-186">테이블을 내보내고 내보낸 결과 비교</span><span class="sxs-lookup"><span data-stu-id="1d302-186">Export a table and compare exported results</span></span>
<span data-ttu-id="1d302-187">내보낸 데이터를 보려면, 명령 프롬프트를 열고 사용자의 매개 변수를 사용하여 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="1d302-188">ServerName은 Azure 논리적 SQL Server의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="1d302-189">새 파일을 열어 데이터를 올바르게 내보냈는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="1d302-190">파일에 포함된 데이터는 아래 텍스트와 일치해야 하지만, 다른 순서로 정렬되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="1d302-191">쿼리 결과 내보내기</span><span class="sxs-lookup"><span data-stu-id="1d302-191">Export the results of a query</span></span>
<span data-ttu-id="1d302-192">bcp의 **queryout** 함수를 사용하면 전체 테이블을 내보내는 대신 쿼리 결과를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d302-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1d302-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d302-193">Next steps</span></span>
<span data-ttu-id="1d302-194">로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d302-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="1d302-195">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d302-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="1d302-196">SQL Data Warehouse에 테이블을 만드는 방법에 대한 내용은 [테이블 개요][Table Overview] 또는 [CREATE TABLE 구문][CREATE TABLE syntax]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d302-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
