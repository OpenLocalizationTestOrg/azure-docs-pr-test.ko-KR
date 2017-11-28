---
title: "Linux 기반 HDInsight-Azure에 aaaAccess Hadoop YARN 응용 프로그램 로그온 | Microsoft Docs"
description: "Tooaccess YARN 응용 프로그램 명령줄 hello와 웹 브라우저를 사용 하는 Linux 기반 HDInsight (Hadoop) 클러스터에 로그온 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a><span data-ttu-id="7a6ea-103">Linux 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="7a6ea-103">Access YARN application logs on Linux-based HDInsight</span></span>

<span data-ttu-id="7a6ea-104">Tooaccess Azure HDInsight의 Hadoop 클러스터의 YARN (아직 다른 리소스 협상 자) 응용 프로그램에 대 한 로그를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-104">Learn how tooaccess hello logs for YARN (Yet Another Resource Negotiator) applications on a Hadoop cluster in Azure HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a6ea-105">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7a6ea-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7a6ea-107">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="7a6ea-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="7a6ea-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span></span>

<span data-ttu-id="7a6ea-109">hello [YARN 타임 라인 서버](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) 완성 된 응용 프로그램 및 두 가지 다른 인터페이스를 통해 응용 프로그램 프레임 워크 관련 정보에 대해 일반 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-109">hello [YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) provides generic information on completed applications and framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="7a6ea-110">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-110">Specifically:</span></span>

* <span data-ttu-id="7a6ea-111">3.1.1.374 이상 버전에서는 HDInsight 클러스터에서 제네릭 응용 프로그램 정보를 저장하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-111">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="7a6ea-112">hello 프레임 워크 관련 응용 프로그램 타임 라인 서버 hello의 구성 요소 정보를 HDInsight 클러스터에서 현재 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="7a6ea-112">hello framework-specific application information component of hello Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="7a6ea-113">응용 프로그램에 대 한 일반 정보는 데이터의 형식 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-113">Generic information on applications includes hello following type of data:</span></span>

* <span data-ttu-id="7a6ea-114">hello 응용 프로그램 ID, 응용 프로그램의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="7a6ea-114">hello application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="7a6ea-115">hello 응용 프로그램을 시작한 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="7a6ea-115">hello user who started hello application</span></span>
* <span data-ttu-id="7a6ea-116">시도에 정보 toocomplete hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="7a6ea-116">Information on attempts made toocomplete hello application</span></span>
* <span data-ttu-id="7a6ea-117">시도 하는 특정된 응용 프로그램에서 사용 하는 hello 컨테이너</span><span class="sxs-lookup"><span data-stu-id="7a6ea-117">hello containers used by any given application attempt</span></span>

## <span data-ttu-id="7a6ea-118"><a name="YARNAppsAndLogs"></a>YARN 응용 프로그램 및 로그</span><span class="sxs-lookup"><span data-stu-id="7a6ea-118"><a name="YARNAppsAndLogs"></a>YARN applications and logs</span></span>

<span data-ttu-id="7a6ea-119">YARN은 여러 프로그래밍 모델(예: MapReduce)을 지원하여 리소스 관리를 응용 프로그램 예약/모니터링과 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-119">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="7a6ea-120">YARN은 *리소스 관리자*(RM), 작업자 노드별 *노드 관리자*(NM) 및 응용 프로그램별 *응용 프로그램 마스터*(AM)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-120">YARN uses a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="7a6ea-121">hello 응용 프로그램별 AM 협상 리소스 (CPU, 메모리, 디스크, 네트워크) hello RM.로 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7a6ea-121">hello per-application AM negotiates resources (CPU, memory, disk, network) for running your application with hello RM.</span></span> <span data-ttu-id="7a6ea-122">RM hello 작동 NMs toogrant으로 권한이 부여 된 이러한 리소스를 *컨테이너*합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-122">hello RM works with NMs toogrant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="7a6ea-123">hello AM는 hello RM. 하 여 hello 할당 된 컨테이너 tooit의 hello 진행률 추적</span><span class="sxs-lookup"><span data-stu-id="7a6ea-123">hello AM is responsible for tracking hello progress of hello containers assigned tooit by hello RM.</span></span> <span data-ttu-id="7a6ea-124">응용 프로그램에 많은 컨테이너 hello 응용 프로그램의 hello 특성에 따라 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-124">An application may require many containers depending on hello nature of hello application.</span></span>

