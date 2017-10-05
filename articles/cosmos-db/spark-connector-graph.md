---
title: "Azure Cosmos DB: Spark 및 Apache TinkerPop Gremlin을 사용하여 그래프 분석 수행 | Microsoft Docs"
description: "이 문서에서는 Spark와 TinkerPop SparkGraphComputer를 사용하여 Azure Cosmos DB에서 그래프 분석 및 병렬 계산을 설정하고 실행하는 지침을 제공합니다."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="f37b7-103">Azure Cosmos DB: Spark 및 Apache TinkerPop Gremlin을 사용하여 그래프 분석 수행</span><span class="sxs-lookup"><span data-stu-id="f37b7-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="f37b7-104">[Azure Cosmos DB](introduction.md)는 Microsoft에서 제공하는 전 세계에 배포된 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="f37b7-105">Azure Cosmos DB의 코어인 전역 배포 및 수평적 규모 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="f37b7-106">Azure Cosmos DB는 [Apache TinkerPop Gremlin](graph-introduction.md)을 사용하는 OLTP(온라인 트랜잭션 처리) 그래프 워크로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="f37b7-107">[Spark](http://spark.apache.org/)는 범용 OLAP(온라인 분석 처리) 데이터 처리에 중점을 둔 Apache Software Foundation 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="f37b7-108">Spark는 Hadoop MapReduce 모델과 유사한 하이브리드 메모리 내/디스크 기반 분산형 컴퓨팅 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="f37b7-109">Apache Spark는 클라우드에서 [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)를 사용하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="f37b7-110">Azure Cosmos DB와 Spark를 결합하여 Gremlin을 사용할 때 OLTP와 OLAP 워크로드를 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="f37b7-111">이 빠른 시작 문서는 Azure HDInsight Spark 클러스터에서 Azure Cosmos DB에 Gremlin 쿼리를 실행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f37b7-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f37b7-112">Prerequisites</span></span>

