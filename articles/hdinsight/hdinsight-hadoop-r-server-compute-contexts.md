---
title: "HDInsight에서 R Server의 계산 컨텍스트 옵션 - Azure | Microsoft Docs"
description: "HDInsight에서 R Server 사용자에게 제공되는 다양한 계산 컨텍스트 옵션에 대해 알아봅니다."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 47f4441612be4f363ba82cc22b09786a6f3bfdc3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a><span data-ttu-id="71b2c-103">HDInsight에서 R 서버의 계산 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="71b2c-103">Compute context options for R Server on HDInsight</span></span>

<span data-ttu-id="71b2c-104">Azure HDInsight의 Microsoft R Server는 계산 컨텍스트를 설정하여 호출을 실행하는 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-104">Microsoft R Server on Azure HDInsight controls how calls are executed by setting the compute context.</span></span> <span data-ttu-id="71b2c-105">이 문서에서는 에지 노드 또는 HDInsight 클러스터의 코어에서 실행 병렬 처리 여부 및 방법을 지정하기 위해 사용할 수 있는 옵션을 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-105">This article outlines the options that are available to specify whether and how execution is parallelized across cores of the edge node or HDInsight cluster.</span></span>

<span data-ttu-id="71b2c-106">클러스터의 에지 노드는 클러스터에 연결하고 R 스크립트를 실행하는 데 편리한 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-106">The edge node of a cluster provides a convenient place to connect to the cluster and to run your R scripts.</span></span> <span data-ttu-id="71b2c-107">에지 노드를 사용하는 경우 에지 노드 서버의 코어에서 ScaleR의 병렬화된 분산 함수를 실행하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-107">With an edge node, you have the option of running the parallelized distributed functions of ScaleR across the cores of the edge node server.</span></span> <span data-ttu-id="71b2c-108">또한 ScaleR의 Hadoop Map Reduce 또는 Spark 계산 컨텍스트를 사용하여 클러스터의 노드에서 함수를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-108">You can also run them across the nodes of the cluster by using ScaleR’s Hadoop Map Reduce or Spark compute contexts.</span></span>

## <a name="microsoft-r-server-on-azure-hdinsight"></a><span data-ttu-id="71b2c-109">Azure HDInsight의 Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="71b2c-109">Microsoft R Server on Azure HDInsight</span></span>
<span data-ttu-id="71b2c-110">[Azure HDInsight의 Microsoft R Server](hdinsight-hadoop-r-server-overview.md)는 R 기반 분석을 위한 최신 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-110">[Microsoft R Server on Azure HDInsight](hdinsight-hadoop-r-server-overview.md) provides the latest capabilities for R-based analytics.</span></span> <span data-ttu-id="71b2c-111">[Azure Blob](../storage/common/storage-introduction.md "Azure Blob Storage") 저장소 계정, Data Lake Store 또는 로컬 Linux 파일 시스템에 있는 컨테이너에 저장된 HDFS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-111">It can use data that is stored in an HDFS container in your [Azure Blob](../storage/common/storage-introduction.md "Azure Blob storage") storage account, a Data Lake store, or the local Linux file system.</span></span> <span data-ttu-id="71b2c-112">R Server가 오픈 소스 R을 기반으로 하기 때문에 빌드한 R 기반 응용 프로그램은 8000개 이상의 오픈 소스 R 패키지를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-112">Since R Server is built on open source R, the R-based applications you build can apply any of the 8000+ open source R packages.</span></span> <span data-ttu-id="71b2c-113">R Server와 함께 포함된 Microsoft의 빅 데이터 분석 패키지인 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)에서 루틴을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-113">They can also use the routines in [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), Microsoft’s big data analytics package that is included with R Server.</span></span>  

## <a name="compute-contexts-for-an-edge-node"></a><span data-ttu-id="71b2c-114">에지 노드에 대한 계산 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="71b2c-114">Compute contexts for an edge node</span></span>
<span data-ttu-id="71b2c-115">일반적으로 에지 노드의 R 서버에서 실행되는 R 스크립트는 해당 노드의 R 인터프리터 내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-115">In general, an R script that's run in R Server on the edge node runs within the R interpreter on that node.</span></span> <span data-ttu-id="71b2c-116">예외는 ScaleR 함수를 호출하는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-116">The exceptions are those steps that call a ScaleR function.</span></span> <span data-ttu-id="71b2c-117">ScaleR 호출은 ScaleR 계산 컨텍스트를 설정하는 방법에 따라 결정된 계산 환경에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-117">The ScaleR calls run in a compute environment that is determined by how you set the ScaleR compute context.</span></span>  <span data-ttu-id="71b2c-118">에지 노드에서 R 스크립트 실행 시 계산 컨텍스트의 가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-118">When you run your R script from an edge node, the possible values of the compute context are:</span></span>

