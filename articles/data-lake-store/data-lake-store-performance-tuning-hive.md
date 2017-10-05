---
title: "Azure Data Lake Store Hive 성능 조정 지침 | Microsoft Docs"
description: "Azure Data Lake Store Hive 성능 조정 지침"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e10bf8f7cbae2b81d22823ff74fe652c6bcb2da3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="2ec74-103">HDInsight의 Hive 및 Azure Data Lake Store에 대한 성능 조정 지침</span><span class="sxs-lookup"><span data-stu-id="2ec74-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="2ec74-104">서로 다른 여러 사용 사례 간에 적절한 성능을 제공하도록 기본 설정이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-104">The default settings have been set to provide good performance across many different use cases.</span></span>  <span data-ttu-id="2ec74-105">I/O 집약적인 쿼리에 대해 ADLS로 더 나은 성능을 얻도록 Hive를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-105">For I/O intensive queries, Hive can be tuned to get better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="2ec74-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ec74-106">Prerequisites</span></span>

* <span data-ttu-id="2ec74-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2ec74-107">**An Azure subscription**.</span></span> <span data-ttu-id="2ec74-108">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec74-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2ec74-109">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="2ec74-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2ec74-110">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2ec74-110">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="2ec74-111">**Azure HDInsight 클러스터** 입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-111">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="2ec74-112">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec74-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="2ec74-113">클러스터에 대한 원격 데스크톱을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-113">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="2ec74-114">**HDInsight에서 Hive 실행**.</span><span class="sxs-lookup"><span data-stu-id="2ec74-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="2ec74-115">HDInsight에서 Hive 작업 실행에 대해 자세히 알아 보려면 [HDInsight에서 Hive 사용] (https://docs.microsoft.com/ko-kr/azure/hdinsight/hdinsight-use-hive)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec74-115">To learn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="2ec74-116">**ADLS에서 성능 조정 지침**.</span><span class="sxs-lookup"><span data-stu-id="2ec74-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="2ec74-117">일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec74-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="2ec74-118">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2ec74-118">Parameters</span></span>

<span data-ttu-id="2ec74-119">ADLS 성능 향상을 위해 조정할 가장 중요한 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-119">Here are the most important settings to tune for improved ADLS performance:</span></span>

* <span data-ttu-id="2ec74-120">**hive.tez.container.size** – 각 태스크에 사용된 메모리 양</span><span class="sxs-lookup"><span data-stu-id="2ec74-120">**hive.tez.container.size** – the amount of memory used by each tasks</span></span>

* <span data-ttu-id="2ec74-121">**tez.grouping.min-size** – 각 매퍼의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="2ec74-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="2ec74-122">**tez.grouping.max-size** – 각 매퍼의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="2ec74-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="2ec74-123">**hive.exec.reducer.bytes.per.reducer** – 각 리듀서의 크기</span><span class="sxs-lookup"><span data-stu-id="2ec74-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="2ec74-124">**hive.tez.container.size** - 컨테이너 크기에 따라 각 태스크에 사용 가능한 메모리 양이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-124">**hive.tez.container.size** - The container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="2ec74-125">Hive에서 동시성을 제어하기 위한 기본 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-125">This is the main input for controlling the concurrency in Hive.</span></span>  

<span data-ttu-id="2ec74-126">**tez.grouping.min-size** – 이 매개 변수를 통해 각 매퍼의 최소 크기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-126">**tez.grouping.min-size** – This parameter allows you to set the minimum size of each mapper.</span></span>  <span data-ttu-id="2ec74-127">Tez에서 선택한 매퍼 수가 이 매개 변수 값보다 작은 경우 Tez에서 여기서 설정된 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-127">If the number of mappers that Tez chooses is smaller than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="2ec74-128">**tez.grouping.max-size** – 매개 변수를 통해 각 매퍼의 최대 크기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-128">**tez.grouping.max-size** – The parameter allows you to set the maximum size of each mapper.</span></span>  <span data-ttu-id="2ec74-129">Tez에서 선택한 매퍼 수가 이 매개 변수 값보다 큰 경우 Tez에서 여기에 설정된 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-129">If the number of mappers that Tez chooses is larger than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="2ec74-130">**hive.exec.reducer.bytes.per.reducer** – 이 매개 변수는 각 리듀서의 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets the size of each reducer.</span></span>  <span data-ttu-id="2ec74-131">기본적으로 각 리듀서는 256MB입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="2ec74-132">인도</span><span class="sxs-lookup"><span data-stu-id="2ec74-132">Guidance</span></span>

<span data-ttu-id="2ec74-133">**hive.exec.reducer.bytes.per.reducer 설정** – 데이터가 압축되지 않은 경우 기본 값이 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-133">**Set hive.exec.reducer.bytes.per.reducer** – The default value works well when the data is uncompressed.</span></span>  <span data-ttu-id="2ec74-134">압축된 데이터의 경우 리듀서의 크기를 줄여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-134">For data that is compressed, you should reduce the size of the reducer.</span></span>  

