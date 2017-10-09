---
title: "사용 하 여 HDInsight의 Hadoop 클러스터를 aaaMonitor hello Ambari API-Azure | Microsoft Docs"
description: "Hello Apache Ambari Api를 사용 하 여 만들고 관리 하 고, Hadoop 클러스터 모니터링에 대 한 합니다. 직관적인 연산자 도구와 Api Hadoop의 hello 복잡성을 숨깁니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="6d5aa-104">Hello Ambari API를 사용 하 여 HDInsight의 Hadoop 클러스터를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="6d5aa-105">Ambari Api를 사용 하 여 toomonitor HDInsight 클러스터 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="6d5aa-106">hello이이 문서의 정보는 읽기 전용 버전의 hello Ambari REST API를 제공 하는 Windows 기반 HDInsight 클러스터를 주로입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="6d5aa-107">Linux 기반 클러스터는 [Ambari를 사용하여 Hadoop 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="6d5aa-108">Ambari 정의</span><span class="sxs-lookup"><span data-stu-id="6d5aa-108">What is Ambari?</span></span>
<span data-ttu-id="6d5aa-109">[Apache Ambari][ambari-home]는 Apache Hadoop 클러스터를 프로비전, 관리 및 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="6d5aa-110">직관적인 도구 컬렉션으로 연산자와 강력한 클러스터 hello 작업 단순화 Hadoop의 hello 복잡성을 숨기는 Api 집합이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="6d5aa-111">Hello Api에 대 한 자세한 내용은 참조 [Ambari API 참조][ambari-api-reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="6d5aa-112">현재 HDInsight만 hello Ambari 모니터링 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="6d5aa-113">Ambari API 1.0은 HDInsight 클러스터 버전 3.0 및 2.1 클러스터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="6d5aa-114">이 문서에서는 HDInsight 버전 3.1 및 2.1 클러스터에서 Ambari API에 액세스하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="6d5aa-115">두 hello 사이의 hello 주요 차이점 hello 소개 새로운 기능 (예: 작업 기록 서버 hello)를 사용 하 여이 변경한 hello 구성 요소의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="6d5aa-116">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="6d5aa-116">**Prerequisites**</span></span>

<span data-ttu-id="6d5aa-117">이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="6d5aa-118">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="6d5aa-119">(선택 사항)[cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="6d5aa-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="6d5aa-120">tooinstall, 참조 [버전 및 다운로드 cURL][curl-download]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6d5aa-121">Windows에서 사용 하 여 큰따옴표 hello 옵션 값에 대 한 단일 따옴표 대신 hello cURL 명령을 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="6d5aa-122">**Azure HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="6d5aa-123">클러스터 프로비전에 대한 자세한 내용은 [HDInsight 사용 시작][hdinsight-get-started] 또는 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="6d5aa-124">Hello 자습서를 통해 데이터 toogo 다음 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="6d5aa-125">클러스터 속성</span><span class="sxs-lookup"><span data-stu-id="6d5aa-125">Cluster property</span></span> | <span data-ttu-id="6d5aa-126">Azure PowerShell 변수 이름</span><span class="sxs-lookup"><span data-stu-id="6d5aa-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="6d5aa-127">값</span><span class="sxs-lookup"><span data-stu-id="6d5aa-127">Value</span></span> | <span data-ttu-id="6d5aa-128">설명</span><span class="sxs-lookup"><span data-stu-id="6d5aa-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="6d5aa-129">HDInsight 클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="6d5aa-129">HDInsight cluster name</span></span> |<span data-ttu-id="6d5aa-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="6d5aa-130">$clusterName</span></span> | |<span data-ttu-id="6d5aa-131">HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="6d5aa-132">클러스터 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="6d5aa-132">Cluster username</span></span> |<span data-ttu-id="6d5aa-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="6d5aa-133">$clusterUsername</span></span> | |<span data-ttu-id="6d5aa-134">클러스터 사용자 이름이 hello 클러스터를 만들 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="6d5aa-135">클러스터 암호</span><span class="sxs-lookup"><span data-stu-id="6d5aa-135">Cluster password</span></span> |<span data-ttu-id="6d5aa-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="6d5aa-136">$clusterPassword</span></span> | |<span data-ttu-id="6d5aa-137">클러스터 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="6d5aa-138">신속한 시작</span><span class="sxs-lookup"><span data-stu-id="6d5aa-138">Jump-start</span></span>
<span data-ttu-id="6d5aa-139">Toouse Ambari toomonitor HDInsight 클러스터는 여러 가지가.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="6d5aa-140">**Azure PowerShell 사용**</span><span class="sxs-lookup"><span data-stu-id="6d5aa-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="6d5aa-141">Azure PowerShell 스크립트 뒤 hello hello MapReduce 작업 추적 장치 정보를 가져옵니다 *3.5 HDInsight 클러스터에 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="6d5aa-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="6d5aa-142">hello 주요 차이점은 hello YARN 서비스 (MapReduce 아님)에서 이러한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="6d5aa-143">PowerShell 스크립트 뒤 hello hello MapReduce 작업 추적 장치 정보를 가져옵니다 *2.1 HDInsight 클러스터에*:</span><span class="sxs-lookup"><span data-stu-id="6d5aa-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="6d5aa-144">hello 출력이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-144">hello output is:</span></span>

![Jobtracker 출력][img-jobtracker-output]

<span data-ttu-id="6d5aa-146">**cURL 사용**</span><span class="sxs-lookup"><span data-stu-id="6d5aa-146">**Use cURL**</span></span>

<span data-ttu-id="6d5aa-147">hello 다음 정보를 가져오는 예제 클러스터 cURL을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="6d5aa-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="6d5aa-148">hello 출력이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-148">hello output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="6d5aa-149">**2014 년 10 월 8 릴리스 hello에 대 한**:</span><span class="sxs-lookup"><span data-stu-id="6d5aa-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="6d5aa-150">때 Ambari hello를 사용 하 여 끝점, "을 (를) https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname" hello *host_name* 필드 hello hello 호스트 이름 대신 hello 노드의 정규화 된 도메인 이름 (FQDN)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="6d5aa-151">Hello 2014 년 10 월 8 릴리스 전에이 예제에서는 반환 단순히 "**headnode0**"입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="6d5aa-152">Hello FQDN을 얻게 hello 2014 년 10 월 8 릴리스 후 "**headnode0. { ClusterDNS}.azurehdinsight.net**"와 같이 hello 앞의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="6d5aa-153">이 변경은 필요한 toofacilitate 시나리오 여러 클러스터 유형 (예: HBase 및 Hadoop)를 배포할 수 있는 하나의 가상 네트워크 (VNET) 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="6d5aa-154">예를 들어 Hadoop의 백 엔드 플랫폼으로 HBase를 사용하는 등의 경우 이 변경이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="6d5aa-155">Ambari 모니터링 API</span><span class="sxs-lookup"><span data-stu-id="6d5aa-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="6d5aa-156">hello 다음 표에서 hello 가장 일반적인 Ambari 모니터링 API 호출 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="6d5aa-157">Hello API에 대 한 자세한 내용은 참조 [Ambari API 참조][ambari-api-reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="6d5aa-158">모니터링 API 호출</span><span class="sxs-lookup"><span data-stu-id="6d5aa-158">Monitor API call</span></span> | <span data-ttu-id="6d5aa-159">URI</span><span class="sxs-lookup"><span data-stu-id="6d5aa-159">URI</span></span> | <span data-ttu-id="6d5aa-160">설명</span><span class="sxs-lookup"><span data-stu-id="6d5aa-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d5aa-161">클러스터 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="6d5aa-162">클러스터 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="6d5aa-163">클러스터, 서비스, 호스트</span><span class="sxs-lookup"><span data-stu-id="6d5aa-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="6d5aa-164">서비스 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="6d5aa-165">서비스에 포함: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="6d5aa-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="6d5aa-166">서비스 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="6d5aa-167">서비스 구성 요소 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="6d5aa-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="6d5aa-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="6d5aa-169">구성 요소 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="6d5aa-170">ServiceComponentInfo, host-components, 메트릭</span><span class="sxs-lookup"><span data-stu-id="6d5aa-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="6d5aa-171">호스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="6d5aa-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="6d5aa-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="6d5aa-173">호스트 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="6d5aa-174">호스트 구성 요소 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="6d5aa-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="6d5aa-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="6d5aa-176">호스트 구성 요소 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="6d5aa-177">HostRoles, 구성 요소, 호스트, 메트릭</span><span class="sxs-lookup"><span data-stu-id="6d5aa-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="6d5aa-178">구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="6d5aa-179">구성 유형: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="6d5aa-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="6d5aa-180">구성 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d5aa-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="6d5aa-181">구성 유형: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="6d5aa-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d5aa-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d5aa-182">Next Steps</span></span>
<span data-ttu-id="6d5aa-183">파악 했으므로 이제 toouse Ambari 모니터링 API를 호출 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="6d5aa-184">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6d5aa-184">toolearn more, see:</span></span>

* <span data-ttu-id="6d5aa-185">[Hello Azure 포털을 사용 하 여 HDInsight 클러스터를 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="6d5aa-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="6d5aa-186">[Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="6d5aa-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="6d5aa-187">[명령줄 인터페이스를 사용하여 HDInsight 클러스터 관리][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="6d5aa-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="6d5aa-188">[HDInsight 설명서][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="6d5aa-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="6d5aa-189">[HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6d5aa-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
