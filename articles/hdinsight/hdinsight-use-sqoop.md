---
title: "Azure HDInsight (Hadoop)와 aaaRun Apache Sqoop 작업 | Microsoft Docs"
description: "워크스테이션 toorun Sqoop에서에서 Azure PowerShell toouse 가져오고 Hadoop 클러스터와 Azure SQL 데이터베이스 내보내기에 대해 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>HDInsight에서 Hadoop과 Sqoop 사용
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

자세한 내용은 방법 HDInsight tooimport 및 HDInsight 클러스터와 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스 간에 내보내기에서 Sqoop toouse 합니다.

Hadoop 로그 파일과 같은 구조화 되지 않은 작업과 구조화 된 데이터를 처리 하기 위한 자연 스러운 선택 되어도 수도 있습니다 관계형 데이터베이스에 저장 된 필요 tooprocess 구조화 된 데이터입니다.

[Sqoop] [ sqoop-user-guide-1.4.4] 은 설계 된 도구 tootransfer Hadoop 클러스터 및 관계형 데이터베이스 간에 데이터입니다. 사용할 수 있습니다 (RDBMS) 관계형 데이터베이스 관리 시스템에서 tooimport 데이터와 같은 SQL Server, MySQL 또는 hello distributed Hadoop 파일 시스템 (HDFS)에 Oracle에서 Hadoop MapReduce 또는 하이브를 hello 데이터 변환한 다음에 다시 hello 데이터를 내보낼는 RDBMS 합니다. 이 자습서에서는 관계형 데이터베이스에 SQL Server 데이터베이스를 사용합니다.

HDInsight 클러스터에서 지원 되는 Sqoop 버전에서는 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Hello 시나리오를 이해합니다

HDInsight 클러스터는 일부 샘플 데이터와 함께 제공됩니다. 다음 두 개의 샘플 hello 사용:

* */example/data/sample.log*에 있는 log4j 로그 파일. 다음 로그 hello hello 파일에서 추출 된:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* 명명 된 Hive 테이블 *hivesampletable*, 참조 데이터 파일에 있는 hello는 */hive/warehouse/hivesampletable*합니다. hello 테이블 일부 모바일 장치 데이터를 포함 합니다. 
  
  | 필드 | 데이터 형식 |
  | --- | --- |
  | clientid |string |
  | querytime |string |
  | market |string |
  | deviceplatform |string |
  | devicemake |string |
  | devicemodel |string |
  | state |string |
  | country |string |
  | querydwelltime |double |
  | sessionid |bigint |
  | sessionpagevieworder |bigint |