<span data-ttu-id="2ec74-135">**Set hive.tez.container.size** – 각 노드에서 메모리는 yarn.nodemanager.resource.memory-mb에 의해 지정되고 기본적으로 HDI 클러스터에서 제대로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="2ec74-136">YARN에서 적절한 메모리 설정에 대한 추가 정보는 이 [게시물](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec74-136">For additional information on setting the appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="2ec74-137">I/O 집약적인 워크로드의 경우 Tez 컨테이너 크기를 줄여 더 많은 병렬 처리의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-137">I/O intensive workloads can benefit from more parallelism by decreasing the Tez container size.</span></span> <span data-ttu-id="2ec74-138">이렇게 하면 사용자에게 더 많은 컨테이너가 제공되어 동시성이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-138">This gives the user more containers which increases concurrency.</span></span>  <span data-ttu-id="2ec74-139">하지만 일부 Hive 쿼리에는 상당한 양의 메모리가 필요합니다(예: MapJoin).</span><span class="sxs-lookup"><span data-stu-id="2ec74-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="2ec74-140">태스크에 충분한 메모리가 없는 경우 런타임 중에 메모리 부족 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-140">If the task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="2ec74-141">메모리 부족 예외가 발생하면 메모리를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-141">If you receive out of memory exceptions, then you should increase the memory.</span></span>   

<span data-ttu-id="2ec74-142">병렬 처리에서 실행 중인 동시 태스크 수는 총 YARN 메모리의 제약을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-142">The concurrent number of tasks running or parallelism will be bounded by the total YARN memory.</span></span>  <span data-ttu-id="2ec74-143">YARN 컨테이너 수에 따라 실행할 수 있는 동시 태스크 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-143">The number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="2ec74-144">노드당 YARN 메모리를 찾으려면 Ambari로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-144">To find the YARN memory per node, you can go to Ambari.</span></span>  <span data-ttu-id="2ec74-145">YARN으로 이동한 후 Configs 탭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-145">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="2ec74-146">이 창에 YARN 메모리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-146">The YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="2ec74-147">ADLS를 사용하여 성능을 개선하기 위한 핵심은 가능한 동시성을 늘리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-147">The key to improving performance using ADLS is to increase the concurrency as much as possible.</span></span>  <span data-ttu-id="2ec74-148">Tez가 생성할 태스크 수를 자동으로 계산하므로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-148">Tez automatically calculates the number of tasks that should be created so you do not need to set it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="2ec74-149">계산 예</span><span class="sxs-lookup"><span data-stu-id="2ec74-149">Example Calculation</span></span>

<span data-ttu-id="2ec74-150">8 노드 D14 클러스터가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-150">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="2ec74-151">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2ec74-151">Limitations</span></span>
<span data-ttu-id="2ec74-152">**ADLS 제한**</span><span class="sxs-lookup"><span data-stu-id="2ec74-152">**ADLS throttling**</span></span> 

<span data-ttu-id="2ec74-153">ADLS에서 제공하는 대역폭 한계에 도달한 경우 태스크 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-153">UIf you hit the limits of bandwidth provided by ADLS, you would start to see task failures.</span></span> <span data-ttu-id="2ec74-154">이것은 태스크 로그에서 제한 오류를 확인하여 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-154">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="2ec74-155">Tez 컨테이너 크기를 늘려 병렬 처리를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-155">You can decrease the parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="2ec74-156">작업에 대한 동시성이 더 필요한 경우 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec74-156">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="2ec74-157">제한 여부를 확인하려면 클라이언트 쪽에서 디버그 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-157">To check if you are getting throttled, you need to enable the debug logging on the client side.</span></span> <span data-ttu-id="2ec74-158">그 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-158">Here’s how you can do that:</span></span>

1. <span data-ttu-id="2ec74-159">Hive 구성의 log4j 속성에 다음 속성을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-159">Put the following property in the log4j properties in Hive config.</span></span> <span data-ttu-id="2ec74-160">Ambari 보기의 log4j.logger.com.microsoft.azure.datalake.store=DEBUG에서 이 작업을 수행할 수 있습니다. 구성을 적용하려면 노드/서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-160">This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all the nodes/service for the config to take effect.</span></span>

2. <span data-ttu-id="2ec74-161">제한이 적용되면 hive 로그 파일에 HTTP 429 오류 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-161">If you are getting throttled, you’ll see the HTTP 429 error code in the hive log file.</span></span> <span data-ttu-id="2ec74-162">hive 로그 파일은 /tmp/&lt;user&gt;/hive.log에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-162">The hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="2ec74-163">Hive 조정에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="2ec74-163">Further information on Hive tuning</span></span>

<span data-ttu-id="2ec74-164">Hive 쿼리를 조정하는 데 도움이 되는 몇 가지 블로그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec74-164">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="2ec74-165">HDInsight에서 Hadoop에 대한 Hive 쿼리 최적화</span><span class="sxs-lookup"><span data-stu-id="2ec74-165">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="2ec74-166">Hive 쿼리 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2ec74-166">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="2ec74-167">HDInsight에서 Hive 최적화에 대한 논의</span><span class="sxs-lookup"><span data-stu-id="2ec74-167">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
