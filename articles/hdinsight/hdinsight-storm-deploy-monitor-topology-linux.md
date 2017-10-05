---
title: "Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리 | Microsoft Docs"
description: "Linux 기반 HDInsight에서 Storm 대시보드를 사용하여 Apache Storm 토폴로지를 배포, 모니터링 및 관리하는 방법에 대해 배웁니다. Visual Studio용 Hadoop 도구를 사용합니다."
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="075da-104">HDInsight에서 Apache Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="075da-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="075da-105">이 문서에서는 HDInsight 클러스터의 Storm에서 실행되는 Storm 토폴로지의 모니터링 및 관리에 관한 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="075da-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="075da-106">이 문서의 단계에는 HDInsight 클러스터의 Linux 기반 Storm이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="075da-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="075da-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="075da-109">Windows 기반 HDInsight에서 토폴로지의 배포 및 모니터링에 대한 정보는 [Windows 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="075da-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="075da-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="075da-110">Prerequisites</span></span>

* <span data-ttu-id="075da-111">**HDInsight 클러스터의 Linux 기반 Storm**: 클러스터를 만드는 단계는 [HDInsight에서 Apache Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="075da-112">(선택 사항) **SSH 및 SCP의 기본적인 지식**: 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="075da-113">(선택 사항) **Visual Studio**: Azure SDK 2.5.1 이상 및 Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="075da-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="075da-114">자세한 내용은 [Data Lake Tools for Visual Studio 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="075da-115">다음과 같은 Visual Studio 버전 중 하나:</span><span class="sxs-lookup"><span data-stu-id="075da-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="075da-116">Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="075da-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="075da-117">Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="075da-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="075da-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="075da-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="075da-119">Visual Studio 2015(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="075da-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="075da-120">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="075da-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="075da-121">Data Lake Tools for Visual Studio 2017은 Azure 워크로드의 일부로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="075da-122">토폴로지 제출: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="075da-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="075da-123">HDInsight 도구는 Storm 클러스터에 C# 또는 하이브리드 토폴로지를 제출하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="075da-124">다음 단계는 샘플 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-124">The following steps use a sample application.</span></span> <span data-ttu-id="075da-125">HDInsight 도구를 사용하여 자신만의 토폴로지 만들기에 대한 자세한 내용은 [Visual Studio용 HDInsight 도구를 사용하여 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="075da-126">최신 버전의 Data Lake Tools for Visual Studio를 아직 설치하지 않은 경우 [Data Lake Tools for Visual Studio 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="075da-127">Data Lake Tools for Visual Studio는 예전에 HDInsight Tools for Visual Studio였습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="075da-128">Data Lake Tools for Visual Studio는 Visual Studio 2017의 __Azure 워크로드__에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="075da-129">Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="075da-130">**새 프로젝트** 대화 상자에서 **설치됨** > **템플릿**을 확장하고 **HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="075da-131">템플릿 목록에서 **Storm 샘플**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="075da-132">대화 상자 아래쪽에서 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![이미지](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="075da-134">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **HDInsight에서 Storm에 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="075da-135">메시지가 표시되면 Azure 구독에 대한 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="075da-136">하나 이상의 구독이 있는 경우 HDInsight 클러스터의 Storm을 포함하는 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="075da-137">**Storm 클러스터** 드롭다운 목록에서 HDInsight의 Storm 클러스터를 선택한 다음 **제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="075da-138">**출력** 창을 사용하여 제출 성공 여부를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="075da-139">토폴로지 제출: SSH 및 Storm 명령</span><span class="sxs-lookup"><span data-stu-id="075da-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="075da-140">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="075da-141">**USERNAME**을 SSH 로그인의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="075da-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="075da-142">**CLUSTERNAME** 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="075da-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="075da-143">SSH를 사용하여 HDInsight 클러스터로 연결하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="075da-144">다음 명령을 사용하여 예제 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="075da-145">이 명령은 클러스터에서 예제 WordCount 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="075da-146">이 토폴로지는 임의로 문장을 생성하고 문장에서 각 단어의 발생 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="075da-147">클러스터에 토폴로지를 제출할 때 `storm` 명령을 사용하기 전에 먼저 Jar 파일을 포함하는 클러스터를 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="075da-148">클러스터에 파일을 복사하려면 `scp` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="075da-149">예를 들어 `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="075da-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="075da-150">WordCount 예제 및 다른 Storm 스타터 예제는 `/usr/hdp/current/storm-client/contrib/storm-starter/`에서 클러스터에 이미 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="075da-151">토폴로지 제출: 프로그래밍 방식으로</span><span class="sxs-lookup"><span data-stu-id="075da-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="075da-152">클러스터에서 호스트되는 Nimbus 서비스와 통신하여 HDInsight에서 Storm에 대한 토폴로지를 프로그래밍 방식으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="075da-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) 는 Nimbus 서비스를 통해 토폴로지를 배포하고 시작하는 방법을 보여 주는 예제 Java 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="075da-154">모니터링 및 관리: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="075da-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="075da-155">Visual Studio를 사용하여 토폴로지를 성공적으로 제출한 경우 클러스터의 **Storm 토폴로지** 보기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="075da-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="075da-156">실행 중인 토폴로지에 대한 정보를 보려면 목록에서 토폴로지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-156">Select the topology from the list to view information about the running topology.</span></span>

![VISUAL STUDIO 모니터](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="075da-158">**Azure** > **HDInsight**를 확장한 다음 HDInsight의 Storm 클러스터를 마우스 오른쪽 단추로 클릭하고 **Storm 토폴로지 보기**를 선택하여 **서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="075da-159">이러한 구성 요소에 대한 정보를 보려면 Spout 또는 Bolt에 대한 셰이프를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="075da-160">선택한 각 항목에 대해 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="075da-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="075da-161">비활성화 및 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="075da-161">Deactivate and reactivate</span></span>

<span data-ttu-id="075da-162">토폴로지를 비활성화하면 작업을 중단하거나 다시 활성화할 때까지 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="075da-163">이러한 작업을 수행하려면 __토폴로지 요약__ 맨 위에 있는 __비활성화__ 및 __다시 활성화__ 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="075da-164">균형 재조정</span><span class="sxs-lookup"><span data-stu-id="075da-164">Rebalance</span></span>

<span data-ttu-id="075da-165">토폴로지의 균형을 재조정하면 시스템이 토폴로지의 병렬 처리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="075da-166">예를 들어 클러스터 크기를 조정하고 더 많은 메모를 추가하려면 균형을 재조정하여 토폴로지가 새 노드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="075da-167">토폴로지의 균형을 재조정하려면 __토폴로지 요약__ 맨 위에 있는 __균형 재조정__ 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="075da-168">먼저 토폴로지의 균형을 재조정하면 토폴로지를 비활성화하고 클러스터에 작업자를 균등하게 다시 배포한 다음 마지막으로 토폴로지를 균형 재조정이 발생하기 전의 상태로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="075da-169">따라서 토폴로지가 활성화되었으면 작업이 다시 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="075da-170">비활성화되어 있다면 비활성화된 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="075da-171">토폴로지 종료</span><span class="sxs-lookup"><span data-stu-id="075da-171">Kill a topology</span></span>

<span data-ttu-id="075da-172">Storm 토폴로지는 중지되거나 클러스터가 삭제될 때까지 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="075da-173">토폴로지를 중지하려면 __토폴로지 요약__ 맨 위에 있는 __종료__ 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="075da-174">모니터링 및 관리: SSH 및 Storm 명령</span><span class="sxs-lookup"><span data-stu-id="075da-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="075da-175">`storm` 유틸리티를 사용하면 명령줄에서 실행하는 토폴로지로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="075da-176">전체 명령 목록에는 `storm -h` 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="075da-177">목록 토폴로지</span><span class="sxs-lookup"><span data-stu-id="075da-177">List topologies</span></span>

<span data-ttu-id="075da-178">다음 명령을 사용하여 실행하는 토폴로지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="075da-179">이 명령은 다음 텍스트와 유사한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="075da-180">비활성화 및 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="075da-180">Deactivate and reactivate</span></span>

<span data-ttu-id="075da-181">토폴로지를 비활성화하면 작업을 중단하거나 다시 활성화할 때까지 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="075da-182">다음 명령을 사용하여 비활성화 및 다시 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="075da-183">실행 중인 토폴로지를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-183">Kill a running topology</span></span>

<span data-ttu-id="075da-184">Storm 토폴로지가 일단 시작되면 중지될 때까지 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="075da-185">토폴로지를 중지하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="075da-186">균형 재조정</span><span class="sxs-lookup"><span data-stu-id="075da-186">Rebalance</span></span>

<span data-ttu-id="075da-187">토폴로지의 균형을 재조정하면 시스템이 토폴로지의 병렬 처리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="075da-188">예를 들어 클러스터 크기를 조정하고 더 많은 메모를 추가하려면 균형을 재조정하여 토폴로지가 새 노드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="075da-189">먼저 토폴로지의 균형을 재조정하면 토폴로지를 비활성화하고 클러스터에 작업자를 균등하게 다시 배포한 다음 마지막으로 토폴로지를 균형 재조정이 발생하기 전의 상태로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="075da-190">따라서 토폴로지가 활성화되었으면 작업이 다시 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="075da-191">비활성화되어 있다면 비활성화된 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="075da-192">모니터링 및 관리: Storm UI</span><span class="sxs-lookup"><span data-stu-id="075da-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="075da-193">Storm UI는 토폴로지를 실행하여 함께 작업하기 위한 웹 인터페이스를 제공하고 HDInsight 클러스터에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="075da-194">Storm UI를 보려면 웹 브라우저를 사용하여 **https://CLUSTERNAME.azurehdinsight.net/stormui**를 엽니다. 여기서 **CLUSTERNAME**은 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="075da-195">사용자 이름 및 암호를 제공하도록 요청을 받으면  클러스터를 만들 때 사용한 클러스터 관리자(관리자) 및암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="075da-196">기본 페이지</span><span class="sxs-lookup"><span data-stu-id="075da-196">Main page</span></span>

<span data-ttu-id="075da-197">Storm UI의 기본 페이지에서는 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="075da-198">**클러스터 요약**: Storm 클러스터에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="075da-199">**토폴로지 요약**: 실행 중인 토폴로지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="075da-200">특정 토폴로지에 대한 자세한 정보를 보려면 이 섹션의 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="075da-201">**감독자 요약**: Storm 감독자에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="075da-202">**Nimbus 구성**: 클러스터에 대한 Nimbus 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="075da-203">토폴로지 요약</span><span class="sxs-lookup"><span data-stu-id="075da-203">Topology summary</span></span>

<span data-ttu-id="075da-204">**토폴로지 요약** 섹션의 링크를 선택하면 토폴로지에 대한 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="075da-205">**토폴로지 요약**: 토폴로지에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="075da-206">**토폴로지 동작**: 토폴로지에 대해 수행할 수 있는 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="075da-207">**활성화**- 비활성화된 토폴로지 처리를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="075da-208">**비활성화**- 실행 중인 토폴로지를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="075da-209">**균형 다시 맞추기**- 토폴로지의 병렬 처리를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="075da-210">클러스터에서 노드 수를 변경한 후 실행 중인 토폴로지의 균형을 다시 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="075da-211">이 작업을 사용하면 토폴로지가 병렬 처리를 조정하여 클러스터에서 증가하거나 감소한 노드 수를 보충할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="075da-212">자세한 내용은 <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Storm 토폴로지의 병렬 처리 이해</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="075da-213">**중단**- 지정된 시간 제한 후 Storm 토폴로지를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="075da-214">**토폴로지 통계**: 토폴로지에 대한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="075da-215">페이지에서 나머지 항목에 대한 시간 프레임을 설정하려면 **창** 열에 있는 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="075da-216">**Spout**: 토폴로지에서 사용하는 Spout입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="075da-217">이 섹션의 링크를 사용하면 특정 Spout에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="075da-218">**Bolt**: 토폴로지에서 사용하는 Bolt입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="075da-219">이 섹션의 링크를 사용하면 특정 Bolt에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="075da-220">**토폴로지 구성**: 선택한 토폴로지의 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="075da-221">Spout 및 Bolt 요약</span><span class="sxs-lookup"><span data-stu-id="075da-221">Spout and Bolt summary</span></span>

<span data-ttu-id="075da-222">**Spouts** 또는 **Bolts** 섹션에서 Spout를 선택하면 선택한 항목에 대해 다음 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="075da-223">**구성 요소 요약**: Spout 또는 Bolt에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="075da-224">**Spout/Bolt 통계**: Spout 또는 Bolt에 대한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="075da-225">페이지에서 나머지 항목에 대한 시간 프레임을 설정하려면 **창** 열에 있는 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="075da-226">**입력 통계** (Bolt에만 해당): Bolt에서 사용하는 입력 스트림에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="075da-227">**출력 통계**: 이 Spout 또는 Bolt가 내보낸 스트림에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="075da-228">**실행자**: Spout 또는 Bolt의 인스턴스에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="075da-229">특정 실행자에 대한 **Port** 항목을 선택하면 이 인스턴스에 대해 처리된 진단 정보의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="075da-230">**오류**: 이 Spout 또는 Bolt에 대한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="075da-231">모니터링 및 관리: REST API</span><span class="sxs-lookup"><span data-stu-id="075da-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="075da-232">Storm UI는 REST API의 맨 위에 기본 제공되므로 REST API를 사용하여 유사한 관리 및 모니터링 기능을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="075da-233">REST API를 사용하여 Storm 토폴로지를 관리 및 모니터링하는 사용자 지정 도구를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="075da-234">자세한 내용은 [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="075da-235">다음 정보는 HDInsight에서 Apache Storm과 REST API 사용하기에 관한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="075da-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="075da-236">Storm REST API는 인터넷을 통해 공개적으로 사용할 수 없고 HDInsight 클러스터 헤드 노드에 SSH 터널을 사용하여 액세스되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="075da-237">SSH 터널의 생성 및 사용에 대한 정보는 [SSH 터널링을 사용하여 Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie 및 기타 웹 UI에 액세스](hdinsight-linux-ambari-ssh-tunnel.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="075da-238">기본 URI</span><span class="sxs-lookup"><span data-stu-id="075da-238">Base URI</span></span>

<span data-ttu-id="075da-239">Linux 기반 HDInsight 클러스터에서 REST API의 기본 URI는 **https://HEADNODEFQDN:8744/api/v1/**에 있는 헤드 노드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="075da-240">헤드 노드의 도메인 이름은 클러스터를 만드는 동안 생성되고 고정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="075da-241">다양한 방법으로 클러스터 헤드 노드의 정규화된 도메인 이름(FQDN)을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="075da-242">**SSH 세션에서**: SSH 세션에서 클러스터로 `headnode -f` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="075da-243">**Ambari 웹에서**: 페이지 맨 위에서 **서비스**를 선택한 다음 **Storm**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="075da-244">**요약** 탭에서 **Storm UI 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="075da-245">Storm UI 및 REST API가 실행 중인 노드의 FQDN은 페이지 맨 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="075da-246">**Ambari REST API에서**: `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` 명령을 사용하여 Storm UI 및 REST API가 실행 중인 노드에 관한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="075da-247">**PASSWORD**는 클러스터의 관리자 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="075da-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="075da-248">**CLUSTERNAME** 을 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="075da-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="075da-249">응답에서 "host_name" 항목에는 노드의 FQDN이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="075da-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="075da-250">인증</span><span class="sxs-lookup"><span data-stu-id="075da-250">Authentication</span></span>

<span data-ttu-id="075da-251">REST API 요청에서는 **기본 인증**을 사용해야 하므로 HDInsight 클러스터 관리자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="075da-252">기본 인증은 일반 텍스트로 전송되기 때문에 클러스터와의 안전한 통신을 위해서는 **항상** HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="075da-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="075da-253">반환 값</span><span class="sxs-lookup"><span data-stu-id="075da-253">Return values</span></span>

<span data-ttu-id="075da-254">REST API에서 반환되는 정보는 클러스터와 동일한 Azure 가상 네트워크에 있는 클러스터 또는 가상 컴퓨터 내에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="075da-255">예를 들어, Zookeeper 서버에 대해 반환된 FQDN(정규화된 도메인 이름)은 인터넷에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="075da-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="075da-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="075da-256">Next Steps</span></span>

<span data-ttu-id="075da-257">Storm 대시보드를 사용하여 토폴로지를 배포 및 모니터링하는 방법에 대해 배웠으므로 [Maven을 사용하여 Java 기반 토폴로지를 개발](hdinsight-storm-develop-java-topology.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="075da-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="075da-258">추가 예제 토폴로지 목록은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="075da-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