<span data-ttu-id="7a6ea-125">각 응용 프로그램은 여러 *응용 프로그램 시도*로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-125">Each application may consist of multiple *application attempts*.</span></span> <span data-ttu-id="7a6ea-126">응용 프로그램이 실패할 경우 새 시도로 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-126">If an application fails, it may be retried as a new attempt.</span></span> <span data-ttu-id="7a6ea-127">각 시도는 하나의 컨테이너에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-127">Each attempt runs in a container.</span></span> <span data-ttu-id="7a6ea-128">즉, 컨테이너 YARN 응용 프로그램에 의해 수행 된 작업의 기본 단위에 대 한 hello 컨텍스트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-128">In a sense, a container provides hello context for basic unit of work performed by a YARN application.</span></span> <span data-ttu-id="7a6ea-129">컨테이너의 hello 컨텍스트 내에서 수행 하는 모든 작업은 hello 단일 작업자 노드는 hello에 할당 된 컨테이너에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-129">All work that is done within hello context of a container is performed on hello single worker node on which hello container was allocated.</span></span> <span data-ttu-id="7a6ea-130">자세한 내용은 [YARN 개념][YARN-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-130">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="7a6ea-131">응용 프로그램 로그 (및 연결 된 hello 컨테이너 로그)는 문제가 있는 Hadoop 응용 프로그램 디버깅에서 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-131">Application logs (and hello associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="7a6ea-132">수집, 집계 및 hello 사용 하 여 응용 프로그램 로그를 저장 하기 위한 훌륭한 프레임 워크를 제공 하는 YARN [로그 집계] [ log-aggregation] 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-132">YARN provides a nice framework for collecting, aggregating, and storing application logs with hello [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="7a6ea-133">hello 로그 집계 기능을 사용 하면 응용 프로그램 로그에 액세스를 보다 명확히 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-133">hello Log Aggregation feature makes accessing application logs more deterministic.</span></span> <span data-ttu-id="7a6ea-134">이 기능은 작업자 노드의 모든 컨테이너에서 로그를 집계한 후 작업자 노드당 하나의 집계된 로그 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-134">It aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node.</span></span> <span data-ttu-id="7a6ea-135">응용 프로그램이 완료 된 후 hello 로그 hello 기본 파일 시스템에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-135">hello log is stored on hello default file system after an application finishes.</span></span> <span data-ttu-id="7a6ea-136">응용 프로그램이 수백 또는 수천 개의 컨테이너를 사용할 수 있습니다 하지만 단일 작업자 노드에서 실행 되는 모든 컨테이너에 대 한 로그는 단일 파일 집계 tooa 항상.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-136">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node are always aggregated tooa single file.</span></span> <span data-ttu-id="7a6ea-137">따라서 응용 프로그램에서 사용하는 작업자 노드당 하나의 로그만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-137">So there is only 1 log per worker node used by your application.</span></span> <span data-ttu-id="7a6ea-138">로그 집계는 HDInsight 클러스터 버전 3.0 이상에서 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-138">Log Aggregation is enabled by default on HDInsight clusters version 3.0 and above.</span></span> <span data-ttu-id="7a6ea-139">집계 된 로그는 hello 클러스터에 대 한 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-139">Aggregated logs are located in default storage for hello cluster.</span></span> <span data-ttu-id="7a6ea-140">경로 따라 hello은 hello HDFS 경로 toohello 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-140">hello following path is hello HDFS path toohello logs:</span></span>

    /app-logs/<user>/logs/<applicationId>

<span data-ttu-id="7a6ea-141">Hello 경로에 `user` hello hello 응용 프로그램을 시작한 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-141">In hello path, `user` is hello name of hello user who started hello application.</span></span> <span data-ttu-id="7a6ea-142">hello `applicationId` 는 hello YARN RM.로 hello 할당 된 고유 식별자 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="7a6ea-142">hello `applicationId` is hello unique identifier assigned tooan application by hello YARN RM.</span></span>

<span data-ttu-id="7a6ea-143">hello 집계 된 로그는 직접 읽을 수 있는 작성 된 대로 [TFile][T-file], [이진 형식] [ binary-format] 컨테이너에 의해 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-143">hello aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="7a6ea-144">이 로그 사용 하 여 hello YARN ResourceManager 기록 또는 CLI 도구 tooview 이러한 일반 텍스트로 응용 프로그램이 나 관심 있는 컨테이너에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-144">Use hello YARN ResourceManager logs or CLI tools tooview these logs as plain text for applications or containers of interest.</span></span>

## <a name="yarn-cli-tools"></a><span data-ttu-id="7a6ea-145">YARN CLI 도구</span><span class="sxs-lookup"><span data-stu-id="7a6ea-145">YARN CLI tools</span></span>

<span data-ttu-id="7a6ea-146">toouse hello YARN CLI 도구를 먼저 toohello HDInsight 클러스터 SSH를 사용 하 여 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-146">toouse hello YARN CLI tools, you must first connect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="7a6ea-147">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-147">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7a6ea-148">일반 텍스트로 hello 다음 명령 중 하나를 실행 하 여 이러한 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-148">You can view these logs as plain text by running one of hello following commands:</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

<span data-ttu-id="7a6ea-149">Hello 지정 &lt;applicationId >, &lt;사용자-사용자-시작-응용 프로그램 >, &lt;containerId >, 및 &lt;작업자 노드 주소 > 이러한 명령을 실행 하는 경우 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-149">Specify hello &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId>, and &lt;worker-node-address> information when running these commands.</span></span>

## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="7a6ea-150">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="7a6ea-150">YARN ResourceManager UI</span></span>

<span data-ttu-id="7a6ea-151">hello YARN ResourceManager UI hello 클러스터 헤드 노드에에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-151">hello YARN ResourceManager UI runs on hello cluster headnode.</span></span> <span data-ttu-id="7a6ea-152">Hello Ambari web UI 통해 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-152">It is accessed through hello Ambari web UI.</span></span> <span data-ttu-id="7a6ea-153">사용 하 여 hello 단계 tooview hello YARN 다음 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-153">Use hello following steps tooview hello YARN logs:</span></span>

1. <span data-ttu-id="7a6ea-154">웹 브라우저에서 toohttps://CLUSTERNAME.azurehdinsight.net 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-154">In your web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="7a6ea-155">CLUSTERNAME를 HDInsight 클러스터의 hello 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-155">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="7a6ea-156">Hello hello 왼쪽에 있는 서비스 목록에서 선택 **YARN**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-156">From hello list of services on hello left, select **YARN**.</span></span>

    ![선택한 Yarn 서비스](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. <span data-ttu-id="7a6ea-158">Hello에서 **빠른 링크** 드롭다운에서 hello 클러스터 헤드 노드 중 하나를 선택 하 고 다음 선택 **ResourceManager 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-158">From hello **Quick Links** dropdown, select one of hello cluster head nodes and then select **ResourceManager Log**.</span></span>

    ![Yarn 빠른 링크](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    <span data-ttu-id="7a6ea-160">링크 tooYARN 로그의 목록으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6ea-160">You are presented with a list of links tooYARN logs.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
