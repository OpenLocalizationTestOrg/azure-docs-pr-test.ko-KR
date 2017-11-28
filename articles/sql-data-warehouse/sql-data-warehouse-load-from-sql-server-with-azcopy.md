---
title: "Azure SQL 데이터 웨어하우스 (PolyBase)에 SQL Server에서 aaaLoad 데이터 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에 SQL Server tooflat 파일, AZCopy tooimport 데이터 tooAzure blob 저장소 및 PolyBase tooingest hello 데이터에서 bcp tooexport 데이터를 사용합니다."
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
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="582f3-103">SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(AZCopy)</span><span class="sxs-lookup"><span data-stu-id="582f3-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="582f3-104">Bcp 및 SQL Server tooAzure blob 저장소에서 AZCopy 명령줄 유틸리티 tooload 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="582f3-105">그런 다음 Azure SQL 데이터 웨어하우스로 PolyBase 또는 Azure Data Factory tooload hello 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="582f3-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="582f3-106">Prerequisites</span></span>
<span data-ttu-id="582f3-107">이 자습서를 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="582f3-108">SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="582f3-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="582f3-109">hello bcp 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="582f3-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="582f3-110">hello SQLCMD 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="582f3-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="582f3-111">Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="582f3-112">SQL 데이터 웨어하우스로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="582f3-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="582f3-113">이 자습서에서는 Azure SQL 데이터 웨어하우스의 테이블을 만들 및 hello 테이블로 데이터를 가져올 됩니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="582f3-114">1단계: Azure SQL 데이터 웨어하우스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="582f3-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="582f3-115">명령 프롬프트에서 sqlcmd toorun hello 쿼리 toocreate 테이블 인스턴스에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="582f3-116">참조 [테이블 개요] [ Table Overview] 또는 [CREATE TABLE 구문을] [ CREATE TABLE syntax] SQL 데이터 웨어하우스 및 hello에서 테이블을 만드는 방법에 대 한 자세한 내용은  hello WITH 절에서 사용할 수 있는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="582f3-117">2단계: 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="582f3-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="582f3-118">새 텍스트 파일에 줄의 데이터로 다음 메모장 및 복사 hello 열고이 파일 tooyour 로컬 임시 디렉터리 C:\Temp\DimDate2.txt를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="582f3-119">중요 한 tooremember는 해당 bcp.exe hello u t F-8 파일 인코딩을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="582f3-120">bcp.exe 사용 시 파일에 ASCII 파일 또는 UTF-16 인코딩 파일을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="582f3-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="582f3-121">3 단계: 연결 및 hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="582f3-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="582f3-122">Bcp를 사용 하 여 연결 하 한 다음 적절 하 게 교체 hello 값 명령에는 hello를 사용 하 여 hello 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="582f3-123">Hello hello 다음 sqlcmd를 사용 하 여 쿼리를 실행 하 여 로드 된 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="582f3-124">Hello 다음 결과 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-124">This should return hello following results:</span></span>

