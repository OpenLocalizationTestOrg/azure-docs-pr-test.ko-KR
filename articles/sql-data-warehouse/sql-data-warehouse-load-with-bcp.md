---
title: "SQL 데이터 웨어하우스로 aaaUse bcp tooload 데이터 | Microsoft Docs"
description: "Bcp 무엇 인지 알아보고 방법과 toouse 데이터 웨어하우징 시나리오에 대 한 것입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="8ea6a-103">bcp를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="8ea6a-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ea6a-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="8ea6a-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="8ea6a-105">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="8ea6a-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="8ea6a-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="8ea6a-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="8ea6a-107">BCP</span><span class="sxs-lookup"><span data-stu-id="8ea6a-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="8ea6a-108">**[bcp] [ bcp]**  는 SQL Server, 데이터 파일 및 SQL 데이터 웨어하우스 간에 toocopy 데이터를 허용 하는 명령줄 대량 로드 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="8ea6a-109">Bcp tooimport 많은 수의 행으로 SQL 데이터 웨어하우스 테이블이 나 tooexport 테이블의 데이터를 SQL Server 데이터 파일에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="8ea6a-110">Hello queryout 옵션을 사용 경우를 제외 하 고 bcp TRANSACT-SQL 지식 없이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="8ea6a-111">bcp는 빠르고 쉬운 방법을 toomove 소량의 데이터 집합 및 SQL 데이터 웨어하우스 데이터베이스 외부로입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="8ea6a-112">hello tooload/추출 bcp 통해 권장는 데이터의 정확한 간격에 따라 달라 집니다 연결 toohello Azure 데이터 센터 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="8ea6a-113">일반적으로 차원 테이블은 bcp를 통해 쉽게 로드 및 추출할 수 있으나, 대용량 데이터를 로드 또는 추출할 때는 bcp가 권장되지 않습니다. </span><span class="sxs-lookup"><span data-stu-id="8ea6a-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="8ea6a-114">Polybase는 hello 권장 도구를 로드 하 고 SQL 데이터 웨어하우스의 hello 방대한 병렬 처리 아키텍처를 활용 하 여 작업을 더 효율적으로 많은 양의 데이터를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="8ea6a-115">bcp를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-115">With bcp you can:</span></span>

* <span data-ttu-id="8ea6a-116">SQL 데이터 웨어하우스에서 간단한 명령줄 유틸리티 tooload 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="8ea6a-117">SQL 데이터 웨어하우스에서 간단한 명령줄 유틸리티 tooextract 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="8ea6a-118">이 자습서는 다음에 대한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="8ea6a-119">명령에 hello bcp를 사용 하 여 테이블로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="8ea6a-120">테이블 데 hello bcp 명령 출력에서 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8ea6a-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8ea6a-121">Prerequisites</span></span>
<span data-ttu-id="8ea6a-122">이 자습서를 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="8ea6a-123">SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8ea6a-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="8ea6a-124">hello bcp 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="8ea6a-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="8ea6a-125">hello SQLCMD 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="8ea6a-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="8ea6a-126">Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="8ea6a-127">SQL 데이터 웨어하우스로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="8ea6a-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="8ea6a-128">이 자습서에서는 Azure SQL 데이터 웨어하우스의 테이블을 만들 및 hello 테이블로 데이터를 가져올 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="8ea6a-129">1단계: Azure SQL 데이터 웨어하우스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8ea6a-130">명령 프롬프트에서 sqlcmd toorun hello 쿼리 toocreate 테이블 인스턴스에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="8ea6a-131">참조 [테이블 개요] [ Table Overview] 또는 [CREATE TABLE 구문을] [ CREATE TABLE syntax] SQL 데이터 웨어하우스 및 hello에서 테이블을 만드는 방법에 대 한 자세한 내용은  hello WITH 절에서 사용할 수 있는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="8ea6a-132">2단계: 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="8ea6a-133">새 텍스트 파일에 줄의 데이터로 다음 메모장 및 복사 hello 열고이 파일 tooyour 로컬 임시 디렉터리 C:\Temp\DimDate2.txt를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="8ea6a-134">중요 한 tooremember는 해당 bcp.exe hello u t F-8 파일 인코딩을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="8ea6a-135">bcp.exe 사용 시 파일에 ASCII 파일 또는 UTF-16 인코딩 파일을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="8ea6a-136">3 단계: 연결 및 hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="8ea6a-137">Bcp를 사용 하 여 연결 하 한 다음 적절 하 게 교체 hello 값 명령에는 hello를 사용 하 여 hello 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="8ea6a-138">Hello hello 다음 sqlcmd를 사용 하 여 쿼리를 실행 하 여 로드 된 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="8ea6a-139">Hello 다음 결과 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-139">This should return hello following results:</span></span>

