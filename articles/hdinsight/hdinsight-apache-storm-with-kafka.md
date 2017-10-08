---
title: "HDInsight-Azure의 Storm와 Apache Kafka aaaUse | Microsoft Docs"
description: "Apache Kafka는 HDInsight에 Apache Storm과 함께 설치됩니다. 어떻게 toowrite tooKafka 및 사용 하 여 여기에서 다음 읽기 hello Storm 함께 제공 된 KafkaBolt 및 KafkaSpout 구성 요소에 알아봅니다. 또한 toouse 표적이 프레임 워크 toodefine hello 하 및 스톰 토폴로지를 제출 하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>HDInsight의 Storm에서 Apache Kafka(미리 보기) 사용

자세한 방법에서 toouse Apache Storm tooread 및 tooApache Kafka 쓰기입니다. 이 예제에서는 또한 스톰 토폴로지 toohello HDFS 호환에서에서 toosave 데이터 파일을 시스템 HDInsight에서 사용 하는 방법을 보여 줍니다.

> [!NOTE]
> 이 문서의 단계 hello HDInsight의 Storm와 HDInsight 클러스터에서 Kafka 모두 포함 된 Azure 리소스 그룹을 만듭니다. 이 클러스터는 Storm 클러스터 toodirectly hello를는 Azure 가상 네트워크 내에 위치한 둘 다 hello Kafka 클러스터와 통신 합니다.
> 
> Hello이이 문서의 단계를 완료 하는 경우 toodelete hello 클러스터 tooavoid 초과 요금을 기억 합니다.

## <a name="get-hello-code"></a>Hello 코드 가져오기

이 문서에 사용 되는 hello 예제에 대 한 hello 코드에서 사용할 수는 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)합니다.

toocompile이이 프로젝트를 hello 같은 개발 환경에 대 한 구성이 필요 합니다.

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상 - HDInsight 3.5 이상에는 Java 8이 필요합니다.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* SSH 클라이언트 (hello 필요한 `ssh` 및 `scp` 명령)-내용은 참조 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

* 텍스트 편집기 또는 IDE

hello 다음과 같은 환경 변수 설정 되어 있습니다 Java와 hello JDK 개발용 워크스테이션에 설치 하는 경우. 그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.

* `JAVA_HOME`-toohello hello JDK가 설치 디렉터리를 가리켜야 합니다.
* `PATH`-경로 따라 hello를 포함 해야 합니다.
  
    * `JAVA_HOME`(또는 hello 해당 하는 경로)입니다.
    * `JAVA_HOME\bin`(또는 hello 해당 하는 경로)입니다.
    * Maven 설치 되어 있는 hello 디렉터리입니다.

## <a name="create-hello-clusters"></a>Hello 클러스터를 만들려면

HDInsight의 Apache Kafka에서는 액세스 toohello Kafka 브로커를 통해 공용 인터넷 hello 합니다. 토론에 tooKafka 있어야 hello hello 노드로 동일한 Azure 가상 네트워크는 모든 작업이 hello Kafka 클러스터입니다. 예를 들어 hello Kafka 및 Storm 클러스터를 모두 Azure 가상 네트워크에 있는 합니다. hello 다음 그림에 hello 클러스터 간의 통신 흐름 방식을:

