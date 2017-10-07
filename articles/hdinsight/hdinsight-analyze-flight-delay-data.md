---
title: "Azure HDInsight에서 Hadoop으로 aaaAnalyze 비행 연착 데이터 | Microsoft Docs"
description: "Toouse 하나의 Windows PowerShell 스크립트 toocreate를 HDInsight 클러스터에 Hive 작업을 실행할 Sqoop 작업을 실행 하는 방법을 알아보고 hello 클러스터를 삭제 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>HDInsight의 Hive를 사용하여 비행 지연 데이터 분석
Hive에서는 대규모 데이터의 요약, 쿼리, 분석에 적용할 수 있는 SQL 스타일 스크립트 언어인 *[HiveQL][hadoop-hiveql]*을 통해 Hadoop MapReduce 작업을 실행할 수 있습니다.

> [!IMPORTANT]
> hello이 문서의 단계는 Windows 기반 HDInsight 클러스터가 필요합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. Linux 기반 클러스터를 사용하는 단계는 [HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석(Linux)](hdinsight-analyze-flight-delay-data-linux.md)을 참조하세요.

Hello Azure HDInsight의 주요 이점 중 하나에 데이터 저장소 및 계산의 hello 분리입니다. HDInsight는 데이터 저장소로 Azure Blob 저장소를 사용합니다. 일반적인 작업은 세 부분으로 구성되어 있습니다.

1. **Azure Blob 저장소에 데이터 저장.**  예를 들어 날씨 데이터, 센서 데이터, 웹 로그 및 이 자습서의 경우 비행 지연 데이터를 Azure Blob 저장소에 저장할 수 있습니다.
2. **작업 실행** Windows PowerShell 스크립트 (또는 클라이언트 응용 프로그램)를 실행 하는 시간 tooprocess hello 데이터 이면 toocreate는 HDInsight 클러스터 작업을 실행 하 고 hello 클러스터를 삭제 합니다. hello 작업 출력 데이터 tooAzure Blob 저장소에 저장 합니다. hello 출력 데이터는 hello 클러스터를 삭제 한 후에 유지 됩니다. 따라서 사용한 데이터에 대해서만 비용을 지불하면 됩니다.
3. **Azure Blob 저장소에서 hello 출력을 검색**, 또는이 자습서에서는 hello 데이터 tooan Azure SQL 데이터베이스 내보내기.

hello 다음 다이어그램에서는 hello 시나리오와이 자습서의 hello 구조 수행 합니다.

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

Hello 다이어그램에서 hello 숫자 toohello 섹션 제목을 모니터는 참고 합니다. **M** 는 hello 주 프로세스를 나타냅니다. **A** 는 hello 부록에서 hello 콘텐츠를 나타냅니다.

hello 자습서의 주요 부분이 hello toouse 하나의 Windows PowerShell 스크립트 tooperform hello 다음 작업 방법을 보여 줍니다.

* HDInsight 클러스터 만들기
* 공항에 hello 클러스터 toocalculate 평균 지연에서 하이브 작업을 실행 합니다. hello 비행 연착 데이터는 Azure Blob 저장소 계정에 저장 됩니다.
* Sqoop 작업 tooexport hello 하이브 작업 출력 tooan Azure SQL 데이터베이스를 실행 합니다.
* Hello HDInsight 클러스터를 삭제 합니다.

Hello 부록 비행 연착 데이터를 업로드, Hive 쿼리 문자열 만들기/업로드 하 고 hello Sqoop 작업에 대 한 hello Azure SQL 데이터베이스를 준비 하기 위한 hello 지침을 찾을 수 있습니다.

> [!NOTE]
> 이 문서의 hello 단계는 특정 tooWindows 기반 HDInsight 클러스터 있습니다. Linux 기반 클러스터를 사용하는 단계는 [HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석(Linux)](hdinsight-analyze-flight-delay-data-linux.md)을 참조하세요.

### <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* **Azure PowerShell이 포함된 워크스테이션**.

    > [!IMPORTANT]
    > Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다. Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.
    >
    > Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell. 해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.

**이 자습서에서 사용하는 파일**

