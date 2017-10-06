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
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="316ea-103">부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="316ea-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="316ea-104">포함 하는 tooconfigure hello 구성 파일을 원하는 경우에 따라:</span><span class="sxs-lookup"><span data-stu-id="316ea-104">Sometimes, you want tooconfigure hello configuration files, which include:</span></span>

* <span data-ttu-id="316ea-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="316ea-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-106">core-site.xml</span></span>
* <span data-ttu-id="316ea-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-107">gateway.xml</span></span>
* <span data-ttu-id="316ea-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-108">hbase-env.xml</span></span>
* <span data-ttu-id="316ea-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-109">hbase-site.xml</span></span>
* <span data-ttu-id="316ea-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-110">hdfs-site.xml</span></span>
* <span data-ttu-id="316ea-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-111">hive-env.xml</span></span>
* <span data-ttu-id="316ea-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-112">hive-site.xml</span></span>
* <span data-ttu-id="316ea-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="316ea-113">mapred-site</span></span>
* <span data-ttu-id="316ea-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-114">oozie-site.xml</span></span>
* <span data-ttu-id="316ea-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-115">oozie-env.xml</span></span>
* <span data-ttu-id="316ea-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-116">storm-site.xml</span></span>
* <span data-ttu-id="316ea-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-117">tez-site.xml</span></span>
* <span data-ttu-id="316ea-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-118">webhcat-site.xml</span></span>
* <span data-ttu-id="316ea-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="316ea-119">yarn-site.xml</span></span>

<span data-ttu-id="316ea-120">부트스트랩는 세 가지 메서드 toouse 있습니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-120">There are three methods toouse bootstrap:</span></span>

* <span data-ttu-id="316ea-121">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="316ea-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="316ea-122">.NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="316ea-122">Use .NET SDK</span></span>
* <span data-ttu-id="316ea-123">Azure Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="316ea-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="316ea-124">Hello 만든 시간 동안 HDInsight 클러스터에 추가 구성 요소 설치에 대 한 내용은 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-124">For information on installing additional components on HDInsight cluster during hello creation time, see:</span></span>

* [<span data-ttu-id="316ea-125">스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정(Linux)</span><span class="sxs-lookup"><span data-stu-id="316ea-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="316ea-126">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="316ea-126">Use Azure PowerShell</span></span>
<span data-ttu-id="316ea-127">다음 PowerShell 코드 hello 하이브 구성 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-127">hello following PowerShell code customizes a Hive configuration:</span></span>

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

<span data-ttu-id="316ea-128">완전히 작동하는 PowerShell 스크립트는 [부록 A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="316ea-129">**tooverify hello 변경 사항:**</span><span class="sxs-lookup"><span data-stu-id="316ea-129">**tooverify hello change:**</span></span>

1. <span data-ttu-id="316ea-130">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-130">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="316ea-131">Hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-131">From hello left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="316ea-132">표시되지 않으면 먼저 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="316ea-133">Hello PowerShell 스크립트를 사용 하 여 방금 만든 hello 클러스터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-133">Click hello cluster you just created using hello PowerShell script.</span></span>
4. <span data-ttu-id="316ea-134">클릭 **대시보드** hello 블레이드 tooopen의 hello 위에서 hello Ambari UI입니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-134">Click **Dashboard** from hello top of hello blade tooopen hello Ambari UI.</span></span>
5. <span data-ttu-id="316ea-135">클릭 **하이브** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-135">Click **Hive** from hello left menu.</span></span>
6. <span data-ttu-id="316ea-136">**요약**에서 **HiveServer2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="316ea-137">Hello 클릭 **Configs** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-137">Click hello **Configs** tab.</span></span>
8. <span data-ttu-id="316ea-138">클릭 **하이브** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-138">Click **Hive** from hello left menu.</span></span>
9. <span data-ttu-id="316ea-139">Hello 클릭 **고급** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-139">Click hello **Advanced** tab.</span></span>
10. <span data-ttu-id="316ea-140">아래로 스크롤한 다음 **고급 hive 사이트**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="316ea-141">검색할 **hive.metastore.client.socket.timeout** hello 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-141">Look for **hive.metastore.client.socket.timeout** in hello section.</span></span>

<span data-ttu-id="316ea-142">다른 구성 파일을 사용자 지정하는 추가 샘플:</span><span class="sxs-lookup"><span data-stu-id="316ea-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="316ea-143">자세한 내용은 Azim Uddin의 [HDInsight 클러스터 만들기 사용자 지정](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)블로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="316ea-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="316ea-144">.NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="316ea-144">Use .NET SDK</span></span>
<span data-ttu-id="316ea-145">참조 [사용 하 여 HDInsight 클러스터 만들기 Linux 기반 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap)합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-145">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="316ea-146">Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="316ea-146">Use Resource Manager template</span></span>
<span data-ttu-id="316ea-147">Resource Manager 템플릿에서 부트스트랩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop 사용자 지정 클러스터 부트스트랩 Azure Resource Manager 템플릿](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="316ea-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="316ea-149">See also</span></span>
* <span data-ttu-id="316ea-150">[HDInsight에서 Hadoop 클러스터를 만들어] [ hdinsight-provision-cluster] 다른 사용자 지정 옵션을 사용 하 여 toocreate HDInsight 클러스터 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="316ea-151">[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="316ea-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="316ea-152">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="316ea-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="316ea-153">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="316ea-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="316ea-154">[HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="316ea-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="316ea-155">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)</span><span class="sxs-lookup"><span data-stu-id="316ea-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="316ea-157">부록 A: PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="316ea-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="316ea-158">이 PowerShell 스크립트는 HDInsight 클러스터를 만들고 Hive 설정을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="316ea-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

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
