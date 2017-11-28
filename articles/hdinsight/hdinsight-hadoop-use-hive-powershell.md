---
title: "powershell에서 Azure HDInsight Hadoop 하이브 aaaUse | Microsoft Docs"
description: "HDInsight의 Hadoop에서 PowerShell toorun 하이브 쿼리를 사용 합니다."
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
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="d3cd0-103">PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="d3cd0-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="d3cd0-104">이 문서에서 HDInsight 클러스터에서 Hadoop hello Azure 리소스 그룹 모드 toorun 하이브 쿼리에에서 Azure PowerShell을 사용 하는 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d3cd0-105">이 문서는 hello 예제에서 사용 하는 hello HiveQL 문을 수행할 작업에 대 한 자세한 설명을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="d3cd0-106">이 예제에 사용 되는 HiveQL hello에 대 한 자세한 내용은 참조 [HDInsight에서 Hadoop으로 사용 하 여 하이브](hdinsight-use-hive.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="d3cd0-107">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="d3cd0-107">**Prerequisites**</span></span>

* <span data-ttu-id="d3cd0-108">**Azure HDInsight 클러스터**: hello 클러스터는 Windows 여부는 중요 하지 않습니다 또는 Linux 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d3cd0-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d3cd0-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d3cd0-111">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="d3cd0-112">Azure PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="d3cd0-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="d3cd0-113">Azure PowerShell에는 *cmdlet* HDInsight의 Hive 쿼리 실행 tooremotely 있습니다 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="d3cd0-114">내부적으로 hello cmdlet 확인 REST 호출 너무[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="d3cd0-115">hello 다음 cmdlet은 사용 되는 원격 HDInsight 클러스터에서 하이브 쿼리를 실행 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="d3cd0-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="d3cd0-116">**추가 AzureRmAccount**: Azure PowerShell 인증 tooyour Azure 구독</span><span class="sxs-lookup"><span data-stu-id="d3cd0-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="d3cd0-117">**새 AzureRmHDInsightHiveJobDefinition**: 만듭니다는 *작업 정의* hello를 사용 하 여 HiveQL 문은 지정 된</span><span class="sxs-lookup"><span data-stu-id="d3cd0-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="d3cd0-118">**시작 AzureRmHDInsightJob**: hello 작업 정의 tooHDInsight hello 작업을 시작 보내고 반환 된 *작업* hello 작업의 사용된 toocheck hello 상태가 될 수 있는 개체</span><span class="sxs-lookup"><span data-stu-id="d3cd0-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="d3cd0-119">**대기 AzureRmHDInsightJob**: hello 작업의 hello 작업 개체 toocheck hello 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="d3cd0-120">Hello 대기 시간을 초과 하거나 hello 작업이 완료 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="d3cd0-121">**Get AzureRmHDInsightJobOutput**: hello 작업의 tooretrieve hello 출력 사용</span><span class="sxs-lookup"><span data-stu-id="d3cd0-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="d3cd0-122">**호출 AzureRmHDInsightHiveJob**: toorun HiveQL 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="d3cd0-123">이 cmdlet 블록 hello 쿼리 완료 된 후 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="d3cd0-124">**사용 하 여 AzureRmHDInsightCluster**: 집합 hello hello에 대 한 현재 클러스터 toouse **Invoke AzureRmHDInsightHiveJob** 명령</span><span class="sxs-lookup"><span data-stu-id="d3cd0-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="d3cd0-125">hello 다음 단계 설명 방법을 toouse 이러한 cmdlet toorun HDInsight 클러스터에서 작업:</span><span class="sxs-lookup"><span data-stu-id="d3cd0-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="d3cd0-126">코드를 다음 hello 저장의 편집기를 사용 하 여 **hivejob.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="d3cd0-127">새 **Azure PowerShell** 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="d3cd0-128">Hello의 디렉터리 toohello 위치를 변경 **hivejob.ps1** 파일을 다음 명령 toorun hello 스크립트 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d3cd0-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="d3cd0-129">Hello 스크립트를 실행 하는 경우 메시지 표시 tooenter hello 클러스터 이름 및 hello HTTPS/관리자 계정 자격 증명 hello 클러스터에 대 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="d3cd0-130">Tooyour Azure 구독에서에서 메시지 표시 toolog 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="d3cd0-131">Hello 작업이 완료 되 면 정보 비슷한 toohello를 thext 다음 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="d3cd0-132">앞에서 설명한 것 처럼 **Invoke-hive** 사용된 toorun 쿼리일 수 있으며 hello 응답을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="d3cd0-133">다음 스크립트 toosee Invoke-hive의 작동 원리 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="d3cd0-134">hello 출력 텍스트 다음 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="d3cd0-135">HiveQL 쿼리가 길면에 대 한 hello Azure PowerShell을 사용할 수 있습니다 **Here-string** cmdlet 또는 HiveQL 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="d3cd0-136">조각과 방법을 따르는 hello toouse hello **Invoke-hive** cmdlet toorun HiveQL 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="d3cd0-137">hello HiveQL 스크립트 파일이 있어야 업로드할 toowasb: / /입니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="d3cd0-138">**Here-Strings**에 대한 자세한 내용은 <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Windows PowerShell Here-Strings 사용</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d3cd0-139">문제 해결</span><span class="sxs-lookup"><span data-stu-id="d3cd0-139">Troubleshooting</span></span>

<span data-ttu-id="d3cd0-140">정보가 없는 hello 작업이 완료 되었을 때 반환 되 면 처리 하는 동안 오류가 발생 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="d3cd0-141">이 작업에 대 한 오류 정보 tooview 추가 toohello의 끝 다음 hello hello **hivejob.ps1** 파일을 저장 하 고 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="d3cd0-142">이 cmdlet는 hello 작업을 실행할 때 tooSTDERR hello 서버에 작성 된 hello 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="d3cd0-143">요약</span><span class="sxs-lookup"><span data-stu-id="d3cd0-143">Summary</span></span>

<span data-ttu-id="d3cd0-144">볼 수 있듯이 Azure PowerShell HDInsight 클러스터에서 하이브 쿼리에 쉽게 toorun에는, 모니터 hello 상태, 작업 및 hello 출력을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3cd0-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3cd0-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3cd0-145">Next steps</span></span>

<span data-ttu-id="d3cd0-146">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="d3cd0-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="d3cd0-147">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="d3cd0-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="d3cd0-148">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="d3cd0-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d3cd0-149">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="d3cd0-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d3cd0-150">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="d3cd0-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