| <span data-ttu-id="8ea6a-140">DateId</span><span class="sxs-lookup"><span data-stu-id="8ea6a-140">DateId</span></span> | <span data-ttu-id="8ea6a-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="8ea6a-141">CalendarQuarter</span></span> | <span data-ttu-id="8ea6a-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="8ea6a-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ea6a-143">20150101</span><span class="sxs-lookup"><span data-stu-id="8ea6a-143">20150101</span></span> |<span data-ttu-id="8ea6a-144">1</span><span class="sxs-lookup"><span data-stu-id="8ea6a-144">1</span></span> |<span data-ttu-id="8ea6a-145">3</span><span class="sxs-lookup"><span data-stu-id="8ea6a-145">3</span></span> |
| <span data-ttu-id="8ea6a-146">20150201</span><span class="sxs-lookup"><span data-stu-id="8ea6a-146">20150201</span></span> |<span data-ttu-id="8ea6a-147">1</span><span class="sxs-lookup"><span data-stu-id="8ea6a-147">1</span></span> |<span data-ttu-id="8ea6a-148">3</span><span class="sxs-lookup"><span data-stu-id="8ea6a-148">3</span></span> |
| <span data-ttu-id="8ea6a-149">20150301</span><span class="sxs-lookup"><span data-stu-id="8ea6a-149">20150301</span></span> |<span data-ttu-id="8ea6a-150">1</span><span class="sxs-lookup"><span data-stu-id="8ea6a-150">1</span></span> |<span data-ttu-id="8ea6a-151">3</span><span class="sxs-lookup"><span data-stu-id="8ea6a-151">3</span></span> |
| <span data-ttu-id="8ea6a-152">20150401</span><span class="sxs-lookup"><span data-stu-id="8ea6a-152">20150401</span></span> |<span data-ttu-id="8ea6a-153">2</span><span class="sxs-lookup"><span data-stu-id="8ea6a-153">2</span></span> |<span data-ttu-id="8ea6a-154">4</span><span class="sxs-lookup"><span data-stu-id="8ea6a-154">4</span></span> |
| <span data-ttu-id="8ea6a-155">20150501</span><span class="sxs-lookup"><span data-stu-id="8ea6a-155">20150501</span></span> |<span data-ttu-id="8ea6a-156">2</span><span class="sxs-lookup"><span data-stu-id="8ea6a-156">2</span></span> |<span data-ttu-id="8ea6a-157">4</span><span class="sxs-lookup"><span data-stu-id="8ea6a-157">4</span></span> |
| <span data-ttu-id="8ea6a-158">20150601</span><span class="sxs-lookup"><span data-stu-id="8ea6a-158">20150601</span></span> |<span data-ttu-id="8ea6a-159">2</span><span class="sxs-lookup"><span data-stu-id="8ea6a-159">2</span></span> |<span data-ttu-id="8ea6a-160">4</span><span class="sxs-lookup"><span data-stu-id="8ea6a-160">4</span></span> |
| <span data-ttu-id="8ea6a-161">20150701</span><span class="sxs-lookup"><span data-stu-id="8ea6a-161">20150701</span></span> |<span data-ttu-id="8ea6a-162">3</span><span class="sxs-lookup"><span data-stu-id="8ea6a-162">3</span></span> |<span data-ttu-id="8ea6a-163">1</span><span class="sxs-lookup"><span data-stu-id="8ea6a-163">1</span></span> |
| <span data-ttu-id="8ea6a-164">20150801</span><span class="sxs-lookup"><span data-stu-id="8ea6a-164">20150801</span></span> |<span data-ttu-id="8ea6a-165">3</span><span class="sxs-lookup"><span data-stu-id="8ea6a-165">3</span></span> |<span data-ttu-id="8ea6a-166">1</span><span class="sxs-lookup"><span data-stu-id="8ea6a-166">1</span></span> |
| <span data-ttu-id="8ea6a-167">20150801</span><span class="sxs-lookup"><span data-stu-id="8ea6a-167">20150801</span></span> |<span data-ttu-id="8ea6a-168">3</span><span class="sxs-lookup"><span data-stu-id="8ea6a-168">3</span></span> |<span data-ttu-id="8ea6a-169">1</span><span class="sxs-lookup"><span data-stu-id="8ea6a-169">1</span></span> |
| <span data-ttu-id="8ea6a-170">20151001</span><span class="sxs-lookup"><span data-stu-id="8ea6a-170">20151001</span></span> |<span data-ttu-id="8ea6a-171">4</span><span class="sxs-lookup"><span data-stu-id="8ea6a-171">4</span></span> |<span data-ttu-id="8ea6a-172">2</span><span class="sxs-lookup"><span data-stu-id="8ea6a-172">2</span></span> |
| <span data-ttu-id="8ea6a-173">20151101</span><span class="sxs-lookup"><span data-stu-id="8ea6a-173">20151101</span></span> |<span data-ttu-id="8ea6a-174">4</span><span class="sxs-lookup"><span data-stu-id="8ea6a-174">4</span></span> |<span data-ttu-id="8ea6a-175">2</span><span class="sxs-lookup"><span data-stu-id="8ea6a-175">2</span></span> |
| <span data-ttu-id="8ea6a-176">20151201</span><span class="sxs-lookup"><span data-stu-id="8ea6a-176">20151201</span></span> |<span data-ttu-id="8ea6a-177">4</span><span class="sxs-lookup"><span data-stu-id="8ea6a-177">4</span></span> |<span data-ttu-id="8ea6a-178">2</span><span class="sxs-lookup"><span data-stu-id="8ea6a-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="8ea6a-179">4단계: 새로 로드한 데이터에 대한 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="8ea6a-180">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="8ea6a-181">순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 통계 hello 첫 번째 로드 한 후 모든 테이블의 모든 열에 만들 수 또는 hello 데이터에서 발생 된 모든 주요 부분을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="8ea6a-182">통계에 대 한 자세한 내용은 참조 hello [통계] [ Statistics] hello 개발 그룹 항목의 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="8ea6a-183">다음은이 예에서 테이블 hello에 대 한 toocreate 통계 로드 하는 방법의 간단한 예</span><span class="sxs-lookup"><span data-stu-id="8ea6a-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="8ea6a-184">Hello CREATE STATISTICS 문을 sqlcmd 프롬프트에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="8ea6a-185">SQL 데이터 웨어하우스에서 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="8ea6a-186">이 자습서에서는 SQL 데이터 웨어하우스의 테이블에서 데이터 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="8ea6a-187">Tooa 새로운 데이터 파일 DimDate2_export.txt 라는 위에서 만든 hello 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="8ea6a-188">1 단계: hello 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="8ea6a-188">Step 1: Export hello data</span></span>
<span data-ttu-id="8ea6a-189">Hello bcp 유틸리티를 사용 하 여 연결을 다음 적절 하 게 교체 hello 값 명령에는 hello를 사용 하 여 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="8ea6a-190">Hello 새 파일을 열어 데이터 올바르게 내보낸 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="8ea6a-191">hello 파일의에서 데이터를 hello 아래 hello 텍스트를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="8ea6a-192">분산된 시스템에서는 toohello 이기 때문 hello 데이터 순서가 않을 SQL 데이터 웨어하우스 데이터베이스에 걸쳐 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="8ea6a-193">두 번째 방법은 toouse hello **queryout** bcp toowrite 쿼리의 추출 대신 함수 hello 전체 테이블을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8ea6a-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ea6a-194">Next steps</span></span>
<span data-ttu-id="8ea6a-195">로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="8ea6a-196">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ea6a-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
