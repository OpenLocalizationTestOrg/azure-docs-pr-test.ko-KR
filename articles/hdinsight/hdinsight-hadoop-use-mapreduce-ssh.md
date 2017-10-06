---
title: "aaaMapReduce 및 Azure HDInsight에서 Hadoop으로 SSH 연결 | Microsoft Docs"
description: "HDInsight에서 Hadoop을 사용 하 여 toouse SSH toorun MapReduce을 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="7425c-103">SSH를 사용하여 HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="7425c-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="7425c-104">SSH (보안 셸) 연결 tooHDInsight에서 MapReduce toosubmit 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="7425c-105">잘 알고 있는 경우 Linux 기반 Hadoop을 사용 하 여 서버에 있지만 새 tooHDInsight 참조 하십시오 [Linux 기반 HDInsight 팁](hdinsight-hadoop-linux-information.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="7425c-106"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="7425c-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7425c-107">Linux 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="7425c-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7425c-108">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7425c-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7425c-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7425c-110">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="7425c-110">An SSH client.</span></span> <span data-ttu-id="7425c-111">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7425c-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="7425c-112"><a id="ssh"></a>SSH를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="7425c-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="7425c-113">SSH를 사용 하 여 toohello 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="7425c-114">다음 명령을 hello 라는 tooa 클러스터를 연결 하는 예를 들어 **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="7425c-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="7425c-115">**SSH 인증에 대 한 인증서 키를 사용 하는 경우**, hello 개인 키의 toospecify hello 위치 클라이언트 시스템에서 같이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="7425c-116">**SSH 인증에 대 한 암호를 사용 하는 경우**, 메시지가 표시 되 면 tooprovide hello 암호 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="7425c-117">HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7425c-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="7425c-118"><a id="hadoop"></a>Hadoop 명령 사용</span><span class="sxs-lookup"><span data-stu-id="7425c-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="7425c-119">연결 된 toohello HDInsight 클러스터를 한 후 명령 toostart MapReduce 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="7425c-120">이 명령은 시작 hello `wordcount` hello에 포함 되어 있는 클래스 `hadoop-mapreduce-examples.jar` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="7425c-121">Hello를 사용 하 여 `/example/data/gutenberg/davinci.txt` 입력 및 출력으로 문서에 저장 된 `/example/data/WordCountOutput`합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7425c-122">이 MapReduce 작업과 hello 예제 데이터에 대 한 자세한 내용은 참조 [HDInsight의 Hadoop에서 사용 하 여 MapReduce](hdinsight-use-mapreduce.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="7425c-123">처리 하 고 텍스트 hello 작업이 완료 되었을 때 다음 정보 비슷한 toohello 반환 hello 작업 세부 정보를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="7425c-124">Hello 작업이 완료 되 면 다음 명령 toolist hello 출력 파일이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="7425c-125">이 명령은 `_SUCCESS` 및 `part-r-00000`의 두 개의 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="7425c-126">hello `part-r-00000` 이 작업에 대 한 hello 출력 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7425c-127">일부 MapReduce 작업은 여러 hello 결과 분할할 수 **파트-r-# # #** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="7425c-128">이 경우 hello를 사용 하 여 # # # hello 파일의 tooindicate hello 순서가 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="7425c-129">다음 명령을 사용 하 여 hello tooview hello 출력:</span><span class="sxs-lookup"><span data-stu-id="7425c-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="7425c-130">이 명령은 hello에 포함 된 hello 단어의 목록을 표시 **wasb://example/data/gutenberg/davinci.txt** 파일과 hello 각 단어 발생 한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="7425c-131">hello 다음 텍스트는 hello 파일에 포함 된 hello 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="7425c-132"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="7425c-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="7425c-133">볼 수 있듯이 Hadoop 명령은 제공 쉽게 toorun는 HDInsight 클러스터와 다음 hello 작업 출력 보기에 있는 MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7425c-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="7425c-134"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="7425c-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7425c-135">HDInsight의 MapReduce 작업에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="7425c-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="7425c-136">HDInsight Hadoop에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="7425c-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7425c-137">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="7425c-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7425c-138">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="7425c-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7425c-139">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="7425c-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