| <span data-ttu-id="582f3-125">DateId</span><span class="sxs-lookup"><span data-stu-id="582f3-125">DateId</span></span> | <span data-ttu-id="582f3-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="582f3-126">CalendarQuarter</span></span> | <span data-ttu-id="582f3-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="582f3-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="582f3-128">20150101</span><span class="sxs-lookup"><span data-stu-id="582f3-128">20150101</span></span> |<span data-ttu-id="582f3-129">1</span><span class="sxs-lookup"><span data-stu-id="582f3-129">1</span></span> |<span data-ttu-id="582f3-130">3</span><span class="sxs-lookup"><span data-stu-id="582f3-130">3</span></span> |
| <span data-ttu-id="582f3-131">20150201</span><span class="sxs-lookup"><span data-stu-id="582f3-131">20150201</span></span> |<span data-ttu-id="582f3-132">1</span><span class="sxs-lookup"><span data-stu-id="582f3-132">1</span></span> |<span data-ttu-id="582f3-133">3</span><span class="sxs-lookup"><span data-stu-id="582f3-133">3</span></span> |
| <span data-ttu-id="582f3-134">20150301</span><span class="sxs-lookup"><span data-stu-id="582f3-134">20150301</span></span> |<span data-ttu-id="582f3-135">1</span><span class="sxs-lookup"><span data-stu-id="582f3-135">1</span></span> |<span data-ttu-id="582f3-136">3</span><span class="sxs-lookup"><span data-stu-id="582f3-136">3</span></span> |
| <span data-ttu-id="582f3-137">20150401</span><span class="sxs-lookup"><span data-stu-id="582f3-137">20150401</span></span> |<span data-ttu-id="582f3-138">2</span><span class="sxs-lookup"><span data-stu-id="582f3-138">2</span></span> |<span data-ttu-id="582f3-139">4</span><span class="sxs-lookup"><span data-stu-id="582f3-139">4</span></span> |
| <span data-ttu-id="582f3-140">20150501</span><span class="sxs-lookup"><span data-stu-id="582f3-140">20150501</span></span> |<span data-ttu-id="582f3-141">2</span><span class="sxs-lookup"><span data-stu-id="582f3-141">2</span></span> |<span data-ttu-id="582f3-142">4</span><span class="sxs-lookup"><span data-stu-id="582f3-142">4</span></span> |
| <span data-ttu-id="582f3-143">20150601</span><span class="sxs-lookup"><span data-stu-id="582f3-143">20150601</span></span> |<span data-ttu-id="582f3-144">2</span><span class="sxs-lookup"><span data-stu-id="582f3-144">2</span></span> |<span data-ttu-id="582f3-145">4</span><span class="sxs-lookup"><span data-stu-id="582f3-145">4</span></span> |
| <span data-ttu-id="582f3-146">20150701</span><span class="sxs-lookup"><span data-stu-id="582f3-146">20150701</span></span> |<span data-ttu-id="582f3-147">3</span><span class="sxs-lookup"><span data-stu-id="582f3-147">3</span></span> |<span data-ttu-id="582f3-148">1</span><span class="sxs-lookup"><span data-stu-id="582f3-148">1</span></span> |
| <span data-ttu-id="582f3-149">20150801</span><span class="sxs-lookup"><span data-stu-id="582f3-149">20150801</span></span> |<span data-ttu-id="582f3-150">3</span><span class="sxs-lookup"><span data-stu-id="582f3-150">3</span></span> |<span data-ttu-id="582f3-151">1</span><span class="sxs-lookup"><span data-stu-id="582f3-151">1</span></span> |
| <span data-ttu-id="582f3-152">20150801</span><span class="sxs-lookup"><span data-stu-id="582f3-152">20150801</span></span> |<span data-ttu-id="582f3-153">3</span><span class="sxs-lookup"><span data-stu-id="582f3-153">3</span></span> |<span data-ttu-id="582f3-154">1</span><span class="sxs-lookup"><span data-stu-id="582f3-154">1</span></span> |
| <span data-ttu-id="582f3-155">20151001</span><span class="sxs-lookup"><span data-stu-id="582f3-155">20151001</span></span> |<span data-ttu-id="582f3-156">4</span><span class="sxs-lookup"><span data-stu-id="582f3-156">4</span></span> |<span data-ttu-id="582f3-157">2</span><span class="sxs-lookup"><span data-stu-id="582f3-157">2</span></span> |
| <span data-ttu-id="582f3-158">20151101</span><span class="sxs-lookup"><span data-stu-id="582f3-158">20151101</span></span> |<span data-ttu-id="582f3-159">4</span><span class="sxs-lookup"><span data-stu-id="582f3-159">4</span></span> |<span data-ttu-id="582f3-160">2</span><span class="sxs-lookup"><span data-stu-id="582f3-160">2</span></span> |
| <span data-ttu-id="582f3-161">20151201</span><span class="sxs-lookup"><span data-stu-id="582f3-161">20151201</span></span> |<span data-ttu-id="582f3-162">4</span><span class="sxs-lookup"><span data-stu-id="582f3-162">4</span></span> |<span data-ttu-id="582f3-163">2</span><span class="sxs-lookup"><span data-stu-id="582f3-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="582f3-164">4단계: 새로 로드한 데이터에 대한 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="582f3-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="582f3-165">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="582f3-166">순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 통계 hello 첫 번째 로드 한 후 모든 테이블의 모든 열에 만들 수 또는 hello 데이터에서 발생 된 모든 주요 부분을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="582f3-167">통계에 대 한 자세한 내용은 참조 hello [통계] [ Statistics] hello 개발 그룹 항목의 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="582f3-168">다음은이 예에서 테이블 hello에 대 한 toocreate 통계 로드 하는 방법의 간단한 예</span><span class="sxs-lookup"><span data-stu-id="582f3-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="582f3-169">Hello CREATE STATISTICS 문을 sqlcmd 프롬프트에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="582f3-170">SQL 데이터 웨어하우스에서 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="582f3-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="582f3-171">이 자습서에서는 SQL 데이터 웨어하우스의 테이블에서 데이터 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="582f3-172">Tooa 새로운 데이터 파일 DimDate2_export.txt 라는 위에서 만든 hello 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="582f3-173">1 단계: hello 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="582f3-173">Step 1: Export hello data</span></span>
<span data-ttu-id="582f3-174">Hello bcp 유틸리티를 사용 하 여 연결을 다음 적절 하 게 교체 hello 값 명령에는 hello를 사용 하 여 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="582f3-175">Hello 새 파일을 열어 데이터 올바르게 내보낸 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="582f3-176">hello 파일의에서 데이터를 hello 아래 hello 텍스트를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="582f3-177">분산된 시스템에서는 toohello 이기 때문 hello 데이터 순서가 않을 SQL 데이터 웨어하우스 데이터베이스에 걸쳐 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="582f3-178">두 번째 방법은 toouse hello **queryout** bcp toowrite 쿼리의 추출 대신 함수 hello 전체 테이블을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="582f3-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="582f3-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="582f3-179">Next steps</span></span>
<span data-ttu-id="582f3-180">로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="582f3-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="582f3-181">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="582f3-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
