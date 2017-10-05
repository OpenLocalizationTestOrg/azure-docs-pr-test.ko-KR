---
title: "HDInsight에서 PowerShell과 Hadoop Pig 사용 - Azure | Microsoft Docs"
description: "Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터에 Pig 작업을 제출하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="c2485-103">Azure PowerShell을 사용하여 HDInsight에서 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c2485-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="c2485-104">이 문서는 Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터에 Pig 작업을 제출하는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="c2485-105">Pig를 사용하면 매핑하고 함수를 줄이는 대신 데이터 변환을 모델링하는 언어(Pig Latin)를 사용하여 MapReduce 작업을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="c2485-106">이 문서에는 예제에 사용된 Pig Latin 문이 수행하는 작업에 대해 자세한 설명을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="c2485-107">이 예제에 사용된 Pig Latin에 대한 자세한 내용은 [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2485-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="c2485-108"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="c2485-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="c2485-109">**Azure HDInsight 클러스터**</span><span class="sxs-lookup"><span data-stu-id="c2485-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c2485-110">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c2485-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2485-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c2485-112">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="c2485-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="c2485-113"><a id="powershell"></a>PowerShell을 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c2485-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="c2485-114">Azure PowerShell은 HDInsight에서 Pig 작업을 원격으로 실행할 수 있는 *cmdlet* 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="c2485-115">내부적으로 PowerShell은 HDInsight 클러스터에서 실행되는 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat)으로 REST 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="c2485-116">다음 cmdlet은 원격 HDInsight 클러스터에서 Pig 작업을 실행할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="c2485-117">**Login-AzureRmAccount**: Azure 구독에 대해 Azure PowerShell을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="c2485-118">**New-AzureRmHDInsightPigJobDefinition**: 지정한 Pig Latin 문을 사용하여 *작업 정의*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="c2485-119">**Start-AzureRmHDInsightJob**: HDInsight로 작업 정의를 보내고, 작업을 시작하고, 작업 상태를 확인하는 데 사용할 수 있는 *작업* 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="c2485-120">**Wait-AzureRmHDInsightJob**: 작업 개체를 사용하여 작업 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="c2485-121">작업이 완료될 때까지 기다리거나 대기 시간이 초과될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="c2485-122">**Get-AzureRmHDInsightJobOutput**: 작업 출력을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="c2485-123">다음 단계는 HDInsight 클러스터에서 작업을 실행하기 위해 이러한 cmdlet을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="c2485-124">편집기를 사용하여 다음 코드를 **pigjob.ps1**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="c2485-125">[!code-powershell[기본](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="c2485-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="c2485-126">새 Windows PowerShell 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="c2485-127">**pigjob.ps1** 파일의 디렉터리 위치를 변경한 다음 명령을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="c2485-128">Azure 구독에 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="c2485-129">그런 다음 HTTPs/관리자 계정 이름과 HDInsight 클러스터 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="c2485-130">작업이 완료되면 다음 텍스트와 유사한 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="c2485-131"><a id="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="c2485-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="c2485-132">작업이 완료될 때 정보가 반환되지 않은 경우, 처리하는 동안 오류가 발생했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="c2485-133">이 작업에 대한 오류 정보를 보려면 **pigjob.ps1** 파일 끝에 다음 명령을 추가하고 저장한 다음 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="c2485-134">이 명령은 작업을 실행할 때 서버의 STDERR에 기록된 정보를 반환하며 이 정보는 작업이 실패한 이유를 확인하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="c2485-135"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="c2485-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="c2485-136">이처럼 Azure PowerShell은 HDInsight 클러스터에서 Pig 작업을 실행하고, 작업 상태를 모니터링하고, 출력을 검색하는 쉬운 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2485-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="c2485-137"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2485-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="c2485-138">HDInsight의 Pig에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="c2485-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="c2485-139">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="c2485-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="c2485-140">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="c2485-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c2485-141">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="c2485-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c2485-142">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="c2485-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
