---
title: "HDInsight의 Hadoop Pig aaaUse | Microsoft Docs"
description: "자세한 내용은 HDInsight에서 Hadoop으로 toouse Pig 하는 방법입니다."
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
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="6945e-103">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="6945e-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="6945e-104">자세한 내용은 방법 toouse [Apache Pig](http://pig.apache.org/) HDInsight와 중...</span><span class="sxs-lookup"><span data-stu-id="6945e-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="6945e-105">Pig는 *Pig Latin*이라는 절차형 언어를 사용하여 Hadoop용 프로그램을 생성하기 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="6945e-106">Pig 되는 대체 tooJava 작성용 *MapReduce* 솔루션, 되며 Azure HDInsight에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="6945e-107">다음 테이블 toodiscover hello 다양 한 방법으로 Pig HDInsight와 사용할 수 있도록 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="6945e-108">**이것을 사용** 하세요...</span><span class="sxs-lookup"><span data-stu-id="6945e-108">**Use this** if you want...</span></span> | <span data-ttu-id="6945e-109">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="6945e-109">...an **interactive** shell</span></span> | <span data-ttu-id="6945e-110">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="6945e-110">...**batch** processing</span></span> | <span data-ttu-id="6945e-111">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="6945e-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="6945e-112">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="6945e-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6945e-113">SSH</span><span class="sxs-lookup"><span data-stu-id="6945e-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="6945e-114">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-114">✔</span></span> |<span data-ttu-id="6945e-115">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-115">✔</span></span> |<span data-ttu-id="6945e-116">Linux</span><span class="sxs-lookup"><span data-stu-id="6945e-116">Linux</span></span> |<span data-ttu-id="6945e-117">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6945e-118">REST API</span><span class="sxs-lookup"><span data-stu-id="6945e-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="6945e-119">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-119">✔</span></span> |<span data-ttu-id="6945e-120">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-120">Linux or Windows</span></span> |<span data-ttu-id="6945e-121">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6945e-122">Hadoop용 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6945e-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="6945e-123">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-123">✔</span></span> |<span data-ttu-id="6945e-124">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-124">Linux or Windows</span></span> |<span data-ttu-id="6945e-125">Windows(당분간)</span><span class="sxs-lookup"><span data-stu-id="6945e-125">Windows (for now)</span></span> |
| [<span data-ttu-id="6945e-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6945e-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="6945e-127">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-127">✔</span></span> |<span data-ttu-id="6945e-128">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-128">Linux or Windows</span></span> |<span data-ttu-id="6945e-129">Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-129">Windows</span></span> |
| <span data-ttu-id="6945e-130">[원격 데스크톱](hdinsight-hadoop-use-pig-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="6945e-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6945e-131">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-131">✔</span></span> |<span data-ttu-id="6945e-132">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-132">✔</span></span> |<span data-ttu-id="6945e-133">Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-133">Windows</span></span> |<span data-ttu-id="6945e-134">Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6945e-135">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6945e-136">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6945e-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6945e-137"><a id="why"></a>Pig를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="6945e-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="6945e-138">Hadoop MapReduce을 사용 하 여 데이터 처리의 hello 과제 중 하나은 지도 및 reduce 함수를 사용 하 여 처리 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="6945e-139">있습니다 종종 복잡 한 처리에 대 한 함께 tooachieve hello 원하는 결과 여러 개의 MapReduce 작업으로 처리 toobreak 연결.</span><span class="sxs-lookup"><span data-stu-id="6945e-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="6945e-140">Pig 처리를 일련의 hello tooproduce hello 원하는 출력을 통해 데이터 흐름 변환 toodefine가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="6945e-141">hello Pig 라틴 문자 언어 있습니다 toodescribe hello에서에서 데이터 흐름 tooproduce hello 원하는 출력 하나 이상의 변형을 통해 원시 입력을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="6945e-142">Pig Latin 프로그램이 일반적인 패턴을 따릅니다:</span><span class="sxs-lookup"><span data-stu-id="6945e-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="6945e-143">**부하**: hello 파일 시스템에서 조작 하는 데이터 toobe 읽기</span><span class="sxs-lookup"><span data-stu-id="6945e-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="6945e-144">**변환**: hello 데이터 조작</span><span class="sxs-lookup"><span data-stu-id="6945e-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="6945e-145">**덤프 또는 저장**: 데이터 toohello 화면 출력 또는 처리를 위해 저장</span><span class="sxs-lookup"><span data-stu-id="6945e-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="6945e-146">사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="6945e-146">User-defined functions</span></span>

<span data-ttu-id="6945e-147">Pig 라틴 사용자 정의 함수 (UDF) 수 있는 지원 하기 어려운 toomodel Pig 라틴 문자에는 논리를 구현 하는 tooinvoke 외부 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="6945e-148">Pig Latin에 대한 자세한 내용은 [Pig Latin 참조 설명서 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) 및 [Pig Latin 참조 설명서 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6945e-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="6945e-149">Udf를 사용 하 여 Pig 사용의 예를 들어 hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6945e-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="6945e-150">[HDInsight에서 HDInsight와 함께 Pig 사용](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu는 Apache에서 유지 관리하는 유용한 UDF의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="6945e-151">HDInsight에서 Pig 및 Hive와 함께 Python 사용</span><span class="sxs-lookup"><span data-stu-id="6945e-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="6945e-152">HDInsight에서 Hive 및 Pig와 함께 C# 사용</span><span class="sxs-lookup"><span data-stu-id="6945e-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="6945e-153"><a id="data"></a>예제 데이터</span><span class="sxs-lookup"><span data-stu-id="6945e-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="6945e-154">HDInsight hello에 저장 되는 다양 한 예제 데이터 집합을 제공 `/example/data` 및 `/HdiSamples` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="6945e-155">클러스터에 대 한 hello 기본 저장소에이 디렉터리는.</span><span class="sxs-lookup"><span data-stu-id="6945e-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="6945e-156">이 문서에 hello Pig 예제 hello를 사용 하 여 *log4j* 에서 파일을 `/example/data/sample.log`합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="6945e-157">Hello 파일 내의 각 로그를 포함 하는 필드의 줄으로 구성 됩니다는 `[LOG LEVEL]` tooshow hello 유형 및 hello 심각도 예를 들어 필드:</span><span class="sxs-lookup"><span data-stu-id="6945e-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="6945e-158">Hello 이전 예에서 hello 로그 수준에는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="6945e-159">Hello를 사용 하 여 log4j 파일을 생성할 수도 있습니다 [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) 도구 로깅 및 다음 해당 파일 tooyour blob을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="6945e-160">참조 [데이터 업로드 tooHDInsight](hdinsight-upload-data.md) 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="6945e-161">HDInsight와 함께 Azure Blob 저장소를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6945e-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="6945e-162"><a id="job"></a>예제 작업</span><span class="sxs-lookup"><span data-stu-id="6945e-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="6945e-163">hello Pig 라틴 작업 로드 hello `sample.log` HDInsight 클러스터에 대 한 hello 기본 저장소 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="6945e-164">그런 다음 일련의 여러 번 각 로그 수준에서 오류가 발생 했습니다 hello 입력된 데이터는 방법의 수에 발생 하는 변환 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="6945e-165">hello 결과가 tooSTDOUT 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="6945e-166">hello 다음 그림에서는 각 변환을 수행 toohello 데이터에 대 한 요약</span><span class="sxs-lookup"><span data-stu-id="6945e-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Hello 변환의 그래픽 표현][image-hdi-pig-data-transformation]

## <span data-ttu-id="6945e-168"><a id="run"></a>Hello Pig 라틴 작업 실행</span><span class="sxs-lookup"><span data-stu-id="6945e-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="6945e-169">HDInsight는 다양한 메서드를 사용하여 Pig Latin 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="6945e-170">어느 방법이 적합 한, 테이블 toodecide 다음 hello를 사용 하 여 다음 연습은 hello 링크를 따라 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="6945e-171">**이것을 사용** 하세요...</span><span class="sxs-lookup"><span data-stu-id="6945e-171">**Use this** if you want...</span></span> | <span data-ttu-id="6945e-172">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="6945e-172">...an **interactive** shell</span></span> | <span data-ttu-id="6945e-173">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="6945e-173">...**batch** processing</span></span> | <span data-ttu-id="6945e-174">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="6945e-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="6945e-175">...**클라이언트**</span><span class="sxs-lookup"><span data-stu-id="6945e-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6945e-176">SSH</span><span class="sxs-lookup"><span data-stu-id="6945e-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="6945e-177">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-177">✔</span></span> |<span data-ttu-id="6945e-178">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-178">✔</span></span> |<span data-ttu-id="6945e-179">Linux</span><span class="sxs-lookup"><span data-stu-id="6945e-179">Linux</span></span> |<span data-ttu-id="6945e-180">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6945e-181">Curl</span><span class="sxs-lookup"><span data-stu-id="6945e-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="6945e-182">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-182">✔</span></span> |<span data-ttu-id="6945e-183">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-183">Linux or Windows</span></span> |<span data-ttu-id="6945e-184">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6945e-185">Hadoop용 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6945e-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="6945e-186">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-186">✔</span></span> |<span data-ttu-id="6945e-187">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-187">Linux or Windows</span></span> |<span data-ttu-id="6945e-188">Windows(당분간)</span><span class="sxs-lookup"><span data-stu-id="6945e-188">Windows (for now)</span></span> |
| [<span data-ttu-id="6945e-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6945e-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="6945e-190">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-190">✔</span></span> |<span data-ttu-id="6945e-191">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-191">Linux or Windows</span></span> |<span data-ttu-id="6945e-192">Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-192">Windows</span></span> |
| <span data-ttu-id="6945e-193">[원격 데스크톱](hdinsight-hadoop-use-pig-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="6945e-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6945e-194">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-194">✔</span></span> |<span data-ttu-id="6945e-195">✔</span><span class="sxs-lookup"><span data-stu-id="6945e-195">✔</span></span> |<span data-ttu-id="6945e-196">Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-196">Windows</span></span> |<span data-ttu-id="6945e-197">Windows</span><span class="sxs-lookup"><span data-stu-id="6945e-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6945e-198">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6945e-199">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6945e-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="6945e-200">Pig 및 SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="6945e-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="6945e-201">SQL Server Integration Services (SSIS) toorun Pig 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="6945e-202">SSIS 용 Azure 기능 팩 hello 다음과 같은 구성 요소가에 HDInsight Pig 작업을 사용 하는 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="6945e-203">[Azure HDInsight Pig 작업][pigtask]</span><span class="sxs-lookup"><span data-stu-id="6945e-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="6945e-204">[Azure 구독 연결 관리자][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="6945e-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="6945e-205">자세한 정보 hello Azure 기능 팩에 대 한 SSIS [여기][ssispack]합니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="6945e-206"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="6945e-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="6945e-207">이제는 어떻게 toouse HDInsight 사용 하 여 hello 뒤와 Pig 링크 tooexplore Azure HDInsight와 다른 방법으로 toowork 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6945e-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="6945e-208">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="6945e-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="6945e-209">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6945e-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="6945e-210">HDInsight에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="6945e-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="6945e-211">HDInsight에서 Oozie 사용</span><span class="sxs-lookup"><span data-stu-id="6945e-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="6945e-212">[HDInsight에서 MapReduce 작업 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6945e-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
