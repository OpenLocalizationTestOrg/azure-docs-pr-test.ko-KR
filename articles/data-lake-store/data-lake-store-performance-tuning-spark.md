---
title: "데이터 레이크 저장소 Spark 성능 튜닝 지침 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="b8982-103">HDInsight의 Spark 및 Azure Data Lake Store에 대한 성능 조정 지침</span><span class="sxs-lookup"><span data-stu-id="b8982-103">Performance tuning guidance for Spark on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="b8982-104">Spark에 성능을 조정 하는 경우에 클러스터에서 실행 되는 앱의 tooconsider hello 번호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-104">When tuning performance on Spark, you need tooconsider hello number of apps that will be running on your cluster.</span></span>  <span data-ttu-id="b8982-105">기본적으로 4를 실행할 수 있습니다 HDI 클러스터에서 동시에 응용 프로그램 (참고: hello 기본 설정은 주체 toochange입니다).</span><span class="sxs-lookup"><span data-stu-id="b8982-105">By default, you can run 4 apps concurrently on your HDI cluster (Note: hello default setting is subject toochange).</span></span>  <span data-ttu-id="b8982-106">Hello 기본 설정을 무시 하 고 hello 클러스터 중 해당 앱에 사용할 수 있도록 더 적은 앱 toouse을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-106">You may decide toouse fewer apps so you can override hello default settings and use more of hello cluster for those apps.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b8982-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b8982-107">Prerequisites</span></span>

* <span data-ttu-id="b8982-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b8982-108">**An Azure subscription**.</span></span> <span data-ttu-id="b8982-109">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8982-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b8982-110">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="b8982-110">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="b8982-111">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b8982-111">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="b8982-112">**Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-112">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="b8982-113">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8982-113">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="b8982-114">Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-114">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="b8982-115">**Azure Data Lake Store에서 실행 중인 Spark 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="b8982-115">**Running Spark cluster on Azure Data Lake Store**.</span></span>  <span data-ttu-id="b8982-116">자세한 내용은 참조 [데이터 레이크 저장소에서 사용 하 여 HDInsight Spark 클러스터 tooanalyze 데이터](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span><span class="sxs-lookup"><span data-stu-id="b8982-116">For more information, see [Use HDInsight Spark cluster tooanalyze data in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span></span>
* <span data-ttu-id="b8982-117">**ADLS에서 성능 조정 지침**.</span><span class="sxs-lookup"><span data-stu-id="b8982-117">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="b8982-118">일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8982-118">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span> 

## <a name="parameters"></a><span data-ttu-id="b8982-119">매개 변수</span><span class="sxs-lookup"><span data-stu-id="b8982-119">Parameters</span></span>

<span data-ttu-id="b8982-120">Spark 작업을 실행할 때 ADLS에서 조정 된 tooincrease 성능을 일 수 있는 hello 가장 중요 한 설정을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-120">When running Spark jobs, here are hello most important settings that can be tuned tooincrease performance on ADLS:</span></span>

* <span data-ttu-id="b8982-121">**Num executor** -hello 실행 될 수 있는 동시 작업 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-121">**Num-executors** - hello number of concurrent tasks that can be executed.</span></span>

* <span data-ttu-id="b8982-122">**Executor 메모리** -hello 할당 된 메모리 양이 tooeach 실행자입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-122">**Executor-memory** - hello amount of memory allocated tooeach executor.</span></span>

* <span data-ttu-id="b8982-123">**Executor 코어** -코어 수가 hello tooeach executor를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-123">**Executor-cores** - hello number of cores allocated tooeach executor.</span></span>                     

<span data-ttu-id="b8982-124">**Num executor** Num executor hello 병렬로 실행할 수 있는 작업의 최대 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-124">**Num-executors** Num-executors will set hello maximum number of tasks that can run in parallel.</span></span>  <span data-ttu-id="b8982-125">동시에 실행할 수 있는 작업의 실제 수 hello hello 메모리 및 CPU 리소스를 클러스터에서 사용할 수 있는으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-125">hello actual number of tasks that can run in parallel is bounded by hello memory and CPU resources available in your cluster.</span></span>

