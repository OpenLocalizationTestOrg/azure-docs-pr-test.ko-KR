---
title: "HDInsight 클러스터에서 SSH와 Hadoop Pig 사용 - Azure | Microsoft Docs"
description: "SSH를 사용하여 Linux 기반 Hadoop 클러스터에 연결한 다음 Pig 명령을 사용하여 Pig Latin 문을 대화형으로 실행하거나 일괄 처리 작업으로 실행하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="d6e8e-103">Pig 명령(SSH)를 사용하여 Linux 기반 클러스터에서 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="d6e8e-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="d6e8e-104">SSH 연결에서 HDInsight 클러스터로 Pig 작업을 대화형으로 실행하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="d6e8e-105">Pig Latin 프로그래밍 언어를 사용하면 원하는 출력을 생성하는 입력 데이터에 적용되는 변환을 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6e8e-106">이 문서의 단계에는 Linux 기반 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d6e8e-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d6e8e-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="d6e8e-109"><a id="ssh"></a>SSH를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="d6e8e-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="d6e8e-110">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="d6e8e-111">다음은 **sshuser** 계정으로 **myhdinsight** 클러스터에 연결하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="d6e8e-112">**SSH 인증을 위해 인증서 키를 제공한 경우** HDInsight 클러스터를 만들 때 클라이언트 시스템에서 개인 키의 위치를 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="d6e8e-113">**SSH 인증을 위해 암호를 제공한 경우** HDInsight 클러스터를 만들 때 메시지가 표시되면 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="d6e8e-114">HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="d6e8e-115"><a id="pig"></a>Pig 명령 사용</span><span class="sxs-lookup"><span data-stu-id="d6e8e-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="d6e8e-116">연결되면 다음 명령을 사용하여 Pig CLI(명령줄 인터페이스)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="d6e8e-117">잠시 후 `grunt>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="d6e8e-118">다음 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="d6e8e-119">이 명령은 sample.log 파일의 내용을 로그에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="d6e8e-120">다음 문을 사용하여 파일의 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="d6e8e-121">이어서 다음 문을 사용하여 각 레코드에서 로깅 수준만 추출하는 정규식을 적용하여 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="d6e8e-122">**DUMP** 를 사용하여 변환 후 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="d6e8e-123">이 예제의 경우 `DUMP LEVELS;`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="d6e8e-124">다음 표에서 문을 사용하여 계속해서 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="d6e8e-125">Pig Latin 문</span><span class="sxs-lookup"><span data-stu-id="d6e8e-125">Pig Latin statement</span></span> | <span data-ttu-id="d6e8e-126">문의 기능</span><span class="sxs-lookup"><span data-stu-id="d6e8e-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="d6e8e-127">로그 수준의 null 값이 포함된 행을 제거하고 결과를 `FILTEREDLEVELS`에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="d6e8e-128">행을 로그 수준으로 그룹화하고 결과를 `GROUPEDLEVELS`에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="d6e8e-129">고유한 각 로그 수준 값 및 발생 횟수를 포함하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="d6e8e-130">데이터 집합은 `FREQUENCIES`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="d6e8e-131">로그 수준을 개수(내림차순)를 기준으로 정렬하고 `RESULT`에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="d6e8e-132">`DUMP`를 사용하여 각 단계 후의 변환 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="d6e8e-133">`STORE` 문을 사용하여 변환 결과를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="d6e8e-134">예를 들어 다음 문은 `RESULT`를 클러스터 기본 저장소의 `/example/data/pigout` 디렉터리에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="d6e8e-135">데이터는 `part-nnnnn` 파일의 지정된 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="d6e8e-136">해당 디렉터리가 이미 존재하는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="d6e8e-137">프롬프트를 종료하려면 다음 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="d6e8e-138">Pig Latin 배치 파일</span><span class="sxs-lookup"><span data-stu-id="d6e8e-138">Pig Latin batch files</span></span>

<span data-ttu-id="d6e8e-139">Pig 명령을 사용하여 파일에 포함된 Pig Latin을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="d6e8e-140">프롬프트를 종료한 후 다음 명령을 사용하여 STDIN을 `pigbatch.pig` 파일에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="d6e8e-141">이 파일은 SSH 사용자 계정의 홈 디렉터리에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="d6e8e-142">다음 줄에 입력하거나 붙여 넣은 다음 완료되면 Ctrl+D를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="d6e8e-143">다음의 Pig 명령을 사용하여 `pigbatch.pig` 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="d6e8e-144">배치 작업이 완료되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="d6e8e-145"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6e8e-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d6e8e-146">HDInsight의 Pig에 대한 일반적인 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="d6e8e-147">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="d6e8e-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="d6e8e-148">HDInsight에서 Hadoop을 사용하여 작업하는 다른 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6e8e-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="d6e8e-149">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="d6e8e-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d6e8e-150">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="d6e8e-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
