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
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>Hello Ambari API를 사용 하 여 HDInsight의 Hadoop 클러스터를 모니터링 합니다.
Ambari Api를 사용 하 여 toomonitor HDInsight 클러스터 하는 방법에 대해 알아봅니다.

> [!NOTE]
> hello이이 문서의 정보는 읽기 전용 버전의 hello Ambari REST API를 제공 하는 Windows 기반 HDInsight 클러스터를 주로입니다. Linux 기반 클러스터는 [Ambari를 사용하여 Hadoop 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.
> 
> 

## <a name="what-is-ambari"></a>Ambari 정의
[Apache Ambari][ambari-home]는 Apache Hadoop 클러스터를 프로비전, 관리 및 모니터링하는 데 사용됩니다. 직관적인 도구 컬렉션으로 연산자와 강력한 클러스터 hello 작업 단순화 Hadoop의 hello 복잡성을 숨기는 Api 집합이 포함 됩니다. Hello Api에 대 한 자세한 내용은 참조 [Ambari API 참조][ambari-api-reference]합니다. 

현재 HDInsight만 hello Ambari 모니터링 기능을 지원합니다. Ambari API 1.0은 HDInsight 클러스터 버전 3.0 및 2.1 클러스터에서만 지원됩니다. 이 문서에서는 HDInsight 버전 3.1 및 2.1 클러스터에서 Ambari API에 액세스하는 방법에 대해 설명합니다. 두 hello 사이의 hello 주요 차이점 hello 소개 새로운 기능 (예: 작업 기록 서버 hello)를 사용 하 여이 변경한 hello 구성 요소의 일부입니다. 

**필수 구성 요소**

이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure PowerShell이 포함된 워크스테이션**.
* (선택 사항)[cURL][curl]. tooinstall, 참조 [버전 및 다운로드 cURL][curl-download]합니다.
  
  > [!NOTE]
  > Windows에서 사용 하 여 큰따옴표 hello 옵션 값에 대 한 단일 따옴표 대신 hello cURL 명령을 때 사용 합니다.
  > 
  > 
* **Azure HDInsight 클러스터**. 클러스터 프로비전에 대한 자세한 내용은 [HDInsight 사용 시작][hdinsight-get-started] 또는 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요. Hello 자습서를 통해 데이터 toogo 다음 hello가 필요 합니다.
  
  | 클러스터 속성 | Azure PowerShell 변수 이름 | 값 | 설명 |
  | --- | --- | --- | --- |
  |   HDInsight 클러스터 이름 |$clusterName | |HDInsight 클러스터의 hello 이름입니다. |
  |   클러스터 사용자 이름 |$clusterUsername | |클러스터 사용자 이름이 hello 클러스터를 만들 때 지정 합니다. |
  |   클러스터 암호 |$clusterPassword | |클러스터 사용자 암호입니다. |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>신속한 시작
Toouse Ambari toomonitor HDInsight 클러스터는 여러 가지가.

**Azure PowerShell 사용**

Azure PowerShell 스크립트 뒤 hello hello MapReduce 작업 추적 장치 정보를 가져옵니다 *3.5 HDInsight 클러스터에 있습니다.*  hello 주요 차이점은 hello YARN 서비스 (MapReduce 아님)에서 이러한 세부 정보를 가져옵니다.

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

PowerShell 스크립트 뒤 hello hello MapReduce 작업 추적 장치 정보를 가져옵니다 *2.1 HDInsight 클러스터에*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

hello 출력이 생성 됩니다.

![Jobtracker 출력][img-jobtracker-output]

**cURL 사용**

hello 다음 정보를 가져오는 예제 클러스터 cURL을 사용 하 여:

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

hello 출력이 생성 됩니다.

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

**2014 년 10 월 8 릴리스 hello에 대 한**:

때 Ambari hello를 사용 하 여 끝점, "을 (를) https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname" hello *host_name* 필드 hello hello 호스트 이름 대신 hello 노드의 정규화 된 도메인 이름 (FQDN)을 반환합니다. Hello 2014 년 10 월 8 릴리스 전에이 예제에서는 반환 단순히 "**headnode0**"입니다. Hello FQDN을 얻게 hello 2014 년 10 월 8 릴리스 후 "**headnode0. { ClusterDNS}.azurehdinsight.net**"와 같이 hello 앞의 예제입니다. 이 변경은 필요한 toofacilitate 시나리오 여러 클러스터 유형 (예: HBase 및 Hadoop)를 배포할 수 있는 하나의 가상 네트워크 (VNET) 했습니다. 예를 들어 Hadoop의 백 엔드 플랫폼으로 HBase를 사용하는 등의 경우 이 변경이 적용됩니다.

## <a name="ambari-monitoring-apis"></a>Ambari 모니터링 API
hello 다음 표에서 hello 가장 일반적인 Ambari 모니터링 API 호출 수입니다. Hello API에 대 한 자세한 내용은 참조 [Ambari API 참조][ambari-api-reference]합니다.

| 모니터링 API 호출 | URI | 설명 |
| --- | --- | --- |
| 클러스터 가져오기 |`/api/v1/clusters` | |
| 클러스터 정보 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |클러스터, 서비스, 호스트 |
| 서비스 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |서비스에 포함: hdfs, mapreduce |
| 서비스 정보 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| 서비스 구성 요소 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker |
| 구성 요소 정보 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo, host-components, 메트릭 |
| 호스트 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0, workernode0 |
| 호스트 정보 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| 호스트 구성 요소 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode, resourcemanager |
| 호스트 구성 요소 정보 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles, 구성 요소, 호스트, 메트릭 |
| 구성 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |구성 유형: core-site, hdfs-site, mapred-site, hive-site |
| 구성 정보 가져오기 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |구성 유형: core-site, hdfs-site, mapred-site, hive-site |

## <a name="next-steps"></a>다음 단계
파악 했으므로 이제 toouse Ambari 모니터링 API를 호출 하는 방법입니다. toolearn 더 참조 하십시오.

* [Hello Azure 포털을 사용 하 여 HDInsight 클러스터를 관리][hdinsight-admin-portal]
* [Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]
* [명령줄 인터페이스를 사용하여 HDInsight 클러스터 관리][hdinsight-admin-cli]
* [HDInsight 설명서][hdinsight-documentation]
* [HDInsight 시작][hdinsight-get-started]

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
