---
title: "aaaMirror Apache Kafka 항목-Azure HDInsight | Microsoft Docs"
description: "어떻게 toouse Apache Kafka 미러링 항목 tooa 보조 클러스터 미러링 여 toomaintain HDInsight 클러스터에서 Kafka의 복제 기능에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>HDInsight (미리 보기)의 Kafka MirrorMaker tooreplicate Apache Kafka 항목 사용

Apache Kafka toouse 서버의 기능 tooreplicate 항목 tooa 보조 클러스터를 미러링 하는 방법에 대해 알아봅니다. 미러링 연속 되는 프로세스를 실행 하거나 사용할 수 간헐적으로 마이그레이션하는 방법으로 하나의 데이터를 tooanother를 클러스터 합니다.

이 예제에서는 미러링은 두 HDInsight 클러스터 간에 사용 되는 tooreplicate 항목입니다. Hello에 Azure 가상 네트워크에 있는 두 클러스터의 동일한 영역입니다.

> [!WARNING]
> 미러링 수단 tooachieve 결함 허용으로 간주 되지 해야 합니다. 항목 내 오프셋된 tooitems hello hello 원본 및 대상 클러스터 간에 서로 다른 되므로 클라이언트는 두 개의 hello를 바꿔서 사용할 수 없습니다.
>
> 내결함성 유지 하려는 경우에 클러스터 내에서 hello 항목에 대 한 복제를 설정 해야 합니다. 자세한 내용은 [HDInsight에서 Kafka 시작](hdinsight-apache-kafka-get-started.md)을 참조하세요.

## <a name="how-kafka-mirroring-works"></a>Kafka 미러링 작동 방식

Hello MirrorMaker 도구 (Apache Kafka의 일부) tooconsume를 사용 하 여 미러링 작동 hello 원본 클러스터에 대 한 항목을 기록 하 고 hello 대상 클러스터에 로컬 복사본을 만듭니다. MirrorMaker 하나 (이상)에 사용 하 여 *소비자* hello 원본 클러스터에서 읽은 및 *생산자* toohello 로컬 (대상) 클러스터를 작성 하 합니다.

다음 다이어그램 hello hello 미러링 프로세스를 보여줍니다.

