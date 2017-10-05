---
title: "HDInsight의 Hadoop 클러스터에 Giraph 설치 및 사용 - Azure | Microsoft Docs"
description: "Giraph를 사용하여 HDInsight 클러스터를 사용자 지정하는 방법 및 Giraph를 사용하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="70fe9-103">Windows 기반 HDInsight 클러스터에서 Giraph 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="70fe9-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="70fe9-104">스크립트 동작을 사용하여 Giraph로 Windows 기반 HDInsight 클러스터를 사용자 지정하는 방법 및 대규모 그래프를 처리하기 위해 Giraph를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="70fe9-105">Linux 기반 클러스터와 함께 Giraph를 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Giraph 설치(Linux)](hdinsight-hadoop-giraph-install-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70fe9-106">이 문서의 단계는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="70fe9-107">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="70fe9-108">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="70fe9-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="70fe9-110">Linux 기반 HDInsight 클러스터에 Giraph를 설치하는 방법에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Giraph 설치(Linux)](hdinsight-hadoop-giraph-install-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="70fe9-111">*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 Giraph를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="70fe9-112">HDInsight 클러스터에 Giraph를 설치하는 샘플 스크립트는 읽기 전용 Azure 저장소 Blob( [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1))에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="70fe9-113">샘플 스크립트는 HDInsight 클러스터 버전 3.1에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="70fe9-114">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="70fe9-115">**관련된 문서**</span><span class="sxs-lookup"><span data-stu-id="70fe9-115">**Related articles**</span></span>

* [<span data-ttu-id="70fe9-116">HDInsight Hadoop 클러스터에 Giraph 설치(Linux)</span><span class="sxs-lookup"><span data-stu-id="70fe9-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="70fe9-117">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="70fe9-118">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="70fe9-119">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="70fe9-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="70fe9-120">Giraph 정의</span><span class="sxs-lookup"><span data-stu-id="70fe9-120">What is Giraph?</span></span>
<span data-ttu-id="70fe9-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a>를 통해 Hadoop을 사용하여 그래프 처리를 수행할 수 있으며, Azure HDInsight에서 이를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="70fe9-122">그래프는 인터넷과 같은 대규모 네트워크의 라우터 간 연결, 소셜 네트워크(또는 소셜 그래프)상의 사람들 간 관계 등 개체 간의 관계를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="70fe9-123">그래프 처리를 통해 그래프의 개체 간 관계를 추론하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="70fe9-124">현재 관계를 기반으로 하여 잠재적인 친구 파악.</span><span class="sxs-lookup"><span data-stu-id="70fe9-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="70fe9-125">네트워크의 두 컴퓨터 간에 가장 짧은 경로 파악.</span><span class="sxs-lookup"><span data-stu-id="70fe9-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="70fe9-126">웹 페이지의 페이지 순위 계산.</span><span class="sxs-lookup"><span data-stu-id="70fe9-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="70fe9-127">포털을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="70fe9-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="70fe9-128">**HDInsight에서 Hadoop 클러스터 만들기**에서 설명한 대로 [사용자 지정 만들기](hdinsight-provision-clusters.md) 옵션을 사용하여 클러스터를 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="70fe9-129">아래와 같이 마법사의 **스크립트 동작** 페이지에서 **스크립트 동작 추가**를 클릭하여 스크립트 동작에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="70fe9-130">![스크립트 작업을 사용하여 클러스터 사용자 지정](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "스크립트 작업을 사용하여 클러스터 사용자 지정")</span><span class="sxs-lookup"><span data-stu-id="70fe9-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="70fe9-131">속성</span><span class="sxs-lookup"><span data-stu-id="70fe9-131">Property</span></span></th><th><span data-ttu-id="70fe9-132">값</span><span class="sxs-lookup"><span data-stu-id="70fe9-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="70fe9-133">이름</span><span class="sxs-lookup"><span data-stu-id="70fe9-133">Name</span></span></td>
            <td><span data-ttu-id="70fe9-134">스크립트 작업의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-134">Specify a name for the script action.</span></span> <span data-ttu-id="70fe9-135">예: <b>Install Giraph</b></span><span class="sxs-lookup"><span data-stu-id="70fe9-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="70fe9-136">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="70fe9-136">Script URI</span></span></td>
            <td><span data-ttu-id="70fe9-137">클러스터를 사용자 지정하기 위해 호출되는 스크립트에 URI(Uniform Resource Identifier)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="70fe9-138">예: <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="70fe9-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="70fe9-139">노드 유형</span><span class="sxs-lookup"><span data-stu-id="70fe9-139">Node Type</span></span></td>
            <td><span data-ttu-id="70fe9-140">사용자 지정 스크립트가 실행되는 노드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="70fe9-141"><b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="70fe9-142">매개 변수</span><span class="sxs-lookup"><span data-stu-id="70fe9-142">Parameters</span></span></td>
            <td><span data-ttu-id="70fe9-143">스크립트에 필요한 경우 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="70fe9-144">Giraph를 설치하는 스크립트는 매개 변수가 필요하지 않으므로 공백으로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="70fe9-145">두 개 이상의 스크립트 작업을 추가하여 클러스터에 여러 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="70fe9-146">스크립트를 추가한 후 확인 표시를 클릭하여 클러스터 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="70fe9-147">Giraph 사용</span><span class="sxs-lookup"><span data-stu-id="70fe9-147">Use Giraph</span></span>
<span data-ttu-id="70fe9-148">SimpleShortestPathsComputation 예제를 사용하여 그래프의 개체 간 가장 짧은 경로를 찾기 위한 기본 <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> 구현을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="70fe9-149">다음 단계에 따라 샘플 데이터와 샘플 jar을 업로드하고, SimpleShortestPathsComputation 예제를 사용하여 작업을 실행한 후 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="70fe9-150">샘플 데이터 파일을 Azure Blob 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="70fe9-151">로컬 워크스테이션에서 **tiny_graph.txt**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="70fe9-152">이 파일은 다음 줄을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="70fe9-153">tiny_graph.txt 파일을 HDInsight 클러스터의 기본 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="70fe9-154">데이터를 업로드하는 방법은 [HDInsight에서 Hadoop 작업에 대한 데이터 업로드](hdinsight-upload-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="70fe9-155">이 데이터는 [source\_id, source\_value,[[dest\_id], [edge\_value],...]]의 형식을 사용하여 방향이 지정된 그래프의 개체 간 관계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="70fe9-156">각 줄은 **source\_id** 개체와 하나 이상의 **dest\_id** 개체 간 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="70fe9-157">**edge\_value**(또는 가중치)는 **source_id**와 **dest\_id** 간 연결의 강도 또는 거리로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="70fe9-158">개체 간 거리로 위의 값(또는 가중치)을 사용하여 그리면 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![원과 거리가 다른 선으로 그린 tiny_graph.txt](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="70fe9-160">SimpleShortestPathsComputation 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="70fe9-161">다음 Azure PowerShell cmdlet에서 tiny_graph.txt 파일을 입력으로 사용하여 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="70fe9-162">Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="70fe9-163">이 문서의 단계에서는 Azure Resource Manager로 작동하는 새 HDInsight cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="70fe9-164">[Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs) 단계를 수행하여 최신 버전의 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="70fe9-165">Azure Resource Manager로 작동하는 새로운 cmdlet을 사용하도록 수정해야 하는 스크립트가 있는 경우 자세한 내용은 [HDInsight 클러스터에 대한 Azure Resource Manager 기반 개발 도구에 마이그레이션](hdinsight-hadoop-development-using-azure-resource-manager.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="70fe9-166">위의 예제에서는 **clustername** 을 Giraph가 설치된 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="70fe9-167">결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-167">View the results.</span></span> <span data-ttu-id="70fe9-168">작업이 완료되면 결과가 **wasb:///example/out/shotestpaths** 폴더에 있는 두 출력 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="70fe9-169">파일 이름은 **part-m-00001** 및 **part-m-00002**입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="70fe9-170">다음 단계에 따라 다운로드하고 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="70fe9-171">그러면 워크스테이션의 현재 디렉터리에 **example/output/shortestpaths** 디렉터리 구조가 만들어지고 해당 위치에 두 출력 파일이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="70fe9-172">다음과 같이 **Cat** cmdlet을 사용하여 파일 내용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="70fe9-173">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="70fe9-174">SimpleShortestPathComputation 예제는 개체 ID 1로 시작하도록 하드 코딩되며 다른 개체에 대한 가장 짧은 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="70fe9-175">따라서 출력은 `destination_id distance`이며, 여기서 distance는 가장자리를 기준으로 개체 ID 1과 대상 ID 간의 거리 값(또는 가중치)입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="70fe9-176">이를 시각화하면 ID 1과 다른 모든 개체 간의 가장 짧은 경로를 이동하여 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="70fe9-177">ID 1과 ID 4 간의 가장 짧은 경로는 5입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="70fe9-178"><span style="color:orange">ID 1과 3</span> 사이의 총 거리와 <span style="color:red">ID 3과 4</span> 사이의 총 거리를 더한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![가장 짧은 경로와 함께 원으로 그린 개체](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="70fe9-180">Aure PowerShell을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="70fe9-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="70fe9-181">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="70fe9-182">샘플은 Azure PowerShell을 사용하여 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="70fe9-183">스크립트를 사용자 지정하여 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="70fe9-184">.NET SDK을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="70fe9-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="70fe9-185">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70fe9-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="70fe9-186">샘플은 .NET SDK를 사용하여 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="70fe9-187">스크립트를 사용자 지정하여 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="70fe9-188">참고 항목</span><span class="sxs-lookup"><span data-stu-id="70fe9-188">See also</span></span>
* [<span data-ttu-id="70fe9-189">HDInsight Hadoop 클러스터에 Giraph 설치(Linux)</span><span class="sxs-lookup"><span data-stu-id="70fe9-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="70fe9-190">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="70fe9-191">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="70fe9-192">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="70fe9-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="70fe9-193">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="70fe9-194">[HDInsight 클러스터에서 R 설치][hdinsight-install-r]: R 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="70fe9-195">[HDInsight 클러스터에서 Solr 설치](hdinsight-hadoop-solr-install.md): Solr 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="70fe9-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
