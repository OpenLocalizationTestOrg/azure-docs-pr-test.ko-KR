---
title: "Azure VM에서 SQL Server로 데이터를 빠르게 병렬로 가져오기 위한 테이블 빌드 및 최적화 | Microsoft Docs"
description: "SQL 파티션 테이블을 사용하여 대량의 데이터를 병렬로 가져오기"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: aae4e4f59e76bf48b00a2ee92aedd7d5643ba91a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="dc945-103">SQL 파티션 테이블을 사용하여 대량의 데이터를 병렬로 가져오기</span><span class="sxs-lookup"><span data-stu-id="dc945-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="dc945-104">이 문서에서는 분할된 테이블을 만들어서 SQL Server 데이터베이스로 대량의 데이터를 병렬로 더 빨리 가져오는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span></span> <span data-ttu-id="dc945-105">SQL Database로 빅 데이터를 로드/전송할 때 *분할된 테이블 및 뷰*를 사용하여 SQL DB로 데이터를 가져오는 작업과 후속 쿼리의 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="dc945-106">새 데이터베이스 및 파일 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="dc945-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="dc945-107">아직 존재하지 않으면 [새 데이터베이스를 만듭니다](https://technet.microsoft.com/library/ms176061.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc945-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="dc945-108">분할된 실제 파일을 보유할 데이터베이스에 데이터베이스 파일 그룹을 추가합니다. 이렇게 하려면 데이터베이스가 존재하지 않는 경우 [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx)를 사용하거나 이미 있는 경우 [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx)를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-108">Add database filegroups to the database which will hold the partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span></span>
* <span data-ttu-id="dc945-109">필요한 경우 각 데이터베이스 파일 그룹에 파일을 하나 이상 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-109">Add one or more files (as needed) to each database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="dc945-110">이 파티션의 데이터를 보유할 대상 파일 그룹과 파일 그룹 데이터가 저장될 실제 데이터베이스 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-110">Specify the target filegroup which holds data for this partition and the physical database file name(s) where the filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="dc945-111">다음은 기본 그룹 및 로그 그룹이 아닌 3개의 파일 그룹이 있고 각 파일 그룹에 물리적 파일 1개가 포함되는 새 데이터베이스를 만드는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-111">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="dc945-112">SQL Server 인스턴스에 구성된 것처럼 데이터베이스 파일은 기본 SQL Server 데이터 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-112">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span></span> <span data-ttu-id="dc945-113">기본 파일 위치에 대한 자세한 내용은 [SQL Server의 기본 인스턴스 및 명명된 인스턴스의 파일 위치](https://msdn.microsoft.com/library/ms143547.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc945-113">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="dc945-114">분할된 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="dc945-114">Create a partitioned table</span></span>
<span data-ttu-id="dc945-115">이전 단계에서 만든 데이터베이스 파일 그룹에 매핑된 데이터 스키마에 따라 분할된 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-115">Create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step.</span></span> <span data-ttu-id="dc945-116">분할된 테이블로 데이터를 대량으로 가져오는 경우 아래에 설명된 것처럼 파티션 스키마에 따라 레코드가 파일 그룹 사이에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-116">When data is bulk imported to the partitioned table(s), records will be distributed among the filegroups according to a partition scheme, as described below.</span></span>

<span data-ttu-id="dc945-117">**파티션 테이블을 만들려면 다음을 수행해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="dc945-117">**To create a partition table, you need to:**</span></span>

* <span data-ttu-id="dc945-118">각 파티션 테이블에 포함될 값/경계 범위를 정의하는 [파티션 함수를 만듭니다](https://msdn.microsoft.com/library/ms187802.aspx). 예를 들어 아래는 2013년 월별로(some\_datetime\_field) 파티션을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines the range of values/boundaries to be included in each individual partition table, e.g., to limit partitions by month(some\_datetime\_field) in the year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="dc945-119">파티션 함수의 각 파티션 범위를 실제 파일 그룹에 매핑하는 [파티션 스키마를 만듭니다](https://msdn.microsoft.com/library/ms179854.aspx). 아래는 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in the partition function to a physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="dc945-120">함수/스키마에 따라 각 파티션에 적용되는 범위를 확인하려면 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-120">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="dc945-121">데이터 스키마에 따라 [분할된 테이블을 만들고](https://msdn.microsoft.com/library/ms174979.aspx) 테이블 분할에 사용할 파티션 스키마 및 제약 조건 필드를 지정합니다. 아래는 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="dc945-122">자세한 내용은 [분할된 테이블 및 인덱스 만들기](https://msdn.microsoft.com/library/ms188730.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc945-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a><span data-ttu-id="dc945-123">각 파티션 테이블의 데이터를 대량으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="dc945-123">Bulk import the data for each individual partition table</span></span>
* <span data-ttu-id="dc945-124">BCP, BULK INSERT 또는 [SQL Server 마이그레이션 마법사](http://sqlazuremw.codeplex.com/)같은 기타 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="dc945-125">제공된 예에서는 BCP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-125">The example provided uses the BCP method.</span></span>
* <span data-ttu-id="dc945-126">로깅 오버헤드를 최소화하기 위해 [데이터베이스를 변경](https://msdn.microsoft.com/library/bb522682.aspx)하여 트랜잭션 로깅 스키마를 BULK_LOGGED로 변경합니다. 아래는 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-126">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="dc945-127">신속한 데이터 로드를 위해 대량 가져오기 작업을 병렬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-127">To expedite data loading, launch the bulk import operations in parallel.</span></span> <span data-ttu-id="dc945-128">빅 데이터를 SQL Server 데이터베이스로 신속하게 대량으로 가져오는 방법에 대한 팁은 [1시간 이내에 1TB 로드하기](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc945-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="dc945-129">다음 PowerShell 스크립트는 BCP를 사용하여 병렬로 데이터를 로드하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-129">The following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a><span data-ttu-id="dc945-130">인덱스를 만들어서 조인 및 쿼리 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="dc945-130">Create indexes to optimize joins and query performance</span></span>
* <span data-ttu-id="dc945-131">여러 테이블에서 모델링에 대한 데이터를 추출하려는 경우 조인 키에 인덱스를 만들어서 조인 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-131">If you will extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span></span>
* <span data-ttu-id="dc945-132">각 파티션에 대해 동일한 파일 그룹을 대상으로 하는 클러스터형 또는 비클러스터형 [인덱스를 만듭니다](https://technet.microsoft.com/library/ms188783.aspx). 아래는 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="dc945-133">또는</span><span class="sxs-lookup"><span data-stu-id="dc945-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="dc945-134">인덱스를 만든 후 데이터를 대량으로 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-134">You may choose to create the indexes before bulk importing the data.</span></span> <span data-ttu-id="dc945-135">인덱스를 만든 후 대량 가져오기를 수행하면 데이터 로드 속도가 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="dc945-135">Index creation before bulk importing will slow down the data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="dc945-136">고급 분석 프로세스 및 기술 작동 예제</span><span class="sxs-lookup"><span data-stu-id="dc945-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="dc945-137">공용 데이터 집합과 Cortana 분석 프로세스를 사용하여 종단간 연습 예제는 [실행 중인 Cortana 분석 프로세스: SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc945-137">For an end-to-end walkthrough example using the Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