먼저, 내보낸 *sample.log* 및 *hivesampletable* toohello Azure SQL 데이터베이스 또는 서버 tooSQL 및 hello 모바일 장치 데이터를 포함 하는 가져오기 hello 테이블 tooHDInsight hello를 사용 하 여 백업 다음 경로:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>클러스터 및 SQL 데이터베이스 만들기
이 섹션에서는 클러스터 toocreate, SQL 데이터베이스 및 hello SQL 데이터베이스 스키마가 실행 중인 hello 자습서를 사용 하 여에 대 한 Azure 포털 및 Azure 리소스 관리자 템플릿 hello 하는 방법을 보여 줍니다. hello 서식 파일에서 확인할 수 있습니다 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/)합니다. 리소스 관리자 템플릿 hello bacpac 패키지 toodeploy hello 테이블 스키마 tooSQL 데이터베이스를 호출합니다.  hello bacpac 패키지 https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac 공용 blob 컨테이너에 배치 됩니다. Hello bacpac 파일에 대 한 toouse 개인 컨테이너를 원하는 경우 다음 hello 서식 파일의 값에는 hello를 사용 합니다.
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Toouse Azure PowerShell toocreate hello 클러스터와 SQL 데이터베이스 hello를 선호 하는 경우 참조 [부록 A](#appendix-a---a-powershell-sample)합니다.

1. 다음 이미지 tooopen hello Azure 포털에서에서 리소스 관리자 템플릿으로 hello를 클릭 합니다.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Hello 다음과 같은 속성을 입력 합니다.

    - **구독**: Azure 구독을 입력합니다.
    - **리소스 그룹**: 새 Azure 리소스 그룹을 만들거나 기존 Azure 리소스 그룹을 선택합니다.  리소스 그룹은 관리 목적으로 사용됩니다.  개체에 대한 컨테이너입니다.
    - **위치**: 지역을 선택합니다.
    - **ClusterName**: hello Hadoop 클러스터에 대 한 이름을 입력 합니다.
    - **로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 관리자입니다.
    - **SSH 사용자 이름 및 암호**.
    - **SQL 데이터베이스 서버 로그인 이름 및 암호**.
    - **위치 _artifacts**: toouse 고유한 backpac 파일을 다른 위치에 사용 하려는 경우가 아니면 hello 기본값을 사용 합니다.
    - **_artifacts 위치 Sas 토큰**: 비워 둡니다.
    - **Bacpac 파일 이름**: toouse backpac 파일을 직접 사용 하려는 경우가 아니면 hello 기본값을 사용 합니다.
     
     다음 값에는 hello는 hello 변수 섹션에서 하드 코드 됨.
     
     | 기본 저장소 계정 이름 | <CluterName>store |
     | --- | --- |
     | Azure SQL 데이터베이스 서버 이름 |<ClusterName>dbserver |
     | Azure SQL 데이터베이스 이름 |<ClusterName>db |
     
     이러한 값을 기록해 두십시오.  Hello 자습서의 뒷부분에 나오는 필요 합니다.

3. 클릭 **확인** toosave hello 매개 변수입니다.

4. hello에서 **사용자 지정 배포** 블레이드에서 클릭 **리소스 그룹** 드롭다운 상자를 선택한 다음 클릭 **새로** toocreate 새 리소스 그룹입니다. hello 리소스 그룹은 hello 클러스터, hello 종속 저장소 계정 및 다른 링크 된 리소스를 그룹화 하는 컨테이너입니다.

5.**약관**을 클릭한 다음 **만들기**를 클릭합니다.

6.**만들기**를 클릭합니다. 템플릿 배포에 배포 제출 중이라는 제목의 새 타일이 표시됩니다. 약 20 분 toocreate hello 클러스터 및 SQL 데이터베이스에 대 한 필요합니다.

Toouse 기존 Azure SQL 데이터베이스 또는 Microsoft SQL Server를 선택 하는 경우

* **Azure SQL 데이터베이스**: 워크스테이션에서 Azure SQL 데이터베이스 서버 tooallow 액세스 hello에 대 한 방화벽 규칙을 구성 해야 합니다. Azure SQL 데이터베이스를 만들고 hello 방화벽을 구성 하는 방법에 대 한 지침은 [Azure SQL 데이터베이스를 사용 하 여 시작][sqldatabase-get-started]합니다. 
  
  > [!NOTE]
  > 기본적으로 Azure SQL 데이터베이스는 Azure HDInsight 같은 Azure 서비스로부터의 연결을 허용합니다. 이 방화벽 설정을 비활성화 해야 tooenable hello Azure 포털에서 합니다. Azure SQL Database 만들기 및 방화벽 규칙 구성에 대한 지침은 [SQL Database 만들기 및 구성][sqldatabase-create-configue]을 참조하세요.
  > 
  > 
* **SQL Server**: hello에 HDInsight 클러스터에 있으면 동일한 가상 네트워크 SQL Server와 Azure의 hello 단계가 문서 tooimport 및 내보내기 데이터 tooa SQL Server 데이터베이스에 사용할 수 있습니다.
  
  > [!NOTE]
  > HDInsight는 위치 기반 가상 네트워크만 지원하며 현재 선호도 그룹 기반 가상 네트워크와는 연동되지 않습니다.
  > 
  > 
  
  * toocreate 가상 네트워크 구성, 참조 및 [hello Azure 포털을 사용 하 여 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다.
    
    * SQL Server 데이터 센터를 사용 하는 경우에 hello와 가상 네트워크 구성 해야 *사이트 간* 또는 *지점 및 사이트*합니다.
      
      > [!NOTE]
      > 에 대 한 **지점-사이트** 가상 네트워크, SQL Server를 실행 해야 hello VPN 클라이언트 hello에서 사용할 수 있는 구성 응용 프로그램 **대시보드** Azure 가상 네트워크 구성 합니다.
      > 
      > 
    * SQL Server를 호스트 하는 hello 가상 컴퓨터가 hello의 멤버인 경우 모든 가상 네트워크 구성을 사용할 수 있습니다는 Azure 가상 컴퓨터에서 SQL 서버를 사용 하는 경우 HDInsight와 동일한 가상 네트워크입니다.
  * 가상 네트워크에는 HDInsight 클러스터 toocreate 참조 [만들기 Hadoop 사용자 지정 옵션을 사용 하 여 HDInsight 클러스터를](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server는 인증도 허용해야 합니다. SQL Server 로그인 toocomplete hello이 문서의 단계를 사용 해야 합니다.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Sqoop 작업 실행
HDInsight는 다양한 메서드를 사용하여 Sqoop 작업을 실행할 수 있습니다. 어느 방법이 적합 한, 테이블 toodecide 다음 hello를 사용 하 여 다음 연습은 hello 링크를 따라 이동 합니다.

| **이것을 사용** 하세요... | ... **대화형** 셸 | ...**배치** 처리 | ... **클러스터 운영 체제** | ... **클라이언트 운영 체제** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X, 또는 Windows |
| [Hadoop용 .NET SDK](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux 또는or Windows |Windows(당분간) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux 또는or Windows |Windows |

## <a name="limitations"></a>제한 사항
* 대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.
* 일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 개의 삽입이 수행 합니다.

## <a name="next-steps"></a>다음 단계
파악 했으므로 이제 어떻게 toouse Sqoop 합니다. toolearn 더 참조 하십시오.

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight와 함께 Oozie 사용][hdinsight-use-oozie]: Oozie 워크플로에서 Sqoop 작업을 사용합니다.
* [HDInsight를 사용 하 여 비행 연착 데이터를 분석][hdinsight-analyze-flight-data]: tooanalyze 비행 하이브 사용 하 여 데이터를 지연 하 고 다음 Sqoop tooexport 데이터 tooan Azure SQL 데이터베이스를 사용 합니다.
* [데이터 tooHDInsight 업로드][hdinsight-upload-data]: 데이터 tooHDInsight/Azure Blob 저장소에 업로드 하기 위한 다른 방법을 찾아야 합니다.

## <a name="appendix-a---a-powershell-sample"></a>부록 A - PowerShell 샘플
hello PowerShell 샘플 hello 다음 단계를 수행 합니다.

1. TooAzure를 연결 합니다.
2. Azure 리소스 그룹 만들기 자세한 내용은 [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)
3. Azure SQL 데이터베이스 서버, Azure SQL 데이터베이스 및 두 개의 테이블을 만듭니다. 
   
    SQL Server를 대신 사용 하는 경우 다음 문은 toocreate hello 표 hello를 사용 합니다.
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    hello 가장 쉬운 방법은 tooexamine hello 데이터베이스 및 테이블에는 Visual Studio toouse입니다. hello 데이터베이스 서버 및 데이터베이스 hello hello Azure 포털을 사용 하 여 검사할 수 있습니다.
4. HDInsight 클러스터 만들기
   
    tooexamine hello 클러스터 hello Azure 포털 또는 Azure PowerShell을 사용할 수 있습니다.
5. Hello 원본 데이터 파일을 전처리 합니다.
   
    이 자습서에서는 log4j 로그 파일 (구분 기호로 분리 된 파일) 및 Hive 테이블 tooan Azure SQL 데이터베이스를 내보냅니다. hello 구분 기호로 분리 된 파일 이라고 */example/data/sample.log*합니다. Hello 자습서의 앞부분에 나오는 준다는 사실을 알았습니다 log4j 로그의 몇 가지 샘플. Hello 로그 파일에는 일부 빈 줄 및 줄 비슷한 toothese 일부:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    이 데이터를 사용 하는 다른 예에 대 한 문제가 있지만 전에 hello Azure SQL 데이터베이스 또는 SQL Server로 가져올 수 있습니다 이러한 예외를 제거 해야 했습니다. 빈 문자열이 나 더 적은 있는 선 경우 Sqoop 내보내기 실패 함 hello Azure SQL 데이터베이스 테이블에 정의 된 필드의 hello 수보다 요소입니다. hello log4jlogs 테이블 7 문자열 형식 필드에 있습니다.
   
    이 절차에서는 hello 클러스터에서 새 파일을 만듭니다: tutorials/usesqoop/data/sample.log 합니다. tooexamine hello 수정 된 데이터 파일을 hello Azure 포털, Azure 저장소 탐색기 도구를 사용 하는 또는 Azure PowerShell을 사용할 수 있습니다. [HDInsight 시작] [ hdinsight-get-started] 코드는 Azure PowerShell toodownload 파일 사용에 대 한 샘플링 하 여 hello 파일 콘텐츠를 표시 합니다.
6. 데이터 파일 toohello Azure SQL 데이터베이스를 내보냅니다.
   
    hello 소스 파일은 tutorials/usesqoop/data/sample.log입니다. hello 데이터를 내보낸된 toois hello 테이블 log4jlogs를 호출 됩니다.
   
   > [!NOTE]
   > 연결 문자열 정보를 이외의 SQL Server 또는 Azure SQL 데이터베이스에 대 한이 섹션의 단계 hello 작동 해야 합니다. 다음이 단계를 같은 구성이 hello를 사용 하 여 테스트 합니다.
   > 
   > * **Azure 가상 네트워크 지점-사이트 구성**: 가상 네트워크 hello HDInsight 클러스터 tooa SQL Server 개인 데이터 센터에 연결 합니다. 참조 [hello 관리 포털에서에서 지점 및 사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-point-to-site-create.md) 자세한 정보에 대 한 합니다.
   > * **Azure HDInsight 3.1**: 가상 네트워크에서 클러스터를 만드는 방법에 대한 자세한 내용은 [사용자 지정 옵션을 사용하여 HDInsight의 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md) 를 참조하세요.
   > * **SQL Server 2014**: tooallow 인증 및 실행 중인 hello VPN 클라이언트 구성 패키지 tooconnect를 안전 하 게 구성 toohello 가상 네트워크입니다.
   > 
   > 
7. 하이브 테이블 toohello Azure SQL 데이터베이스를 내보냅니다.
8. Hello mobiledata 테이블 toohello HDInsight 클러스터를 가져옵니다.
   
    tooexamine hello 수정 된 데이터 파일을 hello Azure 포털, Azure 저장소 탐색기 도구를 사용 하는 또는 Azure PowerShell을 사용할 수 있습니다.  [HDInsight 시작] [ hdinsight-get-started] 코드는 Azure PowerShell toodownload 파일 사용에 대 한 샘플링 하 여 hello 파일 콘텐츠를 표시 합니다.

### <a name="hello-powershell-sample"></a>hello PowerShell 샘플
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

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
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
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

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
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

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
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
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

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
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
