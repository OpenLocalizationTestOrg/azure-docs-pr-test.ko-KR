---
title: "Azure 가상 컴퓨터에서 SQL Server로 데이터 이동 | Microsoft Docs"
description: "플랫 파일 또는 온-프레미스 SQL Server에서 Azure VM의 SQL Server로 데이터를 이동합니다."
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="21c53-103">Azure 가상 컴퓨터에서 SQL Server로 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="21c53-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="21c53-104">이 토픽에서는 플랫 파일(CSV 또는 TSV 형식) 또는 온-프레미스 SQL Server에서 Azure 가상 컴퓨터의 SQL Server로 데이터를 이동하기 위한 옵션에 대해 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="21c53-105">클라우드로 데이터를 이동하는 이러한 작업은 팀 데이터 과학 프로세스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="21c53-106">기계 학습을 위해 Azure SQL 데이터베이스로 데이터를 이동하기 위한 옵션을 설명하는 토픽은 [Azure 기계 학습을 위해 Azure SQL 데이터베이스로 데이터 이동](machine-learning-data-science-move-sql-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="21c53-107">다음 **메뉴** 는 TDSP(팀 데이터 과학 프로세스) 중 데이터를 저장하고 처리할 수 있는 다른 대상 환경에 데이터를 수집하는 방법을 설명하는 토픽에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="21c53-108">다음 표에서는 Azure 가상 컴퓨터에서 SQL Server로 데이터를 이동하는 옵션을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="21c53-109"><b>원본</b></span><span class="sxs-lookup"><span data-stu-id="21c53-109"><b>SOURCE</b></span></span> | <span data-ttu-id="21c53-110"><b>대상: Azure VM의 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="21c53-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="21c53-111"><b>플랫 파일</b></span><span class="sxs-lookup"><span data-stu-id="21c53-111"><b>Flat File</b></span></span> |<span data-ttu-id="21c53-112">1. <a href="#insert-tables-bcp">명령줄 BCP(대량 복사 유틸리티)</a></span><span class="sxs-lookup"><span data-stu-id="21c53-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="21c53-113">2. <a href="#insert-tables-bulkquery">대량 삽입 SQL 쿼리</a></span><span class="sxs-lookup"><span data-stu-id="21c53-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="21c53-114">3. <a href="#sql-builtin-utilities">SQL Server의 기본 제공 그래픽 유틸리티</a></span><span class="sxs-lookup"><span data-stu-id="21c53-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="21c53-115"><b>온-프레미스 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="21c53-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="21c53-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Microsoft Azure 가상 컴퓨터에 SQL Server 데이터베이스 배포 마법사</a></span><span class="sxs-lookup"><span data-stu-id="21c53-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="21c53-117">2. <a href="#export-flat-file">플랫 파일로 내보내기</a></span><span class="sxs-lookup"><span data-stu-id="21c53-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="21c53-118">3. <a href="#sql-migration">SQL Database 마이그레이션 마법사</a></span><span class="sxs-lookup"><span data-stu-id="21c53-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="21c53-119">4. <a href="#sql-backup">데이터베이스 백업 및 복원</a></span><span class="sxs-lookup"><span data-stu-id="21c53-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="21c53-120">이 문서는 SQL Server Management Studio 또는 Visual Studio 데이터베이스 탐색기에서 SQL 명령을 실행하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="21c53-121">하나의 대안으로, [Azure 데이터 팩터리](https://azure.microsoft.com/services/data-factory/) 를 사용하여 Azure의 SQL Server VM으로 데이터를 이동하는 파이프라인을 만들고 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="21c53-122">자세한 내용은 [Azure 데이터 팩터리를 사용하여 데이터 복사(복사 작업)](../data-factory/data-factory-data-movement-activities.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="21c53-123"><a name="prereqs"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="21c53-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="21c53-124">이 자습서에서는 사용자가 다음을 보유하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="21c53-125">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="21c53-125">An **Azure subscription**.</span></span> <span data-ttu-id="21c53-126">구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="21c53-127">**Azure 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="21c53-127">An **Azure storage account**.</span></span> <span data-ttu-id="21c53-128">이 자습서에서는 데이터 저장을 위해 Azure 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="21c53-129">Azure 저장소 계정이 없는 경우 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="21c53-130">저장소 계정을 만든 후에는 저장소 액세스에 사용되는 계정 키를 확보해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="21c53-131">[저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="21c53-132">프로비전된 **Azure VM의 SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="21c53-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="21c53-133">자세한 내용은 [고급 분석을 위해 Azure SQL Server 가상 컴퓨터를 IPython Notebook 서버로 설정](machine-learning-data-science-setup-sql-server-virtual-machine.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="21c53-134">로컬로 설치 및 구성된 **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="21c53-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="21c53-135">자세한 내용은 [Azure PowerShell 설치 및 구성법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="21c53-136"><a name="filesource_to_sqlonazurevm"></a> 플랫 파일 원본에서 Azure VM의 SQL Server로 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="21c53-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="21c53-137">데이터가 플랫 파일에 있는 경우(행/열 형식으로 정렬됨) 다음 방법을 통해 Azure 기반의 SQL Server VM으로 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="21c53-138">명령줄 BCP(대량 복사 유틸리티)</span><span class="sxs-lookup"><span data-stu-id="21c53-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="21c53-139">대량 삽입 SQL 쿼리 </span><span class="sxs-lookup"><span data-stu-id="21c53-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="21c53-140">SQL Server의 기본 제공 그래픽 유틸리티(가져오기/내보내기, SSIS)</span><span class="sxs-lookup"><span data-stu-id="21c53-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="21c53-141"><a name="insert-tables-bcp"></a>명령줄 BCP(대량 복사 유틸리티)</span><span class="sxs-lookup"><span data-stu-id="21c53-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="21c53-142">BCP는 SQL Server와 함께 설치되는 명령줄 유틸리티로, 데이터를 이동하는 가장 빠른 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="21c53-143">이는 모든 SQL Server 버전(온-프레미스 SQL Server, SQL Azure 및 Azure 기반의 SQL Server VM)에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="21c53-144">**BCP를 사용하려면 데이터가 어디에 있어야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="21c53-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="21c53-145">필수 사항은 아니지만 원본 데이터가 포함된 파일을 대상 SQL 서버와 같은 컴퓨터에 배치하면 전송 속도가 빨라집니다(네트워크 속도와 로컬 디스크 IO 속도 차이).</span><span class="sxs-lookup"><span data-stu-id="21c53-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="21c53-146">[AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage 탐색기](http://storageexplorer.com/), Windows 복사/붙여넣기, RDP(원격 데스크톱 프로토콜) 등 다양한 파일 복사 도구를 사용하여 데이터가 포함된 플랫 파일을 SQL Server가 설치된 컴퓨터로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="21c53-147">대상 SQL Server 데이터베이스에 데이터베이스 및 테이블이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="21c53-148">다음은 `Create Database` 및 `Create Table` 명령을 사용하여 이 작업을 수행하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="21c53-149">bcp가 설치된 컴퓨터의 명령줄에서 다음 명령을 실행하여 테이블의 스키마를 설명하는 서식 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="21c53-150">다음과 같이 bcp 명령을 사용하여 데이터베이스에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="21c53-151">SQL Server가 같은 컴퓨터에 설치되었다면 이 명령이 명령줄에서 작동할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="21c53-152">**BCP 삽입 최적화 삽입** 작업을 최적화하는 방법은 ['대량 가져오기를 최적화하기 위한 지침'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="21c53-153"><a name="insert-tables-bulkquery-parallel"></a>더 빠른 데이터 이동을 위한 병렬 처리</span><span class="sxs-lookup"><span data-stu-id="21c53-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="21c53-154">이동하려는 데이터가 큰 경우 PowerShell 스크립트에서 동시에 여러 BCP 명령을 병렬로 수행하면 작업 속도를 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="21c53-155">**빅 데이터 수집** 매우 큰 데이터 집합의 데이터 로드 작업을 최적화하려면 여러 파일 그룹 및 파티션 테이블을 사용하여 논리적 및 물리적 데이터베이스 테이블을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="21c53-156">파티션 테이블을 만들어서 데이터를 로드하는 방법에 대한 자세한 내용은 [SQL 파티션 테이블 병렬 로드](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="21c53-157">아래는 bcp를 사용한 병렬 삽입을 보여 주는 샘플 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="21c53-158"><a name="insert-tables-bulkquery"></a>대량 삽입 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="21c53-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="21c53-159">[대량 삽입 SQL 쿼리](https://msdn.microsoft.com/library/ms188365)는 데이터를 행/열 기반 파일에서 데이터베이스로 가져오는 데 사용할 수 있습니다(지원되는 형식은 [대량 내보내기 또는 가져오기를 위한 데이터 준비(SQL Server)](https://msdn.microsoft.com/library/ms188609) 항목에서 설명).</span><span class="sxs-lookup"><span data-stu-id="21c53-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="21c53-160">아래는 대량 삽입을 위한 몇 가지 샘플 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="21c53-161">SQL Server 데이터베이스에서 날짜 같은 특수 필드의 형식이 동일하도록 데이터를 분석하고 사용자 지정 옵션을 설정한 후 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="21c53-162">다음은 날짜 형식을 년-월-일로 설정하는 방법의 예입니다(데이터에 년-월-일 형식의 날짜가 포함된 경우).</span><span class="sxs-lookup"><span data-stu-id="21c53-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="21c53-163">bulk import 문을 사용하여 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="21c53-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="21c53-164"><a name="sql-builtin-utilities"></a>SQL Server의 기본 제공 그래픽 유틸리티</span><span class="sxs-lookup"><span data-stu-id="21c53-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="21c53-165">SSIS(SQL Server Integrations Services)를 사용하여 플랫 파일의 데이터를 Azure 기반의 SQL Server VM으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="21c53-166">SSIS는 두 가지 스튜디오 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="21c53-167">자세한 내용은 [SSIS(Integration Services) 및 스튜디오 환경](https://technet.microsoft.com/library/ms140028.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="21c53-168">SQL Server 데이터 도구에 대한 자세한 내용은 [Microsoft SQL Server 데이터 도구](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="21c53-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="21c53-169">가져오기/내보내기 마법사에 대한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="21c53-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="21c53-170"><a name="sqlonprem_to_sqlonazurevm"></a>온-프레미스 SQL Server에서 Azure VM의 SQL Server로 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="21c53-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="21c53-171">다음과 같은 마이그레이션 전략을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="21c53-172">Microsoft Azure 가상 컴퓨터에 SQL Server 데이터베이스 배포 마법사</span><span class="sxs-lookup"><span data-stu-id="21c53-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="21c53-173">플랫 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="21c53-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="21c53-174">SQL 데이터베이스 마이그레이션 마법사</span><span class="sxs-lookup"><span data-stu-id="21c53-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="21c53-175">데이터베이스 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="21c53-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="21c53-176">아래는 각 방법에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="21c53-177">Microsoft Azure 가상 컴퓨터에 SQL Server 데이터베이스 배포 마법사</span><span class="sxs-lookup"><span data-stu-id="21c53-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="21c53-178">**Microsoft Azure VM에 SQL Server 데이터베이스 배포 마법사** 는 온-프레미스 SQL Server 인스턴스에서 Azure VM의 SQL Server로 데이터를 이동하는 간단한 권장 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="21c53-179">자세한 단계 및 다른 대안에 대한 설명은 [Azure VM의 SQL Server로 데이터베이스 마이그레이션](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="21c53-180"><a name="export-flat-file"></a>플랫 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="21c53-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="21c53-181">[데이터의 대량 가져오기 및 내보내기(SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) 토픽에 설명된 대로 온-프레미스 SQL Server에서 데이터를 대량으로 내보내는 데 다양한 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="21c53-182">이 문서에서는 그 방법 중 하나로 BCP(대량 복사 프로그램)에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="21c53-183">데이터를 플랫 파일로 내보낸 후에는 대량 삽입을 사용하여 다른 SQL Server로 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="21c53-184">다음과 같이 bcp 유틸리티를 사용하여 온-프레미스 SQL Server에서 파일로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="21c53-185">1단계에서 내보낸 테이블 스키마에 대해 `create database` 및 `create table`을 사용하여 Azure 기반의 SQL Server VM에 데이터베이스 및 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="21c53-186">내보내는/가져오는 데이터의 테이블 스키마를 설명하는 서식 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="21c53-187">서식 파일의 세부 정보는 [서식 파일 만들기(SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="21c53-188">SQL Server 컴퓨터에서 BCP를 실행하는 경우 서식 파일 생성</span><span class="sxs-lookup"><span data-stu-id="21c53-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="21c53-189">SQL Server에 대해 원격으로 BCP를 실행하는 경우 서식 파일 생성</span><span class="sxs-lookup"><span data-stu-id="21c53-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="21c53-190">[파일 원본에서 데이터 이동](#filesource_to_sqlonazurevm) 섹션에 설명된 아무 방법을 사용하여 플랫 파일에서 SQL Server로 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="21c53-191"><a name="sql-migration"></a>SQL 데이터베이스 마이그레이션 마법사</span><span class="sxs-lookup"><span data-stu-id="21c53-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="21c53-192">[SQL Server 데이터베이스 마이그레이션 마법사](http://sqlazuremw.codeplex.com/) 는 두 SQL Server 인스턴스 간에 데이터를 이동할 수 있는 사용자에게 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="21c53-193">사용자가 원본과 대상 테이블 사이에 데이터 스키마를 매핑하고, 열 유형 및 다양한 기타 기능을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="21c53-194">사용자에게는 보이지 않지만 SQL Server 데이터베이스 마이그레이션 마법사는 BCP(대량 복사)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="21c53-195">아래는 SQL 데이터베이스 마이그레이션 마법사의 시작 화면 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![SQL Server 마이그레이션 마법사][2]