<span data-ttu-id="b8982-126">**Executor 메모리** hello tooeach 실행자 할당 되는 메모리 양입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-126">**Executor-memory** This is hello amount of memory that is being allocated tooeach executor.</span></span>  <span data-ttu-id="b8982-127">각 실행 기에 필요한 hello 메모리 hello 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-127">hello memory needed for each executor is dependent on hello job.</span></span>  <span data-ttu-id="b8982-128">복잡 한 작업에 대 한 hello 메모리에 더 높은 toobe가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-128">For complex operations, hello memory needs toobe higher.</span></span>  <span data-ttu-id="b8982-129">읽기 및 쓰기와 같은 간단한 작업의 경우 메모리 요구 사항은 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-129">For simple operations like read and write, memory requirements will be lower.</span></span>  <span data-ttu-id="b8982-130">각 실행 기에 대 한 메모리 양이 hello Ambari에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-130">hello amount of memory for each executor can be viewed in Ambari.</span></span>  <span data-ttu-id="b8982-131">Ambari를 tooSpark 이동한 hello Configs 탭을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-131">In Ambari, navigate tooSpark and view hello Configs tab.</span></span>  

<span data-ttu-id="b8982-132">**Executor 코어** hello 실행자 당 실행 될 수 있는 병렬 스레드 수를 결정 하는 실행자 당 사용 되는 코어 hello 양을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-132">**Executor-cores** This sets hello amount of cores used per executor, which determines hello number of parallel threads that can be run per executor.</span></span>  <span data-ttu-id="b8982-133">예를 들어 경우 실행자 코어 = 2, 각 실행자 hello 실행자에 2 병렬 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-133">For example, if executor-cores = 2, then each executor can run 2 parallel tasks in hello executor.</span></span>  <span data-ttu-id="b8982-134">hello 실행자 코어 hello 작업에 종속 됩니다 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-134">hello executor-cores needed will be dependent on hello job.</span></span>  <span data-ttu-id="b8982-135">I/O가 많은 작업에는 태스크당 큰 메모리가 필요하지 않으므로 각 실행기에서 더 많은 병렬 태스크를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-135">I/O heavy jobs do not require a large amount of memory per task so each executor can handle more parallel tasks.</span></span>

<span data-ttu-id="b8982-136">기본적으로 HDInsight에서 Spark를 실행할 때 각 물리적 코어에 대해 2개의 가상 YARN 코어가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-136">By default, two virtual YARN cores are defined for each physical core when running Spark on HDInsight.</span></span>  <span data-ttu-id="b8982-137">이 값은 여러 스레드에서 동시성 및 컨텍스트 전환 횟수 간에 적절한 균형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-137">This number provides a good balance of concurrecy and amount of context switching from multiple threads.</span></span>  

## <a name="guidance"></a><span data-ttu-id="b8982-138">지침</span><span class="sxs-lookup"><span data-stu-id="b8982-138">Guidance</span></span>

<span data-ttu-id="b8982-139">Spark 데이터 레이크 저장소에서 데이터를 분석 워크 로드 toowork 실행 하면서 데이터 레이크 저장소와 hello 가장 최근의 HDInsight 버전 tooget hello 최상의 성능을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-139">While running Spark analytic workloads toowork with data in Data Lake Store, we recommend that you use hello most recent HDInsight version tooget hello best performance with Data Lake Store.</span></span> <span data-ttu-id="b8982-140">더 많은 I/O 사용량이 작업을 사용 하는 경우 특정 매개 변수에서 구성 된 tooimprove 성능 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-140">When your job is more I/O intensive, then certain parameters can be configured tooimprove performance.</span></span>  <span data-ttu-id="b8982-141">Azure Data Lake Store는 높은 처리량을 처리할 수 있는 확장성 높은 저장소 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-141">Azure Data Lake Store is a highly scalable storage platform that can handle high throughput.</span></span>  <span data-ttu-id="b8982-142">Hello 작업 주로으로 구성 된 경우 읽기 또는 쓰기 다음 Azure 데이터 레이크 저장소에서 I/O tooand에 대 한 동시성을 늘려 성능을 향상 시킬 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-142">If hello job mainly consists of read or writes, then increasing concurrency for I/O tooand from Azure Data Lake Store could increase performance.</span></span>

