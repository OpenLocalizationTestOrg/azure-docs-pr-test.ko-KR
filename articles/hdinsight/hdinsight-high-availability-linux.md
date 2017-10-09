---
title: "Hadoop-Azure HDInsight에 대 한 aaaHigh 가용성 | Microsoft Docs"
description: "HDInsight 클러스터에서 추가 헤드 노드를 사용하여 안정성과 가용성을 높이는 방법을 알아봅니다. 에 대해 알아봅니다 Ambari 하이브가 등의 Hadoop 서비스에 미치는 영향에 tooindividually SSH를 사용 하 여 tooeach 헤드 노드를 연결 하는 방식."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: hadoop high availability
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>HDInsight에서 Hadoop 클러스터의 가용성 및 안정성

HDInsight 클러스터에 두 개의 헤드 노드 tooincrease hello 가용성과 Hadoop 서비스와 실행 중인 작업의 안정성을 제공 합니다.

Hadoop은 클러스터의 여러 노드에서 서비스와 데이터를 복사하여 고가용성과 안정성을 달성합니다. 그러나 Hadoop의 표준 배포에는 일반적으로 단일 헤드 노드만 있습니다. 모든 시간 동안 중단 hello 단일 헤드 노드는 hello 클러스터 toostop 작업을 발생할 수 있습니다. HDInsight 두 headnodes tooimprove Hadoop의 가용성 및 안정성을 제공합니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="availability-and-reliability-of-nodes"></a>노드의 가용성 및 안정성

HDInsight 클러스터에 있는 노드는 Azure 가상 컴퓨터를 사용하여 구현됩니다. hello 다음 섹션에서는 형식에 설명 hello 개별 노드 HDInsight 함께 사용 합니다. 

> [!NOTE]
> 일부 노드 유형은 클러스터 유형에 사용되지 않습니다. 예를 들어 Hadoop 클러스터 유형에는 Nimbus 노드가 없습니다. HDInsight 클러스터 형식에서 사용 하는 노드에 대 한 자세한 내용은 hello의 hello 클러스터 유형 섹션을 참조 하십시오. [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) 문서.

### <a name="head-nodes"></a>헤드 노드

HDInsight은 Hadoop 서비스의 고가용성을 tooensure, 두 헤드 노드를 제공합니다. 두 헤드 노드가 모두 동시에 활성 상태이 고 hello HDInsight 클러스터 내에서 실행 중인 합니다. 일부 서비스(예: HDFS 또는 YARN)는 항상 헤드 노드 하나에서만 '활성' 상태입니다. HiveServer2 또는 Hive MetaStore 같은 다른 서비스는 hello에서 헤드 노드 모두에서 활성 동시 합니다.

헤드 노드 (및 HDInsight의 다른 노드에) hello 노드의 hello hostname의 일환으로 숫자 값이 있어야 합니다. 예를 들면 `hn0-CLUSTERNAME` 또는 `hn4-CLUSTERNAME`과 같습니다.

> [!IMPORTANT]
> 기본 또는 보조 노드 인지와 hello 숫자 값을 연결 하지 마십시오. hello 숫자 값이 있는 tooprovide 각 노드에 대 한 고유 이름입니다.

### <a name="nimbus-nodes"></a>Nimbus 노드

Nimbus 노드는 Storm 클러스터와 함께 사용할 수 있습니다. hello Nimbus 노드를 배포 하 고 작업자 노드 간 처리를 모니터링 하 여 비슷한 기능 toohello Hadoop JobTracker를 제공 합니다. HDInsight는 Storm 클러스터에 두 개의 Nimbus 노드를 제공합니다.

### <a name="zookeeper-nodes"></a>Zookeeper 노드

