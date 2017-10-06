---
title: "이벤트 허브 Azure HDInsight의 Apache Spark 스트리밍를 aaaUse | Microsoft Docs"
description: "데이터 toosend tooAzure 이벤트 허브를 스트림 하 고 다음 scala 응용 프로그램을 사용 하 여 HDInsight Spark 클러스터에서 해당 이벤트를 수신 하는 방법에 Apache Spark 스트리밍 샘플을 빌드하십시오."
keywords: "apache spark 스트리밍, spark 스트리밍, spark 샘플, apache spark 스트리밍 예제, 이벤트 허브 azure 샘플, spark 샘플"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Apache Spark 스트리밍: HDInsight에서 Spark 클러스터로 Azure Event Hubs의 데이터 처리

이 문서의 단계를 수행 하는 hello와 관련 된 샘플 스트리밍 Apache Spark는 만들 수 있습니다.

1. 독립 실행형 응용 프로그램 tooingest 메시지를 사용 하 여 Azure 이벤트 허브로 합니다.

2. 두 가지 방법으로 Azure HDInsight의 Spark 클러스터에서 실행 중인 응용 프로그램을 사용 하 여 실시간 이벤트 허브에서 hello 메시지를 검색 합니다.

3. 스트리밍 분석 파이프라인 toopersist 데이터 toodifferent 저장소 시스템을 작성 또는 hello 신속 하 게 데이터에서에 대 한 정보를 얻기 있습니다.

## <a name="prerequisites"></a>필수 조건

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="spark-streaming-concepts"></a>Spark 스트리밍 개념

Spark 스트리밍에 대한 자세한 내용은 [Apache Spark 스트리밍 개요](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview)를 참조하세요. HDInsight hello Azure에서 동일한 스트리밍 기능 tooa Spark 클러스터를 제공 합니다.  

## <a name="what-does-this-solution-do"></a>이 솔루션의 기능은 무엇입니까?

Toocreate Spark 스트리밍 예제에서는이 문서의 단계를 수행 하는 hello를 수행 합니다.

1. 이벤트 스트림을 받을 Azure 이벤트 허브를 만듭니다.

2. 로컬 독립 실행형 응용 프로그램을 실행 하는 이벤트를 생성 하며 toohello Azure 이벤트 허브를 푸시합니다. 이 작업을 수행 하는 hello 샘플 응용 프로그램에서 게시 [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)합니다.

3. Azure Event Hub에서 스트리밍 이벤트를 읽는 Spark 클러스터에서 원격으로 스트리밍 응용 프로그램을 실행하고 다양한 데이터 처리/분석을 수행합니다.

## <a name="create-an-azure-event-hub"></a>Azure 이벤트 허브 만들기

