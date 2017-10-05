---
title: "Azure Data Lake Store Spark 성능 조정 지침 | Microsoft Docs"
description: "Azure Data Lake Store Spark 성능 조정 지침"
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
ms.openlocfilehash: 2109744fb7ffdfafb7a86bbea355e119718af099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="6d043-103">HDInsight의 Spark 및 Azure Data Lake Store에 대한 성능 조정 지침</span><span class="sxs-lookup"><span data-stu-id="6d043-103">Performance tuning guidance for Spark on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="6d043-104">Spark에서 성능을 조정할 때 클러스터에서 실행될 앱 수를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-104">When tuning performance on Spark, you need to consider the number of apps that will be running on your cluster.</span></span>  <span data-ttu-id="6d043-105">기본적으로 HDI 클러스터에서 4개의 앱을 동시에 실행할 수 있습니다(참고: 기본 설정은 변경될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="6d043-105">By default, you can run 4 apps concurrently on your HDI cluster (Note: the default setting is subject to change).</span></span>  <span data-ttu-id="6d043-106">사용할 앱 수를 줄여서 기본 설정을 재정의하고 해당 앱에 더 많은 클러스터를 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-106">You may decide to use fewer apps so you can override the default settings and use more of the cluster for those apps.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6d043-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d043-107">Prerequisites</span></span>