- <span data-ttu-id="71b2c-119">로컬 순차(*‘local’*)</span><span class="sxs-lookup"><span data-stu-id="71b2c-119">local sequential (*‘local’*)</span></span>
- <span data-ttu-id="71b2c-120">로컬 병렬(*‘localpar’*)</span><span class="sxs-lookup"><span data-stu-id="71b2c-120">local parallel (*‘localpar’*)</span></span>
- <span data-ttu-id="71b2c-121">Map Reduce</span><span class="sxs-lookup"><span data-stu-id="71b2c-121">Map Reduce</span></span>
- <span data-ttu-id="71b2c-122">Spark</span><span class="sxs-lookup"><span data-stu-id="71b2c-122">Spark</span></span>

<span data-ttu-id="71b2c-123">*‘local’* 및 *‘localpar’* 옵션은 **rxExec** 호출 실행 방법에 따라서만 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-123">The *‘local’* and *‘localpar’* options differ only in how **rxExec** calls are executed.</span></span> <span data-ttu-id="71b2c-124">이러한 두 옵션은 ScaleR **numCoresToUse** 옵션(예: `rxOptions(numCoresToUse=6)`)을 사용하여 다르게 지정하지 않는 한, 사용 가능한 모든 코어에서 병렬 방식으로 다른 rx-function 호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-124">They both execute other rx-function calls in a parallel manner across all available cores unless specified otherwise through use of the ScaleR **numCoresToUse** option, for example `rxOptions(numCoresToUse=6)`.</span></span> <span data-ttu-id="71b2c-125">병렬 실행 옵션은 최적의 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-125">Parallel execution options offer optimal performance.</span></span>

<span data-ttu-id="71b2c-126">다음 표에는 호출 실행 방법을 설정하는 다양한 계산 컨텍스트 옵션이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-126">The following table summarizes the various compute context options to set how calls are executed:</span></span>

| <span data-ttu-id="71b2c-127">계산 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="71b2c-127">Compute context</span></span>  | <span data-ttu-id="71b2c-128">설정 방법</span><span class="sxs-lookup"><span data-stu-id="71b2c-128">How to set</span></span>                      | <span data-ttu-id="71b2c-129">실행 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="71b2c-129">Execution context</span></span>                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| <span data-ttu-id="71b2c-130">로컬 순차</span><span class="sxs-lookup"><span data-stu-id="71b2c-130">Local sequential</span></span> | <span data-ttu-id="71b2c-131">rxSetComputeContext('local')</span><span class="sxs-lookup"><span data-stu-id="71b2c-131">rxSetComputeContext(‘local’)</span></span>    | <span data-ttu-id="71b2c-132">직렬로 실행되는 rxExec 호출을 제외하고, 에지 노드 서버의 코어 간 병렬화된 실행</span><span class="sxs-lookup"><span data-stu-id="71b2c-132">Parallelized execution across the cores of the edge node server, except for rxExec calls, which are executed serially</span></span> |
| <span data-ttu-id="71b2c-133">로컬 병렬</span><span class="sxs-lookup"><span data-stu-id="71b2c-133">Local parallel</span></span>   | <span data-ttu-id="71b2c-134">rxSetComputeContext('localpar')</span><span class="sxs-lookup"><span data-stu-id="71b2c-134">rxSetComputeContext(‘localpar’)</span></span> | <span data-ttu-id="71b2c-135">에지 노드 서버의 코어 간 병렬화된 실행</span><span class="sxs-lookup"><span data-stu-id="71b2c-135">Parallelized execution across the cores of the edge node server</span></span> |
| <span data-ttu-id="71b2c-136">Spark</span><span class="sxs-lookup"><span data-stu-id="71b2c-136">Spark</span></span>            | <span data-ttu-id="71b2c-137">RxSpark()</span><span class="sxs-lookup"><span data-stu-id="71b2c-137">RxSpark()</span></span>                       | <span data-ttu-id="71b2c-138">HDI 클러스터의 노드에서 Spark를 통해 분산된 실행 병렬 처리</span><span class="sxs-lookup"><span data-stu-id="71b2c-138">Parallelized distributed execution via Spark across the nodes of the HDI cluster</span></span> |
| <span data-ttu-id="71b2c-139">Map Reduce</span><span class="sxs-lookup"><span data-stu-id="71b2c-139">Map Reduce</span></span>       | <span data-ttu-id="71b2c-140">RxHadoopMR()</span><span class="sxs-lookup"><span data-stu-id="71b2c-140">RxHadoopMR()</span></span>                    | <span data-ttu-id="71b2c-141">HDI 클러스터의 노드에서 Map Reduce를 통해 분산된 실행 병렬 처리</span><span class="sxs-lookup"><span data-stu-id="71b2c-141">Parallelized distributed execution via Map Reduce across the nodes of the HDI cluster</span></span> |

