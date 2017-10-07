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
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Hello Ambari REST API를 사용 하 여 HDInsight 클러스터를 관리 합니다.

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Toouse Ambari REST API toomanage hello 하 고 Azure HDInsight의 Hadoop 클러스터를 모니터링 하는 방법에 대해 알아봅니다.

Apache Ambari hello 관리 및 쉽게 toouse 웹 UI 및 REST API를 제공 하 여 Hadoop 클러스터의 모니터링을 간소화 합니다. Ambari는 hello Linux 운영 체제를 사용 하는 HDInsight 클러스터에 포함 됩니다. Ambari toomonitor hello 클러스터를 사용할 수 있으며 구성을 변경할 수 있습니다.

## <a id="whatis"></a>Ambari 정의

[Apache Ambari](http://ambari.apache.org) 웹 사용된 tooprovision 수, 관리 및 Hadoop 클러스터를 모니터링할 수 있는 UI를 제공 합니다. 개발자 hello를 사용 하 여 응용 프로그램에 이러한 기능을 통합할 수 [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.

Ambari는 Linux 기반 HDInsight 클러스터를 기본으로 제공합니다.

## <a name="how-toouse-hello-ambari-rest-api"></a>어떻게 toouse hello Ambari REST API

> [!IMPORTANT]
> hello 정보 및이 설명서의 예제에는 Linux 운영 체제를 사용 하는 HDInsight 클러스터가 필요 합니다. 자세한 내용은 [HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.

이 문서에 hello 예제는 hello Bourne 셸 (bash) 및 PowerShell 모두에 대해 제공 됩니다. 예제 GNU를 사용 하 여 테스트 된 hello bash 4.3.11를 이용한 적 하지만 다른 Unix 셸 함께 사용할 수 있어야 합니다. hello PowerShell 예에서는 PowerShell 5.0과 함께 테스트 된 제외한 및 PowerShell 3.0 이상이 작동 해야 합니다.

Hello를 사용 하는 경우 __Bourne 셸__ (Bash) hello 다음이 설치 되어 있어야 합니다.

* [cURL](http://curl.haxx.se/): cURL는 hello 명령줄에서 REST Api를 사용 하는 toowork 일 수 있는 유틸리티입니다. 이 문서에서 사용 되는 toocommunicate hello Ambari REST API로입니다.

Bash 또는 PowerShell을 사용할 경우 [jq](https://stedolan.github.io/jq/)도 설치되어 있어야 합니다. Jq는 JSON 문서를 사용하기 위한 유틸리티입니다. 사용 되는 **모든** Bash 예제 hello 및 **하나의** hello PowerShell 예제입니다.

### <a name="base-uri-for-ambari-rest-api"></a>Ambari REST API의 기본 URI

hello hello HDInsight의 Ambari REST API에 대 한 기본 URI는 https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, 여기서 **CLUSTERNAME** hello 클러스터 이름입니다.

> [!IMPORTANT]
> Hello에서 hello 클러스터 이름을 정규화 하는 동안 URI (CLUSTERNAME.azurehdinsight.net) hello의 도메인 이름 (FQDN) 부분은 대/소문자 구분, hello URI에서에서 발생할 수 있는 다른는 대/소문자 구분입니다. 예를 들어, 클러스터의 이름이 `MyCluster`, hello 다음은 유효한 Uri:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> 대/소문자를 수정 하는 hello 다음 Uri는 hello hello 이름의 두 번째 항목은 hello 하지 때문에 오류를 반환 합니다.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>인증

HTTPS 필요 tooAmbari HDInsight에 연결 합니다. 사용 하 여 hello 관리자 계정 이름 (hello 기본값은 **admin**) 및 클러스터를 만드는 동안 지정한 암호입니다.

## <a name="examples-authentication-and-parsing-json"></a>예제: 인증 및 JSON 구문 분석

다음 예제는 hello toomake hello에 대 한 GET 요청의 Ambari REST API를 기반 하는 방법을 보여 줍니다.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> 이 설명서의 hello Bash 예제 hello 다음 가정을 확인 합니다.
>
> * hello 클러스터에 대 한 로그인 이름을 hello의 hello 기본값은 `admin`합니다.
> * `$PASSWORD`hello HDInsight 로그인 명령에 대 한 hello 암호를 포함합니다. `PASSWORD='mypassword'`을 사용하여 이 값을 설정할 수 있습니다.
> * `$CLUSTERNAME`hello 클러스터의 hello 이름을 포함합니다. `set CLUSTERNAME='clustername'`을 사용하여 이 값을 설정할 수 있습니다.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> 이 문서에서 PowerShell 예제를 hello hello 다음 가정을 확인 합니다.
>
> * `$creds`hello 관리자 로그인과 hello 클러스터에 대 한 암호를 포함 하는 자격 증명 개체가입니다. 사용 하 여이 값을 설정할 수 `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` 하 고 메시지가 표시 되 면 hello 자격 증명을 제공 합니다.
> * `$clusterName`hello 클러스터의 hello 이름이 포함 된 문자열이입니다. `$clusterName="clustername"`을 사용하여 이 값을 설정할 수 있습니다.

다음 예제와 비슷한 toohello를 정보로 시작 하는 JSON 문서를 반환 하는 두 예제:

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

### <a name="parsing-json-data"></a>JSON 데이터 구문 분석

hello 다음 예제에서는 `jq` tooparse JSON 응답 문서 hello 및 표시만 hello `health_report` hello 결과에서 정보입니다.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 이상 제공 hello `ConvertFrom-Json` cmdlet는 PowerShell에서 보다 쉽게 toowork 사용 되는 개체가으로 hello JSON 문서를 변환 합니다. hello 다음 예제에서는 `ConvertFrom-Json` toodisplay만 hello `health_report` hello 결과에서 정보입니다.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> 대부분의 예제가 문서에서는 동안 `ConvertFrom-Json` hello 응답 문서에서 요소를 toodisplay hello [업데이트 Ambari 구성](#example-update-ambari-configuration) jq을 사용 하 여 예제입니다. 이 예제에서는 tooconstruct Jq는 hello JSON 응답 문서에서 새 템플릿을 합니다.

Hello REST API의 모든 참조를 참조 하십시오. [Ambari API 참조 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>예: hello 클러스터 노드의 FQDN 가져오기

HDInsight를 사용할 때에 클러스터 노드의 tooknow hello 정규화 된 도메인 이름 (FQDN)를 할 수 있습니다. 쉽게 예제 따르는 hello를 사용 하 여 hello 클러스터에서 다양 한 노드 hello에 대 한 FQDN hello를 검색할 수 있습니다.

* **모든 노드**

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

* **헤드 노드**

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

* **작업자 노드**

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

* **Zookeeper 노드**

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>예: 클러스터 노드의 hello 내부 IP 주소 가져오기

> [!IMPORTANT]
> 이 섹션의 hello 예제에서 반환 된 hello IP 주소에는 액세스할 수 있는 조치 hello 인터넷 직접는입니다. Hello hello HDInsight 클러스터를 포함 하는 Azure 가상 네트워크 내에서 액세스할 수만 됩니다.
>
> HDInsight 및 가상 네트워크 작업에 대한 자세한 내용은 [사용자 지정 Azure Virtual Network를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.

toofind hello IP 주소를 hello 내부 정규화 된 도메인 이름 (FQDN) hello의 클러스터 노드를 알고 있어야 합니다. FQDN hello를 만든 후에 다음 hello 호스트의 hello IP 주소를 가져올 수 있습니다. hello 다음 예에서는 먼저 Ambari hello 모든 hello 호스트 노드 FQDN에 대 한 쿼리 다음 각 호스트의 IP 주소 hello Ambari를 쿼리 합니다.

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

## <a name="example-get-hello-default-storage"></a>예: hello 기본 저장소 가져오기

HDInsight 클러스터를 만들 때 사용 해야 Azure 저장소 계정 또는 데이터 레이크 저장소 hello 기본 저장소로 hello 클러스터에 대 한 합니다. Hello 클러스터를 만든 후이 정보 Ambari tooretrieve을 사용할 수 있습니다. 예를 들어, HDInsight 외부 tooread/쓰기 데이터 toohello 컨테이너에 들어 있습니다.

hello 다음 예제에서는 hello 기본 저장소 구성에서에서 검색 hello 클러스터:

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
> 첫 번째 적용 된 구성을 toohello 서버 hello를 반환 하는 이러한 예제 (`service_config_version=1`)는이 정보를 포함 합니다. 클러스터를 만든 후 수정 된 값을 검색 하는 경우에 toolist hello 구성 버전 해야 하는 수 고 hello 최신을 검색할 수 있습니다.

hello 반환 값은 예제 따르는 hello의 유사한 tooone:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-이 값 해당 hello 클러스터 기본 저장소에 대 한 Azure 저장소 계정을 사용 하는 것을 나타냅니다. hello `ACCOUNTNAME` 값은 hello hello 저장소 계정의 이름입니다. hello `CONTAINER` 부분 hello hello 저장소 계정의 blob 컨테이너의 hello 이름입니다. hello 컨테이너는 hello hello 클러스터에 대 한 HDFS 호환 되는 저장소의 hello 루트입니다.

* `adl://home`-이 값 해당 hello 클러스터에서 기본 저장소에 Azure 데이터 레이크 저장소를 사용 하는 것을 나타냅니다.

    Data Lake 저장소 계정 이름 toofind hello 예제 따르는 hello를 사용 합니다.

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

    hello 반환 값은 유사한 너무`ACCOUNTNAME.azuredatalakestore.net`여기서 `ACCOUNTNAME` hello hello Data Lake 저장소 계정 이름입니다.

    사용 하 여 hello 예제 따르는 hello 클러스터용 hello 저장소를 포함 하는 데이터 레이크 저장소 내에서 toofind hello 디렉터리:

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

    hello 반환 값은 유사한 너무`/clusters/CLUSTERNAME/`합니다. 이 값은 hello Data Lake 저장소 계정 내의 경로입니다. 이 경로 hello hello 클러스터에 대 한 HDFS 호환 되는 파일 시스템의 hello 루트입니다. 

> [!NOTE]
> hello `Get-AzureRmHDInsightCluster` 에서 제공 하는 cmdlet [Azure PowerShell](/powershell/azure/overview) 도 반환 hello hello 클러스터에 대 한 저장소 정보입니다.


## <a name="example-get-configuration"></a>예제: 구성 가져오기

1. 클러스터에 대해 사용할 수 있는 hello 구성을 가져옵니다.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    이 예에서는 반환 hello 현재 구성이 포함 된 JSON 문서 (hello로 식별 되 *태그* 값) hello 클러스터에 설치 하는 hello 구성 요소에 대 한 합니다. hello 다음 예제는 Spark 클러스터 유형에서 반환 된 hello 데이터에서 발췌 한 내용입니다.
   
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

2. 관심이 있는 hello 구성 요소에 대 한 hello 구성을 가져옵니다. Hello에서 다음 예제에서는 대체 `INITIAL` hello 이전 요청에서 반환 된 hello 태그 값을 사용 합니다.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Hello hello에 대 한 현재 구성이 포함 된 JSON 문서를 반환 하는이 예제 `core-site` 구성 요소입니다.

## <a name="example-update-configuration"></a>예제: 구성 업데이트

1. Ambari hello "원하는 구성"으로 저장 하는 hello 현재 구성을 가져오려면

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    이 예에서는 반환 hello 현재 구성이 포함 된 JSON 문서 (hello로 식별 되 *태그* 값) hello 클러스터에 설치 하는 hello 구성 요소에 대 한 합니다. hello 다음 예제는 Spark 클러스터 유형에서 반환 된 hello 데이터에서 발췌 한 내용입니다.
   
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
   
    이 목록에서 필요한 toocopy hello hello 구성 요소의 이름입니다 (예를 들어 **spark\_thrift\_sparkconf** 및 hello **태그** 값입니다.

2. 다음 명령 hello를 사용 하 여 hello 구성 요소 및 태그에 대 한 hello 구성 검색:
   
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
    > 대체 **spark-thrift-sparkconf** 및 **초기** hello 구성 요소와 tooretrieve hello 구성에 대 한 원하는 태그입니다.
   
    Jq는 HDInsight에서 검색 한 새로운 구성 템플릿을 사용 하는 tooturn hello 데이터입니다. 특히,이 예에서는 hello 다음 작업을 수행 합니다.
   
    * Hello 문자열 "version" 및 hello 날짜에 저장 되는 포함 된 고유한 값을 만듭니다 `newtag`합니다.

    * Hello 새 원하는 구성에 대 한 루트 문서를 만듭니다.

    * 가져옵니다 hello hello의 내용을 `.items[]` 배열 하 고 hello에서 추가 **desired_config** 요소입니다.

    * 삭제 hello `href`, `version`, 및 `Config` 요소를 이러한 요소로 아닌 필요한 toosubmit 새 구성 합니다.

    * 값이 `version#################`인 `tag` 요소를 추가합니다. hello 숫자 부분을 기반으로 hello 현재 날짜입니다. 각 구성에 고유한 태그가 있어야 합니다.
     
    마지막으로, hello 데이터 저장 toohello `newconfig.json` 문서. hello 문서 구조에는 다음 예제와 비슷한 toohello 같아야 합니다.
     
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

3. 열기 hello `newconfig.json` hello에서 문서 및 수정/추가 값 `properties` 개체입니다. hello 다음 예제에서는 변경 내용을 hello 값 `"spark.yarn.am.memory"` 에서 `"1g"` 너무`"3g"`합니다. 또한 값이 `"256m"`인 `"spark.kryoserializer.buffer.max"`를 추가합니다.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    수정이 완료 되 면 hello 파일을 저장 합니다.

4. 다음 명령을 toosubmit 업데이트 hello 구성 tooAmbari hello를 사용 합니다.
   
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
   
    이 명령은 제출 hello 내용의 hello **newconfig.json** hello 새로운 필요한 구성 toohello 클러스터의 파일입니다. hello 요청 JSON 문서를 반환합니다. hello **versionTag** 이 문서에서 요소, 전송 및 hello hello 버전 일치 해야 **configs** 개체에는 요청한 hello 구성 변경 내용이 포함 되어 있습니다.

### <a name="example-restart-a-service-component"></a>예: 서비스 구성 요소 다시 시작

이 시점에서 hello Ambari web UI 보면 hello Spark 서비스 toobe hello 새 구성을 적용 하기 전에 다시 시작 필요 함을 나타냅니다. 단계 toorestart hello 서비스는 hello를 사용 합니다.

1. Hello Spark 서비스에 대 한 유지 관리 모드 tooenable 다음 hello를 사용 합니다.

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
   
    이 명령은 유지 관리 모드를 설정 하는 JSON 문서 toohello 서버를 보냅니다. 이제 hello 서비스 요청을 수행 하는 hello를 사용 하 여 유지 관리 모드 인지 확인할 수 있습니다.
   
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
   
    hello 반환 값은 `ON`합니다.

2. 를 사용 하 여 hello tooturn hello 서비스 해제를 수행 합니다.

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
    
    hello 응답은 다음 예제와 비슷한 toohello입니다.
   
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
    > hello `href` 이 URI에서 반환 된 값 hello 클러스터 노드의 hello 내부 IP 주소를 사용 합니다. toouse hello hello 클러스터의 FQDN '10.0.0.18:8080' hello 부분 외부 hello 클러스터에서 대체 합니다. 
    
    hello 요청의 hello 상태를 검색 하는 명령을 수행 하는 hello:

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

    응답 `COMPLETED` 해당 hello 요청을 완료 했음을 나타냅니다.

3. Hello 이전 요청이 완료 되 면 hello toostart hello 서비스를 사용 합니다.
   
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
    hello 서비스는 이제 hello 새 구성을 사용 해야 합니다.

4. 마지막으로, 다음 유지 관리 모드 tooturn hello를 사용 합니다.
   
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

## <a name="next-steps"></a>다음 단계

Hello REST API의 모든 참조를 참조 하십시오. [Ambari API 참조 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.

