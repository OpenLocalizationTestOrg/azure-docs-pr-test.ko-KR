---
title: "aaaDeploy HDInsight의 Apache Storm 토폴로지를 관리할 및 | Microsoft Docs"
description: "Toodeploy를 모니터링 하 고 hello 스톰 대시보드를 사용 하 여 HDInsight의 Apache Storm 토폴로지를 관리 하는 방법에 대해 알아봅니다. Visual Studio용 Hadoop 도구를 사용합니다."
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
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="c1b15-104">Windows 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="c1b15-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="c1b15-105">hello 스톰 대시보드 tooeasily을 사용 하면 배포 하 고 웹 브라우저를 사용 하 여 Apache Storm 토폴로지 tooyour HDInsight 클러스터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="c1b15-106">대시보드 toomonitor hello를 사용 하 고 실행 중인 토폴로지를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="c1b15-107">Visual Studio를 사용 하는 경우 hello HDInsight Tools for Visual Studio는 Visual Studio에서 비슷한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="c1b15-108">hello 스톰 대시보드와 hello 스톰 기능 hello HDInsight 도구에에서 사용 hello 스톰 REST API를 사용 하는 toocreate 될 수 있는 사용자 고유의 솔루션 모니터링 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1b15-109">이 문서의 단계 hello Windows hello 운영 체제로 사용 하 여 HDInsight 클러스터에서 Storm이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="c1b15-110">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c1b15-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1b15-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="c1b15-112">Linux를 사용하는 HDInsight 클러스터에서 Storm 토폴로지 배포 및 관리에 대한 자세한 내용은 [Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1b15-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1b15-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c1b15-113">Prerequisites</span></span>

* <span data-ttu-id="c1b15-114">**HDInsight의 Apache Storm** - 클러스터를 만드는 단계는 [HDInsight에서 Apache Storm 시작](hdinsight-apache-storm-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1b15-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="c1b15-115">Hello에 대 한 **스톰 대시보드**: 지 원하는 HTML5 최신 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="c1b15-116">에 대 한 **Visual Studio** -Azure SDK 2.5.1 나 최신 Visual Studio 용 HDInsight 도구 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="c1b15-117">참조 [Visual Studio 용 HDInsight 도구를 사용 하 여 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall 및 Visual Studio에 대 한 hello HDInsight 도구를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="c1b15-118">다음 버전의 Visual Studio hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="c1b15-119">Visual Studio 2012 업데이트 4</span><span class="sxs-lookup"><span data-stu-id="c1b15-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="c1b15-120">Visual Studio 2013 업데이트 4 또는 Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="c1b15-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="c1b15-121">Visual Studio 2015(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="c1b15-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="c1b15-122">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="c1b15-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="c1b15-123">Storm 대시보드</span><span class="sxs-lookup"><span data-stu-id="c1b15-123">Storm Dashboard</span></span>

<span data-ttu-id="c1b15-124">hello 스톰 대시보드는 Storm 클러스터에서 사용할 수 있는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="c1b15-125">hello URL은 **https://&lt;clustername >.azurehdinsight.net/**여기서 **clustername** HDInsight 클러스터에서 프로그램 스톰 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="c1b15-126">Hello 스톰 대시보드의 hello 위에서 선택 **제출 토폴로지**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="c1b15-127">Hello 페이지 toorun 샘플 토폴로지에 대 한 hello 지침 또는 tooupload 따르고 만든 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![hello 제출 토폴로지 페이지][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="c1b15-129">Storm UI</span><span class="sxs-lookup"><span data-stu-id="c1b15-129">Storm UI</span></span>

<span data-ttu-id="c1b15-130">Hello 스톰 대시보드, 선택 hello **스톰 UI** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="c1b15-131">이 토폴로지를 실행 하는 추가 tooany hello 클러스터에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![hello 스톰 ui][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="c1b15-133">일부 버전의 Internet Explorer와 처음 방문한 후 스톰 UI를 새로 고치지 않습니다 해당 hello를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="c1b15-134">예를 들어이 나타나지 않을 수 있습니다 hello 새 토폴로지 전송한 또는 이전에 비활성화 될 때 활성으로 토폴로지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="c1b15-135">Microsoft는 이 문제를 알고 있으며 해결 방법을 찾기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="c1b15-136">기본 페이지</span><span class="sxs-lookup"><span data-stu-id="c1b15-136">Main page</span></span>

<span data-ttu-id="c1b15-137">hello 스톰 UI의 기본 페이지 hello hello를 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="c1b15-138">**클러스터 요약**: hello Storm 클러스터에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="c1b15-139">**토폴로지 요약**: 실행 중인 토폴로지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="c1b15-140">자세한 내용은이 섹션 tooview의 hello 링크 사용 하 여 특정 토폴로지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="c1b15-141">**요약 감독자**: hello 스톰 감독자에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="c1b15-142">**Nimbus 구성**: hello 클러스터에 대 한 Nimbus 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="c1b15-143">토폴로지 요약</span><span class="sxs-lookup"><span data-stu-id="c1b15-143">Topology summary</span></span>

<span data-ttu-id="c1b15-144">Hello에서 링크를 선택 하면 **토폴로지 요약** hello hello 토폴로지에 대 한 정보를 다음 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="c1b15-145">**토폴로지 요약**: hello 토폴로지에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="c1b15-146">**토폴로지 작업**: hello 토폴로지에 대해 수행할 수 있는 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="c1b15-147">**활성화**- 비활성화된 토폴로지 처리를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="c1b15-148">**비활성화**- 실행 중인 토폴로지를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="c1b15-149">**균형을 다시 조정할**: hello 토폴로지의 hello 병렬 처리를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="c1b15-150">하면 해야 균형을 다시 조정 실행 중인 토폴로지 hello hello 클러스터의 노드 수를 변경한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="c1b15-151">이렇게 하면 hello 토폴로지 tooadjust 병렬 처리 수준 toocompensate hello에 대 한 값 만큼 증가 하거나 감소 하는 hello 클러스터의 노드 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="c1b15-152">자세한 내용은 참조 [스톰 토폴로지 (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)의 hello 병렬 처리 수준이 이해](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="c1b15-153">**Kill**: hello 제한 시간을 지정한 후 스톰 토폴로지를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="c1b15-154">**토폴로지 통계**: hello 토폴로지에 대 한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="c1b15-155">Hello 링크를 사용 하 여 hello에 **창** hello 페이지에 항목이 남아 있는 hello에 대 한 열 tooset hello 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="c1b15-156">**Spouts**: hello spouts hello 토폴로지에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="c1b15-157">특정 spouts에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="c1b15-158">**쐐기**: hello 볼트 hello 토폴로지에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="c1b15-159">특정 볼트에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="c1b15-160">**토폴로지 구성**: 선택한 hello 토폴로지의 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="c1b15-161">Spout 및 Bolt 요약</span><span class="sxs-lookup"><span data-stu-id="c1b15-161">Spout and Bolt summary</span></span>

<span data-ttu-id="c1b15-162">배출구 hello에서 선택 하면 **Spouts** 또는 **쐐기** hello 다음 hello 선택 항목에 대 한 정보를 표시 하는 섹션:</span><span class="sxs-lookup"><span data-stu-id="c1b15-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="c1b15-163">**구성 요소 요약**: hello 배출구 또는 번개에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="c1b15-164">**Stats 배출구/볼트**: hello에 대 한 통계 spout 또는 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="c1b15-165">Hello 링크를 사용 하 여 hello에 **창** hello 페이지에 항목이 남아 있는 hello에 대 한 열 tooset hello 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="c1b15-166">**Stats 입력** (볼트): hello에 대 한 정보 입력 스트림을 hello 볼트에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="c1b15-167">**통계를 출력**:이에서 내보내는 hello 스트림에 대 한 정보 spout 또는 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="c1b15-168">**단일 실행**: hello 배출구 또는 볼트의 인스턴스를 hello에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="c1b15-169">선택 hello **포트** 이 인스턴스에 대 한 특정 실행자 tooview에 대 한 항목 진단 정보에 대 한 로그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="c1b15-170">**오류**: 이 Spout 또는 Bolt에 대한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="c1b15-171">Visual Studio용 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="c1b15-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="c1b15-172">hello HDInsight 도구에 사용 되는 toosubmit C# 또는 하이브리드 토폴로지에 tooyour Storm 클러스터 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="c1b15-173">샘플 응용 프로그램을 사용 하는 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-173">hello following steps use a sample application.</span></span> <span data-ttu-id="c1b15-174">Hello HDInsight 도구를 사용 하 여 사용자 고유의 토폴로지를 만드는 방법은 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio에 대 한 개발 C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="c1b15-175">Hello 단계 toodeploy 샘플 tooyour 스톰 HDInsight 클러스터에서 다음을 사용 하 여 다음 보고 하 고 hello 토폴로지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="c1b15-176">Visual Studio 용 hello 최신 버전의 hello HDInsight 도구를 아직 설치 하지 있을 경우 참조 [Visual Studio 용 HDInsight 도구를 사용 하 여 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="c1b15-177">Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="c1b15-178">Hello에 **새 프로젝트** 대화 상자에서 **설치 됨** > **템플릿**를 선택한 후 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="c1b15-179">Hello 템플릿 목록에서 선택 **스톰 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="c1b15-180">Hello 대화 상자의 hello 아래쪽 hello 응용 프로그램에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![이미지](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="c1b15-182">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **HDInsight의 tooStorm 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c1b15-183">메시지가 표시 되 면 Azure 구독에 대 한 hello 로그인 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="c1b15-184">구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="c1b15-185">Hello에서 HDInsight 클러스터에서 프로그램 스톰 선택 **Storm 클러스터** 드롭 다운 목록에서 선택한 후 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="c1b15-186">Hello 제출은 hello를 사용 하 여 성공 여부를 모니터링할 수 있습니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="c1b15-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="c1b15-187">Hello 토폴로지 성공적으로 제출 되 면 hello **스톰 토폴로지** hello 클러스터 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="c1b15-188">토폴로지를 실행 하는 hello에 대 한 hello 목록 tooview 정보에서 hello 토폴로지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![VISUAL STUDIO 모니터](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="c1b15-190">**Azure** > **HDInsight**를 확장한 다음 HDInsight의 Storm 클러스터를 마우스 오른쪽 단추로 클릭하고 **Storm 토폴로지 보기**를 선택하여 **서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="c1b15-191">Hello spouts 또는 쐐기 이러한 구성 요소에 대 한 tooview 정보에 대 한 hello 셰이프를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="c1b15-192">선택한 각 항목에 대해 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c1b15-193">hello hello 토폴로지 이름이 hello 토폴로지의 hello 클래스 이름 (이 경우 `HelloWord`,) 타임 스탬프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="c1b15-194">Hello에서 **토폴로지 요약** 뷰의 **Kill** toostop hello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c1b15-195">Storm 토폴로지는 중지 하거나 hello 클러스터를 삭제할 때까지 실행을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="c1b15-196">REST API</span><span class="sxs-lookup"><span data-stu-id="c1b15-196">REST API</span></span>

<span data-ttu-id="c1b15-197">hello 스톰 UI 비슷한 관리 및 모니터링 기능 hello REST API를 사용 하 여 수행할 수 있도록 hello REST API를 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="c1b15-198">관리 및 모니터링 스톰 토폴로지 hello REST API toocreate 사용자 지정 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="c1b15-199">자세한 내용은 [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1b15-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="c1b15-200">hello 다음 정보는 특정 toousing hello HDInsight의 Apache Storm를 사용 하 여 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="c1b15-201">기본 URI</span><span class="sxs-lookup"><span data-stu-id="c1b15-201">Base URI</span></span>

<span data-ttu-id="c1b15-202">HDInsight 클러스터에서 REST API hello에 대 한 기본 URI는 hello **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**여기서 **clustername** 에 프로그램 Storm의 hello 이름인 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="c1b15-203">인증</span><span class="sxs-lookup"><span data-stu-id="c1b15-203">Authentication</span></span>

<span data-ttu-id="c1b15-204">REST API를 사용 해야 하는 요청 toohello **기본 인증**이므로 hello HDInsight 클러스터 관리자 이름 및 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="c1b15-205">일반 텍스트를 사용 하 여 기본 인증 보내지므로 해야 **항상** hello 클러스터와 toosecure HTTPS 통신을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="c1b15-206">반환 값</span><span class="sxs-lookup"><span data-stu-id="c1b15-206">Return values</span></span>

<span data-ttu-id="c1b15-207">REST API만 hello 클러스터 내에서 사용할 수 있습니다 또는 가상 컴퓨터에 hello 클러스터와 동일한 Azure 가상 네트워크를 환영 hello에서 반환 되는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="c1b15-208">예를 들어 hello 정규화 된 도메인 이름 (FQDN) 사육 서버에 대해 반환 되는 hello 인터넷에서에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b15-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1b15-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1b15-209">Next Steps</span></span>

<span data-ttu-id="c1b15-210">이제 toodeploy / 모니터 토폴로지를 사용 하 여 스톰 대시보드 hello 하는 방법을 배운, 자세히 배울 방법:</span><span class="sxs-lookup"><span data-stu-id="c1b15-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="c1b15-211">Visual Studio 용 HDInsight 도구 hello를 사용 하 여 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="c1b15-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="c1b15-212">Maven을 사용하여 Java 기반 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="c1b15-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="c1b15-213">추가 예제 토폴로지 목록은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1b15-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
