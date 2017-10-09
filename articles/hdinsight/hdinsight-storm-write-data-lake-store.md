---
title: "aaaApache 스톰 쓰기 tooStorage/데이터 레이크 저장소-Azure HDInsight | Microsoft Docs"
description: "HDInsight에 대 한 toouse Apache Storm toowrite toohello HDFS 호환 저장소 hello 하는 방법에 대해 알아봅니다. Azure 저장소 또는 Azure 데이터 레이크 저장소 HDInsight에 대 한 hello HDFS comptabile 저장소를 제공 합니다. 이 문서 및 hello 관련된 예제 hello HdfsBolt 구성 요소 사용된 toowrite toohello 기본 저장소의 HDInsight 클러스터에서 Storm 수 있는 방법을 보여 줍니다."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>HDInsight의 Apache Storm에서 tooHDFS 작성

HDInsight의 Apache Storm 프로그램 toouse 스톰 toowrite 데이터 toohello HDFS 호환 저장소의 사용 방법에 대해 알아봅니다. HDInsight는 Azure Storage 및 Azure Data Lake Store를 모두 HDFS 호환 저장소로 사용할 수 있습니다. Storm 제공는 [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) 데이터 tooHDFS를 작성 하는 구성 요소입니다. 이 문서에서는 저장소 tooeither 유형의 hello HdfsBolt에서에서 작성 설명 합니다. 

> [!IMPORTANT]
> 이 문서에 사용 된 토폴로지 hello 예제 HDInsight의 Storm에 포함 된 구성 요소를 사용 합니다. Azure 데이터 레이크 저장소 다른 Apache Storm 클러스터와 함께 사용할 때와 수정 toowork가 필요할 수 있습니다.

## <a name="get-hello-code"></a>Hello 코드 가져오기

이 토폴로지를 포함 하는 hello 프로젝트에서 다운로드할 수는 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store)합니다.

toocompile이이 프로젝트를 hello 같은 개발 환경에 대 한 구성이 필요 합니다.

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상 - HDInsight 3.5 이상에는 Java 8이 필요합니다.

