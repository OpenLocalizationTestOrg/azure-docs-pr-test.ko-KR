---
title: "부트스트랩-Azure를 사용 하 여 HDInsight 클러스터 aaaCustomize | Microsoft Docs"
description: "Toocustomize HDInsight 클러스터 부트스트랩을 사용 하 여 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a>부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정

포함 하는 tooconfigure hello 구성 파일을 원하는 경우에 따라:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

부트스트랩는 세 가지 메서드 toouse 있습니다.

* Azure PowerShell 사용
* .NET SDK 사용
* Azure Resource Manager 템플릿 사용

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Hello 만든 시간 동안 HDInsight 클러스터에 추가 구성 요소 설치에 대 한 내용은 다음을 참조 합니다.

* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정(Linux)](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a>Azure PowerShell 사용
다음 PowerShell 코드 hello 하이브 구성 사용자 지정 합니다.

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

완전히 작동하는 PowerShell 스크립트는 [부록 A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)에서 찾을 수 있습니다.

**tooverify hello 변경 사항:**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**합니다. 표시되지 않으면 먼저 **추가 서비스**를 클릭합니다.
3. Hello PowerShell 스크립트를 사용 하 여 방금 만든 hello 클러스터를 클릭 합니다.
4. 클릭 **대시보드** hello 블레이드 tooopen의 hello 위에서 hello Ambari UI입니다.
5. 클릭 **하이브** hello 왼쪽된 메뉴에서 합니다.
6. **요약**에서 **HiveServer2**를 클릭합니다.
7. Hello 클릭 **Configs** 탭 합니다.
8. 클릭 **하이브** hello 왼쪽된 메뉴에서 합니다.
9. Hello 클릭 **고급** 탭 합니다.
10. 아래로 스크롤한 다음 **고급 hive 사이트**를 확장합니다.
11. 검색할 **hive.metastore.client.socket.timeout** hello 섹션에 있습니다.

다른 구성 파일을 사용자 지정하는 추가 샘플:

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

자세한 내용은 Azim Uddin의 [HDInsight 클러스터 만들기 사용자 지정](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)블로그를 참조하세요.

## <a name="use-net-sdk"></a>.NET SDK 사용
참조 [사용 하 여 HDInsight 클러스터 만들기 Linux 기반 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap)합니다.

## <a name="use-resource-manager-template"></a>Resource Manager 템플릿 사용
Resource Manager 템플릿에서 부트스트랩을 사용할 수 있습니다.

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop 사용자 지정 클러스터 부트스트랩 Azure Resource Manager 템플릿](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a>참고 항목
* [HDInsight에서 Hadoop 클러스터를 만들어] [ hdinsight-provision-cluster] 다른 사용자 지정 옵션을 사용 하 여 toocreate HDInsight 클러스터 하는 방법에 대해 설명 합니다.
* [HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]
* [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]
* [HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]
* [HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)
* [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"

## <a name="appx-a-powershell-sample"></a>부록 A: PowerShell 샘플
이 PowerShell 스크립트는 HDInsight 클러스터를 만들고 Hive 설정을 사용자 지정합니다.

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
