---
title: "aaaAccess Hadoop YARN 응용 프로그램 로그-프로그래밍 방식으로 Azure | Microsoft Docs"
description: "HDInsight의 Hadoop 클러스터에서 프로그래밍 방식으로 응용 프로그램 로그에 액세스합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a><span data-ttu-id="a9b74-103">Windows 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="a9b74-103">Access YARN application logs on Windows-based HDInsight</span></span>
<span data-ttu-id="a9b74-104">이 항목에서는 tooaccess 않았기 때문에 Azure HDInsight의 Hadoop Windows 기반 클러스터에서 YARN (아직 다른 리소스 협상 자) 응용 프로그램에 대 한 로그를 hello 하는 방법을 설명합니다</span><span class="sxs-lookup"><span data-stu-id="a9b74-104">This topic explains how tooaccess hello logs for YARN (Yet Another Resource Negotiator) applications that have finished on a Windows-based Hadoop cluster in Azure HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9b74-105">이 문서에 hello 정보에는 HDInsight 클러스터 tooWindows 기반만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-105">hello information in this document applies only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="a9b74-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a9b74-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9b74-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="a9b74-108">Linux 기반 HDInsight 클러스터에서 YARN 로그 액세스에 대한 정보는 [HDInsight의 Linux 기반 Hadoop에 대한 YARN 응용 프로그램 로그 액세스](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span><span class="sxs-lookup"><span data-stu-id="a9b74-108">For information on accessing YARN logs on Linux-based HDInsight clusters, see [Access YARN application logs on Linux-based Hadoop on HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span></span>
>


