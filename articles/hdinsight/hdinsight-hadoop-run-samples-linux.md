---
title: "HDInsight에서 Hadoop MapReduce 예제 실행 - Azure | Microsoft Docs"
description: "HDInsight에 포함된 jar 파일의 MapReduce 샘플을 사용하여 시작하세요. SSH를 통해 클러스터에 연결한 다음 Hadoop 명령을 사용하여 샘플 작업을 실행합니다."
keywords: "hadoop 예제 jar,hadoop 예제 jar,hadoop mapreduce 예제,mapreduce 예제"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="04ff9-105">HDInsight에 포함된 MapReduce 예제 실행</span><span class="sxs-lookup"><span data-stu-id="04ff9-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="04ff9-106">HDInsight의 Hadoop에 포함된 MapReduce 예제를 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04ff9-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="04ff9-107">Prerequisites</span></span>

* <span data-ttu-id="04ff9-108">**HDInsight 클러스터**: [Linux HDInsight에서 Hive와 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ff9-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="04ff9-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="04ff9-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ff9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="04ff9-111">**SSH 클라이언트**: 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ff9-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="04ff9-112">MapReduce 예제</span><span class="sxs-lookup"><span data-stu-id="04ff9-112">The MapReduce examples</span></span>

<span data-ttu-id="04ff9-113">**위치**: 샘플은 HDInsight 클러스터의 `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="04ff9-114">**내용**: 이 보관 파일에는 다음 샘플이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="04ff9-115">`aggregatewordcount`: 입력 파일의 단어 수를 계산하는 집계 기반 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="04ff9-116">`aggregatewordhist`: 입력 파일의 단어 히스토그램을 계산하는 집계 기반 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="04ff9-117">`bbp`: Bailey-Borwein-Plouffe를 사용하여 Pi의 정확한 숫자를 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="04ff9-118">`dbcount`: 데이터베이스에 저장된 페이지 보기 로그를 계산하는 예제 작업</span><span class="sxs-lookup"><span data-stu-id="04ff9-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="04ff9-119">`distbbp`: BBP 형식의 수식을 사용하여 Pi의 정확한 비트를 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="04ff9-120">`grep`: 입력에서 정규식과 일치하는 항목 수를 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="04ff9-121">`join`: 정렬되고 동일하게 분할된 데이터 집합을 통해 조인을 수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="04ff9-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="04ff9-122">`multifilewc`: 여러 파일의 단어 수를 계산하는 작업</span><span class="sxs-lookup"><span data-stu-id="04ff9-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="04ff9-123">`pentomino`: pentomino 문제에 대한 해결 방법을 찾는 mapreduce 타일 배치 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="04ff9-124">`pi`: 준난수 몬테카를로 방법을 사용하여 Pi를 추정하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="04ff9-125">`randomtextwriter`: 노드당 10GB의 임의 텍스트 데이터를 기록하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="04ff9-126">`randomwriter`: 노드당 10GB의 임의 데이터를 기록하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="04ff9-127">`secondarysort`: reduce 단계에 대한 보조 정렬을 정의하는 예제</span><span class="sxs-lookup"><span data-stu-id="04ff9-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="04ff9-128">`sort`: 임의 기록기에서 기록한 데이터를 정렬하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="04ff9-129">`sudoku`: sudoku 해 찾기</span><span class="sxs-lookup"><span data-stu-id="04ff9-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="04ff9-130">`teragen`: terasort에 대한 데이터 생성</span><span class="sxs-lookup"><span data-stu-id="04ff9-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="04ff9-131">`terasort`: terasort 실행</span><span class="sxs-lookup"><span data-stu-id="04ff9-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="04ff9-132">`teravalidate`: terasort 결과 확인</span><span class="sxs-lookup"><span data-stu-id="04ff9-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="04ff9-133">`wordcount`: 입력 파일의 단어 수를 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="04ff9-134">`wordmean`: 입력 파일의 단어 길이에 대한 평균값을 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="04ff9-135">`wordmedian`: 입력 파일의 단어 길이에 대한 중앙값을 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="04ff9-136">`wordstandarddeviation`: 입력 파일의 단어 길이에 대한 표준 편차를 계산하는 mapreduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="04ff9-137">**소스 코드**: 이러한 샘플의 소스 코드는 HDInsight 클러스터의 `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="04ff9-138">경로의 `2.2.4.9-1`은 HDInsight 클러스터용 Hortonworks Data Platform의 버전이며 클러스터에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="04ff9-139">wordcount 예제 실행</span><span class="sxs-lookup"><span data-stu-id="04ff9-139">Run the wordcount example</span></span>

1. <span data-ttu-id="04ff9-140">SSH를 사용하여 HDInsight에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="04ff9-141">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ff9-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="04ff9-142">`username@#######:~$` 프롬프트에서 다음 명령을 사용하여 샘플을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="04ff9-143">이 명령은 이 문서의 이전 섹션에 나와 있는 샘플 목록을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="04ff9-144">특정 샘플에 대한 도움말을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="04ff9-145">이 명령은 **wordcount** 샘플에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="04ff9-146">다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="04ff9-147">이 메시지는 원본 문서에 대해 여러 입력 경로를 제공할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="04ff9-148">최종 경로는 출력(원본 문서의 단어 수)이 저장되는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="04ff9-149">다음을 사용하여 클러스터와 함께 샘플 데이터로 제공되는 Notebooks of Leonardo Da Vinci의 모든 단어 수를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="04ff9-150">이 작업에 대한 입력은 `/example/data/gutenberg/davinci.txt`에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="04ff9-151">이 예제의 출력은 `/example/data/davinciwordcount`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="04ff9-152">두 경로는 모두 로컬 파일 시스템이 아니라 클러스터의 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04ff9-153">Wordcount 샘플에 대한 도움말에서 설명했듯이 여러 입력 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="04ff9-154">예를 들어 `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` 는 davinci.txt와 ulysses.txt 모두에서 단어 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="04ff9-155">작업이 완료되면 다음 명령을 사용하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="04ff9-156">이 명령은 작업에서 생성된 모든 출력 파일을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="04ff9-157">콘솔에 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-157">It displays the output to the console.</span></span> <span data-ttu-id="04ff9-158">다음 텍스트와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="04ff9-159">각 줄은 단어와 해당 단어가 입력 데이터에서 발생한 횟수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="04ff9-160">Sudoku 예제</span><span class="sxs-lookup"><span data-stu-id="04ff9-160">The Sudoku example</span></span>

<span data-ttu-id="04ff9-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) 는 9개의 3x3 표로 구성된 논리 퍼즐입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="04ff9-162">표의 일부 셀에는 숫자가 있고 다른 셀은 비어 있으며, 빈 셀을 해결하는 것이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="04ff9-163">이전 링크에는 퍼즐에 대한 자세한 정보가 있지만, 이 샘플의 목적은 빈 셀을 해결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="04ff9-164">따라서 입력은 다음과 같은 형식의 파일이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="04ff9-165">9개 열의 9개 행</span><span class="sxs-lookup"><span data-stu-id="04ff9-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="04ff9-166">각 열은 숫자 또는 `?` (빈 셀을 나타냄)를 포함할 수 있음</span><span class="sxs-lookup"><span data-stu-id="04ff9-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="04ff9-167">셀은 공백으로 구분됨</span><span class="sxs-lookup"><span data-stu-id="04ff9-167">Cells are separated by a space</span></span>

<span data-ttu-id="04ff9-168">열이나 행에서 숫자를 반복할 수 없다는 Sudoku 퍼즐을 작성하는 특정 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="04ff9-169">적절히 구성된 HDInsight 클러스터에 대한 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="04ff9-170">이 예제는 `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta`에 있으며 다음 텍스트를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="04ff9-171">이 예제 문제를 Sudoku 예제를 통해 실행하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="04ff9-172">결과는 다음 텍스트와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="04ff9-173">Pi(π) 예제</span><span class="sxs-lookup"><span data-stu-id="04ff9-173">Pi (π) example</span></span>

<span data-ttu-id="04ff9-174">Pi 샘플에서는 통계(준난수 몬테카를로) 방법을 사용하여 Pi 값을 추정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="04ff9-175">점은 단위 정사각형 내에 임의로 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="04ff9-176">정사각형에는 원도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-176">The square also contains a circle.</span></span> <span data-ttu-id="04ff9-177">점이 원 안에 들어올 확률은 원의 영역인 pi/4와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="04ff9-178">Pi의 값은 4R의 값에서 추정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="04ff9-179">R은 정사각형 내에 있는 점의 총수에 대한 원 내부에 있는 점 개수의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="04ff9-180">사용한 점 샘플이 크면 클수록 추정이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="04ff9-181">다음 명령을 사용하여 이 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-181">Use the following command to run this sample.</span></span> <span data-ttu-id="04ff9-182">이 명령은 각각 10,000,000개의 샘플이 있는 16개의 맵을 사용하여 pi 값을 추정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="04ff9-183">이 명령에서 반환되는 값은 **3.14159155000000000000**과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="04ff9-184">참고로, Pi의 소수점 이하 10자리는 3.1415926535입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="04ff9-185">10GB Greysort 예제</span><span class="sxs-lookup"><span data-stu-id="04ff9-185">10 GB Greysort example</span></span>

<span data-ttu-id="04ff9-186">GraySort는 벤치마크 정렬입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="04ff9-187">이 메트릭은 엄청난 양, 일반적으로 최소 100TB의 데이터를 정렬하는 동안 도달하는 정렬 속도(TB/분)입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="04ff9-188">이 샘플에서는 비교적 빠르게 실행할 수 있도록 적절한 10GB의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="04ff9-189">Owen O'Malley와 Arun Murthy가 개발한 MapReduce 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="04ff9-190">이 응용 프로그램은 0.578TB/분(100TB 정렬에 173분 소요)의 속도로, 2009년 연간 범용("daytona") 테라바이트 정렬 벤치마크로 선정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="04ff9-191">이 정렬 벤치마크 및 다른 정렬 벤치마크에 대한 자세한 내용은 [정렬 벤치마크](http://sortbenchmark.org/) (영문) 사이트를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="04ff9-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="04ff9-192">이 샘플에서는 세 가지 집합의 MapReduce 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="04ff9-193">**TeraGen**: 정렬할 데이터의 행을 생성하는 MapReduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="04ff9-194">**TeraSort**: 입력 데이터를 샘플링하고 MapReduce를 사용하여 데이터를 전체 순서로 정렬</span><span class="sxs-lookup"><span data-stu-id="04ff9-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="04ff9-195">TeraSort는 사용자 지정 파티셔너를 제외하고 표준 MapReduce 정렬입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="04ff9-196">파티셔너는 각 reduce의 키 범위를 정의하는 N-1 샘플 키의 정렬된 목록을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="04ff9-197">특히, sample[i-1] <= key < sample[i]와 같은 모든 키는 reduce i로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="04ff9-198">이 파티셔너는 reduce i의 출력이 모두 reduce i+1의 출력보다 작도록 보증합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="04ff9-199">**TeraValidate**: 출력이 전역으로 정렬되는지 확인하는 MapReduce 프로그램</span><span class="sxs-lookup"><span data-stu-id="04ff9-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="04ff9-200">이 프로그램은 출력 디렉터리에 파일당 하나의 맵을 만들며 각 맵에서 각 키가 이전 키보다 작거나 같은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="04ff9-201">map 함수는 각 파일의 첫 번째 키와 마지막 키의 레코드를 생성하며,</span><span class="sxs-lookup"><span data-stu-id="04ff9-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="04ff9-202">reduce 함수는 i 파일의 첫 번째 키가 i-1 파일의 마지막 키보다 큰지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="04ff9-203">모든 문제가 뒤바뀐 순서의 키와 함께 reduce 단계의 출력으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="04ff9-204">데이터를 생성하고 정렬한 다음 출력의 유효성을 검사하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="04ff9-205">`/example/data/10GB-sort-input`에 있는 HDInsight 클러스터의 기본 저장소에 저장되는 10GB의 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="04ff9-206">`-Dmapred.map.tasks` 는 이 작업에 사용할 map 작업 수를 Hadoop에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="04ff9-207">마지막 두 매개 변수는 10GB의 데이터를 만들어 `/example/data/10GB-sort-input`에 저장하도록 작업에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="04ff9-208">다음 명령을 사용하여 데이터를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="04ff9-209">`-Dmapred.reduce.tasks` 는 작업에 사용할 reduce 작업 수를 Hadoop에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="04ff9-210">마지막 두 매개 변수는 데이터의 입력 및 출력 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="04ff9-211">다음을 사용하여 정렬에 의해 생성된 데이터의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="04ff9-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04ff9-212">Next steps</span></span>

<span data-ttu-id="04ff9-213">이 문서에서는 Linux 기반 HDInsight 클러스터에 포함된 샘플을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="04ff9-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="04ff9-214">HDInsight에서 Pig, Hive 및 MapReduce를 사용하는 방법에 대한 자습서는 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ff9-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="04ff9-215">[HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="04ff9-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="04ff9-216">[HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="04ff9-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="04ff9-217">[HDInsight에서 Hadoop과 MapReduce 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="04ff9-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
