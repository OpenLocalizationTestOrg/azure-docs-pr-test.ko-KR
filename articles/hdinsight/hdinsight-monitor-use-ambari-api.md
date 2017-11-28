---
title: "Ambari API를 사용하여 HDInsight에서 Hadoop 클러스터 모니터링 - Azure | Microsoft Docs"
description: "Hadoop 클러스터를 생성, 관리 및 모니터링하는 데 Apache Ambari API를 사용합니다. 직관적 운영자 도구와 API를 사용하면 Hadoop의 복잡한 작업을 간편하게 수행할 수 있습니다."
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
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="34504-104">Ambari API를 사용하여 HDInsight에서 Hadoop 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="34504-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="34504-105">Ambari API를 사용하여 HDInsight 클러스터를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="34504-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="34504-106">이 문서의 정보는 주로 Windows 기반 HDInsight 클러스터에 대한 것이며 Ambari REST API의 읽기 전용 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="34504-107">Linux 기반 클러스터는 [Ambari를 사용하여 Hadoop 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34504-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="34504-108">Ambari 정의</span><span class="sxs-lookup"><span data-stu-id="34504-108">What is Ambari?</span></span>
<span data-ttu-id="34504-109">[Apache Ambari][ambari-home]는 Apache Hadoop 클러스터를 프로비전, 관리 및 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34504-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="34504-110">Hadoop의 복잡성을 숨기고 클러스터 작업을 단순화하는 직관적인 연산자 도구 모음 및 강력한 API 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="34504-111">API에 대한 자세한 내용은 [Ambari API 참조][ambari-api-reference]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34504-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="34504-112">HDInsight는 현재 Ambari 모니터링 기능만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="34504-113">Ambari API 1.0은 HDInsight 클러스터 버전 3.0 및 2.1 클러스터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="34504-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="34504-114">이 문서에서는 HDInsight 버전 3.1 및 2.1 클러스터에서 Ambari API에 액세스하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="34504-115">두 버전 간의 가장 큰 차이점은 작업 기록 서버와 같은 새 기능이 도입되면서 일부 구성 요소가 변경되었다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34504-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="34504-116">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="34504-116">**Prerequisites**</span></span>

<span data-ttu-id="34504-117">이 자습서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="34504-118">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="34504-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="34504-119">(선택 사항)[cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="34504-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="34504-120">설치하려면 [cURL 릴리스 및 다운로드][curl-download]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34504-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="34504-121">Windows에서 cURL 명령을 사용할 때는 옵션 값에 작은따옴표 대신 큰따옴표를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="34504-122">**Azure HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="34504-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="34504-123">클러스터 프로비전에 대한 자세한 내용은 [HDInsight 사용 시작][hdinsight-get-started] 또는 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34504-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="34504-124">자습서를 완료하려면 다음 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="34504-125">클러스터 속성</span><span class="sxs-lookup"><span data-stu-id="34504-125">Cluster property</span></span> | <span data-ttu-id="34504-126">Azure PowerShell 변수 이름</span><span class="sxs-lookup"><span data-stu-id="34504-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="34504-127">값</span><span class="sxs-lookup"><span data-stu-id="34504-127">Value</span></span> | <span data-ttu-id="34504-128">설명</span><span class="sxs-lookup"><span data-stu-id="34504-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="34504-129">HDInsight 클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="34504-129">HDInsight cluster name</span></span> |<span data-ttu-id="34504-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="34504-130">$clusterName</span></span> | |<span data-ttu-id="34504-131">HDInsight 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="34504-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="34504-132">클러스터 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="34504-132">Cluster username</span></span> |<span data-ttu-id="34504-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="34504-133">$clusterUsername</span></span> | |<span data-ttu-id="34504-134">클러스터 사용자 이름은 클러스터를 만들 때 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="34504-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="34504-135">클러스터 암호</span><span class="sxs-lookup"><span data-stu-id="34504-135">Cluster password</span></span> |<span data-ttu-id="34504-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="34504-136">$clusterPassword</span></span> | |<span data-ttu-id="34504-137">클러스터 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="34504-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="34504-138">신속한 시작</span><span class="sxs-lookup"><span data-stu-id="34504-138">Jump-start</span></span>
<span data-ttu-id="34504-139">Ambari를 사용하여 HDInsight 클러스터를 모니터링하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="34504-140">**Azure PowerShell 사용**</span><span class="sxs-lookup"><span data-stu-id="34504-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="34504-141">다음 Azure PowerShell 스크립트는 *HDInsight 3.5 클러스터*에서 MapReduce 작업 추적기 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34504-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="34504-142">가장 큰 차이점은 MapReduce가 아니라 YARN 서비스에서 이러한 세부 정보를 가져온다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34504-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="34504-143">다음 Azure PowerShell 스크립트는 *HDInsight 2.1 클러스터*에서 MapReduce 작업 추적기 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34504-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="34504-144">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-144">The output is:</span></span>

![Jobtracker 출력][img-jobtracker-output]

<span data-ttu-id="34504-146">**cURL 사용**</span><span class="sxs-lookup"><span data-stu-id="34504-146">**Use cURL**</span></span>

<span data-ttu-id="34504-147">다음 예제는 cURL을 사용하여 클러스터 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34504-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="34504-148">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-148">The output is:</span></span>

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

<span data-ttu-id="34504-149">**2014/10/8 릴리스**:</span><span class="sxs-lookup"><span data-stu-id="34504-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="34504-150">Ambari 끝점 "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}"을 사용할 때 *host_name* 필드에서 호스트 이름만이 아니라 노드의 FQDN(정규화된 도메인 이름)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="34504-151">10/8/2014 릴리스 이전 버전에서는 이 예가 "**headnode0**"만 반환했습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="34504-152">10/8/2014 릴리스부터는 위의 예에 나와 있는 것처럼 FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**"이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="34504-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="34504-153">이 변경은 HBase, Hadoop 등의 여러 클러스터 유형을 VNET(가상 네트워크) 하나에 배포할 수 있는 시나리오를 원활하게 수행하기 위해 필요한 작업이었습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="34504-154">예를 들어 Hadoop의 백 엔드 플랫폼으로 HBase를 사용하는 등의 경우 이 변경이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34504-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="34504-155">Ambari 모니터링 API</span><span class="sxs-lookup"><span data-stu-id="34504-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="34504-156">다음 테이블은 가장 일반적으로 사용되는 Ambari 모니터링 API 호출을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="34504-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="34504-157">API에 대한 자세한 내용은 [Ambari API 참조][ambari-api-reference]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34504-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="34504-158">모니터링 API 호출</span><span class="sxs-lookup"><span data-stu-id="34504-158">Monitor API call</span></span> | <span data-ttu-id="34504-159">URI</span><span class="sxs-lookup"><span data-stu-id="34504-159">URI</span></span> | <span data-ttu-id="34504-160">설명</span><span class="sxs-lookup"><span data-stu-id="34504-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34504-161">클러스터 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="34504-162">클러스터 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="34504-163">클러스터, 서비스, 호스트</span><span class="sxs-lookup"><span data-stu-id="34504-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="34504-164">서비스 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="34504-165">서비스에 포함: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="34504-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="34504-166">서비스 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="34504-167">서비스 구성 요소 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="34504-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="34504-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="34504-169">구성 요소 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="34504-170">ServiceComponentInfo, host-components, 메트릭</span><span class="sxs-lookup"><span data-stu-id="34504-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="34504-171">호스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="34504-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="34504-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="34504-173">호스트 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="34504-174">호스트 구성 요소 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="34504-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="34504-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="34504-176">호스트 구성 요소 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="34504-177">HostRoles, 구성 요소, 호스트, 메트릭</span><span class="sxs-lookup"><span data-stu-id="34504-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="34504-178">구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="34504-179">구성 유형: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="34504-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="34504-180">구성 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="34504-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="34504-181">구성 유형: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="34504-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="34504-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34504-182">Next Steps</span></span>
<span data-ttu-id="34504-183">Ambari 모니터링 API 호출을 사용하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="34504-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="34504-184">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34504-184">To learn more, see:</span></span>

* <span data-ttu-id="34504-185">[Azure Portal을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="34504-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="34504-186">[Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="34504-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="34504-187">[명령줄 인터페이스를 사용하여 HDInsight 클러스터 관리][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="34504-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="34504-188">[HDInsight 설명서][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="34504-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="34504-189">[HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="34504-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
