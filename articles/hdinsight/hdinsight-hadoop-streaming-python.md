---
title: "HDInsight에서 Python MapReduce 작업 개발 - Azure | Microsoft Docs"
description: "MapReduce 작업을 스트리밍하는 데 Python을 사용하는 방법 알아보기 Hadoop은 Java 이외의 언어로 작성하기 위해 MapReduce용 스트리밍 API를 제공합니다."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="e8525-104">HDInsight용 Python 스트리밍 MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="e8525-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="e8525-105">MapReduce 작업을 스트리밍하는 데 Python을 사용하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="e8525-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="e8525-106">Hadoop은 MapReduce용 스트리밍 API를 제공합니다. 이 API를 사용하여 Java 이외의 언어로 map 및 reduce 함수를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="e8525-107">이 문서의 단계는 맵을 구현하고 Python의 구성 요소를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8525-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e8525-108">Prerequisites</span></span>

* <span data-ttu-id="e8525-109">HDInsight 클러스터의 Linux 기반 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e8525-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e8525-110">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e8525-111">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e8525-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8525-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e8525-113">텍스트 편집기</span><span class="sxs-lookup"><span data-stu-id="e8525-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e8525-114">텍스트 편집기에서 줄 끝으로 LF를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="e8525-115">CRLF의 줄 끝을 사용하는 경우 Linux 기반 HDInsight 클러스터에서 MapReduce 작업을 실행할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="e8525-116">`ssh` 및 `scp` 명령 또는 [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="e8525-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="e8525-117">단어 개수</span><span class="sxs-lookup"><span data-stu-id="e8525-117">Word count</span></span>

<span data-ttu-id="e8525-118">이 예제는 매퍼와 리듀서를 사용하여 python에서 구현된 기본 단어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="e8525-119">mapper는 문장을 개별 단어로 끊고 reducer는 출력하기 위해 단어와 개수를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="e8525-120">다음 순서도는 map 및 reduce 단계가 어떻게 진행되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![mapreduce 프로세스의 그림](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="e8525-122">MapReduce 스트리밍</span><span class="sxs-lookup"><span data-stu-id="e8525-122">Streaming MapReduce</span></span>

<span data-ttu-id="e8525-123">Hadoop을 사용하면 작업에서 사용되는 map 및 reduce 논리를 포함하는 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="e8525-124">map 및 reduce 논리에 대한 특정 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="e8525-125">**입력**: map 및 reduce 구성 요소는 STDIN에서 입력 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="e8525-126">**출력**: map 및 reduce 구성 요소는 STDOUT에 출력 데이터를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="e8525-127">**데이터 형식**: 소비되고 생성되는 데이터는 탭 문자로 구분하는 키/값 쌍이어야 합니다</span><span class="sxs-lookup"><span data-stu-id="e8525-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="e8525-128">Python은 STDIN에서 읽을 수 있는 `sys` 모듈 및 STDOUT에 출력하는 `print`를 사용하여 이러한 요구 사항을 쉽게 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="e8525-129">나머지 작업은 키와 값 사이에 탭(`\t`) 문자를 사용하여 데이터 서식을 지정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="e8525-130">mapper 및 reducer 만들기</span><span class="sxs-lookup"><span data-stu-id="e8525-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="e8525-131">`mapper.py`라는 파일을 만들고 다음 코드를 그 내용으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="e8525-132">**reducer.py**라는 파일을 만들고 다음 코드를 그 내용으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="e8525-133">PowerShell을 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="e8525-133">Run using PowerShell</span></span>

<span data-ttu-id="e8525-134">파일이 올바른 줄 끝을 가지고 있는지 확인하려면 다음 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="e8525-135">[!code-powershell[기본](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="e8525-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="e8525-136">다음 PowerShell 스크립트를 사용하여 파일을 업로드하고 작업을 실행하고 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="e8525-137">[!code-powershell[기본](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="e8525-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="e8525-138">SSH 세션에서 실행</span><span class="sxs-lookup"><span data-stu-id="e8525-138">Run from an SSH session</span></span>

1. <span data-ttu-id="e8525-139">개발 환경의 `mapper.py` 및 `reducer.py` 파일과 동일한 디렉터리에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="e8525-140">`username`은 클러스터의 SSH 사용자 이름으로, `clustername`은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="e8525-141">이 명령은 로컬 시스템에서 헤드 노드로 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e8525-142">SSH 계정을 보호하는 암호를 사용한 경우 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="e8525-143">SSH 키를 사용한 경우 `-i` 매개 변수 및 개인 키에 대한 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="e8525-144">예: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`</span><span class="sxs-lookup"><span data-stu-id="e8525-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="e8525-145">SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="e8525-146">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8525-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="e8525-147">mapper.py 및 reducer.py가 올바른 줄 끝을 가지고 있는지 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="e8525-148">다음 명령을 사용하여 MapReduce 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="e8525-149">다음은 명령어의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-149">This command has the following parts:</span></span>

   * <span data-ttu-id="e8525-150">**hadoop-streaming.jar**: 스트리밍 MapReduce 작업을 수행할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="e8525-151">제공하는 외부 MapReduce 코드로 Hadoop에 접속합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="e8525-152">**-files**: MapReduce 작업에 지정된 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="e8525-153">**-mapper**: Hadoop mapper로 사용될 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="e8525-154">**-reducer**: Hadoop reducer로 사용할 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="e8525-155">**-input**: 단어 수를 계산할 입력 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="e8525-156">**-output**: 출력 내용을 작성할 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="e8525-157">MapReduce 작업이 작동하면 프로세스는 백분율로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="e8525-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="e8525-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="e8525-159">출력을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="e8525-160">이 명령은 단어 목록과 해당 단어가 나타난 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8525-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8525-161">Next steps</span></span>

<span data-ttu-id="e8525-162">HDInsight에서 스트리밍 MapRedcue 작업을 사용하는 방법을 배웠으므로 이제 아래 링크를 사용하여 Azure HDInsight에서 작업하는 다른 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8525-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="e8525-163">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="e8525-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e8525-164">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="e8525-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e8525-165">HDInsight에서 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="e8525-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
