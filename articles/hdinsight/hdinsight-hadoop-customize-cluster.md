---
title: "aaaCustomize HDInsight 클러스터를 사용 하 여 스크립트 작업을-Azure | Microsoft Docs"
description: "Toocustomize HDInsight 클러스터 스크립트 작업을 사용 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="af039-103">스크립트 작업을 사용하여 Windows 기반 HDInsight 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="af039-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="af039-104">**작업 스크립트** tooinvoke 사용된 될 수 있습니다 [사용자 지정 스크립트](hdinsight-hadoop-script-actions.md) 클러스터에 추가 소프트웨어를 설치 하기 위한 hello 클러스터 만들기 프로세스 중입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="af039-105">이 문서의 hello 정보에는 특정 tooWindows 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="af039-106">Linux 기반 클러스터는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af039-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="af039-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="af039-109">Azure 저장소 계정 추가 포함 하 여 같은 다양 한 다른 방법으로,도 지정할 수 있습니다 HDInsight 클러스터, 구성 파일 (코어 site.xml, hive-site.xml 등)을, Hadoop hello를 변경 하거나 (예: 하이브, Oozie) 라이브러리에 공유 추가 hello 클러스터의 공용 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="af039-110">이러한 사용자 지정 Azure HDInsight.NET SDK hello Azure PowerShell을 통해 수행할 수 있습니다 또는 Azure 포털을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="af039-111">자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision-cluster]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="af039-112">Hello 클러스터 만들기 프로세스에 스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="af039-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="af039-113">스크립트 동작 클러스터를 만들려는의 hello 프로세스 중인 동안에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af039-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="af039-114">hello 다음 다이어그램에서는 hello 만드는 프로세스 동안 스크립트 작업을 실행할 때 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="af039-115">![HDInsight 클러스터 사용자 지정 및 클러스터 만드는 동안의 단계][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="af039-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="af039-116">Hello 스크립트가 실행 되 고 hello 클러스터 hello 입력 **ClusterCustomization** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="af039-117">이 단계에서는 hello 스크립트 hello 시스템 관리자 계정에서 실행, 모든 hello에 동시에 지정 된 hello 클러스터의 노드 및 hello 노드에서 모든 관리자 권한을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="af039-118">동안 hello 클러스터 노드에 대 한 관리자 권한이 있으므로 **ClusterCustomization** 단계 Hadoop 관련 서비스를 포함 한 서비스를 시작 및 중지와 같은 hello 스크립트 tooperform 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="af039-119">Hello 스크립트의 일부로 확인 해야 하므로 해당 hello Ambari 서비스 및 다른 Hadoop 관련 서비스는 실행 되 고 hello 스크립트 실행이 완료 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="af039-120">이러한 서비스는 필요한 생성 되는 동안 toosuccessfully hello 상태 및 hello 클러스터의 상태 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="af039-121">이러한 서비스에 영향을 주는 클러스터에서 모든 구성을 변경 하면 제공 하는 hello 도우미 함수를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="af039-122">도우미 함수에 대한 자세한 내용은 [HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="af039-123">hello 출력 및 오류 로그를 hello hello 스크립트 hello 클러스터에 대해 지정 하는 hello 기본 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af039-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="af039-124">hello 로그 테이블에 저장 됩니다는 hello 이름의 **u < \cluster-name-fragment >< \time-stamp > setuplog**합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="af039-125">이들은 hello 클러스터의 모든 hello 노드 (작업자 노드 및 헤드 노드)에서 실행 하는 hello 스크립트에서 로그를 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="af039-126">각 클러스터는 지정 된 hello 순서 대로 호출 되는 여러 스크립트 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="af039-127">스크립트는 hello 헤드 노드, hello 작업자 노드 중 하나 또는 둘 다 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="af039-128">HDInsight는 HDInsight 클러스터에서 다음과 같은 구성 요소가 여러 스크립트 tooinstall hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="af039-129">이름</span><span class="sxs-lookup"><span data-stu-id="af039-129">Name</span></span> | <span data-ttu-id="af039-130">스크립트</span><span class="sxs-lookup"><span data-stu-id="af039-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="af039-131">**Spark 설치**</span><span class="sxs-lookup"><span data-stu-id="af039-131">**Install Spark**</span></span> |<span data-ttu-id="af039-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="af039-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="af039-133">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="af039-134">**R 설치**</span><span class="sxs-lookup"><span data-stu-id="af039-134">**Install R**</span></span> |<span data-ttu-id="af039-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="af039-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="af039-136">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="af039-137">**Solr 설치**</span><span class="sxs-lookup"><span data-stu-id="af039-137">**Install Solr**</span></span> |<span data-ttu-id="af039-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="af039-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="af039-139">[HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="af039-140">- **Giraph 설치**</span><span class="sxs-lookup"><span data-stu-id="af039-140">- **Install Giraph**</span></span> |<span data-ttu-id="af039-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="af039-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="af039-142">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="af039-143">**Hive 라이브러리 사전 로드**</span><span class="sxs-lookup"><span data-stu-id="af039-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="af039-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="af039-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="af039-145">[HDInsight 클러스터에서 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="af039-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="af039-146">Hello Azure 포털을 사용 하 여 스크립트를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="af039-147">**Hello Azure 포털에서**</span><span class="sxs-lookup"><span data-stu-id="af039-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="af039-148">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="af039-149">Hello에 대 한 선택적 구성에서 **스크립트 동작** 블레이드에서 클릭 **스크립트 동작 추가** 아래와 같이 tooprovide hello 스크립트 동작에 대 한 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="af039-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="af039-150">![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")</span><span class="sxs-lookup"><span data-stu-id="af039-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="af039-151">속성</span><span class="sxs-lookup"><span data-stu-id="af039-151">Property</span></span></th><th><span data-ttu-id="af039-152">값</span><span class="sxs-lookup"><span data-stu-id="af039-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="af039-153">이름</span><span class="sxs-lookup"><span data-stu-id="af039-153">Name</span></span></td>
            <td><span data-ttu-id="af039-154">Hello 스크립트 동작에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="af039-155">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="af039-155">Script URI</span></span></td>
            <td><span data-ttu-id="af039-156">가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="af039-157">s</span><span class="sxs-lookup"><span data-stu-id="af039-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="af039-158">헤드/작업자</span><span class="sxs-lookup"><span data-stu-id="af039-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="af039-159">Hello 노드를 지정 (**h e a d** 또는 **작업자**) hello 사용자 정의 스크립트 실행.</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="af039-160">매개 변수</span><span class="sxs-lookup"><span data-stu-id="af039-160">Parameters</span></span></td>
            <td><span data-ttu-id="af039-161">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="af039-162">하나의 스크립트 동작 tooinstall 이상 ENTER tooadd 여러 구성 요소를 눌러 hello 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="af039-163">클릭 **선택** toosave hello 스크립트 작업 구성 및 클러스터 만들기를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="af039-164">Azure PowerShell을 사용하여 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="af039-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="af039-165">이 다음 PowerShell 스크립트는 Windows에서 Spark tooinstall HDInsight 클러스터를 기반 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af039-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
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

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
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


<span data-ttu-id="af039-166">tooinstall 기타 소프트웨어 해야 hello 스크립트에서 tooreplace hello 스크립트 파일:</span><span class="sxs-lookup"><span data-stu-id="af039-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="af039-167">메시지가 표시 되 면 hello 클러스터에 대 한 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="af039-168">Hello 클러스터를 만들기 전에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="af039-169">.NET SDK를 사용하여 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="af039-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="af039-170">hello 다음 예제에서는 Windows에서 Spark tooinstall HDInsight 클러스터를 기반 하는 방법</span><span class="sxs-lookup"><span data-stu-id="af039-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="af039-171">tooinstall 기타 소프트웨어 해야 hello 코드 tooreplace hello 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="af039-172">**toocreate Spark와 함께 하는 HDInsight 클러스터**</span><span class="sxs-lookup"><span data-stu-id="af039-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="af039-173">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af039-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="af039-174">Nuget 패키지 관리자 콘솔 hello hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="af039-175">문을 사용 하 여 hello Program.cs 파일에 다음 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="af039-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="af039-176">Hello 다음을 사용 하 여 hello 클래스에 hello 코드를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
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
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="af039-177">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="af039-178">HDInsight 클러스터에서 사용하는 오픈 소스 소프트웨어 지원</span><span class="sxs-lookup"><span data-stu-id="af039-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="af039-179">Microsoft Azure HDInsight 서비스 hello Hadoop 주위 형성 하는 오픈 소스 기술 프로그램 에코 시스템을 사용 하 여 hello 클라우드에서 toobuild 빅 데이터 응용 프로그램 수 있도록 하는 유연한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="af039-180">Microsoft Azure hello에 설명 된 대로 오픈 소스 기술에 대 한 일반 수준의 지원 제공 **지원 범위** hello 섹션 <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure 지원 FAQ 웹 사이트</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="af039-181">hello HDInsight 서비스 아래 설명 된 대로 추가 수준의 hello 구성 요소 중 일부에 대 한 지원 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="af039-182">Hello HDInsight 서비스에서에서 사용할 수 있는 오픈 소스 구성 요소는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="af039-183">**기본 제공 구성 요소** -이 구성 요소는 HDInsight 클러스터에 미리 설치 되어 하며 hello 클러스터의 핵심 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="af039-184">예를 들어 YARN ResourceManager, hello 하이브 쿼리 언어 (HiveQL) 및 hello Mahout 라이브러리 toothis 범주에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="af039-185">클러스터 구성 요소 전체 목록은 영어로 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="af039-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="af039-186">**사용자 지정 구성 요소** -, hello 클러스터의 사용자로 설치 또는 hello 커뮤니티에서 사용할 수 있거나 사용자가 만든 모든 구성 요소를 작업에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="af039-187">기본 제공 구성 요소가 완전 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="af039-188">Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="af039-189">사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="af039-190">이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="af039-191">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. 또한 Apache 프로젝트에는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="af039-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="af039-192">HDInsight 서비스 hello toouse 사용자 지정 구성 요소를 여러 가지 방법으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="af039-193">어떻게 구성 요소가 사용 되거나 hello 클러스터에 설치에 관계 없이 hello 동일한 지원 수준으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af039-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="af039-194">다음은 HDInsight 클러스터에서 사용자 지정 구성 요소를 사용할 수 있도록 하는 hello 가장 일반적인 방법의 목록이입니다.</span><span class="sxs-lookup"><span data-stu-id="af039-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="af039-195">작업 제출-Hadoop 또는 기타 유형의 작업을 실행 하거나 사용자 지정 구성 요소를 사용 하 여 제출 된 toohello 클러스터가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="af039-196">클러스터를 만드는 동안 클러스터 사용자 지정-추가 설정과 hello 클러스터 노드에 설치 될 사용자 지정 구성 요소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="af039-197">샘플-인기 있는 사용자 지정 구성 요소, Microsoft 등에 대 한 예제는 hello HDInsight 클러스터에서 이러한 구성 요소를 사용할 수 있는 방법을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af039-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="af039-198">이러한 샘플은 지원 없이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="af039-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="af039-199">스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="af039-199">Develop Script Action scripts</span></span>
<span data-ttu-id="af039-200">[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af039-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="af039-201">참고 항목</span><span class="sxs-lookup"><span data-stu-id="af039-201">See also</span></span>
* <span data-ttu-id="af039-202">[HDInsight에서 Hadoop 클러스터를 만들어] [ hdinsight-provision-cluster] 다른 사용자 지정 옵션을 사용 하 여 toocreate HDInsight 클러스터 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af039-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="af039-203">[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="af039-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="af039-204">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="af039-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="af039-205">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="af039-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="af039-206">[HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="af039-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="af039-207">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)</span><span class="sxs-lookup"><span data-stu-id="af039-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"
