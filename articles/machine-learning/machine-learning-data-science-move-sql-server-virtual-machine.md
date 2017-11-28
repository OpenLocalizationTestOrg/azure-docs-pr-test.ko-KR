---
title: "Azure 가상 컴퓨터에서 aaaMove 데이터 tooSQL 서버 | Microsoft Docs"
description: "Azure VM에서 온-프레미스 SQL Server tooSQL 서버 또는 플랫 파일에서 데이터를 이동 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="2177d-103">Azure 가상 컴퓨터에서 데이터 tooSQL 서버 이동</span><span class="sxs-lookup"><span data-stu-id="2177d-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="2177d-104">이 항목에서는 플랫 파일 (CSV 또는 TSV 형식)에서 또는 온-프레미스 SQL Server tooSQL 서버에서에서 Azure 가상 컴퓨터 내의 데이터를 이동 하는 것에 대 한 hello 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="2177d-105">이동 데이터가 toohello 클라우드에 대 한 이러한 작업은 일부 hello 팀 데이터 과학 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="2177d-106">기계 학습에 대 한 이동 데이터 tooan Azure SQL 데이터베이스에 대 한 hello 옵션에 간략하게 설명 하는 항목을 참조 하십시오. [Azure 기계 학습에 대 한 데이터 tooan Azure SQL 데이터베이스를 이동](machine-learning-data-science-move-sql-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="2177d-107">hello **메뉴** hello 데이터 저장 끌어다 하는 동안 처리할 수 있는 다른 대상 환경으로 데이터 tooingest 팀 데이터 과학 프로세스 (TDSP) hello 하는 방법을 설명 하는 링크 tootopics 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="2177d-108">hello 다음 표에 요약 되어 Azure 가상 컴퓨터에서 이동 데이터 tooSQL 서버에 대 한 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="2177d-109"><b>원본</b></span><span class="sxs-lookup"><span data-stu-id="2177d-109"><b>SOURCE</b></span></span> | <span data-ttu-id="2177d-110"><b>대상: Azure VM의 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="2177d-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="2177d-111"><b>플랫 파일</b></span><span class="sxs-lookup"><span data-stu-id="2177d-111"><b>Flat File</b></span></span> |<span data-ttu-id="2177d-112">1. <a href="#insert-tables-bcp">명령줄 BCP(대량 복사 유틸리티)</a></span><span class="sxs-lookup"><span data-stu-id="2177d-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="2177d-113">2. <a href="#insert-tables-bulkquery">대량 삽입 SQL 쿼리</a></span><span class="sxs-lookup"><span data-stu-id="2177d-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="2177d-114">3. <a href="#sql-builtin-utilities">SQL Server의 기본 제공 그래픽 유틸리티</a></span><span class="sxs-lookup"><span data-stu-id="2177d-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="2177d-115"><b>온-프레미스 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="2177d-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="2177d-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사</a></span><span class="sxs-lookup"><span data-stu-id="2177d-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="2177d-117">2. <a href="#export-flat-file">Tooa 내보내기 플랫 파일</a></span><span class="sxs-lookup"><span data-stu-id="2177d-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="2177d-118">3. <a href="#sql-migration">SQL Database 마이그레이션 마법사</a></span><span class="sxs-lookup"><span data-stu-id="2177d-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="2177d-119">4. <a href="#sql-backup">데이터베이스 백업 및 복원</a></span><span class="sxs-lookup"><span data-stu-id="2177d-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="2177d-120">이 문서는 SQL Server Management Studio 또는 Visual Studio 데이터베이스 탐색기에서 SQL 명령을 실행하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="2177d-121">사용할 수 있습니다 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate 하 고 Azure에서 데이터 tooa SQL Server VM을 이동 합니다 하는 파이프라인을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="2177d-122">자세한 내용은 [Azure 데이터 팩터리를 사용하여 데이터 복사(복사 작업)](../data-factory/data-factory-data-movement-activities.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2177d-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="2177d-123"><a name="prereqs"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="2177d-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="2177d-124">이 자습서에서는 사용자가 다음을 보유하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="2177d-125">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2177d-125">An **Azure subscription**.</span></span> <span data-ttu-id="2177d-126">구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2177d-127">**Azure 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="2177d-127">An **Azure storage account**.</span></span> <span data-ttu-id="2177d-128">이 자습서에 hello 데이터를 저장 하기 위한 Azure 저장소 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="2177d-129">Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서.</span><span class="sxs-lookup"><span data-stu-id="2177d-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="2177d-130">Hello 저장소 계정을 만든 후 tooobtain hello 계정 키 tooaccess hello 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="2177d-131">[저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2177d-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="2177d-132">프로비전된 **Azure VM의 SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2177d-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="2177d-133">자세한 내용은 [고급 분석을 위해 Azure SQL Server 가상 컴퓨터를 IPython Notebook 서버로 설정](machine-learning-data-science-setup-sql-server-virtual-machine.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2177d-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="2177d-134">로컬로 설치 및 구성된 **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="2177d-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="2177d-135">자세한 내용은 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="2177d-136"><a name="filesource_to_sqlonazurevm"></a>Azure VM에서 플랫 파일 원본 tooSQL 서버에서에서 데이터를 이동</span><span class="sxs-lookup"><span data-stu-id="2177d-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="2177d-137">(행/열 형식으로 정렬) 플랫 파일에 데이터가 있으면 hello 다음 메서드를 통해 이동된 tooSQL Azure에서 서버 VM 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="2177d-138">명령줄 BCP(대량 복사 유틸리티)</span><span class="sxs-lookup"><span data-stu-id="2177d-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="2177d-139">대량 삽입 SQL 쿼리 </span><span class="sxs-lookup"><span data-stu-id="2177d-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="2177d-140">SQL Server의 기본 제공 그래픽 유틸리티(가져오기/내보내기, SSIS)</span><span class="sxs-lookup"><span data-stu-id="2177d-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="2177d-141"><a name="insert-tables-bcp"></a>명령줄 BCP(대량 복사 유틸리티)</span><span class="sxs-lookup"><span data-stu-id="2177d-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="2177d-142">BCP는 SQL Server와 함께 설치 하는 명령줄 유틸리티 및 hello 가장 빠른 방법으로 toomove 데이터 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="2177d-143">이는 모든 SQL Server 버전(온-프레미스 SQL Server, SQL Azure 및 Azure 기반의 SQL Server VM)에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="2177d-144">**BCP를 사용하려면 데이터가 어디에 있어야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="2177d-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="2177d-145">에 있는 원본 데이터를 포함 하는 파일이 필요 하지 않은 동안 hello 더 빠르게 hello 대상 SQL Server와 동일한 컴퓨터에 대 한 허용 (네트워크 속도 및 로컬 디스크 IO 속도)을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="2177d-146">Hello 플랫 파일을 포함 하는 데이터 toohello 컴퓨터를 이동할 수 있습니다를 사용 하 여 SQL Server가 설치 된와 같은 도구 다양 한 파일을 복사 [AZCopy](../storage/common/storage-use-azcopy.md), [Azure 저장소 탐색기](http://storageexplorer.com/) 또는 원격을 통해 windows 복사/붙여넣기 데스크톱 (RDP) 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="2177d-147">Hello 데이터베이스와 hello 테이블 hello 대상 SQL Server 데이터베이스에 생성 되어 있음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="2177d-148">방법의 예로 toodo hello 사용 하 여 해당 `Create Database` 및 `Create Table` 명령:</span><span class="sxs-lookup"><span data-stu-id="2177d-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="2177d-149">Hello 서식 파일 hello hello hello 컴퓨터의 명령줄에서 다음 명령을 실행 하 여 hello 테이블에 대 한 hello 스키마를 설명 하는 bcp가 설치 되어 있는 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="2177d-150">다음과 같이 hello bcp 명령을 사용 하 여 hello 데이터베이스로 hello 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="2177d-151">Hello SQL Server 컴퓨터에 설치 되어 동일한 이라고 가정할 hello 명령줄에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="2177d-152">**BCP 삽입 최적화** hello 다음 문서를 참조 하십시오 ['대량 가져오기 최적화에 대 한 지침이'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize 이러한 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="2177d-153"><a name="insert-tables-bulkquery-parallel"></a>더 빠른 데이터 이동을 위한 병렬 처리</span><span class="sxs-lookup"><span data-stu-id="2177d-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="2177d-154">Hello 데이터를 이동 하는 큰 경우 하면 작업 속도를 높일 수 동시에 PowerShell 스크립트에서 동시에 여러 BCP 명령을 실행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="2177d-155">**빅 데이터 수집** toooptimize 데이터 로드 크고 매우 큰 데이터 집합에 대 한 여러 파일 그룹 및 파티션 테이블을 사용 하 여 논리적 및 물리적 데이터베이스 테이블을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="2177d-156">만들기 및 데이터 toopartition 테이블에 로드 하는 방법에 대 한 자세한 내용은 참조 [부하 SQL 파티션 테이블 병렬](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="2177d-157">hello 아래 샘플 PowerShell 스크립트 보여 bcp를 사용 하 여 병렬 삽입:</span><span class="sxs-lookup"><span data-stu-id="2177d-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <span data-ttu-id="2177d-158"><a name="insert-tables-bulkquery"></a>대량 삽입 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="2177d-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="2177d-159">[대량 삽입 SQL 쿼리](https://msdn.microsoft.com/library/ms188365) 행/열 기반 파일에서 hello 데이터베이스에 사용 되는 tooimport 데이터가 될 수 있습니다 (지원 hello 형식을 다룹니다는[대량 내보내기 또는 가져오기 (SQL Server)에 대 한 데이터 준비](https://msdn.microsoft.com/library/ms188609)) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="2177d-160">아래는 대량 삽입을 위한 몇 가지 샘플 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="2177d-161">데이터를 분석 하 고 해당 hello SQL Server 데이터베이스에 동일한 날짜와 같은 특수 한 모든 필드에 대 한 형식 hello 가정 하는지 toomake 가져오기 전에 모든 사용자 지정 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="2177d-162">Tooset hello 날짜에 서식을 지정 방법으로 연도-월-일 (hello 연도-월-일 형식의 날짜를 포함 하는 데이터) 하는 경우의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="2177d-163">bulk import 문을 사용하여 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="2177d-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="2177d-164"><a name="sql-builtin-utilities"></a>SQL Server의 기본 제공 그래픽 유틸리티</span><span class="sxs-lookup"><span data-stu-id="2177d-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="2177d-165">플랫 파일에서 Azure에서 SQL Server VM에 SQL Server Integrations Services (SSIS) tooimport 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="2177d-166">SSIS는 두 가지 스튜디오 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="2177d-167">자세한 내용은 [SSIS(Integration Services) 및 스튜디오 환경](https://technet.microsoft.com/library/ms140028.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2177d-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="2177d-168">SQL Server 데이터 도구에 대한 자세한 내용은 [Microsoft SQL Server 데이터 도구](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="2177d-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="2177d-169">Hello 가져오기/내보내기 마법사에 대 한 세부 정보를 참조 하십시오. [SQL Server 가져오기 및 내보내기 마법사](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="2177d-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="2177d-170"><a name="sqlonprem_to_sqlonazurevm"></a>Azure VM에서 온-프레미스 SQL Server tooSQL 서버에서에서 데이터를 이동</span><span class="sxs-lookup"><span data-stu-id="2177d-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="2177d-171">마이그레이션 전략을 따라 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="2177d-172">배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사</span><span class="sxs-lookup"><span data-stu-id="2177d-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="2177d-173">TooFlat 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2177d-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="2177d-174">SQL 데이터베이스 마이그레이션 마법사</span><span class="sxs-lookup"><span data-stu-id="2177d-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="2177d-175">데이터베이스 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="2177d-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="2177d-176">아래는 각 방법에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="2177d-177">배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사</span><span class="sxs-lookup"><span data-stu-id="2177d-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="2177d-178">hello **배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사** 온-프레미스 SQL Server 인스턴스 tooSQL Azure VM에 서버에서에서 간단 하 고 권장 방법 toomove 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="2177d-179">자세한 단계와 같은 다른 방법에 대 한 내용은 참조 하세요. [데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션하려면](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="2177d-180"><a name="export-flat-file"></a>TooFlat 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2177d-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="2177d-181">Hello에 설명 된 대로 다양 한 방법을 사용 하는 toobulk 온-프레미스 SQL Server의 데이터를 내보내는 될 수 있습니다 [대량 가져오기 및 데이터의 내보내기 (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="2177d-182">이 문서에서는 예를 들어 hello 프로그램 BCP (대량 복사)을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="2177d-183">데이터를 플랫 파일로 내보낸 후 가져온된 tooanother SQL server 대량 가져오기 작업을 사용 하 여 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="2177d-184">온-프레미스 SQL Server tooa 파일에서에서 hello 데이터 내보내기 hello bcp 유틸리티를 사용 하 여 다음과 같이</span><span class="sxs-lookup"><span data-stu-id="2177d-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="2177d-185">Hello를 사용 하 여 Azure에서 SQL Server VM에서 hello 데이터베이스 및 hello 테이블을 만드는 `create database` 및 `create table` 1 단계에서 내보낸 hello 테이블 스키마에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="2177d-186">Hello 데이터를 내보내고 가져올 되 고 hello 테이블 스키마를 설명 하기 위해 서식 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="2177d-187">Hello 서식 파일의 세부 정보에 설명 되어 [서식 파일 (SQL Server)을 만들](https://msdn.microsoft.com/library/ms191516.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="2177d-188">때 SQL Server 컴퓨터 hello 실행 BCP에서 서식 파일 생성</span><span class="sxs-lookup"><span data-stu-id="2177d-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="2177d-189">SQL Server에 대해 원격으로 BCP를 실행하는 경우 서식 파일 생성</span><span class="sxs-lookup"><span data-stu-id="2177d-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="2177d-190">섹션에 설명 된 hello 방법 중 하나를 사용 하 여 [파일 원본에서 데이터 이동](#filesource_to_sqlonazurevm) 플랫 파일 tooa SQL Server의에서 toomove hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="2177d-191"><a name="sql-migration"></a>SQL 데이터베이스 마이그레이션 마법사</span><span class="sxs-lookup"><span data-stu-id="2177d-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="2177d-192">[SQL Server 데이터베이스 마이그레이션 마법사](http://sqlazuremw.codeplex.com/) 편리한 방법 toomove 두 SQL server 인스턴스 간에 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="2177d-193">원본 및 대상 테이블 사이 hello 사용자 toomap hello 데이터 스키마를 통해, 열 유형 및 다른 다양 한 기능을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="2177d-194">BCP (대량 복사)를 사용 하 여 hello 내부적입니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="2177d-195">Hello의 스크린 샷 시작 화면에 대 한 hello SQL 데이터베이스 마이그레이션 마법사는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![SQL Server 마이그레이션 마법사][2]

### <span data-ttu-id="2177d-197"><a name="sql-backup"></a>데이터베이스 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="2177d-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="2177d-198">SQL Server는 다음을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-198">SQL Server supports:</span></span>

1. <span data-ttu-id="2177d-199">[데이터베이스 백업 및 복원 기능](https://msdn.microsoft.com/library/ms187048.aspx) (모두 tooa 로컬 파일 또는 bacpac 내보내기 tooblob) 및 [데이터 계층 응용 프로그램](https://msdn.microsoft.com/library/ee210546.aspx) (bacpac를 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="2177d-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="2177d-200">기능 toodirectly 복사 된 데이터베이스 또는 복사 tooan 기존 SQL Azure 데이터베이스와 Azure에서 SQL Server Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="2177d-201">자세한 내용은 참조 하십시오. [데이터베이스 복사 마법사 사용 하 여 hello](https://msdn.microsoft.com/library/ms188664.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="2177d-202">데이터베이스 백업 hello 스크린 샷 위쪽/복원 옵션에서 SQL Server Management Studio는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2177d-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server 가져오기 도구][1]

## <a name="resources"></a><span data-ttu-id="2177d-204">리소스</span><span class="sxs-lookup"><span data-stu-id="2177d-204">Resources</span></span>
[<span data-ttu-id="2177d-205">데이터베이스 tooSQL Azure VM에서 서버 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="2177d-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="2177d-206">Azure Virtual Machines의 SQL Server 개요</span><span class="sxs-lookup"><span data-stu-id="2177d-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