## <a name="guidelines-for-deciding-on-a-compute-context"></a><span data-ttu-id="71b2c-142">계산 컨텍스트를 결정하기 위한 지침</span><span class="sxs-lookup"><span data-stu-id="71b2c-142">Guidelines for deciding on a compute context</span></span>

<span data-ttu-id="71b2c-143">선택한 세 가지 옵션 중 병렬 처리 실행을 제공하는 옵션은 분석 작업의 성격, 크기 그리고 데이터의 위치에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-143">Which of the three options you choose that provide parallelized execution depends on the nature of your analytics work, the size, and the location of your data.</span></span> <span data-ttu-id="71b2c-144">사용할 계산 컨텍스트를 알려주는 수식은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-144">There is no simple formula that tells you which compute context to use.</span></span> <span data-ttu-id="71b2c-145">그러나 올바로 선택할 수 있도록, 또는 적어도 벤치마크를 실행하기 전에 선택할 범위를 좁히는 데 도움이 되는 몇 가지 가이드 원칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-145">There are, however, some guiding principles that can help you make the right choice, or, at least, help you narrow down your choices before you run a benchmark.</span></span> <span data-ttu-id="71b2c-146">기본 원칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-146">These guiding principles include:</span></span>

- <span data-ttu-id="71b2c-147">로컬 Linux 파일 시스템이 HDFS보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-147">The local Linux file system is faster than HDFS.</span></span>
- <span data-ttu-id="71b2c-148">데이터가 로컬에 있고 XDF 형식인 경우 반복된 분석이 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-148">Repeated analyses are faster if the data is local, and if it's in XDF.</span></span>
- <span data-ttu-id="71b2c-149">텍스트 데이터 원본에서 적은 양의 데이터를 스트리밍하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-149">It's preferable to stream small amounts of data from a text data source.</span></span> <span data-ttu-id="71b2c-150">데이터 양이 더 많을 경우 분석 전에 XDF로 변환하세요.</span><span class="sxs-lookup"><span data-stu-id="71b2c-150">If the amount of data is larger, convert it to XDF before analysis.</span></span>
- <span data-ttu-id="71b2c-151">분석을 위해 에지 노드에 데이터를 복사하거나 스트리밍하는 경우 발생하는 오버헤드는 매우 많은 양의 데이터가 감당할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-151">The overhead of copying or streaming the data to the edge node for analysis becomes unmanageable for very large amounts of data.</span></span>
- <span data-ttu-id="71b2c-152">Hadoop의 분석의 경우 Spark가 Map Reduce보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-152">Spark is faster than Map Reduce for analysis in Hadoop.</span></span>

<span data-ttu-id="71b2c-153">이러한 원칙을 감안하여 다음 섹션에서는 계산 컨텍스트 선택에 대한 몇 가지 일반적인 규칙을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-153">Given these principles, the following sections offer some general rules of thumb for selecting a compute context.</span></span>

