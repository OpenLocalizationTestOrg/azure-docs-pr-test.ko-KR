---
title: "HDInsight에서 원격 데스크톱과 Hadoop Hive 사용 - Azure | Microsoft Docs"
description: "Windows 기반 HDInsight Hadoop 클러스터에 대한 원격 데스크톱 연결을 통해 Pig 명령을 사용하여 Pig Latin 문을 실행하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="f45e7-103">원격 데스크탑 연결에서 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f45e7-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="f45e7-104">이 문서에서는 Windows 기반 HDInsight 클러스터에 대한 원격 데스크톱 연결을 통해 Pig 명령을 사용하여 Pig Latin 문을 실행하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="f45e7-105">Pig Latin을 사용하면 매핑하고 함수를 줄이는 대신 데이터 변환을 설명하여 MapReduce 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f45e7-106">원격 데스크톱은 Windows를 운영 체제로 사용하는 HDInsight 클러스터에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="f45e7-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f45e7-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f45e7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="f45e7-109">HDInsight 3.4 이상의 경우 명령줄에서 클러스터의 Pig 작업을 대화형으로 실행하는 방법에 대한 자세한 내용은 [HDInsight 및 SSH로 Pig 사용](hdinsight-hadoop-use-pig-ssh.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f45e7-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="f45e7-110"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="f45e7-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="f45e7-111">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="f45e7-112">Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="f45e7-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="f45e7-113">Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="f45e7-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="f45e7-114"><a id="connect"></a>원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="f45e7-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="f45e7-115">HDInsight 클러스터에 대해 원격 데스크톱을 사용하도록 설정한 다음 [RDP를 사용하여 HDInsight 클러스터에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)의 지침에 따라 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="f45e7-116"><a id="pig"></a>Pig 명령 사용</span><span class="sxs-lookup"><span data-stu-id="f45e7-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="f45e7-117">원격 데스크톱 연결이 설정되면 바탕 화면의 아이콘을 사용하여 **Hadoop 명령줄** 을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="f45e7-118">다음을 사용하여 Pig 명령을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="f45e7-119">`grunt>` 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="f45e7-120">다음 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="f45e7-121">이 명령은 sample.log 파일의 내용을 LOGS 파일에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="f45e7-122">다음 명령을 사용하여 파일의 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="f45e7-123">각 레코드에서 로깅 수준만 추출하는 정규식을 적용하여 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="f45e7-124">**DUMP** 를 사용하여 변환 후 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="f45e7-125">이 예제의 경우 `DUMP LEVELS;`입니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="f45e7-126">다음 문을 사용하여 변환 적용을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="f45e7-127">`DUMP`를 사용하여 각 단계 후의 변환 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="f45e7-128">문</span><span class="sxs-lookup"><span data-stu-id="f45e7-128">Statement</span></span></th><th><span data-ttu-id="f45e7-129">기능</span><span class="sxs-lookup"><span data-stu-id="f45e7-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="f45e7-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="f45e7-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="f45e7-131">로그 수준에 대한 null 값을 포함하는 행을 제거하고 FILTEREDLEVELS에 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f45e7-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="f45e7-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="f45e7-133">로그 수준에 따라 행을 그룹화하고 GROUPEDLEVELS에 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f45e7-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="f45e7-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="f45e7-135">고유한 각 로그 수준 값 및 발생 횟수를 포함하는 데이터의 새 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="f45e7-136">FREQUENCIES에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f45e7-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="f45e7-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="f45e7-138">로그 수준을 개수(내림차순)를 기준으로 정렬하고 RESULT에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="f45e7-139">
6. `STORE` 문을 사용하여 변환 결과를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="f45e7-140">예를 들어 다음 명령은 클러스터의 기본 저장소 컨테이너에 있는 **/example/data/pigout** 디렉터리에 `RESULT`를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="f45e7-141">데이터는 지정된 디렉터리에 **part-nnnnn**이라는 파일로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="f45e7-142">해당 디렉터리가 이미 존재하는 경우 오류 메시지가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="f45e7-143">성가신 프롬프트를 종료하려면 다음 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="f45e7-144">Pig Latin 배치 파일</span><span class="sxs-lookup"><span data-stu-id="f45e7-144">Pig Latin batch files</span></span>
<span data-ttu-id="f45e7-145">Pig 명령을 사용하여 파일에 포함된 Pig Latin을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="f45e7-146">성가신 프롬프트를 종료한 후 **메모장**을 열고 **%PIG_HOME%** 디렉터리에 **pigbatch.pig**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="f45e7-147">다음 줄을 **pigbatch.pig** 파일에 입력하거나 붙여 넣은 다음 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="f45e7-148">pig 명령을 사용하여 **pigbatch.pig** 파일을 실행하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="f45e7-149">일괄 처리 작업이 완료되면 다음과 같은 출력이 표시되며, 이 출력은 이전 단계에서 `DUMP RESULT;` 를 사용했을 때와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="f45e7-150"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="f45e7-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="f45e7-151">이처럼 Pig 명령을 사용하면 MapReduce 작업 또는 배치 파일에 저장된 Pig Latin 작업을 대화형으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f45e7-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="f45e7-152"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f45e7-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f45e7-153">HDInsight의 Pig에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="f45e7-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="f45e7-154">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="f45e7-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="f45e7-155">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="f45e7-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f45e7-156">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="f45e7-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f45e7-157">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="f45e7-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