<span data-ttu-id="b8982-143">I/O 집약적인 작업에 대 한 몇 가지 일반적인 방법으로 tooincrease 동시성 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-143">There are a few general ways tooincrease concurrency for I/O intensive jobs.</span></span>

<span data-ttu-id="b8982-144">**1 단계: 클러스터에서 실행 되는 응용 프로그램과 확인** – hello 현재 항목을 포함 하 여 hello 클러스터에서 실행 중인 응용 프로그램과 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-144">**Step 1: Determine how many apps are running on your cluster** – You should know how many apps are running on hello cluster including hello current one.</span></span>  <span data-ttu-id="b8982-145">hello 기본값 설정은 날짜가 각 Spark에 대 한 4에서는 동시에 실행 되는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-145">hello default values for each Spark setting assumes that there are 4 apps running concurrently.</span></span>  <span data-ttu-id="b8982-146">따라서 각 앱에 사용할 수 있는 hello 클러스터의 25%만 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-146">Therefore, you will only have 25% of hello cluster available for each app.</span></span>  <span data-ttu-id="b8982-147">tooget 더 나은 성능을 executor hello 수를 변경 하 여 hello 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-147">tooget better performance, you can override hello defaults by changing hello number of executors.</span></span>  

<span data-ttu-id="b8982-148">**2 단계: 실행자 메모리 설정** – hello tooset hello 실행자 메모리를가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-148">**Step 2: Set executor-memory** – hello first thing tooset is hello executor-memory.</span></span>  <span data-ttu-id="b8982-149">hello 메모리 하락 toorun는 hello 작업에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-149">hello memory will be dependent on hello job that you are going toorun.</span></span>  <span data-ttu-id="b8982-150">실행기당 메모리 할당량을 줄여 동시성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-150">You can increase concurrency by allocating less memory per executor.</span></span>  <span data-ttu-id="b8982-151">메모리 부족 예외가 표시 작업을 실행 하는 경우이 매개 변수에 대 한 hello 값을 늘리십시오 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-151">If you see out of memory exceptions when you run your job, then you should increase hello value for this parameter.</span></span>  <span data-ttu-id="b8982-152">하나의 대체에서는 tooget 메모리가 더 높은 양의 메모리를 갖고 있는 클러스터를 사용 하 여 클러스터의 hello 크기 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-152">One alternative is tooget more memory by using a cluster that has higher amounts of memory or increasing hello size of your cluster.</span></span>  <span data-ttu-id="b8982-153">더 많은 메모리를 더 많은 executor toobe을 사용 하는 더 많은 동시성 의미를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-153">More memory will enable more executors toobe used, which means more concurrency.</span></span>

<span data-ttu-id="b8982-154">**3 단계: 설정 실행자 코어** – I/O가 많은 작업용 복잡 하 고 작업을 갖지 않는, 것이 좋은 toostart 실행자 당 병렬 태스크 수가 tooincrease hello 실행자 코어 수가 높은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-154">**Step 3: Set executor-cores** – For I/O intensive workloads that do not have complex operations, it’s good toostart with a high number of executor-cores tooincrease hello number of parallel tasks per executor.</span></span>  <span data-ttu-id="b8982-155">Executor 코어 too4 설정은 좋은 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-155">Setting executor-cores too4 is a good start.</span></span>   

    executor-cores = 4