### <a name="prerequisites"></a><span data-ttu-id="a9b74-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9b74-109">Prerequisites</span></span>
* <span data-ttu-id="a9b74-110">Windows 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-110">A Windows-based HDInsight cluster.</span></span>  <span data-ttu-id="a9b74-111">[HDInsight에서 Windows 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9b74-111">See [Create Windows-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="yarn-timeline-server"></a><span data-ttu-id="a9b74-112">YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="a9b74-112">YARN Timeline Server</span></span>
<span data-ttu-id="a9b74-113">hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN 타임 라인 서버</a> 도 같이 프레임 워크 관련 응용 프로그램 정보 두 가지 다른 인터페이스를 통해 완성 된 응용 프로그램에 일반 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-113">hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> provides generic information on completed applications as well as framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="a9b74-114">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-114">Specifically:</span></span>

* <span data-ttu-id="a9b74-115">3.1.1.374 이상 버전에서는 HDInsight 클러스터에서 제네릭 응용 프로그램 정보를 저장하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-115">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="a9b74-116">hello 프레임 워크 관련 응용 프로그램 타임 라인 서버 hello의 구성 요소 정보를 HDInsight 클러스터에서 현재 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="a9b74-116">hello framework-specific application information component of hello Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="a9b74-117">응용 프로그램에 대 한 일반 정보는 hello 다음 종류의 데이터에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-117">Generic information on applications includes hello following sorts of data:</span></span>

* <span data-ttu-id="a9b74-118">hello 응용 프로그램 ID, 응용 프로그램의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a9b74-118">hello application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="a9b74-119">hello 응용 프로그램을 시작한 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="a9b74-119">hello user who started hello application</span></span>
* <span data-ttu-id="a9b74-120">시도에 정보 toocomplete hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a9b74-120">Information on attempts made toocomplete hello application</span></span>
* <span data-ttu-id="a9b74-121">시도 하는 특정된 응용 프로그램에서 사용 하는 hello 컨테이너</span><span class="sxs-lookup"><span data-stu-id="a9b74-121">hello containers used by any given application attempt</span></span>

<span data-ttu-id="a9b74-122">HDInsight 클러스터에서이 정보는 hello 기본 컨테이너의 기본 Azure 저장소 계정에서 Azure 리소스 관리자 tooa 기록 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-122">On your HDInsight clusters, this information will be stored by Azure Resource Manager tooa history store in hello default container of your default Azure Storage account.</span></span> <span data-ttu-id="a9b74-123">완료된 응용 프로그램에 대한 이 제네릭 데이터는 REST API를 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-123">This generic data on completed applications can be retrieved through a REST API:</span></span>

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a><span data-ttu-id="a9b74-124">YARN 응용 프로그램 및 로그</span><span class="sxs-lookup"><span data-stu-id="a9b74-124">YARN applications and logs</span></span>
<span data-ttu-id="a9b74-125">YARN은 여러 프로그래밍 모델(예: MapReduce)을 지원하여 리소스 관리를 응용 프로그램 예약/모니터링과 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-125">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="a9b74-126">이는 전역 *리소스 관리자*(RM), 작업자 노드별 *노드 관리자*(NM) 및 응용 프로그램별 *응용 프로그램 마스터*(AM)를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-126">This is done through a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="a9b74-127">hello 응용 프로그램별 AM 협상 리소스 (CPU, 메모리, 디스크, 네트워크) hello RM.로 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="a9b74-127">hello per-application AM negotiates resources (CPU, memory, disk, network) for running your application with hello RM.</span></span> <span data-ttu-id="a9b74-128">RM hello 작동 NMs toogrant으로 권한이 부여 된 이러한 리소스를 *컨테이너*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-128">hello RM works with NMs toogrant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="a9b74-129">hello AM는 hello RM. 하 여 hello 할당 된 컨테이너 tooit의 hello 진행률 추적</span><span class="sxs-lookup"><span data-stu-id="a9b74-129">hello AM is responsible for tracking hello progress of hello containers assigned tooit by hello RM.</span></span> <span data-ttu-id="a9b74-130">응용 프로그램에 많은 컨테이너 hello 응용 프로그램의 hello 특성에 따라 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-130">An application may require many containers depending on hello nature of hello application.</span></span>

<span data-ttu-id="a9b74-131">각 응용 프로그램의 여러 구성 될 수 있습니다 또한 *응용 프로그램 횟수* 순서 toofinish 크래시 또는 AM 간 통신의 toohello 손실 인해 hello 현재 상태에 RM. 및</span><span class="sxs-lookup"><span data-stu-id="a9b74-131">Furthermore, each application may consist of multiple *application attempts* in order toofinish in hello presence of crashes or due toohello loss of communication between an AM and an RM.</span></span> <span data-ttu-id="a9b74-132">따라서 컨테이너 응용 프로그램의 특정 시도 tooa 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-132">Hence, containers are granted tooa specific attempt of an application.</span></span> <span data-ttu-id="a9b74-133">관점에서 컨테이너 YARN 응용 프로그램에 의해 수행 된 작업의 기본 단위에 대 한 hello 컨텍스트를 제공 하 고 hello 단일 작업자 노드는 hello에 할당 된 컨테이너에 컨테이너의 hello 컨텍스트 내에서 수행 하는 모든 작업 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-133">In a sense, a container provides hello context for basic unit of work performed by a YARN application, and all work that is done within hello context of a container is performed on hello single worker node on which hello container was allocated.</span></span> <span data-ttu-id="a9b74-134">자세한 내용은 [YARN 개념][YARN-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9b74-134">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="a9b74-135">응용 프로그램 로그 (및 연결 된 hello 컨테이너 로그)는 문제가 있는 Hadoop 응용 프로그램 디버깅에서 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-135">Application logs (and hello associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="a9b74-136">수집, 집계 및 hello 사용 하 여 응용 프로그램 로그를 저장 하기 위한 훌륭한 프레임 워크를 제공 하는 YARN [로그 집계] [ log-aggregation] 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-136">YARN provides a nice framework for collecting, aggregating, and storing application logs with hello [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="a9b74-137">hello 로그 집계 기능을 사용 하면 응용 프로그램 로그에 액세스 보다 명확한 작업자 노드에 대 한 모든 컨테이너에서 로그를 집계 하 고 응용 프로그램을 완료 한 후 집계 된 로그 파일 작성 단위 작업자 노드 hello 기본 파일 시스템에로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-137">hello Log Aggregation feature makes accessing application logs more deterministic, as it aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node on hello default file system after an application finishes.</span></span> <span data-ttu-id="a9b74-138">응용 프로그램이 수백 또는 수천 개의 컨테이너를 사용할 수 있습니다 되지만 단일 작업자 노드에서 실행 되는 모든 컨테이너에 대 한 로그 항상 됩니다 집계 tooa 단일를 파일, 응용 프로그램에서 사용 하는 작업자 노드 당 하나의 로그 파일이 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-138">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node will always be aggregated tooa single file, resulting in one log file per worker node used by your application.</span></span> <span data-ttu-id="a9b74-139">로그를 집계 하는 HDInsight 클러스터에는 기본적으로 사용 됩니다 (버전 3.0 이상), 및 hello 수정할 수 있는 위치에 클러스터의 hello 기본 컨테이너에서 집계 된 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-139">Log Aggregation is enabled by default on HDInsight clusters (version 3.0 and above), and aggregated logs can be found in hello default container of your cluster at hello following location:</span></span>

    wasb:///app-logs/<user>/logs/<applicationId>

<span data-ttu-id="a9b74-140">해당 위치에 *사용자* hello 응용 프로그램을 시작한 hello 사용자의 hello 이름인 및 *applicationId* hello YARN RM.가 할당는 응용 프로그램의 고유 식별자 hello</span><span class="sxs-lookup"><span data-stu-id="a9b74-140">In that location, *user* is hello name of hello user who started hello application, and *applicationId* is hello unique identifier of an application as assigned by hello YARN RM.</span></span>

<span data-ttu-id="a9b74-141">hello 집계 된 로그는 직접 읽을 수 있는 작성 된 대로 [TFile][T-file], [이진 형식] [ binary-format] 컨테이너에 의해 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-141">hello aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="a9b74-142">YARN 제공 CLI 도구 toodump 이러한 로그 일반 텍스트로 응용 프로그램 또는 관심 있는 컨테이너에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-142">YARN provides CLI tools toodump these logs as plain text for applications or containers of interest.</span></span> <span data-ttu-id="a9b74-143">일반 텍스트로 hello tooit RDP를 통해 연결) (이후 hello 클러스터 노드에서 직접 YARN 명령이 다음 중 하나를 실행 하 여 이러한 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-143">You can view these logs as plain text by running one of hello following YARN commands directly on hello cluster nodes (after connecting tooit through RDP):</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="a9b74-144">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="a9b74-144">YARN ResourceManager UI</span></span>
<span data-ttu-id="a9b74-145">hello YARN ResourceManager UI hello 클러스터 헤드 노드에에서 실행 되 고 hello Azure 포털 대시보드를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-145">hello YARN ResourceManager UI runs on hello cluster headnode, and can be accessed through hello Azure portal dashboard:</span></span>

1. <span data-ttu-id="a9b74-146">역시 로그인[Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-146">Sign in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a9b74-147">Hello 왼쪽된 메뉴에서 클릭 **찾아보기**, 클릭 **HDInsight 클러스터**를 tooaccess hello YARN 응용 프로그램 로그를 지정 하는 Windows 기반 클러스터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-147">On hello left menu, click **Browse**, click **HDInsight Clusters**, click a Windows-based cluster that you want tooaccess hello YARN application logs.</span></span>
3. <span data-ttu-id="a9b74-148">Hello 상단 메뉴에서 클릭 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-148">On hello top menu, click **Dashboard**.</span></span> <span data-ttu-id="a9b74-149">**HDInsight 쿼리 콘솔**이라는 새 브라우저 탭에 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-149">You will see a page opened on a new browser tab called **HDInsight Query Console**.</span></span>
4. <span data-ttu-id="a9b74-150">**HDInsight 쿼리 콘솔**에서 **Yarn UI**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b74-150">From **HDInsight Query Console**, click **Yarn UI**.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
