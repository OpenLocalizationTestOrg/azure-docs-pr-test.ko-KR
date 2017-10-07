---
title: "Apache Kafka-Azure HDInsight와 aaaStart | Microsoft Docs"
description: "Azure HDInsight의 Apache Kafka toocreate 클러스터링 하는 방법에 대해 알아봅니다. 자세한 내용은 방법 toocreate 항목, 구독자 및 소비자입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>HDInsight의 Apache Kafka(미리 보기) 시작

자세한 방법을 toocreate 사용 하는 [Apache Kafka](https://kafka.apache.org) Azure HDInsight 클러스터 합니다. Kafka는 HDInsight와 함께 제공되는 오픈 소스 분산형 스트리밍 플랫폼입니다. 대개 메시지 브로커로 유사한 기능을 제공 하는 대로 tooa 게시-구독 메시지 큐입니다.

> [!NOTE]
> 현재 HDInsight에는 두 가지 버전의 Kafka, 즉 0.9.0(HDInsight 3.4) 및 0.10.0(HDInsight 3.5 및 3.6)이 제공됩니다. 이 문서에 hello 단계 HDInsight 3.6에 Kafka 사용 한다고 가정 합니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Kafka 클러스터 만들기

Hello 단계 toocreate는 Kafka HDInsight 클러스터에서 다음을 사용 합니다.

1. Hello에서 [Azure 포털](https://portal.azure.com)선택, **+ 새로 만들기**, **인텔리전스 + 분석**를 선택한 후 **HDInsight**합니다.
   
    ![HDInsight 클러스터 만들기](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. **기본 사항**, hello 다음 정보를 입력 합니다.

    * **클러스터 이름**: hello HDInsight 클러스터의 hello 이름입니다.
    * **구독**: hello 구독 toouse를 선택 합니다.
    * **클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**: HTTPS를 통해 hello 클러스터에 액세스할 때 hello 로그인 합니다. Hello Ambari 웹 UI 또는 REST API와 같은 이러한 자격 증명 tooaccess 서비스를 사용 합니다.
    * **SSH 사용자 이름 보안**: SSH를 통해 hello 클러스터에 액세스할 때 사용 하는 hello 로그인 합니다. 기본적으로 hello 암호 hello 클러스터 로그인 암호와 같은 hello 됩니다.
    * **리소스 그룹**: hello 리소스 그룹 toocreate hello 클러스터에 있습니다.
    * **위치**: hello Azure 지역 toocreate hello 클러스터에 있습니다.
   
 ![구독 선택](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. 선택 **형식 클러스터**, 집합 hello에서 값을 누른 다음 **클러스터 구성**:
   
    * **클러스터 유형**: Kafka

    * **버전**: Kafka 0.10.0(HDI 3.6)

    * **클러스터 계층**: 표준
     
 마지막으로 hello를 사용 하 여 **선택** toosave 설정 단추입니다.
     
 ![클러스터 유형 선택](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Hello 클러스터 종류를 선택한 후 hello를 사용 하 여 __선택__ tooset hello 클러스터 유형 단추입니다. 를 사용 하 여 hello __다음__ 단추 toofinish 기본 구성입니다.

5. **Storage**에서 Storage 계정을 선택하거나 만듭니다. 이 문서의 단계 hello에 대 한 hello 나머지 필드는 hello 기본값으로 둡니다. 사용 하 여 hello __다음__ 단추 toosave 저장소 구성.

    ![HDInsight에 대 한 저장소 계정 설정을 hello 설정](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. __(선택 사항) 응용 프로그램__선택, __다음__ toocontinue 합니다. 이 예제에는 응용 프로그램이 필요하지 않습니다.

7. __클러스터 크기__선택, __다음__ toocontinue 합니다.

    > [!WARNING]
    > HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다.

    ![집합 hello Kafka 클러스터 크기](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > hello **작업자 노드당 디스크** 입력 컨트롤 hello HDInsight의 Kafka의 확장성입니다. 자세한 내용은 [HDInsight에서 저장소 및 Kafka의 확장성 구성](hdinsight-apache-kafka-scalability.md)을 참조하세요.

8. __고급 설정__선택, __다음__ toocontinue 합니다.

9. Hello에서 **요약**, hello 클러스터에 대 한 hello 구성을 검토 합니다. 사용 하 여 hello __편집__ toochange 올바르지 않은 설정을 연결 합니다. 마지막으로, the__Create__ 단추 toocreate hello 클러스터를 사용 합니다.
   
    ![클러스터 구성 요약](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Too20 분 toocreate hello 클러스터를 걸릴 수 있습니다.

## <a name="connect-toohello-cluster"></a>Toohello 클러스터에 연결

> [!IMPORTANT]
> Hello 다음 단계를 수행할 때는 SSH 클라이언트를 사용 해야 합니다. 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

사용자 클라이언트에서 SSH tooconnect toohello 클러스터를 사용 합니다.

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

대체 **SSHUSER** hello SSH username 클러스터 생성 중에 입력 합니다. 대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.

메시지가 표시 되 면 hello SSH 계정에 사용한 hello 암호를 입력 합니다.

자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a id="getkafkainfo"></a>Hello 사육 및 브로커 호스트 정보 가져오기

두 개의 호스트 값을 알고 있어야 Kafka를 사용할 때 hello *사육* 호스트 및 hello *브로커* 호스트 합니다. 이러한 호스트와 Kafka hello Kafka API와 많은 hello 제공 하는 유틸리티에 사용 됩니다.

Hello 호스트 정보를 포함 하는 단계 toocreate 환경 변수를 다음 hello를 사용 합니다. 이러한 환경 변수는 hello이이 문서의 단계에 사용 됩니다.

1. SSH 연결 toohello 클러스터에서 사용 하 여 hello 다음 명령은 tooinstall hello `jq` 유틸리티입니다. 이 유틸리티는 사용 되는 tooparse JSON 문서 그리고 hello broker 호스트 정보를 검색 하는 데 유용:
   
    ```bash
    sudo apt -y install jq
    ```

2. 다음 명령을 사용 하 여 hello Ambar에서 tooset hello 환경 변수가 해당 정보로 검색:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > 설정 `CLUSTERNAME=` toohello 이름 hello Kafka 클러스터입니다. 설정 `PASSWORD=` hello 클러스터를 만들 때 사용한 toohello 로그인 (관리자) 암호입니다.

    hello 다음 텍스트는 hello 내용의 예로 `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    hello 다음 텍스트는 hello 내용의 예로 `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > hello `cut` 명령 호스트 tootwo 호스트 항목의 사용 되는 tootrim hello 목록입니다. Kafka 소비자 또는 공급자를 만들 때 호스트 tooprovide hello 전체 목록을 않아도 됩니다.
   
    > [!WARNING]
    > Tooalways 정확할이 세션에서 반환 된 hello 정보에 의존 하지 마십시오. Hello 클러스터를 크기를 조정 하는 경우 새 브로커 추가 또는 제거 합니다. 오류가 발생 하는 경우 노드는 대체 hello 노드에 대 한 hello 호스트 이름을 변경할 수 있습니다.
    >
    > Tooensure 유효한 정보를 사용 하기 전에 잠시 후에 hello 사육 및 브로커 호스트 정보를 검색 해야 합니다.

## <a name="create-a-topic"></a>토픽 만들기

Kafka는 *토픽*이라는 범주에 데이터 스트림을 저장합니다. 프로그램의 SSH 연결 tooa 클러스터 헤드 노드에에서 항목을 Kafka toocreate 함께 제공 되는 스크립트를 사용 하 여:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

이 명령은 연결에 저장 된 hello 호스트 정보를 사용 하 여 tooZookeeper `$KAFKAZKHOSTS`, 한 다음 이라는 Kafka 항목을 만들 **테스트**합니다. 다음 스크립트 toolist 항목 hello를 사용 하 여 해당 hello 항목을 만든 날짜를 확인할 수 있습니다.

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

hello이 명령의 출력에 항목을 나열 Kafka, hello가 포함 되어 있는 **테스트** 항목입니다.

## <a name="produce-and-consume-records"></a>레코드 생성 및 소비

Kafka는 토픽에 *레코드*를 저장합니다. *생산자*에서 레코드를 생성하고, *소비자*에서 이 레코드를 소비합니다. 생산자는 Kafka *broker*로부터 레코드를 검색합니다. HDInsight 클러스터의 각 작업자 노드는 Kafka broker입니다.

이전에 만든 및 소비자를 사용 하 여를 읽을 hello 테스트 항목으로 단계 toostore 레코드 로우 hello를 사용 합니다.

1. Hello SSH 세션에서 Kafka toowrite 레코드 toohello 항목을 제공 하는 스크립트를 사용 하 여:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    하면 반환 되지 않습니다 toohello 프롬프트이 명령입니다. 대신, 몇 가지 문자 메시지를 입력 하 고 사용 하 여 **Ctrl + C** toostop toohello 항목을 전송 합니다. 각 행은 별도의 레코드로 전송됩니다.

2. Hello 항목에서 Kafka tooread 레코드와 함께 제공 되는 스크립트를 사용 합니다.
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    이 명령은 hello 항목에서 hello 레코드를 검색 하 고 목록이 표시 됩니다. 사용 하 여 `--from-beginning` 모든 레코드를 검색 하므로 hello 소비자 toostart hello 스트림의 hello 시작 부분에서 알려 줍니다.

3. 사용 하 여 __Ctrl + C__ toostop hello 소비자입니다.

## <a name="producer-and-consumer-api"></a>생산자 및 소비자 API

또한 프로그래밍 방식으로 생성 하 고 hello를 사용 하 여 레코드 사용 수 [Kafka Api](http://kafka.apache.org/documentation#api)합니다. toobuild Java 생산자와 소비자를 hello 개발 환경에서 다음 단계를 사용 합니다.

> [!IMPORTANT]
> Hello 다음과 같은 구성 요소가 개발 환경에 설치 되어 있어야 합니다.
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 또는 이와 동등한 프로그램(예: OpenJDK)
>
> * [Apache Maven](http://maven.apache.org/)
>
> * SSH 클라이언트와 hello `scp` 명령입니다. 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

1. Hello 예제를 다운로드 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started)합니다. 예: hello 생산자/소비자 hello 프로젝트 hello에서 사용 하 여 `Producer-Consumer` 디렉터리입니다. 이 예제는 hello를 아래의 클래스가 포함 되어 있습니다.
   
    * **실행** -hello 소비자 또는 공급자 중 하나를 시작 합니다.

    * **생산자** -저장소 1000000 레코드 toohello 항목입니다.

    * **소비자** -hello 항목에서 레코드를 읽습니다.

2. hello의 디렉터리 toohello 위치를 변경 하는 jar 패키지 toocreate `Producer-Consumer` 다음 명령을 디렉터리 및 사용 하 여 hello:

    ```
    mvn clean package
    ```

    이 명령은 `kafka-producer-consumer-1.0-SNAPSHOT.jar`라는 파일이 포함된 `target`이라는 디렉터리를 만듭니다.

3. 사용 하 여 hello 다음 명령을 toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` 파일 tooyour HDInsight 클러스터:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    대체 **SSHUSER** 클러스터 및 바꾸기에 대 한 hello SSH 사용자와 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다. 메시지가 표시 되 면 hello SSH 사용자 hello 암호를 입력 합니다.

4. 한 번 hello `scp` hello 파일 복사 완료, SSH를 사용 하 여 toohello 클러스터에 연결 합니다. Hello 명령 toowrite 레코드 toohello 테스트 항목을 사용 합니다.

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Hello 프로세스가 완료 되 면 hello 명령 tooread hello 항목에서 다음을 사용 합니다.
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    hello 레코드 읽기, 레코드의 수와 함께 표시 됩니다. 이전 단계에서 스크립트를 사용 하 여 여러 레코드 toohello 항목 전송 기록 1000000 보다 몇 가지 표시 될 수 있습니다.

6. 사용 하 여 __Ctrl + C__ tooexit hello 소비자입니다.

### <a name="multiple-consumers"></a>여러 소비자

Kafka 소비자는 레코드를 읽을 때 소비자 그룹을 사용합니다. 여러 소비자와 같은 그룹 hello를 사용 하 여 항목에서 읽기 분산 된 부하의 결과입니다. Hello 그룹의 각 소비자는 hello 레코드의 일부를 받습니다. 이 과정을 사용 하 여 hello 다음 단계를 toosee:

1. 그 중 두 개 있을 수 있도록 새 SSH 세션 toohello 클러스터를 엽니다. Hello를 사용 하 여 각 세션에서 다음 toostart 인 소비자 hello 같은 소비자 그룹 ID:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    이 명령은 hello 그룹 ID를 사용 하 여 소비자 시작 `mygroup`합니다.

    > [!NOTE]
    > Hello 명령을 사용 하 여 hello에 [hello 사육 및 브로커 호스트 정보를 얻을](#getkafkainfo) 섹션 tooset `$KAFKABROKERS` 이 SSH 세션에 대 한 합니다.

2. Hello 항목에서 받는 각 세션 개수 hello 레코드 것을 확인 합니다. 두 세션의 hello 합계는 하나의 소비자에서 이전에 받은 대로 동일한 hello 해야 합니다.

클라이언트 hello hello 항목에 대 한 hello 파티션을 통해 처리 같은 그룹 내의 사용입니다. Hello에 대 한 `test` , 이전에 만든 항목 8 개의 파티션이 있습니다. 8 개의 SSH 세션을 열고 모든 세션에서 소비자를 시작 하는 경우 각 소비자 hello 항목에 대 한 단일 파티션을에서 레코드를 읽습니다.

> [!IMPORTANT]
> 소비자 그룹에는 파티션보다 더 많은 소비자 인스턴스가 있을 수 없습니다. 이 예제에서는 하나의 소비자 그룹 hello hello 항목의 파티션 수가 이므로 tooeight 소비자를 포함할 수 있습니다. 또는 소비자가 8개 이하인 소비자 그룹이 여러 개 있을 수 있습니다.

Kafka에 저장 된 레코드 파티션 내에서 수신 된 hello 순서에 저장 됩니다. 레코드에 대 한 tooachieve 순차적에서 전달 *파티션 내에서*, 소비자 인스턴스 수가 hello hello 파티션 수와 일치 하는 소비자 그룹을 만듭니다. 레코드에 대 한 tooachieve 순차적에서 전달 *hello 항목 내에서*를 하나만 소비자 인스턴스와 소비자 그룹을 만듭니다.

## <a name="streaming-api"></a>스트리밍 API

hello 스트리밍 API 버전 0.10.0; tooKafka 추가한 이전 버전 스트림 처리에 대 한 Apache Spark 또는 스톰에 의존 합니다.

1. 그렇게 이미 하지 않은 경우 다운로드에서 hello 예제 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour 개발 환경입니다. 스트리밍 예제는 hello에 대 한 hello 프로젝트 hello에서 사용 하 여 `streaming` 디렉터리입니다.
   
    이 프로젝트에는 하나의 클래스만 `Stream`, hello에서 레코드를 읽고 있는 `test` 이전에 만든 항목입니다. 읽기, hello 단어 수를 계산 하 고 명명 된 각 단어 및 count tooa 항목 내보냅니다 `wordcounts`합니다. hello `wordcounts` 주제는이 단원의 이후 단계에서 만들어집니다.

2. Hello 명령줄에서 개발 환경에서의 hello 디렉터리 toohello 위치를 변경 `Streaming` 디렉터리와 다음 명령 toocreate jar 패키지를 사용 하 여 hello:

    ```bash
    mvn clean package
    ```

    이 명령은 `kafka-streaming-1.0-SNAPSHOT.jar`라는 파일이 포함된 `target`이라는 디렉터리를 만듭니다.

3. 사용 하 여 hello 다음 명령을 toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` 파일 tooyour HDInsight 클러스터:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    대체 **SSHUSER** 클러스터 및 바꾸기에 대 한 hello SSH 사용자와 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다. 메시지가 표시 되 면 hello SSH 사용자 hello 암호를 입력 합니다.

4. 한 번 hello `scp` hello 파일 복사 완료 명령, SSH를 사용 하 여 toohello 클러스터 연결 및 명령 toocreate hello 다음 hello를 사용 하 여 `wordcounts` 항목:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. 다음으로 hello 다음 명령을 사용 하 여 프로세스를 스트리밍 hello를 시작 합니다.
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    이 명령은 hello 스트리밍 hello 백그라운드에서 프로세스를 시작 합니다.

6. 사용 하 여 hello 다음 명령은 toosend 메시지 toohello `test` 항목입니다. Hello 스트리밍 예제에서 이러한 메시지를 처리 합니다.
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. 사용 하 여 hello toohello 작성 된 명령 tooview hello 출력 다음 `wordcounts` 프로세스 스트리밍 hello 하 여 항목:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > tooview hello 데이터 hello 소비자 tooprint hello 키와 hello deserializer toouse hello 키와 값에 대 한 설명 해야 합니다. hello 키 이름은 hello 단어가 고 hello 키 값 hello 수를 포함 합니다.
   
    hello는 텍스트 다음 비슷한 toohello 출력:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > hello 개수에는 단어 발생할 때마다를 증가 합니다.

7. Hello를 사용 하 여 __Ctrl + C__ tooexit 소비자 hello 다음 hello를 사용 하 여 `fg` toobring hello 스트리밍 백그라운드 작업 백 toohello 전경 명령입니다. 사용 하 여 __Ctrl + C__ tooexit 것도 합니다.

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계

이 문서에서는 hello의 기본적인 사용 HDInsight의 Apache Kafka 방법을 배웠습니다. 다음 Kafka 사용에 대 한 더 toolearn hello를 사용 합니다.

* [HDInsight의 Kafka를 통한 데이터 고가용성 보장](hdinsight-apache-kafka-high-availability.md)
* [HDInsight에서 Kafka로 관리 디스크를 구성하여 확장성 높이기](hdinsight-apache-kafka-scalability.md)
* kafka.apache.org의 [Apache Kafka 문서](http://kafka.apache.org/documentation.html)
* [HDInsight의 MirrorMaker toocreate Kafka의 복제본을 사용 하 여](hdinsight-apache-kafka-mirroring.md)
* [HDInsight의 Kafka에서 Apache Storm 사용](hdinsight-apache-storm-with-kafka.md)
* [HDInsight의 Kafka에서 Apache Spark 사용](hdinsight-apache-spark-with-kafka.md)
* [Azure 가상 네트워크를 통해 tooKafka 연결](hdinsight-apache-kafka-connect-vpn-gateway.md)