<span data-ttu-id="b8982-156">Hello 실행자 코어 수를 늘리면 됩니다 제공 많은 병렬 처리 하므로 다른 실행자 코어를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-156">Increasing hello number of executor-cores will give you more parallelism so you can experiment with different executor-cores.</span></span>  <span data-ttu-id="b8982-157">보다 복잡 한 작업 인 작업은, 실행자 당 코어 수가 hello 줄여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-157">For jobs that have more complex operations, you should reduce hello number of cores per executor.</span></span>  <span data-ttu-id="b8982-158">executor-cores가 4보다 높게 설정된 경우 가비지 수집이 부족하여 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-158">If executor-cores is set higher than 4, then garbage collection may become inefficient and degrade performance.</span></span>

<span data-ttu-id="b8982-159">**4단계: 클러스터에서 YARN 메모리 양 결정** – 이 정보는 Ambari에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-159">**Step 4: Determine amount of YARN memory in cluster** – This information is available in Ambari.</span></span>  <span data-ttu-id="b8982-160">TooYARN를 탐색 하 고 hello Configs 탭을 표시 합니다.  hello YARN 메모리가이 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-160">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  
<span data-ttu-id="b8982-161">참고: hello 창에 있는 동안 참고할 수 있습니다 hello 기본 YARN 컨테이너 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-161">Note: while you are in hello window, you can also see hello default YARN container size.</span></span>  <span data-ttu-id="b8982-162">hello YARN 컨테이너 크기 실행자 매개 변수가 당 메모리와 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-162">hello YARN container size is hello same as memory per executor paramter.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="b8982-163">**5단계: num-executors 계산**</span><span class="sxs-lookup"><span data-stu-id="b8982-163">**Step 5: Calculate num-executors**</span></span>

<span data-ttu-id="b8982-164">**메모리 제약 조건 계산** -hello num executor 매개 변수는 메모리 또는 CPU 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-164">**Calculate memory constraint** - hello num-executors parameter is constrained either by memory or by CPU.</span></span>  <span data-ttu-id="b8982-165">hello 메모리 제약 조건은 hello 응용 프로그램에 대 한 사용 가능한 YARN 메모리 양으로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-165">hello memory constraint is determined by hello amount of available YARN memory for your application.</span></span>  <span data-ttu-id="b8982-166">총 YARN 메모리를 가져와 executor-memory로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-166">You should take total YARN memory and divide that by executor-memory.</span></span>  <span data-ttu-id="b8982-167">hello 제약 조건 해제 되므로 앱 hello 수로 나눕니다 hello 수의 앱에 대 한 크기가 조정 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-167">hello constraint needs toobe de-scaled for hello number of apps so we divide by hello number of apps.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
<span data-ttu-id="b8982-168">**CPU 제약 조건 계산** -hello CPU 제약 조건이 hello 총 가상 코어 hello 실행자 당 코어 수로 나눈 값으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-168">**Calculate CPU constraint** - hello CPU constraint is calculated as hello total virtual cores divided by hello number of cores per executor.</span></span>  <span data-ttu-id="b8982-169">각 물리적 코어당 2개의 가상 코어가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-169">There are 2 virtual cores for each physical core.</span></span>  <span data-ttu-id="b8982-170">비슷한 toohello 메모리 제약 조건, 응용 프로그램의 hello 번호로 나누기를 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-170">Similar toohello memory constraint, we have divide by hello number of apps.</span></span>

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
<span data-ttu-id="b8982-171">**Num executor 설정** – hello num executor 매개 변수 hello 메모리 제약 조건 및 제약 조건 hello CPU의 최소 hello을 수행 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-171">**Set num-executors** – hello num-executors parameter is determined by taking hello minimum of hello memory constraint and hello CPU constraint.</span></span> 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
<span data-ttu-id="b8982-172">num-executors 수를 높게 설정한다고 성능이 반드시 향상되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-172">Setting a higher number of num-executors does not necessarily increase performance.</span></span>  <span data-ttu-id="b8982-173">더 많은 실행기를 추가하면 각 실행기당 오버헤드가 더 추가되며 이로 인해 성능이 저하될 수 있다는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-173">You should consider that adding more executors will add extra overhead for each additional executor, which can potentially degrade performance.</span></span>  <span data-ttu-id="b8982-174">Num executor hello 클러스터 리소스에 의해 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-174">Num-executors is bounded by hello cluster resources.</span></span>    

