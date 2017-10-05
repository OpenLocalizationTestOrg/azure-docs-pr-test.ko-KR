---
title: "HDInsight(Hadoop)에서 Giraph 설치 및 사용 - Azure | Microsoft Docs"
description: "스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터에 Giraph를 설치하는 방법에 대해 알아봅니다. 스크립트 작업을 사용하면 클러스터 구성을 변경하거나 서비스 및 유틸리티를 설치하여 생성 중 클러스터를 사용자 지정할 수 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="6e20b-104">HDInsight Hadoop 클러스터에 Giraph를 설치하고 Giraph를 사용하여 대규모 그래프를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="6e20b-105">HDInsight 클러스터에 Apache Giraph를 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="6e20b-106">Hdinsight의 스크립트 작업 기능을 사용하면 bash 스크립트를 실행하여 클러스터를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="6e20b-107">클러스터를 만드는 도중 및 만든 후에 클러스터를 사용자 지정하는 데 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e20b-108">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6e20b-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6e20b-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e20b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6e20b-111"><a name="whatis"></a>Giraph 정의</span><span class="sxs-lookup"><span data-stu-id="6e20b-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="6e20b-112">[Apache Giraph](http://giraph.apache.org/)를 통해 Hadoop을 사용하여 그래프 처리를 수행할 수 있으며, Azure HDInsight에서 이를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="6e20b-113">Graph는 개체 간의 관계를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="6e20b-114">예를 들어 인터넷 또는 소셜 네트워크 상의 사람들 간 관계와 같은 대규모 네트워크의 라우터 간의 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="6e20b-115">그래프 처리를 통해 그래프의 개체 간 관계를 추론하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="6e20b-116">현재 관계를 기반으로 하여 잠재적인 친구 파악.</span><span class="sxs-lookup"><span data-stu-id="6e20b-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="6e20b-117">네트워크의 두 컴퓨터 간에 가장 짧은 경로 파악.</span><span class="sxs-lookup"><span data-stu-id="6e20b-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="6e20b-118">웹 페이지의 페이지 순위 계산.</span><span class="sxs-lookup"><span data-stu-id="6e20b-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="6e20b-119">HDInsight 클러스터와 함께 제공되는 구성 요소는 완벽하게 지원됩니다. Microsoft 지원은 이러한 구성 요소와 관련된 문제를 격리하고 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="6e20b-120">Giraph와 같은 사용자 지정 구성 요소는 문제 해결에 도움이 되는 합리적인 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="6e20b-121">Microsoft 지원은 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="6e20b-122">그렇지 않으면 해당 기술에 대한 전문 지식을 찾을 수 있는 오픈 소스 커뮤니티를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="6e20b-123">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="6e20b-124">Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="6e20b-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="6e20b-125">스크립트가 수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="6e20b-125">What the script does</span></span>

<span data-ttu-id="6e20b-126">이 스크립트는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-126">This script performs the following actions:</span></span>

* <span data-ttu-id="6e20b-127">Giraph를 `/usr/hdp/current/giraph`에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="6e20b-128">클러스터에 대한 기본 저장소(WASB)에 `giraph-examples.jar` 파일을 복사합니다. `/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="6e20b-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="6e20b-129"><a name="install"></a>스크립트 동작을 사용하여 Giraph 설치</span><span class="sxs-lookup"><span data-stu-id="6e20b-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="6e20b-130">HDInsight 클러스터에서 Giraph를 설치하는 샘플 스크립트는 다음 위치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="6e20b-131">이 섹션에서는 Azure 포털을 사용하여 클러스터를 만들면서 샘플 스크립트를 사용하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6e20b-132">스크립트 작업은 다음 방법 중 하나를 사용하여 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="6e20b-133">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e20b-133">Azure PowerShell</span></span>
> * <span data-ttu-id="6e20b-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6e20b-134">The Azure CLI</span></span>
> * <span data-ttu-id="6e20b-135">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6e20b-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="6e20b-136">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="6e20b-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="6e20b-137">이미 실행 중인 클러스터에도 스크립트 동작을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="6e20b-138">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e20b-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="6e20b-139">[Linux 기반 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-portal.md)의 단계를 사용하여 클러스터를 만들기 시작하지만 완료하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6e20b-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="6e20b-140">**선택적 구성** 블레이드에서 **스크립트 동작**을 선택하고 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="6e20b-141">**이름**: 스크립트 동작의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="6e20b-142">**스크립트 URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="6e20b-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="6e20b-143">**HEAD**: 이 항목 선택</span><span class="sxs-lookup"><span data-stu-id="6e20b-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="6e20b-144">**작업자**: 이 항목을 선택 취소된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="6e20b-145">**ZOOKEEPER**: 이 항목을 선택 취소된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="6e20b-146">**PARAMETERS**: 이 필드는 공백으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="6e20b-147">**스크립트 동작**의 아래 쪽에서 **선택** 단추를 사용하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="6e20b-148">마지막으로 **선택적 구성** 블레이드의 아래 쪽에서 **선택** 단추를 사용하여 선택적 구성 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="6e20b-149">[Linux 기반 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-portal.md)에서 설명한 대로 클러스터를 계속 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="6e20b-150"><a name="usegiraph"></a>HDInsight에서 Giraph를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="6e20b-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="6e20b-151">클러스터를 만든 후 다음 단계를 사용하여 Giraph에 포함된 SimpleShortestPathsComputation 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="6e20b-152">이 예제는 그래프의 개체 간 가장 짧은 경로를 찾기 위한 기본 [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="6e20b-153">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6e20b-154">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e20b-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6e20b-155">다음 명령을 사용하여 **tiny_graph.txt**라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="6e20b-156">이 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="6e20b-157">이 데이터는 `[source_id, source_value,[[dest_id], [edge_value],...]]` 형식을 사용하여 유향 그래프에서 개체 간 관계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="6e20b-158">각 줄은 `source_id` 개체와 하나 이상의 `dest_id` 개체 간 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="6e20b-159">`edge_value`는 `source_id`와 `dest\_id` 간 연결의 강도 또는 거리로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="6e20b-160">개체 간 거리로 값(또는 가중치)을 사용하여 그리면 데이터는 다음 다이어그램과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![원과 거리가 다른 선으로 그린 tiny_graph.txt](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="6e20b-162">파일을 저장하려면 **Ctrl + X**, **Y**, 마지막으로 **Enter**를 차례로 사용하여 파일 이름을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="6e20b-163">다음을 사용하여 HDInsight 클러스터에 대한 주 저장소로 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="6e20b-164">다음 명령을 사용하여 SimpleShortestPathsComputation 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="6e20b-165">이 명령에 사용되는 매개 변수를 다음 테이블에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="6e20b-166">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-166">Parameter</span></span> | <span data-ttu-id="6e20b-167">기능</span><span class="sxs-lookup"><span data-stu-id="6e20b-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="6e20b-168">예를 포함하는 jar 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="6e20b-169">예를 시작하는 데 사용되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="6e20b-170">사용되는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-170">The example that is used.</span></span> <span data-ttu-id="6e20b-171">이 예제에서는 그래프에서 ID 1과 다른 모든 ID 사이의 최단 경로를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="6e20b-172">클러스터에 대한 헤드 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="6e20b-173">입력 데이터에 사용할 입력 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="6e20b-174">입력 데이터 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="6e20b-175">출력 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-175">The output format.</span></span> <span data-ttu-id="6e20b-176">이 예제에서는 일반 텍스트인 ID 및 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="6e20b-177">출력 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="6e20b-178">사용할 작업자의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-178">The number of workers to use.</span></span> <span data-ttu-id="6e20b-179">이 예제에서는 2입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-179">In this example, 2.</span></span> |

    <span data-ttu-id="6e20b-180">이 밖에 Giraph 샘플과 함께 사용된 기타 매개 변수에 대한 자세한 내용은 [Giraph 빠른 시작](http://giraph.apache.org/quick_start.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e20b-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="6e20b-181">작업이 완료되면 결과는 **/example/out/shotestpathss** 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="6e20b-182">출력 파일 이름은 **part-m-**으로 시작하고 첫 번째, 두 번째 파일 등을 나타내는 숫자로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="6e20b-183">다음 명령을 사용하여 출력을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="6e20b-184">출력은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="6e20b-185">SimpleShortestPathComputation 예제는 개체 ID 1로 시작하도록 하드 코딩되며 다른 개체에 대한 가장 짧은 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="6e20b-186">출력은 `destination_id` 및 `distance` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="6e20b-187">`distance`는 가장자리를 기준으로 개체 ID 1과 대상 ID 간의 거리 값(또는 가중치)입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="6e20b-188">이 데이터를 시각화하면 ID 1과 다른 모든 개체 간의 가장 짧은 경로를 이동하여 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="6e20b-189">ID 1과 ID 4 간의 가장 짧은 경로는 5입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="6e20b-190">이 값은 <span style="color:orange">ID 1과 3</span> 사이의 총 거리와 <span style="color:red">ID 3과 4</span> 사이의 총 거리입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![가장 짧은 경로와 함께 원으로 그린 개체](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="6e20b-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e20b-192">Next steps</span></span>

* <span data-ttu-id="6e20b-193">[HDInsight 클러스터에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6e20b-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="6e20b-194">[HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6e20b-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
