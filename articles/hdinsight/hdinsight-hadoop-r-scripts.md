---
title: "HDInsight toocustomize 클러스터-Azure에서에서 R aaaUse | Microsoft Docs"
description: "자세한 방법을 스크립트 tooinstall R를 사용 하 여 동작 및 HDInsight 클러스터에서 R 사용 합니다."
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
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="af984-103">HDInsight Hadoop 클러스터에 R 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="af984-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="af984-104">Windows toocustomize r 스크립트 동작을 사용 하 여 HDInsight 클러스터에 기반 하는 방법 및 HDInsight의 R toouse 클러스터 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="af984-104">Learn how toocustomize Windows based HDInsight cluster with R using Script Action, and how toouse R on HDInsight clusters.</span></span> <span data-ttu-id="af984-105">hello [HDInsight 제공](https://azure.microsoft.com/pricing/details/hdinsight/) HDInsight 클러스터의 일부로 R 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-105">hello [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="af984-106">이렇게 하면 R 스크립트 toouse MapReduce 및 Spark distributed toorun 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-106">This allows R scripts toouse MapReduce and Spark toorun distributed computations.</span></span> <span data-ttu-id="af984-107">자세한 내용은 [HDInsight에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af984-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="af984-108">Linux 기반 클러스터와 함께 R을 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)](hdinsight-hadoop-r-scripts-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af984-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="af984-109">*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 R을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="af984-110">HDInsight 클러스터에서 샘플 스크립트 tooinstall R에서 읽기 전용 Azure 저장소 blob에서 사용할 수는 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-110">A sample script tooinstall R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="af984-111">**관련된 문서**</span><span class="sxs-lookup"><span data-stu-id="af984-111">**Related articles**</span></span>

* [<span data-ttu-id="af984-112">HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="af984-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="af984-113">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="af984-114">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="af984-115">HDInsight용 스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="af984-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="af984-116">R이란?</span><span class="sxs-lookup"><span data-stu-id="af984-116">What is R?</span></span>
<span data-ttu-id="af984-117">hello <a href="http://www.r-project.org/" target="_blank">for Statistical Computing R 프로젝트</a> 는 오픈 소스 언어 및 환경 통계 컴퓨팅입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-117">hello <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="af984-118">R은 수백 개의 통계 함수와 기능 및 개체 지향 프로그래밍의 측면을 결합하는 자체 프로그래밍 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="af984-119">또한 광범위한 그래픽 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="af984-120">R은 전문적인 통계학자 및 다양 한 필드에에서 과학자 hello 기본 프로그래밍 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-120">R is hello preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="af984-121">R은 Azure Blob 저장소(WASB)와 호환되므로 HDInsight의 R을 사용하여 이 저장소에 저장된 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="af984-122">R 설치</span><span class="sxs-lookup"><span data-stu-id="af984-122">Install R</span></span>
<span data-ttu-id="af984-123">A [샘플 스크립트](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R는 HDInsight 클러스터에는 Azure 저장소에 읽기 전용 blob에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="af984-124">이 섹션에서는 toouse hello Azure 포털을 사용 하 여 hello 클러스터를 만드는 동안 샘플 스크립트를 hello 하는 방법에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-124">This section provides instructions about how toouse hello sample script while creating hello cluster using hello Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="af984-125">hello 샘플 스크립트는 HDInsight 클러스터 버전이 3.1에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-125">hello sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="af984-126">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af984-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="af984-127">Hello 포털에서에서 하는 HDInsight 클러스터를 만들 때 클릭 **옵션 구성**, 클릭 하 고 **스크립트 동작**합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-127">When you create an HDInsight cluster from hello Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="af984-128">Hello에 **스크립트 동작** 페이지에서 다음 값에는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-128">On hello **Script Actions** page, enter hello following values:</span></span>

    <span data-ttu-id="af984-129">![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")</span><span class="sxs-lookup"><span data-stu-id="af984-129">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="af984-130">속성</span><span class="sxs-lookup"><span data-stu-id="af984-130">Property</span></span></th><th><span data-ttu-id="af984-131">값</span><span class="sxs-lookup"><span data-stu-id="af984-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="af984-132">이름</span><span class="sxs-lookup"><span data-stu-id="af984-132">Name</span></span></td>
            <td><span data-ttu-id="af984-133">예를 들어 hello 스크립트 동작의 이름을 지정 <b>R 설치</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-133">Specify a name for hello script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="af984-134">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="af984-134">Script URI</span></span></td>
            <td><span data-ttu-id="af984-135">예를 들어 호출 된 toocustomize hello 클러스터 있는 hello URI toohello 스크립트 지정 <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="af984-135">Specify hello URI toohello script that is invoked toocustomize hello cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="af984-136">노드 유형</span><span class="sxs-lookup"><span data-stu-id="af984-136">Node Type</span></span></td>
            <td><span data-ttu-id="af984-137">Hello 사용자 지정 스크립트가 실행 되는 hello 노드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="af984-138"><b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="af984-139">매개 변수</span><span class="sxs-lookup"><span data-stu-id="af984-139">Parameters</span></span></td>
            <td><span data-ttu-id="af984-140">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="af984-141">그러나, hello 스크립트 tooinstall R이을 비워 둘 수 있도록 매개 변수가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-141">However, hello script tooinstall R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="af984-142">Hello 클러스터에서 둘 이상의 스크립트 동작 tooinstall 여러 구성 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="af984-143">Hello 스크립트를 추가한 후에 hello 확인 표시가 toostart hello 클러스터를 만들 수 있는 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-143">After you have added hello scripts, click hello check mark toostart crating hello cluster.</span></span>

<span data-ttu-id="af984-144">Azure PowerShell 또는 hello HDInsight.NET SDK를 사용 하 여 HDInsight의 hello 스크립트 tooinstall R를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-144">You can also use hello script tooinstall R on HDInsight by using Azure PowerShell or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="af984-145">이 절차에 대한 자세한 내용은 이 문서의 뒷부분에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="af984-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="af984-146">R 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="af984-146">Run R scripts</span></span>
<span data-ttu-id="af984-147">이 섹션에서는 HDInsight와 toorun R 스크립트 hello Hadoop에 클러스터 되는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-147">This section describes how toorun an R script on hello Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="af984-148">**원격 데스크톱 연결 toohello 클러스터 설정**: hello 포털에서에서 R 설치를 사용 하 여 만든 hello 클러스터에 대 한 원격 데스크톱을 사용 하 고 다음 toohello 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-148">**Establish a Remote Desktop connection toohello cluster**: From hello Portal, enable Remote Desktop for hello cluster you created with R installed, and then connect toohello cluster.</span></span> <span data-ttu-id="af984-149">자세한 내용은 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-149">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="af984-150">**열기 hello R 콘솔**: hello R 설치 hello 헤드 노드의 hello 바탕 화면에서 링크 toohello R 콘솔을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-150">**Open hello R console**: hello R installation puts a link toohello R console on hello desktop of hello head node.</span></span> <span data-ttu-id="af984-151">클릭 하 여 조치 tooopen hello R 콘솔.</span><span class="sxs-lookup"><span data-stu-id="af984-151">Click on it tooopen hello R console.</span></span>
3. <span data-ttu-id="af984-152">**Hello R 스크립트 실행**: 붙여 넣어을 선택 하 고 ENTER 키를 눌러 여 hello R 콘솔에서 직접 hello R 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-152">**Run hello R script**: hello R script can be run directly from hello R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="af984-153">숫자 1 too100 hello를 생성 하 고 2로 곱하여 하는 간단한 예제 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af984-153">Here is a simple example script that generates hello numbers 1 too100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="af984-154">hello 처음 두 줄 호출 hello RHadoop 라이브러리 오른쪽과 함께 설치 된 hello 마지막 줄 인쇄 hello 결과 toohello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="af984-154">hello first two lines call hello RHadoop libraries that are installed with R. hello final line prints hello results toohello console.</span></span> <span data-ttu-id="af984-155">hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af984-155">hello output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="af984-156">Azure PowerShell을 사용하여 R 설치</span><span class="sxs-lookup"><span data-stu-id="af984-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="af984-157">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af984-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="af984-158">hello 샘플 방법을 tooinstall Azure PowerShell을 사용 하 여 Spark 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-158">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="af984-159">Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-159">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="af984-160">.NET SDK를 사용하여 R 설치</span><span class="sxs-lookup"><span data-stu-id="af984-160">Install R using .NET SDK</span></span>
<span data-ttu-id="af984-161">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af984-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="af984-162">hello 샘플 방법을 tooinstall Spark.NET SDK hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-162">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="af984-163">Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)합니다.</span><span class="sxs-lookup"><span data-stu-id="af984-163">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="af984-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="af984-164">See also</span></span>
* [<span data-ttu-id="af984-165">HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="af984-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="af984-166">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="af984-167">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="af984-168">HDInsight용 스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="af984-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="af984-169">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="af984-170">[HDInsight 클러스터에서 Giraph 설치](hdinsight-hadoop-giraph-install.md): Giraph 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="af984-171">[HDInsight 클러스터에서 Solr 설치](hdinsight-hadoop-solr-install-linux.md): Solr 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="af984-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
