---
title: "Azure HDInsight aaaApache 스톰 Java 토폴로지 예제-| Microsoft Docs"
description: "Java 예제 word 만들어 toocreate Apache Storm 토폴로지에 토폴로지를 계산 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm,apache storm example,storm java,storm topology example
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Java에서 Apache Storm 토폴로지 만들기

자세한 내용은 방법 toocreate Apache Storm의 Java 기반 토폴로지입니다. 단어 계산 응용 프로그램을 구현하는 Storm 토폴로지를 만들어야 합니다. Maven toobuild 및 패키지 hello 프로젝트를 사용 합니다. 그런 다음 어떻게 결정 프레임 워크를 사용 하 여 toodefine hello 토폴로지 hello 방법을 배웁니다.

> [!NOTE]
> hello 표적이 프레임 워크 이상 스톰 0.10.0에서에서 사용할 수는 있습니다. Storm 0.10.0은 HDInsight 3.3 및 3.4에서 사용할 수 있습니다.

이 문서의 hello 단계를 완료 한 후 hello 토폴로지 tooApache 스톰 HDInsight에 배포할 수 있습니다.

> [!NOTE]
> 이 문서에서 만든 hello 스톰 토폴로지 예제의 전체 버전에서 제공 됩니다. [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount)합니다.

## <a name="prerequisites"></a>필수 조건

