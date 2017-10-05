---
title: "Linux 기반 HDInsight에서 Hadoop YARN 응용 프로그램 로그에 액세스 - Azure | Microsoft Docs"
description: "명령줄과 웹 브라우저를 사용하여 Linux 기반 HDInsight(Hadoop) 클러스터에서 YARN 응용 프로그램 로그에 액세스하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: fbbbddc47f24a46eac9bc64d4420ee8429ed4ad1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a><span data-ttu-id="edea7-103">Linux 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="edea7-103">Access YARN application logs on Linux-based HDInsight</span></span>

<span data-ttu-id="edea7-104">Azure HDInsight의 Hadoop 클러스터에서 YARN(Yet Another Resource Negotiator) 응용 프로그램의 로그에 액세스하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-104">Learn how to access the logs for YARN (Yet Another Resource Negotiator) applications on a Hadoop cluster in Azure HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="edea7-105">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="edea7-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="edea7-107">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edea7-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="edea7-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="edea7-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span></span>

<span data-ttu-id="edea7-109">[YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) 는 두 가지 다른 인터페이스를 통해 완료된 응용 프로그램에 대한 제네릭 정보 및 프레임워크별 응용 프로그램 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-109">The [YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) provides generic information on completed applications and framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="edea7-110">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-110">Specifically:</span></span>

* <span data-ttu-id="edea7-111">3.1.1.374 이상 버전에서는 HDInsight 클러스터에서 제네릭 응용 프로그램 정보를 저장하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-111">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="edea7-112">Timeline Server의 프레임워크별 응용 프로그램 정보 구성 요소는 HDInsight 클러스터에서 현재 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-112">The framework-specific application information component of the Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="edea7-113">응용 프로그램에 대한 제네릭 정보에는 다음과 같은 유형의 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-113">Generic information on applications includes the following type of data:</span></span>

* <span data-ttu-id="edea7-114">응용 프로그램의 고유한 식별자인 응용 프로그램 ID</span><span class="sxs-lookup"><span data-stu-id="edea7-114">The application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="edea7-115">응용 프로그램을 시작한 사용자</span><span class="sxs-lookup"><span data-stu-id="edea7-115">The user who started the application</span></span>
* <span data-ttu-id="edea7-116">응용 프로그램을 완료하려고 시도한 횟수</span><span class="sxs-lookup"><span data-stu-id="edea7-116">Information on attempts made to complete the application</span></span>
* <span data-ttu-id="edea7-117">지정된 응용 프로그램 시도에 사용된 컨테이너</span><span class="sxs-lookup"><span data-stu-id="edea7-117">The containers used by any given application attempt</span></span>

## <span data-ttu-id="edea7-118"><a name="YARNAppsAndLogs"></a>YARN 응용 프로그램 및 로그</span><span class="sxs-lookup"><span data-stu-id="edea7-118"><a name="YARNAppsAndLogs"></a>YARN applications and logs</span></span>

<span data-ttu-id="edea7-119">YARN은 여러 프로그래밍 모델(예: MapReduce)을 지원하여 리소스 관리를 응용 프로그램 예약/모니터링과 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-119">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="edea7-120">YARN은 *리소스 관리자*(RM), 작업자 노드별 *노드 관리자*(NM) 및 응용 프로그램별 *응용 프로그램 마스터*(AM)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-120">YARN uses a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="edea7-121">응용 프로그램별 AM은 응용 프로그램을 실행하기 위한 리소스(CPU, 메모리, 디스크, 네트워크)를 RM과 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-121">The per-application AM negotiates resources (CPU, memory, disk, network) for running your application with the RM.</span></span> <span data-ttu-id="edea7-122">RM은 NM과 협력하여 이러한 리소스를 부여하며, 이 리소스는 *컨테이너는*로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-122">The RM works with NMs to grant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="edea7-123">AM은 RM에 의해 부여받은 컨테이너의 진행률 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-123">The AM is responsible for tracking the progress of the containers assigned to it by the RM.</span></span> <span data-ttu-id="edea7-124">응용 프로그램의 특성에 따라 응용 프로그램에 여러 컨테이너가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-124">An application may require many containers depending on the nature of the application.</span></span>

