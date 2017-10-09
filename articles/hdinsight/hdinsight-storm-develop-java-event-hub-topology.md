---
title: "Java를 사용 하 여 HDInsight의 Storm으로 이벤트 허브에서 aaaProcess 이벤트 | Microsoft Docs"
description: "Java 스톰 토폴로지를 사용 하 여 이벤트 허브 데이터 tooprocess Maven을 사용 하 여 만든 하는 방법에 대해 알아봅니다."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리(Java)

자세한 내용은 방법 toouse HDInsight의 Storm와 Azure 이벤트 허브입니다. 이 예제에서는 Azure 이벤트 허브의 Java 기반 구성 요소 데이터 tooread 및 쓰기를 사용합니다.

Azure 이벤트 허브는 대량의 웹 사이트, 앱 및 장치에서 데이터를 tooprocess 수 있습니다. hello 배출구 이벤트 허브를 사용 하면 쉽게 toouse Apache Storm HDInsight tooanalyze에이 데이터를 실시간으로 합니다. 이벤트 허브 볼트 hello를 사용 하 여 스톰에서 tooEvent 데이터 허브를 작성할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

* HDInsight 클러스터 버전 3.6의 Apache Storm 자세한 내용은 [HDInsight 클러스터에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.

    > [!IMPORTANT]
    > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* [Azure 이벤트 허브](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [OpenJDK](http://openjdk.java.net/)와 같은 [Oracle JDK(Java 개발자 키트) 버전 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 또는 그와 동등

* [Maven](https://maven.apache.org/download.cgi): Maven은 Java 프로젝트용 프로젝트 빌드 시스템입니다.

* 텍스트 편집기 또는 통합 개발 환경(IDE)입니다.

    > [!NOTE]
    > 편집기 또는 IDE에 이 문서에서 다루지 않은 Maven과 함께 동작하는 특정 기능이 있을 수 있습니다. 편집 환경의 hello 기능에 대 한 정보를 사용 하는 hello 제품에 대 한 hello 설명서를 참조 합니다.

    * SSH 클라이언트. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

* hello `ssh` 및 `scp` 명령입니다. 이들은 사용된 toocopy 파일 toohello HDInsight 클러스터입니다. Windows의 경우 Windows 10의 Bash를 통해 이러한 명령을 사용할 수 있습니다.

## <a name="understanding-hello-example"></a>이해 hello 예제

hello [java 스톰 eventhub hdinsight](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) 예제에는 두 가지 토폴로지:

hello `resources/writer.yaml` 토폴로지 임의의 데이터 tooan Azure 이벤트 허브를 씁니다. hello hello 데이터를 생성 `DeviceSpout` 구성 요소는 임의 장치 ID와 장치 값 이며 합니다. 따라서 문자열 ID 및 숫자 값을 내보내는 하드웨어 일부를 시뮬레이션 중입니다.

3 개 `resources/reader.yaml` 토폴로지 hello JSON 데이터를 구문 분석 하 고 hello를 로그 하는 이벤트 허브 (EventHubWriter를 통해 작성 된 hello 데이터)에서 데이터를 읽고 `deviceId` 및 `deviceValue` 데이터입니다.

hello 데이터 형식이 JSON द tooEvent 허브에 기록 되 고 hello 판독기가 읽을 때 전에 구문 분석 되어야 JSON를 튜플 합니다. hello JSON 형식은 다음과 같습니다.

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>프로젝트 구성

hello `POM.xml` 파일이 Maven 프로젝트에 대 한 구성 정보를 포함 합니다. hello 흥미로운 부분에는

#### <a name="event-hub-components"></a>Event Hub 구성 요소

hello 구성 요소를 읽고 쓰는 tooAzure 이벤트 허브 hello에 위치한 [HDInsight 리포지토리](https://github.com/hdinsight/mvn-rep)합니다. hello의 섹션에서는 다음 hello `POM.xml` 이 리포지토리의 파일 부하 hello 구성 요소

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>hello EventHubs 스톰 Spout 종속성

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

이 xml 이벤트 허브에서 읽기 위해 배출구 tooit 작성 하기 위한 볼트 모두 들어 있는 hello eventhubs 패키지에 대 한 종속성을 정의 합니다.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

이 xml 이상 HDInsight 3.5에서 사용 되는 Java 8에 대 한 hello 프로젝트 toogenerate 출력을 구성 합니다.

#### <a name="hello-maven-shade-plugin"></a>hello maven-음영-플러그 인

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
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

이 xml uber jar에 hello 솔루션 toopackage hello 출력을 구성합니다. hello jar hello 프로젝트 코드와 필요한 종속성을 모두 포함 되어 있습니다. 다음에 사용됩니다.

* Hello 종속성에 대 한 라이선스 파일을 이름을 바꿉니다.
* 보안/서명을 제외합니다.
* 여러 번 구현 hello 동일 있는지 확인 한 항목으로 병합 하는 인터페이스입니다.

이러한 구성 설정은 런타임 시 오류를 방지합니다.

#### <a name="topology-definitions"></a>토폴로지 정의

이 예에서는 hello [표적이](https://storm.apache.org/releases/1.1.0/flux.html) 프레임 워크입니다. 이 프레임 워크 YAML toodefine hello 토폴로지를 사용합니다. hello 기본 이점은 하드 코딩 hello 토폴로지 Java 코드를 주는 점입니다. Hello 정의 YAML 이기 때문에 모든 toorecompile 필요 없이 hello 토폴로지를 전송 하기 전에 변경할 수 있습니다.

__writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>이벤트 허브에 대해 어떤 hello 토폴로지

런타임 시 hello `dev.properties` 파일은 사용 되는 toopass hello 이벤트 허브 구성 toohello 토폴로지입니다. hello 다음 예제는 hello 파일의 기본 내용 hello:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>환경 변수 구성

hello 다음과 같은 환경 변수 설정 되어 있습니다 Java와 hello JDK 개발용 워크스테이션에 설치 하는 경우. 그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.

* **JAVA_HOME** -toohello hello Java runtime environment (JRE)가 설치 디렉터리를 가리켜야 합니다. 예를 들어, Unix 또는 Linux 배포 없어야과 유사한 값 너무`/usr/lib/jvm/java-7-oracle`합니다. Windows에서 동일 하 게과 유사한 값 너무`c:\Program Files (x86)\Java\jre1.7`
* **경로** -hello 다음 경로 포함 해야 합니다.

  * **JAVA_HOME** (또는 hello 해당 하는 경로)
  * **JAVA_HOME\bin** (또는 hello 해당 하는 경로)
  * Maven 설치 되어 있는 hello 디렉터리

## <a name="configure-event-hub"></a>이벤트 허브 구성

이벤트 허브는이 예제에 대 한 hello 데이터 원본. 다음 단계 toocreate 이벤트 허브를 hello를 사용 합니다.

1. Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **새로** > **서비스 버스** > **이벤트 허브**  >  **사용자 지정 만들기**합니다.

2. Hello에 **새 이벤트 허브 추가** 화면에서 입력 한 **이벤트 허브 이름**합니다. 선택 hello **지역** toocreate hello 허브에서는 다음 네임 스페이스를 만들거나 기존 템플릿을 선택 합니다. 마지막으로 hello 클릭 **화살표** toocontinue 합니다.

    ![마법사 페이지 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > 동일한 select hello **위치** HDInsight 서버 tooreduce 대기 시간 및 비용에 프로그램 스톰으로 합니다.

3. Hello에 **이벤트 허브 구성** 화면에서 입력 하는 hello **count 파티션** 및 **메시지 보존** 값입니다. 이 예에서는 파티션 개수로 10을, 메시지 보존으로는 1을 사용합니다. 이 값을 나중에 필요 하기 때문에 hello 파티션 수를 note 합니다.

    ![마법사 페이지 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Hello 이벤트 허브에 대 한 생성을 선택 하는 hello 네임 스페이스를 수행한 후에 선택 **이벤트 허브**, 한 다음 이전에 만든 hello 이벤트 허브를 선택 합니다.
5. 선택 **구성**, 다음 두 가지 새로운 액세스 정책을 hello 다음 정보를 사용 하 여 만듭니다.

    <table>
    <tr><th>이름</th><th>권한</th></tr>
    <tr><td>기록기</td><td>보내기</td></tr>
    <tr><td>읽기 권한자</td><td>수신 대기</td></tr>
    </table>

    Hello 사용 권한을 만든 후 선택 hello **저장** hello hello 페이지 맨 위에 있는 아이콘입니다. 이러한 공유 액세스 정책은 사용 되는 tooread 있으며 tooEvent 허브를 작성 합니다.

    ![정책](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Hello를 사용 하 여 hello 정책을 저장 한 후 **공유 액세스 키 생성기** hello에 대 한 hello 페이지 tooretrieve hello 키 hello 맨 아래에 **기록기** 및 **판독기** 정책입니다. 이러한 키를 저장합니다.

## <a name="download-and-build-hello-project"></a>다운로드 하 고 hello 프로젝트 빌드

1. GitHub에서 hello 프로젝트를 다운로드: [java 스톰 eventhub hdinsight](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)합니다. Zip 보관 파일로 hello 패키지를 다운로드 하거나 사용할 [git](https://git-scm.com/) 로컬로 tooclone hello 프로젝트.

2. Hello 수정 `dev.properties` 이벤트 허브에 대 한 hello 구성 파일입니다.

3. 다음 toobuild 및 패키지 hello 프로젝트 hello를 사용 합니다.

        mvn package

    이 명령은 빌드에 필요한 종속성을 다운로드 한 다음 패키지 hello 프로젝트 합니다. hello 출력이 hello에 저장 됩니다 **/대상** 으로 디렉터리 **EventHubExample-1.0-SNAPSHOT.jar**합니다.

## <a name="test-locally"></a>로컬에서 테스트

이러한 토폴로지가 바로 읽고 쓰는 tooEvent 허브, 이후 테스트할 수 있습니다 있는 경우에 로컬로 [스톰 개발 환경](http://storm.apache.org/releases/current/Setting-up-development-environment.html)합니다. Hello 개발 환경에서 로컬로 toorun 단계를 수행 하는 hello를 사용 합니다.

1. Hello 기록기를 실행 합니다.

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Hello 판독기를 실행 합니다.

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Hello 토폴로지 모드에서 실행 로컬 (비 배포).
> * `-R /writer.yaml`: Hello에서 hello 토폴로지 정의 로드 합니다. `resources` hello jar에 패키지 합니다. Hello 토폴로지는 hello 로컬 파일 시스템에 파일을 대신 hello 경로 tooit hello 마지막 매개 변수로 지정 합니다.
> * `--filter dev.properties`: 사용 하 여 hello 내용의 `dev.properties` toofill hello 토폴로지 정의에 hello 값입니다. 예: `${eventhub.read.policy.name}`.

출력은 로컬로 실행 하는 경우 로깅된 toohello 콘솔입니다. 사용 하 여 __Ctrl + C__ toostop hello 토폴로지입니다.

## <a name="deploy-hello-topologies"></a>Hello 토폴로지를 배포 합니다.

1. SCP toocopy hello jar 패키지 tooyour HDInsight 클러스터를 사용 합니다. 클러스터에 대 한 hello SSH 사용자와 사용자 이름을 대체 합니다. CLUSTERNAME를 HDInsight 클러스터의 hello 이름을 바꿉니다.

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    SSH 계정에 대 한 암호를 사용 하는 경우 메시지 표시 tooenter hello 암호입니다. SSH 키를 사용 하는 hello 계정과 toouse hello를 할 수 있습니다 `-i` 매개 변수 toospecify hello 경로 toohello 키 파일입니다. 예를 들어 `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    이 명령은 hello 파일 toohello hello 클러스터에 대 한 SSH 사용자의 홈 디렉터리에 복사합니다.

2. Hello 파일 업로드 완료 되 면 SSH tooconnect toohello HDInsight 클러스터를 사용 합니다. 대체 **USERNAME** hello 이름 SSH 로그인입니다. **CLUSTERNAME** 을 HDInsight 클러스터 이름으로 바꿉니다.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > SSH 계정에 대 한 암호를 사용 하는 경우 메시지 표시 tooenter hello 암호입니다. SSH 키를 사용 하는 hello 계정과 toouse hello를 할 수 있습니다 `-i` 매개 변수 toospecify hello 경로 toohello 키 파일입니다. hello 다음 예제에서는 로드에서 개인 키 hello `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. 다음 명령 toostart hello 토폴로지 hello를 사용 합니다.

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Hello 토폴로지 toohello hello 클러스터의 작업자 노드 hello에 시작 Nimbus 서비스에 전송 합니다.

4. tooview hello 기록 데이터를 이동 toohttps://CLUSTERNAME.azurehdinsight.net/stormui, 여기서 __CLUSTERNAME__ HDInsight 클러스터의 hello 이름입니다. Hello 토폴로지를 선택 하 고 드릴 다운 toohello 구성 요소. 선택 hello __포트__ 항목 구성 요소 tooview의 인스턴스에 대 한 정보를 기록 합니다.

5. 사용 하 여 hello 다음 명령 toostop hello 토폴로지:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>클러스터 삭제

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>다음 단계

* [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)
