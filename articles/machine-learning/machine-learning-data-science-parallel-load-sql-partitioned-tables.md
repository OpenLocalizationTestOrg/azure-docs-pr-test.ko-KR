---
title: "aaaBuild Azure VM에서 SQL Server에 최적화 된 데이터의 빠른 병렬 가져오기 위한 테이블 및 | Microsoft Docs"
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
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="69249-103">SQL 파티션 테이블을 사용하여 대량의 데이터를 병렬로 가져오기</span><span class="sxs-lookup"><span data-stu-id="69249-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="69249-104">이 문서에서는 toobuild 데이터 tooa SQL Server 데이터베이스의 빠른 병렬 대량 가져오기를 위해 테이블을 분할 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="69249-105">빅 데이터 로드/transfer tooa SQL 데이터베이스에 대 한 데이터 toohello SQL DB 및 후속 쿼리 가져오기 향상 될 수 있습니다를 사용 하 여 *분할 테이블 및 뷰*합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="69249-106">새 데이터베이스 및 파일 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="69249-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="69249-107">아직 존재하지 않으면 [새 데이터베이스를 만듭니다](https://technet.microsoft.com/library/ms176061.aspx).</span><span class="sxs-lookup"><span data-stu-id="69249-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="69249-108">분할 된 hello 물리적 파일을 포함 하는 데이터베이스 파일 그룹 toohello 데이터베이스를 추가 합니다. 이를 수행할 수 있습니다 [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) 이면 새 또는 [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) hello 데이터베이스가 이미 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="69249-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="69249-109">하나 이상의 파일이 필요에 따라 tooeach 데이터베이스 파일 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="69249-110">Hello 파일 그룹 데이터를 저장할이 파티션과 hello 물리적 데이터베이스 파일 이름에 대 한 데이터를 보유 하는 hello 대상 파일 그룹을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="69249-111">hello 다음 예제에서는 새 데이터베이스를 주 hello와 각각에서 하나의 물리적 파일을 포함 하는 로그 그룹 이외의 3 개의 파일 그룹이 포함 된</span><span class="sxs-lookup"><span data-stu-id="69249-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="69249-112">hello 데이터베이스 파일은 hello SQL Server 인스턴스에 구성 된 대로 hello 기본 SQL Server 데이터 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69249-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="69249-113">Hello 기본 파일 위치에 대 한 자세한 내용은 참조 [Named Instances of SQL Server 인스턴스 및 기본 파일 위치](https://msdn.microsoft.com/library/ms143547.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

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

## <a name="create-a-partitioned-table"></a><span data-ttu-id="69249-114">분할된 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="69249-114">Create a partitioned table</span></span>
<span data-ttu-id="69249-115">Hello 이전 단계에서 만든 데이터베이스 파일 그룹 매핑된 toohello toohello 데이터 스키마에 따라 분할 된 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69249-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="69249-116">데이터를 대량 가져오는 경우 toohello 분할 테이블, 레코드 아래 설명 된 대로 tooa 파티션 구성표에 따라 hello 파일 그룹 간에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69249-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="69249-117">**파티션 테이블 toocreate 해야합니다.**</span><span class="sxs-lookup"><span data-stu-id="69249-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="69249-118">[파티션 함수를 만들](https://msdn.microsoft.com/library/ms187802.aspx) 값/경계 toobe hello 범위를 정의 하는에 포함 된 각 개별 파티션의 테이블 예를 들어, 월별 toolimit 파티션 (일부\_datetime\_필드) hello 연도의 2013:</span><span class="sxs-lookup"><span data-stu-id="69249-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="69249-119">[파티션 구성표를 만들](https://msdn.microsoft.com/library/ms179854.aspx) hello 파티션 함수 tooa 물리적 파일 그룹의 각 파티션 범위 예: 매핑되는:</span><span class="sxs-lookup"><span data-stu-id="69249-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="69249-120">각에서 적용 tooverify hello 범위 toohello 함수/체계에 따라 분할 hello 다음 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="69249-121">[분할 된 테이블 만들기](https://msdn.microsoft.com/library/ms174979.aspx)(s) tooyour 데이터 스키마에 따라 및 hello 파티션 구성표 및 제약 조건 필드 사용 toopartition hello 테이블 예를 들어 지정:</span><span class="sxs-lookup"><span data-stu-id="69249-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="69249-122">자세한 내용은 [분할된 테이블 및 인덱스 만들기](https://msdn.microsoft.com/library/ms188730.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69249-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="69249-123">각 개별 파티션의 테이블에 대 한 대량 가져오기 hello 데이터</span><span class="sxs-lookup"><span data-stu-id="69249-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="69249-124">BCP, BULK INSERT 또는 [SQL Server 마이그레이션 마법사](http://sqlazuremw.codeplex.com/)같은 기타 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69249-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="69249-125">제공 하는 hello 예제의 hello BCP 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="69249-126">[Hello 데이터베이스 변경](https://msdn.microsoft.com/library/bb522682.aspx) toochange 트랜잭션 로깅 예를 들어 구성표 tooBULK_LOGGED toominimize 오버 헤드를 로깅:</span><span class="sxs-lookup"><span data-stu-id="69249-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="69249-127">tooexpedite 데이터 로드를 병렬로 hello 대량 가져오기 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="69249-128">빅 데이터를 SQL Server 데이터베이스로 신속하게 대량으로 가져오는 방법에 대한 팁은 [1시간 이내에 1TB 로드하기](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69249-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="69249-129">hello 다음 PowerShell 스크립트는 BCP를 사용 하 여 로드 하는 병렬 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="69249-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="69249-130">인덱스 toooptimize 조인 및 쿼리 성능을 만들기</span><span class="sxs-lookup"><span data-stu-id="69249-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="69249-131">여러 테이블에서 모델링에 대 한 데이터를 추출 하는 하는 경우 인덱스를 만들 조인 키의 hello tooimprove hello 조인 성능.</span><span class="sxs-lookup"><span data-stu-id="69249-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="69249-132">[인덱스를 만들](https://technet.microsoft.com/library/ms188783.aspx) 에 대 한 각 파티션에 대해 동일한 파일 그룹 예를 들어 hello (클러스터형 또는 비클러스터형) 대상으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="69249-133">또는</span><span class="sxs-lookup"><span data-stu-id="69249-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="69249-134">Hello 데이터 대량 가져오기 수행 하기 전에 hello 인덱스 toocreate를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69249-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="69249-135">대량 가져오기 전에 인덱스 생성 hello 데이터 로드 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="69249-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="69249-136">고급 분석 프로세스 및 기술 작동 예제</span><span class="sxs-lookup"><span data-stu-id="69249-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="69249-137">공용 데이터 집합과 hello Cortana 분석 프로세스를 사용 하 여 종단 간 연습 예제를 참조 하십시오. [Cortana 분석 과정: SQL Server를 사용 하 여](machine-learning-data-science-process-sql-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69249-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

