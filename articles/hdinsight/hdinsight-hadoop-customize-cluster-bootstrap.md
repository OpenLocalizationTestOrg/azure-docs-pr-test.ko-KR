---
title: "부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정 - Azure | Microsoft Docs"
description: "부트스트랩을 사용하여 HDInsight 클러스터를 사용자 지정하는 방법을 알아봅니다."
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
ms.openlocfilehash: c7a6fafa90eac66774d564c82c926c662baf784c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="46307-103">부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="46307-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="46307-104">경우에 따라 다음과 같이 구성 파일을 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46307-104">Sometimes, you want to configure the configuration files, which include:</span></span>

* <span data-ttu-id="46307-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="46307-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="46307-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-106">core-site.xml</span></span>
* <span data-ttu-id="46307-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="46307-107">gateway.xml</span></span>
* <span data-ttu-id="46307-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="46307-108">hbase-env.xml</span></span>
* <span data-ttu-id="46307-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-109">hbase-site.xml</span></span>
* <span data-ttu-id="46307-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-110">hdfs-site.xml</span></span>
* <span data-ttu-id="46307-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="46307-111">hive-env.xml</span></span>
* <span data-ttu-id="46307-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-112">hive-site.xml</span></span>
* <span data-ttu-id="46307-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="46307-113">mapred-site</span></span>
* <span data-ttu-id="46307-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-114">oozie-site.xml</span></span>
* <span data-ttu-id="46307-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="46307-115">oozie-env.xml</span></span>
* <span data-ttu-id="46307-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-116">storm-site.xml</span></span>
* <span data-ttu-id="46307-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-117">tez-site.xml</span></span>
* <span data-ttu-id="46307-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-118">webhcat-site.xml</span></span>
* <span data-ttu-id="46307-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="46307-119">yarn-site.xml</span></span>

<span data-ttu-id="46307-120">Bootstrap을 사용하는 방법은 3가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46307-120">There are three methods to use bootstrap:</span></span>

* <span data-ttu-id="46307-121">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="46307-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="46307-122">.NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="46307-122">Use .NET SDK</span></span>
* <span data-ttu-id="46307-123">Azure Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="46307-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="46307-124">만든 시간 동안 HDInsight 클러스터에 추가 구성 요소 설치에 대한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46307-124">For information on installing additional components on HDInsight cluster during the creation time, see:</span></span>

* [<span data-ttu-id="46307-125">스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정(Linux)</span><span class="sxs-lookup"><span data-stu-id="46307-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="46307-126">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="46307-126">Use Azure PowerShell</span></span>
<span data-ttu-id="46307-127">다음 PowerShell 코드는 Hive 구성을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-127">The following PowerShell code customizes a Hive configuration:</span></span>

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

<span data-ttu-id="46307-128">완전히 작동하는 PowerShell 스크립트는 [부록 A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46307-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="46307-129">**변경을 확인하려면:**</span><span class="sxs-lookup"><span data-stu-id="46307-129">**To verify the change:**</span></span>

1. <span data-ttu-id="46307-130">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-130">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="46307-131">왼쪽 메뉴에서 **HDInsight 클러스터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-131">From the left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="46307-132">표시되지 않으면 먼저 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="46307-133">PowerShell 스크립트를 사용하여 방금 만든 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-133">Click the cluster you just created using the PowerShell script.</span></span>
4. <span data-ttu-id="46307-134">블레이드 맨 위에서 **대시보드** 를 클릭하여 Ambari UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46307-134">Click **Dashboard** from the top of the blade to open the Ambari UI.</span></span>
5. <span data-ttu-id="46307-135">왼쪽 메뉴에서 **Hive** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-135">Click **Hive** from the left menu.</span></span>
6. <span data-ttu-id="46307-136">**요약**에서 **HiveServer2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="46307-137">**Configs** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-137">Click the **Configs** tab.</span></span>
8. <span data-ttu-id="46307-138">왼쪽 메뉴에서 **Hive** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-138">Click **Hive** from the left menu.</span></span>
9. <span data-ttu-id="46307-139">**고급** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-139">Click the **Advanced** tab.</span></span>
10. <span data-ttu-id="46307-140">아래로 스크롤한 다음 **고급 hive 사이트**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="46307-141">섹션에서 **hive.metastore.client.socket.timeout** 을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="46307-141">Look for **hive.metastore.client.socket.timeout** in the section.</span></span>

<span data-ttu-id="46307-142">다른 구성 파일을 사용자 지정하는 추가 샘플:</span><span class="sxs-lookup"><span data-stu-id="46307-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="46307-143">자세한 내용은 Azim Uddin의 [HDInsight 클러스터 만들기 사용자 지정](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)블로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46307-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="46307-144">.NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="46307-144">Use .NET SDK</span></span>
<span data-ttu-id="46307-145">[.NET SDK를 사용하여 HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46307-145">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="46307-146">Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="46307-146">Use Resource Manager template</span></span>
<span data-ttu-id="46307-147">Resource Manager 템플릿에서 부트스트랩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46307-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop 사용자 지정 클러스터 부트스트랩 Azure Resource Manager 템플릿](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="46307-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="46307-149">See also</span></span>
* <span data-ttu-id="46307-150">[HDInsight의 Hadoop 클러스터 만들기][hdinsight-provision-cluster]에서는 다른 사용자 지정 옵션을 사용하여 HDInsight 클러스터를 만드는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="46307-151">[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="46307-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="46307-152">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="46307-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="46307-153">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="46307-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="46307-154">[HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="46307-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="46307-155">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)</span><span class="sxs-lookup"><span data-stu-id="46307-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="46307-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"</span><span class="sxs-lookup"><span data-stu-id="46307-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="46307-157">부록 A: PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="46307-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="46307-158">이 PowerShell 스크립트는 HDInsight 클러스터를 만들고 Hive 설정을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="46307-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

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
    # Connect to Azure
    ####################################
    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

    Write-Host "Creating the default storage account and default blob container ..."  -ForegroundColor Green
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
        -Context $defaultStorageContext #use the cluster name as the container name

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
    # Verify the cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
