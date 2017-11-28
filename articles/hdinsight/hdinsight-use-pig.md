---
title: "HDInsight|Microsoft Docs에서 Hadoop Pig 사용"
description: "HDInsight에서 Hadoop와 함께 Pig를 사용하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="f4089-103">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="f4089-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="f4089-104">HDInsight에서 [Apache Pig](http://pig.apache.org/)를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="f4089-105">Pig는 *Pig Latin*이라는 절차형 언어를 사용하여 Hadoop용 프로그램을 생성하기 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="f4089-106">Pig는 *MapReduce* 을 만드는 Java를 대체하는 솔루션이며 Azure HDInsight와 함께 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="f4089-107">다음 표를 사용하여 HDInsight에서 Pig를 사용하는 다양한 방법을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="f4089-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="f4089-108">**이것을 사용** 하세요...</span><span class="sxs-lookup"><span data-stu-id="f4089-108">**Use this** if you want...</span></span> | <span data-ttu-id="f4089-109">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="f4089-109">...an **interactive** shell</span></span> | <span data-ttu-id="f4089-110">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="f4089-110">...**batch** processing</span></span> | <span data-ttu-id="f4089-111">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="f4089-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="f4089-112">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="f4089-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="f4089-113">SSH</span><span class="sxs-lookup"><span data-stu-id="f4089-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="f4089-114">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-114">✔</span></span> |<span data-ttu-id="f4089-115">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-115">✔</span></span> |<span data-ttu-id="f4089-116">Linux</span><span class="sxs-lookup"><span data-stu-id="f4089-116">Linux</span></span> |<span data-ttu-id="f4089-117">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f4089-118">REST API</span><span class="sxs-lookup"><span data-stu-id="f4089-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="f4089-119">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-119">✔</span></span> |<span data-ttu-id="f4089-120">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-120">Linux or Windows</span></span> |<span data-ttu-id="f4089-121">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f4089-122">Hadoop용 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f4089-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="f4089-123">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-123">✔</span></span> |<span data-ttu-id="f4089-124">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-124">Linux or Windows</span></span> |<span data-ttu-id="f4089-125">Windows(당분간)</span><span class="sxs-lookup"><span data-stu-id="f4089-125">Windows (for now)</span></span> |
| [<span data-ttu-id="f4089-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4089-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="f4089-127">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-127">✔</span></span> |<span data-ttu-id="f4089-128">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-128">Linux or Windows</span></span> |<span data-ttu-id="f4089-129">Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-129">Windows</span></span> |
| <span data-ttu-id="f4089-130">[원격 데스크톱](hdinsight-hadoop-use-pig-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="f4089-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="f4089-131">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-131">✔</span></span> |<span data-ttu-id="f4089-132">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-132">✔</span></span> |<span data-ttu-id="f4089-133">Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-133">Windows</span></span> |<span data-ttu-id="f4089-134">Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f4089-135">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f4089-136">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4089-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="f4089-137"><a id="why"></a>Pig를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="f4089-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="f4089-138">Hadoop의 MapReduce를 사용하여 데이터를 처리할 때 문제는 지도 및 reduce 함수만을 사용하여 처리 논리를 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="f4089-139">복잡한 처리를 위해 종종 처리를 같이 연결된 여러 MapReduce 작업으로 나누어야 원하는 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="f4089-140">Pig를 사용하면 원하는 출력을 생산하기 위해 데이터가 통과하는 일련의 변환으로 처리를 규정할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="f4089-141">원하는 출력을 생산하기 위해 Pig Litin 언어를 사용하여 하나 이상의 변환을 거쳐 원시 입력을 데이터 플로로 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="f4089-142">Pig Latin 프로그램이 일반적인 패턴을 따릅니다:</span><span class="sxs-lookup"><span data-stu-id="f4089-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="f4089-143">**부하**: 파일 시스템에서 조작할 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="f4089-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="f4089-144">**변환**: 데이터 조작</span><span class="sxs-lookup"><span data-stu-id="f4089-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="f4089-145">**덤프 또는 저장**: 데이터를 화면에 출력하거나 처리를 위해 저장</span><span class="sxs-lookup"><span data-stu-id="f4089-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="f4089-146">사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="f4089-146">User-defined functions</span></span>

<span data-ttu-id="f4089-147">또한 Pig Latin는 사용자가 Pig Latin의 모델에 어려운 논리를 구현하는 외부 구성 요소를 적용할 수 있도록 사용자 정의 함수(UDF)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="f4089-148">Pig Latin에 대한 자세한 내용은 [Pig Latin 참조 설명서 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) 및 [Pig Latin 참조 설명서 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4089-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="f4089-149">Pig와 UDF를 사용하는 예로, 다음 문서를 참조하십시오:</span><span class="sxs-lookup"><span data-stu-id="f4089-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="f4089-150">[HDInsight에서 HDInsight와 함께 Pig 사용](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu는 Apache에서 유지 관리하는 유용한 UDF의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="f4089-151">HDInsight에서 Pig 및 Hive와 함께 Python 사용</span><span class="sxs-lookup"><span data-stu-id="f4089-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="f4089-152">HDInsight에서 Hive 및 Pig와 함께 C# 사용</span><span class="sxs-lookup"><span data-stu-id="f4089-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="f4089-153"><a id="data"></a>예제 데이터</span><span class="sxs-lookup"><span data-stu-id="f4089-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="f4089-154">HDInsight에서는 `/example/data` 및 `/HdiSamples` 디렉터리에 저장되는 다양한 예제 데이터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="f4089-155">이러한 디렉터리는 클러스터의 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="f4089-156">이 문서의 Pig 예제는 `/example/data/sample.log`의 *log4j* 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="f4089-157">파일 내부의 각 로그는 유형과 심각도를 표시하는 `[LOG LEVEL]`  필드가 포함된 필드의 줄로 구성되어 있습니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="f4089-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="f4089-158">이전 예에서 로그 수준은 ERROR입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="f4089-159">[Apache Log4j](http://en.wikipedia.org/wiki/Log4j) 도구 로깅하여 log4j 파일을 생성하고 해당 파일을 사용자의 blob에 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="f4089-160">해당 지침은 [HDInsight에 데이터 업로드](hdinsight-upload-data.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4089-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="f4089-161">HDInsight와 함께 Azure Blob 저장소를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4089-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="f4089-162"><a id="job"></a>예제 작업</span><span class="sxs-lookup"><span data-stu-id="f4089-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="f4089-163">다음 Pig Latin 작업은 HDInsight 클러스터의 기본 저장소에서 `sample.log` 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="f4089-164">그런 다음 입력된 데이터에서 각 로그 수준이 발생한 횟수로 나타나는 일련의 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="f4089-165">결과는 STDOUT에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="f4089-166">다음 그림에서는 각 변환으로 인해 데이터에 수행되는 작업을 요약해서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-166">The following image shows a summary of what each transformation does to the data.</span></span>

![변환의 그래픽 표현][image-hdi-pig-data-transformation]

## <span data-ttu-id="f4089-168"><a id="run"></a>Pig Latin 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f4089-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="f4089-169">HDInsight는 다양한 메서드를 사용하여 Pig Latin 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="f4089-170">어떤 메서드가 적합한지 결정하는 다음 테이블을 사용하여 연습할 수 있는 링크를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f4089-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="f4089-171">**이것을 사용** 하세요...</span><span class="sxs-lookup"><span data-stu-id="f4089-171">**Use this** if you want...</span></span> | <span data-ttu-id="f4089-172">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="f4089-172">...an **interactive** shell</span></span> | <span data-ttu-id="f4089-173">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="f4089-173">...**batch** processing</span></span> | <span data-ttu-id="f4089-174">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="f4089-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="f4089-175">...**클라이언트**</span><span class="sxs-lookup"><span data-stu-id="f4089-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="f4089-176">SSH</span><span class="sxs-lookup"><span data-stu-id="f4089-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="f4089-177">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-177">✔</span></span> |<span data-ttu-id="f4089-178">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-178">✔</span></span> |<span data-ttu-id="f4089-179">Linux</span><span class="sxs-lookup"><span data-stu-id="f4089-179">Linux</span></span> |<span data-ttu-id="f4089-180">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f4089-181">Curl</span><span class="sxs-lookup"><span data-stu-id="f4089-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="f4089-182">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-182">✔</span></span> |<span data-ttu-id="f4089-183">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-183">Linux or Windows</span></span> |<span data-ttu-id="f4089-184">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f4089-185">Hadoop용 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f4089-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="f4089-186">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-186">✔</span></span> |<span data-ttu-id="f4089-187">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-187">Linux or Windows</span></span> |<span data-ttu-id="f4089-188">Windows(당분간)</span><span class="sxs-lookup"><span data-stu-id="f4089-188">Windows (for now)</span></span> |
| [<span data-ttu-id="f4089-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4089-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="f4089-190">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-190">✔</span></span> |<span data-ttu-id="f4089-191">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-191">Linux or Windows</span></span> |<span data-ttu-id="f4089-192">Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-192">Windows</span></span> |
| <span data-ttu-id="f4089-193">[원격 데스크톱](hdinsight-hadoop-use-pig-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="f4089-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="f4089-194">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-194">✔</span></span> |<span data-ttu-id="f4089-195">✔</span><span class="sxs-lookup"><span data-stu-id="f4089-195">✔</span></span> |<span data-ttu-id="f4089-196">Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-196">Windows</span></span> |<span data-ttu-id="f4089-197">Windows</span><span class="sxs-lookup"><span data-stu-id="f4089-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f4089-198">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f4089-199">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4089-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="f4089-200">Pig 및 SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="f4089-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="f4089-201">SSIS(SQL Server Integration Services)를 사용하여 Pig 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="f4089-202">Azure Feature Pack for SSIS는 HDInsight에서 Pig 작업을 하는 다음 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="f4089-203">[Azure HDInsight Pig 작업][pigtask]</span><span class="sxs-lookup"><span data-stu-id="f4089-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="f4089-204">[Azure 구독 연결 관리자][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="f4089-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="f4089-205">[여기][ssispack]에서 Azure Feature Pack for SSIS에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f4089-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="f4089-206"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4089-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f4089-207">Scalding을 사용하여 HDInsight와 함께 Pig를 사용하는 방법을 살펴보았으므로 이제 다음 링크를 사용하여 Azure HDInsight로 작업하는 다른 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="f4089-208">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="f4089-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="f4089-209">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f4089-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="f4089-210">HDInsight에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="f4089-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="f4089-211">HDInsight에서 Oozie 사용</span><span class="sxs-lookup"><span data-stu-id="f4089-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="f4089-212">[HDInsight에서 MapReduce 작업 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f4089-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
