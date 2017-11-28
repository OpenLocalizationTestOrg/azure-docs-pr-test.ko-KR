---
title: "aaaMonitor Ambari REST api-Azure HDInsight Hadoop 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Ambari toomonitor 및 Azure HDInsight의 Hadoop 클러스터를 관리 합니다. 이 문서에서는 toouse hello Ambari REST API에 포함 된 HDInsight 클러스터 방법을 배웁니다."
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
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="b8b3d-104">Hello Ambari REST API를 사용 하 여 HDInsight 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="b8b3d-105">Toouse Ambari REST API toomanage hello 하 고 Azure HDInsight의 Hadoop 클러스터를 모니터링 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="b8b3d-106">Apache Ambari hello 관리 및 쉽게 toouse 웹 UI 및 REST API를 제공 하 여 Hadoop 클러스터의 모니터링을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="b8b3d-107">Ambari는 hello Linux 운영 체제를 사용 하는 HDInsight 클러스터에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="b8b3d-108">Ambari toomonitor hello 클러스터를 사용할 수 있으며 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="b8b3d-109"><a id="whatis"></a>Ambari 정의</span><span class="sxs-lookup"><span data-stu-id="b8b3d-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="b8b3d-110">[Apache Ambari](http://ambari.apache.org) 웹 사용된 tooprovision 수, 관리 및 Hadoop 클러스터를 모니터링할 수 있는 UI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="b8b3d-111">개발자 hello를 사용 하 여 응용 프로그램에 이러한 기능을 통합할 수 [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="b8b3d-112">Ambari는 Linux 기반 HDInsight 클러스터를 기본으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="b8b3d-113">어떻게 toouse hello Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="b8b3d-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8b3d-114">hello 정보 및이 설명서의 예제에는 Linux 운영 체제를 사용 하는 HDInsight 클러스터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="b8b3d-115">자세한 내용은 [HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="b8b3d-116">이 문서에 hello 예제는 hello Bourne 셸 (bash) 및 PowerShell 모두에 대해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="b8b3d-117">예제 GNU를 사용 하 여 테스트 된 hello bash 4.3.11를 이용한 적 하지만 다른 Unix 셸 함께 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="b8b3d-118">hello PowerShell 예에서는 PowerShell 5.0과 함께 테스트 된 제외한 및 PowerShell 3.0 이상이 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="b8b3d-119">Hello를 사용 하는 경우 __Bourne 셸__ (Bash) hello 다음이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="b8b3d-120">[cURL](http://curl.haxx.se/): cURL는 hello 명령줄에서 REST Api를 사용 하는 toowork 일 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="b8b3d-121">이 문서에서 사용 되는 toocommunicate hello Ambari REST API로입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="b8b3d-122">Bash 또는 PowerShell을 사용할 경우 [jq](https://stedolan.github.io/jq/)도 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="b8b3d-123">Jq는 JSON 문서를 사용하기 위한 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="b8b3d-124">사용 되는 **모든** Bash 예제 hello 및 **하나의** hello PowerShell 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="b8b3d-125">Ambari REST API의 기본 URI</span><span class="sxs-lookup"><span data-stu-id="b8b3d-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="b8b3d-126">hello hello HDInsight의 Ambari REST API에 대 한 기본 URI는 https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, 여기서 **CLUSTERNAME** hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8b3d-127">Hello에서 hello 클러스터 이름을 정규화 하는 동안 URI (CLUSTERNAME.azurehdinsight.net) hello의 도메인 이름 (FQDN) 부분은 대/소문자 구분, hello URI에서에서 발생할 수 있는 다른는 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="b8b3d-128">예를 들어, 클러스터의 이름이 `MyCluster`, hello 다음은 유효한 Uri:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="b8b3d-129">대/소문자를 수정 하는 hello 다음 Uri는 hello hello 이름의 두 번째 항목은 hello 하지 때문에 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="b8b3d-130">인증</span><span class="sxs-lookup"><span data-stu-id="b8b3d-130">Authentication</span></span>

