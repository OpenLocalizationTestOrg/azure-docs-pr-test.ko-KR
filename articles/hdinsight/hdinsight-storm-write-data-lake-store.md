---
title: "Apache Storm에서 Storage/Data Lake Store에 쓰기 - Azure HDInsight | Microsoft Docs"
description: "Apache Storm을 사용하여 HDInsight용 HDFS 호환 저장소에 쓰는 방법을 알아봅니다. Azure Storage 또는 Azure Data Lake Store는 HDInsight용 HDFS 호환 저장소를 제공합니다. 이 문서 및 관련 예제에서는 HdfsBolt 구성 요소를 사용하여 HDInsight 클러스터에서 Storm의 기본 저장소에 쓰는 방법을 보여 줍니다."
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
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="35324-105">HDInsight의 Apache Storm에서 HDFS에 쓰기</span><span class="sxs-lookup"><span data-stu-id="35324-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="35324-106">Storm을 사용하여 HDInsight의 Apache Storm에서 사용하는 HDFS 호환 저장소에 데이터를 쓰는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="35324-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="35324-107">HDInsight는 Azure Storage 및 Azure Data Lake Store를 모두 HDFS 호환 저장소로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="35324-108">Storm은 HDFS에 데이터를 쓰는 [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="35324-109">이 문서는 HdfsBolt에서 두 가지 유형의 저장소에 쓰는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="35324-110">이 문서에서 사용되는 예제 토폴로지는 HDInsight의 Storm에 포함된 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="35324-111">다른 Apache Storm 클러스터와 함께 Azure Data Lake Store를 사용하려면 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="35324-112">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="35324-112">Get the code</span></span>

<span data-ttu-id="35324-113">이 토폴로지를 포함하는 프로젝트는 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store)에서 다운로드로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="35324-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="35324-114">이 프로젝트를 컴파일하기 위해 개발 환경에 필요한 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="35324-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상</span><span class="sxs-lookup"><span data-stu-id="35324-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="35324-116">- HDInsight 3.5 이상에는 Java 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="35324-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="35324-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="35324-118">Java 및 JDK를 설치할 때 사용자의 개발 워크스테이션에 다음 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="35324-119">하지만 변수가 존재하며 시스템에 대한 올바른 값을 포함하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="35324-120">`JAVA_HOME` - JDK가 설치된 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="35324-121">`PATH` - 다음 경로를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="35324-122">`JAVA_HOME`(또는 이와 동등한 경로)</span><span class="sxs-lookup"><span data-stu-id="35324-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="35324-123">`JAVA_HOME\bin`(또는 이와 동등한 경로)</span><span class="sxs-lookup"><span data-stu-id="35324-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="35324-124">Maven이 설치된 디렉터리</span><span class="sxs-lookup"><span data-stu-id="35324-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="35324-125">HDInsight에서 HdfsBolt를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="35324-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35324-126">HDInsight의 Storm에서 HdfsBolt를 사용하려면 먼저 스크립트 동작을 사용하여 필요한 jar 파일에 Storm에 대한 `extpath`를 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="35324-127">자세한 내용은 [클러스터 구성](#configure)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35324-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="35324-128">HdfsBolt는 사용자가 제공하는 파일 구성표를 사용하여 HDFS에 쓰는 방법을 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="35324-129">HDInsight를 사용하는 경우 다음 구성표 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="35324-130">`wasb://`: Azure Storage 계정과 함께 사용</span><span class="sxs-lookup"><span data-stu-id="35324-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="35324-131">`adl://`: Azure Data Lake Store와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="35324-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="35324-132">다음 표에서는 여러 시나리오에 대한 파일 구성표를 사용하는 경우의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="35324-133">구성표</span><span class="sxs-lookup"><span data-stu-id="35324-133">Scheme</span></span> | <span data-ttu-id="35324-134">참고 사항</span><span class="sxs-lookup"><span data-stu-id="35324-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="35324-135">기본 저장소 계정은 Azure Storage 계정의 Blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="35324-136">기본 저장소 계정은 Azure Data Lake Store의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="35324-137">클러스터를 만드는 동안 클러스터의 HDFS 루트인 Data Lake Store의 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="35324-138">예를 들어 `/clusters/myclustername/` 디렉터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="35324-139">클러스터와 연결된 기본이 아닌 추가 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="35324-140">클러스터에서 사용하는 Data Lake Store의 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="35324-141">이 구성표를 사용하면 클러스터 파일 시스템이 포함된 디렉터리 외부에 있는 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="35324-142">자세한 내용은 Apache.org의 [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35324-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="35324-143">예제 구성</span><span class="sxs-lookup"><span data-stu-id="35324-143">Example configuration</span></span>

<span data-ttu-id="35324-144">다음 YAML은 예제에 포함된 `resources/writetohdfs.yaml` 파일에서 인용한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="35324-145">이 파일에서는 Apache Storm의 [Flux](https://storm.apache.org/releases/1.1.0/flux.html) 프레임워크를 사용하여 Storm 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="35324-146">이 YAML에서 정의하는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="35324-147">`syncPolicy`: 파일 시스템에 파일이 동기화/플러시되는 시기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="35324-148">이 예제에서는 1,000개 튜플마다 동기화/플러시되도록 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="35324-149">`fileNameFormat`: 파일을 쓸 때 사용할 경로 및 파일 이름 패턴을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="35324-150">이 예제에서 경로는 필터를 사용하여 런타임에 제공되며 파일 확장명은 `.txt`입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="35324-151">`recordFormat`: 기록된 파일의 내부 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="35324-152">이 예제에서 필드는 `|` 문자로 구분되었습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="35324-153">`rotationPolicy`: 파일을 회전하는 시기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="35324-154">이 예제에서는 회전이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="35324-155">`hdfs-bolt`: 이전 구성 요소를 `HdfsBolt` 클래스의 구성 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="35324-156">Flux 프레임워크에 대한 자세한 내용은 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35324-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="35324-157">클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="35324-157">Configure the cluster</span></span>

<span data-ttu-id="35324-158">기본적으로 HDInsight의 Storm에는 HdfsBolt에서 Storm의 클래스 경로에 있는 Azure Storage 또는 Data Lake Store와 통신하는 데 사용하는 구성 요소가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="35324-159">다음 스크립트 동작을 사용하여 클러스터의 Storm에 대한 `extlib` 디렉터리에 이러한 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="35324-160">| 스크립트 URI | 이를 적용하는 노드 | 매개 변수 | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, 감독자 | None |</span><span class="sxs-lookup"><span data-stu-id="35324-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="35324-161">HDInsight에서 이 스크립트를 사용하는 방법에 대한 자세한 내용은 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](./hdinsight-hadoop-customize-cluster-linux.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35324-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="35324-162">토폴로지 빌드 및 패키지</span><span class="sxs-lookup"><span data-stu-id="35324-162">Build and package the topology</span></span>

1. <span data-ttu-id="35324-163">[https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) 에서 개발 환경에 예제 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="35324-164">명령 프롬프트, 터미널 또는 셸 세션에서 다운로드한 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="35324-165">토폴로지를 빌드하고 패키지하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="35324-166">빌드 및 패키징이 완료되면 `StormToHdfs-1.0-SNAPSHOT.jar`이라는 파일이 포함된 `target`이라는 새 디렉터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="35324-167">이 파일에는 컴파일된 토폴로지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35324-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="35324-168">토폴로지 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="35324-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="35324-169">다음 명령을 사용하여 HDInsight 클러스터에 토폴로지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="35324-170">**USER** 를 클러스터를 만들 때 사용한 SSH 사용자 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="35324-171">**CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="35324-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="35324-172">메시지가 표시되면 클러스터에 대한 SSH 사용자를 만들 때 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="35324-173">암호 대신 공용 키를 사용하는 경우 `-i` 매개 변수를 사용하여 개인 키와 일치하는 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="35324-174">HDInsight에서의 `scp` 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](./hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35324-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="35324-175">업로드가 완료되면 SSH를 사용하여 HDInsight 클러스터에 연결하도록 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="35324-176">**USER** 를 클러스터를 만들 때 사용한 SSH 사용자 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="35324-177">**CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="35324-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="35324-178">메시지가 표시되면 클러스터에 대한 SSH 사용자를 만들 때 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="35324-179">암호 대신 공용 키를 사용하는 경우 `-i` 매개 변수를 사용하여 개인 키와 일치하는 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="35324-180">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35324-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="35324-181">연결되면 다음 명령을 사용하여 `dev.properties`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35324-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="35324-182">`dev.properties` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="35324-183">이 예제에서는 클러스터에서 Azure Storage 계정을 기본 저장소로 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="35324-184">클러스터에서 Azure Data Lake Store를 사용하는 경우 `hdfs.url: adl:///`을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="35324-185">파일을 저장하려면 __Ctrl + X__를 사용한 다음 __Y__를 입력하고 마지막으로 __Enter__ 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="35324-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="35324-186">이 파일의 값은 데이터가 기록되는 Data Lake store URL 및 디렉터리 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="35324-187">다음 명령을 사용하여 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="35324-188">이 명령은 클러스터의 Nimbus 노드에 제출하여 Flux 프레임워크를 사용하는 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="35324-189">토폴로지를 jar에 포함된 `writetohdfs.yaml` 파일에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="35324-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="35324-190">`dev.properties` 파일은 필터로 전달되고 파일에 포함된 값은 토폴로지에서 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="35324-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="35324-191">출력 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="35324-191">View output data</span></span>

<span data-ttu-id="35324-192">데이터를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="35324-193">이 토폴로지로 만든 파일 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35324-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="35324-194">다음 목록은 이전 명령에서 반환된 데이터 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="35324-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="35324-195">토폴로지 중지</span><span class="sxs-lookup"><span data-stu-id="35324-195">Stop the topology</span></span>

<span data-ttu-id="35324-196">Storm 토폴로지가 중지될 때까지 실행되거나 클러스터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="35324-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="35324-197">토폴로지를 중지하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="35324-198">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="35324-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="35324-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35324-199">Next steps</span></span>

<span data-ttu-id="35324-200">이제 Storm을 사용하여 Azure Data Lake Store에 쓰는 방법을 알아보았으므로 다른 [HDInsight에 대한 Storm 예제](hdinsight-storm-example-topology.md)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="35324-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

