---
title: "Python 불일치가-Azure HDInsight와 스톰 aaaApache | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Python 구성 요소를 사용 하는 Apache Storm 토폴로지입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>HDInsight에서 Python을 사용하여 Apache Storm 토폴로지 개발

자세한 내용은 방법 toocreate Python 구성 요소를 사용 하는 Apache Storm 토폴로지입니다. Apache Storm도 한 토폴로지의 여러 언어에서 구성 요소를 toocombine 허용 여러 언어를 지원 합니다. hello 표적이 프레임 워크 (스톰 0.10.0에서 도입)를 있습니다 tooeasily Python 구성 요소를 사용 하는 솔루션을 만듭니다.

> [!IMPORTANT]
> 이 문서에서 hello 정보 스톰 HDInsight 3.6에서 사용 하 여 테스트 되었습니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

이 프로젝트에 대 한 hello 코드에서 사용할 수는 [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount)합니다.

## <a name="prerequisites"></a>필수 조건

* Python 2.7 이상

* JDK Java 1.8 이상

* Maven 3

* (선택 사항) 로컬 Storm 개발 환경 - 로컬 스톰 환경 toorun hello 토폴로지 로컬로 하려는 경우에 필요 합니다. 자세한 내용은 [개발 환경 설정](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)(영문)을 참조하세요.

## <a name="storm-multi-language-support"></a>Storm 다중 언어 지원

Apache Storm 모든 프로그래밍 언어를 사용 하 여 작성 된 구성 요소 디자인 된 toowork 했습니다. hello 구성 요소를 이해 해야 어떻게 hello로 toowork [스톰에 대 한 Thrift 정의](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift)합니다. Python에 대 한 모듈 Storm tooeasily 인터페이스를 허용 하는 hello Apache Storm 프로젝트의 일부로 제공 됩니다. 이 모듈을 [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py)에서 찾을 수 있습니다.

Storm는 hello 가상 컴퓨터 JVM (Java)에서 실행 되는 Java 프로세스입니다. 다른 언어로 작성된 구성 요소는 하위 프로세스로 실행됩니다. hello 스톰 stdin/stdout 통해 전송 된 JSON 메시지를 사용 하 여 이러한 하위 프로세스와 통신 합니다. 구성 요소 간의 통신에 대 한 자세한 내용은 hello에서 확인할 수 있습니다 [다중 lang 프로토콜](https://storm.apache.org/documentation/Multilang-protocol.html) 설명서입니다.

## <a name="python-with-hello-flux-framework"></a>Python hello 표적이 프레임 워크 사용

hello 표적이 프레임 워크에서는 hello 구성 요소와는 별도로 toodefine 스톰 토폴로지가 있습니다. hello 표적이 framework YAML toodefine hello 스톰 토폴로지를 사용합니다. hello 다음 텍스트는 방법의 예로 tooreference hello YAML 문서에서 Python 구성 요소:

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

클래스를 hello `FluxShellSpout` 는 사용 되는 toostart hello `sentencespout.py` hello 배출구를 구현 하는 스크립트입니다.

표적이 hello에 hello Python 스크립트 toobe 리라 전망 `/resources` hello 토폴로지를 포함 하는 hello jar 파일 내 디렉터리입니다. 이 예제에서는 hello에 hello Python 스크립트를 저장 하므로 `/multilang/resources` 디렉터리입니다. hello `pom.xml` hello 다음과 같은 XML을 사용 하 여이 파일을 포함 합니다.

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

앞서 설명한 것 처럼은 `storm.py` 스톰에 대 한 hello Thrift 정의 구현 하는 파일입니다. hello 표적이 framework 포함 `storm.py` 자동으로 때 hello 프로젝트 빌드를 포함 하는 방법에 대 한 tooworry 필요가 없습니다.

## <a name="build-hello-project"></a>Hello 프로젝트 빌드

Hello hello 프로젝트의 루트에서 다음 명령을 hello를 사용 합니다.

```bash
mvn clean compile package
```

이 명령은 만듭니다는 `target/WordCount-1.0-SNAPSHOT.jar` hello 포함 된 파일에는 토폴로지 컴파일됩니다.

## <a name="run-hello-topology-locally"></a>Hello 토폴로지를 로컬로 실행

toorun hello 토폴로지를 로컬로 hello 다음 명령을 사용 합니다.

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> 이 명령에는 로컬 Storm 개발 환경이 필요합니다. 자세한 내용은 [개발 환경 설정](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)(영문)을 참조하세요.

한 번 hello 토폴로지 시작 정보 toohello 로컬 콘솔 비슷한 toohello를 텍스트 다음 내보냅니다.


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


toostop hello 토폴로지를 사용 하 여 __Ctrl + C__합니다.

## <a name="run-hello-storm-topology-on-hdinsight"></a>HDInsight에서 hello 스톰 토폴로지를 실행 합니다.

1. 사용 하 여 hello 다음 명령은 toocopy hello `WordCount-1.0-SNAPSHOT.jar` tooyour 스톰 HDInsight 클러스터에서 파일:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    대체 `sshuser` 클러스터에 대 한 SSH 사용자 hello와 합니다. 대체 `mycluster` hello 클러스터 이름을 사용 합니다. Hello SSH 사용자에 대 한 증명된 tooenter hello 암호 수 있습니다.

    SSH 및 SCP 사용에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. Hello 파일을 업로드 한 후에 SSH를 사용 하 여 toohello 클러스터 연결:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Hello SSH 세션에서 명령을 toostart hello 토폴로지 hello 클러스터에서 다음 hello를 사용 합니다.

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. Hello 스톰 UI tooview hello 토폴로지 hello 클러스터에서 사용할 수 있습니다. hello 스톰 UI는 https://mycluster.azurehdinsight.net/stormui에 있습니다. `mycluster`를 클러스터 이름으로 바꿉니다.

> [!NOTE]
> Storm 토폴로지가 시작되면 중지될 때까지 실행됩니다. toostop은 토폴로지 hello hello 메서드를 다음 중 하나를 사용 합니다.
>
> * hello `storm kill TOPOLOGYNAME` hello 명령줄에서 명령을
> * hello **Kill** hello 스톰 UI의에서 단추입니다.


## <a name="next-steps"></a>다음 단계

Hello 다음 다른 방법으로 toouse HDInsight와 Python에 대 한 문서를 참조 하십시오.

* [어떻게 스트리밍 MapReduce 작업에 대 한 Python toouse](hdinsight-hadoop-streaming-python.md)
* [어떻게 toouse Python UDF 사용자 정의 함수 ()에서 Pig 및 Hive](hdinsight-python.md)
