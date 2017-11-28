---
title: "Azure HDInsight에서 Hadoop aaaRun hello 샘플 | Microsoft Docs"
description: "Hello Azure HDInsight 서비스를 사용 하 여 제공 된 hello 샘플을 시작 합니다. 또한 데이터 클러스터에 대해 MapReduce 프로그램을 실행하는 PowerShell 스크립트를 사용합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="1b76b-104">Windows 기반 HDInsight에서 Hadoop MapReduce 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="1b76b-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="1b76b-105">샘플 집합을 시작 하는 데 Azure HDInsight를 사용 하 여 Hadoop 클러스터에서 실행 중인 MapReduce 작업 toohelp을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-105">A set of samples are provided toohelp you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="1b76b-106">이 샘플에서 사용할 수 hello HDInsight의 각 관리 되는 클러스터를 만들면 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-106">These samples are made available on each of hello HDInsight managed clusters that you create.</span></span> <span data-ttu-id="1b76b-107">Azure PowerShell cmdlet toorun 작업을 사용 하 여 Hadoop 클러스터에 대해 설명 이러한 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-107">Running these samples familiarize you with using Azure PowerShell cmdlets toorun jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="1b76b-108">[**단어 개수**][hdinsight-sample-wordcount]: 텍스트 파일에 나오는 단어 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="1b76b-109">[**C#의 경우이 단어 개수를 스트리밍**][hdinsight-sample-csharp-streaming]: 사용 하 여 텍스트 파일에서 발생할 수 있는 개수 단어 hello Hadoop 스트리밍 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using hello Hadoop streaming interface.</span></span>
* <span data-ttu-id="1b76b-110">[**Pi 평가기**][hdinsight-sample-pi-estimator]: 통계를 사용 하 여 (준 Monte Carlo) pi 메서드 tooestimate hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span>
* <span data-ttu-id="1b76b-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: HDInsight를 사용하여 10GB 파일에 대해 일반적인 용도의 GraySort를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="1b76b-112">세 가지 작업 toorun: Teragen toogenerate hello 데이터, Terasort toosort hello 데이터 및 Teravalidate tooconfirm hello 데이터가 제대로 정렬 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-112">There are three jobs toorun: Teragen toogenerate hello data, Terasort toosort hello data, and Teravalidate tooconfirm that hello data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="1b76b-113">hello 소스 코드 hello 부록에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-113">hello source code can be found in hello Appendix.</span></span>