1. Toohello 로그온 [Azure 포털](https://ms.portal.azure.com), 클릭 하 고 **새로** hello에 왼쪽 상단 hello 화면에 있습니다.

2. **사물 인터넷**을 클릭한 다음 **Event Hubs**를 클릭합니다.

    ![Spark 스트리밍 예제에 대한 이벤트 허브 만들기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Spark 스트리밍 예제에 대한 이벤트 허브 만들기")

3. Hello에 **네임 스페이스 만들기** 블레이드에서 네임 스페이스 이름을 입력 합니다. hello 가격 책정 계층 (기본 또는 표준)를 선택 합니다. 또한 toocreate hello 리소스에는 Azure 구독, 리소스 그룹 및 위치를 선택 합니다. 클릭 **만들기** toocreate hello 네임 스페이스입니다.

      ![Spark 스트리밍 예제에 대한 이벤트 허브 이름 제공](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Spark 스트리밍 예제에 대한 이벤트 허브 이름 제공")

    > [!NOTE]
    > 하면 해야 선택 hello 동일 **위치** HDInsight tooreduce 대기 시간 및 비용 Apache Spark 클러스터로 합니다.
    >
    >

4. Hello 이벤트 허브 네임 스페이스 목록에서 hello 새로 만든 네임 스페이스를 클릭 합니다.      


5. Hello 네임 스페이스 블레이드에서 클릭 **이벤트 허브**, 클릭 하 고 **+ 이벤트 허브** toocreate 새 이벤트 허브를 합니다.
   
    ![Spark 스트리밍 예제에 대한 이벤트 허브 만들기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Spark 스트리밍 예제에 대한 이벤트 허브 만들기")

6. 이벤트 허브, 집합 hello 파티션 수 too10 및 메시지 보존 too1에 대 한 이름을 입력 합니다. म 하지를 보관 하는이 솔루션에서는 hello 메시지 hello rest 기본적으로 유지 하 고 클릭 수 있도록 **만들기**합니다.
   
    ![Spark 스트리밍 예제에 대한 이벤트 허브 세부 정보 제공](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Spark 스트리밍 예제에 대한 이벤트 허브 세부 정보 제공")

7. 이벤트 허브를 새로 만든 hello hello 이벤트 허브 블레이드에 나열 됩니다.
    
     ![이벤트 허브 hello Spark 스트리밍 예제에 대 한 보기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "hello에 대 한 보기 이벤트 허브는 스트리밍 예제 멤버")

8. Hello 네임 스페이스 블레이드에서 (하지 hello 특정 이벤트 허브 블레이드)에서 다시 클릭 **공유 액세스 정책을**, 클릭 하 고 **RootManageSharedAccessKey**합니다.
    
     ![Hello Spark 스트리밍 예제에 대 한 이벤트 허브 정책 설정](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "hello에 대 한 이벤트 허브 설정 정책을 멤버 스트리밍 예제")

9. Hello 복사 단추 toocopy hello 클릭 **RootManageSharedAccessKey** 기본 키와 연결 문자열 toohello 클립보드 합니다. Hello 자습서의 뒷부분에 나오는 이러한 toouse를 저장 합니다.
    
     ![이벤트 허브 정책 키 hello Spark 스트리밍 예제를 보려면](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "hello에 대 한 보기 이벤트 허브 정책 키 멤버 스트리밍 예제")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>보낼 메시지 tooAzure 샘플 Scala 응용 프로그램을 사용 하 여 이벤트 허브

이 섹션에서는 독립 실행형 로컬 Scala 하는 응용 프로그램 이벤트 스트림을 생성 하 고 앞에서 만든 이벤트 허브 tooAzure 보냅니다 사용할 수 있습니다. 이 응용 프로그램은 [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer)의 GitHub에서 사용할 수 있습니다. hello 단계 여기이 GitHub 리포지토리를 분기 이미 있는 것을 전제로 합니다.

1. Hello 다음이이 응용 프로그램을 실행 하는 hello 컴퓨터에 설치 되어 있는지 확인 합니다.

    * Oracle Java Development 키트. [여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.
    * Apache Maven [여기](https://maven.apache.org/download.cgi)에서 다운로드할 수 있습니다. 사용할 수 있는 지침 tooinstall Maven [여기](https://maven.apache.org/install.html)합니다.

2. 명령 프롬프트를 열고 고 hello 샘플 Scala 응용 프로그램에 대 한 hello GitHub 리포지토리를 복제 toohello 위치 이동한 hello 다음 명령 toobuild hello 응용 프로그램을 실행 합니다.

        mvn package

3. hello 응용 프로그램에 대 한 hello 출력 jar **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, 아래에 생성 됩니다 **/대상** 디렉터리입니다. 이 문서 tootest hello 완벽 한 솔루션의 뒷부분에 나오는이 jar 파일을 사용할 수 있습니다.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Spark 클러스터에 이벤트 허브에서 응용 프로그램 tooreceive 메시지 만들기 

두 방법 tooconnect Spark 스트리밍 및 Azure 이벤트 허브, 수신기 기반 연결 및 DStream 기반 시작 직접 연결 했습니다. Direct-DStream 기반 hello 2.0.3 릴리스에서 2017 년 1 월에 도입 되었습니다. 형식의 성능이 더 우수 그대로 tooreplace hello 원래 수신기 기반 연결 예상한 하 고 리소스를 효율적으로 합니다. 자세한 내용은 [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs)에서 확인하세요. Direct DStream은 Spark 2.0+만을 지원합니다.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Hello 종속성 toospark eventhubs 커넥터와 함께 응용 프로그램을 구축

또한 GitHub에서 Spark EventHubs의 버전을 준비 하는 hello를 발표 합니다. toouse hello 준비 버전인 Spark EventHubs의 hello 첫 번째 단계는 hello 항목 toopom.xml 다음을 추가 하 여 소스 리포지토리 hello으로 GitHub tooindicate:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

종속성 tooyour 프로젝트 tootake hello 시험판된 버전에 따라 hello를 추가할 수 있습니다.

Maven 종속성

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

SBT 종속성

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Direct DStream 연결

[http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar)에서 Direct DStream을 사용하는 예제를 포함하는 미리 작성된 jar 파일을 다운로드할 수 있습니다.

소스 코드에서 사용할 수 있는 세 가지 예제를 포함 하는 hello jar 파일 [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream)합니다.

[WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala)를 예로 듭니다.

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

위 예제를 hello에 `eventhubParameters` 는 hello 매개 변수가 특정 tooa 단일 EventHubs 인스턴스에 있는 경우 toopass 것 toohello `createDirectStreams` 직접 DStream 개체 매핑 tooa 이벤트 허브 네임 스페이스를 생성 하는 API입니다. Hello 직접 DStream 개체에 대해 Spark 스트리밍 API 프레임 워크에서 제공 하는 모든 DStream API를 호출할 수 있습니다. 이 예제에서는 hello 마지막 3 마이크로 일괄 처리 간격 내에서 각 단어의 hello 주파수를 계산합니다.

### <a name="receiver-based-connection"></a>수신기 기반 연결

제공 된 이벤트 및 경로 hello toodifferent 대상 받는 Scala로 작성 된 예제 응용 프로그램 스트리밍 Spark 됩니다 [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)합니다. 이벤트 허브 구성에 대 한 tooupdate hello 응용 프로그램 아래 hello 단계를 수행 하 고 hello 출력 jar를 만듭니다.

1. IntelliJ 아이디어를 시작 하 고 시작 화면 선택 hello에서 **버전 제어에서 체크 아웃** 클릭 하 고 **Git**합니다.
   
    ![Apache Spark 스트리밍 예제 - Git에서 원본 가져오기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark 스트리밍 예제 - Git에서 원본 가져오기")

2. Hello에 **복제 저장소** 대화 상자에서 hello URL toohello Git 리포지토리 tooclone 제공, 디렉터리 tooclone hello를 지정 하 고 클릭 **복제**합니다.
   
    ![Apache Spark 스트리밍 예제 - Git에서 복제](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark 스트리밍 예제 - Git에서 복제")
3. Hello 프로젝트를 완전히 복제할 때까지 hello 지시를 따릅니다. 키를 눌러 **Alt + 1** tooopen hello **프로젝트 보기**합니다. Hello 다음과 비슷해야 합니다.
   
    ![Apache Spark 스트리밍 예제 - 프로젝트 보기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark 스트리밍 예제 - 프로젝트 보기")
4. Hello 응용 프로그램 코드는 Java8으로 컴파일된 있는지 확인 합니다. tooensure이를 클릭 하이 여 **파일**, 클릭 **프로젝트 구조**, 및 hello에 **프로젝트** 탭에서 프로젝트 언어 수준 너무 설정 되어 있는지 확인**8-람다 형식 주석, 등**합니다.
   
    ![Apache Spark 스트리밍 예제 - 컴파일러 설정](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark 스트리밍 예제 - 컴파일러 설정")
5. 열기 hello **pom.xml** hello Spark 버전이 올바른지 확인 합니다. `<properties>` 노드를 다음 코드 조각 hello를 검색 하 고 hello Spark 버전을 확인 합니다.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. hello 응용 프로그램에 필요한 호출 하는 종속성 jar **JDBC 드라이버 jar**합니다. Azure SQL 데이터베이스에 이벤트 허브에서 수신 하는 필수 toowrite hello 메시지 수입니다. 이 jar(v4.1 이상)을 [여기](https://msdn.microsoft.com/sqlserver/aa937724.aspx)에서 다운로드할 수 있습니다. 참조 toothis jar hello 프로젝트 라이브러리에 추가 합니다. Hello 다음 단계를 수행 합니다.
     
     1. Hello 응용 프로그램을 열고 있는 IntelliJ 아이디어 창에서 클릭 **파일**, 클릭 **프로젝트 구조**, 클릭 하 고 **라이브러리**합니다. 
     2. Hello 클릭 추가 아이콘 (![추가 아이콘](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png))를 클릭 하 여 **Java**, hello JDBC 드라이버 jar 다운로드 toohello 위치를 이동 합니다. Hello 프롬프트 tooadd hello jar 파일 toohello 프로젝트 라이브러리에 따라 합니다.

         ![누락된 종속성 추가](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "누락된 종속성 jar 추가")
     3. **Apply**를 클릭합니다.

7. Hello 출력 jar 파일을 만듭니다. Hello 다음 단계를 수행 합니다.

   1. Hello에 **프로젝트 구조** 대화 상자에서 클릭 **아티팩트** 다음 hello 및 기호를 클릭 합니다. Hello 팝업 대화 상자에서 클릭 **JAR**, 클릭 하 고 **종속성이 있는 모듈에서**합니다.      
       
       ![Apache Spark 스트리밍 예제 - JAR 만들기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark 스트리밍 예제 - JAR 만들기")
   2. Hello에 **모듈에서 JAR 만들** 대화 상자에서 hello 줄임표를 클릭 (![줄임표](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) hello에 대 한 **Main 클래스**합니다.
   3. Hello에 **Main 클래스 선택** 대화 상자, hello 사용 가능한 클래스 중 하나를 선택 하 고, 클릭 **확인**합니다.
      
       ![Apache Spark 스트리밍 예제 - jar에 대한 클래스 선택](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark 스트리밍 예제 - jar에 대한 클래스 선택")
   4. Hello에 **모듈에서 JAR 만들** 대화 상자, 반드시 해당 hello 옵션 너무**toohello 대상 JAR 추출** 을 선택한 다음 클릭 **확인**합니다. 이렇게 하면 모든 종속성이 있는 단일 JAR이 만들어집니다.
      
       ![Apache Spark 스트리밍 예제 - 모듈에서 jar 만들기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark 스트리밍 예제 - 모듈에서 jar 만들기")
   5. hello **출력 레이아웃** 탭 hello Maven 프로젝트의 일부분으로 포함 된 모든 hello jar를 나열 합니다. 선택할 수 있으며 더는 hello Scala 응용 프로그램 삭제 hello 의존 하지 않고 직접입니다. 제거할 수는 여기 만들기는 hello 응용 프로그램에 대 한 마지막을 제외 하 고 모두 hello (**spark-스트리밍-데이터-지 속성-예제 출력 컴파일**). Hello jar toodelete를 선택 하 고 hello를 클릭 한 다음 **삭제** 아이콘 (![삭제 아이콘](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Apache Spark 스트리밍 예제 - 추출된 jar 삭제](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark 스트리밍 예제 - 추출된 jar 삭제")
      
       있는지 확인 **확인을 토대로** 내용이 해당 hello jar hello 프로젝트를 작성 하거나 업데이트할 때마다 생성 되는 확인란을 선택 합니다. **Apply**를 클릭합니다.
   6. Hello에 **출력 레이아웃** hello hello 맨 오른쪽에 탭 **사용 가능한 요소** 이전 toohello 프로젝트 라이브러리를 추가한 hello SQL JDBC jar 있는 상자입니다. 이 toohello 추가 해야 **출력 레이아웃** 탭 합니다. Hello jar 파일을 마우스 오른쪽 단추로 누른 **출력 루트를 추출**합니다.
      
       ![Apache Spark 스트리밍 예제 - 종속성 jar 추출](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark 스트리밍 예제 - 종속성 jar 추출")  
      
       hello **출력 레이아웃** 탭에 이제 다음과 같아야 합니다.
      
       ![Apache Spark 스트리밍 예제 - 최종 출력 탭](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark 스트리밍 예제 - 최종 출력 탭")        
      
       Hello에 **프로젝트 구조** 대화 상자를 클릭 **적용** 클릭 하 고 **확인**합니다.    
   7. Hello 메뉴 모음에서 **빌드**, 클릭 하 고 **프로젝트 만들기**합니다. 클릭할 수도 있습니다 **빌드 아티팩트** toocreate hello jar. hello 출력 jar 아래에 생성 됩니다 **\classes\artifacts**합니다.
      
       ![Apache Spark 스트리밍 예제 - 출력 JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark 스트리밍 예제 - 출력 JAR")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>리비를 사용 하 여 Spark 클러스터에서 hello 응용 프로그램을 원격으로 실행

이 문서의 사용 하 여 리비 toorun hello Apache Spark 스트리밍 응용 프로그램 원격으로 Spark 클러스터에서. 어떻게 toouse 리비 HDInsight spark 클러스터에 대 한 자세한 내용은 참조 하십시오. [전송 작업 원격으로 tooan Apache Spark 클러스터에 Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md)합니다. Hello Spark 스트리밍 응용 프로그램 실행을 시작 하기 전에 수행 해야 할 작업의 두 가지가 있습니다.

1. 로컬 독립 실행형 응용 프로그램 toogenerate 이벤트 hello 시작한 tooEvent 허브 전송 합니다. Hello 명령 toodo 되므로 다음을 사용 합니다.

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. 복사 hello jar 스트리밍 (**spark-스트리밍-데이터-지 속성-examples.jar**) toohello hello 클러스터와 연결 된 Azure Blob 저장소입니다. 따라서 hello jar 액세스할 수 있는 tooLivy 있습니다. 사용할 수 있습니다 [ **AzCopy**](../storage/common/storage-use-azcopy.md), 명령줄 유틸리티, toodo 되므로 명령입니다. 있 다른 클라이언트의 tooupload 데이터를 사용할 수 있습니다. [HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.
3. 이러한 응용 프로그램을 실행 되 고 있는 hello 컴퓨터에 CURL을 설치 합니다. CURL tooinvoke hello 리비 끝점 toorun hello 작업이 원격으로 사용 합니다.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>텍스트도 Azure 저장소 Blob에 hello Spark 스트리밍 응용 프로그램 tooreceive hello 이벤트 실행

명령 프롬프트를 열고 CURL을 설치한 toohello 디렉터리 탐색 hello 다음 명령을 (바꾸기 사용자 이름/암호 및 클러스터 이름)를 실행 합니다.

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello 파일의 매개 변수를 hello **inputBlob.txt** ´ ï ´ ù.

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Hello 매개 변수 hello 입력된 파일에 이란 이해 알려 주세요.

* **파일** hello 클러스터와 연결 된 hello Azure 저장소 계정에 hello 경로 toohello 응용 프로그램 jar 파일이 있습니다.
* **className** hello hello jar의 hello 클래스 이름입니다.
* **args** hello hello 클래스에 필요한 인수 목록
* **numExecutors** hello Spark toorun hello 스트리밍 응용 프로그램에서 사용 하는 코어 수입니다. 이 두 번 이상 hello 이벤트 허브 파티션 수가 항상 있어야 합니다.
* **executorMemory**, **executorCores**, **driverMemory** 리소스가 사용 매개 변수에 필요한 tooassign toohello 스트리밍 응용 프로그램입니다.

> [!NOTE]
> Toocreate hello 출력 폴더 (EventCheckpoint, EventCount/EventCount10) 매개 변수로 사용 되는 필요가 없습니다. 응용 프로그램 스트리밍을 hello가 만들어 합니다.
>
>

Hello 명령을 실행 하면 hello 다음과 같은 출력이 표시 되어야 합니다.

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

이 예에서는 '1' hello 출력의 마지막 줄 hello에에서 hello 일괄 처리 ID 기록해 둡니다. 응용 프로그램 hello tooverify 성공적으로 실행, hello 클러스터와 연결 된 Azure 저장소 계정을 볼 수 있습니다 및 hello 표시 되어야 **/EventCount/EventCount10** 만든 폴더입니다. 이 폴더는 hello 수가 hello 매개 변수에 대해 지정 된 시간 동안 hello 내에서 처리 된 이벤트를 캡처하는 blob을 포함 해야 **초에서 일괄 처리 간격**합니다.

hello Spark 스트리밍 응용 프로그램을 중지 하기까지 toorun을 계속 됩니다. 따라서 toodo 다음 명령을 hello를 사용 합니다.

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Hello 응용 프로그램을 실행 tooreceive hello 이벤트는 Azure 저장소 Blob에 JSON으로
명령 프롬프트를 열고 CURL을 설치한 toohello 디렉터리 탐색 hello 다음 명령을 (바꾸기 사용자 이름/암호 및 클러스터 이름)를 실행 합니다.

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello 파일의 매개 변수를 hello **inputJSON.txt** ´ ï ´ ù.

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

hello 매개 변수는 유사한 toowhat hello 이전 단계에서 hello 텍스트 출력에 지정 합니다. 다시, toocreate hello 출력 폴더 (EventCheckpoint, EventCount/EventCount10) 매개 변수로 사용 되는 필요 하지 않습니다. 응용 프로그램 스트리밍을 hello가 만들어 합니다.

 실행 한 후 hello 명령, hello 클러스터와 연결 된 Azure 저장소 계정을 살펴보면 hello 표시 되어야 **/EventStore10** 만든 폴더입니다. 열려 있는 파일을 접두사로 **파트-** JSON 형식으로 처리 된 hello 이벤트 표시 되어야 합니다.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Hive 테이블에 hello 응용 프로그램 tooreceive hello 이벤트를 실행 합니다.
toorun hello 스트림을 이벤트를 하이브 테이블 있습니다 Spark 스트리밍 응용 프로그램에는 몇 가지 추가 구성 요소 필요 합니다. 다음과 같습니다.

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

hello **.jar** 파일에 HDInsight Spark 클러스터에서 사용할 수 있는 `/usr/hdp/current/spark-client/lib`합니다. hello **hive-site.xml** 에 `/usr/hdp/current/spark-client/conf`합니다.

사용할 수 있습니다 [WinScp](http://winscp.net/eng/download.php) toocopy hello 클러스터 tooyour 로컬 컴퓨터에서 해당 파일입니다. 다음 도구 toocopy hello 클러스터와 연결 된 tooyour 저장소 계정을 통해 이러한 파일을 사용할 수 있습니다. Tooupload toohello 저장소 계정 파일 하는 방법에 대 한 자세한 내용은 참조 하십시오. [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드](hdinsight-upload-data.md)합니다.

Hello 파일 tooyour Azure 저장소 계정을 통해으로 복사한 후에 명령 프롬프트를 열고 CURL을 설치한 toohello 디렉터리 이동한 hello 다음 (바꾸기 사용자 이름/암호 및 클러스터 이름) 명령을 실행 합니다.

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello 파일의 매개 변수를 hello **inputHive.txt** ´ ï ´ ù.

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

hello 매개 변수는 유사한 toowhat hello 이전 단계에서 hello 텍스트 출력에 지정 합니다. 다시, 않아도 toocreate hello 출력 폴더 (EventCheckpoint, EventCount/EventCount10) 또는 hello 출력 매개 변수로 사용 되는 하이브 테이블 (EventHiveTable10). 응용 프로그램 스트리밍을 hello가 만들어 합니다. 해당 hello 참고 **jar** 및 **파일** toohello.jar 파일 경로 및 hello hive-site.xml toohello 저장소 계정을 통해 복사 하는 옵션에 포함 됩니다.

hive 테이블 hello tooverify 성공적으로 만들었습니다., SSH hello 클러스터 및 실행된 된 Hive 쿼리를 수행할 수 있습니다. 자세한 내용은 [SSH를 사용하는 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-ssh.md)을 참조하세요. SSH를 사용 하 여 연결 된 후 실행할 수 있습니다 다음 명령 tooverify hello hello Hive 테이블에 **EventHiveTable10**, 만들어집니다.

    show tables;

출력 유사한 toohello 다음을 나타나야 합니다.

    OK
    eventhivetable10
    hivesampletable

또한 hello 테이블의 tooview hello 내용을 선택 쿼리를 실행할 수 있습니다.

    SELECT * FROM eventhivetable10 LIMIT 10;

Hello 다음과 같은 출력을 표시 되어야 합니다.

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Azure SQL 데이터베이스 테이블에 hello 응용 프로그램 tooreceive hello 이벤트를 실행 합니다.
이 단계를 실행하기 전에 Azure SQL 데이터베이스를 만들었는지 확인합니다. 자세한 내용은 [몇 분 만에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)를 참조하세요. 이 섹션 toocomplete, 데이터베이스 이름, 데이터베이스 서버 이름 및 매개 변수로 hello 데이터베이스 관리자 자격 증명에 대 한 값이 있어야 합니다. 않아도 toocreate hello 데이터베이스 테이블 이지만 합니다. hello Spark 스트리밍 응용 프로그램을를 만듭니다.

명령 프롬프트를 열고, CURL을 설치한 toohello 디렉터리 이동한 hello 다음 명령을 실행 합니다.

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello 파일의 매개 변수를 hello **inputSQL.txt** ´ ï ´ ù.

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

응용 프로그램 hello tooverify 성공적으로 실행, SQL Server Management Studio를 사용 하 여 toohello Azure SQL 데이터베이스를 연결할 수 있습니다. 방법에 대 한 참조는 toodo [tooSQL 데이터베이스 SQL Server Management Studio를 사용 하 여 연결](../sql-database/sql-database-connect-query-ssms.md)합니다. 연결 된 toohello 데이터베이스 했으면 toohello 탐색할 수 있습니다 **EventContent** hello 스트리밍 응용 프로그램에 의해 만들어진 테이블입니다. 빠른 쿼리 tooget hello 데이터 hello 테이블에서 실행할 수 있습니다. Hello 다음 쿼리를 실행 합니다.

    SELECT * FROM EventCount

유사한 toohello 다음 출력이 표시 되어야 합니다.

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)
* [수신기 기반 연결 및 Direct DStream 설계](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