### <span data-ttu-id="21c53-197"><a name="sql-backup"></a>데이터베이스 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="21c53-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="21c53-198">SQL Server는 다음을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-198">SQL Server supports:</span></span>

1. <span data-ttu-id="21c53-199">[데이터베이스 백업 및 복원 기능](https://msdn.microsoft.com/library/ms187048.aspx)(로컬 파일 백업 또는 blob로 bacpac 내보내기 모두 지원) 및 [데이터 계층 응용 프로그램](https://msdn.microsoft.com/library/ee210546.aspx)(bacpac 사용).</span><span class="sxs-lookup"><span data-stu-id="21c53-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="21c53-200">복사된 데이터베이스를 사용하여 또는 기존 SQL Azure 데이터베이스에 복사하여 Azure에서 직접 SQL Server VM을 만드는 기능.</span><span class="sxs-lookup"><span data-stu-id="21c53-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="21c53-201">자세한 내용은 [데이터베이스 복사 마법사 사용](https://msdn.microsoft.com/library/ms188664.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21c53-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="21c53-202">아래는 SQL Server Management Studio의 데이터베이스 백업/복원 옵션 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="21c53-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server 가져오기 도구][1]

## <a name="resources"></a><span data-ttu-id="21c53-204">리소스</span><span class="sxs-lookup"><span data-stu-id="21c53-204">Resources</span></span>
[<span data-ttu-id="21c53-205">Azure VM에서 SQL Server로 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="21c53-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="21c53-206">Azure Virtual Machines의 SQL Server 개요</span><span class="sxs-lookup"><span data-stu-id="21c53-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
