---
title: "HDInsight | Microsoft Docs에서 Apache Storm 토폴로지 배포 및 관리"
description: "HDInsight에서 Storm 대시보드를 사용하여 Apache Storm 토폴로지를 배포, 모니터링 및 관리하는 방법에 대해 배웁니다. Visual Studio용 Hadoop 도구를 사용합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="a96e2-104">Windows 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="a96e2-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="a96e2-105">Storm 대시보드를 사용하면 사용자의 웹 브라우저를 사용하는 HDInsight 클러스터에 Apache Storm 토폴로지를 쉽게 배포 및 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="a96e2-106">실행 중인 토폴로지를 모니터링 및 관리하기 위해 대시보드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="a96e2-107">Visual Studio를 사용하는 경우 Visual Studio용 HDInsight 도구는 Visual Studio에서 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="a96e2-108">Storm 대시보드와 HDInsight 도구의 Storm 기능은 사용자 고유의 모니터링 및 관리 솔루션을 만들기 위해 사용할 수 있는 Storm REST API를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a96e2-109">이 문서의 단계에는 운영 체제로 Windows를 사용하는 HDInsight 클러스터에 Storm이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="a96e2-110">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a96e2-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="a96e2-112">Linux를 사용하는 HDInsight 클러스터에서 Storm 토폴로지 배포 및 관리에 대한 자세한 내용은 [Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a96e2-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a96e2-113">Prerequisites</span></span>