이 자습서에서 airline 비행 데이터의 지정 된 시간에 성능 hello를 사용 하 여 [연구 혁신적인 기술을 관리, 운송 Bureau 통계 또는 RITA][rita-website]합니다.
된 데이터는 hello 사본을 hello 공용 Blob 액세스 권한이 tooan Azure Blob 저장소 컨테이너를 업로드 합니다.
PowerShell 스크립트의 일부 hello 공용 blob 컨테이너 toohello 기본 blob 컨테이너에서 클러스터의 hello 데이터를 복사합니다. 이 스크립트는 또한 HiveQL hello 복사 toohello 동일한 Blob 컨테이너입니다.
Toolearn 하려는 경우 어떻게 tooget/업로드 hello 데이터 tooyour 소유 저장소 계정당 하나만 그리고 toocreate/업로드 hello HiveQL 스크립트 파일을 어떻게 참조 [부록 A](#appendix-a) 및 [부록 B](#appendix-b)합니다.

hello 다음 표에이 자습서에 사용 된 hello 파일.

<table border="1">
<tr><th>파일</th><th>설명</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>하이브 작업 hello hello HiveQL 스크립트 파일 사용. 이 스크립트는 업로드 된 tooan hello 공용 액세스를 사용 하는 Azure Blob 저장소 계정 되었습니다. <a href="#appendix-b">부록 B</a> 를 준비 하 고 업로드 하는이 파일 tooyour 직접 Azure Blob 저장소 계정에 대 한 지침을 했습니다.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Hello 하이브 작업에 대 한 입력된 데이터입니다. hello 데이터가 업로드 tooan hello 공용 액세스를 사용 하는 Azure Blob 저장소 계정 되었습니다. <a href="#appendix-a">부록 A</a> 지침에 hello 데이터 가져오기 및 hello 데이터 tooyour 직접 Azure Blob 저장소 계정에 업로드 합니다.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>hello hello 하이브 작업에 대 한 출력 경로입니다. hello 기본 컨테이너 hello 출력 데이터를 저장 하는 데 사용 됩니다.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>hello 하이브 작업 상태에 폴더 hello 기본 컨테이너입니다.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>클러스터 만들기 및 Hive/Sqoop 작업 실행
Hadoop MapReduce에서는 작업을 일괄 처리 방식으로 실행합니다. hello 대부분 비용 효율적인 방식으로 toorun 하이브 작업 toocreate hello 작업에 대 한 클러스터 이며 hello 작업이 완료 되 면 hello 작업을 삭제 합니다. 다음 스크립트에서는 hello에 대 한 전체 프로세스를 수행 하는 번호입니다.
HDInsight 클러스터를 만들고 Hive 작업을 실행하는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision] 및 [HDInsight에서 Hive 사용][hdinsight-use-hive]을 참조하세요.

**Azure PowerShell에서 toorun hello 하이브 쿼리**

