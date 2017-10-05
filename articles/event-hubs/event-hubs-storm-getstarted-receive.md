---
title: "Apache Storm을 사용하여 Azure Event Hubs에서 이벤트 수신 | Microsoft Docs"
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
ms.openlocfilehash: 3e15370c7602276ef323708632b324fe05497f41
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="0f7b6-103">Apache Storm을 사용하여 Event Hubs에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="0f7b6-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="0f7b6-104">[Apache Storm](https://storm.incubator.apache.org)은 분산된 실시간 계산 시스템으로, 바인딩되지 않은 데이터 스트림의 안정적인 처리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="0f7b6-105">이 섹션에서는 Azure Event Hubs Storm Spout를 사용하여 Event Hubs에서 이벤트를 수신하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="0f7b6-106">Apache Storm을 사용하면 다른 노드에 호스트된 여러 프로세스 간에 이벤트를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="0f7b6-107">이벤트 허브와 Storm을 통합하면 Storm의 Zookeeper 설치를 통해 진행률을 투명하게 확인하고 지속적인 검사점을 관리하여 이벤트 사용이 간소화되고 이벤트 허브에서 병렬 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="0f7b6-108">Event Hubs 수신기 패턴에 대한 자세한 내용은 [Event Hubs 개요][Event Hubs overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="0f7b6-109">프로젝트 만들기 및 코드 추가</span><span class="sxs-lookup"><span data-stu-id="0f7b6-109">Create project and add code</span></span>

<span data-ttu-id="0f7b6-110">이 자습서에서는 이미 사용할 수 있는 이벤트 허브 spout와 함께 제공되는 [HDInsight Storm][HDInsight Storm] 설치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="0f7b6-111">[HDInsight Storm - 시작 절차](../hdinsight/hdinsight-storm-overview.md)에 따라 새 HDInsight 클러스터를 만들고 원격 데스크톱을 통해 이 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-111">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="0f7b6-112">`%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` 파일을 로컬 개발 환경에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-112">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="0f7b6-113">이 파일에는 events-storm-spout가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-113">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="0f7b6-114">다음 명령을 사용하여 패키지를 로컬 Maven 저장소에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-114">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="0f7b6-115">그러면 이후 단계에서 Storm 프로젝트에 참조로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-115">This enables you to add it as a reference in the Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="0f7b6-116">Eclipse에서 새 Maven 프로젝트를 만듭니다(**파일**, **새로 만들기**, **프로젝트**를 차례로 클릭).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="0f7b6-117">**Use default Workspace location**(기본 작업 영역 위치 사용)을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="0f7b6-118">**maven-archetype-quickstart** 원형을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-118">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="0f7b6-119">**GroupId** 및 **ArtifactId**를 삽입하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="0f7b6-120">**pom.xml**에서 `<dependency>` 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-120">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>

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

9. <span data-ttu-id="0f7b6-121">**src** 폴더에서 **Config.properties**라는 파일을 만들고 다음 콘텐츠를 복사하여 `receive rule key` 및 `event hub name` 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-121">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="0f7b6-122">**eventhub.receiver.credits** 의 값에 따라 이벤트를 Storm 파이프라인으로 릴리스하기 전에 얼마나 많은 수의 이벤트가 일괄 처리되는지 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-122">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="0f7b6-123">간단히 하기 위해 이 예에서는 이 값을 10으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-123">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="0f7b6-124">프로덕션 환경에서 일반적으로 더 높게(예: 1024) 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-124">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="0f7b6-125">다음 코드를 포함하는 **LoggerBolt** 클래스를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-125">Create a new class called **LoggerBolt** with the following code:</span></span>
    
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
    
    <span data-ttu-id="0f7b6-126">이 Storm 볼트는 수신된 이벤트의 콘텐츠를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-126">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="0f7b6-127">튜플을 저장소 서비스에 저장하도록 간단히 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-127">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="0f7b6-128">[HDInsight 센서 분석 자습서]에서는 동일한 방법을 사용하여 데이터를 HBase에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-128">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="0f7b6-129">다음 코드를 포함하는 **LogTopology**라는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-129">Create a class called **LogTopology** with the following code:</span></span>
    
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
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
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

    <span data-ttu-id="0f7b6-130">이 클래스는 새 Event Hubs spout를 만들고, 구성 파일의 속성을 사용하여 spout를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-130">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="0f7b6-131">이 예에서는 이벤트 허브에서 허용하는 최대 병렬 처리를 사용하기 위해 이벤트 허브의 파티션 수만큼 Spout 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-131">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f7b6-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f7b6-132">Next steps</span></span>
<span data-ttu-id="0f7b6-133">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-133">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="0f7b6-134">[Event Hubs 개요][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="0f7b6-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="0f7b6-135">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="0f7b6-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="0f7b6-136">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="0f7b6-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
<span data-ttu-id="0f7b6-137">[HDInsight 센서 분석 자습서]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span><span class="sxs-lookup"><span data-stu-id="0f7b6-137">[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span></span>

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