* <span data-ttu-id="a96e2-114">**HDInsight의 Apache Storm** - 클러스터를 만드는 단계는 [HDInsight에서 Apache Storm 시작](hdinsight-apache-storm-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="a96e2-115">**Storm 대시보드** - HTML5를 지원하는 최신 웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="a96e2-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="a96e2-116">**Visual Studio** - Azure SDK 2.5.1 이상 및 Visual Studio용 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="a96e2-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="a96e2-117">Visual Studio용 HDInsight 도구를 설치하고 구성하려면 [Visual Studio용 HDInsight 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="a96e2-118">다음과 같은 Visual Studio 버전 중 하나:</span><span class="sxs-lookup"><span data-stu-id="a96e2-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="a96e2-119">Visual Studio 2012 업데이트 4</span><span class="sxs-lookup"><span data-stu-id="a96e2-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="a96e2-120">Visual Studio 2013 업데이트 4 또는 Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="a96e2-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="a96e2-121">Visual Studio 2015(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="a96e2-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="a96e2-122">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="a96e2-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="a96e2-123">Storm 대시보드</span><span class="sxs-lookup"><span data-stu-id="a96e2-123">Storm Dashboard</span></span>

<span data-ttu-id="a96e2-124">Storm 대시보드는 Storm 클러스터에서 사용할 수 있는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="a96e2-125">URL은 **https://&lt;clustername>.azurehdinsight.net/**이며, **clustername**은 HDInsight 클러스터에서 Storm의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="a96e2-126">Storm 대시보드의 위쪽에서 **토폴로지 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="a96e2-127">샘플 토폴로지를 실행하거나 사용자가 만든 토폴로지를 업로드 및 실행하려면 페이지의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![토폴로지 제출 페이지][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="a96e2-129">Storm UI</span><span class="sxs-lookup"><span data-stu-id="a96e2-129">Storm UI</span></span>

<span data-ttu-id="a96e2-130">Storm 대시보드에서 **Storm UI** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="a96e2-131">실행 중인 토폴로지 외에도 클러스터에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![Storm UI][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="a96e2-133">일부 버전의 Internet Explorer에서는 처음으로 방문한 후 rm UI가 새로 고쳐지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="a96e2-134">예를 들어 제출한 새 토폴로지가 표시되지 않거나 이전에 비활성화한 토폴로지가 활성 상태로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="a96e2-135">Microsoft는 이 문제를 알고 있으며 해결 방법을 찾기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="a96e2-136">기본 페이지</span><span class="sxs-lookup"><span data-stu-id="a96e2-136">Main page</span></span>

<span data-ttu-id="a96e2-137">Storm UI의 기본 페이지에서는 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="a96e2-138">**클러스터 요약**: Storm 클러스터에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="a96e2-139">**토폴로지 요약**: 실행 중인 토폴로지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="a96e2-140">특정 토폴로지에 대한 자세한 정보를 보려면 이 섹션의 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="a96e2-141">**감독자 요약**: Storm 감독자에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="a96e2-142">**Nimbus 구성**: 클러스터에 대한 Nimbus 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="a96e2-143">토폴로지 요약</span><span class="sxs-lookup"><span data-stu-id="a96e2-143">Topology summary</span></span>

<span data-ttu-id="a96e2-144">**토폴로지 요약** 섹션의 링크를 선택하면 토폴로지에 대한 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="a96e2-145">**토폴로지 요약**: 토폴로지에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="a96e2-146">**토폴로지 동작**: 토폴로지에 대해 수행할 수 있는 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="a96e2-147">**활성화**- 비활성화된 토폴로지 처리를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="a96e2-148">**비활성화**- 실행 중인 토폴로지를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="a96e2-149">**균형 다시 맞추기**- 토폴로지의 병렬 처리를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="a96e2-150">클러스터에서 노드 수를 변경한 후 실행 중인 토폴로지의 균형을 다시 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="a96e2-151">이렇게 하면 토폴로지가 병렬 처리를 조정하여 클러스터에서 증가하거나 감소한 노드 수를 보충할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="a96e2-152">자세한 내용은 [Storm 토폴로지의 병렬 처리 이해(http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="a96e2-153">**중단**- 지정된 시간 제한 후 Storm 토폴로지를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="a96e2-154">**토폴로지 통계**: 토폴로지에 대한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="a96e2-155">**창** 열에 있는 링크를 사용하여 페이지에서 나머지 항목에 대한 시간 프레임을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="a96e2-156">**Spout**: 토폴로지에서 사용하는 Spout입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="a96e2-157">이 섹션의 링크를 사용하면 특정 Spout에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="a96e2-158">**Bolt**: 토폴로지에서 사용하는 Bolt입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="a96e2-159">이 섹션의 링크를 사용하면 특정 Bolt에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="a96e2-160">**토폴로지 구성**: 선택한 토폴로지의 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="a96e2-161">Spout 및 Bolt 요약</span><span class="sxs-lookup"><span data-stu-id="a96e2-161">Spout and Bolt summary</span></span>

<span data-ttu-id="a96e2-162">**Spouts** 또는 **Bolts** 섹션에서 Spout를 선택하면 선택한 항목에 대해 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="a96e2-163">**구성 요소 요약**: Spout 또는 Bolt에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="a96e2-164">**Spout/Bolt 통계**: Spout 또는 Bolt에 대한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="a96e2-165">**창** 열에 있는 링크를 사용하여 페이지에서 나머지 항목에 대한 시간 프레임을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="a96e2-166">**입력 통계** (Bolt에만 해당): Bolt에서 사용하는 입력 스트림에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="a96e2-167">**출력 통계**: 이 Spout 또는 Bolt가 내보낸 스트림에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="a96e2-168">**실행자**: Spout 또는 Bolt의 인스턴스에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="a96e2-169">특정 실행자에 대한 **Port** 항목을 선택하면 이 인스턴스에 대해 처리된 진단 정보의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="a96e2-170">**오류**: 이 Spout 또는 Bolt에 대한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="a96e2-171">Visual Studio용 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="a96e2-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="a96e2-172">HDInsight 도구는 Storm 클러스터에 C# 또는 하이브리드 토폴로지를 제출하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="a96e2-173">다음 단계는 샘플 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-173">The following steps use a sample application.</span></span> <span data-ttu-id="a96e2-174">HDInsight 도구를 사용하여 자신만의 토폴로지 만들기에 대한 자세한 내용은 [Visual Studio용 HDInsight 도구를 사용하여 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="a96e2-175">다음 단계를 통해 HDInsight 클러스터에서 Storm에 샘플을 배포한 다음 토폴로지를 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="a96e2-176">최신 버전의 Visual Studio용 HDInsight 도구를 아직 설치하지 않은 경우 [Visual Studio용 HDInsight 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="a96e2-177">Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="a96e2-178">**새 프로젝트** 대화 상자에서 **설치됨** > **템플릿**을 확장하고 **HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="a96e2-179">템플릿 목록에서 **Storm 샘플**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="a96e2-180">대화 상자 아래쪽에서 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![이미지](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="a96e2-182">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **HDInsight에서 Storm에 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a96e2-183">메시지가 표시되면 Azure 구독에 대한 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="a96e2-184">하나 이상의 구독이 있는 경우 HDInsight 클러스터의 Storm을 포함하는 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="a96e2-185">**Storm 클러스터** 드롭다운 목록에서 HDInsight의 Storm 클러스터를 선택한 다음 **제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="a96e2-186">**출력** 창을 사용하여 제출 성공 여부를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="a96e2-187">토폴로지 제출에 성공하면 클러스터에 대한 **Storm 토폴로지** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="a96e2-188">실행 중인 토폴로지에 대한 정보를 보려면 목록에서 토폴로지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-188">Select the topology from the list to view information about the running topology.</span></span>

    ![VISUAL STUDIO 모니터](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="a96e2-190">**Azure** > **HDInsight**를 확장한 다음 HDInsight의 Storm 클러스터를 마우스 오른쪽 단추로 클릭하고 **Storm 토폴로지 보기**를 선택하여 **서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="a96e2-191">이러한 구성 요소에 대한 정보를 보려면 Spout 또는 Bolt에 대한 셰이프를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="a96e2-192">선택한 각 항목에 대해 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a96e2-193">토폴로지 이름은 추가된 타임 스탬프가 있는 토폴로지의 클래스 이름입니다(이 경우 `HelloWord`).</span><span class="sxs-lookup"><span data-stu-id="a96e2-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="a96e2-194">토폴로지를 중단하려면 **토폴로지 요약** 보기에서 **중단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a96e2-195">Storm 토폴로지는 중지되거나 클러스터가 삭제될 때까지 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="a96e2-196">REST API</span><span class="sxs-lookup"><span data-stu-id="a96e2-196">REST API</span></span>

<span data-ttu-id="a96e2-197">Storm UI는 REST API의 맨 위에 기본 제공되므로 REST API를 사용하여 유사한 관리 및 모니터링 기능을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="a96e2-198">REST API를 사용하여 Storm 토폴로지를 관리 및 모니터링하는 사용자 지정 도구를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="a96e2-199">자세한 내용은 [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="a96e2-200">다음 정보는 HDInsight에서 Apache Storm과 REST API 사용하기에 관한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="a96e2-201">기본 URI</span><span class="sxs-lookup"><span data-stu-id="a96e2-201">Base URI</span></span>

<span data-ttu-id="a96e2-202">HDInsight 클러스터에서 REST API의 기본 URI는 **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**이며**clustername**은 HDInsight 클러스터에서 Storm의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="a96e2-203">인증</span><span class="sxs-lookup"><span data-stu-id="a96e2-203">Authentication</span></span>

<span data-ttu-id="a96e2-204">REST API 요청에서는 **기본 인증**을 사용해야 하므로 HDInsight 클러스터 관리자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="a96e2-205">기본 인증은 일반 텍스트로 전송되기 때문에 클러스터와의 안전한 통신을 위해서는 **항상** HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="a96e2-206">반환 값</span><span class="sxs-lookup"><span data-stu-id="a96e2-206">Return values</span></span>

<span data-ttu-id="a96e2-207">REST API에서 반환되는 정보는 클러스터와 동일한 Azure 가상 네트워크에 있는 클러스터 또는 가상 컴퓨터 내에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="a96e2-208">예를 들어, Zookeeper 서버에 대해 반환된 FQDN(정규화된 도메인 이름)은 인터넷에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a96e2-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a96e2-209">Next Steps</span></span>

<span data-ttu-id="a96e2-210">Storm 대시보드를 사용하여 토폴로지를 배포 및 모니터링하는 방법을 배웠으므로 이제 다음 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a96e2-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="a96e2-211">Visual Studio용 HDInsight 도구를 사용하여 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="a96e2-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="a96e2-212">Maven을 사용하여 Java 기반 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="a96e2-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="a96e2-213">추가 예제 토폴로지 목록은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96e2-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