![미러링 프로세스 hello의 다이어그램](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

HDInsight의 Apache Kafka hello를 통해 액세스 toohello Kafka 서비스를 제공 하지 않습니다 공용 인터넷 합니다. Hello에 Kafka 생산자 또는 소비자 있어야 hello Kafka 클러스터에서에서 노드 hello와 동일한 Azure 가상 네트워크입니다. 이 예제에서는 hello Kafka 소스와 대상 클러스터는 Azure 가상 네트워크에 있습니다. hello 다음 그림에 hello 클러스터 간의 통신 흐름 방식을:

![Azure 가상 네트워크에 있는 원본 및 대상 Kafka 클러스터 다이어그램](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

hello 원본 및 대상 클러스터의 노드 및 파티션 hello 번호에 서로 다를 수와 hello 항목 내의 오프셋 서로 합니다. 미러링 키 당 별로 레코드 순서는 유지 되므로 hello 키 값을 분할에 사용 되는 유지 관리 합니다.

### <a name="mirroring-across-network-boundaries"></a>네트워크 경계를 넘은 미러링

서로 다른 네트워크에 Kafka 클러스터 간의 toomirror 해야 할 경우 다음 추가 고려 사항 hello 가지가 있습니다.

* **게이트웨이**: hello 네트워크 수 toocommunicate hello TCPIP 수준에 있어야 합니다.

* **이름 확인**: hello Kafka 각 네트워크에서 클러스터 호스트 이름을 사용 하 여 다른 수 tooconnect tooeach 이어야 합니다. 이 각 네트워크의 도메인 이름 (DNS System) 서버 tooforward 요청 toohello 다른 네트워크를 구성 해야 합니다.

    Hello 네트워크와 함께 제공 된 자동 DNS hello를 사용 하는 대신 Azure 가상 네트워크를 만들 때 사용자 지정 DNS 서버 및 hello IP 주소를 hello 서버를 지정 해야 합니다. 가상 네트워크를 만든 hello, 후 있습니다 다음 해당 IP 주소를 사용 하는 Azure 가상 컴퓨터를 만드는 다음 설치 및 구성 해야 DNS 소프트웨어에 합니다.

    > [!WARNING]
    > 만들고 HDInsight hello 가상 네트워크에 설치 하기 전에 hello 사용자 지정 DNS 서버를 구성 합니다. HDInsight toouse hello DNS 서버 hello 가상 네트워크에 대해 구성 하는 데 필요한 추가 구성이 없습니다.

두 개의 Azure Virtual Network 연결에 대한 자세한 내용은 [VNet 간 연결 구성](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)을 참조하세요.

## <a name="create-kafka-clusters"></a>Kafka 클러스터 만들기

Azure 가상 네트워크를 만들고 Kafka 수동으로 클러스터를 보다 쉽게 toouse Azure 리소스 관리자 템플릿을. 다음 단계 toodeploy hello를 사용 하 여 Azure 가상 네트워크 및 두 개의 Kafka 클러스터 tooyour Azure 구독.

1. Hello tooAzure에서 단추 toosign 및 hello Azure 포털에서에서 열기 hello 서식 파일을 사용 합니다.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    hello Azure 리소스 관리자 템플릿에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**합니다.

    > [!WARNING]
    > HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다. 이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.

2. 정보 toopopulate hello 항목에 나오는 hello에 사용 하 여 hello **사용자 지정 배포** 블레이드:
    
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다. 이 그룹 hello HDInsight 클러스터를 포함합니다.

    * **위치**: 위치 지리적으로 닫기 tooyou를 선택 합니다.
     
    * **기본 클러스터 이름을**:이 값 hello Kafka 클러스터 hello에 대 한 기본 이름으로 사용 됩니다. 예를 들어 **hdi**를 입력하면 **source-hdi** 및 **dest-hdi** 클러스터가 만들어집니다.

    * **클러스터 로그인 사용자 이름**: Kafka 클러스터 hello 원본과 대상에 대 한 hello 관리자 사용자 이름입니다.

    * **로그인 암호 클러스터**: hello 원본과 대상에 대 한 hello 관리자 사용자 암호 Kafka 클러스터입니다.

    * **SSH 사용자 이름이**: hello 원본과 대상에 대 한 hello SSH 사용자 toocreate Kafka 클러스터입니다.

    * **SSH 암호**: hello 원본과 대상에 대 한 SSH 사용자 hello에 대 한 hello 암호 Kafka 클러스터입니다.

3. 읽기 hello **약관**를 선택한 후 **toohello 약관 위에서 설명한 동의**합니다.

4. 마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다. Hello 클러스터 toocreate 약 20 분이 필요합니다.

Hello 리소스를 만든 hello 클러스터 및 웹 대시보드를 포함 하는 hello 리소스 그룹에 대 한 리디렉션된 tooa 블레이드 됩니다.

![Hello vnet 및 클러스터 리소스 그룹 블레이드](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Hello HDInsight 클러스터의 이름이 hello **소스 BASENAME** 및 **dest BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다. Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.

## <a name="create-topics"></a>토픽 만들기

1. Toohello 연결 **소스** SSH를 사용 하 여 클러스터:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    대체 **sshuser** hello SSH 사용자 이름이 hello 클러스터를 만들 때 사용 합니다. 대체 **BASENAME** 를 hello hello 클러스터를 만들 때 사용 되는 기본 이름입니다.

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. 사용 하 여 hello 다음 toofind hello 사육 호스트 hello 원본 클러스터에 대 한 명령:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. 다음 항목을 hello 명령 tooverify 사용 하 여 hello는 만들었습니다.

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    hello 응답에 포함 된 `testtopic`합니다.

4. 다음 tooview hello 사육 호스트 정보를 사용 하 여 hello (hello **소스**) 클러스터:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    이 정보를 저장합니다. Hello 다음 섹션에 사용 됩니다.

## <a name="configure-mirroring"></a>미러링 구성

1. Toohello 연결 **대상** 다른 SSH 세션을 사용 하 여 클러스터:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    대체 **sshuser** hello SSH 사용자 이름이 hello 클러스터를 만들 때 사용 합니다. 대체 **BASENAME** 를 hello hello 클러스터를 만들 때 사용 되는 기본 이름입니다.

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. 사용 하 여 hello 다음 명령은 toocreate는 `consumer.properties` 파일에 설명 하는 방법을 hello로 toocommunicate **소스** 클러스터:

    ```bash
    nano consumer.properties
    ```

    콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `consumer.properties` 파일:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    대체 **SOURCE_ZKHOSTS** 사육 hello로 hello에서 정보를 호스트 **소스** 클러스터입니다.

    이 파일 hello 원본 Kafka 클러스터에서에서 읽을 때 hello 소비자 정보 toouse를 설명 합니다. 소비자 구성에 대한 자세한 내용은 kafka.apache.org의 [소비자 구성](https://kafka.apache.org/documentation#consumerconfigs)(영문)을 참조하세요.

    toosave hello 파일을 사용 하 여 **Ctrl + X**, **Y**, 차례로 **Enter**합니다.

3. Hello 대상 클러스터와 통신 하는 hello 생산자를 구성 하기 전에 찾아야 하는데 hello 브로커 호스트 hello에 대 한 **대상** 클러스터입니다. 이 정보 다음 명령을 tooretrieve hello를 사용 합니다.

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    대체 `$PASSWORD` hello 클러스터에 대 한 hello 로그인 계정 (관리자) 암호를 사용 합니다.

    대체 `$CLUSTERNAME` hello 대상 클러스터의 hello 이름의 합니다.

    이 명령은 비슷한 toohello 다음 정보를 반환합니다.

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. 사용 하 여 hello toocreate 뒤는 `producer.properties` 파일에 설명 하는 방법을 hello로 toocommunicate **대상** 클러스터:

    ```bash
    nano producer.properties
    ```

    콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `producer.properties` 파일:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    대체 **DEST_BROKERS** hello broker 정보 hello 이전 단계를 사용 합니다.

    생산자 구성에 대한 자세한 내용은 kafka.apache.org의 [생산자 구성](https://kafka.apache.org/documentation#producerconfigs)(영문)을 참조하세요.

## <a name="start-mirrormaker"></a>MirrorMaker 시작

1. SSH 연결 toohello hello에서에서 **대상** 클러스터 명령 toostart hello MirrorMaker 프로세스를 수행 하는 hello를 사용 합니다.

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    이 예제에서 사용 하는 hello 매개 변수는.

    * **-consumer.config**: 소비자 속성을 포함 하는 hello 파일을 지정 합니다. 이러한 속성은 사용 되는 toocreate hello에서 읽는 소비자 *소스* Kafka 클러스터입니다.

    * **-producer.config**: 생산자 속성을 포함 하는 hello 파일을 지정 합니다. 이러한 속성은 사용 되는 toocreate toohello 쓰는 생산자 *대상* Kafka 클러스터입니다.

    * **-화이트 리스트**: MirrorMaker hello 원본 클러스터 toohello 대상에서 복제 하는 항목의 목록입니다.

    * **-num.streams**: hello 소비자 스레드 toocreate의 수입니다.

 시작 시 MirrorMaker 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. SSH 연결 toohello hello에서에서 **소스** 클러스터 명령 toostart 생산자 다음 hello를 사용 하 고 toohello 부분 메시지를 보냅니다.

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    대체 `$PASSWORD` hello 원본 클러스터에 대 한 hello 로그인 (관리자) 암호를 사용 합니다.

    대체 `$CLUSTERNAME` hello 원본 클러스터의 hello 이름을 가진 합니다.

     커서로 빈 라인에 도달하면 몇 개의 텍스트 메시지를 입력합니다. Hello toohello 항목 전송 되므로 이러한 **소스** 클러스터입니다. 사용을 완료 한 후 **Ctrl + C** tooend hello 생산자 프로세스입니다.

3. SSH 연결 toohello hello에서에서 **대상** 클러스터를 사용 하 여 **Ctrl + C** tooend hello MirrorMaker 프로세스입니다. 사용 하 여 hello 다음 명령을 tooverify 해당 hello 다음 `testtopic` 항목 만들어지고 hello 항목의 해당 데이터를 복제 된 toothis 미러:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    대체 `$PASSWORD` hello 대상 클러스터에 대 한 hello 로그인 (관리자) 암호를 사용 합니다.

    대체 `$CLUSTERNAME` hello 대상 클러스터의 hello 이름의 합니다.

    hello 목록 항목에 포함 `testtopic`, hello 원본 클러스터 toohello 대상에서 hello 항목을 미러링합니다. MirrorMaster 때 생성 됩니다. hello 항목에서 검색 된 hello 메시지는 hello hello 원본 클러스터에 입력 된 것과 동일 합니다.

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

이 문서의 단계 hello 만들 둘 다에서 클러스터 hello 같은 Azure 리소스 그룹, hello Azure 포털의에서 hello 리소스 그룹을 삭제할 수 있습니다. 이 문서, hello Azure 가상 네트워크 및 hello 클러스터에서 사용 하는 저장소 계정에 따라 생성 된 모든 리소스를 제거 하는 hello 리소스 그룹을 삭제 합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 어떻게 toouse MirrorMaker toocreate는 Kafka의 복제본 클러스터 배웠습니다. Kafka 다른 방법으로 toowork hello 링크 toodiscover 다음 사용 합니다.

* [Apache Kafka MirrorMaker 문서](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330)(cwiki.apache.org)
* [HDInsight에서 Apache Kafka 시작](hdinsight-apache-kafka-get-started.md)
* [HDInsight의 Kafka에서 Apache Spark 사용](hdinsight-apache-spark-with-kafka.md)
* [HDInsight의 Kafka에서 Apache Storm 사용](hdinsight-apache-storm-with-kafka.md)
* [Azure 가상 네트워크를 통해 tooKafka 연결](hdinsight-apache-kafka-connect-vpn-gateway.md)
