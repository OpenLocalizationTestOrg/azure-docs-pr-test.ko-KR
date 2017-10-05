---
title: "Ambari REST API를 사용하여 Hadoop 모니터링 및 관리 - Azure HDInsight | Microsoft Docs"
description: "Ambari를 사용하여 Azure HDInsight에서 Hadoop 클러스터를 모니터링하고 관리하는 방법에 대해 알아봅니다. 이 문서에서는 HDInsight 클러스터에 포함된 Ambari REST API를 사용하는 방법을 배웁니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="c5b51-104">Ambari REST API를 사용하여 HDInsight 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="c5b51-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="c5b51-105">Ambari REST API를 사용하여 Azure HDInsight에서 Hadoop 클러스터를 관리하고 모니터링하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="c5b51-106">Apache Ambari는 손쉬운 웹 UI 및 REST API 사용을 제공하여 Hadoop 클러스터의 관리 및 모니터링을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="c5b51-107">Ambari는 Linux 운영 체제를 사용하는 HDInsight 클러스터에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="c5b51-108">Ambari를 사용하여 클러스터를 모니터링하고 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="c5b51-109"><a id="whatis"></a>Ambari 정의</span><span class="sxs-lookup"><span data-stu-id="c5b51-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="c5b51-110">[Apache Ambari](http://ambari.apache.org)는 Hadoop 클러스터를 프로비저닝, 관리 및 모니터링하는 데 사용되는 웹 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="c5b51-111">개발자는 [Ambari REST API](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)를 사용하여 자신의 응용 프로그램에 이러한 기능을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="c5b51-112">Ambari는 Linux 기반 HDInsight 클러스터를 기본으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="c5b51-113">Ambari REST API 사용 방법</span><span class="sxs-lookup"><span data-stu-id="c5b51-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5b51-114">이 문서의 정보 및 예제에는 Linux 운영 체제를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="c5b51-115">자세한 내용은 [HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5b51-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="c5b51-116">이 문서의 예제는 Bourne 셸(bash) 및 PowerShell 둘 다로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="c5b51-117">bash 예제는 GNU bash 4.3.11로 테스트되었으나 다른 Unix 셸에서도 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="c5b51-118">PowerShell 예제는 PowerShell 5.0으로 테스트되었으나 PowerShell 3.0 이상에서 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="c5b51-119">__Bourne 셸__(Bash)을 사용하는 경우에는 다음이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="c5b51-120">[cURL](http://curl.haxx.se/): cURL은 명령줄에서 REST API와 함께 작동하도록 사용할 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="c5b51-121">이 문서에서 Ambari REST API와 통신하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="c5b51-122">Bash 또는 PowerShell을 사용할 경우 [jq](https://stedolan.github.io/jq/)도 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="c5b51-123">Jq는 JSON 문서를 사용하기 위한 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="c5b51-124">이 유틸리티는 **모든** Bash 예제와 PowerShell 예제 중 **하나**에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="c5b51-125">Ambari REST API의 기본 URI</span><span class="sxs-lookup"><span data-stu-id="c5b51-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="c5b51-126">HDInsight에서 Ambari REST API의 기본 URI는 https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME이며, 여기서 **CLUSTERNAME**은 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5b51-127">URI의 FQDN(정규화된 도메인 이름) 부분에 있는 클러스터 이름(CLUSTERNAME.azurehdinsight.net)은 대/소문자를 구분하지 않지만 URI의 다른 항목은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="c5b51-128">예를 들어 클러스터 이름이 `MyCluster`인 경우 올바른 URI는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="c5b51-129">이름의 두 번째 항목에 대/소문자가 잘못되었기 때문에 다음 URI는 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="c5b51-130">인증</span><span class="sxs-lookup"><span data-stu-id="c5b51-130">Authentication</span></span>

