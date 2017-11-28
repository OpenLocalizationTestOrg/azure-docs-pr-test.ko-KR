---
title: "Hadoop에서 Giraph Azure HDInsight 클러스터를 aaaInstall 및 사용 | Microsoft Docs"
description: "고 toocustomize HDInsight 클러스터 Giraph,으로 하는 방법에 대해 알아봅니다 toouse Giraph 합니다."
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
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="d9e31-103">Windows 기반 HDInsight 클러스터에서 Giraph 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="d9e31-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="d9e31-104">고 toocustomize Windows와 Giraph 스크립트 동작을 사용 하 여 HDInsight 클러스터를 기반으로 하는 방법에 대해 알아봅니다 toouse Giraph tooprocess 대규모 그래프입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="d9e31-105">Linux 기반 클러스터와 함께 Giraph를 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Giraph 설치(Linux)](hdinsight-hadoop-giraph-install-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e31-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9e31-106">이 문서 에서만 작동 하는 Windows 기반 HDInsight 클러스터의에서 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="d9e31-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d9e31-107">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="d9e31-108">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d9e31-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e31-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="d9e31-110">방법에 대 한 Linux 기반 HDInsight 클러스터에서 Giraph tooinstall 참조 [HDInsight Hadoop 클러스터 (Linux)에서 설치 Giraph](hdinsight-hadoop-giraph-install-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="d9e31-111">*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 Giraph를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="d9e31-112">HDInsight 클러스터에서 샘플 스크립트 tooinstall Giraph에서 읽기 전용 Azure 저장소 blob에서 사용할 수는 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="d9e31-113">hello 샘플 스크립트는 HDInsight 클러스터 버전 3.1과만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="d9e31-114">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e31-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="d9e31-115">**관련된 문서**</span><span class="sxs-lookup"><span data-stu-id="d9e31-115">**Related articles**</span></span>

* [<span data-ttu-id="d9e31-116">HDInsight Hadoop 클러스터에 Giraph 설치(Linux)</span><span class="sxs-lookup"><span data-stu-id="d9e31-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="d9e31-117">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="d9e31-118">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="d9e31-119">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="d9e31-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="d9e31-120">Giraph 정의</span><span class="sxs-lookup"><span data-stu-id="d9e31-120">What is Giraph?</span></span>
<span data-ttu-id="d9e31-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> tooperform 그래프 Hadoop을 사용 하 여 처리를 허용 하 고 Azure HDInsight 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="d9e31-122">인터넷, hello와 같은 대규모 네트워크에 있는 라우터 간 hello 연결 등의 개체 간의 관계를 모델링 하는 그래프 또는 소셜 네트워크 (경우에 따라 참조 tooas 소셜 그래프)에 사용자 간의 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="d9e31-123">Graph 처리 하면 그래프를 개체 간의 관계 hello에 대 한 tooreason 같은:</span><span class="sxs-lookup"><span data-stu-id="d9e31-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="d9e31-124">현재 관계를 기반으로 하여 잠재적인 친구 파악.</span><span class="sxs-lookup"><span data-stu-id="d9e31-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="d9e31-125">네트워크에 두 컴퓨터 간에 hello 최단 경로 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="d9e31-126">웹 페이지의 hello 페이지 순위를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="d9e31-127">포털을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="d9e31-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="d9e31-128">Hello를 사용 하 여 클러스터를 만들기 시작 **사용자 지정 만들기** 옵션에 설명 된 대로 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-provision-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="d9e31-129">Hello에 **스크립트 동작** 페이지 hello 마법사의 클릭 **스크립트 동작 추가** 아래와 같이 tooprovide hello 스크립트 동작에 대 한 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="d9e31-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="d9e31-130">![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")</span><span class="sxs-lookup"><span data-stu-id="d9e31-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d9e31-131">속성</span><span class="sxs-lookup"><span data-stu-id="d9e31-131">Property</span></span></th><th><span data-ttu-id="d9e31-132">값</span><span class="sxs-lookup"><span data-stu-id="d9e31-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d9e31-133">이름</span><span class="sxs-lookup"><span data-stu-id="d9e31-133">Name</span></span></td>
            <td><span data-ttu-id="d9e31-134">Hello 스크립트 동작에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-134">Specify a name for hello script action.</span></span> <span data-ttu-id="d9e31-135">예: <b>Install Giraph</b></span><span class="sxs-lookup"><span data-stu-id="d9e31-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="d9e31-136">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="d9e31-136">Script URI</span></span></td>
            <td><span data-ttu-id="d9e31-137">호출 된 toocustomize hello 클러스터는 hello 식별자 URI (Uniform Resource) toohello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="d9e31-138">예: <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="d9e31-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="d9e31-139">노드 유형</span><span class="sxs-lookup"><span data-stu-id="d9e31-139">Node Type</span></span></td>
            <td><span data-ttu-id="d9e31-140">Hello 사용자 지정 스크립트가 실행 되는 hello 노드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="d9e31-141"><b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="d9e31-142">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d9e31-142">Parameters</span></span></td>
            <td><span data-ttu-id="d9e31-143">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="d9e31-144">hello 스크립트 tooinstall Giraph 모든 매개 변수를 필요 하지 않으므로이 비워 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="d9e31-145">Hello 클러스터에서 둘 이상의 스크립트 동작 tooinstall 여러 구성 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="d9e31-146">Hello 스크립트를 추가한 후 hello 확인 표시 toostart hello 클러스터 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="d9e31-147">Giraph 사용</span><span class="sxs-lookup"><span data-stu-id="d9e31-147">Use Giraph</span></span>
<span data-ttu-id="d9e31-148">사용 하 여 hello SimpleShortestPathsComputation 예제 toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> hello 그래프에 있는 개체 사이의 최단 경로 찾기 위한 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="d9e31-149">다음 단계 tooupload hello 샘플 데이터와 hello 샘플 jar, hello SimpleShortestPathsComputation 예제 및 hello 결과 보기를 사용 하 여 작업을 실행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="d9e31-150">예제 데이터 파일 tooAzure Blob 저장소에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="d9e31-151">로컬 워크스테이션에서 **tiny_graph.txt**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="d9e31-152">위의 삼각형 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="d9e31-153">Hello tiny_graph.txt 파일 toohello 기본 저장소에 HDInsight 클러스터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="d9e31-154">방법에 대 한 지침은 tooupload 데이터 참조 [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드](hdinsight-upload-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="d9e31-155">Hello 형식을 사용 하 여는 방향된 그래프에 있는 개체 사이의 관계를 설명 하는이 데이터 [소스\_id, 소스\_값 [[dest\_id]를 [가장자리\_값],...]]. 각 줄은 **source\_id** 개체와 하나 이상의 **dest\_id** 개체 간 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="d9e31-156">hello **가장자리\_값** (또는 가중치) hello 수준 또는 거리 간의 hello 연결의으로 생각할 수 **source_id** 및 **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="d9e31-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="d9e31-157">으로 그린 hello 값 (또는 가중치)를 사용 하 여 개체 간의 hello 거리로, 데이터 위에 hello 다음과 같은 형식 및:</span><span class="sxs-lookup"><span data-stu-id="d9e31-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![원과 거리가 다른 선으로 그린 tiny_graph.txt](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="d9e31-159">Hello SimpleShortestPathsComputation 예제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="d9e31-160">입력으로 hello tiny_graph.txt 파일을 사용 하 여 다음 Azure PowerShell cmdlet toorun hello 예제 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d9e31-161">Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="d9e31-162">Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="d9e31-163">Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9e31-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="d9e31-164">해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="d9e31-165">위 예제는 hello, 바꿉니다 **clustername** Giraph 설치 되어 있는 HDInsight 클러스터의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="d9e31-166">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-166">View hello results.</span></span> <span data-ttu-id="d9e31-167">Hello 결과 hello에 두 개의 출력 파일에 저장 될 hello 작업이 완료 되 면 **wasb: / / / 예제/out/shotestpaths** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="d9e31-168">hello 파일 이라고 **파트-m-00001** 및 **00002-m-부분이**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="d9e31-169">Hello 단계 toodownload 및 보기 hello 출력 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="d9e31-170">이렇게 하면 hello 만들어집니다 **예제/출력/shortestpaths** hello 워크스테이션 및 다운로드 hello 두 출력 파일 toothat 위치에서 현재 디렉터리에서 디렉터리 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="d9e31-171">사용 하 여 hello **Cat** hello 파일 내용의 toodisplay hello cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d9e31-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="d9e31-172">hello 출력에는 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="d9e31-173">hello SimpleShortestPathComputation 예제 개체 ID가 1와 하드 코드 된 toostart and hello 가장 짧은 경로 tooother 개체를 찾는입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="d9e31-174">Hello 출력으로 읽어야 하므로 `destination_id distance`여기서 거리는 hello 가장자리 짧아 지도록 hello 값 (또는 가중치) 개체 ID가 1 사이의 hello 대상 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="d9e31-175">이 시각화를 ID 1과 다른 모든 개체 사이의 hello 가장 짧은 경로 이동 하 여 hello 결과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="d9e31-176">ID가 1에서 ID 4 사이의 최단 경로 hello 참고는 5입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="d9e31-177">이 hello 사이의 총 거리 <span style="color:orange">ID 1과 3</span>, 차례로 <span style="color:red">ID가 3 및 4</span>합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![가장 짧은 경로와 함께 원으로 그린 개체](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="d9e31-179">Aure PowerShell을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="d9e31-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="d9e31-180">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e31-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="d9e31-181">hello 샘플 방법을 tooinstall Azure PowerShell을 사용 하 여 Spark 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="d9e31-182">Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="d9e31-183">.NET SDK을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="d9e31-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="d9e31-184">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e31-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="d9e31-185">hello 샘플 방법을 tooinstall Spark.NET SDK hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="d9e31-186">Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="d9e31-187">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d9e31-187">See also</span></span>
* [<span data-ttu-id="d9e31-188">HDInsight Hadoop 클러스터에 Giraph 설치(Linux)</span><span class="sxs-lookup"><span data-stu-id="d9e31-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="d9e31-189">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="d9e31-190">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="d9e31-191">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="d9e31-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="d9e31-192">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="d9e31-193">[HDInsight 클러스터에서 R 설치][hdinsight-install-r]: R 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="d9e31-194">[HDInsight 클러스터에서 Solr 설치](hdinsight-hadoop-solr-install.md): Solr 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e31-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
