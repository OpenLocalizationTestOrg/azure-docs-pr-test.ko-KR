---
title: "Azure Data Lake Store MapReduce 성능 조정 지침 | Microsoft Docs"
description: "Azure Data Lake Store MapReduce 성능 조정 지침"
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
ms.openlocfilehash: 9528148792f083cb0e48d356e61cf61762ee954f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="175c4-103">HDInsight and Azure Data Lake Store에서 MapReduce에 대한 성능 조정 지침</span><span class="sxs-lookup"><span data-stu-id="175c4-103">Performance tuning guidance for MapReduce on HDInsight and Azure Data Lake Store</span></span>


## <a name="prerequisites"></a><span data-ttu-id="175c4-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="175c4-104">Prerequisites</span></span>

* <span data-ttu-id="175c4-105">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="175c4-105">**An Azure subscription**.</span></span> <span data-ttu-id="175c4-106">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="175c4-106">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="175c4-107">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="175c4-107">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="175c4-108">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="175c4-108">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="175c4-109">**Azure HDInsight 클러스터** 입니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-109">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="175c4-110">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="175c4-110">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="175c4-111">클러스터에 대한 원격 데스크톱을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-111">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="175c4-112">**HDInsight에서 MapReduce 사용**.</span><span class="sxs-lookup"><span data-stu-id="175c4-112">**Using MapReduce on HDInsight**.</span></span>  <span data-ttu-id="175c4-113">자세한 내용은 [HDInsight에서 Hadoop과 MapReduce 사용](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="175c4-113">For more information, see [Use MapReduce in Hadoop on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)</span></span>  
* <span data-ttu-id="175c4-114">**ADLS에서 성능 조정 지침**.</span><span class="sxs-lookup"><span data-stu-id="175c4-114">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="175c4-115">일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="175c4-115">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>  

## <a name="parameters"></a><span data-ttu-id="175c4-116">매개 변수</span><span class="sxs-lookup"><span data-stu-id="175c4-116">Parameters</span></span>

<span data-ttu-id="175c4-117">MapReduce 작업을 실행할 때 ADLS에서 성능을 향상시키기 위해 구성할 수 있는 가장 중요한 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-117">When running MapReduce jobs, here are the most important parameters that you can configure to increase performance on ADLS:</span></span>

* <span data-ttu-id="175c4-118">**Mapreduce.map.memory.mb** – 각 매퍼에 할당할 메모리 양</span><span class="sxs-lookup"><span data-stu-id="175c4-118">**Mapreduce.map.memory.mb** – The amount of memory to allocate to each mapper</span></span>
* <span data-ttu-id="175c4-119">**Mapreduce.job.maps** – 작업당 맵 태스크 수</span><span class="sxs-lookup"><span data-stu-id="175c4-119">**Mapreduce.job.maps** – The number of map tasks per job</span></span>
* <span data-ttu-id="175c4-120">**Mapreduce.reduce.memory.mb** – 각 리듀서에 할당할 메모리 양</span><span class="sxs-lookup"><span data-stu-id="175c4-120">**Mapreduce.reduce.memory.mb** – The amount of memory to allocate to each reducer</span></span>
* <span data-ttu-id="175c4-121">**Mapreduce.job.reduces** – 작업당 reduce 태스크 수</span><span class="sxs-lookup"><span data-stu-id="175c4-121">**Mapreduce.job.reduces** – The number of reduce tasks per job</span></span>

<span data-ttu-id="175c4-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** 맵 및/또는 리듀스 태스크에 필요한 메모리 양에 따라 이 숫자를 조정해야 합니다</span><span class="sxs-lookup"><span data-stu-id="175c4-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** This number should be adjusted based on how much memory is needed for the map and/or reduce task.</span></span>  <span data-ttu-id="175c4-123">mapreduce.map.memory 및 mapreduce.reduce.memory에 대한 기본 값은 Yarn 구성을 통해 Ambari에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-123">The default values of mapreduce.map.memory and mapreduce.reduce.memory can be viewed in Ambari via the Yarn configuration.</span></span>  <span data-ttu-id="175c4-124">Ambari에서 YARN으로 이동한 후 Configs 탭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-124">In Ambari, navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="175c4-125">YARN 메모리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-125">The YARN memory will be displayed.</span></span>  

<span data-ttu-id="175c4-126">**Mapreduce.job.maps / Mapreduce.job.reduces** 생성할 최대 매퍼 또는 리듀서 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-126">**Mapreduce.job.maps / Mapreduce.job.reduces** This will determine the maximum number of mappers or reducers to be created.</span></span>  <span data-ttu-id="175c4-127">분할 수에 따라 MapReduce 작업에 대해 생성될 매퍼 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-127">The number of splits will determine how many mappers will be created for the MapReduce job.</span></span>  <span data-ttu-id="175c4-128">따라서 분할 수가 요청한 매퍼 수보다 적은 경우 요청한 것보다 적은 수의 매퍼를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-128">Therefore, you may get less mappers than you requested if there are less splits than the number of mappers requested.</span></span>       

## <a name="guidance"></a><span data-ttu-id="175c4-129">인도</span><span class="sxs-lookup"><span data-stu-id="175c4-129">Guidance</span></span>

<span data-ttu-id="175c4-130">**1단계: 실행 중인 작업 수 결정** - 기본적으로 MapReduce는 작업에 대한 전체 클러스터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-130">**Step 1: Determine number of jobs running** - By default, MapReduce will use the entire cluster for your job.</span></span>  <span data-ttu-id="175c4-131">제공되는 컨테이너보다 적은 수의 매퍼를 사용하면 클러스터를 덜 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-131">You can use less of the cluster by using less mappers than there are available containers.</span></span>  <span data-ttu-id="175c4-132">이 문서의 내용에서는 응용 프로그램이 클러스터에서 실행 중인 유일한 응용 프로그램이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-132">The guidance in this document assumes that your application is the only application running on your cluster.</span></span>      

<span data-ttu-id="175c4-133">**2단계: mapreduce.map.memory/mapreduce.reduce.memory 설정** –  맵 및 리듀스 태스크에 대한 메모리 크기는 작업에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-133">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** –  The size of the memory for map and reduce tasks will be dependent on your specific job.</span></span>  <span data-ttu-id="175c4-134">동시성을 늘리려면 메모리 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-134">You can reduce the memory size if you want to increase concurrency.</span></span>  <span data-ttu-id="175c4-135">동시에 실행 중인 태스크 수는 컨테이너 수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-135">The number of concurrently running tasks depends on the number of containers.</span></span>  <span data-ttu-id="175c4-136">매퍼 또는 리듀서당 메모리 양을 줄이면 더 많은 컨테이너를 생성할 수 있으며 따라서 더 많은 매퍼 또는 리듀서를 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-136">By decreasing the amount of memory per mapper or reducer, more containers can be created, which enable more mappers or reducers to run concurrently.</span></span>  <span data-ttu-id="175c4-137">메모리 양을 너무 많이 줄이면 일부 프로세스에서 메모리 부족이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-137">Decreasing the amount of memory too much may cause some processes to run out of memory.</span></span>  <span data-ttu-id="175c4-138">작업을 실행할 때 힙 오류가 발생하면 매퍼 또는 리듀서당 메모리를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-138">If you get a heap error when running your job, you should increase the memory per mapper or reducer.</span></span>  <span data-ttu-id="175c4-139">더 많은 컨테이너를 추가하면 각 컨테이너당 오버헤드가 더 추가되며 이로 인해 성능이 저하될 수 있다는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-139">You should consider that adding more containers will add extra overhead for each additional container, which can potentially degrade performance.</span></span>  <span data-ttu-id="175c4-140">다른 대안은 메모리가 많은 클러스터를 사용하거나 클러스터의 노드 수를 늘려 더 많은 메모리를 확보하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-140">Another alternative is to get more memory by using a cluster that has higher amounts of memory or increasing the number of nodes in your cluster.</span></span>  <span data-ttu-id="175c4-141">메모리가 많아지면 더 많은 컨테이너가 사용되며 이것은 동시성 증가로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-141">More memory will enable more containers to be used, which means more concurrency.</span></span>  

<span data-ttu-id="175c4-142">**3단계: 총 YARN 메모리 결정** - mapreduce.job.maps/mapreduce.job.reduces를 조정하려면 사용할 수 있는 총 YARN 메모리 양을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-142">**Step 3: Determine Total YARN memory** - To tune mapreduce.job.maps/mapreduce.job.reduces, you should consider the amount of total YARN memory available for use.</span></span>  <span data-ttu-id="175c4-143">이 정보는 Ambari에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-143">This information is available in Ambari.</span></span>  <span data-ttu-id="175c4-144">YARN으로 이동한 후 Configs 탭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-144">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="175c4-145">이 창에 YARN 메모리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-145">The YARN memory is displayed in this window.</span></span>  <span data-ttu-id="175c4-146">YARN 메모리에 클러스터에 있는 노드 수를 곱하여 총 YARN 메모리를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-146">You should multiply the YARN memory with the number of nodes in your cluster to get the total YARN memory.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="175c4-147">비어 있는 클러스터를 사용 중인 경우 이 메모리가 클러스터의 총 YARN 메모리일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-147">If you are using an empty cluster, then memory can be the total YARN memory for your cluster.</span></span>  <span data-ttu-id="175c4-148">다른 응용 프로그램에서 메모리를 사용하고 있으면 매퍼 또는 리듀서 수를 사용하려는 컨테이너 수로 줄여서 클러스터 메모리 중에서 일부만 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-148">If other applications are using memory, then you can choose to only use a portion of your cluster’s memory by reducing the number of mappers or reducers to the number of containers you want to use.</span></span>  

<span data-ttu-id="175c4-149">**4단계: YARN 컨테이너 수 계산** – YARN 컨테이너는 작업에 대해 사용 가능한 동시성의 양을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-149">**Step 4: Calculate number of YARN containers** – YARN containers dictate the amount of concurrency available for the job.</span></span>  <span data-ttu-id="175c4-150">총 YARN 메모리를 가져와 mapreduce.map.memory로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-150">Take total YARN memory and divide that by mapreduce.map.memory.</span></span>  

    # of YARN containers = total YARN memory / mapreduce.map.memory

<span data-ttu-id="175c4-151">**5단계: mapreduce.job.maps/mapreduce.job.reduces 설정** mapreduce.job.maps/mapreduce.job.reduces를 사용 가능한 컨테이너 수 이상의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-151">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces** Set mapreduce.job.maps/mapreduce.job.reduces to at least the number of available containers.</span></span>  <span data-ttu-id="175c4-152">매퍼 및 리듀서 수를 늘리면 더 나은 성능을 얻을 수 있는지 실험해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-152">You can experiment further by increasing the number of mappers and reducers to see if you get better performance.</span></span>  <span data-ttu-id="175c4-153">매퍼 수가 늘어나면 추가 오버헤드가 발생하므로 매퍼 수가 너무 많으면 성능이 저하될 수 있음에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-153">Keep in mind that more mappers will have additional overhead so having too many mappers may degrade performance.</span></span>  

<span data-ttu-id="175c4-154">기본적으로 CPU 예약 및 CPU 격리는 해제되어 있으므로 YARN 컨테이너 수가 메모리로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-154">CPU scheduling and CPU isolation are turned off by default so the number of YARN containers is constrained by memory.</span></span>

## <a name="example-calculation"></a><span data-ttu-id="175c4-155">계산 예</span><span class="sxs-lookup"><span data-stu-id="175c4-155">Example Calculation</span></span>

<span data-ttu-id="175c4-156">현재 D14 노드 8개로 구성된 클러스터가 있고 I/O 집약적인 작업을 실행하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-156">Let’s say you currently have a cluster composed of 8 D14 nodes and you want to run an I/O intensive job.</span></span>  <span data-ttu-id="175c4-157">수행할 계산은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-157">Here are the calculations you should do:</span></span>

<span data-ttu-id="175c4-158">**1단계: 실행 중인 작업 수 결정** - 이 예에서는 이 작업이 실행 중인 유일한 작업이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-158">**Step 1: Determine number of jobs running** - for our example, we assume that our job is the only one running.</span></span>  

<span data-ttu-id="175c4-159">**2단계: mapreduce.map.memory/mapreduce.reduce.memory 설정** – 이 예에서는 I/O 집약적인 작업을 실행 중이고 맵 태스크에 대해 3GB 메모리면 충분하다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-159">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** – for our example, you are running an I/O intensive job and decide that 3GB of memory for map tasks will be sufficient.</span></span>

    mapreduce.map.memory = 3GB
<span data-ttu-id="175c4-160">**3단계: 총 YARN 메모리 결정**</span><span class="sxs-lookup"><span data-stu-id="175c4-160">**Step 3: Determine Total YARN memory**</span></span>

    total memory from the cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
<span data-ttu-id="175c4-161">**4단계: YARN 컨테이너 수 결정**</span><span class="sxs-lookup"><span data-stu-id="175c4-161">**Step 4: Calculate # of YARN containers**</span></span>

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

<span data-ttu-id="175c4-162">**5단계: mapreduce.job.maps/mapreduce.job.reduces 설정**</span><span class="sxs-lookup"><span data-stu-id="175c4-162">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces**</span></span>

    mapreduce.map.jobs = 256

## <a name="limitations"></a><span data-ttu-id="175c4-163">제한 사항</span><span class="sxs-lookup"><span data-stu-id="175c4-163">Limitations</span></span>

<span data-ttu-id="175c4-164">**ADLS 제한**</span><span class="sxs-lookup"><span data-stu-id="175c4-164">**ADLS throttling**</span></span>

<span data-ttu-id="175c4-165">다중 테넌트 서비스로 ADLS는 계정 수준 대역폭 제한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-165">As a multi-tenant service, ADLS sets account level bandwidth limits.</span></span>  <span data-ttu-id="175c4-166">이러한 제한에 도달하면 태스크 실패가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-166">If you hit these limits, you will start to see task failures.</span></span> <span data-ttu-id="175c4-167">이것은 태스크 로그에서 제한 오류를 확인하여 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-167">This can be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="175c4-168">작업에 대한 대역폭이 더 필요한 경우 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="175c4-168">If you need more bandwidth for your job, please contact us.</span></span>   

<span data-ttu-id="175c4-169">제한 여부를 확인하려면 클라이언트 쪽에서 디버그 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-169">To check if you are getting throttled, you need to enable the debug logging on the client side.</span></span> <span data-ttu-id="175c4-170">그 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-170">Here’s how you can do that:</span></span>

1. <span data-ttu-id="175c4-171">Ambari > YARN > Config > Advanced yarn-log4j에서 log4j 속성에 다음 속성을 배치합니다. log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span><span class="sxs-lookup"><span data-stu-id="175c4-171">Put the following property in the log4j properties in Ambari > YARN > Config > Advanced yarn-log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span></span>

2. <span data-ttu-id="175c4-172">구성을 적용하려면 노드/서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-172">Restart all the nodes/service for the config to take effect.</span></span>

3. <span data-ttu-id="175c4-173">제한이 적용되면 YARN 로그 파일에 HTTP 429 오류 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-173">If you are getting throttled, you’ll see the HTTP 429 error code in the YARN log file.</span></span> <span data-ttu-id="175c4-174">YARN 로그 파일은 /tmp/&lt;user&gt;/yarn.log에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-174">The YARN log file is in /tmp/&lt;user&gt;/yarn.log</span></span>

## <a name="examples-to-run"></a><span data-ttu-id="175c4-175">실행 예</span><span class="sxs-lookup"><span data-stu-id="175c4-175">Examples to Run</span></span>

<span data-ttu-id="175c4-176">Azure Data Lake Store에서 MapReduce가 실행되는 방식을 보여 주기 위해 다음 설정으로 클러스터에서 실행된 샘플 코드가 아래에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-176">To demonstrate how MapReduce runs on Azure Data Lake Store, below is some sample code that was run on a cluster with the following settings:</span></span>

* <span data-ttu-id="175c4-177">16 노드 D14v2</span><span class="sxs-lookup"><span data-stu-id="175c4-177">16 node D14v2</span></span>
* <span data-ttu-id="175c4-178">HDI 3.6을 실행하는 Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="175c4-178">Hadoop cluster running HDI 3.6</span></span>

<span data-ttu-id="175c4-179">다음은 출발점으로 MapReduce Teragen, Terasort 및 Teravalidate를 실행할 몇 가지 명령 예입니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-179">For a starting point, here are some example commands to run MapReduce Teragen, Terasort, and Teravalidate.</span></span>  <span data-ttu-id="175c4-180">리소스에 따라 이러한 명령을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175c4-180">You can adjust these commands based on your resources.</span></span>

<span data-ttu-id="175c4-181">**Teragen**</span><span class="sxs-lookup"><span data-stu-id="175c4-181">**Teragen**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

<span data-ttu-id="175c4-182">**Terasort**</span><span class="sxs-lookup"><span data-stu-id="175c4-182">**Terasort**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

<span data-ttu-id="175c4-183">**Teravalidate**</span><span class="sxs-lookup"><span data-stu-id="175c4-183">**Teravalidate**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