* [JDK(Java Developer Kit) 버전 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven(https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Java 프로젝트를 위한 프로젝트 빌드 시스템입니다.

* 텍스트 편집기 또는 IDE

## <a name="configure-environment-variables"></a>환경 변수 구성

hello 다음과 같은 환경 변수 설정 되어 있습니다 Java 및 hello JDK 설치. 그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.

* **JAVA_HOME** -toohello hello Java runtime environment (JRE)가 설치 디렉터리를 가리켜야 합니다. 예를 들어, Unix 또는 Linux 배포 없어야과 유사한 값 너무`/usr/lib/jvm/java-7-oracle`합니다. Windows에서 동일 하 게과 유사한 값 너무`c:\Program Files (x86)\Java\jre1.7`

* **경로** -hello 다음 경로 포함 해야 합니다.

  * **JAVA_HOME** (또는 hello 해당 하는 경로)

  * **JAVA_HOME\bin** (또는 hello 해당 하는 경로)

  * Maven 설치 되어 있는 hello 디렉터리

## <a name="create-a-maven-project"></a>Maven 프로젝트 만들기

Hello 명령줄에서 사용 하 여 hello 다음 명령은 toocreate 라는 Maven 프로젝트가 **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> PowerShell을 사용하는 경우 큰 따옴표로 `-D` 매개 변수를 묶어야 합니다.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

이 명령은 라는 디렉터리를 만듭니다. `WordCount` 기본 Maven 프로젝트를 포함 하는 hello 현재 위치에 있습니다. hello `WordCount` hello 다음 항목을 포함 하는 디렉터리:

* `pom.xml`: Hello Maven 프로젝트에 대 한 설정을 포함합니다.
* `src\main\java\com\microsoft\example`: 응용 프로그램 코드를 포함합니다.
* `src\test\java\com\microsoft\example`: 응용 프로그램에 대한 테스트를 포함합니다. 

### <a name="remove-hello-generated-example-code"></a>예제 코드를 생성 하는 hello 제거

생성 된 hello 테스트 및 hello 응용 프로그램 파일을 삭제 합니다.

* **src\test\java\com\microsoft\example\AppTest.java**
* **src\main\java\com\microsoft\example\App.java**

## <a name="add-maven-repositories"></a>Maven 리포지토리 추가

HDInsight는 hello Hortonworks Data Platform (HDP)에 기반 하므로 Apache Storm 프로젝트에 대 한 hello Hortonworks 리포지토리 toodownload 종속성을 사용 하는 것이 좋습니다. Hello에 __pom.xml__ 파일에서 다음과 같은 XML hello 후 hello 추가 `<url>http://maven.apache.org</url>` 줄:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>속성 추가

Maven 속성 이라는 toodefine 프로젝트 수준 값을 허용 합니다. Hello에 __pom.xml__, hello 텍스트 hello 후 다음 추가 `</repositories>` 줄:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

이제 hello의 다른 섹션에서이 값을 사용할 수 `pom.xml`합니다. 예를 들어 hello 버전의 Storm 구성 요소를 지정할 때는 사용할 수 있습니다 `${storm.version}` 하드 코딩 된 값 대신 합니다.

## <a name="add-dependencies"></a>종속성 추가

Storm 구성 요소에 대한 종속성을 추가합니다. 열기 hello `pom.xml` 파일 및 코드 hello에 다음 hello 추가 `<dependencies>` 섹션:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

컴파일 타임에 Maven 소진이 정보 toolook `storm-core` hello Maven 리포지토리에 합니다. 먼저 로컬 컴퓨터에 대 한 hello 리포지토리에 찾습니다. Hello 파일 반영 되지 않을, Maven hello 공개 Maven 저장소에서 다운로드 hello 로컬 저장소에 저장 합니다.

> [!NOTE]
> 공지 hello `<scope>provided</scope>` 줄이이 섹션에 있습니다. 이 설정은 Maven tooexclude를 알려 줍니다. **스톰 코어** hello 시스템에서 제공 되기 때문에 생성 된 JAR 파일에서입니다.

## <a name="build-configuration"></a>빌드 구성

Maven 플러그 인을 사용 하면 hello 프로젝트의 toocustomize hello 빌드 단계 있습니다. Hello 프로젝트 컴파일 방식을 예를 들어 방식이 나 toopackage JAR 파일을 넣습니다. 열기 hello `pom.xml` 파일 및 코드 hello 바로 위에 다음 hello 추가 `</project>` 선입니다.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

이 섹션에 사용 되는 tooadd 플러그 인, 리소스 및 기타 빌드 구성 옵션입니다. 전체 참조의 hello **pom.xml** 파일, 참조 [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html)합니다.

### <a name="add-plug-ins"></a>플러그 인 추가

Java에서 구현 되는 Apache Storm 토폴로지, hello [Exec Maven 플러그 인](http://www.mojohaus.org/exec-maven-plugin/) tooeasily 개발 환경에서 hello 토폴로지를 로컬로 실행할 수 있기 때문에 유용 합니다. Hello toohello 다음 추가 `<plugins>` hello 섹션 `pom.xml` tooinclude hello Exec Maven 플러그 인 파일:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

유용한 다른 플러그 인은 hello [Apache Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/), 어떤가 사용 되는 toochange 컴파일 옵션입니다. hello 변경 hello Maven hello 원본과 응용 프로그램에 대 한 대상에 대 한 사용 하는 Java 버전입니다.

* HDInsight에 대 한 __3.4 또는 이전 버전__hello 소스 설정, 및 Java 버전 too__1.7__ 대상으로 합니다.

* HDInsight에 대 한 __3.5__hello 소스 설정, 및 Java 버전 too__1.8__ 대상으로 합니다.

Hello hello에서 텍스트 다음 추가 `<plugins>` hello 섹션 `pom.xml` tooinclude hello Apache Maven 컴파일러 플러그 인 파일입니다. 이 예에서는 hello 대상 HDInsight 버전은 3.5 1.8을 지정 합니다.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>리소스 구성

hello 리소스 섹션 hello 토폴로지의 구성 요소에 필요한 구성 파일과 같은 tooinclude 비 코드 리소스를 허용 합니다. 예를 들어 hello hello에서 텍스트 다음 추가 `<resources>` hello 섹션 ' pom.xml 파일입니다.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

Hello 프로젝트의 hello 루트에서 hello resources 디렉터리를 추가 하는이 예제 (`${basedir}`) 리소스를 포함 하 고 라는 hello 파일을 포함 한 위치로 `log4j2.xml`합니다. 이 파일은 hello 토폴로지에서 정보를 기록 하는 사용 되는 tooconfigure 합니다.

## <a name="create-hello-topology"></a>Hello 토폴로지 만들기

Java 기반 Apache Storm 토폴로지는 사용자가 작성자이거나 종속성으로 참조되는 세 개의 구성 요소로 이루어져 있습니다.

* **Spouts**: 외부에서 데이터 원본 및 데이터 스트림을 hello 토폴로지 내보냅니다 읽습니다.

* **Bolt**: Spout 또는 다른 Bolt가 내보낸 스트림에서 처리를 수행하고 하나 이상의 스트림을 내보냅니다.

* **토폴로지**: 및 방법을 정의 hello spouts 볼트 정리 되 고 hello 토폴로지에 대 한 hello 진입점을 제공 합니다.

### <a name="create-hello-spout"></a>Hello 배출구 만들기

다음 외부 데이터 소스를 설정 하기 위한 요구 사항 tooreduce hello 배출구 단순히 임의의 문장을 내보냅니다. Hello로 제공 되는 배출구의 수정 된 버전이 [스톰 스타터 예제](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter)합니다.

> [!NOTE]
> 외부 데이터 원본에서 읽는 배출구의 예 예제 따르는 hello 중 하나를 참조 합니다.
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): Twitter에서 읽는 예제 Spout
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): Kafka에서 읽는 Spout

Hello 배출구 라는 파일을 만들 `RandomSentenceSpout.java` hello에 `src\main\java\com\microsoft\example` Java 코드를 hello 내용으로 다음 디렉터리 및 사용 하 여 hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> 이 토폴로지 하나만 배출구를 사용 하지만 다른 hello 토폴로지에 서로 다른 원본의 데이터를 공급 하는 몇 가지 있을 수 있습니다.

### <a name="create-hello-bolts"></a>Hello 볼트 만들기

볼트 hello 데이터 처리를 처리합니다. 이 토폴로지는 두 개의 bolt를 사용합니다.

* **SplitSentence**: hello 문장에서 내보낸 분할 **RandomSentenceSpout** 개별 단어로 나눕니다.

* **WordCount**: 각각의 단어가 발생한 횟수를 계산합니다.

> [!NOTE]
> 볼트 것, 예를 들어, 계산, 저장, 또는 tooexternal 구성 요소와 통신 작업을 수행할 수 있습니다.

두 개의 새 파일 만들기 `SplitSentence.java` 및 `WordCount.java` hello에 `src\main\java\com\microsoft\example` 디렉터리입니다. Hello 콘텐츠로 사용 hello 파일에 대 한 텍스트를 다음 hello를 사용 합니다.

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Hello 토폴로지 정의

hello 토폴로지 hello spouts 연결 및 hello 구성 요소 간 데이터 흐름 방식을 정의 하는 그래프로 함께 쐐기 합니다. 또한 스톰 hello 클러스터 내에서 hello 구성 요소의 인스턴스를 만들 때 사용 되는 병렬 처리 수준 힌트를 제공 합니다.

hello 다음 그림은이 토폴로지에 대 한 구성 요소의 hello 그래프의 기본 다이어그램.

![다이어그램 보여 주는 hello spouts 및 쐐기 정렬](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement 토폴로지 hello, 라는 파일을 만들어 `WordCountTopology.java` hello에 `src\main\java\com\microsoft\example` 디렉터리입니다. Hello 파일의 내용을 hello로 Java 코드를 다음 hello를 사용 합니다.

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>로깅 구성

Storm은 Apache Log4j toolog 정보를 사용합니다. 로깅을 구성 하지 않으면 hello 토폴로지 진단 정보를 내보냅니다. 기록 된 값, toocontrol 라는 파일을 만들어 `log4j2.xml` hello에 `resources` 디렉터리입니다. Hello hello 파일의 내용을 hello로 다음과 같은 XML을 사용 합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

이 XML 구성 hello에 대 한 새로운 로거가 `com.microsoft.example` 토폴로지가 예제에 hello 구성 요소를 포함 하는 클래스입니다. hello 수준은이 토폴로지의 구성 요소에서 내보낸 모든 로깅 정보를 캡처하고이 거에 대 한 tootrace를 설정 됩니다.

hello `<Root level="error">` 섹션 hello 루트 수준의 로깅 구성 (모든 항목에 속하지 않은 `com.microsoft.example`) tooonly 로그 오류 정보입니다.

Log4j에 대한 로깅 구성과 관련된 자세한 내용은 [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html)을 참조하세요.

> [!NOTE]
> Storm 버전 0.10.0 이상은 Log4j 2.x를 사용합니다. 이전 버전의 Storm은 로그 구성에 다른 형식을 사용하는 Log4j 1.x를 사용합니다. Hello 오래 된 구성에 대 한 자세한 내용은 참조 하십시오. [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat)합니다.

## <a name="test-hello-topology-locally"></a>로컬로 테스트 hello 토폴로지

Hello 파일을 저장 한 후 다음 명령을 로컬로 토폴로지 tootest hello hello를 사용 합니다.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

이 실행 될 때 hello 토폴로지 시작 정보를 표시 합니다. hello 다음 텍스트는 hello 단어 개수 출력 예입니다.

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

이 예에서는 로그 hello 단어 ' 나타내고 ' 113 번 내보냈습니다. hello 수가 계속 해 서 toogo를 hello 배출구 hello를 지속적으로 내보내는 hello 토폴로지 실행으로 같은 문장입니다.

단어 내보내기와 개수 사이에는 5초의 간격이 있습니다. hello **WordCount** 구성 요소가 구성 되어 tooonly 눈금 튜플 도착할 때 정보를 내보냅니다. 틱 튜플은 5초마다 배달되어야 합니다.

## <a name="convert-hello-topology-tooflux"></a>Hello 토폴로지 tooFlux 변환

결정은 새 프레임 워크 스톰 0.10.0 사용할 수 있는 이상 구현에서 tooseparate 구성이 있습니다. 구성 요소 Java에 여전히 정의 되어 있지만 YAML 파일을 사용 하 여 hello 토폴로지를 정의 합니다. 프로젝트에서 기본 토폴로지 정의 패키지 하거나 hello 토폴로지를 전송할 때 독립 실행형 파일을 사용할 수 있습니다. Hello 토폴로지 tooStorm를 전송할 때 hello YAML 토폴로지 정의의 환경 변수 또는 구성 파일 toopopulate 값을 사용할 수 있습니다.

hello YAML 파일 hello 토폴로지 및 서로 hello 데이터 흐름에 대 한 구성 요소 toouse hello를 정의합니다. Hello jar 파일의 일부로 YAML 파일을 포함할 수 있습니다 또는 외부 YAML 파일을 사용할 수 있습니다.

Flux에 대한 자세한 내용은 [Flux 프레임워크(https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)를 참조하세요.

> [!WARNING]
> 기한 tooa [버그 (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) 1.0.1 스톰 tooinstall을 할 수 있습니다는 [스톰 개발 환경](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun 표적이 토폴로지 로컬로 합니다.

1. Hello 이동 `WordCountTopology.java` hello 프로젝트에서 파일입니다. 이전에이 파일 hello 토폴로지 정의 되지만 결정으로 필요 하지 않습니다.

2. Hello에 `resources` 디렉터리 라는 파일을 만들어 `topology.yaml`합니다. 이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. 다음 변경 내용을 toohello hello 확인 `pom.xml` 파일입니다.
   
   * Hello에 대 한 새 종속성을 따라 hello 추가 `<dependencies>` 섹션:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * 플러그 인 toohello 다음 hello 추가 `<plugins>` 섹션. 이 플러그 인 hello 프로젝트에 대 한 패키지 (jar 파일)의 hello 생성을 처리 하 고 hello 패키지를 만들 때 일부 변환 특정 tooFlux를 적용 합니다.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ```

   * Hello에 **플러그 인 maven-exec-** `<configuration>` 섹션에 대 한 hello 값을 변경 하세요 `<mainClass>` 너무`org.apache.storm.flux.Flux`합니다. 이 설정을 통해 결정 toohandle 개발에서 hello 토폴로지를 로컬로 실행 합니다.

   * Hello에 `<resources>` 섹션을 따라 toohello hello 추가 `<includes>`합니다. 이 XML hello 프로젝트의 일부로 hello 토폴로지를 정의 하는 hello YAML 파일에 포함 됩니다.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>로컬로 hello 표적이 토폴로지를 테스트 합니다.

1. 다음 toocompile hello를 사용 하 고 Maven을 사용 하 여 hello 표적이 토폴로지를 실행 합니다.

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    PowerShell을 사용 하는 경우 다음 명령을 hello를 사용 합니다.

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > 토폴로지가 Storm 1.0.1 비트를 사용하는 경우 이 명령은 실패합니다. 이 문제는 [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055)로 인해 발생합니다. 대신, [스톰 개발 환경에서 설치](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) 다음 정보를 사용 하 여 hello 및 합니다.

    있는 경우 [스톰 개발 환경에 설치](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), hello 명령 대신 다음을 사용할 수 있습니다.

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    hello `--local` 매개 변수 개발 환경에서 로컬 모드에서 hello 토폴로지를 실행 합니다. hello `-R /topology.yaml` hello를 사용 하는 매개 변수 `topology.yaml` hello jar 파일 toodefine hello 토폴로지에서 리소스 파일입니다.

    이 실행 될 때 hello 토폴로지 시작 정보를 표시 합니다. hello 텍스트 다음은 hello 출력의 예:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    기록된 정보 배치 간에 10초의 지연이 있습니다.

2. Hello의 사본을 `topology.yaml` hello 프로젝트에서 파일입니다. 새 파일 이름 hello `newtopology.yaml`합니다. Hello에 `newtopology.yaml` 파일을 찾아 hello 다음 섹션의 값을 hello 변경 `10` 너무`5`합니다. 10 초 too5에서이 수정 변경 내용을 hello 간격 표시 하 고 word의 일괄 처리 사이 계산 합니다.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    또는 개발 환경에서 Storm을 설치한 경우:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    변경 hello `/path/to/newtopology.yaml` hello 이전 단계에서 만든 toohello 경로 toohello newtopology.yaml 파일입니다. 이 명령은 hello 토폴로지 정의를 hello newtopology.yaml를 사용 합니다. Hello 포함 되지 이후 `compile` 매개 변수를 Maven 이전 단계에서 빌드한 hello 프로젝트의 hello 버전을 사용 합니다.

    Hello 한 번 시작 되는 토폴로지를 내보낸된 일괄 처리 간격 hello newtopology.yaml tooreflect hello 값이 변경 되었음을 확인 해야 합니다. 따라서 toorecompile hello 토폴로지 필요 없이 구성의 변경할 YAML 파일을 통해 수 있는지 확인할 수 있습니다.

이러한 기술 및 hello 표적이 framework의 기타 기능에 대 한 자세한 내용은 참조 하십시오. [표적이 (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)합니다.

## <a name="trident"></a>Trident

Trident는 Storm에서 제공하는 높은 수준의 추상화이며 상태 저장 처리를 지원합니다. hello Trident의 주요 이점은 hello 토폴로지가 입력 하는 모든 메시지가 한 번만 처리는 보장할 수입니다. Trident를 사용하지 않으면 토폴로지는 메시지가 최소한 한 번은 처리된다는 것만 보장할 수 있습니다. Bolt를 만드는 대신 사용할 수 있는 기본 제공 구성 요소와 같은 다른 차이점도 있습니다. 사실 Bolt는 필터, 프로젝션 및 함수와 같이 덜 일반적인 구성 요소로 대체됩니다.

Trident 응용 프로그램은 Maven 프로젝트를 사용하여 만들 수 있습니다. Hello를 사용 하 여이 문서의 앞부분에 제공 된 대로 동일한 기본 단계-hello 코드는 다른만 합니다. Trident 수 없습니다 (현재) 함께 사용할 수도 hello 표적이 프레임 워크입니다.

Trident에 대 한 자세한 내용은 참조 hello [Trident API 개요](http://storm.apache.org/documentation/Trident-API-Overview.html)합니다.

Trident 응용 프로그램 예제는 [HDInsight에서 Apache Storm을 사용하는 Twitter 추세 항목](hdinsight-storm-twitter-trending.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

배웠습니다 어떻게 toocreate Java를 사용 하 여 스톰 토폴로지입니다. 이제 다음으로 이동합니다.

* [HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology.md)

* [Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Storm 토폴로지에 대한 추가 예제는 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.