<span data-ttu-id="b8b3d-131">HTTPS 필요 tooAmbari HDInsight에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="b8b3d-132">사용 하 여 hello 관리자 계정 이름 (hello 기본값은 **admin**) 및 클러스터를 만드는 동안 지정한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="b8b3d-133">예제: 인증 및 JSON 구문 분석</span><span class="sxs-lookup"><span data-stu-id="b8b3d-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="b8b3d-134">다음 예제는 hello toomake hello에 대 한 GET 요청의 Ambari REST API를 기반 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="b8b3d-135">이 설명서의 hello Bash 예제 hello 다음 가정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="b8b3d-136">hello 클러스터에 대 한 로그인 이름을 hello의 hello 기본값은 `admin`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="b8b3d-137">`$PASSWORD`hello HDInsight 로그인 명령에 대 한 hello 암호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="b8b3d-138">`PASSWORD='mypassword'`을 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="b8b3d-139">`$CLUSTERNAME`hello 클러스터의 hello 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="b8b3d-140">`set CLUSTERNAME='clustername'`을 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="b8b3d-141">이 문서에서 PowerShell 예제를 hello hello 다음 가정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="b8b3d-142">`$creds`hello 관리자 로그인과 hello 클러스터에 대 한 암호를 포함 하는 자격 증명 개체가입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="b8b3d-143">사용 하 여이 값을 설정할 수 `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` 하 고 메시지가 표시 되 면 hello 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="b8b3d-144">`$clusterName`hello 클러스터의 hello 이름이 포함 된 문자열이입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="b8b3d-145">`$clusterName="clustername"`을 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="b8b3d-146">다음 예제와 비슷한 toohello를 정보로 시작 하는 JSON 문서를 반환 하는 두 예제:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="b8b3d-147">JSON 데이터 구문 분석</span><span class="sxs-lookup"><span data-stu-id="b8b3d-147">Parsing JSON data</span></span>

