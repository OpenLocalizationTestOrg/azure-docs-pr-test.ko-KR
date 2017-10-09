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
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="c6ca2-105">HDInsight의 Apache Storm에서 tooHDFS 작성</span><span class="sxs-lookup"><span data-stu-id="c6ca2-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="c6ca2-106">HDInsight의 Apache Storm 프로그램 toouse 스톰 toowrite 데이터 toohello HDFS 호환 저장소의 사용 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="c6ca2-107">HDInsight는 Azure Storage 및 Azure Data Lake Store를 모두 HDFS 호환 저장소로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="c6ca2-108">Storm 제공는 [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) 데이터 tooHDFS를 작성 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="c6ca2-109">이 문서에서는 저장소 tooeither 유형의 hello HdfsBolt에서에서 작성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c6ca2-110">이 문서에 사용 된 토폴로지 hello 예제 HDInsight의 Storm에 포함 된 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="c6ca2-111">Azure 데이터 레이크 저장소 다른 Apache Storm 클러스터와 함께 사용할 때와 수정 toowork가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="c6ca2-112">Hello 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="c6ca2-112">Get hello code</span></span>

<span data-ttu-id="c6ca2-113">이 토폴로지를 포함 하는 hello 프로젝트에서 다운로드할 수는 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="c6ca2-114">toocompile이이 프로젝트를 hello 같은 개발 환경에 대 한 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="c6ca2-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상</span><span class="sxs-lookup"><span data-stu-id="c6ca2-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="c6ca2-116">- HDInsight 3.5 이상에는 Java 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="c6ca2-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="c6ca2-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="c6ca2-118">hello 다음과 같은 환경 변수 설정 되어 있습니다 Java와 hello JDK 개발용 워크스테이션에 설치 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="c6ca2-119">그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="c6ca2-120">`JAVA_HOME`-toohello hello JDK가 설치 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="c6ca2-121">`PATH`-경로 따라 hello를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="c6ca2-122">`JAVA_HOME`(또는 hello 해당 하는 경로)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="c6ca2-123">`JAVA_HOME\bin`(또는 hello 해당 하는 경로)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="c6ca2-124">Maven 설치 되어 있는 hello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="c6ca2-125">Toouse는 HDInsight와 HdfsBolt hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="c6ca2-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6ca2-126">Hello HdfsBolt HDInsight의 Storm를 사용 하기 전에 먼저 사용 해야 스크립트 동작 필요한 toocopy jar 파일 hello에 `extpath` Storm의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="c6ca2-127">자세한 내용은 참조 hello [구성 hello 클러스터](#configure) 섹션.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="c6ca2-128">toounderstand을 어떻게 제공 하는 hello 파일 체계를 사용 하는 hello HdfsBolt toowrite tooHDFS 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="c6ca2-129">HDInsight를와 hello 구성표를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="c6ca2-130">`wasb://`: Azure Storage 계정과 함께 사용</span><span class="sxs-lookup"><span data-stu-id="c6ca2-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="c6ca2-131">`adl://`: Azure Data Lake Store와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="c6ca2-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="c6ca2-132">hello 다음 표에서 hello 파일 체계를 사용 하 여 다양 한 시나리오에 대 한 예:</span><span class="sxs-lookup"><span data-stu-id="c6ca2-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="c6ca2-133">구성표</span><span class="sxs-lookup"><span data-stu-id="c6ca2-133">Scheme</span></span> | <span data-ttu-id="c6ca2-134">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c6ca2-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="c6ca2-135">hello 기본 저장소 계정 blob 컨테이너는 Azure 저장소 계정에는</span><span class="sxs-lookup"><span data-stu-id="c6ca2-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="c6ca2-136">hello 기본 저장소 계정에는 Azure 데이터 레이크 저장소의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="c6ca2-137">클러스터를 만드는 동안 hello 루트 hello 클러스터의 HDFS에 있는 데이터 레이크 저장소의 hello 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="c6ca2-138">예를 들어 hello `/clusters/myclustername/` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="c6ca2-139">Hello 클러스터와 연결 된 기본이 아닌 (추가) Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="c6ca2-140">hello hello 클러스터에서 사용 하는 데이터 레이크 저장소의 hello 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="c6ca2-141">이 체계 hello 클러스터 파일 시스템을 포함 하는 hello 디렉터리 외부에 있는 tooaccess 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="c6ca2-142">자세한 내용은 참조 hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) Apache.org에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="c6ca2-143">예제 구성</span><span class="sxs-lookup"><span data-stu-id="c6ca2-143">Example configuration</span></span>

<span data-ttu-id="c6ca2-144">hello 다음 YAML는 hello 발췌 `resources/writetohdfs.yaml` hello 예제에 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="c6ca2-145">이 파일은 hello를 사용 하 여 hello 스톰 토폴로지 정의 [표적이](https://storm.apache.org/releases/1.1.0/flux.html) Apache Storm의 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="c6ca2-146">이 YAML hello 다음 항목을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="c6ca2-147">`syncPolicy`: 경우 파일은 동기화/플러시 toohello 파일 시스템을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="c6ca2-148">이 예제에서는 1,000개 튜플마다 동기화/플러시되도록 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="c6ca2-149">`fileNameFormat`: 파일을 작성할 때 hello 경로 파일 이름 패턴 toouse를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="c6ca2-150">이 예제에서는 hello 경로 필터를 사용 하 여 런타임에 제공 되 고 hello 파일 확장명은 `.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="c6ca2-151">`recordFormat`: Hello 기록 된 hello 파일의 내부 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="c6ca2-152">이 예제에서는 필드 hello로 구분 된 `|` 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="c6ca2-153">`rotationPolicy`: 시기를 정의 toorotate 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="c6ca2-154">이 예제에서는 회전이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="c6ca2-155">`hdfs-bolt`: 사용 하 여 hello에 대 한 구성 매개 변수로 이전 구성 요소를 hello `HdfsBolt` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="c6ca2-156">Hello 표적이 프레임 워크에 대 한 자세한 내용은 참조 하십시오. [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="c6ca2-157">Hello 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="c6ca2-157">Configure hello cluster</span></span>

<span data-ttu-id="c6ca2-158">기본적으로 HDInsight의 Storm HdfsBolt 사용 된 Azure 저장소 서비스 또는 데이터 레이크 저장소 toocommunicate Storm의 클래스 경로에서 하는 hello 구성 요소를 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="c6ca2-159">사용 하 여 hello 다음 스크립트 동작 tooadd 이러한 구성 요소 toohello `extlib` 디렉터리 Storm의 클러스터에:</span><span class="sxs-lookup"><span data-stu-id="c6ca2-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="c6ca2-160">| 스크립트 URI | 노드 tooapply 하도록 | 매개 변수 | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, 감독자 | None |</span><span class="sxs-lookup"><span data-stu-id="c6ca2-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="c6ca2-161">이 스크립트를 사용 하 여 클러스터 사용에 대 한 내용은 hello 참조 [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](./hdinsight-hadoop-customize-cluster-linux.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="c6ca2-162">빌드 및 패키징합니다 hello 토폴로지</span><span class="sxs-lookup"><span data-stu-id="c6ca2-162">Build and package hello topology</span></span>

1. <span data-ttu-id="c6ca2-163">hello 예제 프로젝트를 다운로드 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="c6ca2-164">명령 프롬프트에서 터미널 또는 셸 세션 디렉터리 toohello 루트 변경 hello의 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="c6ca2-165">토폴로지 hello toobuild 및 패키지 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="c6ca2-166">라는 새 디렉터리 없는 hello 빌드 및 패키징 완료 되 면 `target`, 라는 파일을 포함 하는 `StormToHdfs-1.0-SNAPSHOT.jar`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="c6ca2-167">이 파일에 컴파일된 hello 토폴로지 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="c6ca2-168">배포 하 고 hello 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="c6ca2-169">Hello 다음 명령 toocopy hello 토폴로지 toohello HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="c6ca2-170">대체 **사용자** hello 클러스터를 만들 때 사용한 hello SSH 사용자 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="c6ca2-171">대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="c6ca2-172">메시지가 표시 되 면 hello 클러스터에 대 한 hello SSH 사용자를 만들 때 사용 하는 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="c6ca2-173">공개 키 대신 암호를 사용 하는 경우 toouse hello 할 수 있습니다 `-i` 개인 키와 일치 하는 매개 변수 toospecify hello 경로 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c6ca2-174">HDInsight에서의 `scp` 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](./hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c6ca2-175">Hello 업로드가 완료 되 면 hello tooconnect toohello HDInsight 클러스터 SSH를 사용 하 여 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="c6ca2-176">대체 **사용자** hello 클러스터를 만들 때 사용한 hello SSH 사용자 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="c6ca2-177">대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="c6ca2-178">메시지가 표시 되 면 hello 클러스터에 대 한 hello SSH 사용자를 만들 때 사용 하는 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="c6ca2-179">공개 키 대신 암호를 사용 하는 경우 toouse hello 할 수 있습니다 `-i` 개인 키와 일치 하는 매개 변수 toospecify hello 경로 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="c6ca2-180">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="c6ca2-181">사용 하 여 hello 다음 명령은 이라는 파일로 내보내집니다 toocreate 연결 되 면 `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="c6ca2-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="c6ca2-182">콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `dev.properties` 파일:</span><span class="sxs-lookup"><span data-stu-id="c6ca2-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="c6ca2-183">이 예제에서는 클러스터에 Azure 저장소 계정을 사용 하 여 hello 기본 저장소로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="c6ca2-184">클러스터에서 Azure Data Lake Store를 사용하는 경우 `hdfs.url: adl:///`을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="c6ca2-185">toosave hello 파일을 사용 하 여 __Ctrl + X__, 다음 __Y__, 마지막으로 __Enter__합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="c6ca2-186">이 파일에 hello 값 hello 데이터 레이크 저장소 URL 및 데이터에 기록 되는 hello 디렉터리 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="c6ca2-187">다음 명령 toostart hello 토폴로지 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="c6ca2-188">이 명령은 hello 표적이 프레임 워크를 사용 하 여 hello 클러스터의 toohello Nimbus 노드에 전송 하 여 hello 토폴로지를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="c6ca2-189">hello hello 토폴로지를 정의 `writetohdfs.yaml` hello jar에 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="c6ca2-190">hello `dev.properties` 파일 필터를 변수로 전달 되 고 hello 토폴로지 hello 파일에 포함 된 hello 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="c6ca2-191">출력 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="c6ca2-191">View output data</span></span>

<span data-ttu-id="c6ca2-192">다음 명령을 사용 하 여 hello tooview hello 데이터:</span><span class="sxs-lookup"><span data-stu-id="c6ca2-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="c6ca2-193">이 토폴로지에서 만든 hello 파일의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="c6ca2-194">hello 다음 목록은 hello 이전 명령에서 반환 하는 hello 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="c6ca2-195">Hello 토폴로지를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-195">Stop hello topology</span></span>

<span data-ttu-id="c6ca2-196">Storm 토폴로지 중지 될 때까지 실행 또는 hello 클러스터가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="c6ca2-197">다음 명령을 사용 하 여 hello toostop hello 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="c6ca2-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="c6ca2-198">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="c6ca2-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="c6ca2-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6ca2-199">Next steps</span></span>

<span data-ttu-id="c6ca2-200">Toouse 스톰 toowrite tooAzure 저장소 및 Azure 데이터 레이크 저장소 검색 방법을 다른 배웠습니다 했으므로 [HDInsight에 대 한 예제 스톰](hdinsight-storm-example-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ca2-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

