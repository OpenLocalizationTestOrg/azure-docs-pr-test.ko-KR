---
title: "HDInsight에서 Hadoop으로 aaaMapReduce | Microsoft Docs"
description: "HDInsight 클러스터의 MapReduce toorun Hadoop에서 작업 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="385f8-103">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="385f8-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="385f8-104">HDInsight 클러스터에서 toorun MapReduce 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="385f8-105">다음 테이블 toodiscover hello MapReduce HDInsight와 사용할 수 있도록 하는 다양 한 방법으로 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="385f8-106">**사용 기능**...</span><span class="sxs-lookup"><span data-stu-id="385f8-106">**Use this**...</span></span> | <span data-ttu-id="385f8-107">**...toodo가**</span><span class="sxs-lookup"><span data-stu-id="385f8-107">**...toodo this**</span></span> | <span data-ttu-id="385f8-108">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="385f8-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="385f8-109">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="385f8-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="385f8-110">SSH</span><span class="sxs-lookup"><span data-stu-id="385f8-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="385f8-111">통해 hello Hadoop 명령을 사용 하 여 **SSH**</span><span class="sxs-lookup"><span data-stu-id="385f8-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="385f8-112">Linux</span><span class="sxs-lookup"><span data-stu-id="385f8-112">Linux</span></span> |<span data-ttu-id="385f8-113">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="385f8-114">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="385f8-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="385f8-115">사용 하 여 hello 작업을 원격으로 제출 **REST** (예제 cURL를 사용 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="385f8-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="385f8-116">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-116">Linux or Windows</span></span> |<span data-ttu-id="385f8-117">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="385f8-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="385f8-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="385f8-119">사용 하 여 hello 작업을 원격으로 제출 **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="385f8-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="385f8-120">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-120">Linux or Windows</span></span> |<span data-ttu-id="385f8-121">Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-121">Windows</span></span> |
| <span data-ttu-id="385f8-122">[원격 데스크톱](hdinsight-hadoop-use-mapreduce-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="385f8-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="385f8-123">통해 hello Hadoop 명령을 사용 하 여 **원격 데스크톱**</span><span class="sxs-lookup"><span data-stu-id="385f8-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="385f8-124">Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-124">Windows</span></span> |<span data-ttu-id="385f8-125">Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="385f8-126">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="385f8-127">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="385f8-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="385f8-128"><a id="whatis"></a>MapReduce란</span><span class="sxs-lookup"><span data-stu-id="385f8-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="385f8-129">Hadoop MapReduce는 방대한 양의 데이터를 처리하는 작업을 작성하기 위한 소프트웨어 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="385f8-130">입력된 데이터는 다음 클러스터의 hello 노드에서 동시에 처리 되는 독립 청크로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="385f8-131">MapReduce 작업은 두 함수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="385f8-132">**매퍼**: 입력된 데이터를 소비하고 분석하며(일반적으로 필터 및 정렬 작업) 튜플을 내보냅니다.(키-값 쌍)</span><span class="sxs-lookup"><span data-stu-id="385f8-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="385f8-133">**리 듀 서**: hello 맵 편집기에서 내보낸 된 튜플을 소비 하 고 더 작은, 결합 된 결과 hello 매퍼 데이터 로부터 만드는 요약 연산을 수행</span><span class="sxs-lookup"><span data-stu-id="385f8-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="385f8-134">기본적인 word count MapReduce 작업 예제는 hello 다음 다이어그램에서에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="385f8-136">이 작업의 hello 출력은 각 단어 hello 텍스트 분석 된에서 발생 했습니다. 몇 번의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="385f8-137">hello 매퍼 각 줄을 입력으로 hello 입력된 텍스트에서 걸리며 단어로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="385f8-138">내보낸 키/값 쌍 단어 나올 때마다 hello 단어의 뒤에 1입니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="385f8-139">hello 출력이 tooreducer 보내기 전에 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="385f8-140">hello 리 듀 서 각 단어에 대 한 이러한 개별 수의 합계를 계산 하 고 hello 단어 하나 다음에 발생 빈도의 hello 합계를 포함 하는 단일 키/값 쌍을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="385f8-141">MapReduce는 다양한 언어로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="385f8-142">Java는 hello 가장 일반적인 구현 하며이 문서의 설명을 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="385f8-143">개발 언어</span><span class="sxs-lookup"><span data-stu-id="385f8-143">Development languages</span></span>

<span data-ttu-id="385f8-144">언어 또는 hello Java 가상 컴퓨터 및 Java를 기반으로 하는 프레임 워크는 MapReduce 작업으로 직접 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="385f8-145">이 문서에 사용 되는 hello 예제는 MapReduce Java 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="385f8-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="385f8-146">C#, Python, 독립 실행형 실행 파일 등의 비-Java 언어는 Hadoop 스트리밍을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="385f8-147">Hadoop 스트리밍 STDIN 및 STDOUT hello 매퍼 및 리 듀 서와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="385f8-148">hello 매퍼 및 리 듀 서 데이터 줄에서 STDIN 한 번에 읽고 hello 출력 tooSTDOUT 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="385f8-149">각 줄 읽기 또는 hello 매퍼 및 리 듀 서에서 내보낸 탭 문자로 구분 된 키/값 쌍의 hello 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="385f8-150">자세한 내용은 [Hadoop 스트리밍](http://hadoop.apache.org/docs/r1.2.1/streaming.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="385f8-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="385f8-151">Hadoop 스트리밍 HDInsight를 사용 하 여의 예 hello 다음 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="385f8-152">C# MapReduce 작업 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="385f8-153">Python MapReduce 작업 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="385f8-154"><a id="data"></a>예제 데이터</span><span class="sxs-lookup"><span data-stu-id="385f8-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="385f8-155">HDInsight hello에 저장 되는 다양 한 예제 데이터 집합을 제공 `/example/data` 및 `/HdiSamples` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="385f8-156">클러스터에 대 한 hello 기본 저장소에이 디렉터리는.</span><span class="sxs-lookup"><span data-stu-id="385f8-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="385f8-157">이 문서를 사용 하 여 hello `/example/data/gutenberg/davinci.txt` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="385f8-158">이 파일의 레오나르도 다빈치 hello 전자 필기장 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="385f8-159"><a id="job"></a>예제 MapReduce</span><span class="sxs-lookup"><span data-stu-id="385f8-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="385f8-160">MapReduce 단어 수 세기 응용 프로그램 예가 HDInsight 클러스터에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="385f8-161">이 예제에는 `/example/jars/hadoop-mapreduce-examples.jar` hello 기본 저장소 클러스터에 대해에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="385f8-162">다음 Java 코드는 hello은 hello hello에 포함 된 MapReduce 응용 프로그램의 hello 소스 `hadoop-mapreduce-examples.jar` 파일:</span><span class="sxs-lookup"><span data-stu-id="385f8-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="385f8-163">지침 toowrite MapReduce 응용 프로그램 hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="385f8-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="385f8-164">HDInsight용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="385f8-165">HDInsight용 Python MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="385f8-166"><a id="run"></a>MapReduce hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="385f8-167">HDInsight는 다양한 메서드를 사용하여 HiveQL 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="385f8-168">어느 방법이 적합 한, 테이블 toodecide 다음 hello를 사용 하 여 다음 연습은 hello 링크를 따라 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="385f8-169">**사용 기능**...</span><span class="sxs-lookup"><span data-stu-id="385f8-169">**Use this**...</span></span> | <span data-ttu-id="385f8-170">**...toodo가**</span><span class="sxs-lookup"><span data-stu-id="385f8-170">**...toodo this**</span></span> | <span data-ttu-id="385f8-171">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="385f8-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="385f8-172">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="385f8-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="385f8-173">SSH</span><span class="sxs-lookup"><span data-stu-id="385f8-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="385f8-174">통해 hello Hadoop 명령을 사용 하 여 **SSH**</span><span class="sxs-lookup"><span data-stu-id="385f8-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="385f8-175">Linux</span><span class="sxs-lookup"><span data-stu-id="385f8-175">Linux</span></span> |<span data-ttu-id="385f8-176">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="385f8-177">Curl</span><span class="sxs-lookup"><span data-stu-id="385f8-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="385f8-178">사용 하 여 hello 작업을 원격으로 제출 **REST**</span><span class="sxs-lookup"><span data-stu-id="385f8-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="385f8-179">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-179">Linux or Windows</span></span> |<span data-ttu-id="385f8-180">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="385f8-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="385f8-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="385f8-182">사용 하 여 hello 작업을 원격으로 제출 **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="385f8-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="385f8-183">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-183">Linux or Windows</span></span> |<span data-ttu-id="385f8-184">Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-184">Windows</span></span> |
| <span data-ttu-id="385f8-185">[원격 데스크톱](hdinsight-hadoop-use-mapreduce-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="385f8-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="385f8-186">통해 hello Hadoop 명령을 사용 하 여 **원격 데스크톱**</span><span class="sxs-lookup"><span data-stu-id="385f8-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="385f8-187">Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-187">Windows</span></span> |<span data-ttu-id="385f8-188">Windows</span><span class="sxs-lookup"><span data-stu-id="385f8-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="385f8-189">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="385f8-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="385f8-190">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="385f8-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="385f8-191"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="385f8-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="385f8-192">HDInsight에서 데이터 작업에 대해 자세히 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="385f8-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="385f8-193">HDInsight용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="385f8-194">HDInsight용 Python 스트리밍 MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="385f8-195">HDInsight에서 Apache Hadoop을 사용하여 Scalding MapReduce 작업 개발</span><span class="sxs-lookup"><span data-stu-id="385f8-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="385f8-196">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="385f8-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="385f8-197">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="385f8-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
