---
title: "Azure SQL 데이터 웨어하우스 (bcp)에 SQL Server에서 aaaLoad 데이터 | Microsoft Docs"
description: "작은 데이터 크기에 대 한 Azure SQL 데이터 웨어하우스에 직접 hello 데이터 가져오기 및 SQL Server tooflat 파일에서 bcp tooexport 데이터를 사용 합니다."
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
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="29573-103">SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(플랫 파일)</span><span class="sxs-lookup"><span data-stu-id="29573-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29573-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="29573-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="29573-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="29573-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="29573-106">bcp</span><span class="sxs-lookup"><span data-stu-id="29573-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="29573-107">작은 데이터 집합에 대 한 hello bcp 명령줄 유틸리티 tooexport 데이터 SQL Server를 사용 하 고 tooAzure SQL 데이터 웨어하우스 직접 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="29573-108">이 자습서에서는 bcp를 사용하여:</span><span class="sxs-lookup"><span data-stu-id="29573-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="29573-109">테이블에서 SQL Server에서에서 내보냅니다 hello bcp 명령을 사용 하 여 (또는 간단한 샘플 파일 만들기)</span><span class="sxs-lookup"><span data-stu-id="29573-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="29573-110">플랫 파일 tooSQL 데이터 웨어하우스에서에서 hello 테이블을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="29573-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="29573-111">Hello 로드 된 데이터에 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29573-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="29573-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="29573-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="29573-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="29573-113">Prerequisites</span></span>
<span data-ttu-id="29573-114">이 자습서를 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="29573-115">SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="29573-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="29573-116">hello bcp 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="29573-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="29573-117">hello sqlcmd 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="29573-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="29573-118">Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="29573-119">ASCII 또는 UTF-16 형식 데이터</span><span class="sxs-lookup"><span data-stu-id="29573-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="29573-120">이 자습서에서는 사용자 고유의 데이터로 시도 하는 경우 데이터 toouse hello ASCII 또는 utf-16 인코딩 bcp u t F-8을 지원 하지 않으므로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="29573-121">PolyBase는 UTF-8을 지원하지만 아직 UTF-16은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="29573-122">Polybase toocombine bcp 하려는 경우 시켜야 하 tootransform hello 데이터 tooUTF 8 SQL Server에서 내보낸 후 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="29573-123">1. 대상 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="29573-123">1. Create a destination table</span></span>
<span data-ttu-id="29573-124">SQL 데이터 웨어하우스에 hello 부하에 대 한 대상 테이블 hello 될 테이블을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="29573-125">hello 테이블의 hello 열에는 데이터 파일의 각 행에 toohello 데이터 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="29573-126">toocreate 테이블을 명령 프롬프트를 열고 sqlcmd.exe toorun hello 다음 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="29573-127">2. 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="29573-127">2. Create a source data file</span></span>
<span data-ttu-id="29573-128">새 텍스트 파일에 줄의 데이터로 다음 메모장 및 복사 hello 열고이 파일 tooyour 로컬 임시 디렉터리 C:\Temp\DimDate2.txt를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="29573-129">이 데이터는 ASCII 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="29573-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="29573-130">(선택 사항) tooexport SQL Server 데이터베이스에서 사용자 고유의 데이터는 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="29573-131">TableName, ServerName, DatabaseName, Username 및 Password를 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="29573-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="29573-132">3. Hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="29573-132">3. Load hello data</span></span>
<span data-ttu-id="29573-133">tooload hello 데이터 명령 프롬프트를 열고 다음 명령을, hello 값을 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호에 대 한 사용자의 정보로 대체 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="29573-134">이 명령은 tooverify hello 데이터가 제대로 로드 사용</span><span class="sxs-lookup"><span data-stu-id="29573-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="29573-135">hello 결과 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29573-135">hello results should look like this:</span></span>