<span data-ttu-id="c5b51-131">HTTPS를 요구하는 HDInsight에서 Ambari로 연결</span><span class="sxs-lookup"><span data-stu-id="c5b51-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="c5b51-132">클러스터 만들기 중 입력한 관리자 계정 이름(기본값은 **admin**) 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="c5b51-133">예제: 인증 및 JSON 구문 분석</span><span class="sxs-lookup"><span data-stu-id="c5b51-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="c5b51-134">다음 예제에서는 기본 Ambari REST API에 대해 GET 요청을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="c5b51-135">이 문서의 Bash 예제는 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="c5b51-136">클러스터의 로그인 이름 기본값은 `admin`입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="c5b51-137">`$PASSWORD`에는 HDInsight 로그인 명령에 대한 암호가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="c5b51-138">`PASSWORD='mypassword'`를 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="c5b51-139">`$CLUSTERNAME`에는 클러스터의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="c5b51-140">`set CLUSTERNAME='clustername'`을 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="c5b51-141">이 문서의 PowerShell 예제는 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="c5b51-142">`$creds`는 클러스터에 대한 관리자 로그인 및 암호를 포함하는 자격 증명 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="c5b51-143">`$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"`을 사용하고 자격 증명을 제공하라는 메시지가 표시되면 제공하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="c5b51-144">`$clusterName`은 클러스터의 이름을 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="c5b51-145">`$clusterName="clustername"`을 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="c5b51-146">두 예제 모두 다음과 비슷한 정보로 시작되는 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="c5b51-147">JSON 데이터 구문 분석</span><span class="sxs-lookup"><span data-stu-id="c5b51-147">Parsing JSON data</span></span>

