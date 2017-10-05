---
title: "HDInsight에서 PowerShell과 Hadoop Hive 사용 - Azure | Microsoft Docs"
description: "PowerShell을 사용하여 HDInsight의 Hadoop에서 Hive 쿼리 실행"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="308bb-103">PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="308bb-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="308bb-104">이 문서는 Azure 리소스 그룹 모드에서 Azure PowerShell을 사용하여 HDInsight 클러스터의 Hadoop에서 Hive 쿼리를 실행하는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="308bb-105">이 문서에는 예제에 사용된 HiveQL 문이 수행하는 작업에 대해 자세한 설명을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="308bb-106">이 예제에서 사용된 HiveQL에 대한 자세한 내용은 [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="308bb-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="308bb-107">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="308bb-107">**Prerequisites**</span></span>

* <span data-ttu-id="308bb-108">**Azure HDInsight 클러스터**: 클러스터가 Windows 기반인지 또는 Linux 기반인지는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="308bb-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="308bb-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="308bb-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="308bb-111">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="308bb-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="308bb-112">Azure PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="308bb-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="308bb-113">Azure PowerShell은 HDInsight에서 Hive 쿼리를 원격으로 실행할 수 있는 *cmdlet* 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="308bb-114">내부적으로 cmdlet은 HDInsight 클러스터에서 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat)에 대한 REST를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="308bb-115">다음 cmdlet은 원격 HDInsight 클러스터에서 Hive 쿼리를 실행할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="308bb-116">**Add-AzureRmAccount**: Azure 구독에 대해 Azure PowerShell을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="308bb-117">**New-AzureRmHDInsightHiveJobDefinition**: 지정한 HiveQL 문을 사용하여 *작업 정의*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="308bb-118">**Start-AzureRmHDInsightJob**: HDInsight로 작업 정의를 보내고, 작업을 시작하고, 작업 상태를 확인하는 데 사용할 수 있는 *작업* 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="308bb-119">**Wait-AzureRmHDInsightJob**: 작업 개체를 사용하여 작업 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="308bb-120">작업이 완료되거나 대기 시간이 초과될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="308bb-121">**Get-AzureRmHDInsightJobOutput**: 작업 출력을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="308bb-122">**Invoke-AzureRmHDInsightHiveJob**: HiveQL 문을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="308bb-123">이 cmdlet은 쿼리 완료를 차단한 다음 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="308bb-124">**Use-AzureRmHDInsightCluster**: **Invoke-AzureRmHDInsightHiveJob** 명령에 사용할 현재 클러스터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="308bb-125">다음 단계는 HDInsight 클러스터에서 작업을 실행하기 위해 이러한 cmdlet을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="308bb-126">편집기를 사용하여 다음 코드를 **hivejob.ps1**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="308bb-127">[!code-powershell[기본](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="308bb-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="308bb-128">새 **Azure PowerShell** 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="308bb-129">**hivejob.ps1** 파일의 디렉터리 위치를 변경한 다음 명령을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="308bb-130">스크립트를 실행할 때 클러스터에 대한 클러스터 이름 및 HTTPS/관리자 계정 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="308bb-131">Azure 구독에 로그인하라는 메시지도 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="308bb-132">작업이 완료되면 다음 텍스트과 유사한 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="308bb-133">앞서 설명한 것처럼 **Invoke-hive** 는 쿼리를 실행하고 응답을 기다리는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="308bb-134">다음 스크립트를 사용하여 Invoke-Hive 작동 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="308bb-135">[!code-powershell[기본](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="308bb-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="308bb-136">출력은 다음 텍스트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="308bb-137">더 긴 HiveQL 쿼리에는 Azure PowerShell **Here-Strings** cmdlet 또는 HiveQL 스크립트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="308bb-138">다음 코드 조각은 **Invoke-Hive** cmdlet을 사용하여 HiveQL 스크립트 파일을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="308bb-139">HiveQL 스크립트 파일은 wasb://에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="308bb-140">**Here-Strings**에 대한 자세한 내용은 <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Windows PowerShell Here-Strings 사용</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="308bb-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="308bb-141">문제 해결</span><span class="sxs-lookup"><span data-stu-id="308bb-141">Troubleshooting</span></span>

<span data-ttu-id="308bb-142">작업이 완료될 때 정보가 반환되지 않은 경우, 처리하는 동안 오류가 발생했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="308bb-143">이 작업에 대한 오류 정보를 보려면 **hivejob.ps1** 파일의 끝에 다음 내용을 추가하고 파일을 저장한 다음 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="308bb-144">이 cmdlet은 작업을 실행할 때 서버의 STDERR에 기록된 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="308bb-145">요약</span><span class="sxs-lookup"><span data-stu-id="308bb-145">Summary</span></span>

<span data-ttu-id="308bb-146">여기에서 볼 수 있듯이 Azure PowerShell은 HDInsight 클러스터에서 Hive 쿼리 실행 작업 상태를 모니터링하고, 출력을 검색하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="308bb-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="308bb-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="308bb-147">Next steps</span></span>

<span data-ttu-id="308bb-148">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="308bb-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="308bb-149">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="308bb-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="308bb-150">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="308bb-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="308bb-151">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="308bb-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="308bb-152">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="308bb-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