1. 지침에 hello를 사용 하 여 hello Sqoop 작업 출력에 대 한 Azure SQL 데이터베이스와 hello 테이블을 만들 [부록 C](#appendix-c)합니다.
2. Windows PowerShell ISE를 열고 다음 스크립트는 hello를 실행 합니다.

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. Tooyour SQL 데이터베이스를 연결 하 고 hello AvgDelays 표에 도시별 평균 비행 연착 정보를 참조 하십시오.

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>부록 A-업로드 비행 지연 데이터 tooAzure Blob 저장소
Hello 데이터 파일 및 hello HiveQL 스크립트 파일을 업로드 (참조 [부록 B](#appendix-b)) 일부 계획이 필요 합니다. hello 개념 toostore hello 데이터 파일 및 HDInsight 클러스터를 만들고 hello 하이브 작업을 실행 하기 전에 hello HiveQL 파일은입니다. 다음 두 가지 옵션을 사용할 수 있습니다.

* **사용 하 여 hello 동일 hello 기본 파일 시스템으로 hello HDInsight 클러스터에서 사용할 Azure 저장소 계정입니다.** Hello HDInsight 클러스터 hello 저장소 계정 액세스 키를 더 추가 변경 toomake 필요 없습니다.
* **Hello HDInsight 클러스터 기본 파일 시스템에서에서 다른 Azure 저장소 계정을 사용 합니다.** Hello 상황에 hello 생성 부분이 hello Windows PowerShell에서 발견 된 스크립트를 수정 해야 [만들 HDInsight 클러스터와 실행된 Hive/Sqoop 작업](#runjob) toolink hello 추가 저장소 계정으로 저장소 계정입니다. 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision]를 참조하세요. hello HDInsight 클러스터는 다음 hello 저장소 계정에 대 한 hello 액세스 키를 알고 있습니다.

> [!NOTE]
> hello HiveQL 스크립트 파일에서 코딩 된 데이터 파일은 하드 hello에 대 한 hello Blob 저장소 경로입니다. 수정 내용에 따라 이를 업데이트해야 합니다.

**toodownload hello 비행 데이터**

1. 너무 찾아보기[연구 및 운송 통계 Bureau 혁신적인 기술을 관리][rita-website]합니다.
2. Hello 페이지에서 다음 값에는 hello를 선택 합니다.

    <table border="1">
    <tr><th>이름</th><th>값</th></tr>
    <tr><td>Filter Year</td><td>2013 </td></tr>
    <tr><td>Filter Period</td><td>January</td></tr>
    <tr><td>필드</td><td>*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay*(다른 모든 필드는 선택하지 않음)</td></tr>
    </table>
3. **다운로드**를 클릭합니다.
4. Hello 파일 toohello의 압축을 푸는 **C:\Tutorials\FlightDelay\2013Data** 폴더입니다. 각 파일은 CSV 파일이며 크기가 60GB 정도입니다.
5. Hello 파일 toohello 이름에 대 한 데이터를 포함 하는 hello 달의 이름을 변경 합니다. Hello 년 1 월 데이터를 포함 하는 hello 파일의 이름이 예를 들어 *January.csv*합니다.
6. 2013에서 12 개월 각각 hello에 대 한 단계 2와 5 단계 toodownload 파일을 반복 합니다. 하나의 파일 toorun hello 자습서의 최소가 필요 합니다.

**tooupload hello 비행 지연 데이터 tooAzure Blob 저장소**

1. Hello 매개 변수를 준비 합니다.

    <table border="1">
    <tr><th>변수 이름</th><th>참고 사항</th></tr>
    <tr><td>$storageAccountName</td><td>hello tooupload hello 데이터를 저장할 Azure 저장소 계정입니다.</td></tr>
    <tr><td>$blobContainerName</td><td>tooupload hello 데이터를 저장할 Blob 컨테이너를 hello입니다.</td></tr>
    </table>
2. Azure PowerShell ISE를 엽니다.
3. Hello를 hello 스크립트 창에 스크립트를 다음에 붙여 넣습니다.

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. 키를 눌러 **F5** toorun hello 스크립트입니다.

Toouse hello 파일을 업로드 하기 위한 다른 방법을 선택 하면 파일 경로 hello 자습서/flightdelay/데이터 인지를 확인 하십시오. hello hello 파일에 액세스 하기 위한 구문은 다음과 같습니다.

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

hello 경로 자습서/flightdelay/데이터는 hello 파일을 업로드 했을 때 만들었으므로 hello 가상 폴더입니다. 달마다 하나씩 12개의 파일이 있는지 확인합니다.

> [!NOTE]
> Hello 하이브 쿼리 tooread hello 새 위치에서 업데이트 해야 합니다.
>
> Hello 컨테이너 액세스 권한을 toobe 공용 구성 하거나 hello 저장소 계정 toohello HDInsight 클러스터를 바인딩합니다. 그렇지 않으면 hello 하이브 쿼리 문자열 hello 데이터 파일 수 tooaccess 되지 않습니다.

- - -

## <a id="appendix-b"></a>부록 B - HiveQL 스크립트 만들기 및 업로드
Azure PowerShell을 사용 하는 스크립트 파일에 한 번, 패키지 hello HiveQL 문은에 여러 HiveQL 문은 하나 실행할 수 있습니다. 이 섹션에서는 어떻게 toocreate HiveQL 스크립트 및 업로드 hello 스크립트 tooAzure Blob 저장소 Azure PowerShell을 사용 하 여 보여 줍니다. 하이브는 hello HiveQL 스크립트 toobe Azure Blob 저장소에 저장 해야 합니다.

hello HiveQL 스크립트 hello 다음을 수행 합니다.

1. **Hello delays_raw 테이블을 삭제**hello 테이블이 이미 존재 하는 경우, 합니다.
2. **Hello delays_raw 외부 하이브 테이블 만들기** hello 비행 지연 파일을 toohello Blob 저장소 위치를 가리키는 합니다. 이 쿼리는 필드는 ","로 구분되고 줄은 "\n"로 끝나도록 지정합니다. 필드 값 하이브는 필드 구분 기호는 쉼표와 필드 값의 일부인 하나를 구별할 수 없으므로 쉼표를 사용할 경우 이것은 문제가 (원점에 대 한 필드 값의 대/소문자 hello 변수인\_도시\_이름과 DEST\_ 도시\_이름). tooaddress이,이 hello 쿼리 열으로 잘못 분할은 toohold 데이터 임시 열을 만듭니다.
3. **Hello 지연 테이블을 삭제**hello 테이블이 이미 존재 하는 경우, 합니다.
4. **Hello 지연 테이블 만들기**합니다. 추가 처리 전에 hello 데이터를 유용한 tooclean 것 합니다. 이 쿼리는 새 테이블을 만듭니다 *지연*, hello delays_raw 테이블에서 합니다. 참고 (앞서 언급 했 듯이) hello TEMP 열 복사 되지 않습니다 및 그 hello **부분 문자열** 함수는 hello 데이터에서 사용 되는 tooremove 따옴표입니다.
5. **도시 이름별으로 hello 평균 날씨 지연 및 그룹 hello 결과 계산 합니다.** Hello 결과 tooBlob 저장소를 출력도 것입니다. 짧으며 hello 쿼리 아포스트로피 hello 데이터에서 제거 됩니다 hello에 대 한 값에 행을 제외 합니다 **weather_delay** null입니다. 이 작업은 이 자습서의 뒷부분에서 사용되는 Sqoop가 기본적으로 이러한 값을 정상적으로 처리하지 않기 때문에 필요합니다.

전체 hello HiveQL 명령 목록을 참조 하십시오. [데이터 정의 언어 하이브][hadoop-hiveql]합니다. 각 HiveQL 명령은 세미콜론으로 끝나야 합니다.

**toocreate HiveQL 스크립트 파일**

1. Hello 매개 변수를 준비 합니다.

    <table border="1">
    <tr><th>변수 이름</th><th>참고 사항</th></tr>
    <tr><td>$storageAccountName</td><td>hello tooupload hello HiveQL 스크립트를 저장할 Azure 저장소 계정입니다.</td></tr>
    <tr><td>$blobContainerName</td><td>tooupload hello HiveQL 스크립트를 저장할 Blob 컨테이너를 hello입니다.</td></tr>
    </table>
2. Azure PowerShell ISE를 엽니다.
3. 복사한 hello 스크립트 창에 스크립트를 다음 hello를 붙여넣습니다.

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Hello 스크립트에 사용 되는 hello 변수는 다음과 같습니다.

   * **$hqlLocalFileName** -hello 스크립트 파일을 저장 hello HiveQL 스크립트 로컬로 업로드 하기 전에 tooBlob 저장소입니다. Hello 파일 이름입니다. hello 기본값은 <u>C:\tutorials\flightdelay\flightdelays.hql</u>합니다.
   * **$hqlBlobName** -hello Azure Blob 저장소에에서 사용 된 hello HiveQL 스크립트 파일 blob 이름입니다. hello 기본값은 tutorials/flightdelay/flightdelays.hql입니다. 없기 때문에 hello 파일이 기록 될 직접 tooAzure Blob 저장소, 하지는 "/" hello blob 이름의 hello 시작 부분에 있습니다. Blob 저장소에서 tooaccess hello 파일을 사용 하도록 하려는 경우는 "/" hello hello 파일 이름 앞에 tooadd를 해야 합니다.
   * **$srcDataFolder** 및 **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"

- - -
## <a id="appendix-c"></a>부록 C-hello Sqoop 작업 출력에 대 한 Azure SQL 데이터베이스 준비
**tooprepare hello SQL 데이터베이스 (병합이 Sqoop 스크립트 hello로)**

1. Hello 매개 변수를 준비 합니다.

    <table border="1">
    <tr><th>변수 이름</th><th>참고 사항</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>hello hello Azure SQL 데이터베이스 서버의 이름입니다. 아무것도 입력 toocreate 새 서버입니다.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>hello hello Azure SQL 데이터베이스 서버에 대 한 로그인 이름입니다. $SqlDatabaseServerName 기존 서버 이면 hello 로그인 및 로그인 암호가 사용 되는 tooauthenticate hello 서버와는입니다. 그렇지 않으면 새 서버를 사용 하는 toocreate 됩니다.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>hello hello Azure SQL 데이터베이스 서버에 대 한 로그인 암호입니다.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>이 값은 새 Azure 데이터베이스 서버를 만드는 경우에만 사용됩니다.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>hello Sqoop 작업에 대 한 toocreate hello AvgDelays 표를 사용 하는 hello SQL 데이터베이스입니다. 이 매개 변수를 비워 두면 HDISqoop라는 데이터베이스가 만들어집니다. hello Sqoop 작업 출력에 대 한 hello 테이블 이름은 AvgDelays를입니다. </td></tr>
    </table>
2. Azure PowerShell ISE를 엽니다.
3. 복사한 hello 스크립트 창에 스크립트를 다음 hello를 붙여넣습니다.

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > hello 스크립트 사용 하 여 representational 상태 (transfer) 서비스, http://bot.whatismyipaddress.com, tooretrieve 외부 IP 주소입니다. hello IP 주소는 SQL 데이터베이스 서버에 대 한 방화벽 규칙을 만드는 데 사용 됩니다.

    Hello 스크립트에 사용 되는 일부 변수는 다음과 같습니다.

   * **$ipAddressRestService** -hello 기본값은 http://bot.whatismyipaddress.com 합니다. 외부 IP 주소를 가져오기 위한 공용 IP 주소 REST 서비스입니다. 원하는 경우 다른 서비스를 사용할 수 있습니다. hello 서비스를 통해 검색 된 hello 외부 IP 주소 (사용 하 여 Windows PowerShell 스크립트) 워크스테이션에서 hello 데이터베이스에 액세스할 수 있도록 Azure SQL 데이터베이스 서버에 대 한 방화벽 규칙 사용된 toocreate 됩니다.
   * **$fireWallRuleName** -hello Azure SQL 데이터베이스 서버에 대 한 hello 방화벽 규칙의 hello 이름입니다. 기본 이름은 hello <u>FlightDelay</u>합니다. 원하는 경우 이름을 바꿀 수 있습니다.
   * **$sqlDatabaseMaxSizeGB** - 이 값은 새 Azure SQL 데이터베이스 서버를 만드는 경우에만 사용됩니다. hello 기본값은 10GB입니다. 이 자습서에서는 크기가 10GB이면 충분합니다.
   * **$sqlDatabaseName** - 이 값은 새 Azure SQL 데이터베이스를 만드는 경우에만 사용됩니다. hello 기본값은 HDISqoop입니다. 이름을 변경한 후 hello Sqoop Windows PowerShell 스크립트를 적절 하 게 업데이트 해야 합니다.
4. 키를 눌러 **F5** toorun hello 스크립트입니다.
5. Hello 스크립트 출력의 유효성을 검사 합니다. Hello 스크립트가 성공적으로 실행 해야 합니다.

## <a id="nextsteps"></a> 다음 단계
알아야 이제 방법을 파일 tooAzure Blob 저장소 tooupload hello 데이터 Azure Blob 저장소를 사용 하 여 toopopulate 하이브 테이블 방법 어떻게 toorun 하이브 쿼리를 방법과 toouse HDFS tooan Azure SQL 데이터베이스에서 Sqoop tooexport 데이터입니다. 더 toolearn hello 다음 문서를 참조:

* [HDInsight 시작][hdinsight-get-started]
* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Oozie 사용][hdinsight-use-oozie]
* [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