[ZooKeeper](http://zookeeper.apache.org/) 노드는 헤드 노드에서 마스터 서비스의 리더 선택에 사용됩니다. 사용 되는 tooinsure 서비스, 데이터 (작업자) 노드 및 게이트웨이 마스터 서비스에서 활성화 되어 있는 헤드 노드를 알고 있는 수도 있습니다. 기본적으로 HDInsight는 3개의 ZooKeeper 노드를 제공합니다.

### <a name="worker-nodes"></a>작업자 노드

작업자 노드는 작업을 제출 된 toohello 클러스터 hello 실제 데이터 분석을 수행 합니다. 작업자 노드 실패 하면 수행 된 hello 작업은 제출 된 tooanother 작업자 노드입니다. 기본적으로 HDInsight는 네 개의 작업자 노드를 만듭니다. 및 클러스터를 만든 후 요구에 맞게가 숫자 toosuit을 변경할 수 있습니다.

### <a name="edge-node"></a>에지 노드

가장자리 노드 hello 클러스터 내에서 분석 데이터에에서 적극적으로 참여 하지 않습니다. 이는 개발자 또는 데이터 과학자가 Hadoop과 함께 작업하는 경우 사용합니다. hello 모서리 생활에서 노드 hello 클러스터의 다른 노드와 hello와 동일한 Azure 가상 네트워크를 hello 및 다른 모든 노드에서 직접 액세스할 수 있습니다. hello 가장자리 노드는 분석 작업 또는 중요 한 Hadoop 서비스 리소스를 차지 하지 않고 사용할 수 있습니다.

현재 HDInsight에 R Server 가장자리 노드는 기본적으로 제공 하는 hello만 클러스터 유형입니다. HDInsight의 R 서버용 hello 가장자리 노드 사용 되는 분산된 처리에 대 한 클러스터 toohello 제출 하기 전에 hello 노드에서 로컬로 테스트 R 코드입니다.

가장자리 노드를 사용 하 여 R 서버가 아닌 다른 클러스터 형식에 대 한 내용은 hello 참조 [가장자리 노드를 사용 하 여 HDInsight의](hdinsight-apps-use-edge-node.md) 문서.

## <a name="accessing-hello-nodes"></a>Hello 노드에 액세스

Hello 통해 액세스 toohello 클러스터 인터넷 공용 게이트웨이 통해 제공 됩니다. 액세스 제한 tooconnecting toohello 헤드 노드에 사용 되며 (하는 경우 하나 존재) hello 가장자리 노드. 액세스 tooservices hello 헤드 노드에서 실행 하 여 여러 헤드 노드에 영향을 받지 않습니다. hello 공용 게이트웨이 경로 요청 toohello 헤드 노드 hello를 호스팅하는 서비스를 요청 했습니다. 예를 들어 Ambari hello 보조 헤드 노드에서 현재 호스팅되면, hello 게이트웨이 Ambari toothat 노드에 대 한 들어오는 요청을 라우팅합니다.

Hello 공용 게이트웨이 통해 액세스가 제한 된 tooport 443 (HTTPS), 22, 및 23 합니다.

* 포트 __443__ 사용 되는 tooaccess은 Ambari 오류 코드 및 기타 웹 UI 또는 hello 헤드 노드에 호스팅되는 REST Api입니다.

* 포트 __22__ 가 사용 되는 tooaccess hello 기본 헤드 노드 또는 SSH 노드 가장자리입니다.

* 포트 __23__ 사용 되는 tooaccess hello 보조 헤드 노드의 SSH 합니다. 예를 들어 `ssh username@mycluster-ssh.azurehdinsight.net` toohello 기본 헤드 노드 라는 hello 클러스터의 연결 **mycluster**합니다.

SSH를 사용 하 여에 대 한 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>내부 FQDN(정규화된 도메인 이름)

HDInsight 클러스터의 노드 내부 IP 주소와 FQDN만 hello 클러스터에서 액세스할 수 있어야 합니다. Hello 내부 FQDN 또는 IP 주소를 사용 하 여 hello 클러스터에서 서비스에 액세스할 때는 hello 서비스에 액세스할 때 Ambari tooverify hello IP 또는 FQDN toouse를 사용 해야 합니다.

예를 들어, 헤드 노드 하나에서 서비스 에서만 실행할 수 Oozie hello 및 hello를 사용 하 여 `oozie` 대 한 SSH 세션에서 명령을 hello URL toohello 서비스가 필요 합니다. 다음 명령을 hello를 사용 하 여 Ambari에서이 URL은 검색할 수 있습니다.

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

이 명령은 다음 hello 내부 URL toouse hello로 포함 된 명령을 값 비슷한 toohello 반환 `oozie` 명령:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Hello Ambari REST API를 사용한 작업에 대 한 자세한 내용은 참조 하십시오. [모니터 및 hello Ambari REST API를 사용 하 여 관리할 HDInsight](hdinsight-hadoop-manage-ambari-rest-api.md)합니다.

### <a name="accessing-other-node-types"></a>다른 노드 유형에 액세스

액세스할 수 있는 조치 hello 다음 메서드를 사용 하 여 인터넷 hello 직접 않은 toonodes를 연결할 수 있습니다.

* **SSH**: SSH를 사용 하 여 tooa 헤드 노드에 연결 되 면 hello 클러스터의 헤드 노드 tooconnect tooother 노드 hello에서에서 SSH를 사용 하 여 있습니다. 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

* **SSH 터널이**: toohello 노출 하지 않은 hello 노드 중 하나에서 호스팅되는 웹 서비스 tooaccess 해야 할 경우 인터넷에는 SSH 터널을 사용 해야 합니다. 자세한 내용은 참조 hello [HDInsight와 SSH 터널을 사용 하 여](hdinsight-linux-ambari-ssh-tunnel.md) 문서.

* **Azure 가상 네트워크**: 경우 HDInsight 클러스터의 모든 리소스에 Azure 가상 네트워크의 일부인 hello 동일한 가상 네트워크 직접 액세스할 수 hello 클러스터의 모든 노드가 있습니다. 자세한 내용은 참조 hello [Azure 가상 네트워크를 사용 하 여 확장 HDInsight](hdinsight-extend-hadoop-virtual-network.md) 문서.

## <a name="how-toocheck-on-a-service-status"></a>어떻게 toocheck 서비스 상태에

hello 헤드 노드에서 실행 되는 서비스의 toocheck hello 상태 hello Ambari 웹 UI를 사용 하 여 또는 Ambari REST API를 환영 합니다.

### <a name="ambari-web-ui"></a>Ambari 웹 UI

hello Ambari 웹 UI https://CLUSTERNAME.azurehdinsight.net에 표시 됩니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다. 메시지가 표시 되 면 클러스터에 대 한 hello HTTP 사용자 자격 증명을 입력 합니다. hello 기본 HTTP 사용자 이름은 **admin** hello 암호도 hello 클러스터를 만들 때 입력 hello 암호를 입력 합니다.

Hello Ambari 페이지에 도착 하면 hello 설치 된 서비스는 hello hello 페이지 왼쪽에 나열 됩니다.

![설치된 서비스](./media/hdinsight-high-availability-linux/services.png)

일련의 다음 tooa 서비스 tooindicate 상태 표시 될 수 있는 아이콘 있습니다. Tooa 서비스는 hello를 사용 하 여 볼 수 있습니다 하는 모든 경고와 관련 된 **경고** hello hello 페이지 맨 아래에 링크 합니다. 자세한 내용은 각 서비스 tooview를 선택할 수 있습니다.

Hello 서비스 페이지 hello 상태와 각 서비스의 구성 정보를 제공 하며, 헤드 노드 hello 서비스에서 실행 되는 정보를 제공 하지 않습니다. tooview이 정보를 사용 하 여 hello **호스트** hello hello 페이지 맨 아래에 링크 합니다. 이 페이지는 hello 헤드 노드를 포함 하 여 hello 클러스터 내의 호스트를 표시 합니다.

![호스트 목록](./media/hdinsight-high-availability-linux/hosts.png)

Hello 헤드 노드 중 하나에 대 한 hello 링크를 선택 하는 hello 서비스와 해당 노드에서 실행 되는 구성 요소를 표시 합니다.

![구성 요소 상태](./media/hdinsight-high-availability-linux/nodeservices.png)

Ambari를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [모니터 HDInsight hello Ambari 웹 UI를 사용 하 여 관리 및](hdinsight-hadoop-manage-ambari.md)합니다.

### <a name="ambari-rest-api"></a>Ambari REST API

hello Ambari REST API는 hello를 통해 사용할 수 있는 인터넷 합니다. hello HDInsight 공용 게이트웨이 라우팅 요청 toohello 헤드 노드 hello REST API를 현재 호스팅 중인를 처리 합니다.

다음 명령 toocheck hello 상태 hello Ambari REST API를 통해 서비스의 hello를 사용할 수 있습니다.

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* 대체 **암호** hello HTTP 사용자 (관리자) 계정 암호를 사용 합니다.
* 대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.
* 대체 **SERVICENAME** toocheck hello 상태의 hello 서비스의 hello 이름의 원하는 합니다.

예를 들어 toocheck hello 상태의 hello **HDFS** 서비스 라는 클러스터에 **mycluster**, 암호는 **암호**, hello 다음 명령을 사용 하 여:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

hello 응답은 JSON 다음 유사한 toohello입니다.

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

hello URL 알려줍니다. 명명 된 헤드 노드에서 hello 서비스가 실행 중이 **hn0 CLUSTERNAME**합니다.

hello 상태를 알려줍니다. hello 서비스를 현재 실행 중인지 또는 **STARTED**합니다.

Hello 클러스터에 설치 하는 서비스 잘 모르는 경우에 hello tooretrieve 명령 목록을 다음을 사용할 수 있습니다.

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Hello Ambari REST API를 사용한 작업에 대 한 자세한 내용은 참조 하십시오. [모니터 및 hello Ambari REST API를 사용 하 여 관리할 HDInsight](hdinsight-hadoop-manage-ambari-rest-api.md)합니다.

#### <a name="service-components"></a>서비스 구성 요소

서비스의 toocheck hello 상태를 개별적으로 원하는 구성 요소를 포함할 수 있습니다. 예를 들어 HDFS hello NameNode 구성 요소를 포함 합니다. 구성 요소에 대 한 tooview 내용은 hello 명령이 합니다.

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

구성 요소는 서비스에서 제공 잘 모르는 경우에 hello tooretrieve 명령 목록을 다음을 사용할 수 있습니다.

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Tooaccess는 hello 헤드 노드에서 파일을 로그 하는 방법은

### <a name="ssh"></a>SSH

SSH 통해 연결 된 tooa 헤드 노드는 동안 로그 파일을 찾을 수에서 **/var/로그**합니다. 예를 들어 **/var/log/hadoop-yarn/yarn** 은 YARN에 대한 로그를 포함합니다.

각 헤드 노드 hello 모두에 로그를 확인 해야 하므로 고유한 로그 항목에 있을 수 있습니다.

### <a name="sftp"></a>SFTP

파일 전송 프로토콜 SFTP (보안), 또는 hello SSH 파일 전송 프로토콜을 사용 하 여 toohello 헤드 노드를 연결 하 고 hello 로그 파일을 직접 다운로드할 수도 있습니다.

비슷한 toousing SSH 클라이언트를 제공 해야 toohello 클러스터를 연결할 때 SSH 사용자 계정 이름 및 hello SSH 주소 hello 클러스터의 hello 합니다. 예: `sftp username@mycluster-ssh.azurehdinsight.net`. 메시지가 표시 되 면 hello 계정에 대 한 hello 암호를 제공 하거나 hello를 사용 하 여 공개 키 제공 `-i` 매개 변수입니다.

연결되면 `sftp>` 프롬프트가 나타납니다. 이 프롬프트에서 디렉터리를 변경하고 파일을 업로드 및 다운로드할 수 있습니다. 다음 명령을 hello 디렉터리 toohello를 변경 하는 예를 들어 **/var/log/hadoop/hdfs** 디렉터리와 hello 디렉터리의 모든 파일 다음 다운로드 합니다.

    cd /var/log/hadoop/hdfs
    get *

사용할 수 있는 명령 목록에 대 한 입력 `help` hello에 `sftp>` 프롬프트입니다.

> [!NOTE]
> SFTP를 사용 하 여 연결 하는 경우 toovisualize hello 파일 시스템을 수 있는 그래픽 인터페이스도 있습니다. 예를 들어 [MobaXTerm](http://mobaxterm.mobatek.net/) toobrowse hello 파일 시스템 인터페이스 비슷한 tooWindows 탐색기를 사용 하 여 있습니다.

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess 로그 Ambari를 사용 하 여 파일, SSH 터널을 사용 해야 합니다. hello 개별 서비스에 대 한 hello 웹 인터페이스 hello 인터넷에서 공개적으로 노출 되지 않습니다. SSH 터널을 사용 하는 방법은 참조 hello [사용 하 여 SSH 터널링](hdinsight-linux-ambari-ssh-tunnel.md) 문서.

Hello Ambari 웹 UI에서에서 tooview 로그 (예를 들어 YARN)에 대 한 원하는 hello 서비스를 선택 합니다. 다음 사용 하 여 **빠른 링크** tooselect는 헤드 노드 tooview hello에 대 한 로그입니다.

![Tooview 로그 링크 빠른을 사용 하 여](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Tooconfigure 노드 크기를 hello 하는 방법

hello 크기 노드 클러스터를 만드는 동안만 선택할 수 있습니다. 찾을 수 있습니다 hello 목록을 사용할 수 있는 다른 VM 크기 HDInsight에 대 한 hello [HDInsight 가격 책정 페이지](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.

클러스터를 만들 때는 hello 노드의 hello 크기를 지정할 수 있습니다. hello 다음 정보에 지침을 제공 방법을 사용 하 여 toospecify hello 크기 hello [Azure 포털][preview-portal], [Azure PowerShell][azure-powershell], hello 및 [Azure CLI][azure-cli]:

* **Azure 포털**: hello 클러스터에서 사용 하는 hello 노드의 hello 크기는 클러스터를 만들 때 설정할 수 있습니다.

    ![노드 크기 선택이 포함된 클러스터 만들기 마법사의 이미지](./media/hdinsight-high-availability-linux/headnodesize.png)

* **Azure CLI**: hello를 사용 하는 경우 `azure hdinsight cluster create` 명령을 hello를 사용 하 여 hello h e a d, 작업자 및 사육 노드의 hello 크기를 설정할 수 있습니다 `--headNodeSize`, `--workerNodeSize`, 및 `--zookeeperNodeSize` 매개 변수입니다.

* **Azure PowerShell**: hello를 사용 하는 경우 `New-AzureRmHDInsightCluster` cmdlet hello를 사용 하 여 hello h e a d, 작업자 및 사육 노드의 hello 크기를 설정할 수 있습니다 `-HeadNodeVMSize`, `-WorkerNodeSize`, 및 `-ZookeeperNodeSize` 매개 변수입니다.

## <a name="next-steps"></a>다음 단계

이 문서에 설명 된 항목에 대 한 자세한 링크 toolearn 다음 hello를 사용 합니다.

* [Ambari REST 참조](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [설치 하 고 hello Azure CLI를 구성 합니다.](../cli-install-nodejs.md)
* [Azure PowerShell 설치 및 구성](/powershell/azure/overview)
* [Ambari를 사용하여 HDInsight 관리](hdinsight-hadoop-manage-ambari.md)
* [Linux 기반 HDInsight 클러스터 프로비전을](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