* <span data-ttu-id="6d043-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="6d043-108">**An Azure subscription**.</span></span> <span data-ttu-id="6d043-109">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d043-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6d043-110">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="6d043-110">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="6d043-111">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6d043-111">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="6d043-112">**Azure HDInsight 클러스터** 입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-112">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="6d043-113">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d043-113">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="6d043-114">클러스터에 대한 원격 데스크톱을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-114">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="6d043-115">**Azure Data Lake Store에서 실행 중인 Spark 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="6d043-115">**Running Spark cluster on Azure Data Lake Store**.</span></span>  <span data-ttu-id="6d043-116">자세한 내용은 [HDInsight Spark 클러스터를 사용하여 Data Lake Store의 데이터 분석](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d043-116">For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span></span>
* <span data-ttu-id="6d043-117">**ADLS에서 성능 조정 지침**.</span><span class="sxs-lookup"><span data-stu-id="6d043-117">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="6d043-118">일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d043-118">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span> 

## <a name="parameters"></a><span data-ttu-id="6d043-119">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6d043-119">Parameters</span></span>

<span data-ttu-id="6d043-120">Spark 작업을 실행할 때 ADLS에서 성능을 향상시키기 위해 조정할 수 있는 가장 중요한 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-120">When running Spark jobs, here are the most important settings that can be tuned to increase performance on ADLS:</span></span>

* <span data-ttu-id="6d043-121">**Num-executors** - 실행할 수 있는 동시 태스크 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-121">**Num-executors** - The number of concurrent tasks that can be executed.</span></span>

* <span data-ttu-id="6d043-122">**Executor-memory** - 각 실행기에 할당된 메모리 양입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-122">**Executor-memory** - The amount of memory allocated to each executor.</span></span>

* <span data-ttu-id="6d043-123">**Executor-cores** - 각 실행기에 할당된 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-123">**Executor-cores** - The number of cores allocated to each executor.</span></span>                     

<span data-ttu-id="6d043-124">**Num-executors** Num-executors는 병렬로 실행할 수 있는 최대 태스크 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-124">**Num-executors** Num-executors will set the maximum number of tasks that can run in parallel.</span></span>  <span data-ttu-id="6d043-125">병렬로 실행할 수 있는 실제 태스크 수는 클러스터에서 사용 가능한 메모리 및 CPU 리소스로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-125">The actual number of tasks that can run in parallel is bounded by the memory and CPU resources available in your cluster.</span></span>

<span data-ttu-id="6d043-126">**Executor-memory** 각 실행기에 할당되는 메모리 양입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-126">**Executor-memory** This is the amount of memory that is being allocated to each executor.</span></span>  <span data-ttu-id="6d043-127">각 실행기에 필요한 메모리는 작업에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-127">The memory needed for each executor is dependent on the job.</span></span>  <span data-ttu-id="6d043-128">복잡한 작업의 경우 메모리가 더 많이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-128">For complex operations, the memory needs to be higher.</span></span>  <span data-ttu-id="6d043-129">읽기 및 쓰기와 같은 간단한 작업의 경우 메모리 요구 사항은 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-129">For simple operations like read and write, memory requirements will be lower.</span></span>  <span data-ttu-id="6d043-130">각 실행기에 대한 메모리 양은 Ambari에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-130">The amount of memory for each executor can be viewed in Ambari.</span></span>  <span data-ttu-id="6d043-131">Ambari에서 Spark로 이동한 후 Configs 탭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-131">In Ambari, navigate to Spark and view the Configs tab.</span></span>  

<span data-ttu-id="6d043-132">**Executor-cores** 실행기당 사용된 코어 양을 설정하며 이 값에 따라 실행기당 실행할 수 있는 병렬 스레드 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-132">**Executor-cores** This sets the amount of cores used per executor, which determines the number of parallel threads that can be run per executor.</span></span>  <span data-ttu-id="6d043-133">예를 들어 executor-cores = 2인 경우 각 실행기는 실행기에서 2개의 병렬 태스크를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-133">For example, if executor-cores = 2, then each executor can run 2 parallel tasks in the executor.</span></span>  <span data-ttu-id="6d043-134">필요한 executor-cores는 작업에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-134">The executor-cores needed will be dependent on the job.</span></span>  <span data-ttu-id="6d043-135">I/O가 많은 작업에는 태스크당 큰 메모리가 필요하지 않으므로 각 실행기에서 더 많은 병렬 태스크를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-135">I/O heavy jobs do not require a large amount of memory per task so each executor can handle more parallel tasks.</span></span>

<span data-ttu-id="6d043-136">기본적으로 HDInsight에서 Spark를 실행할 때 각 물리적 코어에 대해 2개의 가상 YARN 코어가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-136">By default, two virtual YARN cores are defined for each physical core when running Spark on HDInsight.</span></span>  <span data-ttu-id="6d043-137">이 값은 여러 스레드에서 동시성 및 컨텍스트 전환 횟수 간에 적절한 균형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-137">This number provides a good balance of concurrecy and amount of context switching from multiple threads.</span></span>  

## <a name="guidance"></a><span data-ttu-id="6d043-138">인도</span><span class="sxs-lookup"><span data-stu-id="6d043-138">Guidance</span></span>

<span data-ttu-id="6d043-139">Data Lake Store의 데이터로 작업하는 Spark 분석 워크로드를 실행하는 동안 Data Lake Store의 성능을 극대화하려면 최신 HDInsight 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-139">While running Spark analytic workloads to work with data in Data Lake Store, we recommend that you use the most recent HDInsight version to get the best performance with Data Lake Store.</span></span> <span data-ttu-id="6d043-140">작업이 I/O 집약적인 경우 성능 개선을 위해 특정 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-140">When your job is more I/O intensive, then certain parameters can be configured to improve performance.</span></span>  <span data-ttu-id="6d043-141">Azure Data Lake Store는 높은 처리량을 처리할 수 있는 확장성 높은 저장소 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-141">Azure Data Lake Store is a highly scalable storage platform that can handle high throughput.</span></span>  <span data-ttu-id="6d043-142">작업이 주로 읽기 또는 쓰기를 구성하는 경우 Azure Data Lake Store 간의 I/O에 대한 동시성이 증가하면 성능도 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-142">If the job mainly consists of read or writes, then increasing concurrency for I/O to and from Azure Data Lake Store could increase performance.</span></span>

<span data-ttu-id="6d043-143">I/O 집약적인 작업에 대한 동시성을 높이는 몇 가지 일반적인 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-143">There are a few general ways to increase concurrency for I/O intensive jobs.</span></span>

<span data-ttu-id="6d043-144">**1단계: 클러스터에서 실행되는 앱 수 결정** – 현재 앱을 포함하여 클러스터에서 실행되는 앱 수를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-144">**Step 1: Determine how many apps are running on your cluster** – You should know how many apps are running on the cluster including the current one.</span></span>  <span data-ttu-id="6d043-145">각 Spark 설정에 대한 기본 값에서는 4개의 앱이 동시에 실행 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-145">The default values for each Spark setting assumes that there are 4 apps running concurrently.</span></span>  <span data-ttu-id="6d043-146">따라서 앱당 클러스터의 25%만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-146">Therefore, you will only have 25% of the cluster available for each app.</span></span>  <span data-ttu-id="6d043-147">더 나은 성능을 얻기 위해 실행기 수를 변경하여 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-147">To get better performance, you can override the defaults by changing the number of executors.</span></span>  

<span data-ttu-id="6d043-148">**2단계: executor-memory 설정** – 가장 먼저 설정할 항목은 executor-memory입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-148">**Step 2: Set executor-memory** – the first thing to set is the executor-memory.</span></span>  <span data-ttu-id="6d043-149">메모리는 실행할 작업에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-149">The memory will be dependent on the job that you are going to run.</span></span>  <span data-ttu-id="6d043-150">실행기당 메모리 할당량을 줄여 동시성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-150">You can increase concurrency by allocating less memory per executor.</span></span>  <span data-ttu-id="6d043-151">작업을 실행할 때 메모리 부족 예외가 표시되면 이 매개 변수 값을 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-151">If you see out of memory exceptions when you run your job, then you should increase the value for this parameter.</span></span>  <span data-ttu-id="6d043-152">한 가지 대안은 메모리가 많은 클러스터를 사용하거나 클러스터 크기를 늘려 더 많은 메모리를 확보하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-152">One alternative is to get more memory by using a cluster that has higher amounts of memory or increasing the size of your cluster.</span></span>  <span data-ttu-id="6d043-153">메모리가 많아지면 더 많은 실행기가 사용되며 이것은 동시성 증가로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-153">More memory will enable more executors to be used, which means more concurrency.</span></span>

<span data-ttu-id="6d043-154">**3단계: executor-cores 설정** – 복잡한 작업이 없는 I/O 집약적인 워크로드의 경우 실행기당 병렬 태스크 수를 늘리기 위해 executor-cores 수를 높게 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-154">**Step 3: Set executor-cores** – For I/O intensive workloads that do not have complex operations, it’s good to start with a high number of executor-cores to increase the number of parallel tasks per executor.</span></span>  <span data-ttu-id="6d043-155">executor-cores를 4로 설정하여 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-155">Setting executor-cores to 4 is a good start.</span></span>   

    executor-cores = 4
<span data-ttu-id="6d043-156">executor-cores 수를 늘리면 더 많은 병렬 처리를 제공하므로 서로 다른 executor-cores로 실험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-156">Increasing the number of executor-cores will give you more parallelism so you can experiment with different executor-cores.</span></span>  <span data-ttu-id="6d043-157">더욱 복잡한 작업(operation)이 있는 작업(job)의 경우 실행기당 코어 수를 줄여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-157">For jobs that have more complex operations, you should reduce the number of cores per executor.</span></span>  <span data-ttu-id="6d043-158">executor-cores가 4보다 높게 설정된 경우 가비지 수집이 부족하여 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-158">If executor-cores is set higher than 4, then garbage collection may become inefficient and degrade performance.</span></span>

<span data-ttu-id="6d043-159">**4단계: 클러스터에서 YARN 메모리 양 결정** – 이 정보는 Ambari에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-159">**Step 4: Determine amount of YARN memory in cluster** – This information is available in Ambari.</span></span>  <span data-ttu-id="6d043-160">YARN으로 이동한 후 Configs 탭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-160">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="6d043-161">이 창에 YARN 메모리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-161">The YARN memory is displayed in this window.</span></span>  
<span data-ttu-id="6d043-162">참고: 이 창에 있는 동안 기본 YARN 컨테이너 크기도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-162">Note: while you are in the window, you can also see the default YARN container size.</span></span>  <span data-ttu-id="6d043-163">YARN 컨테이너 크기는 실행기 매개 변수당 메모리와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-163">The YARN container size is the same as memory per executor paramter.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="6d043-164">**5단계: num-executors 계산**</span><span class="sxs-lookup"><span data-stu-id="6d043-164">**Step 5: Calculate num-executors**</span></span>

<span data-ttu-id="6d043-165">**메모리 제약 조건 계산** - num-executors 매개 변수는 메모리 또는 CPU에 의해 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-165">**Calculate memory constraint** - The num-executors parameter is constrained either by memory or by CPU.</span></span>  <span data-ttu-id="6d043-166">메모리 제약 조건은 응용 프로그램에 사용 가능한 YARN 메모리 양에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-166">The memory constraint is determined by the amount of available YARN memory for your application.</span></span>  <span data-ttu-id="6d043-167">총 YARN 메모리를 가져와 executor-memory로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-167">You should take total YARN memory and divide that by executor-memory.</span></span>  <span data-ttu-id="6d043-168">앱 수에 맞게 제약 조건을 조정해야 하므로 앱 수로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-168">The constraint needs to be de-scaled for the number of apps so we divide by the number of apps.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
<span data-ttu-id="6d043-169">**CPU 제약 조건 계산** - CPU 제약 조건은 총 가상 코어 수를 실행기당 코어 수로 나누어 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-169">**Calculate CPU constraint** - The CPU constraint is calculated as the total virtual cores divided by the number of cores per executor.</span></span>  <span data-ttu-id="6d043-170">각 물리적 코어당 2개의 가상 코어가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-170">There are 2 virtual cores for each physical core.</span></span>  <span data-ttu-id="6d043-171">메모리 제약 조건과 마찬가지로 앱 수로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-171">Similar to the memory constraint, we have divide by the number of apps.</span></span>

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
<span data-ttu-id="6d043-172">**num-executors 설정** – num-executors 매개 변수는 메모리 제약 조건 및 CPU 제약 조건 중 최소값을 사용하여 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-172">**Set num-executors** – The num-executors parameter is determined by taking the minimum of the memory constraint and the CPU constraint.</span></span> 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
<span data-ttu-id="6d043-173">num-executors 수를 높게 설정한다고 성능이 반드시 향상되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-173">Setting a higher number of num-executors does not necessarily increase performance.</span></span>  <span data-ttu-id="6d043-174">더 많은 실행기를 추가하면 각 실행기당 오버헤드가 더 추가되며 이로 인해 성능이 저하될 수 있다는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-174">You should consider that adding more executors will add extra overhead for each additional executor, which can potentially degrade performance.</span></span>  <span data-ttu-id="6d043-175">Num-executors는 클러스터 리소스의 제한을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-175">Num-executors is bounded by the cluster resources.</span></span>    

## <a name="example-calculation"></a><span data-ttu-id="6d043-176">계산 예</span><span class="sxs-lookup"><span data-stu-id="6d043-176">Example Calculation</span></span>

<span data-ttu-id="6d043-177">실행 예정인 앱을 포함하여 현재 2개의 앱을 실행 중인 D4v2 노드 8개로 구성된 클러스터가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-177">Let’s say you currently have a cluster composed of 8 D4v2 nodes that is running 2 apps including the one you are going to run.</span></span>  

<span data-ttu-id="6d043-178">**1단계: 클러스터에서 실행되는 앱 수 결정** – 실행 예정인 앱을 포함하여 클러스터에 2개의 앱이 있다는 것을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-178">**Step 1: Determine how many apps are running on your cluster** – you know that you have 2 apps on your cluster, including the one you are going to run.</span></span>  

<span data-ttu-id="6d043-179">**2단계: executor-memory 설정** – 이 예의 경우 I/O 집약적인 작업에 대해 6GB의 실행기 메모리면 충분하다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-179">**Step 2: Set executor-memory** – for this example, we determine that 6GB of executor-memory will be sufficient for I/O intensive job.</span></span>  

    executor-memory = 6GB
<span data-ttu-id="6d043-180">**3단계: executor-cores 설정** – I/O 집약적인 작업이므로 실행기당 코어 수를 4로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-180">**Step 3: Set executor-cores** – Since this is an I/O intensive job, we can set the number of cores for each executor to 4.</span></span>  <span data-ttu-id="6d043-181">실행기당 코어 수를 4보다 높게 설정하면 가비지 수집 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-181">Setting cores per executor to larger than 4 may cause garbage collection problems.</span></span>  

    executor-cores = 4
<span data-ttu-id="6d043-182">**4단계: 클러스터에서 YARN 메모리 양 결정** – Ambari로 이동하여 각 D4v2에 25GB의 YARN 메모리가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-182">**Step 4: Determine amount of YARN memory in cluster** – We navigate to Ambari to find out that each D4v2 has 25GB of YARN memory.</span></span>  <span data-ttu-id="6d043-183">8개의 노드가 있으므로 사용 가능한 YARN 메모리에 8을 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-183">Since there are 8 nodes, the available YARN memory is multiplied by 8.</span></span>

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
<span data-ttu-id="6d043-184">**5단계: num-executors 계산** – num-executors 매개 변수는 메모리 제약 조건 및 CPU 제약 조건 중 최소값을 Spark에서 실행 중인 앱 수로 나누어 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-184">**Step 5: Calculate num-executors** – The num-executors parameter is determined by taking the minimum of the memory constraint and the CPU constraint divided by the # of apps running on Spark.</span></span>    

<span data-ttu-id="6d043-185">**메모리 제약 조건 계산** - 메모리 제약 조건은 총 YARN 메모리를 실행기당 메모리로 나누어 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-185">**Calculate memory constraint** – The memory constraint is calculated as the total YARN memory divided by the memory per executor.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
<span data-ttu-id="6d043-186">**CPU 제약 조건 계산** - CPU 제약 조건은 총 yarn 코어 수를 실행기당 코어 수로 나누어 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="6d043-186">**Calculate CPU constraint** - The CPU constraint is calculated as the total yarn cores divided by the number of cores per executor.</span></span>
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
<span data-ttu-id="6d043-187">**num-executors 설정**</span><span class="sxs-lookup"><span data-stu-id="6d043-187">**Set num-executors**</span></span>

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