## <a name="example-calculation"></a><span data-ttu-id="b8982-175">계산 예</span><span class="sxs-lookup"><span data-stu-id="b8982-175">Example Calculation</span></span>

<span data-ttu-id="b8982-176">실행 중인 2 앱 hello를 포함 한 보아야 toorun 하는 클러스터 D4v2 8 개의 노드로 구성에 현재 있는 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-176">Let’s say you currently have a cluster composed of 8 D4v2 nodes that is running 2 apps including hello one you are going toorun.</span></span>  

<span data-ttu-id="b8982-177">**1 단계: 클러스터에서 실행 되는 응용 프로그램과 확인** – 2 있는지 알고 hello toorun 보아야 하나를 포함 하 여 클러스터에는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-177">**Step 1: Determine how many apps are running on your cluster** – you know that you have 2 apps on your cluster, including hello one you are going toorun.</span></span>  

<span data-ttu-id="b8982-178">**2단계: executor-memory 설정** – 이 예의 경우 I/O 집약적인 작업에 대해 6GB의 실행기 메모리면 충분하다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-178">**Step 2: Set executor-memory** – for this example, we determine that 6GB of executor-memory will be sufficient for I/O intensive job.</span></span>  

    executor-memory = 6GB
<span data-ttu-id="b8982-179">**3 단계: 설정 실행자 코어** – I/O 집약적인 작업 이므로, 각 실행자 too4에 대 한 코어의 hello 수 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-179">**Step 3: Set executor-cores** – Since this is an I/O intensive job, we can set hello number of cores for each executor too4.</span></span>  <span data-ttu-id="b8982-180">4 가비지 컬렉션 문제를 일으킬 수 있는 보다 실행자 toolarger 당 코어를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-180">Setting cores per executor toolarger than 4 may cause garbage collection problems.</span></span>  

    executor-cores = 4
<span data-ttu-id="b8982-181">**4 단계: 클러스터의 YARN 메모리 양을 결정** – 각 D4v2 25GB의 YARN 메모리에 out tooAmbari toofind 이동 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-181">**Step 4: Determine amount of YARN memory in cluster** – We navigate tooAmbari toofind out that each D4v2 has 25GB of YARN memory.</span></span>  <span data-ttu-id="b8982-182">8 개의 노드로 구성 되므로 hello YARN 메모리가 8에 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-182">Since there are 8 nodes, hello available YARN memory is multiplied by 8.</span></span>

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
<span data-ttu-id="b8982-183">**5 단계: 계산 num executor** – hello num executor 매개 변수 hello 메모리 제약 조건 및 hello CPU 제약 조건 hello로 나눈 값의 최소 hello을 수행 하 여 결정 됩니다 # of Spark에서 실행 되는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-183">**Step 5: Calculate num-executors** – hello num-executors parameter is determined by taking hello minimum of hello memory constraint and hello CPU constraint divided by hello # of apps running on Spark.</span></span>    

<span data-ttu-id="b8982-184">**메모리 제약 조건 계산** – hello 메모리 제약 조건은 hello 총 YARN 메모리 실행자 당 hello 메모리로 나눈 값으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-184">**Calculate memory constraint** – hello memory constraint is calculated as hello total YARN memory divided by hello memory per executor.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
<span data-ttu-id="b8982-185">**CPU 제약 조건 계산** -hello CPU 제약 조건이 hello 총 yarn 코어 hello 실행자 당 코어 수로 나눈 값으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8982-185">**Calculate CPU constraint** - hello CPU constraint is calculated as hello total yarn cores divided by hello number of cores per executor.</span></span>
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
<span data-ttu-id="b8982-186">**num-executors 설정**</span><span class="sxs-lookup"><span data-stu-id="b8982-186">**Set num-executors**</span></span>

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

