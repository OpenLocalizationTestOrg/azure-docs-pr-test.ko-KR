---
title: "스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정 - Azure | Microsoft Docs"
description: "스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="51e7d-103">스크립트 작업을 사용하여 Windows 기반 HDInsight 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="51e7d-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="51e7d-104">**스크립트 동작** 은 클러스터 생성 과정 중 클러스터에 추가 소프트웨어를 설치하기 위해 [사용자 지정 스크립트](hdinsight-hadoop-script-actions.md) 를 호출하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="51e7d-105">이 문서에 있는 정보는 Windows 기반 HDInsight 클러스터에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="51e7d-106">Linux 기반 클러스터는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51e7d-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="51e7d-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="51e7d-109">HDInsight 클러스터를 사용자 지정하는 방법은 추가 Azure 저장소 계정 포함, hadoop 구성 파일(core-site.xml, hive-site.xml 등) 변경, 클러스터의 공통 위치에 공유 라이브러리(예: Hive, Oozie) 추가 등을 비롯해 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="51e7d-110">이러한 사용자 지정은 Azure PowerShell, Azure HDInsight .NET SDK 또는 Azure Portal을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="51e7d-111">자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision-cluster]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="51e7d-112">클러스터 만들기 프로세스의 스크립트 작업</span><span class="sxs-lookup"><span data-stu-id="51e7d-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="51e7d-113">스크립트 작업은 클러스터를 만드는 프로세스 동안에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="51e7d-114">다음 다이어그램에서는 만들기 프로세스 중 스크립트 작업을 실행할 때를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="51e7d-115">![HDInsight 클러스터 사용자 지정 및 클러스터 만드는 동안의 단계][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="51e7d-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="51e7d-116">스크립트가 실행 중이면 클러스터의 **Cluster 사용자 지정** 단계가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="51e7d-117">이 단계에서 스크립트는 시스템 관리자 계정으로 클러스터의 지정된 모든 노드에서 병렬로 실행되며 해당 노드에서 모든 관리자 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="51e7d-118">**Cluster 사용자 지정** 단계 중 클러스터 노드에 대한 관리 권한이 있으므로 스크립트를 사용하여 Hadoop 관련 서비스를 비롯한 서비스의 중지 및 시작과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="51e7d-119">따라서 스크립트의 일부로 스크립트 실행이 완료되기 전에 Ambari 서비스 및 기타 Hadoop 관련 서비스가 실행 중인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="51e7d-120">클러스터가 생성되는 동안 클러스터의 상태를 확인하려면 이러한 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="51e7d-121">클러스터에서 이러한 서비스에 영향을 주는 구성을 변경하는 경우 제공되는 도우미 함수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="51e7d-122">도우미 함수에 대한 자세한 내용은 [HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="51e7d-123">스크립트의 출력 및 오류 로그는 클러스터에 대해 지정한 기본 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="51e7d-124">오류는 **u<\cluster-name-fragment><\time-stamp>setuplog**라는 이름으로 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="51e7d-125">클러스터의 모든 노드(헤드 노드 및 작업자 노드)에서 실행된 스크립트의 집계 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="51e7d-126">각 클러스터에서는 지정된 순서대로 호출되는 여러 스크립트 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="51e7d-127">스크립트를 헤드 노드, 작업자 노드 또는 두 노드 모두에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="51e7d-128">HDInsight는 HDInsight 클러스터에서 다음 구성 요소를 설치하는 여러 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="51e7d-129">이름</span><span class="sxs-lookup"><span data-stu-id="51e7d-129">Name</span></span> | <span data-ttu-id="51e7d-130">스크립트</span><span class="sxs-lookup"><span data-stu-id="51e7d-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="51e7d-131">**Spark 설치**</span><span class="sxs-lookup"><span data-stu-id="51e7d-131">**Install Spark**</span></span> |<span data-ttu-id="51e7d-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="51e7d-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="51e7d-133">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="51e7d-134">**R 설치**</span><span class="sxs-lookup"><span data-stu-id="51e7d-134">**Install R**</span></span> |<span data-ttu-id="51e7d-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="51e7d-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="51e7d-136">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="51e7d-137">**Solr 설치**</span><span class="sxs-lookup"><span data-stu-id="51e7d-137">**Install Solr**</span></span> |<span data-ttu-id="51e7d-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="51e7d-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="51e7d-139">[HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="51e7d-140">- **Giraph 설치**</span><span class="sxs-lookup"><span data-stu-id="51e7d-140">- **Install Giraph**</span></span> |<span data-ttu-id="51e7d-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="51e7d-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="51e7d-142">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="51e7d-143">**Hive 라이브러리 사전 로드**</span><span class="sxs-lookup"><span data-stu-id="51e7d-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="51e7d-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="51e7d-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="51e7d-145">[HDInsight 클러스터에서 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="51e7d-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="51e7d-146">Azure Portal을 사용하여 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="51e7d-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="51e7d-147">**Azure Portal에서**</span><span class="sxs-lookup"><span data-stu-id="51e7d-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="51e7d-148">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="51e7d-149">[선택적 구성]의 **스크립트 동작** 블레이드에서 **스크립트 동작 추가**를 클릭하여 아래와 같이 스크립트 동작에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="51e7d-150">![스크립트 작업을 사용하여 클러스터 사용자 지정](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "스크립트 작업을 사용하여 클러스터 사용자 지정")</span><span class="sxs-lookup"><span data-stu-id="51e7d-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="51e7d-151">속성</span><span class="sxs-lookup"><span data-stu-id="51e7d-151">Property</span></span></th><th><span data-ttu-id="51e7d-152">값</span><span class="sxs-lookup"><span data-stu-id="51e7d-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="51e7d-153">이름</span><span class="sxs-lookup"><span data-stu-id="51e7d-153">Name</span></span></td>
            <td><span data-ttu-id="51e7d-154">스크립트 작업의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="51e7d-155">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="51e7d-155">Script URI</span></span></td>
            <td><span data-ttu-id="51e7d-156">클러스터를 사용자 지정하기 위해 호출되는 스크립트에 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="51e7d-157">s</span><span class="sxs-lookup"><span data-stu-id="51e7d-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="51e7d-158">헤드/작업자</span><span class="sxs-lookup"><span data-stu-id="51e7d-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="51e7d-159">사용자 지정 스크립트가 실행되는 노드(**헤드** 또는 **작업자**)를 지정합니다.</b></span><span class="sxs-lookup"><span data-stu-id="51e7d-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="51e7d-160">매개 변수</span><span class="sxs-lookup"><span data-stu-id="51e7d-160">Parameters</span></span></td>
            <td><span data-ttu-id="51e7d-161">스크립트에 필요한 경우 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="51e7d-162">ENTER 키를 누르고 두 개 이상의 스크립트 작업을 추가하여 클러스터에 여러 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="51e7d-163">**선택** 을 클릭하여 스크립트 작업 구성을 저장하고 계속 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="51e7d-164">Azure PowerShell을 사용하여 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="51e7d-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="51e7d-165">이 다음 PowerShell 스크립트는 Windows 기반 HDInsight 클러스터에 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="51e7d-166">다른 소프트웨어를 설치하려면 스크립트에서 스크립트 파일을 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="51e7d-167">메시지가 나타나면 클러스터에 대한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="51e7d-168">클러스터가 생성되는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="51e7d-169">.NET SDK를 사용하여 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="51e7d-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="51e7d-170">다음 샘플은 Windows 기반 HDInsight 클러스터에서 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="51e7d-171">다른 소프트웨어를 설치하려면 코드에서 스크립트 파일을 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="51e7d-172">**Spark로 HDInsight 클러스터를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="51e7d-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="51e7d-173">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="51e7d-174">NuGet 패키지 관리자 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="51e7d-175">Program.cs 파일에서 다음 using 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="51e7d-176">클래스의 코드를 다음과 같이 둡니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="51e7d-177">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="51e7d-178">HDInsight 클러스터에서 사용하는 오픈 소스 소프트웨어 지원</span><span class="sxs-lookup"><span data-stu-id="51e7d-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="51e7d-179">Microsoft Azure HDInsight 서비스는 Hadoop에 형성된 오픈 소스 기술의 에코시스템을 사용하여 클라우드에 빅 데이터 응용 프로그램을 빌드할 수 있는 유연한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="51e7d-180">Microsoft Azure에서는 **Azure 지원 FAQ 웹 사이트** 의 <a href="http://azure.microsoft.com/support/faq/" target="_blank">지원 범위</a>섹션에 설명된 대로 일반적인 수준의 오픈 소스 기술을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="51e7d-181">HDInsight 서비스는 아래에 설명된 일부 구성 요소에 대해 추가 수준의 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="51e7d-182">HDInsight 서비스에서 사용할 수 있는 오픈 소스 구성 요소에는 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="51e7d-183">**기본 제공 구성 요소** - 이러한 구성 요소는 HDInsight 클러스터에 미리 설치 되어 있으며 클러스터의 핵심 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="51e7d-184">예를 들어, YARN ResourceManager, Hive 쿼리 언어(HiveQL) 및 Mahout 라이브러리는 이 범주에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="51e7d-185">클러스터 구성 요소의 전체 목록은 [HDInsight에서 제공하는 Hadoop 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)에 있습니다</a>.</span><span class="sxs-lookup"><span data-stu-id="51e7d-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="51e7d-186">**사용자 지정 구성 요소** - 클러스터의 사용자로서 사용자는 커뮤니티에서 사용 가능한 모든 구성 요소 또는 사용자가 만든 구성 요소를 작업에 설치하거나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="51e7d-187">기본 제공 구성 요소는 완전히 지원되며, Microsoft 지원에서 이러한 구성 요소와 관련된 문제를 해결하는 데 도움을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="51e7d-188">HDInsight 클러스터와 함께 제공된 구성 요소는 완전히 지원되며 Microsoft 지원에서 이러한 구성 요소와 관련된 문제를 해결하는 데 도움을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="51e7d-189">사용자 지정 구성 요소는 문제 해결에 도움이 되는 합리적인 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="51e7d-190">지원을 통해 문제를 해결하거나 해당 기술에 대한 전문 지식이 있는, 오픈 소스 기술에 대해 사용 가능한 채널에 참여하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="51e7d-191">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="51e7d-192">또한 Apache 프로젝트에는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="51e7d-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="51e7d-193">HDInsight 서비스는 사용자 지정 구성 요소를 사용하는 여러 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="51e7d-194">구성 요소가 클러스터에 설치되고 사용되는 방법과 상관없이, 동일한 수준의 지원이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="51e7d-195">다음은 HDInsight 클러스터에서 사용자 지정 구성 요소를 사용할 수 있는 가장 일반적인 방법의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="51e7d-196">작업 제출 - 사용자 지정 구성 요소를 실행하거나 사용하는 Hadoop 또는 기타 유형의 작업을 클러스터에 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="51e7d-197">클러스터 사용자 지정 - 클러스터를 만들 때 클러스터 노드에 설치되는 사용자 지정 구성 요소 및 추가 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="51e7d-198">샘플 - 인기 있는 사용자 지정 구성 요소의 경우, Microsoft와 다른 사람들이 이러한 구성 요소를 HDInsight 클러스터에서 어떻게 사용할 수 있는지에 대한 샘플을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="51e7d-199">이러한 샘플은 지원 없이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="51e7d-200">스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="51e7d-200">Develop Script Action scripts</span></span>
<span data-ttu-id="51e7d-201">[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51e7d-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="51e7d-202">참고 항목</span><span class="sxs-lookup"><span data-stu-id="51e7d-202">See also</span></span>
* <span data-ttu-id="51e7d-203">[HDInsight의 Hadoop 클러스터 만들기][hdinsight-provision-cluster]에서는 다른 사용자 지정 옵션을 사용하여 HDInsight 클러스터를 만드는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e7d-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="51e7d-204">[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="51e7d-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="51e7d-205">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="51e7d-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="51e7d-206">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="51e7d-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="51e7d-207">[HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="51e7d-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="51e7d-208">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)</span><span class="sxs-lookup"><span data-stu-id="51e7d-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="51e7d-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"</span><span class="sxs-lookup"><span data-stu-id="51e7d-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
