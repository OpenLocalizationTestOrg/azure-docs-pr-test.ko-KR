---
title: "HDInsight에서 Hadoop과 MapReduce 및 원격 데스크톱 사용 - Azure | Microsoft Docs"
description: "원격 데스크톱을 사용하여 HDInsight에서 Hadoop에 연결하여 MapReduce 작업을 실행하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: b56674857b013f9bb3d4dd4b6e97b34e0a97b1b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="90832-103">원격 데스크톱을 사용하는 HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="90832-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="90832-104">이 문서에서는 원격 데스크톱을 사용하여 HDInsight 클러스터에서 Hadoop에 연결한 다음 Hadoop 명령을 사용하여 MapReduce 작업을 실행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="90832-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90832-105">원격 데스크톱은 Windows 기반 HDInsight 클러스터에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90832-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="90832-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="90832-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="90832-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90832-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="90832-108">HDInsight 3.4 이상의 경우 HDInsight 클러스터에 연결 및 MapReduce 작업 실행에 대한 자세한 내용은 [SSH로 MapReduce 사용](hdinsight-hadoop-use-mapreduce-ssh.md)을 참좋세요.</span><span class="sxs-lookup"><span data-stu-id="90832-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="90832-109"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="90832-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="90832-110">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="90832-111">Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="90832-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="90832-112">Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="90832-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="90832-113"><a id="connect"></a>원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="90832-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="90832-114">HDInsight 클러스터에 대해 원격 데스크톱을 사용하도록 설정한 다음 [RDP를 사용하여 HDInsight 클러스터에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)의 지침에 따라 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="90832-115"><a id="hadoop"></a>Hadoop 명령 사용</span><span class="sxs-lookup"><span data-stu-id="90832-115"><a id="hadoop"></a>Use the Hadoop command</span></span>
<span data-ttu-id="90832-116">HDInsight 클러스터에 대한 데스크톱에 연결된 후 Hadoop 명령을 사용하여 MapReduce 작업을 실행하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="90832-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="90832-117">HDInsight 데스크톱에서 **Hadoop 명령줄**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="90832-118">**c:\apps\dist\hadoop-&lt;version number>** 디렉터리에서 새 명령 프롬프트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="90832-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="90832-119">버전 번호는 Hadoop를 업데이트할 때 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="90832-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="90832-120">해당 경로를 찾으려면 **HADOOP_HOME** 환경 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90832-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="90832-121">예를 들어 `cd %HADOOP_HOME%` 은 버전 번호를 알 필요 없이 디렉터리를 Hadoop 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="90832-122">**Hadoop** 명령을 사용하여 예제 MapReduce 작업을 실행하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="90832-123">이 명령은 현재 디렉터리에 있는 **hadoop-mapreduce-examples.jar** 파일의 **wordcount** 클래스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="90832-124">입력으로 **wasb://example/data/gutenberg/davinci.txt** 문서를 사용하고 출력은 **wasb:///example/data/WordCountOutput**에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="90832-124">As input, it uses the **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="90832-125">이 MapReduce 작업 및 예제 데이터에 대한 자세한 내용은 <a href="hdinsight-use-mapreduce.md">HDInsight Hadoop에서 MapReduce 사용</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90832-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="90832-126">작업이 처리되는 동안 세부 정보를 내보내며 마지막으로 작업이 완료될 때 반환 정보는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="90832-127">작업이 완료된 후 **wasb://example/data/WordCountOutput**에 저장된 출력 파일을 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-127">When the job is complete, use the following command to list the output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="90832-128">**_SUCCESS** 및 **part-r-00000**이라는 두 개의 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90832-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="90832-129">**part-r-00000** 파일은 이 작업에 대한 출력을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="90832-130">일부 MapReduce 작업은 여러 **part-r-#####** 파일로 결과를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90832-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="90832-131">그럴 경우 ##### 접미사가 파일의 순서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90832-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="90832-132">출력을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="90832-133">그러면 각 단어가 나타나는 횟수뿐만 아니라 **wasb://example/data/gutenberg/davinci.txt** 파일에 포함된 단어의 목록도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90832-133">This displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="90832-134">다음은 파일에 포함된 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="90832-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="90832-135"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="90832-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="90832-136">여기에서 볼 수 있듯이 Hadoop 명령은 HDInsight 클러스터에서 MapReduce 작업을 실행하고 작업 출력을 볼 수 있는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90832-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="90832-137"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="90832-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="90832-138">HDInsight의 MapReduce 작업에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="90832-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="90832-139">HDInsight Hadoop에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="90832-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="90832-140">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="90832-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="90832-141">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="90832-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="90832-142">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="90832-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
