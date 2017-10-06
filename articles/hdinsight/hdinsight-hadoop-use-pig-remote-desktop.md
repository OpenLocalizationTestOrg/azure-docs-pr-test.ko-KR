---
title: "Hadoop Pig HDInsight-Azure의에서 원격 데스크톱 aaaUse | Microsoft Docs"
description: "Toouse HDInsight의 원격 데스크톱 연결 tooa Windows 기반 Hadoop 클러스터에서 Pig 명령 toorun Pig 라틴 문 hello 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="40954-103">원격 데스크탑 연결에서 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="40954-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="40954-104">이 문서는 원격 데스크톱 연결 tooa Windows 기반 HDInsight 클러스터에서 hello Pig 명령 toorun Pig 라틴 문 사용에 대 한 연습을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="40954-105">Pig 라틴 toocreate MapReduce 응용 프로그램 데이터 변환을 기반으로 하지 않고 매핑할 수 있으며 함수 줄일 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40954-106">원격 데스크톱은만 hello 운영 체제로 Windows를 사용 하는 HDInsight 클러스터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40954-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="40954-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="40954-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40954-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="40954-109">HDInsight 3.4 또는 큰 참조 하십시오 [HDInsight 및 SSH와 Pig](hdinsight-hadoop-use-pig-ssh.md) Pig를 대화형으로 실행에 대 한 내용은 hello에 직접 작업 명령줄에서 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="40954-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="40954-110"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="40954-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="40954-111">이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="40954-112">Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="40954-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="40954-113">Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="40954-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="40954-114"><a id="connect"></a>원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="40954-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="40954-115">Hello HDInsight 클러스터에 대 한 원격 데스크톱을 사용 합니다. 다음 hello 지침에 따라 tooit 연결 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="40954-116"><a id="pig"></a>Hello Pig 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="40954-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="40954-117">원격 데스크톱 연결을 설정한 후 시작 hello **Hadoop 명령줄** hello 바탕 화면에서 hello 아이콘을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="40954-118">다음 toostart hello Pig 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="40954-119">`grunt>` 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="40954-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="40954-120">Hello 문 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="40954-121">이 명령은 hello 로그 파일에 hello sample.log 파일의 내용을 hello를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="40954-122">다음 명령을 hello를 사용 하 여 hello 파일의 hello 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40954-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="40954-123">각 레코드에서 정규식 tooextract 유일한 hello 로깅 수준을 적용 하 여 hello 데이터를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="40954-124">사용할 수 있습니다 **덤프** hello 변환 후 tooview hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="40954-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="40954-125">이 예제의 경우 `DUMP LEVELS;`입니다.</span><span class="sxs-lookup"><span data-stu-id="40954-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="40954-126">다음 조건 hello를 사용 하 여 변환을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="40954-127">사용 하 여 `DUMP` tooview hello 결과의 각 단계를 수행한 후 hello 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="40954-128">문</span><span class="sxs-lookup"><span data-stu-id="40954-128">Statement</span></span></th><th><span data-ttu-id="40954-129">기능</span><span class="sxs-lookup"><span data-stu-id="40954-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="40954-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="40954-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="40954-131">Hello 로그 수준에 대 한 null 값을 포함 하는 행을 제거 하 고 FILTEREDLEVELS에 hello 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="40954-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="40954-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="40954-133">그룹 hello 로그 수준에 따라 행 GROUPEDLEVELS에 hello 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="40954-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="40954-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="40954-135">고유한 각 로그 수준 값 및 발생 횟수를 포함하는 데이터의 새 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40954-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="40954-136">FREQUENCIES에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="40954-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="40954-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="40954-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="40954-138">횟수 (내림차순)와 저장소 hello 로그 수준에 결과 정렬</span><span class="sxs-lookup"><span data-stu-id="40954-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="40954-139">
6.Hello를 사용 하 여 변환의 hello 결과 저장할 수도 있습니다 `STORE` 문.</span><span class="sxs-lookup"><span data-stu-id="40954-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="40954-140">예를 들어 다음 명령을 hello 저장 hello `RESULT` toohello **/example/data/pigout** 디렉터리에서 클러스터에 대 한 hello 기본 저장소 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="40954-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="40954-141">hello 데이터 hello 이라는 파일에 지정 된 디렉터리에 저장 됩니다 **파트 nnnnn**합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="40954-142">Hello 디렉터리가 이미 있는 경우는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40954-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="40954-143">tooexit hello grunt 프롬프트를 hello 문 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="40954-144">Pig Latin 배치 파일</span><span class="sxs-lookup"><span data-stu-id="40954-144">Pig Latin batch files</span></span>
<span data-ttu-id="40954-145">또한 파일에 hello Pig 명령 toorun 포함 된 Pig 라틴 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40954-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="40954-146">Hello grunt 프롬프트를 종료 한 후 엽니다 **메모장** 라는 새 파일을 만들고 **pigbatch.pig** hello에 **% PIG_HOME %** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="40954-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="40954-147">Hello에 형식 또는 붙여넣기 hello 다음 줄 **pigbatch.pig** 파일을 선택한 다음 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="40954-148">사용 하 여 hello toorun hello 다음 **pigbatch.pig** hello pig 명령을 사용 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="40954-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="40954-149">Hello 일괄 처리 작업이 완료 되 면 hello 출력 해야 수 hello 동일로 사용 하는 경우 다음이 표시 됩니다 `DUMP RESULT;` hello 이전 단계에서:</span><span class="sxs-lookup"><span data-stu-id="40954-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="40954-150"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="40954-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="40954-151">볼 수 있듯이 hello Pig 명령 있습니다 toointeractively를 MapReduce 작업을 실행 하거나 배치 파일에 저장 된 Pig 라틴 문자 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="40954-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="40954-152"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="40954-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="40954-153">HDInsight의 Pig에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="40954-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="40954-154">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="40954-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="40954-155">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="40954-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="40954-156">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="40954-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="40954-157">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="40954-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
