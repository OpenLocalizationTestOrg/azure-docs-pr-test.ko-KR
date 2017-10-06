---
title: "PowerShell 및 Azure HDInsight를 사용 하 여 aaaRun Sqoop 작업 | Microsoft Docs"
description: "워크스테이션 toorun Sqoop에서에서 Azure PowerShell toouse 가져오고 Hadoop 클러스터와 Azure SQL 데이터베이스 내보내기에 대해 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: bbb6f53a-e019-4d01-92bd-92c208c760b6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 8313bbd109e968aeab540bbcefefe84ebd64c87e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-azure-powershell-for-hadoop-in-hdinsight"></a><span data-ttu-id="e7e5b-103">HDInsight에서 Hadoop용 Azure PowerShell을 사용하여 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e7e5b-103">Run Sqoop jobs using Azure PowerShell for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="e7e5b-104">HDInsight 클러스터와 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스 간에 내보내기 한 HDInsight tooimport toouse Azure PowerShell toorun Sqoop 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-104">Learn how toouse Azure PowerShell toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="e7e5b-105">이 문서의 hello 단계 중 하나는 Windows 기반 또는 Linux 기반 HDInsight 클러스터; 함께 사용할 수 있습니다. 그러나 다음이 단계 에서만 Windows 클라이언트에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-105">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps will only work from a Windows client.</span></span> <span data-ttu-id="e7e5b-106">다른 작업을 전송 방법에 대 한 hello 문서의 hello 위에 hello 탭 선택기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-106">For other job submission methods, click hello tab selector on hello top of hello article.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="e7e5b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e7e5b-107">Prerequisites</span></span>
<span data-ttu-id="e7e5b-108">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-108">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="e7e5b-109">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-109">**A workstation with Azure PowerShell**.</span></span>
  
    [!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
* <span data-ttu-id="e7e5b-110">**HDInsight에 Hadoop 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="e7e5b-111">[클러스터 및 SQL 데이터베이스 만들기](hdinsight-use-sqoop.md#create-cluster-and-sql-database)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="run-sqoop-using-powershell"></a><span data-ttu-id="e7e5b-112">PowerShell을 사용하여 Sqoop 실행</span><span class="sxs-lookup"><span data-stu-id="e7e5b-112">Run Sqoop using PowerShell</span></span>
<span data-ttu-id="e7e5b-113">PowerShell 스크립트 뒤 hello 미리 hello 소스 파일을 처리 하 고 tooan Azure SQL 데이터베이스를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-113">hello following PowerShell script pre-processes hello source file, and exports it tooan Azure SQL database:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $hdinsightClusterName = "<HDInsightClusterName>"

    $httpUserName = "admin"
    $httpPassword = "<Password>"

    $defaultStorageAccountName = $hdinsightClusterName + "store"
    $defaultBlobContainerName = $hdinsightClusterName


    $sqlDatabaseServerName = $hdinsightClusterName + "dbserver"
    $sqlDatabaseName = $hdinsightClusterName + "db"
    $sqlDatabaseLogin = "sqluser"
    $sqlDatabasePassword = "<Password>"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - pre-process hello source file

    Write-Host "`nPreprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = Get-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $defaultStorageAccountName
    $storageContainer = ($storageAccount |Get-AzureStorageContainer -Name $defaultBlobContainerName).CloudBlobContainer
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export hello log file from hello cluster toohello SQL database

    Write-Host "Exporting hello log file ..." -ForegroundColor Green

    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $tableName_log4j = "log4jlogs"
    $exportDir_log4j = "/tutorials/usesqoop/data"
    $sqljdbcdriver = "/user/oozie/share/lib/sqoop/sqljdbc41.jar"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1" `
        -Files $sqljdbcdriver

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput
    #endregion

## <a name="limitations"></a><span data-ttu-id="e7e5b-114">제한 사항</span><span class="sxs-lookup"><span data-stu-id="e7e5b-114">Limitations</span></span>
* <span data-ttu-id="e7e5b-115">대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-115">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="e7e5b-116">일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 삽입을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-116">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7e5b-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7e5b-117">Next steps</span></span>
<span data-ttu-id="e7e5b-118">파악 했으므로 이제 어떻게 toouse Sqoop 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-118">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="e7e5b-119">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-119">toolearn more, see:</span></span>

* <span data-ttu-id="e7e5b-120">[HDInsight와 함께 Oozie 사용](hdinsight-use-oozie.md): Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-120">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="e7e5b-121">[HDInsight를 사용 하 여 비행 연착 데이터를 분석](hdinsight-analyze-flight-delay-data.md): tooanalyze 비행 하이브 사용 하 여 데이터를 지연 하 고 다음 Sqoop tooexport 데이터 tooan Azure SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-121">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="e7e5b-122">[데이터 tooHDInsight 업로드](hdinsight-upload-data.md): 데이터 tooHDInsight/Azure Blob 저장소에 업로드 하기 위한 다른 방법을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e5b-122">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
