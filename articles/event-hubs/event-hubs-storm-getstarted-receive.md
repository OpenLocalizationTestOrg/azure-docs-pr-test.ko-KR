---
title: "Apache Storm를 사용 하 여 Azure 이벤트 허브에서 aaaReceive 이벤트 | Microsoft Docs"
description: "Apache Storm을 사용하여 Event Hubs에서 수신 시작"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a>Apache Storm을 사용하여 Event Hubs에서 이벤트 수신

[Apache Storm](https://storm.incubator.apache.org)은 분산된 실시간 계산 시스템으로, 바인딩되지 않은 데이터 스트림의 안정적인 처리를 간소화합니다. 이 섹션에서는 Azure 이벤트 허브 스톰 toouse 이벤트 허브에서 tooreceive 이벤트 spout 하는 방법을 보여 줍니다. Apache Storm을 사용하면 다른 노드에 호스트된 여러 프로세스 간에 이벤트를 분할할 수 있습니다. hello 스톰와 이벤트 허브 통합 단순화 이벤트 소비 검사점을 투명 하 게 설정 하 여 진행 상황을 Storm의 사육 설치를 사용 하 여 영구 검사점 관리 및 이벤트 허브에서 병렬 수신 합니다.

이벤트 허브에 대 한 자세한 정보에 대 한 패턴을 수신 hello를 참조 하십시오 [이벤트 허브 개요][Event Hubs overview]합니다.

## <a name="create-project-and-add-code"></a>프로젝트 만들기 및 코드 추가

이 자습서에서는 [HDInsight 스톰] [ HDInsight Storm] 설치와 함께 제공 되 이벤트 허브 spout hello 이미 사용할 수 있습니다.

1. Hello에 따라 [HDInsight 스톰-시작](../hdinsight/hdinsight-storm-overview.md) 프로시저 toocreate 새 HDInsight tooit 원격 데스크톱을 통해 연결 하 고, 클러스터입니다.
2. 복사 hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` 파일 tooyour 로컬 개발 환경입니다. 이 hello 이벤트 스톰 배출구 포함 되어 있습니다.
3. Hello 명령 tooinstall hello 패키지 hello 로컬 Maven 저장소로 다음을 사용 합니다. 이렇게 하면 이후 단계에서 프로젝트 스톰 hello에 대 한 참조로 tooadd 있습니다.

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. Eclipse에서 새 Maven 프로젝트를 만듭니다(**파일**, **새로 만들기**, **프로젝트**를 차례로 클릭).
   
    ![][12]
5. **Use default Workspace location**(기본 작업 영역 위치 사용)을 선택하고 **다음**을 클릭합니다.
6. 선택 hello **maven-아키타-빠른 시작** 아키타, 클릭 **다음**
7. **GroupId** 및 **ArtifactId**를 삽입하고 **마침**을 클릭합니다.
8. **pom.xml**, hello에서 종속성을 따라 hello 추가 `<dependency>` 노드.

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. Hello에 **src** 폴더를 파일을 만들 **Config.properties** 및 콘텐츠에 따라, hello 대체 복사본 hello `receive rule key` 및 `event hub name` 값:

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    값에 대 한 hello **eventhub.receiver.credits** 이벤트 개수 내용이 toohello 스톰 파이프라인을 릴리스하기 전에 일괄 처리를 결정 합니다. 간단한 hello 위해서이 예제에서는이 값 too10를 설정합니다. 프로덕션 환경에서 일반적으로 설정 해야 toohigher 값이 있습니다. 예를 들어 1024입니다.
10. 라는 새 클래스를 만들고 **LoggerBolt** 코드 다음 hello로:
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    이 스톰 볼트 hello 받은 이벤트 hello 콘텐츠를 기록합니다. 이 수 쉽게 확장할 toostore 튜플은 저장소 서비스에서. hello [HDInsight 센서 분석 자습서] 이와 동일한 접근 방식을 toostore 데이터를 사용 하 여 HBase로 합니다.
11. 라는 클래스를 만들고 **LogTopology** 코드 다음 hello로:
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    이 클래스는 hello 속성을 사용 하 여 구성 파일 tooinstantiate hello에에서 새 이벤트 허브 배출구 만듭니다 것입니다. 이 예제에서는 많은 만듭니다 toonote hello hello 이벤트 허브의 파티션 수가으로 작업 순서 toouse hello 최대 병렬 처리 수준에서 해당 이벤트 허브 허용에 spouts 유용 합니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [Event Hubs 개요][Event Hubs overview]
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[HDInsight 센서 분석 자습서]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
