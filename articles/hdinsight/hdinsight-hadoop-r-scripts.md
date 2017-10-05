---
title: "HDInsight에서 R을 사용하여 클러스터 사용자 지정 - Azure | Microsoft Docs"
description: "스크립트 동작을 사용하여 R을 설치하는 방법을 알아보고 HDInsight 클러스터에서 R을 사용합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="d4b22-103">HDInsight Hadoop 클러스터에 R 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="d4b22-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="d4b22-104">스크립트 동작을 사용하여 R로 Windows 기반 HDInsight 클러스터를 사용자 지정하는 방법 및 HDInsight 클러스터에서 R을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="d4b22-105">[HDInsight 제품](https://azure.microsoft.com/pricing/details/hdinsight/)에는 HDInsight 클러스터의 일부로 R Server가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="d4b22-106">이를 통해 R 스크립트에서 MapReduce 및 Spark를 사용하여 분산된 계산을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="d4b22-107">자세한 내용은 [HDInsight에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4b22-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="d4b22-108">Linux 기반 클러스터와 함께 R을 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)](hdinsight-hadoop-r-scripts-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4b22-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="d4b22-109">*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 R을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="d4b22-110">HDInsight 클러스터에 R을 설치하는 샘플 스크립트는 읽기 전용 Azure 저장소 Blob( [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1))에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="d4b22-111">**관련된 문서**</span><span class="sxs-lookup"><span data-stu-id="d4b22-111">**Related articles**</span></span>

* [<span data-ttu-id="d4b22-112">HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="d4b22-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="d4b22-113">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="d4b22-114">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="d4b22-115">HDInsight용 스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="d4b22-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="d4b22-116">R이란?</span><span class="sxs-lookup"><span data-stu-id="d4b22-116">What is R?</span></span>
<span data-ttu-id="d4b22-117"><a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a>은 통계 계산을 위한 오픈 소스 언어 및 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="d4b22-118">R은 수백 개의 통계 함수와 기능 및 개체 지향 프로그래밍의 측면을 결합하는 자체 프로그래밍 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="d4b22-119">또한 광범위한 그래픽 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="d4b22-120">R은 다양한 분야에서 전문 통계학자와 과학자 대부분의 기본 프로그래밍 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="d4b22-121">R은 Azure Blob 저장소(WASB)와 호환되므로 HDInsight의 R을 사용하여 이 저장소에 저장된 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="d4b22-122">R 설치</span><span class="sxs-lookup"><span data-stu-id="d4b22-122">Install R</span></span>
<span data-ttu-id="d4b22-123">HDInsight 클러스터에 R을 설치하기 위한 [샘플 스크립트](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) 는 Azure 저장소의 읽기 전용 Blob에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="d4b22-124">이 섹션에서는 Azure 포털을 사용하여 클러스터를 만드는 동안 샘플 스크립트를 사용하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d4b22-125">샘플 스크립트는 HDInsight 클러스터 버전 3.1에서 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="d4b22-126">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4b22-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="d4b22-127">Azure Portal에서 HDInsight 클러스터를 만드는 경우 **선택적 구성**, **스크립트 동작**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="d4b22-128">**스크립트 동작** 페이지에서 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="d4b22-129">![스크립트 작업을 사용하여 클러스터 사용자 지정](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "스크립트 작업을 사용하여 클러스터 사용자 지정")</span><span class="sxs-lookup"><span data-stu-id="d4b22-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d4b22-130">속성</span><span class="sxs-lookup"><span data-stu-id="d4b22-130">Property</span></span></th><th><span data-ttu-id="d4b22-131">값</span><span class="sxs-lookup"><span data-stu-id="d4b22-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d4b22-132">이름</span><span class="sxs-lookup"><span data-stu-id="d4b22-132">Name</span></span></td>
            <td><span data-ttu-id="d4b22-133">스크립트 동작의 이름(예: <b>Install R</b>)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="d4b22-134">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="d4b22-134">Script URI</span></span></td>
            <td><span data-ttu-id="d4b22-135">클러스터를 사용자 지정하기 위해 호출되는 스크립트에 대한 URI(예: <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i>)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="d4b22-136">노드 유형</span><span class="sxs-lookup"><span data-stu-id="d4b22-136">Node Type</span></span></td>
            <td><span data-ttu-id="d4b22-137">사용자 지정 스크립트가 실행되는 노드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="d4b22-138"><b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="d4b22-139">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d4b22-139">Parameters</span></span></td>
            <td><span data-ttu-id="d4b22-140">스크립트에 필요한 경우 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="d4b22-141">그러나 R을 설치하는 스크립트는 매개 변수가 필요하지 않으므로 공백으로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="d4b22-142">두 개 이상의 스크립트 작업을 추가하여 클러스터에 여러 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="d4b22-143">스크립트를 추가한 후 확인 표시를 클릭하여 클러스터 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="d4b22-144">스크립트를 사용하여 Azure PowerShell 또는 HDInsight.NET SDK로 HDInsight에 R을 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="d4b22-145">이 절차에 대한 자세한 내용은 이 문서의 뒷부분에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="d4b22-146">R 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="d4b22-146">Run R scripts</span></span>
<span data-ttu-id="d4b22-147">이 섹션에서는 HDInsight를 사용하는 Hadoop 클러스터에서 R 스크립트를 실행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="d4b22-148">**클러스터에 대한 원격 데스크톱 연결 설정**: 포털에서 R을 설치하여 만든 클러스터에 대해 원격 데스크톱을 사용하도록 설정한 다음 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="d4b22-149">지침은 [RDP를 사용하여 HDInsight 클러스터에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4b22-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="d4b22-150">**R 콘솔 열기**: R 설치에서는 R 콘솔에 대한 링크를 헤드 노드의 데스크톱에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="d4b22-151">이 링크를 클릭하여 R 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="d4b22-152">**R 스크립트 실행**: R 콘솔에서 R 스크립트를 붙여 넣고 선택한 후 Enter 키를 눌러 콘솔에서 직접 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="d4b22-153">다음은 1에서 100까지의 숫자를 생성한 후 각 숫자에 2를 곱하는 간단한 예제 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="d4b22-154">첫 번째 두 줄은 R이 설치된 RHadoop 라이브러리를 호출하고, 마지막 줄은 결과를 콘솔에 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="d4b22-155">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="d4b22-156">Azure PowerShell을 사용하여 R 설치</span><span class="sxs-lookup"><span data-stu-id="d4b22-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="d4b22-157">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4b22-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="d4b22-158">샘플은 Azure PowerShell을 사용하여 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="d4b22-159">스크립트를 사용자 지정하여 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="d4b22-160">.NET SDK를 사용하여 R 설치</span><span class="sxs-lookup"><span data-stu-id="d4b22-160">Install R using .NET SDK</span></span>
<span data-ttu-id="d4b22-161">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4b22-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="d4b22-162">샘플은 .NET SDK를 사용하여 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="d4b22-163">스크립트를 사용자 지정하여 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="d4b22-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d4b22-164">See also</span></span>
* [<span data-ttu-id="d4b22-165">HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="d4b22-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="d4b22-166">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="d4b22-167">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="d4b22-168">HDInsight용 스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="d4b22-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="d4b22-169">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="d4b22-170">[HDInsight 클러스터에서 Giraph 설치](hdinsight-hadoop-giraph-install.md): Giraph 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="d4b22-171">[HDInsight 클러스터에서 Solr 설치](hdinsight-hadoop-solr-install-linux.md): Solr 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d4b22-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