### <a name="local"></a><span data-ttu-id="71b2c-154">Local</span><span class="sxs-lookup"><span data-stu-id="71b2c-154">Local</span></span>
* <span data-ttu-id="71b2c-155">분석할 데이터 양이 적고 반복된 분석이 필요하지 않을 경우 *'local'* 또는 *'localpar'*를 사용하여 분석 루틴으로 직접 스트림이 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-155">If the amount of data to analyze is small and does not require repeated analysis, then stream it directly into the analysis routine using *'local'* or *'localpar'*.</span></span>
* <span data-ttu-id="71b2c-156">분석할 데이터의 양이 적거나 중간 크기이고 분석을 반복해야 하는 경우 로컬 파일 시스템에 복사하고 XDF로 가져와서 *'local'* 또는 *'localpar'*를 통해 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-156">If the amount of data to analyze is small or medium-sized and requires repeated analysis, then copy it to the local file system, import it to XDF, and analyze it via *'local'* or *'localpar'*.</span></span>

### <a name="hadoop-spark"></a><span data-ttu-id="71b2c-157">Hadoop Spark</span><span class="sxs-lookup"><span data-stu-id="71b2c-157">Hadoop Spark</span></span>
* <span data-ttu-id="71b2c-158">분석할 데이터 양이 많은 경우 **RxHiveData** 또는 **RxParquetData**를 사용하여 Spark DataFrame으로 가져오거나 저장소 문제가 아닌 한 HDFS의 XDF로 가져와서 Spark 계산 컨텍스트를 사용하여 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-158">If the amount of data to analyze is large, then import it to a Spark DataFrame using **RxHiveData** or **RxParquetData**, or to XDF in HDFS (unless storage is an issue), and analyze it using the Spark compute context.</span></span>

### <a name="hadoop-map-reduce"></a><span data-ttu-id="71b2c-159">Hadoop Map Reduce</span><span class="sxs-lookup"><span data-stu-id="71b2c-159">Hadoop Map Reduce</span></span>
* <span data-ttu-id="71b2c-160">일반적으로 느려질 수 있기 때문에 Spark 계산 컨텍스트를 사용하여 대처할 수 없는 문제가 발생하는 경우에만 Map Reduce 계산 컨텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-160">Use the Map Reduce compute context only if you encounter an insurmountable problem with the Spark compute context since it is generally slower.</span></span>  

## <a name="inline-help-on-rxsetcomputecontext"></a><span data-ttu-id="71b2c-161">rxSetComputeContext의 인라인 도움말</span><span class="sxs-lookup"><span data-stu-id="71b2c-161">Inline help on rxSetComputeContext</span></span>
<span data-ttu-id="71b2c-162">자세한 내용 및 ScaleR 계산 컨텍스트의 예제는 다음과 같이 rxSetComputeContext 메서드에 대한 R의 인라인 도움말을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71b2c-162">For more information and examples of ScaleR compute contexts, see the inline help in R on the rxSetComputeContext method, for example:</span></span>

    > ?rxSetComputeContext

<span data-ttu-id="71b2c-163">[R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "MSDN의 R Server") 라이브러리에서 사용할 수 있는 "[ScaleR 분산 컴퓨팅 가이드](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)"(영문)를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-163">You can also refer to the “[ScaleR Distributed Computing Guide](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)” that's available from the [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server on MSDN") library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71b2c-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71b2c-164">Next steps</span></span>
<span data-ttu-id="71b2c-165">이 문서에서는 에지 노드 또는 HDInsight 클러스터의 코어에서 실행 병렬 처리 여부 및 방법을 지정하기 위해 사용할 수 있는 옵션에 대해 알아봤습니다.</span><span class="sxs-lookup"><span data-stu-id="71b2c-165">In this article, you learned about the options that are available to specify whether and how execution is parallelized across cores of the edge node or HDInsight cluster.</span></span> <span data-ttu-id="71b2c-166">HDInsight 클러스터에서 R 서버를 사용하는 방법에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71b2c-166">To learn more about how to use R Server with HDInsight clusters, see the following topics:</span></span>

* [<span data-ttu-id="71b2c-167">Hadoop용 R 서버 개요</span><span class="sxs-lookup"><span data-stu-id="71b2c-167">Overview of R Server for Hadoop</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="71b2c-168">Hadoop용 R Server 시작</span><span class="sxs-lookup"><span data-stu-id="71b2c-168">Get started with R Server for Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="71b2c-169">HDInsight에 RStudio Server 추가(클러스터를 만드는 중에 추가되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="71b2c-169">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="71b2c-170">HDInsight에서 R Server의 Azure Storage 옵션</span><span class="sxs-lookup"><span data-stu-id="71b2c-170">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

