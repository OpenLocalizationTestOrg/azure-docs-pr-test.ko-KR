---
title: "데이터 레이크 저장소 MapReduce 성능 튜닝 지침 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="6689c-103">HDInsight and Azure Data Lake Store에서 MapReduce에 대한 성능 조정 지침</span><span class="sxs-lookup"><span data-stu-id="6689c-103">Performance tuning guidance for MapReduce on HDInsight and Azure Data Lake Store</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6689c-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6689c-104">Prerequisites</span></span>

* <span data-ttu-id="6689c-105">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="6689c-105">**An Azure subscription**.</span></span> <span data-ttu-id="6689c-106">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6689c-106">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6689c-107">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="6689c-107">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="6689c-108">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6689c-108">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="6689c-109">**Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-109">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="6689c-110">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6689c-110">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="6689c-111">Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-111">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="6689c-112">**HDInsight에서 MapReduce 사용**.</span><span class="sxs-lookup"><span data-stu-id="6689c-112">**Using MapReduce on HDInsight**.</span></span>  <span data-ttu-id="6689c-113">자세한 내용은 [HDInsight에서 Hadoop과 MapReduce 사용](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6689c-113">For more information, see [Use MapReduce in Hadoop on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)</span></span>  
* <span data-ttu-id="6689c-114">**ADLS에서 성능 조정 지침**.</span><span class="sxs-lookup"><span data-stu-id="6689c-114">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="6689c-115">일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6689c-115">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>  

## <a name="parameters"></a><span data-ttu-id="6689c-116">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6689c-116">Parameters</span></span>

<span data-ttu-id="6689c-117">MapReduce 작업을 실행할 때 ADLS에서 tooincrease 성능을 구성할 수 있습니다 hello 가장 중요 한 매개 변수 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-117">When running MapReduce jobs, here are hello most important parameters that you can configure tooincrease performance on ADLS:</span></span>

* <span data-ttu-id="6689c-118">**Mapreduce.map.memory.mb** – hello 양의 메모리 tooallocate tooeach 매퍼</span><span class="sxs-lookup"><span data-stu-id="6689c-118">**Mapreduce.map.memory.mb** – hello amount of memory tooallocate tooeach mapper</span></span>
* <span data-ttu-id="6689c-119">**Mapreduce.job.maps** – hello 작업당 맵 작업 수</span><span class="sxs-lookup"><span data-stu-id="6689c-119">**Mapreduce.job.maps** – hello number of map tasks per job</span></span>
* <span data-ttu-id="6689c-120">**Mapreduce.reduce.memory.mb** – 메모리 tooallocate tooeach 리 듀 서의 hello 양</span><span class="sxs-lookup"><span data-stu-id="6689c-120">**Mapreduce.reduce.memory.mb** – hello amount of memory tooallocate tooeach reducer</span></span>
* <span data-ttu-id="6689c-121">**Mapreduce.job.reduces** – hello 작업당 reduce 작업 수</span><span class="sxs-lookup"><span data-stu-id="6689c-121">**Mapreduce.job.reduces** – hello number of reduce tasks per job</span></span>

<span data-ttu-id="6689c-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** 이 숫자 hello 지도에 얼마나 많은 메모리가 필요에 따라 조정 해야 및/또는 작업을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** This number should be adjusted based on how much memory is needed for hello map and/or reduce task.</span></span>  <span data-ttu-id="6689c-123">hello 및 기본값을 mapreduce.map.memory mapreduce.reduce.memory hello Yarn 구성을 통해 Ambari에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-123">hello default values of mapreduce.map.memory and mapreduce.reduce.memory can be viewed in Ambari via hello Yarn configuration.</span></span>  <span data-ttu-id="6689c-124">Ambari를 tooYARN 이동한 hello Configs 탭을 표시 합니다.  hello YARN 메모리에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-124">In Ambari, navigate tooYARN and view hello Configs tab.  hello YARN memory will be displayed.</span></span>  

<span data-ttu-id="6689c-125">**Mapreduce.job.maps / Mapreduce.job.reduces** 이 만든 매퍼 또는 이경소켓 toobe hello 최대 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-125">**Mapreduce.job.maps / Mapreduce.job.reduces** This will determine hello maximum number of mappers or reducers toobe created.</span></span>  <span data-ttu-id="6689c-126">hello MapReduce 작업에 대 한 개수 매퍼 만들어집니다 hello 분할 수가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-126">hello number of splits will determine how many mappers will be created for hello MapReduce job.</span></span>  <span data-ttu-id="6689c-127">따라서 요청 매퍼 hello 개수 보다 작은 분할이 많은 경우 요청 된 수보다 덜 매퍼 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-127">Therefore, you may get less mappers than you requested if there are less splits than hello number of mappers requested.</span></span>       

## <a name="guidance"></a><span data-ttu-id="6689c-128">지침</span><span class="sxs-lookup"><span data-stu-id="6689c-128">Guidance</span></span>

<span data-ttu-id="6689c-129">**1 단계: 실행 중인 작업의 수를 결정** -기본적으로 MapReduce에서 hello 전체 클러스터 작업에 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-129">**Step 1: Determine number of jobs running** - By default, MapReduce will use hello entire cluster for your job.</span></span>  <span data-ttu-id="6689c-130">사용 가능한 컨테이너 보다 적은 매퍼를 사용 하 여 작은 hello 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-130">You can use less of hello cluster by using less mappers than there are available containers.</span></span>  <span data-ttu-id="6689c-131">이 문서에 hello 설명서 hello만 응용 프로그램 클러스터에서 실행 중인 응용 프로그램을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-131">hello guidance in this document assumes that your application is hello only application running on your cluster.</span></span>      

<span data-ttu-id="6689c-132">**2 단계: mapreduce.map.memory/mapreduce.reduce.memory 설정** – 맵에 대 한 hello 메모리의 크기를 hello 및 줄이기 작업은 특정 작업에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-132">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** –  hello size of hello memory for map and reduce tasks will be dependent on your specific job.</span></span>  <span data-ttu-id="6689c-133">Tooincrease 동시성을 원하는 경우 hello 메모리 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-133">You can reduce hello memory size if you want tooincrease concurrency.</span></span>  <span data-ttu-id="6689c-134">hello 동시에 실행 중인 작업 수가 hello 컨테이너 수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-134">hello number of concurrently running tasks depends on hello number of containers.</span></span>  <span data-ttu-id="6689c-135">Hello 맵 편집기 또는 리 듀 서 당 메모리 양을 줄여 자세한 컨테이너를 만들 수, 동시에 더 많은 매퍼 또는 이경소켓 toorun 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-135">By decreasing hello amount of memory per mapper or reducer, more containers can be created, which enable more mappers or reducers toorun concurrently.</span></span>  <span data-ttu-id="6689c-136">너무 많이 감소 hello 메모리 양을 메모리 부족 일부 프로세스 toorun을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-136">Decreasing hello amount of memory too much may cause some processes toorun out of memory.</span></span>  <span data-ttu-id="6689c-137">작업을 실행 하는 경우 힙 오류가 발생할 경우 맵 편집기 또는 리 듀 서 당 hello 메모리를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-137">If you get a heap error when running your job, you should increase hello memory per mapper or reducer.</span></span>  <span data-ttu-id="6689c-138">더 많은 컨테이너를 추가하면 각 컨테이너당 오버헤드가 더 추가되며 이로 인해 성능이 저하될 수 있다는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-138">You should consider that adding more containers will add extra overhead for each additional container, which can potentially degrade performance.</span></span>  <span data-ttu-id="6689c-139">다른 대체에서는 tooget 메모리가 더 높은 양의 메모리를 갖고 있는 클러스터를 사용 하 여 hello 클러스터의 노드 수가 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-139">Another alternative is tooget more memory by using a cluster that has higher amounts of memory or increasing hello number of nodes in your cluster.</span></span>  <span data-ttu-id="6689c-140">더 많은 메모리를 더 많은 컨테이너 toobe을 사용 하는 더 많은 동시성 의미를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-140">More memory will enable more containers toobe used, which means more concurrency.</span></span>  

<span data-ttu-id="6689c-141">**3 단계: 총 YARN 메모리 확인** -tootune mapreduce.job.maps/mapreduce.job.reduces hello 사용 하기 위해 사용할 수 있는 총 YARN 메모리 크기를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-141">**Step 3: Determine Total YARN memory** - tootune mapreduce.job.maps/mapreduce.job.reduces, you should consider hello amount of total YARN memory available for use.</span></span>  <span data-ttu-id="6689c-142">이 정보는 Ambari에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-142">This information is available in Ambari.</span></span>  <span data-ttu-id="6689c-143">TooYARN를 탐색 하 고 hello Configs 탭을 표시 합니다.  hello YARN 메모리가이 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-143">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  <span data-ttu-id="6689c-144">클러스터 tooget hello 총 YARN 메모리에 hello 노드 수를 사용 하 여 hello YARN 메모리를 곱하기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-144">You should multiply hello YARN memory with hello number of nodes in your cluster tooget hello total YARN memory.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="6689c-145">빈 클러스터를 사용 하는 경우 메모리 클러스터에 대 한 총 YARN 메모리 hello를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-145">If you are using an empty cluster, then memory can be hello total YARN memory for your cluster.</span></span>  <span data-ttu-id="6689c-146">컨테이너의 매퍼 또는 이경소켓 toohello 번호 hello 수를 줄여 tooonly 사용 하 여 클러스터의 메모리의 부분을 선택할 수 있습니다 다른 응용 프로그램 메모리를 사용 하는 경우 원하는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-146">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s memory by reducing hello number of mappers or reducers toohello number of containers you want toouse.</span></span>  

<span data-ttu-id="6689c-147">**4 단계: YARN 컨테이너의 개수를 계산** – YARN 컨테이너 hello 작업에 사용할 수 있는 동시성의 hello 양을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-147">**Step 4: Calculate number of YARN containers** – YARN containers dictate hello amount of concurrency available for hello job.</span></span>  <span data-ttu-id="6689c-148">총 YARN 메모리를 가져와 mapreduce.map.memory로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-148">Take total YARN memory and divide that by mapreduce.map.memory.</span></span>  

    # of YARN containers = total YARN memory / mapreduce.map.memory

<span data-ttu-id="6689c-149">**5 단계: 설정 mapreduce.job.maps/mapreduce.job.reduces** mapreduce.job.maps/mapreduce.job.reduces tooat 설정 최소 hello 수가 사용 가능한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-149">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces** Set mapreduce.job.maps/mapreduce.job.reduces tooat least hello number of available containers.</span></span>  <span data-ttu-id="6689c-150">결과 실험해볼 수 더 나은 성능을 얻을 수 있는 경우 매퍼 및 이경소켓 toosee hello 수를 늘려 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-150">You can experiment further by increasing hello number of mappers and reducers toosee if you get better performance.</span></span>  <span data-ttu-id="6689c-151">매퍼 수가 늘어나면 추가 오버헤드가 발생하므로 매퍼 수가 너무 많으면 성능이 저하될 수 있음에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-151">Keep in mind that more mappers will have additional overhead so having too many mappers may degrade performance.</span></span>  

<span data-ttu-id="6689c-152">CPU 예약 및 CPU 격리는 기본적으로 해제 되어 있으므로 hello YARN 컨테이너 수가 메모리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-152">CPU scheduling and CPU isolation are turned off by default so hello number of YARN containers is constrained by memory.</span></span>

## <a name="example-calculation"></a><span data-ttu-id="6689c-153">계산 예</span><span class="sxs-lookup"><span data-stu-id="6689c-153">Example Calculation</span></span>

<span data-ttu-id="6689c-154">현재 클러스터 D14 8 개의 노드로 이루어진 있고 toorun I/O 집약적인 작업을 원하는 경우를 가정해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="6689c-154">Let’s say you currently have a cluster composed of 8 D14 nodes and you want toorun an I/O intensive job.</span></span>  <span data-ttu-id="6689c-155">다음은 작업을 수행 해야 하는 hello 계산입니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-155">Here are hello calculations you should do:</span></span>

<span data-ttu-id="6689c-156">**1 단계: 실행 중인 작업의 수를 결정** -이 예에서는 작업이 하나만 실행을 hello은 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-156">**Step 1: Determine number of jobs running** - for our example, we assume that our job is hello only one running.</span></span>  

<span data-ttu-id="6689c-157">**2단계: mapreduce.map.memory/mapreduce.reduce.memory 설정** – 이 예에서는 I/O 집약적인 작업을 실행 중이고 맵 태스크에 대해 3GB 메모리면 충분하다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-157">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** – for our example, you are running an I/O intensive job and decide that 3GB of memory for map tasks will be sufficient.</span></span>

    mapreduce.map.memory = 3GB
<span data-ttu-id="6689c-158">**3단계: 총 YARN 메모리 결정**</span><span class="sxs-lookup"><span data-stu-id="6689c-158">**Step 3: Determine Total YARN memory**</span></span>

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
<span data-ttu-id="6689c-159">**4단계: YARN 컨테이너 수 결정**</span><span class="sxs-lookup"><span data-stu-id="6689c-159">**Step 4: Calculate # of YARN containers**</span></span>

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

<span data-ttu-id="6689c-160">**5단계: mapreduce.job.maps/mapreduce.job.reduces 설정**</span><span class="sxs-lookup"><span data-stu-id="6689c-160">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces**</span></span>

    mapreduce.map.jobs = 256

## <a name="limitations"></a><span data-ttu-id="6689c-161">제한 사항</span><span class="sxs-lookup"><span data-stu-id="6689c-161">Limitations</span></span>

<span data-ttu-id="6689c-162">**ADLS 제한**</span><span class="sxs-lookup"><span data-stu-id="6689c-162">**ADLS throttling**</span></span>

<span data-ttu-id="6689c-163">다중 테넌트 서비스로 ADLS는 계정 수준 대역폭 제한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-163">As a multi-tenant service, ADLS sets account level bandwidth limits.</span></span>  <span data-ttu-id="6689c-164">이러한 한도 도달 하면 toosee 작업 실패를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-164">If you hit these limits, you will start toosee task failures.</span></span> <span data-ttu-id="6689c-165">이것은 태스크 로그에서 제한 오류를 확인하여 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-165">This can be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="6689c-166">작업에 대한 대역폭이 더 필요한 경우 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6689c-166">If you need more bandwidth for your job, please contact us.</span></span>   

<span data-ttu-id="6689c-167">toocheck 조절 됩니다 가져오는 경우, 클라이언트 쪽 hello에 대 한 로깅을 tooenable hello 디버그를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-167">toocheck if you are getting throttled, you need tooenable hello debug logging on hello client side.</span></span> <span data-ttu-id="6689c-168">그 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-168">Here’s how you can do that:</span></span>

1. <span data-ttu-id="6689c-169">Put hello hello log4j에서에서 속성에에서 속성 Ambari 다음 > YARN > 구성 > yarn log4j 고급: log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span><span class="sxs-lookup"><span data-stu-id="6689c-169">Put hello following property in hello log4j properties in Ambari > YARN > Config > Advanced yarn-log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span></span>

2. <span data-ttu-id="6689c-170">모든 hello 노드/서비스 hello 구성 tootake 효과 대 한 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-170">Restart all hello nodes/service for hello config tootake effect.</span></span>

3. <span data-ttu-id="6689c-171">사용자는 제한에 이르기, hello YARN 로그 파일의 hello HTTP 429 오류 코드를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-171">If you are getting throttled, you’ll see hello HTTP 429 error code in hello YARN log file.</span></span> <span data-ttu-id="6689c-172">hello YARN 로그 파일을 /tmp/&lt;사용자&gt;/yarn.log</span><span class="sxs-lookup"><span data-stu-id="6689c-172">hello YARN log file is in /tmp/&lt;user&gt;/yarn.log</span></span>

## <a name="examples-toorun"></a><span data-ttu-id="6689c-173">예제 tooRun</span><span class="sxs-lookup"><span data-stu-id="6689c-173">Examples tooRun</span></span>

<span data-ttu-id="6689c-174">toodemonstrate는 MapReduce Azure 데이터 레이크 저장소에서 실행 하는 방법 다음은 몇 가지 샘플 코드 hello 다음 설정으로 클러스터에서 실행 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-174">toodemonstrate how MapReduce runs on Azure Data Lake Store, below is some sample code that was run on a cluster with hello following settings:</span></span>

* <span data-ttu-id="6689c-175">16 노드 D14v2</span><span class="sxs-lookup"><span data-stu-id="6689c-175">16 node D14v2</span></span>
* <span data-ttu-id="6689c-176">HDI 3.6을 실행하는 Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="6689c-176">Hadoop cluster running HDI 3.6</span></span>

<span data-ttu-id="6689c-177">시작 지점에 대 한 몇 가지 예제 명령 toorun MapReduce Teragen, Terasort과 Teravalidate 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-177">For a starting point, here are some example commands toorun MapReduce Teragen, Terasort, and Teravalidate.</span></span>  <span data-ttu-id="6689c-178">리소스에 따라 이러한 명령을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6689c-178">You can adjust these commands based on your resources.</span></span>

<span data-ttu-id="6689c-179">**Teragen**</span><span class="sxs-lookup"><span data-stu-id="6689c-179">**Teragen**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

<span data-ttu-id="6689c-180">**Terasort**</span><span class="sxs-lookup"><span data-stu-id="6689c-180">**Terasort**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

<span data-ttu-id="6689c-181">**Teravalidate**</span><span class="sxs-lookup"><span data-stu-id="6689c-181">**Teravalidate**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
