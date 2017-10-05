---
title: "Python 구성 요소를 사용하는 Apache Storm - Azure HDInsight | Microsoft Docs"
description: "Python 구성 요소를 사용하는 Apache Storm 토폴로지를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="44215-104">HDInsight에서 Python을 사용하여 Apache Storm 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="44215-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="44215-105">Python 구성 요소를 사용하는 Apache Storm 토폴로지를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="44215-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="44215-106">Apache Storm은 여러 언어를 지원하여 한 토폴로지에 여러 언어의 구성 요소를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="44215-107">Flux 프레임워크(Storm 0.10.0에서 소개)를 사용하면 Python 구성 요소를 사용하는 솔루션을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44215-108">이 문서의 정보는 HDInsight 3.6에서 Storm을 사용하여 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="44215-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="44215-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="44215-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44215-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="44215-111">이 프로젝트의 코드는 [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44215-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="44215-112">Prerequisites</span></span>

* <span data-ttu-id="44215-113">Python 2.7 이상</span><span class="sxs-lookup"><span data-stu-id="44215-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="44215-114">JDK Java 1.8 이상</span><span class="sxs-lookup"><span data-stu-id="44215-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="44215-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="44215-115">Maven 3</span></span>

* <span data-ttu-id="44215-116">(선택 사항) 로컬 Storm 개발 환경 -</span><span class="sxs-lookup"><span data-stu-id="44215-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="44215-117">로컬 Storm 환경은 토폴로지를 로컬로 실행하려는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="44215-118">자세한 내용은 [개발 환경 설정](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44215-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="44215-119">Storm 다중 언어 지원</span><span class="sxs-lookup"><span data-stu-id="44215-119">Storm multi-language support</span></span>

<span data-ttu-id="44215-120">Apache Storm은 모든 프로그래밍 언어로 작성된 구성 요소를 사용하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="44215-121">구성 요소에서 [Storm에 대한 Thrift 정의](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift)를 사용하는 방법을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="44215-122">Python의 경우 모듈은 Apache Storm 프로젝트의 일부로 제공되므로 Storm과 쉽게 인터페이스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="44215-123">이 모듈을 [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="44215-124">Storm은 JVM(Java Virtual Machine)에서 실행되는 Java 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="44215-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="44215-125">다른 언어로 작성된 구성 요소는 하위 프로세스로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="44215-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="44215-126">Storm은 stdin/stdout을 통해 전송되는 JSON 메시지를 사용하여 이러한 하위 프로세스와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="44215-127">구성 요소 간의 통신에 대한 자세한 내용은 [다중 언어 프로토콜](https://storm.apache.org/documentation/Multilang-protocol.html) (영문) 설명서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="44215-128">Flux 프레임워크를 사용하는 Python</span><span class="sxs-lookup"><span data-stu-id="44215-128">Python with the Flux framework</span></span>

<span data-ttu-id="44215-129">Flux 프레임워크를 사용하면 구성 요소와 별도로 Storm 토폴로지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="44215-130">Flux 프레임워크는 YAML을 사용하여 Storm 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="44215-131">다음 텍스트는 YAML 문서에서 Python 구성 요소를 참조하는 방법의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="44215-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

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

<span data-ttu-id="44215-132">`FluxShellSpout` 클래스는 Spout를 구현하는 `sentencespout.py` 스크립트를 시작하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="44215-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="44215-133">Flux에서는 토폴로지를 포함하는 jar 파일 내의 `/resources` 디렉터리에 Python 스크립트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="44215-134">따라서 이 예제는 Python 스크립트를 `/multilang/resources` 디렉터리에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="44215-135">`pom.xml`은 다음 XML을 사용하여 이 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="44215-136">앞에서 언급했듯이 Storm에 대한 Thrift 정의를 구현하는 `storm.py` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="44215-137">Flux 프레임워크는 프로젝트를 빌드할 때 `storm.py`를 자동으로 포함하므로 파일을 포함하는 것에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="44215-138">프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="44215-138">Build the project</span></span>

<span data-ttu-id="44215-139">프로젝트의 루트에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="44215-140">이 명령은 컴파일된 토폴로지를 포함하는 `target/WordCount-1.0-SNAPSHOT.jar` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44215-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="44215-141">로컬로 토폴로지 실행</span><span class="sxs-lookup"><span data-stu-id="44215-141">Run the topology locally</span></span>

<span data-ttu-id="44215-142">토폴로지를 로컬로 실행하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="44215-143">이 명령에는 로컬 Storm 개발 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="44215-144">자세한 내용은 [개발 환경 설정](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44215-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="44215-145">토폴로지가 시작되면 다음 텍스트와 비슷한 정보를 로컬 콘솔로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="44215-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="44215-146">토폴로지를 중지하려면 __Ctrl + C__를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="44215-147">HDInsight에서 Storm 토폴로지 실행</span><span class="sxs-lookup"><span data-stu-id="44215-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="44215-148">다음 명령을 사용하여 HDInsight 클러스터의 Storm에 `WordCount-1.0-SNAPSHOT.jar` 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="44215-149">`sshuser`를 클러스터의 SSH 사용자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="44215-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="44215-150">`mycluster`를 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="44215-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="44215-151">SSH 사용자의 암호를 입력하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="44215-152">SSH 및 SCP 사용에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44215-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="44215-153">파일이 업로드되면 SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="44215-154">SSH 세션에서 다음 명령을 사용하여 클러스터에서 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="44215-155">Storm UI를 사용하여 클러스터에서 토폴로지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="44215-156">Storm UI는 https://mycluster.azurehdinsight.net/stormui에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44215-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="44215-157">`mycluster`를 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="44215-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="44215-158">Storm 토폴로지가 시작되면 중지될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="44215-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="44215-159">토폴로지를 중지하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44215-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="44215-160">명령줄에서 `storm kill TOPOLOGYNAME` 명령</span><span class="sxs-lookup"><span data-stu-id="44215-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="44215-161">Storm UI의 **종료**(Kill) 단추</span><span class="sxs-lookup"><span data-stu-id="44215-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="44215-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44215-162">Next steps</span></span>

<span data-ttu-id="44215-163">HDInsight와 함께 Python을 사용하는 다른 방법은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44215-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="44215-164">MapReduce 작업을 스트리밍하는 데 Python을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="44215-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="44215-165">Pig 및 Hive에서 UDF(사용자 정의 함수)를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="44215-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
