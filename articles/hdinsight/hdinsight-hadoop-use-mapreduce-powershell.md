---
title: "Hadoop과 MapReduce 및 PowerShell 사용 - Azure HDInsight | Microsoft Docs"
description: "PowerShell을 사용하여 HDInsight에서 Hadoop으로 MapReduce 작업을 원격으로 실행하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="98f6f-103">PowerShell을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="98f6f-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="98f6f-104">이 문서에서는 Azure PowerShell을 사용하여 HDInsight 클러스터의 Hadoop에서 MapReduce 작업을 실행하는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="98f6f-105"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="98f6f-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="98f6f-106">**Azure HDInsight(HDInsight의 Hadoop) 클러스터**</span><span class="sxs-lookup"><span data-stu-id="98f6f-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="98f6f-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="98f6f-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98f6f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="98f6f-109">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="98f6f-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="98f6f-110"><a id="powershell"></a>Azure PowerShell을 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="98f6f-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="98f6f-111">Azure PowerShell은 HDInsight에서 MapReduce 작업을 원격으로 실행할 수 있는 *cmdlet* 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="98f6f-112">내부적으로는 HDInsight 클러스터에서 실행되는 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (이전의 Templeton)에 대한 REST 호출을 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="98f6f-113">다음 cmdlet은 원격 HDInsight 클러스터에서 MapReduce 작업을 실행할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="98f6f-114">**Login-AzureRmAccount**: Azure 구독에 대해 Azure PowerShell을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="98f6f-115">**New-AzureRmHDInsightMapReduceJobDefinition**: 지정한 MapReduce 정보를 사용하여 새 *작업 정의*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="98f6f-116">**Start-AzureRmHDInsightJob**: HDInsight로 작업 정의를 보내고, 작업을 시작하고, 작업 상태를 확인하는 데 사용할 수 있는 *작업* 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="98f6f-117">**Wait-AzureRmHDInsightJob**: 작업 개체를 사용하여 작업 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="98f6f-118">작업이 완료되거나 대기 시간이 초과될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="98f6f-119">**Get-AzureRmHDInsightJobOutput**: 작업 출력을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="98f6f-120">다음 단계는 HDInsight 클러스터에서 작업을 실행하기 위해 이러한 cmdlet을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="98f6f-121">편집기를 사용하여 다음 코드를 **mapreducejob.ps1**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="98f6f-122">[!code-powershell[기본](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="98f6f-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="98f6f-123">새 **Azure PowerShell** 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="98f6f-124">**mapreducejob.ps1** 파일의 디렉터리 위치를 변경한 다음 명령을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="98f6f-125">스크립트를 실행하는 경우 HDInsight 클러스터의 이름 및 클러스터의 HTTPS/관리자 계정 이름 및 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="98f6f-126">Azure 구독에서 인증을 받으라는 메시지도 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="98f6f-127">작업이 완료되면 다음 텍스트와 유사한 출력이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="98f6f-128">이 출력은 작업이 성공적으로 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="98f6f-129">**ExitCode** 가 0이 아닌 값이면 [문제 해결](#troubleshooting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98f6f-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="98f6f-130">이 예제에서도 다운로드한 파일을 스크립트를 실행한 디렉터리의 **output.txt** 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="98f6f-131">출력 보기</span><span class="sxs-lookup"><span data-stu-id="98f6f-131">View output</span></span>

<span data-ttu-id="98f6f-132">작업에서 생성한 단어 및 단어 개수를 보려면 **output.txt** 파일을 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="98f6f-133">MapReduce 작업의 출력 파일은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="98f6f-134">따라서 이 샘플을 다시 실행하는 경우 출력 파일의 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="98f6f-135"><a id="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="98f6f-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="98f6f-136">작업이 완료될 때 정보가 반환되지 않은 경우, 처리하는 동안 오류가 발생했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="98f6f-137">이 작업에 대한 오류 정보를 보려면 **mapreducejob.ps1** 파일의 끝에 다음 명령을 추가하고 파일을 저장한 다음 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="98f6f-138">이 cmdlet은 작업을 실행할 때 서버의 STDERR에 기록된 정보를 반환하며 이 정보는 작업이 실패한 이유를 확인하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="98f6f-139"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="98f6f-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="98f6f-140">여기에서 볼 수 있듯이 Azure PowerShell은 HDInsight 클러스터에서 MapReduce 작업 상태를 모니터링하고, 출력을 검색하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98f6f-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="98f6f-141"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="98f6f-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="98f6f-142">HDInsight의 MapReduce 작업에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="98f6f-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="98f6f-143">HDInsight Hadoop에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="98f6f-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="98f6f-144">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="98f6f-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="98f6f-145">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="98f6f-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="98f6f-146">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="98f6f-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
