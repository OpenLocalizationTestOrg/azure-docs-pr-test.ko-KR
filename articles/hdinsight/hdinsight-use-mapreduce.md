---
title: "HDInsight의 Hadoop 및 MapReduce | Microsoft Docs"
description: "HDInsight 클러스터의 Hadoop에서 MapReduce 작업을 실행하는 방법을 알아봅니다."
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="45a01-103">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="45a01-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="45a01-104">HDInsight 클러스터에서 MapReduce 작업을 실행하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="45a01-105">다음 표를 사용하여 HDInsight에서 MapReduce를 사용하는 다양한 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="45a01-106">**사용 기능**...</span><span class="sxs-lookup"><span data-stu-id="45a01-106">**Use this**...</span></span> | <span data-ttu-id="45a01-107">**...다음을 수행합니다**</span><span class="sxs-lookup"><span data-stu-id="45a01-107">**...to do this**</span></span> | <span data-ttu-id="45a01-108">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="45a01-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="45a01-109">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="45a01-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="45a01-110">SSH</span><span class="sxs-lookup"><span data-stu-id="45a01-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="45a01-111">**SSH**</span><span class="sxs-lookup"><span data-stu-id="45a01-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="45a01-112">Linux</span><span class="sxs-lookup"><span data-stu-id="45a01-112">Linux</span></span> |<span data-ttu-id="45a01-113">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="45a01-114">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="45a01-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="45a01-115">**REST**를 사용하여 작업 원격 제출(예제 용도 cURL)</span><span class="sxs-lookup"><span data-stu-id="45a01-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="45a01-116">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-116">Linux or Windows</span></span> |<span data-ttu-id="45a01-117">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="45a01-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="45a01-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="45a01-119">**Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="45a01-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="45a01-120">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-120">Linux or Windows</span></span> |<span data-ttu-id="45a01-121">Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-121">Windows</span></span> |
| <span data-ttu-id="45a01-122">[원격 데스크톱](hdinsight-hadoop-use-mapreduce-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="45a01-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="45a01-123">**원격 데스크톱**</span><span class="sxs-lookup"><span data-stu-id="45a01-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="45a01-124">Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-124">Windows</span></span> |<span data-ttu-id="45a01-125">Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="45a01-126">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="45a01-127">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="45a01-128"><a id="whatis"></a>MapReduce란</span><span class="sxs-lookup"><span data-stu-id="45a01-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="45a01-129">Hadoop MapReduce는 방대한 양의 데이터를 처리하는 작업을 작성하기 위한 소프트웨어 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="45a01-130">입력된 데이터는 사용자 클러스터의 노드에 걸쳐 동시에 처리되는 독립적인 청크로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="45a01-131">MapReduce 작업은 두 함수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="45a01-132">**매퍼**: 입력된 데이터를 소비하고 분석하며(일반적으로 필터 및 정렬 작업) 튜플을 내보냅니다.(키-값 쌍)</span><span class="sxs-lookup"><span data-stu-id="45a01-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="45a01-133">**리듀서**: 매퍼에서 나온 튜플을 소배하고 매퍼 데이터에서 더 작고 결합된 결과를 생성하는 요약 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="45a01-134">다음 다이어그램에서는 기본 단어 계산 MapReduce 작업 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="45a01-136">이 작업의 출력은 분석된 텍스트에서 각 단어가 발생한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="45a01-137">매퍼는 입력 텍스트의 각 줄을 입력으로 가져오고 해당 줄을 단어로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="45a01-138">단어 뒤에 1이 표시되는 단어가 발생할 때마다 키/값 쌍을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="45a01-139">리듀서로 보내기 전에 출력이 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="45a01-140">리듀서가 각 단어의 개별 발생 수를 합산하고 단어 뒤에 발생 합계가 포함된 단일 키/값 쌍을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="45a01-141">MapReduce는 다양한 언어로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="45a01-142">Java는 가장 일반적인 구현으로 해당 문서의 데모 용도로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="45a01-143">개발 언어</span><span class="sxs-lookup"><span data-stu-id="45a01-143">Development languages</span></span>

<span data-ttu-id="45a01-144">Java 및 Java 가상 컴퓨터를 기반으로 하는 언어 또는 프레임워크는 MapReduce 작업으로 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="45a01-145">이 문서에서 사용된 예는 Java MapReduce 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="45a01-146">C#, Python, 독립 실행형 실행 파일 등의 비-Java 언어는 Hadoop 스트리밍을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="45a01-147">Hadoop 스트리밍은 STDIN 및 STDOUT을 통해 매퍼 및 리듀서와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="45a01-148">매퍼와 리듀서는 STDIN에서 한 번에 한 줄씩 데이터를 읽고 STDOUT에 출력을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="45a01-149">매퍼 및 리듀서가 읽거나 내보낸 각 줄은 탭 문자로 구분된 키/값 쌍의 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="45a01-150">자세한 내용은 [Hadoop 스트리밍](http://hadoop.apache.org/docs/r1.2.1/streaming.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="45a01-151">HDInsight에서 Hadoop 스트리밍을 사용하는 예를 보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="45a01-152">C# MapReduce 작업 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="45a01-153">Python MapReduce 작업 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="45a01-154"><a id="data"></a>예제 데이터</span><span class="sxs-lookup"><span data-stu-id="45a01-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="45a01-155">HDInsight는 `/example/data` 및 `/HdiSamples` 디렉터리에 저장되는 다양한 예제 데이터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="45a01-156">이러한 디렉터리는 클러스터의 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="45a01-157">이 문서에서는 `/example/data/gutenberg/davinci.txt` 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="45a01-158">이 파일에는 레오나르도 다빈치의 메모장이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="45a01-159"><a id="job"></a>예제 MapReduce</span><span class="sxs-lookup"><span data-stu-id="45a01-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="45a01-160">MapReduce 단어 수 세기 응용 프로그램 예가 HDInsight 클러스터에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="45a01-161">이 예제는 클러스터의 기본 저장소인 `/example/jars/hadoop-mapreduce-examples.jar`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="45a01-162">다음 Java 코드는 `hadoop-mapreduce-examples.jar` 파일에 포함된 MapReduce 응용 프로그램의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="45a01-163">고유한 MapReduce 응용 프로그램을 쓰는 지침은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="45a01-164">HDInsight용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="45a01-165">HDInsight용 Python MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="45a01-166"><a id="run"></a>MapReduce 실행</span><span class="sxs-lookup"><span data-stu-id="45a01-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="45a01-167">HDInsight는 다양한 메서드를 사용하여 HiveQL 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="45a01-168">어떤 메서드가 적합한지 결정하는 다음 테이블을 사용하여 연습할 수 있는 링크를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="45a01-169">**사용 기능**...</span><span class="sxs-lookup"><span data-stu-id="45a01-169">**Use this**...</span></span> | <span data-ttu-id="45a01-170">**...다음을 수행합니다**</span><span class="sxs-lookup"><span data-stu-id="45a01-170">**...to do this**</span></span> | <span data-ttu-id="45a01-171">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="45a01-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="45a01-172">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="45a01-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="45a01-173">SSH</span><span class="sxs-lookup"><span data-stu-id="45a01-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="45a01-174">**SSH**</span><span class="sxs-lookup"><span data-stu-id="45a01-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="45a01-175">Linux</span><span class="sxs-lookup"><span data-stu-id="45a01-175">Linux</span></span> |<span data-ttu-id="45a01-176">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="45a01-177">Curl</span><span class="sxs-lookup"><span data-stu-id="45a01-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="45a01-178">**REST**</span><span class="sxs-lookup"><span data-stu-id="45a01-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="45a01-179">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-179">Linux or Windows</span></span> |<span data-ttu-id="45a01-180">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="45a01-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="45a01-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="45a01-182">**Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="45a01-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="45a01-183">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-183">Linux or Windows</span></span> |<span data-ttu-id="45a01-184">Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-184">Windows</span></span> |
| <span data-ttu-id="45a01-185">[원격 데스크톱](hdinsight-hadoop-use-mapreduce-remote-desktop.md)(HDInsight 3.2 및 3.3)</span><span class="sxs-lookup"><span data-stu-id="45a01-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="45a01-186">**원격 데스크톱**</span><span class="sxs-lookup"><span data-stu-id="45a01-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="45a01-187">Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-187">Windows</span></span> |<span data-ttu-id="45a01-188">Windows</span><span class="sxs-lookup"><span data-stu-id="45a01-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="45a01-189">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="45a01-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="45a01-190">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="45a01-191"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="45a01-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="45a01-192">HDInsight에서 데이터를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a01-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="45a01-193">HDInsight용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="45a01-194">HDInsight용 Python 스트리밍 MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="45a01-195">HDInsight에서 Apache Hadoop을 사용하여 Scalding MapReduce 작업 개발</span><span class="sxs-lookup"><span data-stu-id="45a01-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="45a01-196">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="45a01-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="45a01-197">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="45a01-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