![Azure 가상 네트워크에 있는 Storm 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> SSH 및 Ambari를 통해 액세스할 수와 같은 hello 클러스터에 있는 다른 서비스는 인터넷에 hello 합니다. HDInsight와 사용할 수 있는 공용 포트 hello에 대 한 자세한 내용은 참조 하십시오. [포트 및 HDInsight에서 사용 하는 Uri](hdinsight-hadoop-port-settings-for-services.md)합니다.

Storm 클러스터를 수동으로 Kafka, Azure 가상 네트워크를 만들 수는 것 보다 쉽게 toouse Azure 리소스 관리자 템플릿을 합니다. 사용 하 여 hello 다음 단계는 Azure 가상 네트워크, Kafka toodeploy 및 Storm 클러스터 tooyour Azure 구독.

1. Hello tooAzure에서 단추 toosign 및 hello Azure 포털에서에서 열기 hello 서식 파일을 사용 합니다.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    hello Azure 리소스 관리자 템플릿에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**합니다. 다음 리소스는 hello를 생성 됩니다.
    
    * Azure 리소스 그룹
    * Azure 가상 네트워크
    * Azure 저장소 계정
    * HDInsight 버전 3.6의 Kafka(작업자 노드 3개)
    * HDInsight 버전 3.6의 Storm(작업자 노드 3개)

  > [!WARNING]
  > HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다. 이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.

2. 지침 toopopulate hello 항목에 나오는 hello에 사용 하 여 hello **사용자 지정 배포** 블레이드:
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다. 이 그룹 hello HDInsight 클러스터를 포함합니다.
   
    * **위치**: 위치 지리적으로 닫기 tooyou를 선택 합니다.

    * **기본 클러스터 이름을**:이 값 hello hello 스톰 및 Kafka 클러스터에 대 한 기본 이름으로 사용 됩니다. 예를 들어 **hdi**를 입력하면 **storm-hdi**라는 Storm 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.
   
    * **클러스터 로그인 사용자 이름**: hello 스톰 및 Kafka 클러스터에 대 한 hello 관리자 사용자 이름입니다.
   
    * **로그인 암호 클러스터**: hello 스톰 및 Kafka 클러스터에 대 한 hello 관리자 사용자 암호입니다.
    
    * **SSH 사용자 이름이**: hello 스톰 및 Kafka 클러스터에 대 한 SSH 사용자 toocreate hello 합니다.
    
    * **SSH 암호**: hello 스톰 및 Kafka 클러스터에 대 한 SSH 사용자 hello에 대 한 hello 암호입니다.

3. 읽기 hello **약관**를 선택한 후 **toohello 약관 위에서 설명한 동의**합니다.

4. 마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다. Hello 클러스터 toocreate 약 20 분이 필요합니다.

Hello 리소스를 만든 후 hello 리소스 그룹에 대 한 hello 블레이드가 표시 됩니다.

![Hello vnet 및 클러스터 리소스 그룹 블레이드](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Hello HDInsight 클러스터의 이름이 hello **스톰 BASENAME** 및 **kafka BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다. Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.

## <a name="understanding-hello-code"></a>Hello 코드 이해

이 프로젝트에는 다음 두 가지 토폴로지가 있습니다.

* **KafkaWriter**: hello 정의한 **writer.yaml** 파일을이 토폴로지에 Apache Storm와 함께 제공 되는 KafkaBolt hello를 사용 하 여 임의의 문장 tooKafka 씁니다.

    사용자 지정을 사용 하 여이 토폴로지 **SentenceSpout** toogenerate 임의의 문장 구성 요소입니다.

* **KafkaReader**: hello 정의한 **reader.yaml** 파일을이 토폴로지에에서 데이터를 읽고 Kafka Apache Storm와 함께 제공 되는 KafkaSpout hello를 사용 하 여 다음 로그 데이터 toostdout hello 합니다.

    이 토폴로지는 hello Storm 클러스터에 대 한 hello 스톰 HdfsBolt toowrite 데이터 toodefault 저장소를 사용합니다.
### <a name="flux"></a>Flux

hello 토폴로지를 사용 하 여 정의 된 [표적이](https://storm.apache.org/releases/1.1.0/flux.html)합니다. 결정에 도입 된 스톰 0.10. x 하 고 hello 코드에서 tooseparate hello 토폴로지 구성이 있습니다. Hello 표적이 프레임 워크를 사용 하는 토폴로지에서 hello 토폴로지 YAML 파일에 정의 됩니다. hello YAML 파일 hello 토폴로지의 일부로 포함할 수 있습니다. Hello 토폴로지를 전송할 때 사용 하는 독립 실행형 파일 일 수도 있습니다. Flux는 런타임 시 변수 대체도 지원하며, 이 예제에서 사용됩니다.

hello 다음 매개 변수가 설정 이러한 토폴로지에 대 한 실행 시:

* `${kafka.topic}`: hello 이름 hello Kafka 항목을 읽기/쓰기를 hello 토폴로지입니다.

* `${kafka.broker.hosts}`: hello에서 실행 하는 hello Kafka 브로커를 호스트 합니다. hello broker 정보 tooKafka를 작성할 때 hello KafkaBolt에서 사용 됩니다.

* `${kafka.zookeeper.hosts}`: 사육에서 실행 하는 hello 호스트 hello Kafka 클러스터입니다.

Flux 토폴로지에 대한 자세한 내용은 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)을 참조하세요.

## <a name="download-and-compile-hello-project"></a>다운로드 하 고 hello 프로젝트 컴파일

1. hello 프로젝트를 다운로드 하 여 개발 환경에 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)를 명령줄을 열고 hello 프로젝트를 다운로드 한 디렉터리 toohello 위치를 변경 합니다.

2. Hello에서 **스톰 java kafka hdinsight** 디렉터리 사용 하 여 hello 다음 toocompile hello 프로젝트 명령 및 배포에 대 한 패키지를 만듭니다.

  ```bash
  mvn clean package
  ```

    hello 패키지 프로세스 라는 파일을 만듭니다 `KafkaTopology-1.0-SNAPSHOT.jar` hello에 `target` 디렉터리입니다.

3. Hello 명령을 toocopy hello 패키지 tooyour 스톰 HDInsight 클러스터에서 다음을 사용 합니다. 대체 **USERNAME** hello 클러스터에 대 한 hello SSH 사용자 이름이 있습니다. 대체 **BASENAME** hello 클러스터를 만들 때 사용한를 hello 기본 이름입니다.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    메시지가 표시 되 면 hello 클러스터를 만들 때 사용한 hello 암호를 입력 합니다.

## <a name="configure-hello-topology"></a>Hello 토폴로지 구성

1. Hello toodiscover 메서드를 다음 중 하나를 사용 하 여 hello Kafka 브로커 호스트:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > hello Bash 가정 `$CLUSTERNAME` hello HDInsight 클러스터의 hello 이름을 포함 합니다. [jq](https://stedolan.github.io/jq/)도 설치되어 있다고 가정합니다. 메시지가 표시 되 면 hello 클러스터 로그인 계정에 대 한 hello 암호를 입력 합니다.

    반환 된 hello 값은 텍스트 다음 비슷한 toohello:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > 클러스터에 대해 두 개 이상의 브로커 호스트 있을 수 있습니다 하는 동안에 모든 호스트 tooclients의 전체 목록은 tooprovide를 설치할 필요가 없습니다. 하나 또는 두 개로도 충분합니다.

2. Hello 메서드 toodiscover hello Kafka 사육 호스트를 다음 중 하나를 사용 합니다.

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > hello Bash 가정 `$CLUSTERNAME` hello HDInsight 클러스터의 hello 이름을 포함 합니다. [jq](https://stedolan.github.io/jq/)도 설치되어 있다고 가정합니다. 메시지가 표시 되 면 hello 클러스터 로그인 계정에 대 한 hello 암호를 입력 합니다.

    반환 된 hello 값은 텍스트 다음 비슷한 toohello:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > 두 개 이상의 사육 노드가 하는 동안에 모든 호스트 tooclients의 전체 목록은 tooprovide를 설치할 필요가 없습니다. 하나 또는 두 개로도 충분합니다.

    나중에 사용하므로 이 값을 저장합니다.

3. Hello 편집 `dev.properties` hello 프로젝트의 hello 루트에 파일입니다. 이 파일에 hello 브로커 및 사육 호스트 정보 toohello 일치 하는 줄을 추가 합니다. hello 다음 예제에서는 구성 된 hello 이전 단계에서 hello 예제 값을 사용 하 여:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Hello 저장 `dev.properties` 파일과 hello 명령 tooupload 다음 그 toohello Storm 클러스터를 사용 합니다.

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    대체 **USERNAME** hello 클러스터에 대 한 hello SSH 사용자 이름이 있습니다. 대체 **BASENAME** hello 클러스터를 만들 때 사용한를 hello 기본 이름입니다.

## <a name="start-hello-writer"></a>Hello 작성기를 시작 합니다.

1. Hello tooconnect toohello Storm 클러스터 SSH를 사용 하 여 다음을 사용 합니다. 대체 **USERNAME** hello SSH 사용자 이름이 hello 클러스터를 만들 때 사용 합니다. 대체 **BASENAME** 를 hello hello 클러스터를 만들 때 사용 되는 기본 이름입니다.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    메시지가 표시 되 면 hello 클러스터를 만들 때 사용한 hello 암호를 입력 합니다.
   
    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. SSH 연결 hello에서 다음 명령 toocreate hello Kafka 항목 hello 토폴로지에서 사용 하는 hello를 사용 하 여:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    대체 `$KAFKAZKHOSTS` 사육 hello로 hello 이전 섹션에서 검색 된 정보를 호스트 합니다.

2. Hello SSH 연결 toohello Storm 클러스터에서 다음 명령 toostart hello 기록기 토폴로지 hello를 사용 합니다.

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    이 명령과 함께 사용 하는 hello 매개 변수는.

    * `org.apache.storm.flux.Flux`: 표적이 tooconfigure를 사용 하 고이 토폴로지를 실행 합니다.

    * `--remote`: Hello 토폴로지 tooNimbus 제출 합니다. hello 토폴로지 hello 클러스터의 작업자 노드 hello 분산 됩니다.

    * `-R /writer.yaml`: 사용 하 여 hello `writer.yaml` tooconfigure hello 토폴로지 파일입니다. `-R`이 리소스 hello jar 파일에 포함 되어 있는지를 나타냅니다. 따라서 hello jar의 hello 루트에서이 `/writer.yaml` hello 경로 tooit 됩니다.

    * `--filter`: Hello에 항목을 채우는 `writer.yaml` hello에 값을 사용 하 여 토폴로지 `dev.properties` 파일입니다. 예를 들어 hello의 값을 hello `kafka.topic` hello 파일 항목에에서는 사용 되는 tooreplace hello `${kafka.topic}` hello 토폴로지 정의 항목입니다.

5. Hello 토폴로지가 시작 되 면 다음 명령 tooverify 데이터 toohello Kafka 항목을 작성 하는 hello를 사용 합니다.

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    대체 `$KAFKAZKHOSTS` 사육 hello로 hello 이전 섹션에서 검색 된 정보를 호스트 합니다.

    이 명령은 Kafka toomonitor hello 항목와 함께 제공 되는 스크립트를 사용 합니다. 잠시 후 toohello 항목 기록 된 임의의 문장 반환 하기 시작 해야 합니다. hello 비슷한 toohello 다음은 예제 출력:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Ctrl + c toostop hello 스크립트를 사용 합니다.

## <a name="start-hello-reader"></a>Hello 판독기를 시작 합니다.

1. Hello SSH 세션 toohello Storm 클러스터에서 다음 명령 toostart hello 판독기 토폴로지 hello를 사용 합니다.

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Hello 토폴로지 시작 되 면 hello 스톰 UI를 엽니다. 이 웹 UI는 https://storm-BASENAME.azurehdinsight.net/stormui에 있습니다. 대체 __BASENAME__ hello 기본 이름이 hello 클러스터를 만들 때 사용 합니다. 

    요청 시 사용 hello 관리자 로그인 이름 (기본적으로 `admin`) 및 hello 클러스터를 만들 때 사용한 암호입니다. 다음 이미지는 웹 페이지와 유사한 toohello를 표시 됩니다.

    ![Storm UI](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Hello 스톰 UI에서에서 선택 hello __kafka 판독기__ hello에 대 한 링크 __토폴로지 요약__ hello에 대 한 toodisplay 정보 섹션 __kafka 판독기__ 토폴로지입니다.

    ![Hello 스톰 웹 UI의 요약 섹션 토폴로지](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. hello 인스턴스의 선택 hello hello로 거 볼트 구성 요소에 대 한 정보 toodisplay __로 거 볼트__ hello에 대 한 링크 __볼트 (항상)__ 섹션.

    ![Hello 볼트 섹션에서로 거 볼트 링크](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. Hello에 __Executor__ 섹션에서 hello에서 링크를 선택 __포트__ 열 toodisplay 기록은 hello 구성 요소의이 인스턴스에 대 한 정보입니다.

    ![실행자 링크](./media/hdinsight-apache-storm-with-kafka/executors.png)

    hello 로그 hello Kafka 항목에서에서 읽은 hello 데이터 로그를 포함 합니다. hello 로그의 hello 정보는 텍스트 다음 유사한 toohello:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Hello 토폴로지를 중지 합니다.

SSH 세션 toohello Storm 클러스터에서 다음 명령을 toostop hello 스톰 토폴로지 hello를 사용 합니다.

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

이 문서의 단계 hello 만들 둘 다에서 클러스터 hello 같은 Azure 리소스 그룹, hello Azure 포털의에서 hello 리소스 그룹을 삭제할 수 있습니다. 이 문서에 따라 생성 된 모든 리소스를 제거 하는 hello 리소스 그룹을 삭제 합니다.

## <a name="next-steps"></a>다음 단계

HDInsight의 Storm에서 사용할 수 있는 더 많은 예제 토폴로지는 [예제 Storm 토폴로지 및 구성 요소](hdinsight-storm-example-topology.md)를 참조하세요.

Linux 기반 HDInsight에서 토폴로지 배포 및 모니터링에 대한 정보는 [Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md)를 참조하세요.