<span data-ttu-id="b8b3d-148">hello 다음 예제에서는 `jq` tooparse JSON 응답 문서 hello 및 표시만 hello `health_report` hello 결과에서 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="b8b3d-149">PowerShell 3.0 이상 제공 hello `ConvertFrom-Json` cmdlet는 PowerShell에서 보다 쉽게 toowork 사용 되는 개체가으로 hello JSON 문서를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="b8b3d-150">hello 다음 예제에서는 `ConvertFrom-Json` toodisplay만 hello `health_report` hello 결과에서 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="b8b3d-151">대부분의 예제가 문서에서는 동안 `ConvertFrom-Json` hello 응답 문서에서 요소를 toodisplay hello [업데이트 Ambari 구성](#example-update-ambari-configuration) jq을 사용 하 여 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="b8b3d-152">이 예제에서는 tooconstruct Jq는 hello JSON 응답 문서에서 새 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="b8b3d-153">Hello REST API의 모든 참조를 참조 하십시오. [Ambari API 참조 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="b8b3d-154">예: hello 클러스터 노드의 FQDN 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8b3d-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="b8b3d-155">HDInsight를 사용할 때에 클러스터 노드의 tooknow hello 정규화 된 도메인 이름 (FQDN)를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="b8b3d-156">쉽게 예제 따르는 hello를 사용 하 여 hello 클러스터에서 다양 한 노드 hello에 대 한 FQDN hello를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="b8b3d-157">**모든 노드**</span><span class="sxs-lookup"><span data-stu-id="b8b3d-157">**All nodes**</span></span>

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

* <span data-ttu-id="b8b3d-158">**헤드 노드**</span><span class="sxs-lookup"><span data-stu-id="b8b3d-158">**Head nodes**</span></span>

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

* <span data-ttu-id="b8b3d-159">**작업자 노드**</span><span class="sxs-lookup"><span data-stu-id="b8b3d-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="b8b3d-160">**Zookeeper 노드**</span><span class="sxs-lookup"><span data-stu-id="b8b3d-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="b8b3d-161">예: 클러스터 노드의 hello 내부 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8b3d-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8b3d-162">이 섹션의 hello 예제에서 반환 된 hello IP 주소에는 액세스할 수 있는 조치 hello 인터넷 직접는입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="b8b3d-163">Hello hello HDInsight 클러스터를 포함 하는 Azure 가상 네트워크 내에서 액세스할 수만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="b8b3d-164">HDInsight 및 가상 네트워크 작업에 대한 자세한 내용은 [사용자 지정 Azure Virtual Network를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="b8b3d-165">toofind hello IP 주소를 hello 내부 정규화 된 도메인 이름 (FQDN) hello의 클러스터 노드를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="b8b3d-166">FQDN hello를 만든 후에 다음 hello 호스트의 hello IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="b8b3d-167">hello 다음 예에서는 먼저 Ambari hello 모든 hello 호스트 노드 FQDN에 대 한 쿼리 다음 각 호스트의 IP 주소 hello Ambari를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="b8b3d-168">예: hello 기본 저장소 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8b3d-168">Example: Get hello default storage</span></span>

<span data-ttu-id="b8b3d-169">HDInsight 클러스터를 만들 때 사용 해야 Azure 저장소 계정 또는 데이터 레이크 저장소 hello 기본 저장소로 hello 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="b8b3d-170">Hello 클러스터를 만든 후이 정보 Ambari tooretrieve을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="b8b3d-171">예를 들어, HDInsight 외부 tooread/쓰기 데이터 toohello 컨테이너에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="b8b3d-172">hello 다음 예제에서는 hello 기본 저장소 구성에서에서 검색 hello 클러스터:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="b8b3d-173">첫 번째 적용 된 구성을 toohello 서버 hello를 반환 하는 이러한 예제 (`service_config_version=1`)는이 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="b8b3d-174">클러스터를 만든 후 수정 된 값을 검색 하는 경우에 toolist hello 구성 버전 해야 하는 수 고 hello 최신을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="b8b3d-175">hello 반환 값은 예제 따르는 hello의 유사한 tooone:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="b8b3d-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-이 값 해당 hello 클러스터 기본 저장소에 대 한 Azure 저장소 계정을 사용 하는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="b8b3d-177">hello `ACCOUNTNAME` 값은 hello hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="b8b3d-178">hello `CONTAINER` 부분 hello hello 저장소 계정의 blob 컨테이너의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="b8b3d-179">hello 컨테이너는 hello hello 클러스터에 대 한 HDFS 호환 되는 저장소의 hello 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="b8b3d-180">`adl://home`-이 값 해당 hello 클러스터에서 기본 저장소에 Azure 데이터 레이크 저장소를 사용 하는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="b8b3d-181">Data Lake 저장소 계정 이름 toofind hello 예제 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="b8b3d-182">hello 반환 값은 유사한 너무`ACCOUNTNAME.azuredatalakestore.net`여기서 `ACCOUNTNAME` hello hello Data Lake 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="b8b3d-183">사용 하 여 hello 예제 따르는 hello 클러스터용 hello 저장소를 포함 하는 데이터 레이크 저장소 내에서 toofind hello 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="b8b3d-184">hello 반환 값은 유사한 너무`/clusters/CLUSTERNAME/`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="b8b3d-185">이 값은 hello Data Lake 저장소 계정 내의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="b8b3d-186">이 경로 hello hello 클러스터에 대 한 HDFS 호환 되는 파일 시스템의 hello 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="b8b3d-187">hello `Get-AzureRmHDInsightCluster` 에서 제공 하는 cmdlet [Azure PowerShell](/powershell/azure/overview) 도 반환 hello hello 클러스터에 대 한 저장소 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="b8b3d-188">예제: 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8b3d-188">Example: Get configuration</span></span>

1. <span data-ttu-id="b8b3d-189">클러스터에 대해 사용할 수 있는 hello 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="b8b3d-190">이 예에서는 반환 hello 현재 구성이 포함 된 JSON 문서 (hello로 식별 되 *태그* 값) hello 클러스터에 설치 하는 hello 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="b8b3d-191">hello 다음 예제는 Spark 클러스터 유형에서 반환 된 hello 데이터에서 발췌 한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="b8b3d-192">관심이 있는 hello 구성 요소에 대 한 hello 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="b8b3d-193">Hello에서 다음 예제에서는 대체 `INITIAL` hello 이전 요청에서 반환 된 hello 태그 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="b8b3d-194">Hello hello에 대 한 현재 구성이 포함 된 JSON 문서를 반환 하는이 예제 `core-site` 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="b8b3d-195">예제: 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="b8b3d-195">Example: Update configuration</span></span>

1. <span data-ttu-id="b8b3d-196">Ambari hello "원하는 구성"으로 저장 하는 hello 현재 구성을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="b8b3d-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="b8b3d-197">이 예에서는 반환 hello 현재 구성이 포함 된 JSON 문서 (hello로 식별 되 *태그* 값) hello 클러스터에 설치 하는 hello 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="b8b3d-198">hello 다음 예제는 Spark 클러스터 유형에서 반환 된 hello 데이터에서 발췌 한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="b8b3d-199">이 목록에서 필요한 toocopy hello hello 구성 요소의 이름입니다 (예를 들어 **spark\_thrift\_sparkconf** 및 hello **태그** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="b8b3d-200">다음 명령 hello를 사용 하 여 hello 구성 요소 및 태그에 대 한 hello 구성 검색:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="b8b3d-201">대체 **spark-thrift-sparkconf** 및 **초기** hello 구성 요소와 tooretrieve hello 구성에 대 한 원하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="b8b3d-202">Jq는 HDInsight에서 검색 한 새로운 구성 템플릿을 사용 하는 tooturn hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="b8b3d-203">특히,이 예에서는 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="b8b3d-204">Hello 문자열 "version" 및 hello 날짜에 저장 되는 포함 된 고유한 값을 만듭니다 `newtag`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="b8b3d-205">Hello 새 원하는 구성에 대 한 루트 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="b8b3d-206">가져옵니다 hello hello의 내용을 `.items[]` 배열 하 고 hello에서 추가 **desired_config** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="b8b3d-207">삭제 hello `href`, `version`, 및 `Config` 요소를 이러한 요소로 아닌 필요한 toosubmit 새 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="b8b3d-208">값이 `version#################`인 `tag` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="b8b3d-209">hello 숫자 부분을 기반으로 hello 현재 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="b8b3d-210">각 구성에 고유한 태그가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="b8b3d-211">마지막으로, hello 데이터 저장 toohello `newconfig.json` 문서.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="b8b3d-212">hello 문서 구조에는 다음 예제와 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="b8b3d-213">열기 hello `newconfig.json` hello에서 문서 및 수정/추가 값 `properties` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="b8b3d-214">hello 다음 예제에서는 변경 내용을 hello 값 `"spark.yarn.am.memory"` 에서 `"1g"` 너무`"3g"`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="b8b3d-215">또한 값이 `"256m"`인 `"spark.kryoserializer.buffer.max"`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="b8b3d-216">수정이 완료 되 면 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="b8b3d-217">다음 명령을 toosubmit 업데이트 hello 구성 tooAmbari hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="b8b3d-218">이 명령은 제출 hello 내용의 hello **newconfig.json** hello 새로운 필요한 구성 toohello 클러스터의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="b8b3d-219">hello 요청 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-219">hello request returns a JSON document.</span></span> <span data-ttu-id="b8b3d-220">hello **versionTag** 이 문서에서 요소, 전송 및 hello hello 버전 일치 해야 **configs** 개체에는 요청한 hello 구성 변경 내용이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="b8b3d-221">예: 서비스 구성 요소 다시 시작</span><span class="sxs-lookup"><span data-stu-id="b8b3d-221">Example: Restart a service component</span></span>

<span data-ttu-id="b8b3d-222">이 시점에서 hello Ambari web UI 보면 hello Spark 서비스 toobe hello 새 구성을 적용 하기 전에 다시 시작 필요 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="b8b3d-223">단계 toorestart hello 서비스는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="b8b3d-224">Hello Spark 서비스에 대 한 유지 관리 모드 tooenable 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="b8b3d-225">이 명령은 유지 관리 모드를 설정 하는 JSON 문서 toohello 서버를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="b8b3d-226">이제 hello 서비스 요청을 수행 하는 hello를 사용 하 여 유지 관리 모드 인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="b8b3d-227">hello 반환 값은 `ON`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="b8b3d-228">를 사용 하 여 hello tooturn hello 서비스 해제를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="b8b3d-229">hello 응답은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="b8b3d-230">hello `href` 이 URI에서 반환 된 값 hello 클러스터 노드의 hello 내부 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="b8b3d-231">toouse hello hello 클러스터의 FQDN '10.0.0.18:8080' hello 부분 외부 hello 클러스터에서 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="b8b3d-232">hello 요청의 hello 상태를 검색 하는 명령을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="b8b3d-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="b8b3d-233">응답 `COMPLETED` 해당 hello 요청을 완료 했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="b8b3d-234">Hello 이전 요청이 완료 되 면 hello toostart hello 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="b8b3d-235">hello 서비스는 이제 hello 새 구성을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="b8b3d-236">마지막으로, 다음 유지 관리 모드 tooturn hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="b8b3d-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8b3d-237">Next steps</span></span>

<span data-ttu-id="b8b3d-238">Hello REST API의 모든 참조를 참조 하십시오. [Ambari API 참조 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b3d-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