<span data-ttu-id="1b76b-114">MapReduce Java 기반 프로그래밍 및 스트리밍 및 Windows PowerShell에서 사용 되는 hello cmdlet에 대 한 설명서와 같은 Hadoop 관련 기술에 대 한 hello 웹 역할이 한 추가 문서는 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-114">Much additional documentation exists on hello web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about hello cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="1b76b-115">이러한 리소스에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b76b-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="1b76b-116">HDInsight의 Hadoop용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="1b76b-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="1b76b-117">HDInsight에서 Hadoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1b76b-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="1b76b-118">[소개 tooAzure HDInsight][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="1b76b-118">[Introduction tooAzure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="1b76b-119">오늘날에 많은 사람들이 MapReduce를 통한 Hive 및 Pig를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="1b76b-120">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b76b-120">For more information, see:</span></span>

* [<span data-ttu-id="1b76b-121">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="1b76b-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1b76b-122">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="1b76b-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="1b76b-123">**필수 조건**:</span><span class="sxs-lookup"><span data-stu-id="1b76b-123">**Prerequisites**:</span></span>

* <span data-ttu-id="1b76b-124">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="1b76b-124">**An Azure subscription**.</span></span> <span data-ttu-id="1b76b-125">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b76b-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1b76b-126">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="1b76b-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="1b76b-127">Hello 이러한 클러스터를 만들 수 있습니다는 다양 한 방법에 지침은 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-127">For instructions on hello various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="1b76b-128">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="1b76b-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1b76b-129">Azure 서비스 관리자를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="1b76b-130">Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-130">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1b76b-131">Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b76b-131">Follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="1b76b-132">해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-132">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="1b76b-133"><a name="hdinsight-sample-wordcount"></a>단어 개수 - Java</span><span class="sxs-lookup"><span data-stu-id="1b76b-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="1b76b-134">MapReduce 프로젝트 toosubmit 먼저 MapReduce 작업 정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-134">toosubmit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="1b76b-135">Hello 작업 정의에서 hello MapReduce 프로그램 jar 파일 및 있는 hello jar 파일의 hello 위치 지정 **wasb:///example/jars/hadoop-mapreduce-examples.jar**, 클래스 이름에 hello 및 hello 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-135">In hello job definition, you specify hello MapReduce program jar file and hello location of hello jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, hello class name, and hello arguments.</span></span>  <span data-ttu-id="1b76b-136">두 인수를 사용 하는 hello wordcount MapReduce 프로그램: hello 소스 파일을 사용 하는 toocount 단어 및 출력을 위한 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-136">hello wordcount MapReduce program takes two arguments: hello source file that is used toocount words, and hello location for output.</span></span>

<span data-ttu-id="1b76b-137">hello에서 hello 소스 코드를 확인할 수 있습니다 [부록 A](#apendix-a---the-word-count-MapReduce-program-in-java)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-137">hello source code can be found in hello [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="1b76b-138">Java MapReduce 개발 hello 프로시저에 대 한 프로그램의 경우 참조- [HDInsight에서 Hadoop에 대 한 개발 Java MapReduce 프로그램](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1b76b-138">For hello procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="1b76b-139">**toosubmit 단어 개수 MapReduce 작업**</span><span class="sxs-lookup"><span data-stu-id="1b76b-139">**toosubmit a word count MapReduce job**</span></span>

1. <span data-ttu-id="1b76b-140">**Windows PowerShell ISE**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="1b76b-141">자세한 내용은 [Azure PowerShell 설치 및 구성][powershell-install-configure]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b76b-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="1b76b-142">PowerShell 스크립트 뒤 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-142">Paste hello following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="1b76b-143">hello MapReduce 작업 파일을 생성 한 명명 된 *파트-r-00000*, 단어를 포함 하 고 hello를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-143">hello MapReduce job produces a file named *part-r-00000*, which contains words and hello counts.</span></span> <span data-ttu-id="1b76b-144">hello 스크립트 hello를 사용 하 여 **findstr** toolist hello 모든 단어를 명령에 포함 *"there"*합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-144">hello script uses hello **findstr** command toolist all hello words that contains *"there"*.</span></span>
3. <span data-ttu-id="1b76b-145">Hello 처음 세 개의 변수를 설정 하 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-145">Set hello first three variables, and run hello script.</span></span>

## <span data-ttu-id="1b76b-146"><a name="hdinsight-sample-csharp-streaming"></a>단어 개수 - C# 스트리밍</span><span class="sxs-lookup"><span data-stu-id="1b76b-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="1b76b-147">Hadoop 스트리밍 API tooMapReduce toowrite 지도 있고 Java 이외의 언어에서 함수를 줄이려면을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-147">Hadoop provides a streaming API tooMapReduce, which enables you toowrite map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="1b76b-148">이 자습서의 단계 hello만 tooWindows 기반 HDInsight 클러스터에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-148">hello steps in this tutorial apply only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="1b76b-149">Linux 기반 HDInsight 클러스터를 스트리밍하는 예제는 [HDInsight용 Python 스트리밍 프로그램 개발](hdinsight-hadoop-streaming-python.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b76b-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="1b76b-150">Hello 예제에서 hello 매퍼 및 리 듀 서 hello는 hello 입력에서 읽기를 실행 파일 [stdin] [ stdin-stdout-stderr] (줄-) 및 너무 hello 출력을 내보낼[stdout] [stdin-stdout-stderr].</span><span class="sxs-lookup"><span data-stu-id="1b76b-150">In hello example, hello mapper and hello reducer are executables that read hello input from [stdin][stdin-stdout-stderr] (line-by-line) and emit hello output too[stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="1b76b-151">hello 프로그램 hello 텍스트에서 모든 hello 단어 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-151">hello program counts all hello words in hello text.</span></span>

<span data-ttu-id="1b76b-152">실행 파일에 대 한 지정 된 경우 **매퍼**, hello 매퍼 초기화 될 때 각 매퍼 작업 hello 별도 프로세스로 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-152">When an executable is specified for **mappers**, each mapper task launches hello executable as a separate process when hello mapper is initialized.</span></span> <span data-ttu-id="1b76b-153">Hello 매퍼 작업을 실행 하 고을 입력 선으로 변환, 피드 hello 줄 toohello [stdin] [ stdin-stdout-stderr] hello 프로세스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-153">As hello mapper task runs, it converts its input into lines, and feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="1b76b-154">Hello에 그 동안 hello 매퍼 hello 기호로 출력에서에서 수집 hello 프로세스의 hello stdout 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-154">In hello meantime, hello mapper collects hello line-oriented output from hello stdout of hello process.</span></span> <span data-ttu-id="1b76b-155">각 줄의 hello 맵 편집기 hello 출력으로 수집 되는 키/값 쌍으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-155">It converts each line into a key/value pair, which is collected as hello output of hello mapper.</span></span> <span data-ttu-id="1b76b-156">기본적으로 toohello 첫 번째 탭 문자를 줄의 hello 접두사 hello 키 이며 hello 줄 (탭 문자 hello 제외)의 hello 나머지는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-156">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span> <span data-ttu-id="1b76b-157">Hello 줄에 탭 문자가 없으면 전체 줄 hello 키로 간주 됩니다 및 hello 값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-157">If there is no Tab character in hello line, entire line is considered as hello key, and hello value is null.</span></span>

<span data-ttu-id="1b76b-158">실행 파일에 대 한 지정 된 경우 **이경소켓**, hello 리 듀 서 초기화 될 때 각 리 듀 서 작업 hello 별도 프로세스로 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-158">When an executable is specified for **reducers**, each reducer task launches hello executable as a separate process when hello reducer is initialized.</span></span> <span data-ttu-id="1b76b-159">Hello 리 듀 서 작업을 실행 하 고 해당 입력된 키/값 쌍 선으로 변환 하 고 hello 줄 toohello 피드를 [stdin] [ stdin-stdout-stderr] hello 프로세스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-159">As hello reducer task runs, it converts its input key/values pairs into lines, and it feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="1b76b-160">Hello에 그 동안 hello 리 듀 서 hello 기호로 출력에서에서 수집 hello [stdout] [ stdin-stdout-stderr] hello 프로세스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-160">In hello meantime, hello reducer collects hello line-oriented output from hello [stdout][stdin-stdout-stderr] of hello process.</span></span> <span data-ttu-id="1b76b-161">Hello 리 듀 서의 hello 출력으로 수집 하는 각 줄 tooa 키/값 쌍으로 변환.</span><span class="sxs-lookup"><span data-stu-id="1b76b-161">It converts each line tooa key/value pair, which is collected as hello output of hello reducer.</span></span> <span data-ttu-id="1b76b-162">기본적으로 toohello 첫 번째 탭 문자를 줄의 hello 접두사 hello 키 이며 hello 줄 (탭 문자 hello 제외)의 hello 나머지는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-162">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span>

<span data-ttu-id="1b76b-163">**C# toosubmit 스트리밍 단어 개수 작업**</span><span class="sxs-lookup"><span data-stu-id="1b76b-163">**toosubmit a C# streaming word count job**</span></span>

* <span data-ttu-id="1b76b-164">Hello 절차에 따라 [단어 수-Java](#word-count-java), 다음 줄 hello hello 작업 정의 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-164">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="1b76b-165">hello 출력 파일 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-165">hello output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="1b76b-166"><a name="hdinsight-sample-pi-estimator"></a>PI 추정</span><span class="sxs-lookup"><span data-stu-id="1b76b-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="1b76b-167">hello pi 평가기를 사용 하 여 통계 (준 Monte Carlo) pi 메서드 tooestimate hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-167">hello pi estimator uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="1b76b-168">포인트 단위 내부의 임의로 사각형 감소 시킬 수도 hello 원의 확률 같은 toohello 영역이 있는 해당 사각형 내에서 새겨진 원 안에 pi/4입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="1b76b-169">여기서 R은 hello 원 toohello hello 사각형 내에 있는 요소의 총 수 내에 있는 점의 hello 수의 hello 비율 4R의 hello 값에서 pi의 hello 값을 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-169">hello value of pi can be estimated from hello value of 4R, where R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="1b76b-170">hello 큰 hello 샘플 사용 하는 지점의 hello 더 나은 hello 예상 값은입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-170">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="1b76b-171">이 샘플에 제공 된 hello 스크립트 Hadoop jar 작업을 제출 하 고 16 맵, 각각은 hello 매개 변수 값에 따라 필요한 toocompute 10 백만 샘플 포인트를 값으로 toorun 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-171">hello script provided for this sample submits a Hadoop jar job and is set up toorun with a value 16 maps, each of which is required toocompute 10 million sample points by hello parameter values.</span></span> <span data-ttu-id="1b76b-172">Pi의 tooimprove hello 예상 값을 변경 하는 이러한 매개 변수 값이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-172">These parameter values can be changed tooimprove hello estimated value of pi.</span></span> <span data-ttu-id="1b76b-173">참조용으로 hello pi의 처음 10 개의 소수 자릿수는 3.1415926535 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-173">For reference, hello first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="1b76b-174">**toosubmit pi 평가기 작업**</span><span class="sxs-lookup"><span data-stu-id="1b76b-174">**toosubmit a pi estimator job**</span></span>

* <span data-ttu-id="1b76b-175">Hello 절차에 따라 [단어 수-Java](#word-count-java), 다음 줄 hello hello 작업 정의 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-175">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="1b76b-176"><a name="hdinsight-sample-10gb-graysort"></a>10GB Graysort</span><span class="sxs-lookup"><span data-stu-id="1b76b-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="1b76b-177">이 샘플에서는 비교적 빠르게 실행할 수 있도록 적절한 10GB의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="1b76b-178">Hello MapReduce Owen O'Malley 및 hello 연간 범용 ("daytona") 테라바이트 정렬 벤치 마크 0.578 TB/min (173 분에서 100TB)의 속도와 2009 년에 성공한 Arun Murthy에서 개발 된 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-178">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy that won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="1b76b-179">이 및 다른 정렬 벤치 마크에 대 한 자세한 내용은 참조 hello [Sortbenchmark](http://sortbenchmark.org/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-179">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="1b76b-180">이 샘플에서는 세 가지 집합의 MapReduce 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="1b76b-181">**TeraGen** 는 MapReduce 프로그램의 데이터 toosort toogenerate hello 행을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-181">**TeraGen** is a MapReduce program that you can use toogenerate hello rows of data toosort.</span></span>
2. <span data-ttu-id="1b76b-182">**TeraSort** hello 입력된 데이터를 샘플링 하 고 MapReduce toosort hello 데이터를 사용 하 여 총 주문으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-182">**TeraSort** samples hello input data and uses MapReduce toosort hello data into a total order.</span></span> <span data-ttu-id="1b76b-183">TeraSort는 MapReduce 함수 hello 각 reduce에 대 한 키 범위를 정의 하는 샘플링 N-1 키의 정렬 된 목록을 사용 하는 사용자 지정 파티 셔 너 제외 하 고 표준 정렬입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="1b76b-184">특히, 모든 키 이러한 샘플 [i-1] < = k e y < 샘플 [i] tooreduce 보내집니다 i.</span><span class="sxs-lookup"><span data-stu-id="1b76b-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="1b76b-185">이 hello 출력의 감소할 i 보장은 hello 출력을 줄이려면 i + 1 보다 작은 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-185">This guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>
3. <span data-ttu-id="1b76b-186">**TeraValidate** 해당 hello 출력의 유효성을 검사 하는 MapReduce 프로그램 전역적으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-186">**TeraValidate** is a MapReduce program that validates that hello output is globally sorted.</span></span> <span data-ttu-id="1b76b-187">파일당 하나의 맵 hello 출력 디렉터리에 생성 하 고 각 지도 사용 하면 각 키 보다 작거나 같은 toohello 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-187">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="1b76b-188">hello 맵 함수 생성의 hello 레코드 먼저 및 각 파일과 hello의 마지막 키 reduce 함수 해당 hello를 사용 하면 i 파일의 첫 번째 키 파일 i-1의 마지막 키 hello 보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-188">hello map function also generates records of hello first and last keys of each file, and hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="1b76b-189">Hello의 출력으로 모든 문제가 보고의 순서가 hello 키를 가진 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-189">Any problems are reported as an output of hello reduce with hello keys that are out of order.</span></span>

<span data-ttu-id="1b76b-190">hello 입력 및 출력 형식으로 모든 세 개의 응용 프로그램에서 사용 하는 hello 텍스트 파일에 있는 읽고 쓰는 hello 올바른 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-190">hello input and output format, used by all three applications, reads and writes hello text files in hello right format.</span></span> <span data-ttu-id="1b76b-191">hello의 hello 출력 줄일가 복제 설정 hello 기본값 3, 대신 too1 hello 벤치 마크 콘테스트 toomultiple 노드에 hello 출력 데이터를 복제 하는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-191">hello output of hello reduce has replication set too1, instead of hello default 3, because hello benchmark contest does not require that hello output data be replicated on toomultiple nodes.</span></span>

<span data-ttu-id="1b76b-192">Hello 소개에 설명 된 hello MapReduce 프로그램의 각 해당 tooone hello 샘플에서 세 가지 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-192">Three tasks are required by hello sample, each corresponding tooone of hello MapReduce programs described in hello introduction:</span></span>

1. <span data-ttu-id="1b76b-193">Hello를 실행 하 여 정렬에 대 한 hello 데이터 생성 **TeraGen** MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-193">Generate hello data for sorting by running hello **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="1b76b-194">Hello를 실행 하 여 hello 데이터 정렬 **TeraSort** MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-194">Sort hello data by running hello **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="1b76b-195">Hello를 실행 하 여 hello 데이터가 제대로 정렬 되어 있는지 확인 **TeraValidate** MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-195">Confirm that hello data has been correctly sorted by running hello **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="1b76b-196">**toosubmit hello 작업**</span><span class="sxs-lookup"><span data-stu-id="1b76b-196">**toosubmit hello jobs**</span></span>

* <span data-ttu-id="1b76b-197">Hello 절차에 따라 [단어 수-Java](#word-count-java)를 사용 하 여 hello 작업 정의 따라:</span><span class="sxs-lookup"><span data-stu-id="1b76b-197">Follow hello procedure in [Word count - Java](#word-count-java), and use hello following job definitions:</span></span>

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a><span data-ttu-id="1b76b-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b76b-198">Next steps</span></span>
<span data-ttu-id="1b76b-199">이 문서 및 각 hello 샘플의 hello 문서에서 어떻게 toorun hello 샘플에 포함 된 hello HDInsight 클러스터에 Azure PowerShell을 사용 하 여 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-199">From this article and hello articles in each of hello samples, you learned how toorun hello samples included with hello HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="1b76b-200">HDInsight Pig, Hive, 및 MapReduce 사용에 대 한 자습서, hello 다음 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1b76b-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="1b76b-201">[HDInsight tooanalyze 모바일 송수화기 사용 중인 Hadoop 하이브 사용을 시작.][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1b76b-201">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="1b76b-202">[HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1b76b-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1b76b-203">[HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1b76b-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1b76b-204">[HDInsight에서 Hadoop 작업 제출][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="1b76b-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="1b76b-205">[Azure HDInsight SDK 설명서][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="1b76b-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---hello-word-count-source-code"></a><span data-ttu-id="1b76b-206">부록 A-hello 단어 개수 소스 코드</span><span class="sxs-lookup"><span data-stu-id="1b76b-206">Appendix A - hello Word count source code</span></span>

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---hello-word-count-streaming-source-code"></a><span data-ttu-id="1b76b-207">부록 B-소스 코드를 스트리밍 hello 단어 개수</span><span class="sxs-lookup"><span data-stu-id="1b76b-207">Appendix B - hello word count streaming source code</span></span>
<span data-ttu-id="1b76b-208">hello MapReduce 프로그램을 hello 단어 문서에서 스트리밍 인터페이스 toocount hello 수를 줄일 hello cat.exe 응용 프로그램 매핑 인터페이스 toostream hello 텍스트로 hello 콘솔로 및 hello wc.exe 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-208">hello MapReduce program uses hello cat.exe application as a mapping interface toostream hello text into hello console and hello wc.exe application as hello reduce interface toocount hello number of words that are streamed from a document.</span></span> <span data-ttu-id="1b76b-209">Hello 매퍼 및 리 듀 서 모두 hello 표준 입력 스트림에서 (stdin) 문자를 줄 단위로 읽고 toohello 표준 출력 스트림에 (stdout)를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-209">Both hello mapper and reducer read characters, line-by-line, from hello standard input stream (stdin) and write toohello standard output stream (stdout).</span></span>

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

<span data-ttu-id="1b76b-210">hello hello cat.cs 파일 사용 하 여에서 코드 맵 편집기는 [StreamReader] [ streamreader] tooread hello 자의 hello 들어오는 스트림 toohello 콘솔에 기록 합니다 hello 스트림 toohello 표준 출력 스트림에 개체 정적 hello로 [Console.Writeline] [ console-writeline] 메서드.</span><span class="sxs-lookup"><span data-stu-id="1b76b-210">hello mapper code in hello cat.cs file uses a [StreamReader][streamreader] object tooread hello characters of hello incoming stream toohello console, which then writes hello stream toohello standard output stream with hello static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

<span data-ttu-id="1b76b-211">hello wc.cs 파일 사용의 리 듀 서 코드 hello는 [StreamReader] [ streamreader] tooread 문자 hello 표준 입력 스트림에서 hello cat.exe 맵 편집기에서 출력 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-211">hello reducer code in hello wc.cs file uses a [StreamReader][streamreader]   object tooread characters from hello standard input stream that have been output by hello cat.exe mapper.</span></span> <span data-ttu-id="1b76b-212">Hello로 hello 문자를 읽을 때 [Console.Writeline] [ console-writeline] 메서드를 계산 hello 단어 공백 및 줄 끝 문자 각 단어 hello 계산 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-212">As it reads hello characters with hello [Console.Writeline][console-writeline] method, it counts hello words by counting spaces and end-of-line characters at hello end of each word.</span></span> <span data-ttu-id="1b76b-213">그런 다음 hello로 hello 총 toohello 표준 출력 스트림에 기록 [Console.Writeline] [ console-writeline] 메서드.</span><span class="sxs-lookup"><span data-stu-id="1b76b-213">It then writes hello total toohello standard output stream with hello [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---hello-pi-estimator-source-code"></a><span data-ttu-id="1b76b-214">부록 C-hello Pi 평가기 소스 코드</span><span class="sxs-lookup"><span data-stu-id="1b76b-214">Appendix C - hello Pi estimator source code</span></span>
<span data-ttu-id="1b76b-215">hello pi 평가기 hello 매퍼 및 리 듀 서 함수를 포함 하는 Java 코드는 아래 검사 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-215">hello pi estimator Java code that contains hello mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="1b76b-216">hello 매퍼 프로그램은 지정 된 된 수의 단위 정사각형 내의 임의로 배치 하는 요소를 생성 하 고 hello hello 원 안에 있는 해당 지점 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-216">hello mapper program generates a specified number of points placed at random inside of a unit square and then counts hello number of those points that are inside hello circle.</span></span> <span data-ttu-id="1b76b-217">hello 리 듀 서 프로그램 누적 포인트 hello 매퍼도 계산 되 고 여기서 R은 내부 hello 원 toohello hello 사각형 내에 있는 요소의 총 수를 계산 하는 지점의 hello 수의 hello 비율 hello 수식 4R에서 pi의 hello 값을 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-217">hello reducer program accumulates points counted by hello mappers and then estimates hello value of pi from hello formula 4R, where R is hello ratio of hello number of points counted inside hello circle toohello total number of points that are within hello square.</span></span>

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a><span data-ttu-id="1b76b-218">부록 D-hello 10gb graysort 소스 코드</span><span class="sxs-lookup"><span data-stu-id="1b76b-218">Appendix D - hello 10gb graysort source code</span></span>
<span data-ttu-id="1b76b-219">hello TeraSort MapReduce 프로그램에 대 한 hello 코드는이 섹션의 검사 하기 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76b-219">hello code for hello TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
