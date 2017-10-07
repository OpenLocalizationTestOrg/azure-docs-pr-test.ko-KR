---
title: "aaaDeploy 및 Linux 기반 HDInsight의 Apache Storm 토폴로지 관리 | Microsoft Docs"
description: "Toodeploy를 모니터링 하 고 hello 스톰 대시보드를 사용 하 여 Linux 기반 HDInsight의 Apache Storm 토폴로지를 관리 하는 방법에 대해 알아봅니다. Visual Studio용 Hadoop 도구를 사용합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="066ce-104">HDInsight에서 Apache Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="066ce-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="066ce-105">이 문서에서 관리 및 모니터링 스톰에서 HDInsight 클러스터에서 실행 되는 스톰 토폴로지 hello 기본 사항에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="066ce-106">hello이 문서의 단계 필요 HDInsight 클러스터에서 Linux 기반 스톰 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="066ce-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="066ce-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066ce-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="066ce-109">Windows 기반 HDInsight에서 토폴로지의 배포 및 모니터링에 대한 정보는 [Windows 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="066ce-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="066ce-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="066ce-110">Prerequisites</span></span>

* <span data-ttu-id="066ce-111">**HDInsight 클러스터의 Linux 기반 Storm**: 클러스터를 만드는 단계는 [HDInsight에서 Apache Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066ce-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="066ce-112">(선택 사항) **SSH 및 SCP의 기본적인 지식**: 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066ce-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="066ce-113">(선택 사항) **Visual Studio**: Azure SDK 2.5.1 나 최신 Visual Studio에 대 한 데이터 레이크 도구 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="066ce-114">자세한 내용은 [Data Lake Tools for Visual Studio 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066ce-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="066ce-115">다음 버전의 Visual Studio hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="066ce-116">Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="066ce-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="066ce-117">Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="066ce-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="066ce-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="066ce-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="066ce-119">Visual Studio 2015(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="066ce-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="066ce-120">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="066ce-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="066ce-121">데이터 레이크 Tools for Visual Studio 2017 hello Azure 작업의 일부로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="066ce-122">토폴로지 제출: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="066ce-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="066ce-123">hello HDInsight 도구에 사용 되는 toosubmit C# 또는 하이브리드 토폴로지에 tooyour Storm 클러스터 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="066ce-124">샘플 응용 프로그램을 사용 하는 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-124">hello following steps use a sample application.</span></span> <span data-ttu-id="066ce-125">Hello HDInsight 도구를 사용 하 여 사용자 고유의 토폴로지를 만드는 방법은 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio에 대 한 개발 C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="066ce-126">Visual Studio 용 hello 최신 버전의 hello 데이터 레이크 도구를 아직 설치 하지 있을 경우 참조 [데이터 레이크 도구를 사용 하 여 Visual Studio 용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="066ce-127">hello 데이터 레이크 Tools for Visual Studio는 Visual Studio에 대 한 hello HDInsight 도구 호출 이전 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="066ce-128">데이터 레이크 Tools for Visual Studio hello에 포함 된 __Azure 작업__ Visual Studio 2017에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="066ce-129">Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="066ce-130">Hello에 **새 프로젝트** 대화 상자에서 **설치 됨** > **템플릿**를 선택한 후 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="066ce-131">Hello 템플릿 목록에서 선택 **스톰 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="066ce-132">Hello 대화 상자의 hello 아래쪽 hello 응용 프로그램에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![이미지](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="066ce-134">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **HDInsight의 tooStorm 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="066ce-135">메시지가 표시 되 면 Azure 구독에 대 한 hello 로그인 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="066ce-136">구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="066ce-137">Hello에서 HDInsight 클러스터에서 프로그램 스톰 선택 **Storm 클러스터** 드롭 다운 목록에서 선택한 후 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="066ce-138">Hello 제출은 hello를 사용 하 여 성공 여부를 모니터링할 수 있습니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="066ce-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="066ce-139">토폴로지 전송: SSH 및 hello 스톰 명령</span><span class="sxs-lookup"><span data-stu-id="066ce-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="066ce-140">SSH tooconnect toohello HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="066ce-141">대체 **USERNAME** hello 이름 SSH 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="066ce-142">**CLUSTERNAME** 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="066ce-143">클러스터 SSH tooconnect tooyour HDInsight를 사용 하 여 대 한 자세한 내용은 참조 하십시오. [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="066ce-144">다음 명령 예제에서는 토폴로지 toostart hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="066ce-145">이 명령은 hello 클러스터에서 hello WordCount 토폴로지 예제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="066ce-146">이 토폴로지는 임의로 hello 문장에서 문장을 하 고 각 단어 hello 발생 횟수를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="066ce-147">Hello를 사용 하기 전에 hello 클러스터를 포함 하는 hello jar 파일을 먼저 복사 해야 toohello 클러스터 토폴로지를 전송할 때 `storm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="066ce-148">toocopy hello 파일 toohello 클러스터 hello를 사용할 수 있습니다 `scp` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="066ce-149">예를 들어 `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="066ce-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="066ce-150">hello WordCount 예제 및 기타 스톰 시작 예제에서 클러스터에 이미 포함 되어 `/usr/hdp/current/storm-client/contrib/storm-starter/`합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="066ce-151">토폴로지 제출: 프로그래밍 방식으로</span><span class="sxs-lookup"><span data-stu-id="066ce-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="066ce-152">Hello 클러스터에서 호스팅되는 Nimbus 서비스와 통신 하 여 HDInsight의 토폴로지 tooStorm를 프로그래밍 방식으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="066ce-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) 보여 주는 Java 응용 프로그램 예제를 제공 방법을 toodeploy hello Nimbus 서비스를 통해 토폴로지를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="066ce-154">모니터링 및 관리: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="066ce-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="066ce-155">토폴로지가 제출 될 때 성공적으로 Visual Studio를 사용 하 여, hello **스톰 토폴로지** 보기 hello 클러스터 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="066ce-156">토폴로지를 실행 하는 hello에 대 한 hello 목록 tooview 정보에서 hello 토폴로지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![VISUAL STUDIO 모니터](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="066ce-158">**Azure** > **HDInsight**를 확장한 다음 HDInsight의 Storm 클러스터를 마우스 오른쪽 단추로 클릭하고 **Storm 토폴로지 보기**를 선택하여 **서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="066ce-159">Hello spouts 또는 쐐기 이러한 구성 요소에 대 한 tooview 정보에 대 한 hello 셰이프를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="066ce-160">선택한 각 항목에 대해 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="066ce-161">비활성화 및 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="066ce-161">Deactivate and reactivate</span></span>

<span data-ttu-id="066ce-162">토폴로지를 비활성화하면 작업을 중단하거나 다시 활성화할 때까지 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="066ce-163">tooperform 이러한 작업을 사용 하 여 hello __비활성화__ 및 __다시 활성화__ hello hello 위쪽에 단추 __토폴로지 요약__합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="066ce-164">균형 재조정</span><span class="sxs-lookup"><span data-stu-id="066ce-164">Rebalance</span></span>

<span data-ttu-id="066ce-165">한 토폴로지를 리 밸런스 hello 시스템 toorevise hello의 병렬 처리 수준이 hello 토폴로지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="066ce-166">예를 들어, 크기를 조정 했습니다 hello 클러스터 tooadd 메모를 더 이상를 리 밸런스 하면 구성 토폴로지 toosee hello 새 노드 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="066ce-167">toorebalance 토폴로지를 사용 하 여 hello __균형을 다시 조정할__ hello hello 위쪽에 단추 __토폴로지 요약__합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="066ce-168">먼저 토폴로지를 리 밸런스 hello 토폴로지를 비활성화 한 다음 hello 클러스터 전체에서 균등 하 게 작업자를 재배포 하 다음 마지막으로 hello 토폴로지 toohello의 상태로 작업 재 분산 발생 하기 전에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="066ce-169">따라서 hello 토폴로지를 활성화 한 경우 그 다시 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="066ce-170">비활성화되어 있다면 비활성화된 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="066ce-171">토폴로지 종료</span><span class="sxs-lookup"><span data-stu-id="066ce-171">Kill a topology</span></span>

<span data-ttu-id="066ce-172">Storm 토폴로지는 중지 하거나 hello 클러스터를 삭제할 때까지 실행을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="066ce-173">toostop 토폴로지를 사용 하 여 hello __Kill__ hello hello 위쪽에 단추 __토폴로지 요약__합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="066ce-174">모니터링 및 관리: SSH 및 hello 스톰 명령</span><span class="sxs-lookup"><span data-stu-id="066ce-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="066ce-175">hello `storm` 유틸리티 토폴로지 hello 명령줄에서 실행 된 toowork을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="066ce-176">전체 명령 목록에는 `storm -h` 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="066ce-177">목록 토폴로지</span><span class="sxs-lookup"><span data-stu-id="066ce-177">List topologies</span></span>

<span data-ttu-id="066ce-178">모든 실행 중인 토폴로지에 명령 toolist 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="066ce-179">이 명령은 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="066ce-180">비활성화 및 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="066ce-180">Deactivate and reactivate</span></span>

<span data-ttu-id="066ce-181">토폴로지를 비활성화하면 작업을 중단하거나 다시 활성화할 때까지 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="066ce-182">다음 명령은 toodeactivate hello를 사용 하 고 다시 활성화:</span><span class="sxs-lookup"><span data-stu-id="066ce-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="066ce-183">실행 중인 토폴로지를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-183">Kill a running topology</span></span>

<span data-ttu-id="066ce-184">Storm 토폴로지가 일단 시작되면 중지될 때까지 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="066ce-185">toostop 토폴로지에서 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="066ce-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="066ce-186">균형 재조정</span><span class="sxs-lookup"><span data-stu-id="066ce-186">Rebalance</span></span>

<span data-ttu-id="066ce-187">한 토폴로지를 리 밸런스 hello 시스템 toorevise hello의 병렬 처리 수준이 hello 토폴로지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="066ce-188">예를 들어, 크기를 조정 했습니다 hello 클러스터 tooadd 메모를 더 이상를 리 밸런스 하면 구성 토폴로지 toosee hello 새 노드 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="066ce-189">먼저 토폴로지를 리 밸런스 hello 토폴로지를 비활성화 한 다음 hello 클러스터 전체에서 균등 하 게 작업자를 재배포 하 다음 마지막으로 hello 토폴로지 toohello의 상태로 작업 재 분산 발생 하기 전에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="066ce-190">따라서 hello 토폴로지를 활성화 한 경우 그 다시 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="066ce-191">비활성화되어 있다면 비활성화된 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="066ce-192">모니터링 및 관리: Storm UI</span><span class="sxs-lookup"><span data-stu-id="066ce-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="066ce-193">hello 스톰 UI 작업 토폴로지, 실행을 위한 웹 인터페이스를 제공 하 고 HDInsight 클러스터에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="066ce-194">tooview hello 스톰 UI를 사용 하 여 웹 브라우저 tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**여기서 **CLUSTERNAME** hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="066ce-195">사용자 이름 및 암호 tooprovide 요청 되 면 hello 클러스터 관리자 (관리자) 및 때 사용한 암호를 입력 hello 클러스터를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="066ce-196">기본 페이지</span><span class="sxs-lookup"><span data-stu-id="066ce-196">Main page</span></span>

<span data-ttu-id="066ce-197">hello 스톰 UI의 기본 페이지 hello hello를 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="066ce-198">**클러스터 요약**: hello Storm 클러스터에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="066ce-199">**토폴로지 요약**: 실행 중인 토폴로지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="066ce-200">자세한 내용은이 섹션 tooview의 hello 링크 사용 하 여 특정 토폴로지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="066ce-201">**요약 감독자**: hello 스톰 감독자에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="066ce-202">**Nimbus 구성**: hello 클러스터에 대 한 Nimbus 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="066ce-203">토폴로지 요약</span><span class="sxs-lookup"><span data-stu-id="066ce-203">Topology summary</span></span>

<span data-ttu-id="066ce-204">Hello에서 링크를 선택 하면 **토폴로지 요약** hello hello 토폴로지에 대 한 정보를 다음 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="066ce-205">**토폴로지 요약**: hello 토폴로지에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="066ce-206">**토폴로지 작업**: hello 토폴로지에 대해 수행할 수 있는 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="066ce-207">**활성화**- 비활성화된 토폴로지 처리를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="066ce-208">**비활성화**- 실행 중인 토폴로지를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="066ce-209">**균형을 다시 조정할**: hello 토폴로지의 hello 병렬 처리를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="066ce-210">하면 해야 균형을 다시 조정 실행 중인 토폴로지 hello hello 클러스터의 노드 수를 변경한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="066ce-211">이 작업에는 hello에 대 한 hello 토폴로지 tooadjust 병렬 처리 수준 toocompensate hello 클러스터의 노드 수가 늘어나거나 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="066ce-212">자세한 내용은 참조 <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">스톰 토폴로지의 hello parallelism 이해</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="066ce-213">**Kill**: hello 제한 시간을 지정한 후 스톰 토폴로지를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="066ce-214">**토폴로지 통계**: hello 토폴로지에 대 한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="066ce-215">tooset hello hello 페이지에 항목이 남아 있는 hello에 대 한 시간 범위, hello 링크를 사용 하 여 hello에 **창** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="066ce-216">**Spouts**: hello spouts hello 토폴로지에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="066ce-217">특정 spouts에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="066ce-218">**쐐기**: hello 볼트 hello 토폴로지에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="066ce-219">특정 볼트에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="066ce-220">**토폴로지 구성**: 선택한 hello 토폴로지의 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="066ce-221">Spout 및 Bolt 요약</span><span class="sxs-lookup"><span data-stu-id="066ce-221">Spout and Bolt summary</span></span>

<span data-ttu-id="066ce-222">배출구 hello에서 선택 하면 **Spouts** 또는 **쐐기** hello 다음 hello 선택 항목에 대 한 정보를 표시 하는 섹션:</span><span class="sxs-lookup"><span data-stu-id="066ce-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="066ce-223">**구성 요소 요약**: hello 배출구 또는 번개에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="066ce-224">**Stats 배출구/볼트**: hello에 대 한 통계 spout 또는 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="066ce-225">tooset hello hello 페이지에 항목이 남아 있는 hello에 대 한 시간 범위, hello 링크를 사용 하 여 hello에 **창** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="066ce-226">**Stats 입력** (볼트): hello에 대 한 정보 입력 스트림을 hello 볼트에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="066ce-227">**통계를 출력**:이에서 내보내는 hello 스트림에 대 한 정보 spout 또는 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="066ce-228">**단일 실행**: hello 배출구 또는 볼트의 인스턴스를 hello에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="066ce-229">선택 hello **포트** 이 인스턴스에 대 한 특정 실행자 tooview에 대 한 항목 진단 정보에 대 한 로그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="066ce-230">**오류**: 이 Spout 또는 Bolt에 대한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="066ce-231">모니터링 및 관리: REST API</span><span class="sxs-lookup"><span data-stu-id="066ce-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="066ce-232">hello 스톰 UI 비슷한 관리 및 모니터링 기능 hello REST API를 사용 하 여 수행할 수 있도록 hello REST API를 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="066ce-233">관리 및 모니터링 스톰 토폴로지 hello REST API toocreate 사용자 지정 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="066ce-234">자세한 내용은 [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066ce-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="066ce-235">hello 다음 정보는 특정 toousing hello HDInsight의 Apache Storm를 사용 하 여 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="066ce-236">hello 스톰 REST API를 공개적으로 사용할 수 없는 이상 인터넷 hello 및에서 SSH 터널 toohello HDInsight 클러스터 헤드 노드를 사용 하 여 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="066ce-237">만들고 SSH 터널을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [사용 하 여 SSH 터널링 tooaccess Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie, 및 기타 웹 Ui](hdinsight-linux-ambari-ssh-tunnel.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="066ce-238">기본 URI</span><span class="sxs-lookup"><span data-stu-id="066ce-238">Base URI</span></span>

<span data-ttu-id="066ce-239">hello hello REST API는 Linux 기반 HDInsight 클러스터에 대 한 기본 URI에 있는 hello에 헤드 노드 **https://HEADNODEFQDN:8744/api/v1/**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="066ce-240">hello 도메인 hello 헤드 노드의 이름에 클러스터를 만드는 동안 생성 되 고 static이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="066ce-241">여러 가지 방법으로 hello hello 클러스터 헤드 노드에 대 한 정규화 된 도메인 이름 (FQDN)을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="066ce-242">**한 SSH 세션에서**: hello 명령을 사용 하 여 `headnode -f` SSH 세션 toohello 클러스터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="066ce-243">**Ambari Web에서**: 선택 **서비스** hello hello 페이지의 위쪽에서 선택 **스톰**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="066ce-244">Hello에서 **요약** 탭에서 **스톰 UI 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="066ce-245">hello hello 페이지 위쪽에 hello hello 스톰 UI 및 REST API를 실행 하는 hello 노드의 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="066ce-246">**Ambari REST API에서**: hello 명령을 사용 하 여 `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` 스톰 UI 및 REST API hello hello 노드에 대 한 tooretrieve 정보에서 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="066ce-247">대체 **암호** hello 클러스터에 대 한 hello 관리자 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="066ce-248">대체 **CLUSTERNAME** hello 클러스터 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="066ce-249">Hello 응답 hello "host_name" 항목 hello hello 노드의 FQDN을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="066ce-250">인증</span><span class="sxs-lookup"><span data-stu-id="066ce-250">Authentication</span></span>

<span data-ttu-id="066ce-251">REST API를 사용 해야 하는 요청 toohello **기본 인증**이므로 hello HDInsight 클러스터 관리자 이름 및 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="066ce-252">일반 텍스트를 사용 하 여 기본 인증 보내지므로 해야 **항상** hello 클러스터와 toosecure HTTPS 통신을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="066ce-253">반환 값</span><span class="sxs-lookup"><span data-stu-id="066ce-253">Return values</span></span>

<span data-ttu-id="066ce-254">REST API만 hello 클러스터 내에서 사용할 수 있습니다 또는 가상 컴퓨터에 hello 클러스터와 동일한 Azure 가상 네트워크를 환영 hello에서 반환 되는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="066ce-255">예를 들어 hello 정규화 된 도메인 이름 (FQDN) 사육 서버에 대해 반환 되는 hello 인터넷에서에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="066ce-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="066ce-256">Next Steps</span></span>

<span data-ttu-id="066ce-257">이제 toodeploy / 모니터 토폴로지를 사용 하 여 스톰 대시보드 hello 하는 방법을 배운, 자세히 배울 방법 너무[Maven를 사용 하 여 개발 하는 Java 기반 토폴로지](hdinsight-storm-develop-java-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="066ce-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="066ce-258">추가 예제 토폴로지 목록은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066ce-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