<span data-ttu-id="f37b7-113">이 샘플을 실행하기 전에 다음 필수 조건이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="f37b7-114">Azure HDInsight Spark 클러스터 2.0</span><span class="sxs-lookup"><span data-stu-id="f37b7-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="f37b7-115">JDK 1.8+(JDK가 없는 경우 `apt-get install default-jdk` 실행)</span><span class="sxs-lookup"><span data-stu-id="f37b7-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="f37b7-116">Maven(Maven이 없는 경우 `apt-get install maven` 실행)</span><span class="sxs-lookup"><span data-stu-id="f37b7-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="f37b7-117">Azure 구독([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="f37b7-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="f37b7-118">Azure HDInsight Spark 클러스터를 설정하는 방법에 대한 자세한 내용은 [HDInsight 클러스터 프로비전](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f37b7-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="f37b7-119">Azure Cosmos DB 데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f37b7-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="f37b7-120">먼저 다음을 수행하여 Graph API로 데이터베이스 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="f37b7-121">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="f37b7-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="f37b7-122">Apache TinkerPop 가져오기</span><span class="sxs-lookup"><span data-stu-id="f37b7-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="f37b7-123">다음을 수행하여 Apache TinkerPop을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="f37b7-124">HDInsight 클러스터 `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`의 마스터 노드에 원격 연결</span><span class="sxs-lookup"><span data-stu-id="f37b7-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="f37b7-125">TinkerPop3 소스 코드 복제, 로컬에서 빌드 및 Maven 캐시에 설치</span><span class="sxs-lookup"><span data-stu-id="f37b7-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="f37b7-126">Spark-Gremlin 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="f37b7-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="f37b7-127">a.</span><span class="sxs-lookup"><span data-stu-id="f37b7-127">a.</span></span> <span data-ttu-id="f37b7-128">플러그 인 설치는 Grape에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="f37b7-129">플러그인과 해당 종속성을 다운로드 할 수 있도록 Grape에 대한 리포지토리 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="f37b7-130">`~/.groovy/grapeConfig.xml`에 grape 구성 파일이 없으면 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="f37b7-131">다음 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-131">Use the following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="f37b7-132">b.</span><span class="sxs-lookup"><span data-stu-id="f37b7-132">b.</span></span> <span data-ttu-id="f37b7-133">Gremlin 콘솔 `bin/gremlin.sh`을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="f37b7-134">c.</span><span class="sxs-lookup"><span data-stu-id="f37b7-134">c.</span></span> <span data-ttu-id="f37b7-135">이전 단계에서 빌드한 버전 3.3.0-SNAPSHOT으로 Spark-Gremlin 플러그인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="f37b7-136">`Hadoop-Gremlin`이 `:plugin list`를 사용하여 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="f37b7-137">Spark Gremlin 플러그 인 `:plugin unuse tinkerpop.hadoop`을 방해할 수 있기 때문에 이 플러그 인을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="f37b7-138">TinkerPop3 종속성 준비</span><span class="sxs-lookup"><span data-stu-id="f37b7-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="f37b7-139">이전 단계에서 TinkerPop3을 빌드할 때 프로세스는 대상 디렉터리에 있는 Spark 및 Hadoop의 모든 jar 종속성도 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="f37b7-140">HDI로 미리 설치된 jar 파일을 사용하고 필요한 대로 추가 종속성만 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="f37b7-141">`tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`에서 Gremlin 콘솔 대상 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="f37b7-142">`ext/`에서 모든 jar를 `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`으로 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="f37b7-143">아래 목록에 없는 `lib/`에서 모든 jar 라이브러리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="f37b7-144">Azure Cosmos DB Spark 커넥터 가져오기</span><span class="sxs-lookup"><span data-stu-id="f37b7-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="f37b7-145">Azure Cosmos DB Spark 커넥터 `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` 및 Cosmos DB Java SDK`azure-documentdb-1.10.0.jar`를 [GitHub의 Azure Cosmos DB Spark 커넥터](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11)에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="f37b7-146">또는 로컬에서 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="f37b7-147">최신 버전의 Spark-Gremlin이 Spark 1.6.1로 빌드되었고 Azure Cosmos DB Spark 커넥터에서 현재 사용되는 Spark 2.0.2와 호환되지 않으므로 수동으로 최신 TinkerPop3 코드를 빌드하고 jar를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="f37b7-148">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-148">Do the following:</span></span>

    <span data-ttu-id="f37b7-149">a.</span><span class="sxs-lookup"><span data-stu-id="f37b7-149">a.</span></span> <span data-ttu-id="f37b7-150">Azure Cosmos DB Spark 커넥터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="f37b7-151">b.</span><span class="sxs-lookup"><span data-stu-id="f37b7-151">b.</span></span> <span data-ttu-id="f37b7-152">TinkerPop3 빌드(이전 단계에서 이미 수행됨).</span><span class="sxs-lookup"><span data-stu-id="f37b7-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="f37b7-153">모든 TinkerPop 3.3.0-SNAPSHOT jar를 로컬로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="f37b7-154">c.</span><span class="sxs-lookup"><span data-stu-id="f37b7-154">c.</span></span> <span data-ttu-id="f37b7-155">`tinkerpop.version` `azure-documentdb-spark/pom.xml`를 `3.3.0-SNAPSHOT`으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="f37b7-156">d.</span><span class="sxs-lookup"><span data-stu-id="f37b7-156">d.</span></span> <span data-ttu-id="f37b7-157">Maven으로 빌드.</span><span class="sxs-lookup"><span data-stu-id="f37b7-157">Build with Maven.</span></span> <span data-ttu-id="f37b7-158">필요한 jar가 `target` 및 `target/alternateLocation`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="f37b7-159">이전에 언급한 jar를 로컬 디렉터리 ~/azure-documentdb-spark에 복사</span><span class="sxs-lookup"><span data-stu-id="f37b7-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="f37b7-160">종속성을 Spark 작업자 노드에 배포</span><span class="sxs-lookup"><span data-stu-id="f37b7-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="f37b7-161">그래프 데이터의 변환이 TinkerPop3에 달려 있기 때문에 관련 종속성을 모든 Spark 작업자 노드에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="f37b7-162">이전에 언급한 Gremlin 종속성과 CosmosDB Spark 커넥터 jar 및 CosmosDB Java SDK를 다음과 같이 작업자 노드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="f37b7-163">a.</span><span class="sxs-lookup"><span data-stu-id="f37b7-163">a.</span></span> <span data-ttu-id="f37b7-164">모든 jar를 `~/azure-documentdb-spark`에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="f37b7-165">b.</span><span class="sxs-lookup"><span data-stu-id="f37b7-165">b.</span></span> <span data-ttu-id="f37b7-166">Ambari 대시보드에 있는 `Spark2` 섹션의 `Spark2 Clients` 리스트에서 모든 Spark 작업자 노드의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="f37b7-167">c.</span><span class="sxs-lookup"><span data-stu-id="f37b7-167">c.</span></span> <span data-ttu-id="f37b7-168">해당 디렉터리를 각 노드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="f37b7-169">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="f37b7-169">Set up the environment variables</span></span>

1. <span data-ttu-id="f37b7-170">Spark 클러스터의 HDP 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="f37b7-171">`/usr/hdp/`에서 디렉터리 이름입니다(예: 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="f37b7-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="f37b7-172">모든 노드에 hdp.version을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="f37b7-173">Ambari 대시보드에서 **YARN 섹션** > **구성** > **고급**으로 이동하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="f37b7-174">a.</span><span class="sxs-lookup"><span data-stu-id="f37b7-174">a.</span></span> <span data-ttu-id="f37b7-175">`Custom yarn-site`에서 마스터 노드의 HDP 버전 값으로 새 속성 `hdp.version`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="f37b7-176">b.</span><span class="sxs-lookup"><span data-stu-id="f37b7-176">b.</span></span> <span data-ttu-id="f37b7-177">구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-177">Save the configurations.</span></span> <span data-ttu-id="f37b7-178">발생한 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="f37b7-179">c.</span><span class="sxs-lookup"><span data-stu-id="f37b7-179">c.</span></span> <span data-ttu-id="f37b7-180">알림 아이콘이 나타내는 대로 YARN 및 Oozie 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="f37b7-181">마스터 노드에서 다음 환경 변수를 설정(적절하게 값을 대체)합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="f37b7-182">그래프 구성 준비</span><span class="sxs-lookup"><span data-stu-id="f37b7-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="f37b7-183">Azure Cosmos DB 연결 매개 변수와 Spark 설정으로 구성 파일을 생성하고 `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for the driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="f37b7-184">이 경우에 이전 단계에서 배포한 jar 디렉터리를 포함하도록 `spark.driver.extraClassPath` 및 `spark.executor.extraClassPath`를 `/home/sshuser/azure-documentdb-spark/*`으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="f37b7-185">Azure Cosmos DB에 다음 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="f37b7-186">TinkerPop 그래프를 로드하고 Azure Cosmos DB에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="f37b7-187">Azure Cosmos DB에 그래프를 유지할 수 있는 방법을 보여주려면 이 예제에서는 TinkerPop 미리 정의된 TinkerPop 최신 그래프를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="f37b7-188">그래프는 Kryo 형식으로 저장되었으며 TinkerPop 리포지토리에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="f37b7-189">Gremlin을 YARN 모드로 실행하기 때문에 Hadoop 파일 시스템에서 그래프 데이터를 사용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="f37b7-190">다음 명령을 사용하여 디렉터리를 만들고 그 안에 로컬 그래프 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="f37b7-191">그래프를 읽기 위해 `GryoInputFormat`을 사용하도록 `gremlin-spark.properties` 파일을 임시로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="f37b7-192">또한 `inputLocation`을 다음과 같이 만든 디렉터리로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="f37b7-193">Gremlin 콘솔을 시작하고 다음 계산 단계를 만들어서 구성된 Azure Cosmos DB 컬렉션에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="f37b7-194">a.</span><span class="sxs-lookup"><span data-stu-id="f37b7-194">a.</span></span> <span data-ttu-id="f37b7-195">`graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")` 그래프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="f37b7-196">b.</span><span class="sxs-lookup"><span data-stu-id="f37b7-196">b.</span></span> <span data-ttu-id="f37b7-197">`graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`을 작성하기 위해 SparkGraphComputer를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="f37b7-198">데이터 탐색기에서 Azure Cosmos DB에 데이터가 유지되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="f37b7-199">Azure Cosmos DB에서 그래프를 로드하고 Gremlin 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="f37b7-200">그래프를 로드하려면 `graphReader`를 `DocumentDBInputRDD`로 설정하도록 `gremlin-spark.properties`를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="f37b7-201">다음을 수행하여 그래프를 로드하고 데이터를 순회한 다음 Gremlin 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="f37b7-202">a.</span><span class="sxs-lookup"><span data-stu-id="f37b7-202">a.</span></span> <span data-ttu-id="f37b7-203">Gremlin 콘솔 `bin/gremlin.sh`을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="f37b7-204">b.</span><span class="sxs-lookup"><span data-stu-id="f37b7-204">b.</span></span> <span data-ttu-id="f37b7-205">`graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')` 구성으로 그래프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="f37b7-206">c.</span><span class="sxs-lookup"><span data-stu-id="f37b7-206">c.</span></span> <span data-ttu-id="f37b7-207">SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`로 그래프 순회를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="f37b7-208">d.</span><span class="sxs-lookup"><span data-stu-id="f37b7-208">d.</span></span> <span data-ttu-id="f37b7-209">다음 Gremlin 그래프 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-209">Run the following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="f37b7-210">자세한 로그를 보려면 `conf/log4j-console.properties`의 로그 수준을 보다 자세한 수준으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="f37b7-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f37b7-211">Next steps</span></span>

<span data-ttu-id="f37b7-212">이 빠른 시작 문서에서는 Azure Cosmos DB와 Spark를 결합하여 그래프를 사용하는 방법을 알아 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f37b7-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
