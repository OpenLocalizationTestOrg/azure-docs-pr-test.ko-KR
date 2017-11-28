---
title: "aaaMapReduce 및 Azure HDInsight에서 Hadoop으로 원격 데스크톱 | Microsoft Docs"
description: "자세한 방법을 toouse 원격 데스크톱 tooconnect tooHadoop HDInsight 및 MapReduce 작업을 실행된 합니다."
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
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="36b2f-103">원격 데스크톱을 사용하는 HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="36b2f-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="36b2f-104">이 문서에서는 원격 데스크톱을 사용 하 여 tooconnect tooa HDInsight의 Hadoop 클러스터 하는 방법에 대해 알아봅니다 쿼리하고 hello Hadoop 명령을 사용 하 여 MapReduce 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36b2f-105">원격 데스크톱은 Windows 기반 HDInsight 클러스터에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="36b2f-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="36b2f-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b2f-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="36b2f-108">예: HDInsight 3.4 또는 큰 참조 [SSH 사용 하 여 MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md) toohello HDInsight 클러스터를 연결 하 고 MapReduce 작업 실행에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="36b2f-109"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="36b2f-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="36b2f-110">이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="36b2f-111">Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="36b2f-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="36b2f-112">Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="36b2f-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="36b2f-113"><a id="connect"></a>원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="36b2f-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="36b2f-114">Hello HDInsight 클러스터에 대 한 원격 데스크톱을 사용 합니다. 다음 hello 지침에 따라 tooit 연결 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="36b2f-115"><a id="hadoop"></a>Hello Hadoop 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="36b2f-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="36b2f-116">Hello HDInsight 클러스터에 연결 된 toohello 데스크톱 인 경우 hello Hadoop 명령을 사용 하 여 단계 toorun MapReduce 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="36b2f-117">Hello HDInsight 바탕 화면에서 시작 hello **Hadoop 명령줄**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="36b2f-118">새 명령 프롬프트에서 hello 열립니다 **c:\apps\dist\hadoop-&lt;버전 번호 >** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36b2f-119">hello 버전 번호는 Hadoop를 업데이트할 때 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="36b2f-120">hello **HADOOP_HOME** 환경 변수 사용된 toofind hello 경로가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="36b2f-121">예를 들어 `cd %HADOOP_HOME%` tooknow hello 버전 번호를 요구 하지 않고 변경 내용 디렉터리 toohello Hadoop 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="36b2f-122">toouse hello **Hadoop** toorun 예제 MapReduce 작업 명령에서 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="36b2f-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="36b2f-123">Hello 시작 **wordcount** hello에 포함 되어 있는 클래스 **mapreduce hadoop-examples.jar** hello 현재 디렉터리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="36b2f-124">입력으로 사용 하 여 hello **wasb://example/data/gutenberg/davinci.txt** 문서 및 출력에 저장 됩니다: **wasb: / / / 예제/데이터/WordCountOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36b2f-125">이 MapReduce 작업과 hello 예제 데이터에 대 한 자세한 내용은 참조 <a href="hdinsight-use-mapreduce.md">HDInsight Hadoop에서 사용 하 여 MapReduce</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="36b2f-126">처리 되 고 hello 작업이 완료 되 면 유사한 toohello 다음 정보를 반환 hello 작업 세부 정보를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="36b2f-127">다음 명령 toolist hello 출력 파일에 저장 하는 hello를 사용 하 여 hello 작업이 완료 되 면 **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="36b2f-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="36b2f-128">**_SUCCESS** 및 **part-r-00000**이라는 두 개의 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="36b2f-129">hello **파트-r-00000** 이 작업에 대 한 hello 출력 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36b2f-130">일부 MapReduce 작업은 여러 hello 결과 분할할 수 **파트-r-# # #** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="36b2f-131">이 경우 hello를 사용 하 여 # # # hello 파일의 tooindicate hello 순서가 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="36b2f-132">다음 명령을 사용 하 여 hello tooview hello 출력:</span><span class="sxs-lookup"><span data-stu-id="36b2f-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="36b2f-133">그러면 목록이 포함 된 hello 단어 hello에 표시 됩니다 **wasb://example/data/gutenberg/davinci.txt** hello 각 단어 발생 한 횟수와 함께 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="36b2f-134">hello 다음은 hello 파일에 포함 되어야 하는 hello 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="36b2f-135"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="36b2f-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="36b2f-136">볼 수 있듯이 hello Hadoop 명령 쉽게 toorun MapReduce 작업에 제공 된 HDInsight 클러스터와 다음 보기 hello 작업 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b2f-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="36b2f-137"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="36b2f-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="36b2f-138">HDInsight의 MapReduce 작업에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="36b2f-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="36b2f-139">HDInsight Hadoop에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="36b2f-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="36b2f-140">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="36b2f-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="36b2f-141">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="36b2f-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="36b2f-142">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="36b2f-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
