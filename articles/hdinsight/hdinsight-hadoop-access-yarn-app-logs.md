---
title: "프로그래밍 방식으로 Hadoop YARN 응용 프로그램 로그에 액세스 - Azure | Microsoft Docs"
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
ms.openlocfilehash: 90323af4a1f4526ab9b26811c8679337076112d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a><span data-ttu-id="1e8ce-103">Windows 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="1e8ce-103">Access YARN application logs on Windows-based HDInsight</span></span>
<span data-ttu-id="1e8ce-104">이 항목에서는 Azure HDInsight의 Windows 기반 Hadoop 클러스터에서 완료된 YARN (Yet Another Resource Negotiator) 응용 프로그램에 대한 로그에 액세스하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-104">This topic explains how to access the logs for YARN (Yet Another Resource Negotiator) applications that have finished on a Windows-based Hadoop cluster in Azure HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e8ce-105">이 문서의 정보는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-105">The information in this document applies only to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1e8ce-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1e8ce-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1e8ce-108">Linux 기반 HDInsight 클러스터에서 YARN 로그 액세스에 대한 정보는 [HDInsight의 Linux 기반 Hadoop에 대한 YARN 응용 프로그램 로그 액세스](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1e8ce-108">For information on accessing YARN logs on Linux-based HDInsight clusters, see [Access YARN application logs on Linux-based Hadoop on HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span></span>
>


### <a name="prerequisites"></a><span data-ttu-id="1e8ce-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1e8ce-109">Prerequisites</span></span>
* <span data-ttu-id="1e8ce-110">Windows 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-110">A Windows-based HDInsight cluster.</span></span>  <span data-ttu-id="1e8ce-111">[HDInsight에서 Windows 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-111">See [Create Windows-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="yarn-timeline-server"></a><span data-ttu-id="1e8ce-112">YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="1e8ce-112">YARN Timeline Server</span></span>
<span data-ttu-id="1e8ce-113"><a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> (영문)는 두 가지 다른 인터페이스를 통해 완료된 응용 프로그램에 대한 제네릭 정보 및 프레임워크별 응용 프로그램 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-113">The <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> provides generic information on completed applications as well as framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="1e8ce-114">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-114">Specifically:</span></span>

* <span data-ttu-id="1e8ce-115">3.1.1.374 이상 버전에서는 HDInsight 클러스터에서 제네릭 응용 프로그램 정보를 저장하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-115">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="1e8ce-116">Timeline Server의 프레임워크별 응용 프로그램 정보 구성 요소는 HDInsight 클러스터에서 현재 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-116">The framework-specific application information component of the Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="1e8ce-117">응용 프로그램에 대한 제네릭 정보에는 다음과 같은 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-117">Generic information on applications includes the following sorts of data:</span></span>

* <span data-ttu-id="1e8ce-118">응용 프로그램의 고유한 식별자인 응용 프로그램 ID</span><span class="sxs-lookup"><span data-stu-id="1e8ce-118">The application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="1e8ce-119">응용 프로그램을 시작한 사용자</span><span class="sxs-lookup"><span data-stu-id="1e8ce-119">The user who started the application</span></span>
* <span data-ttu-id="1e8ce-120">응용 프로그램을 완료하려고 시도한 횟수</span><span class="sxs-lookup"><span data-stu-id="1e8ce-120">Information on attempts made to complete the application</span></span>
* <span data-ttu-id="1e8ce-121">지정된 응용 프로그램 시도에 사용된 컨테이너</span><span class="sxs-lookup"><span data-stu-id="1e8ce-121">The containers used by any given application attempt</span></span>

<span data-ttu-id="1e8ce-122">HDInsight 클러스터에서 이 정보는 Azure 리소스 관리자가 기본 Azure 저장소 계정의 기본 컨테이너에 있는 기록 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-122">On your HDInsight clusters, this information will be stored by Azure Resource Manager to a history store in the default container of your default Azure Storage account.</span></span> <span data-ttu-id="1e8ce-123">완료된 응용 프로그램에 대한 이 제네릭 데이터는 REST API를 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-123">This generic data on completed applications can be retrieved through a REST API:</span></span>

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a><span data-ttu-id="1e8ce-124">YARN 응용 프로그램 및 로그</span><span class="sxs-lookup"><span data-stu-id="1e8ce-124">YARN applications and logs</span></span>
<span data-ttu-id="1e8ce-125">YARN은 여러 프로그래밍 모델(예: MapReduce)을 지원하여 리소스 관리를 응용 프로그램 예약/모니터링과 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-125">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="1e8ce-126">이는 전역 *리소스 관리자*(RM), 작업자 노드별 *노드 관리자*(NM) 및 응용 프로그램별 *응용 프로그램 마스터*(AM)를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-126">This is done through a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="1e8ce-127">응용 프로그램별 AM은 응용 프로그램을 실행하기 위한 리소스(CPU, 메모리, 디스크, 네트워크)를 RM과 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-127">The per-application AM negotiates resources (CPU, memory, disk, network) for running your application with the RM.</span></span> <span data-ttu-id="1e8ce-128">RM은 NM과 협력하여 이러한 리소스를 부여하며, 이 리소스는 *컨테이너는*로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-128">The RM works with NMs to grant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="1e8ce-129">AM은 RM에 의해 부여받은 컨테이너의 진행률 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-129">The AM is responsible for tracking the progress of the containers assigned to it by the RM.</span></span> <span data-ttu-id="1e8ce-130">응용 프로그램의 특성에 따라 응용 프로그램에 여러 컨테이너가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-130">An application may require many containers depending on the nature of the application.</span></span>

<span data-ttu-id="1e8ce-131">또한 각 응용 프로그램은 작동 중단이 발생하거나 AM과 RM 간의 통신 손실로 인해 응용 프로그램을 완료하기 위해 여러 *응용 프로그램 시도* 로 구성될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-131">Furthermore, each application may consist of multiple *application attempts* in order to finish in the presence of crashes or due to the loss of communication between an AM and an RM.</span></span> <span data-ttu-id="1e8ce-132">따라서 컨테이너는 응용 프로그램의 특정 시도에 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-132">Hence, containers are granted to a specific attempt of an application.</span></span> <span data-ttu-id="1e8ce-133">컨테이너는 YARN 응용 프로그램에서 수행하는 기본 작업 단위에 대한 컨텍스트를 제공하고 컨테이너의 컨텍스트 내에서 수행되는 모든 작업은 컨테이너가 할당된 단일 작업자 노드에서 수행된다고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-133">In a sense, a container provides the context for basic unit of work performed by a YARN application, and all work that is done within the context of a container is performed on the single worker node on which the container was allocated.</span></span> <span data-ttu-id="1e8ce-134">자세한 내용은 [YARN 개념][YARN-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-134">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="1e8ce-135">응용 프로그램 로그(및 연관된 컨테이너 로그)는 문제가 있는 Hadoop 응용 프로그램을 디버깅하는 데 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-135">Application logs (and the associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="1e8ce-136">YARN은 [로그 집계][log-aggregation] 기능을 사용하여 응용 프로그램 로그를 수집, 집계 및 저장하기 위한 유용한 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-136">YARN provides a nice framework for collecting, aggregating, and storing application logs with the [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="1e8ce-137">로그 집계 기능은 응용 프로그램이 완료된 후 작업자 노드의 모든 컨테이너에서 로그를 집계하고 이를 작업자 노드별 하나의 집계 파일로 기본 파일 시스템에 저장하므로 응용 프로그램 로그에 더 명확하게 액세스할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-137">The Log Aggregation feature makes accessing application logs more deterministic, as it aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node on the default file system after an application finishes.</span></span> <span data-ttu-id="1e8ce-138">응용 프로그램은 수백 수천 개의 컨테이너를 사용할 수 있지만 단일 작업자 노드에서 실행되는 모든 컨테이너에 대한 로그는 항상 단일 파일로 집계되므로, 응용 프로그램에서 작업자 노드당 하나의 로그 파일만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-138">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node will always be aggregated to a single file, resulting in one log file per worker node used by your application.</span></span> <span data-ttu-id="1e8ce-139">로그 집계는 HDInsight 클러스터(버전 3.0 이상)에서 기본적으로 사용하도록 설정되며 집계된 로그는 클러스터의 기본 컨테이너인 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-139">Log Aggregation is enabled by default on HDInsight clusters (version 3.0 and above), and aggregated logs can be found in the default container of your cluster at the following location:</span></span>

    wasb:///app-logs/<user>/logs/<applicationId>

<span data-ttu-id="1e8ce-140">이 위치에서 *user*는 응용 프로그램을 시작한 사용자의 이름이고, *applicationId*는 YARN RM이 할당한 응용 프로그램의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-140">In that location, *user* is the name of the user who started the application, and *applicationId* is the unique identifier of an application as assigned by the YARN RM.</span></span>

<span data-ttu-id="1e8ce-141">집계된 로그는 컨테이너별로 인덱싱된 [이진 형식][binary-format]인 [TFile][T-file]로 작성되므로 직접 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-141">The aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="1e8ce-142">YARN에서는 관심 있는 응용 프로그램 또는 컨테이너에 대한 이러한 로그를 일반 텍스트로 덤프하는 CLI 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-142">YARN provides CLI tools to dump these logs as plain text for applications or containers of interest.</span></span> <span data-ttu-id="1e8ce-143">RDP를 통해 연결한 후 클러스터 노드에서 직접 다음 YARN 명령 중 하나를 실행하여 이러한 로그를 일반 텍스트로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-143">You can view these logs as plain text by running one of the following YARN commands directly on the cluster nodes (after connecting to it through RDP):</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="1e8ce-144">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="1e8ce-144">YARN ResourceManager UI</span></span>
<span data-ttu-id="1e8ce-145">YARN ResourceManager UI 클러스터 헤드 노드에서 실행되며 Azure 포털 대시보드를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-145">The YARN ResourceManager UI runs on the cluster headnode, and can be accessed through the Azure portal dashboard:</span></span>

1. <span data-ttu-id="1e8ce-146">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-146">Sign in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1e8ce-147">왼쪽 메뉴에서 **찾아보기**, **HDInsight 클러스터**, YARN 응용 프로그램 로그에 액세스할 Windows 기반 클러스터를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-147">On the left menu, click **Browse**, click **HDInsight Clusters**, click a Windows-based cluster that you want to access the YARN application logs.</span></span>
3. <span data-ttu-id="1e8ce-148">위쪽 메뉴에서 **대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-148">On the top menu, click **Dashboard**.</span></span> <span data-ttu-id="1e8ce-149">**HDInsight 쿼리 콘솔**이라는 새 브라우저 탭에 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-149">You will see a page opened on a new browser tab called **HDInsight Query Console**.</span></span>
4. <span data-ttu-id="1e8ce-150">**HDInsight 쿼리 콘솔**에서 **Yarn UI**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e8ce-150">From **HDInsight Query Console**, click **Yarn UI**.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
