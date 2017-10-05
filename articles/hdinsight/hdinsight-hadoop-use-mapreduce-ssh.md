---
title: "HDInsight에서 Hadoop과 MapReduce 및 SSH 연결 사용 - Azure | Microsoft Docs"
description: "SSH를 사용하여 HDInsight에서 Hadoop으로 MapReduce 작업을 실행하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: eaf6278f97cd5ddd7e049ff4745181f39d7949a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="1f032-103">SSH를 사용하여 HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="1f032-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="1f032-104">SSH(Secure Shell) 연결에서 HDInsight로 MapReduce 작업을 제출하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="1f032-105">이미 익숙한 Linux 기반 Hadoop 서버를 사용하지만 HDInsight는 처음인 경우 [Linux 기반 HDInsight 팁](hdinsight-hadoop-linux-information.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f032-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="1f032-106"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f032-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="1f032-107">Linux 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="1f032-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1f032-108">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1f032-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f032-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1f032-110">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="1f032-110">An SSH client.</span></span> <span data-ttu-id="1f032-111">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f032-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="1f032-112"><a id="ssh"></a>SSH를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="1f032-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="1f032-113">SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="1f032-114">예를 들어 다음 명령은 **myhdinsight**라는 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-114">For example, the following command connects to a cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="1f032-115">**SSH 인증을 위해 인증서 키를 사용하는 경우** 클라이언트 시스템에서 개인 키의 위치를 지정해야 할 수도 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="1f032-116">**SSH 인증을 위해 암호를 사용하는 경우** 메시지가 표시되면 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="1f032-117">HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f032-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="1f032-118"><a id="hadoop"></a>Hadoop 명령 사용</span><span class="sxs-lookup"><span data-stu-id="1f032-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="1f032-119">HDInsight 클러스터에 연결되면 다음 명령을 사용하여 MapReduce 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="1f032-120">이 명령은 `hadoop-mapreduce-examples.jar` 파일에 포함되어 있는 `wordcount` 클래스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="1f032-121">입력으로 `/example/data/gutenberg/davinci.txt` 문서를 사용하고 출력은 `/example/data/WordCountOutput`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f032-122">이 MapReduce 작업 및 예 데이터에 대한 자세한 내용은 [HDInsight Hadoop에서 MapReduce 사용](hdinsight-use-mapreduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f032-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="1f032-123">작업이 처리되는 동안 세부 정보를 내보내며 작업이 완료될 때 다음 텍스트와 유사한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="1f032-124">작업이 완료되면 다음 명령을 사용하여 출력 파일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="1f032-125">이 명령은 `_SUCCESS` 및 `part-r-00000`의 두 개의 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="1f032-126">`part-r-00000` 파일은 이 작업에 대한 출력을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f032-127">일부 MapReduce 작업은 여러 **part-r-#####** 파일로 결과를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="1f032-128">그럴 경우 ##### 접미사가 파일의 순서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="1f032-129">출력을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="1f032-130">이 명령은 **wasb://example/data/gutenberg/davinci.txt** 파일에 포함된 단어의 목록과 각 단어가 나타나는 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="1f032-131">다음 텍스트는 파일에 포함된 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="1f032-132"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="1f032-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="1f032-133">여기에서 볼 수 있듯이 Hadoop 명령은 HDInsight 클러스터에서 MapReduce 작업을 실행하고 작업 출력을 볼 수 있는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f032-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="1f032-134"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f032-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1f032-135">HDInsight의 MapReduce 작업에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="1f032-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="1f032-136">HDInsight Hadoop에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="1f032-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1f032-137">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="1f032-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1f032-138">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="1f032-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1f032-139">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="1f032-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
