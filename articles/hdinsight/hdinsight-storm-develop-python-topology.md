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
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="6c68f-104">HDInsight에서 Python을 사용하여 Apache Storm 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="6c68f-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="6c68f-105">자세한 내용은 방법 toocreate Python 구성 요소를 사용 하는 Apache Storm 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="6c68f-106">Apache Storm도 한 토폴로지의 여러 언어에서 구성 요소를 toocombine 허용 여러 언어를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="6c68f-107">hello 표적이 프레임 워크 (스톰 0.10.0에서 도입)를 있습니다 tooeasily Python 구성 요소를 사용 하는 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c68f-108">이 문서에서 hello 정보 스톰 HDInsight 3.6에서 사용 하 여 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="6c68f-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6c68f-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c68f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="6c68f-111">이 프로젝트에 대 한 hello 코드에서 사용할 수는 [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c68f-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6c68f-112">Prerequisites</span></span>

* <span data-ttu-id="6c68f-113">Python 2.7 이상</span><span class="sxs-lookup"><span data-stu-id="6c68f-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="6c68f-114">JDK Java 1.8 이상</span><span class="sxs-lookup"><span data-stu-id="6c68f-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="6c68f-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="6c68f-115">Maven 3</span></span>

* <span data-ttu-id="6c68f-116">(선택 사항) 로컬 Storm 개발 환경 -</span><span class="sxs-lookup"><span data-stu-id="6c68f-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="6c68f-117">로컬 스톰 환경 toorun hello 토폴로지 로컬로 하려는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="6c68f-118">자세한 내용은 [개발 환경 설정](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c68f-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="6c68f-119">Storm 다중 언어 지원</span><span class="sxs-lookup"><span data-stu-id="6c68f-119">Storm multi-language support</span></span>

<span data-ttu-id="6c68f-120">Apache Storm 모든 프로그래밍 언어를 사용 하 여 작성 된 구성 요소 디자인 된 toowork 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="6c68f-121">hello 구성 요소를 이해 해야 어떻게 hello로 toowork [스톰에 대 한 Thrift 정의](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="6c68f-122">Python에 대 한 모듈 Storm tooeasily 인터페이스를 허용 하는 hello Apache Storm 프로젝트의 일부로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="6c68f-123">이 모듈을 [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="6c68f-124">Storm는 hello 가상 컴퓨터 JVM (Java)에서 실행 되는 Java 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="6c68f-125">다른 언어로 작성된 구성 요소는 하위 프로세스로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="6c68f-126">hello 스톰 stdin/stdout 통해 전송 된 JSON 메시지를 사용 하 여 이러한 하위 프로세스와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="6c68f-127">구성 요소 간의 통신에 대 한 자세한 내용은 hello에서 확인할 수 있습니다 [다중 lang 프로토콜](https://storm.apache.org/documentation/Multilang-protocol.html) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="6c68f-128">Python hello 표적이 프레임 워크 사용</span><span class="sxs-lookup"><span data-stu-id="6c68f-128">Python with hello Flux framework</span></span>

<span data-ttu-id="6c68f-129">hello 표적이 프레임 워크에서는 hello 구성 요소와는 별도로 toodefine 스톰 토폴로지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="6c68f-130">hello 표적이 framework YAML toodefine hello 스톰 토폴로지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="6c68f-131">hello 다음 텍스트는 방법의 예로 tooreference hello YAML 문서에서 Python 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="6c68f-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="6c68f-132">클래스를 hello `FluxShellSpout` 는 사용 되는 toostart hello `sentencespout.py` hello 배출구를 구현 하는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="6c68f-133">표적이 hello에 hello Python 스크립트 toobe 리라 전망 `/resources` hello 토폴로지를 포함 하는 hello jar 파일 내 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="6c68f-134">이 예제에서는 hello에 hello Python 스크립트를 저장 하므로 `/multilang/resources` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="6c68f-135">hello `pom.xml` hello 다음과 같은 XML을 사용 하 여이 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="6c68f-136">앞서 설명한 것 처럼은 `storm.py` 스톰에 대 한 hello Thrift 정의 구현 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="6c68f-137">hello 표적이 framework 포함 `storm.py` 자동으로 때 hello 프로젝트 빌드를 포함 하는 방법에 대 한 tooworry 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="6c68f-138">Hello 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="6c68f-138">Build hello project</span></span>

<span data-ttu-id="6c68f-139">Hello hello 프로젝트의 루트에서 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="6c68f-140">이 명령은 만듭니다는 `target/WordCount-1.0-SNAPSHOT.jar` hello 포함 된 파일에는 토폴로지 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="6c68f-141">Hello 토폴로지를 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="6c68f-141">Run hello topology locally</span></span>

<span data-ttu-id="6c68f-142">toorun hello 토폴로지를 로컬로 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="6c68f-143">이 명령에는 로컬 Storm 개발 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="6c68f-144">자세한 내용은 [개발 환경 설정](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c68f-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="6c68f-145">한 번 hello 토폴로지 시작 정보 toohello 로컬 콘솔 비슷한 toohello를 텍스트 다음 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="6c68f-146">toostop hello 토폴로지를 사용 하 여 __Ctrl + C__합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="6c68f-147">HDInsight에서 hello 스톰 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="6c68f-148">사용 하 여 hello 다음 명령은 toocopy hello `WordCount-1.0-SNAPSHOT.jar` tooyour 스톰 HDInsight 클러스터에서 파일:</span><span class="sxs-lookup"><span data-stu-id="6c68f-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6c68f-149">대체 `sshuser` 클러스터에 대 한 SSH 사용자 hello와 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="6c68f-150">대체 `mycluster` hello 클러스터 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="6c68f-151">Hello SSH 사용자에 대 한 증명된 tooenter hello 암호 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="6c68f-152">SSH 및 SCP 사용에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c68f-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6c68f-153">Hello 파일을 업로드 한 후에 SSH를 사용 하 여 toohello 클러스터 연결:</span><span class="sxs-lookup"><span data-stu-id="6c68f-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="6c68f-154">Hello SSH 세션에서 명령을 toostart hello 토폴로지 hello 클러스터에서 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="6c68f-155">Hello 스톰 UI tooview hello 토폴로지 hello 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="6c68f-156">hello 스톰 UI는 https://mycluster.azurehdinsight.net/stormui에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="6c68f-157">`mycluster`를 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="6c68f-158">Storm 토폴로지가 시작되면 중지될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="6c68f-159">toostop은 토폴로지 hello hello 메서드를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="6c68f-160">hello `storm kill TOPOLOGYNAME` hello 명령줄에서 명령을</span><span class="sxs-lookup"><span data-stu-id="6c68f-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="6c68f-161">hello **Kill** hello 스톰 UI의에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c68f-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6c68f-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c68f-162">Next steps</span></span>

<span data-ttu-id="6c68f-163">Hello 다음 다른 방법으로 toouse HDInsight와 Python에 대 한 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c68f-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="6c68f-164">어떻게 스트리밍 MapReduce 작업에 대 한 Python toouse</span><span class="sxs-lookup"><span data-stu-id="6c68f-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="6c68f-165">어떻게 toouse Python UDF 사용자 정의 함수 ()에서 Pig 및 Hive</span><span class="sxs-lookup"><span data-stu-id="6c68f-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
