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
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB: Spark 및 Apache TinkerPop Gremlin을 사용하여 그래프 분석 수행

[Azure Cosmos DB](introduction.md) 세계적으로 분산 된 다중 모델 데이터베이스 서비스로, Microsoft에서 hello 됩니다. 만들기 및 문서, 키/값 및 그래프 데이터베이스의 경우는 모두 Cosmos DB Azure의 hello 핵심 hello 글로벌 메일 및 가로 배율 기능에서 혜택을 쿼리할 수 있습니다. Azure Cosmos DB는 [Apache TinkerPop Gremlin](graph-introduction.md)을 사용하는 OLTP(온라인 트랜잭션 처리) 그래프 워크로드를 지원합니다.

[Spark](http://spark.apache.org/)는 범용 OLAP(온라인 분석 처리) 데이터 처리에 중점을 둔 Apache Software Foundation 프로젝트입니다. Spark는 하이브리드에 메모리/디스크 기반 분산된 하는 컴퓨팅 모델은 비슷한 toohello Hadoop MapReduce 모델을 제공 합니다. 사용 하 여 hello 클라우드에서 Apache Spark를 배포할 수 있습니다 [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)합니다.

Azure Cosmos DB와 Spark를 결합하여 Gremlin을 사용할 때 OLTP와 OLAP 워크로드를 모두 수행할 수 있습니다. 이 빠른 시작 문서 toorun Gremlin Azure Cosmos DB에 대 한 Azure HDInsight Spark 클러스터에서 쿼리 하는 방법을 보여줍니다.

## <a name="prerequisites"></a>필수 조건

이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.
* Azure HDInsight Spark 클러스터 2.0
* JDK 1.8+(JDK가 없는 경우 `apt-get install default-jdk` 실행)
* Maven(Maven이 없는 경우 `apt-get install maven` 실행)
* Azure 구독([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

방법에 대 한 정보에 대 한 Azure HDInsight Spark 클러스터를 tooset 참조 [프로 비전 하는 HDInsight 클러스터](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)합니다.

## <a name="create-an-azure-cosmos-db-database-account"></a>Azure Cosmos DB 데이터베이스 계정 만들기

첫째, hello 다음을 수행 하 여 hello Graph API로 데이터베이스 계정을 만듭니다.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>컬렉션 추가

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Apache TinkerPop 가져오기

Hello 다음을 수행 하 여 Apache TinkerPop를 가져옵니다.

1. Hello HDInsight 클러스터의 마스터 노드에 원격 toohello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`합니다.

2. Hello TinkerPop3 소스 코드를 복제 하 고 로컬로 빌드 tooMaven 캐시를 설치 합니다.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Hello Spark Gremlin 플러그 인 설치 

    a. 플러그 인 hello hello 설치 포도에 의해 처리 됩니다. 플러그 인 hello 및 해당 종속성을 다운로드할 수 있도록 포도 대 한 hello 저장소 정보를 채웁니다. 

      에 없는 경우 hello 포도 구성 파일을 만들 `~/.groovy/grapeConfig.xml`합니다. 다음 설정을 사용 하 여 hello:

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

    b. Gremlin 콘솔 `bin/gremlin.sh`을 시작합니다.
        
    c. Hello Spark Gremlin 플러그 인을 설치 3.3.0-SNAPSHOT hello 이전 단계에서 기본 제공 합니다.

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
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

4. Toosee 여부 확인 `Hadoop-Gremlin` 사용 하 여 활성화 `:plugin list`합니다. 사용 안 함이 플러그 인, 플러그 인이 Spark Gremlin hello로 충돌할 수 있으므로 `:plugin unuse tinkerpop.hadoop`합니다.

## <a name="prepare-tinkerpop3-dependencies"></a>TinkerPop3 종속성 준비

Hello 이전 단계에서 TinkerPop3을 작성할 때 hello 프로세스가 가져왔습니다 모든 jar 종속성 Spark 및 Hadoop에 대 한 hello 대상 디렉터리에 있습니다. HDI와 미리 설치 된 끌어오도록 추가 종속성만 필요에 따라 jar hello를 사용 합니다.

1. 이동 toohello Gremlin 콘솔 대상 디렉터리 `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`합니다. 

2. 모든 jar 이동 `ext/` 너무`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`합니다.

3. 라이브러리에서 모든 jar 제거 `lib/` 있는지에 속하지 않은 hello를 따르는 목록:

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Hello Azure Cosmos DB Spark 커넥터 가져오기

1. Hello Azure Cosmos DB Spark 커넥터 가져오기 `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` 및 Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` 에서 [GitHub의 Azure Cosmos DB Spark 커넥터](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11)합니다.

2. 또는 로컬에서 빌드할 수 있습니다. Spark Gremlin의 hello 최신 버전이 1.6.1 Spark와 함께 빌드된 있고 hello Azure Cosmos DB Spark 커넥터에 현재 사용 되는 Spark 2.0.2와 호환 되지 않습니다 hello 최신 TinkerPop3 코드를 작성 하 고 hello jar를 수동으로 설치할 수 있습니다. 다음 hello지 않습니다.

    a. Hello Azure Cosmos DB Spark 커넥터를 복제 합니다.

    b. TinkerPop3 빌드(이전 단계에서 이미 수행됨). 모든 TinkerPop 3.3.0-SNAPSHOT jar를 로컬로 설치합니다.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. 업데이트 `tinkerpop.version` `azure-documentdb-spark/pom.xml` 너무`3.3.0-SNAPSHOT`합니다.
    
    d. Maven으로 빌드. hello 필요한 jar에 배치 됩니다 `target` 및 `target/alternateLocation`합니다.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. 앞에서 언급 한 jar tooa 로컬 디렉터리에 복사 hello ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Hello 종속성 toohello Spark 작업자 노드를 배포 합니다. 

1. 그래프 데이터의 hello 변환을 TinkerPop3에 의존 하기 때문에 배포 해야 hello 관련 종속성 tooall Spark 작업자 노드.

2. 복사 hello 앞에서 언급 한 Gremlin 종속성, hello CosmosDB Spark 커넥터 jar 및 CosmosDB Java SDK toohello 작업자 노드 hello 다음을 수행 하 여:

    a. 에 모든 hello jar 복사 `~/azure-documentdb-spark`합니다.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Hello hello에서 Ambari 대시보드에서 찾을 수 있는 모든 Spark 작업자 노드 목록이 `Spark2 Clients` hello 목록 `Spark2` 섹션.

    c. 해당 디렉터리 tooeach hello 노드를 복사 합니다.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Hello 환경 변수를 설정 합니다.

1. Hello HDP 버전을의 hello Spark 클러스터를 찾습니다. Hello 디렉터리 이름 아래에서 `/usr/hdp/` (예를 들어 2.5.4.2-7).

2. 모든 노드에 hdp.version을 설정합니다. Ambari 대시보드에 이동 너무**YARN 섹션** > **Configs** > **고급**, 수행가 다음를 hello 다음 및: 
 
    a. `Custom yarn-site`, 새 속성 추가 `hdp.version` hello 마스터 노드에서 hello HDP 버전의 hello 값을 사용 합니다. 
     
    b. Hello 구성을 저장 합니다. 발생한 경고를 무시할 수 있습니다. 
     
    c. Hello 알림 아이콘으로 표시 하는 대로 hello YARN 및 Oozie 서비스를 다시 시작 합니다.

3. 환경 변수 hello 마스터 노드 (적절 하 게 바꾸기 hello 값)에 따라 집합 hello:

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Hello 그래프 구성을 준비합니다

1. 구성 파일을 hello로 Azure Cosmos DB 연결 매개 변수 및 설정, 멤버를 만들고에 넣습니다. `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`합니다.

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

    # Classpath for hello driver and executors
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

2. 업데이트 hello `spark.driver.extraClassPath` 및 `spark.executor.extraClassPath` hello 이전 단계에서이 경우 배포 된 hello jar의 tooinclude hello 디렉터리 `/home/sshuser/azure-documentdb-spark/*`합니다.

3. Hello Azure Cosmos DB에 대 한 다음 세부 정보를 제공 합니다.

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Hello TinkerPop 그래프를 로드 하 고 tooAzure Cosmos DB 저장
toodemonstrate toopersist Azure Cosmos DB를 사용 하 여 hello TinkerPop이이 예제에는 그래프 미리 TinkerPop 최신 그래프를 정의 하는 방법입니다. hello 그래프는 Kryo 형식으로 저장 하 고 hello TinkerPop 저장소에 제공 됩니다.

1. 하므로 Gremlin YARN 모드에서를 실행 하는 확인 해야 hello 그래프 데이터 hello Hadoop 파일 시스템에서에서 사용할 수 있습니다. 사용 하 여 hello 다음 toomake 디렉터리 및 hello 로컬 그래프 파일 복사에는 명령입니다. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. 일시적으로 hello 업데이트 `gremlin-spark.properties` toouse 파일 `GryoInputFormat` tooread hello 그래프입니다. 또한 나타낼 `inputLocation` hello 디렉터리로 만들면 hello 다음과 같이 합니다.

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Gremlin 콘솔을 시작 하 고 계산 단계 toopersist 데이터 구성 toohello Azure Cosmos DB 컬렉션 다음 hello를 만듭니다.  

    a. Hello 그래프 만들기 `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`합니다.

    b. `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`을 작성하기 위해 SparkGraphComputer를 사용합니다.

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

4. 데이터 탐색기에서 해당 hello 된 데이터는 유지 tooAzure Cosmos DB 확인할 수 있습니다.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Azure Cosmos DB에서 hello 그래프를 로드 하 고 Gremlin 쿼리 실행

1. tooload hello 그래프 편집 `gremlin-spark.properties` tooset `graphReader` 너무`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. 부하 hello 그래프 hello 데이터를 트래버스하 고 hello 다음을 수행 하 여 함께 Gremlin 쿼리를 실행 합니다.

    a. Hello Gremlin 콘솔 시작 `bin/gremlin.sh`합니다.

    b. Hello 구성으로 hello 그래프 만들기 `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`합니다.

    c. SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`로 그래프 순회를 만듭니다.

    d. Hello 다음 Gremlin graph 쿼리를 실행 합니다.

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
> 더 자세한 toosee에 hello 로그 수준 설정 로깅, `conf/log4j-console.properties` tooa 더 자세한 수준입니다.
>

## <a name="next-steps"></a>다음 단계

이 빠른 시작 문서와 toowork Azure Cosmos DB 및 Spark 결합 하 여 그래프로 표시 하는 방법을 배웠습니다.

> [!div class="nextstepaction"]