* [Maven 3.x](https://maven.apache.org/download.cgi)

hello 다음과 같은 환경 변수 설정 되어 있습니다 Java와 hello JDK 개발용 워크스테이션에 설치 하는 경우. 그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.

* `JAVA_HOME`-toohello hello JDK가 설치 디렉터리를 가리켜야 합니다.
* `PATH`-경로 따라 hello를 포함 해야 합니다.
  
    * `JAVA_HOME`(또는 hello 해당 하는 경로)입니다.
    * `JAVA_HOME\bin`(또는 hello 해당 하는 경로)입니다.
    * Maven 설치 되어 있는 hello 디렉터리입니다.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Toouse는 HDInsight와 HdfsBolt hello 하는 방법

> [!IMPORTANT]
> Hello HdfsBolt HDInsight의 Storm를 사용 하기 전에 먼저 사용 해야 스크립트 동작 필요한 toocopy jar 파일 hello에 `extpath` Storm의 합니다. 자세한 내용은 참조 hello [구성 hello 클러스터](#configure) 섹션.

toounderstand을 어떻게 제공 하는 hello 파일 체계를 사용 하는 hello HdfsBolt toowrite tooHDFS 합니다. HDInsight를와 hello 구성표를 다음 중 하나를 사용 합니다.

* `wasb://`: Azure Storage 계정과 함께 사용
* `adl://`: Azure Data Lake Store와 함께 사용

hello 다음 표에서 hello 파일 체계를 사용 하 여 다양 한 시나리오에 대 한 예:

| 구성표 | 참고 사항 |
| ----- | ----- |
| `wasb:///` | hello 기본 저장소 계정 blob 컨테이너는 Azure 저장소 계정에는 |
| `adl:///` | hello 기본 저장소 계정에는 Azure 데이터 레이크 저장소의 디렉터리입니다. 클러스터를 만드는 동안 hello 루트 hello 클러스터의 HDFS에 있는 데이터 레이크 저장소의 hello 디렉터리를 지정 합니다. 예를 들어 hello `/clusters/myclustername/` 디렉터리입니다. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Hello 클러스터와 연결 된 기본이 아닌 (추가) Azure 저장소 계정입니다. |
| `adl://STORENAME/` | hello hello 클러스터에서 사용 하는 데이터 레이크 저장소의 hello 루트입니다. 이 체계 hello 클러스터 파일 시스템을 포함 하는 hello 디렉터리 외부에 있는 tooaccess 데이터가 있습니다. |

자세한 내용은 참조 hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) Apache.org에서 참조 합니다.

### <a name="example-configuration"></a>예제 구성

hello 다음 YAML는 hello 발췌 `resources/writetohdfs.yaml` hello 예제에 포함 된 파일입니다. 이 파일은 hello를 사용 하 여 hello 스톰 토폴로지 정의 [표적이](https://storm.apache.org/releases/1.1.0/flux.html) Apache Storm의 프레임 워크입니다.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

이 YAML hello 다음 항목을 정의 합니다.

* `syncPolicy`: 경우 파일은 동기화/플러시 toohello 파일 시스템을 정의 합니다. 이 예제에서는 1,000개 튜플마다 동기화/플러시되도록 정의했습니다.
* `fileNameFormat`: 파일을 작성할 때 hello 경로 파일 이름 패턴 toouse를 정의 합니다. 이 예제에서는 hello 경로 필터를 사용 하 여 런타임에 제공 되 고 hello 파일 확장명은 `.txt`합니다.
* `recordFormat`: Hello 기록 된 hello 파일의 내부 형식을 정의 합니다. 이 예제에서는 필드 hello로 구분 된 `|` 문자입니다.
* `rotationPolicy`: 시기를 정의 toorotate 파일입니다. 이 예제에서는 회전이 수행되지 않습니다.
* `hdfs-bolt`: 사용 하 여 hello에 대 한 구성 매개 변수로 이전 구성 요소를 hello `HdfsBolt` 클래스입니다.

Hello 표적이 프레임 워크에 대 한 자세한 내용은 참조 하십시오. [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)합니다.

## <a name="configure-hello-cluster"></a>Hello 클러스터 구성

기본적으로 HDInsight의 Storm HdfsBolt 사용 된 Azure 저장소 서비스 또는 데이터 레이크 저장소 toocommunicate Storm의 클래스 경로에서 하는 hello 구성 요소를 포함 되지 않습니다. 사용 하 여 hello 다음 스크립트 동작 tooadd 이러한 구성 요소 toohello `extlib` 디렉터리 Storm의 클러스터에:

| 스크립트 URI | 노드 tooapply 하도록 | 매개 변수 | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, 감독자 | None |

이 스크립트를 사용 하 여 클러스터 사용에 대 한 내용은 hello 참조 [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](./hdinsight-hadoop-customize-cluster-linux.md) 문서.

## <a name="build-and-package-hello-topology"></a>빌드 및 패키징합니다 hello 토폴로지

1. hello 예제 프로젝트를 다운로드 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour 개발 환경입니다.

2. 명령 프롬프트에서 터미널 또는 셸 세션 디렉터리 toohello 루트 변경 hello의 프로젝트를 다운로드 합니다. 토폴로지 hello toobuild 및 패키지 다음 명령을 hello를 사용 합니다.
   
        mvn compile package
   
    라는 새 디렉터리 없는 hello 빌드 및 패키징 완료 되 면 `target`, 라는 파일을 포함 하는 `StormToHdfs-1.0-SNAPSHOT.jar`합니다. 이 파일에 컴파일된 hello 토폴로지 포함 되어 있습니다.

## <a name="deploy-and-run-hello-topology"></a>배포 하 고 hello 토폴로지를 실행 합니다.

1. Hello 다음 명령 toocopy hello 토폴로지 toohello HDInsight 클러스터를 사용 합니다. 대체 **사용자** hello 클러스터를 만들 때 사용한 hello SSH 사용자 이름이 사용 됩니다. 대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    메시지가 표시 되 면 hello 클러스터에 대 한 hello SSH 사용자를 만들 때 사용 하는 hello 암호를 입력 합니다. 공개 키 대신 암호를 사용 하는 경우 toouse hello 할 수 있습니다 `-i` 개인 키와 일치 하는 매개 변수 toospecify hello 경로 toohello 합니다.
   
   > [!NOTE]
   > HDInsight에서의 `scp` 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](./hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. Hello 업로드가 완료 되 면 hello tooconnect toohello HDInsight 클러스터 SSH를 사용 하 여 다음을 사용 합니다. 대체 **사용자** hello 클러스터를 만들 때 사용한 hello SSH 사용자 이름이 사용 됩니다. 대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    메시지가 표시 되 면 hello 클러스터에 대 한 hello SSH 사용자를 만들 때 사용 하는 hello 암호를 입력 합니다. 공개 키 대신 암호를 사용 하는 경우 toouse hello 할 수 있습니다 `-i` 개인 키와 일치 하는 매개 변수 toospecify hello 경로 toohello 합니다.
   
   자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. 사용 하 여 hello 다음 명령은 이라는 파일로 내보내집니다 toocreate 연결 되 면 `dev.properties`:

        nano dev.properties

4. 콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `dev.properties` 파일:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > 이 예제에서는 클러스터에 Azure 저장소 계정을 사용 하 여 hello 기본 저장소로 가정 합니다. 클러스터에서 Azure Data Lake Store를 사용하는 경우 `hdfs.url: adl:///`을 대신 사용합니다.
    
    toosave hello 파일을 사용 하 여 __Ctrl + X__, 다음 __Y__, 마지막으로 __Enter__합니다. 이 파일에 hello 값 hello 데이터 레이크 저장소 URL 및 데이터에 기록 되는 hello 디렉터리 이름을 설정 합니다.

3. 다음 명령 toostart hello 토폴로지 hello를 사용 합니다.
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    이 명령은 hello 표적이 프레임 워크를 사용 하 여 hello 클러스터의 toohello Nimbus 노드에 전송 하 여 hello 토폴로지를 시작 합니다. hello hello 토폴로지를 정의 `writetohdfs.yaml` hello jar에 포함 된 파일입니다. hello `dev.properties` 파일 필터를 변수로 전달 되 고 hello 토폴로지 hello 파일에 포함 된 hello 값을 읽습니다.

## <a name="view-output-data"></a>출력 데이터 보기

다음 명령을 사용 하 여 hello tooview hello 데이터:

    hdfs dfs -ls /stormdata/

이 토폴로지에서 만든 hello 파일의 목록이 표시 됩니다.

hello 다음 목록은 hello 이전 명령에서 반환 하는 hello 데이터의 예입니다.

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Hello 토폴로지를 중지 합니다.

Storm 토폴로지 중지 될 때까지 실행 또는 hello 클러스터가 삭제 됩니다. 다음 명령을 사용 하 여 hello toostop hello 토폴로지:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>클러스터 삭제

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>다음 단계

Toouse 스톰 toowrite tooAzure 저장소 및 Azure 데이터 레이크 저장소 검색 방법을 다른 배웠습니다 했으므로 [HDInsight에 대 한 예제 스톰](hdinsight-storm-example-topology.md)합니다.

