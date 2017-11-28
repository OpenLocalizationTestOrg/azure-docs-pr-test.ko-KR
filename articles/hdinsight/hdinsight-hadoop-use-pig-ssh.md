---
title: "-Azure HDInsight 클러스터에서 Hadoop Pig SSH와 aaaUse | Microsoft Docs"
description: "자세한 내용은 SSH와 tooa Linux 기반 Hadoop 클러스터를 연결 하는 방법 및 다음 사용 하 여 hello Pig 명령 toorun Pig 라틴 문을 대화형으로 또는 일괄 처리로 작업 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="a83da-103">Hello Pig 명령 SSH ()를 사용 하 여 Linux 기반 클러스터에서 Pig 작업을 실행</span><span class="sxs-lookup"><span data-stu-id="a83da-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="a83da-104">Toointeractively SSH 연결 tooyour HDInsight 클러스터에서 Pig 작업을 실행 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="a83da-105">hello Pig 라틴 프로그래밍 언어에는 적용 된 toohello 입력 데이터 tooproduce hello 원하는 출력 toodescribe 변환을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a83da-106">hello이 문서의 단계는 Linux 기반 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a83da-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a83da-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a83da-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a83da-109"><a id="ssh"></a>SSH를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="a83da-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="a83da-110">SSH tooconnect tooyour HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="a83da-111">hello 다음 예제에서는 tooa 클러스터 연결 라는 **myhdinsight** hello 계정인으로 **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="a83da-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="a83da-112">**SSH 인증에 대 한 인증서 키를 제공한 경우** hello HDInsight 클러스터를 만든 경우 클라이언트 시스템에서 hello 개인 키의 toospecify hello 위치를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="a83da-113">**SSH 인증을 위해 암호를 제공 하는 경우** hello HDInsight 클러스터를 만들 때 메시지가 표시 되 면 hello 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="a83da-114">HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a83da-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="a83da-115"><a id="pig"></a>Hello Pig 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a83da-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="a83da-116">연결 되 면 다음 명령을 hello를 사용 하 여 hello Pig CLI (명령줄 인터페이스)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="a83da-117">잠시 후 `grunt>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="a83da-118">Hello 문 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="a83da-119">이 명령은 로그 hello sample.log 파일의 hello 내용을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="a83da-120">문 다음 hello를 사용 하 여 hello 파일의 hello 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="a83da-121">문 다음 hello를 사용 하 여 각 레코드에서 정규식 tooextract 유일한 hello 로깅 수준을 적용 하 여 hello 데이터를 다음으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="a83da-122">사용할 수 있습니다 **덤프** hello 변환 후 tooview hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="a83da-123">이 예제의 경우 `DUMP LEVELS;`입니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="a83da-124">다음 표에 hello에 hello 문을 사용 하 여 변환을 계속:</span><span class="sxs-lookup"><span data-stu-id="a83da-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="a83da-125">Pig Latin 문</span><span class="sxs-lookup"><span data-stu-id="a83da-125">Pig Latin statement</span></span> | <span data-ttu-id="a83da-126">어떤 hello 문은 수행</span><span class="sxs-lookup"><span data-stu-id="a83da-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="a83da-127">Hello 로그 수준에 대 한 null 값을 포함 하는 행을 제거 하 고 hello 결과를 저장 `FILTEREDLEVELS`합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="a83da-128">로그 수준에 따라 행 하 고 hello 결과를 저장 하는 그룹 hello `GROUPEDLEVELS`합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="a83da-129">고유한 각 로그 수준 값 및 발생 횟수를 포함하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="a83da-130">hello 데이터 집합에 저장 될 `FREQUENCIES`합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="a83da-131">Hello 로그 수준 count (내림차순)을 기준으로 정렬 하 고로 저장 `RESULT`합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="a83da-132">사용 하 여 `DUMP` tooview hello 결과의 각 단계를 수행한 후 hello 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="a83da-133">Hello를 사용 하 여 변환의 hello 결과 저장할 수도 있습니다 `STORE` 문.</span><span class="sxs-lookup"><span data-stu-id="a83da-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="a83da-134">예를 들어 다음 문의 hello 저장 hello `RESULT` toohello `/example/data/pigout` hello 기본 저장소 클러스터에 대 한 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="a83da-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="a83da-135">hello 데이터 hello 이라는 파일에 지정 된 디렉터리에 저장 됩니다 `part-nnnnn`합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="a83da-136">Hello 디렉터리가 이미 있으면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="a83da-137">tooexit hello grunt 프롬프트를 hello 문 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="a83da-138">Pig Latin 배치 파일</span><span class="sxs-lookup"><span data-stu-id="a83da-138">Pig Latin batch files</span></span>

<span data-ttu-id="a83da-139">Hello Pig 명령 toorun 파일에 포함 된 Pig 라틴 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="a83da-140">Hello grunt 프롬프트를 종료 한 후 사용 하 여 hello 다음 명령은 라는 파일로 STDIN toopipe `pigbatch.pig`합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="a83da-141">이 파일은 hello hello SSH 사용자 계정에 대 한 홈 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="a83da-142">입력 또는 hello 다음 줄을 붙여 하 고 완료 되 면 Ctrl + D를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="a83da-143">사용 하 여 hello 다음 명령은 toorun hello `pigbatch.pig` hello Pig 명령을 사용 하 여 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="a83da-144">Hello 일괄 처리 작업이 완료 되 면 hello 출력을 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a83da-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="a83da-145"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="a83da-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a83da-146">Pig HDInsight에 대 한 일반 정보를 hello 문서 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a83da-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="a83da-147">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="a83da-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="a83da-148">HDInsight에서 Hadoop으로 다른 방법으로 toowork에 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="a83da-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="a83da-149">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="a83da-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a83da-150">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="a83da-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