<span data-ttu-id="edea7-125">각 응용 프로그램은 여러 *응용 프로그램 시도*로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-125">Each application may consist of multiple *application attempts*.</span></span> <span data-ttu-id="edea7-126">응용 프로그램이 실패할 경우 새 시도로 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-126">If an application fails, it may be retried as a new attempt.</span></span> <span data-ttu-id="edea7-127">각 시도는 하나의 컨테이너에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-127">Each attempt runs in a container.</span></span> <span data-ttu-id="edea7-128">어떤 의미에서 컨테이너는 YARN 응용 프로그램에서 수행되는 작업의 기본 단위에 대한 컨텍스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-128">In a sense, a container provides the context for basic unit of work performed by a YARN application.</span></span> <span data-ttu-id="edea7-129">컨테이너의 컨텍스트 내에서 수행되는 모든 작업은 컨테이너가 할당되는 단일 작업자 노드에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-129">All work that is done within the context of a container is performed on the single worker node on which the container was allocated.</span></span> <span data-ttu-id="edea7-130">자세한 내용은 [YARN 개념][YARN-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edea7-130">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="edea7-131">응용 프로그램 로그(및 연관된 컨테이너 로그)는 문제가 있는 Hadoop 응용 프로그램을 디버깅하는 데 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-131">Application logs (and the associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="edea7-132">YARN은 [로그 집계][log-aggregation] 기능을 사용하여 응용 프로그램 로그를 수집, 집계 및 저장하기 위한 유용한 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-132">YARN provides a nice framework for collecting, aggregating, and storing application logs with the [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="edea7-133">로그 집계 기능을 사용하면 응용 프로그램 로그에 좀 더 확실하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-133">The Log Aggregation feature makes accessing application logs more deterministic.</span></span> <span data-ttu-id="edea7-134">이 기능은 작업자 노드의 모든 컨테이너에서 로그를 집계한 후 작업자 노드당 하나의 집계된 로그 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-134">It aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node.</span></span> <span data-ttu-id="edea7-135">로그는 응용 프로그램이 완료된 후 기본 파일 시스템에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-135">The log is stored on the default file system after an application finishes.</span></span> <span data-ttu-id="edea7-136">응용 프로그램은 수백 수천 개의 컨테이너를 사용할 수 있지만 단일 작업자 노드에서 실행되는 모든 컨테이너에 대한 로그는 항상 단일 파일로 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-136">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node are always aggregated to a single file.</span></span> <span data-ttu-id="edea7-137">따라서 응용 프로그램에서 사용하는 작업자 노드당 하나의 로그만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-137">So there is only 1 log per worker node used by your application.</span></span> <span data-ttu-id="edea7-138">로그 집계는 HDInsight 클러스터 버전 3.0 이상에서 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-138">Log Aggregation is enabled by default on HDInsight clusters version 3.0 and above.</span></span> <span data-ttu-id="edea7-139">집계된 로그는 클러스터에 대한 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-139">Aggregated logs are located in default storage for the cluster.</span></span> <span data-ttu-id="edea7-140">다음 경로는 로그에 대한 HDFS 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-140">The following path is the HDFS path to the logs:</span></span>

    /app-logs/<user>/logs/<applicationId>

<span data-ttu-id="edea7-141">경로에서 `user`는 응용 프로그램을 시작한 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-141">In the path, `user` is the name of the user who started the application.</span></span> <span data-ttu-id="edea7-142">`applicationId`는 YARN RM에서 응용 프로그램에 할당한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-142">The `applicationId` is the unique identifier assigned to an application by the YARN RM.</span></span>

<span data-ttu-id="edea7-143">집계된 로그는 컨테이너별로 인덱싱된 [이진 형식][binary-format]인 [TFile][T-file]로 작성되므로 직접 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-143">The aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="edea7-144">관심 있는 응용 프로그램 또는 컨테이너에 대한 이러한 로그를 일반 텍스트로 보려면 YARN ResourceManager 로그 또는 CLI 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-144">Use the YARN ResourceManager logs or CLI tools to view these logs as plain text for applications or containers of interest.</span></span>

## <a name="yarn-cli-tools"></a><span data-ttu-id="edea7-145">YARN CLI 도구</span><span class="sxs-lookup"><span data-stu-id="edea7-145">YARN CLI tools</span></span>

<span data-ttu-id="edea7-146">YARN CLI 도구를 사용하려면 먼저 SSH를 사용하여 HDInsight 클러스터에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-146">To use the YARN CLI tools, you must first connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="edea7-147">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edea7-147">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="edea7-148">이러한 로그를 다음 명령 중 하나를 실행하여 일반 텍스트로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-148">You can view these logs as plain text by running one of the following commands:</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

<span data-ttu-id="edea7-149">이러한 명령을 실행할 때 &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId> 및 &lt;worker-node-address> 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-149">Specify the &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId>, and &lt;worker-node-address> information when running these commands.</span></span>

## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="edea7-150">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="edea7-150">YARN ResourceManager UI</span></span>

<span data-ttu-id="edea7-151">YARN ResourceManager UI는 클러스터 헤드 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-151">The YARN ResourceManager UI runs on the cluster headnode.</span></span> <span data-ttu-id="edea7-152">Ambari 웹 UI를 통해 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-152">It is accessed through the Ambari web UI.</span></span> <span data-ttu-id="edea7-153">다음 단계를 사용하여 YARN 로그를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-153">Use the following steps to view the YARN logs:</span></span>

1. <span data-ttu-id="edea7-154">웹 브라우저에서 https://CLUSTERNAME.azurehdinsight.net으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-154">In your web browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="edea7-155">CLUSTERNAME은 HDInsight 클러스터 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-155">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="edea7-156">왼쪽에 있는 서비스 목록에서 **YARN**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-156">From the list of services on the left, select **YARN**.</span></span>

    ![선택한 Yarn 서비스](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. <span data-ttu-id="edea7-158">**빠른 링크** 드롭다운에서 클러스터 헤드 노드 중 하나를 선택한 다음 **ResourceManager 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-158">From the **Quick Links** dropdown, select one of the cluster head nodes and then select **ResourceManager Log**.</span></span>

    ![Yarn 빠른 링크](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    <span data-ttu-id="edea7-160">YARN 로그에 대한 링크 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="edea7-160">You are presented with a list of links to YARN logs.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