| <span data-ttu-id="29573-136">DateId</span><span class="sxs-lookup"><span data-stu-id="29573-136">DateId</span></span> | <span data-ttu-id="29573-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="29573-137">CalendarQuarter</span></span> | <span data-ttu-id="29573-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="29573-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29573-139">20150101</span><span class="sxs-lookup"><span data-stu-id="29573-139">20150101</span></span> |<span data-ttu-id="29573-140">1</span><span class="sxs-lookup"><span data-stu-id="29573-140">1</span></span> |<span data-ttu-id="29573-141">3</span><span class="sxs-lookup"><span data-stu-id="29573-141">3</span></span> |
| <span data-ttu-id="29573-142">20150201</span><span class="sxs-lookup"><span data-stu-id="29573-142">20150201</span></span> |<span data-ttu-id="29573-143">1</span><span class="sxs-lookup"><span data-stu-id="29573-143">1</span></span> |<span data-ttu-id="29573-144">3</span><span class="sxs-lookup"><span data-stu-id="29573-144">3</span></span> |
| <span data-ttu-id="29573-145">20150301</span><span class="sxs-lookup"><span data-stu-id="29573-145">20150301</span></span> |<span data-ttu-id="29573-146">1</span><span class="sxs-lookup"><span data-stu-id="29573-146">1</span></span> |<span data-ttu-id="29573-147">3</span><span class="sxs-lookup"><span data-stu-id="29573-147">3</span></span> |
| <span data-ttu-id="29573-148">20150401</span><span class="sxs-lookup"><span data-stu-id="29573-148">20150401</span></span> |<span data-ttu-id="29573-149">2</span><span class="sxs-lookup"><span data-stu-id="29573-149">2</span></span> |<span data-ttu-id="29573-150">4</span><span class="sxs-lookup"><span data-stu-id="29573-150">4</span></span> |
| <span data-ttu-id="29573-151">20150501</span><span class="sxs-lookup"><span data-stu-id="29573-151">20150501</span></span> |<span data-ttu-id="29573-152">2</span><span class="sxs-lookup"><span data-stu-id="29573-152">2</span></span> |<span data-ttu-id="29573-153">4</span><span class="sxs-lookup"><span data-stu-id="29573-153">4</span></span> |
| <span data-ttu-id="29573-154">20150601</span><span class="sxs-lookup"><span data-stu-id="29573-154">20150601</span></span> |<span data-ttu-id="29573-155">2</span><span class="sxs-lookup"><span data-stu-id="29573-155">2</span></span> |<span data-ttu-id="29573-156">4</span><span class="sxs-lookup"><span data-stu-id="29573-156">4</span></span> |
| <span data-ttu-id="29573-157">20150701</span><span class="sxs-lookup"><span data-stu-id="29573-157">20150701</span></span> |<span data-ttu-id="29573-158">3</span><span class="sxs-lookup"><span data-stu-id="29573-158">3</span></span> |<span data-ttu-id="29573-159">1</span><span class="sxs-lookup"><span data-stu-id="29573-159">1</span></span> |
| <span data-ttu-id="29573-160">20150801</span><span class="sxs-lookup"><span data-stu-id="29573-160">20150801</span></span> |<span data-ttu-id="29573-161">3</span><span class="sxs-lookup"><span data-stu-id="29573-161">3</span></span> |<span data-ttu-id="29573-162">1</span><span class="sxs-lookup"><span data-stu-id="29573-162">1</span></span> |
| <span data-ttu-id="29573-163">20150801</span><span class="sxs-lookup"><span data-stu-id="29573-163">20150801</span></span> |<span data-ttu-id="29573-164">3</span><span class="sxs-lookup"><span data-stu-id="29573-164">3</span></span> |<span data-ttu-id="29573-165">1</span><span class="sxs-lookup"><span data-stu-id="29573-165">1</span></span> |
| <span data-ttu-id="29573-166">20151001</span><span class="sxs-lookup"><span data-stu-id="29573-166">20151001</span></span> |<span data-ttu-id="29573-167">4</span><span class="sxs-lookup"><span data-stu-id="29573-167">4</span></span> |<span data-ttu-id="29573-168">2</span><span class="sxs-lookup"><span data-stu-id="29573-168">2</span></span> |
| <span data-ttu-id="29573-169">20151101</span><span class="sxs-lookup"><span data-stu-id="29573-169">20151101</span></span> |<span data-ttu-id="29573-170">4</span><span class="sxs-lookup"><span data-stu-id="29573-170">4</span></span> |<span data-ttu-id="29573-171">2</span><span class="sxs-lookup"><span data-stu-id="29573-171">2</span></span> |
| <span data-ttu-id="29573-172">20151201</span><span class="sxs-lookup"><span data-stu-id="29573-172">20151201</span></span> |<span data-ttu-id="29573-173">4</span><span class="sxs-lookup"><span data-stu-id="29573-173">4</span></span> |<span data-ttu-id="29573-174">2</span><span class="sxs-lookup"><span data-stu-id="29573-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="29573-175">4. 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="29573-175">4. Create statistics</span></span>
<span data-ttu-id="29573-176">SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="29573-177">tooget hello 최고의 쿼리 성능을 인지 모든 테이블의 모든 열에 대 한 중요 한 toocreate 통계 hello 첫 번째 로드 한 후 모든 변경이 hello 데이터에서 발생 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="29573-178">통계에 대한 자세한 설명은 [통계][Statistics]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29573-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="29573-179">Hello 명령 toocreate 통계에 새로 로드 된 테이블에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="29573-180">5. SQL 데이터 웨어하우스에서 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="29573-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="29573-181">쉽도록 SQL 데이터 웨어하우스 밖으로 다시 로드 된 hello 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="29573-182">hello 명령 tooexport은 SQL Server에서 내보내기 동일 hello 정확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="29573-183">그러나 hello 결과에 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="29573-184">Hello 데이터는 데이터를 내보낼 때 SQL 데이터 웨어하우스 내에서 분산 된 위치에 저장 되므로 각 계산 노드가 데이터 toohello 출력 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="29573-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="29573-185">hello hello 출력 파일에는 데이터의 hello 순서가 가능성이 toobe hello hello 입력된 파일에는 데이터의 hello 순서와 다른 경우</span><span class="sxs-lookup"><span data-stu-id="29573-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="29573-186">테이블을 내보내고 내보낸 결과 비교</span><span class="sxs-lookup"><span data-stu-id="29573-186">Export a table and compare exported results</span></span>
<span data-ttu-id="29573-187">toosee hello 내보낸된 데이터를 명령 프롬프트를 열고 고유한 매개 변수를 사용 하 여이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29573-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="29573-188">서버 이름에는 논리 SQL Server에 Azure의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="29573-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="29573-189">Hello 새 파일을 열어 데이터 올바르게 내보낸 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="29573-190">hello 파일의에서 데이터를 hello 아래의 hello 텍스트와 일치 해야 하지만 다른 순서로 정렬 될 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="29573-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="29573-191">쿼리의 hello 결과 내보내기</span><span class="sxs-lookup"><span data-stu-id="29573-191">Export hello results of a query</span></span>
<span data-ttu-id="29573-192">Hello를 사용할 수 있습니다 **queryout** bcp tooexport hello 쿼리 결과를 내보내는 hello 전체 테이블 대신의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="29573-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="29573-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29573-193">Next steps</span></span>
<span data-ttu-id="29573-194">로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29573-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="29573-195">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29573-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="29573-196">SQL Data Warehouse에 테이블을 만드는 방법에 대한 내용은 [테이블 개요][Table Overview] 또는 [CREATE TABLE 구문][CREATE TABLE syntax]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29573-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