<span data-ttu-id="c5b51-148">다음 예제에서는 `jq`를 사용하여 JSON 응답 문서를 구문 분석하고 결과 중에서 `health_report` 문서만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="c5b51-149">PowerShell 3.0 이상에서는 JSON 문서를 PowerShell에서 보다 쉽게 사용할 수 있는 개체로 변환하는 `ConvertFrom-Json` cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="c5b51-150">다음 예제에서는 `ConvertFrom-Json`을 사용하여 결과 중에서 `health_report` 정보만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="c5b51-151">이 문서의 예제 대부분은 `ConvertFrom-Json`을 사용하여 응답 문서의 요소를 표시하고 [Ambari 구성 업데이트](#example-update-ambari-configuration) 예제는 jq를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="c5b51-152">Jq는 JSON 응답 문서에서 새 템플릿을 생성하기 위해 이 예제에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="c5b51-153">REST API의 모든 참조 문서를 보려면 [Ambari API 참조 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5b51-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="c5b51-154">예: 클러스터 노드의 FQDN 가져오기</span><span class="sxs-lookup"><span data-stu-id="c5b51-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="c5b51-155">HDInsight에서 작업할 때 클러스터 노드의 정규화된 도메인 이름(FQDN)에 대해 알아야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="c5b51-156">다음 예제를 사용하여 클러스터의 다양한 노드에 대한 FQDN을 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="c5b51-157">**모든 노드**</span><span class="sxs-lookup"><span data-stu-id="c5b51-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="c5b51-158">**헤드 노드**</span><span class="sxs-lookup"><span data-stu-id="c5b51-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="c5b51-159">**작업자 노드**</span><span class="sxs-lookup"><span data-stu-id="c5b51-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="c5b51-160">**Zookeeper 노드**</span><span class="sxs-lookup"><span data-stu-id="c5b51-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="c5b51-161">예제: 클러스터 노드의 내부 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="c5b51-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5b51-162">이 섹션의 예제에서 반환된 IP 주소는 인터넷을 통해 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="c5b51-163">HDInsight 클러스터를 포함하는 Azure Virtual Network 내에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="c5b51-164">HDInsight 및 가상 네트워크 작업에 대한 자세한 내용은 [사용자 지정 Azure Virtual Network를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5b51-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="c5b51-165">IP 주소를 찾으려면 클러스터 노드의 내부 FQDN(정규화된 도메인 이름)을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="c5b51-166">FQDN을 알고 있으므로 호스트의 IP 주소를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="c5b51-167">다음 예제에서는 먼저 Ambari를 쿼리하여 모든 호스트 노드의 FQDN을 알아낸 다음 다시 Ambari를 쿼리하여 각 호스트의 IP 주소를 알아냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="c5b51-168">예제: 기본 저장소 가져오기</span><span class="sxs-lookup"><span data-stu-id="c5b51-168">Example: Get the default storage</span></span>

<span data-ttu-id="c5b51-169">HDInsight 클러스터를 만드는 경우 Azure Storage 계정 또는 Data Lake Store를 클러스터에 대한 기본 저장소로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="c5b51-170">클러스터를 만든 후 Ambari를 사용하여 이 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="c5b51-171">예를 들어 HDInsight 외부 컨테이너에 데이터를 읽고 쓰려는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="c5b51-172">다음 예제에서는 클러스터에서 기본 저장소 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="c5b51-173">이러한 예제는 서버(`service_config_version=1`)에 적용된 첫 번째 구성을 반환하며 이 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="c5b51-174">클러스터를 만든 후에 수정된 값을 검색하는 경우 구성 버전을 나열하고 최신 버전을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="c5b51-175">반환 값은 다음 예제 중 하나와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="c5b51-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - 이 값은 클러스터에서 기본 저장소에 Azure Storage 계정을 사용하고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="c5b51-177">`ACCOUNTNAME` 값은 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="c5b51-178">`CONTAINER` 부분은 저장소 계정에서 blob 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="c5b51-179">이 컨테이너는 클러스터에 대한 HDFS 호환 저장소의 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="c5b51-180">`adl://home` - 이 값은 클러스터가 기본 저장소에 Azure Data Lake Store를 사용하고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="c5b51-181">Data Lake Store 계정 이름을 찾으려면 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-181">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="c5b51-182">반환 값은 `ACCOUNTNAME.azuredatalakestore.net`과 비슷합니다. 여기서 `ACCOUNTNAME`은 Data Lake Store 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="c5b51-183">Data Lake Store 내에서 클러스터에 대한 저장소를 포함하는 디렉터리를 찾으려면 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="c5b51-184">반환 값은 `/clusters/CLUSTERNAME/`과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="c5b51-185">이 값은 Data Lake Store 계정 내의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="c5b51-186">이 경로는 클러스터에 대한 HDFS 호환 파일 시스템의 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="c5b51-187">[Azure PowerShell](/powershell/azure/overview)에서 제공하는 `Get-AzureRmHDInsightCluster` cmdlet 또한 클러스터에 대한 저장소 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="c5b51-188">예제: 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="c5b51-188">Example: Get configuration</span></span>

1. <span data-ttu-id="c5b51-189">클러스터에 사용할 수 있는 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="c5b51-190">이 예제는 클러스터에 설치된 구성 요소에 대한 현재 구성이 포함된 JSON 문서(*tag* 값으로 식별됨)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="c5b51-191">다음 예제는 Spark 클러스터 형식에서 반환된 데이터에서 발췌한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="c5b51-192">관심 있는 구성 요소에 대한 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="c5b51-193">다음 예제에서는 이전 요청에서 반환된 태그 값으로 `INITIAL`을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="c5b51-194">이 예제는 `core-site` 구성 요소에 대한 현재 구성을 포함하는 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="c5b51-195">예제: 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="c5b51-195">Example: Update configuration</span></span>

1. <span data-ttu-id="c5b51-196">Ambari에서 "필요한 구성"으로 저장하는 현재 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="c5b51-197">이 예제는 클러스터에 설치된 구성 요소에 대한 현재 구성이 포함된 JSON 문서(*tag* 값으로 식별됨)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="c5b51-198">다음 예제는 Spark 클러스터 형식에서 반환된 데이터에서 발췌한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="c5b51-199">이 목록에서 구성 요소의 이름(예: **spark\_thrift\_sparkconf** 및 **tag** 값을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="c5b51-200">다음 명령을 사용하여 구성 요소 및 태그의 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="c5b51-201">**spark-thrift-sparkconf** 및 **INITIAL**을 검색할 구성 요소 및 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="c5b51-202">Jq는 HDInsight에서 검색한 데이터를 새 구성 템플릿으로 반환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="c5b51-203">특히, 이러한 예제에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="c5b51-204">문자열 "version" 및 날짜를 포함하는 고유 값을 만듭니다. 이 값은 `newtag`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="c5b51-205">필요한 새 구성의 루트 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="c5b51-206">`.items[]` 배열의 내용을 가져와서 **desired_config** 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="c5b51-207">`href`, `version`, and `Config` 요소는 새 구성을 제출하는 데 필요하지 않으므로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="c5b51-208">값이 `version#################`인 `tag` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="c5b51-209">숫자 부분은 현재 날짜를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="c5b51-210">각 구성에 고유한 태그가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="c5b51-211">마지막으로 데이터가 `newconfig.json` 문서에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="c5b51-212">문서 구조는 다음 예제와 유사하게 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-212">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="c5b51-213">`newconfig.json` 문서를 열고 `properties` 개체의 값을 수정/추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="c5b51-214">다음 예제는 `"spark.yarn.am.memory"` 값을 `"1g"`에서 `"3g"`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="c5b51-215">또한 값이 `"256m"`인 `"spark.kryoserializer.buffer.max"`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="c5b51-216">수정을 완료했으면 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="c5b51-217">다음 명령을 사용하여 업데이트된 구성을 Ambari에 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="c5b51-218">이러한 명령은 **newconfig.json** 파일의 내용을 새 구성으로 클러스터에 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="c5b51-219">이 요청은 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-219">The request returns a JSON document.</span></span> <span data-ttu-id="c5b51-220">이 문서의 **versionTag** 요소는 제출한 버전과 일치해야 하며, **configs** 개체에는 요청한 구성 변경 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="c5b51-221">예: 서비스 구성 요소 다시 시작</span><span class="sxs-lookup"><span data-stu-id="c5b51-221">Example: Restart a service component</span></span>

<span data-ttu-id="c5b51-222">이제 새 구성을 적용하려면 먼저 Spark 서비스를 다시 시작해야 한다는 메시지가 Ambari 웹 UI에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="c5b51-223">다음 단계를 사용하여 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="c5b51-224">다음을 사용하여 Spark 서비스에 대한 유지 관리 모드를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-224">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="c5b51-225">이러한 명령은 서버에 JSON 문서를 보내 유지 관리 모드를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="c5b51-226">이제 다음 요청을 사용하여 서비스가 유지 관리 모드인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="c5b51-227">반환 값은 `ON`입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="c5b51-228">그런 후 다음을 사용하여 서비스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-228">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="c5b51-229">응답은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-229">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="c5b51-230">이 URI에서 반환된 `href` 값은 클러스터 노드의 내부 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="c5b51-231">클러스터 외부에서 이를 사용하려면 '10.0.0.18:8080' 부분을 클러스터의 FQDN으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="c5b51-232">다음 명령은 요청의 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-232">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="c5b51-233">응답 `COMPLETED`는 요청이 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="c5b51-234">이전 요청이 완료되면 다음을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-234">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="c5b51-235">이제 서비스는 새 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="c5b51-236">마지막으로, 다음을 사용하여 유지 관리 모드를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b51-236">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="c5b51-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5b51-237">Next steps</span></span>

<span data-ttu-id="c5b51-238">REST API의 모든 참조 문서를 보려면 [Ambari API 참조 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5b51-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

