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
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="61fa9-103">Apache Storm을 사용하여 Event Hubs에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="61fa9-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="61fa9-104">[Apache Storm](https://storm.incubator.apache.org)은 분산된 실시간 계산 시스템으로, 바인딩되지 않은 데이터 스트림의 안정적인 처리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="61fa9-105">이 섹션에서는 Azure 이벤트 허브 스톰 toouse 이벤트 허브에서 tooreceive 이벤트 spout 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="61fa9-106">Apache Storm을 사용하면 다른 노드에 호스트된 여러 프로세스 간에 이벤트를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="61fa9-107">hello 스톰와 이벤트 허브 통합 단순화 이벤트 소비 검사점을 투명 하 게 설정 하 여 진행 상황을 Storm의 사육 설치를 사용 하 여 영구 검사점 관리 및 이벤트 허브에서 병렬 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="61fa9-108">이벤트 허브에 대 한 자세한 정보에 대 한 패턴을 수신 hello를 참조 하십시오 [이벤트 허브 개요][Event Hubs overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="61fa9-109">프로젝트 만들기 및 코드 추가</span><span class="sxs-lookup"><span data-stu-id="61fa9-109">Create project and add code</span></span>

<span data-ttu-id="61fa9-110">이 자습서에서는 [HDInsight 스톰] [ HDInsight Storm] 설치와 함께 제공 되 이벤트 허브 spout hello 이미 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="61fa9-111">Hello에 따라 [HDInsight 스톰-시작](../hdinsight/hdinsight-storm-overview.md) 프로시저 toocreate 새 HDInsight tooit 원격 데스크톱을 통해 연결 하 고, 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="61fa9-112">복사 hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` 파일 tooyour 로컬 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="61fa9-113">이 hello 이벤트 스톰 배출구 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="61fa9-114">Hello 명령 tooinstall hello 패키지 hello 로컬 Maven 저장소로 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="61fa9-115">이렇게 하면 이후 단계에서 프로젝트 스톰 hello에 대 한 참조로 tooadd 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="61fa9-116">Eclipse에서 새 Maven 프로젝트를 만듭니다(**파일**, **새로 만들기**, **프로젝트**를 차례로 클릭).</span><span class="sxs-lookup"><span data-stu-id="61fa9-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="61fa9-117">**Use default Workspace location**(기본 작업 영역 위치 사용)을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="61fa9-118">선택 hello **maven-아키타-빠른 시작** 아키타, 클릭 **다음**</span><span class="sxs-lookup"><span data-stu-id="61fa9-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="61fa9-119">**GroupId** 및 **ArtifactId**를 삽입하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="61fa9-120">**pom.xml**, hello에서 종속성을 따라 hello 추가 `<dependency>` 노드.</span><span class="sxs-lookup"><span data-stu-id="61fa9-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

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

9. <span data-ttu-id="61fa9-121">Hello에 **src** 폴더를 파일을 만들 **Config.properties** 및 콘텐츠에 따라, hello 대체 복사본 hello `receive rule key` 및 `event hub name` 값:</span><span class="sxs-lookup"><span data-stu-id="61fa9-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="61fa9-122">값에 대 한 hello **eventhub.receiver.credits** 이벤트 개수 내용이 toohello 스톰 파이프라인을 릴리스하기 전에 일괄 처리를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="61fa9-123">간단한 hello 위해서이 예제에서는이 값 too10를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="61fa9-124">프로덕션 환경에서 일반적으로 설정 해야 toohigher 값이 있습니다. 예를 들어 1024입니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="61fa9-125">라는 새 클래스를 만들고 **LoggerBolt** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="61fa9-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
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
    
    <span data-ttu-id="61fa9-126">이 스톰 볼트 hello 받은 이벤트 hello 콘텐츠를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="61fa9-127">이 수 쉽게 확장할 toostore 튜플은 저장소 서비스에서.</span><span class="sxs-lookup"><span data-stu-id="61fa9-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="61fa9-128">hello [HDInsight 센서 분석 자습서] 이와 동일한 접근 방식을 toostore 데이터를 사용 하 여 HBase로 합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="61fa9-129">라는 클래스를 만들고 **LogTopology** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="61fa9-129">Create a class called **LogTopology** with hello following code:</span></span>
    
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

    <span data-ttu-id="61fa9-130">이 클래스는 hello 속성을 사용 하 여 구성 파일 tooinstantiate hello에에서 새 이벤트 허브 배출구 만듭니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="61fa9-131">이 예제에서는 많은 만듭니다 toonote hello hello 이벤트 허브의 파티션 수가으로 작업 순서 toouse hello 최대 병렬 처리 수준에서 해당 이벤트 허브 허용에 spouts 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61fa9-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61fa9-132">Next steps</span></span>
<span data-ttu-id="61fa9-133">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61fa9-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="61fa9-134">[Event Hubs 개요][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="61fa9-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="61fa9-135">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="61fa9-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="61fa9-136">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="61fa9-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[HDInsight 센서 분석 자습서]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
