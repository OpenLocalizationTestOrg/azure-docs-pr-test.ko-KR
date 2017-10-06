---
title: "데이터 레이크 저장소 하이브 성능 튜닝 지침 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="35b9c-103">HDInsight의 Hive 및 Azure Data Lake Store에 대한 성능 조정 지침</span><span class="sxs-lookup"><span data-stu-id="35b9c-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="35b9c-104">hello 기본 설정은 통해 여러 다른 사용 사례 tooprovide 좋은 성능을 설정 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-104">hello default settings have been set tooprovide good performance across many different use cases.</span></span>  <span data-ttu-id="35b9c-105">I/O 집약적인 쿼리 하이브 튜닝된 tooget ADLS 성능이 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-105">For I/O intensive queries, Hive can be tuned tooget better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="35b9c-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="35b9c-106">Prerequisites</span></span>

* <span data-ttu-id="35b9c-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="35b9c-107">**An Azure subscription**.</span></span> <span data-ttu-id="35b9c-108">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35b9c-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="35b9c-109">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="35b9c-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="35b9c-110">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="35b9c-110">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="35b9c-111">**Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-111">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="35b9c-112">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35b9c-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="35b9c-113">Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-113">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="35b9c-114">**HDInsight에서 Hive 실행**.</span><span class="sxs-lookup"><span data-stu-id="35b9c-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="35b9c-115">[사용 하 여 HDInsight의 Hive] toolearn, HDInsight의 Hive 작업을 실행 하는 방법에 대 한 참조 (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span><span class="sxs-lookup"><span data-stu-id="35b9c-115">toolearn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="35b9c-116">**ADLS에서 성능 조정 지침**.</span><span class="sxs-lookup"><span data-stu-id="35b9c-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="35b9c-117">일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35b9c-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="35b9c-118">매개 변수</span><span class="sxs-lookup"><span data-stu-id="35b9c-118">Parameters</span></span>

<span data-ttu-id="35b9c-119">ADLS 성능 향상된을 위해 가장 중요 한 설정을 tootune hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-119">Here are hello most important settings tootune for improved ADLS performance:</span></span>

* <span data-ttu-id="35b9c-120">**hive.tez.container.size** – 각 작업에 의해 사용 되는 메모리 양을 hello</span><span class="sxs-lookup"><span data-stu-id="35b9c-120">**hive.tez.container.size** – hello amount of memory used by each tasks</span></span>

* <span data-ttu-id="35b9c-121">**tez.grouping.min-size** – 각 매퍼의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="35b9c-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="35b9c-122">**tez.grouping.max-size** – 각 매퍼의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="35b9c-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="35b9c-123">**hive.exec.reducer.bytes.per.reducer** – 각 리듀서의 크기</span><span class="sxs-lookup"><span data-stu-id="35b9c-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="35b9c-124">**hive.tez.container.size** -hello 컨테이너 크기에 따라 결정 메모리의 크기를 각 작업에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-124">**hive.tez.container.size** - hello container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="35b9c-125">이 hello 하이브에 hello 동시성 제어에 대 한 주 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-125">This is hello main input for controlling hello concurrency in Hive.</span></span>  

<span data-ttu-id="35b9c-126">**tez.grouping.min 크기** –이 매개 변수는 hello tooset 각 맵 편집기의 최소 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-126">**tez.grouping.min-size** – This parameter allows you tooset hello minimum size of each mapper.</span></span>  <span data-ttu-id="35b9c-127">Hello 수가 매퍼 Tez 선택 하는 hello이 매개이 변수 값 보다 작은 경우 Tez 여기서 설정한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-127">If hello number of mappers that Tez chooses is smaller than hello value of this parameter, then Tez will use hello value set here.</span></span>  

<span data-ttu-id="35b9c-128">**tez.grouping.max 크기** – tooset hello 각 맵 편집기의 최대 크기 hello 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-128">**tez.grouping.max-size** – hello parameter allows you tooset hello maximum size of each mapper.</span></span>  <span data-ttu-id="35b9c-129">Hello 수가 매퍼 Tez 선택 하는 hello이 매개이 변수 값 보다 큰 경우 Tez 여기서 설정한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-129">If hello number of mappers that Tez chooses is larger than hello value of this parameter, then Tez will use hello value set here.</span></span>  

<span data-ttu-id="35b9c-130">**hive.exec.reducer.bytes.per.reducer** –이 매개 변수는 각 리 듀 서의 hello 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets hello size of each reducer.</span></span>  <span data-ttu-id="35b9c-131">기본적으로 각 리듀서는 256MB입니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="35b9c-132">지침</span><span class="sxs-lookup"><span data-stu-id="35b9c-132">Guidance</span></span>

<span data-ttu-id="35b9c-133">**Hive.exec.reducer.bytes.per.reducer 설정** – hello 기본값 hello 데이터를 압축 된 경우 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-133">**Set hive.exec.reducer.bytes.per.reducer** – hello default value works well when hello data is uncompressed.</span></span>  <span data-ttu-id="35b9c-134">압축 된 데이터에 대 한 hello 리 듀 서의 hello 크기를 줄여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-134">For data that is compressed, you should reduce hello size of hello reducer.</span></span>  

<span data-ttu-id="35b9c-135">**Set hive.tez.container.size** – 각 노드에서 메모리는 yarn.nodemanager.resource.memory-mb에 의해 지정되고 기본적으로 HDI 클러스터에서 제대로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="35b9c-136">이 YARN에 hello 적합 한 메모리를 설정에 대 한 자세한 내용은 참조 [게시](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom)합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-136">For additional information on setting hello appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="35b9c-137">I/O가 많은 작업용 hello Tez 컨테이너 크기 감소 하 여 많은 병렬 처리에서 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-137">I/O intensive workloads can benefit from more parallelism by decreasing hello Tez container size.</span></span> <span data-ttu-id="35b9c-138">Hello 사용자 동시성을 향상 시키는 컨테이너가 더 이상 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-138">This gives hello user more containers which increases concurrency.</span></span>  <span data-ttu-id="35b9c-139">하지만 일부 Hive 쿼리에는 상당한 양의 메모리가 필요합니다(예: MapJoin).</span><span class="sxs-lookup"><span data-stu-id="35b9c-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="35b9c-140">Hello 작업에 충분 한 메모리가 없는 경우에 메모리 부족 예외가 런타임 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-140">If hello task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="35b9c-141">메모리 부족 예외가 표시 되 면 hello 메모리를 증가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-141">If you receive out of memory exceptions, then you should increase hello memory.</span></span>   

<span data-ttu-id="35b9c-142">hello 동시 실행 되는 작업 또는 수가 병렬 처리는 hello 총 YARN 메모리에 의해 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-142">hello concurrent number of tasks running or parallelism will be bounded by hello total YARN memory.</span></span>  <span data-ttu-id="35b9c-143">동시 작업 수를 실행할 수 hello YARN 컨테이너 수가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-143">hello number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="35b9c-144">노드당 hello YARN 메모리 toofind tooAmbari 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-144">toofind hello YARN memory per node, you can go tooAmbari.</span></span>  <span data-ttu-id="35b9c-145">TooYARN를 탐색 하 고 hello Configs 탭을 표시 합니다.  hello YARN 메모리가이 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-145">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="35b9c-146">ADLS를 사용 하 여 hello 키 tooimproving 성능을 최대한 많은 tooincrease hello 동시성입니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-146">hello key tooimproving performance using ADLS is tooincrease hello concurrency as much as possible.</span></span>  <span data-ttu-id="35b9c-147">Tez hello 되므로 tooset 하지 않고도 만들어야 하는 작업 수를 자동으로 계산 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-147">Tez automatically calculates hello number of tasks that should be created so you do not need tooset it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="35b9c-148">계산 예</span><span class="sxs-lookup"><span data-stu-id="35b9c-148">Example Calculation</span></span>

<span data-ttu-id="35b9c-149">8 노드 D14 클러스터가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-149">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="35b9c-150">제한 사항</span><span class="sxs-lookup"><span data-stu-id="35b9c-150">Limitations</span></span>
<span data-ttu-id="35b9c-151">**ADLS 제한**</span><span class="sxs-lookup"><span data-stu-id="35b9c-151">**ADLS throttling**</span></span> 

<span data-ttu-id="35b9c-152">Hello 적중 UIf toosee 작업 실패를 시작, ADLS 하 여 제공 된 대역폭의 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-152">UIf you hit hello limits of bandwidth provided by ADLS, you would start toosee task failures.</span></span> <span data-ttu-id="35b9c-153">이것은 태스크 로그에서 제한 오류를 확인하여 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-153">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="35b9c-154">Tez 컨테이너 크기를 늘려 hello 병렬 처리를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-154">You can decrease hello parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="35b9c-155">작업에 대한 동시성이 더 필요한 경우 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="35b9c-155">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="35b9c-156">toocheck 조절 됩니다 가져오는 경우, 클라이언트 쪽 hello에 대 한 로깅을 tooenable hello 디버그를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-156">toocheck if you are getting throttled, you need tooenable hello debug logging on hello client side.</span></span> <span data-ttu-id="35b9c-157">그 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-157">Here’s how you can do that:</span></span>

1. <span data-ttu-id="35b9c-158">하이브 config에서 hello log4j 속성에 속성을 다음 hello를 넣습니다. Ambari 보기에서이 작업을 수행할 수 있습니다: log4j.logger.com.microsoft.azure.datalake.store=DEBUG 모든 hello 노드/서비스를 다시 시작 hello 구성 tootake 효과입니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-158">Put hello following property in hello log4j properties in Hive config. This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all hello nodes/service for hello config tootake effect.</span></span>

2. <span data-ttu-id="35b9c-159">스로틀 가져오기는, hello 하이브 로그 파일의 hello HTTP 429 오류 코드를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-159">If you are getting throttled, you’ll see hello HTTP 429 error code in hello hive log file.</span></span> <span data-ttu-id="35b9c-160">hello 하이브 로그 파일을 /tmp/&lt;사용자&gt;/hive.log</span><span class="sxs-lookup"><span data-stu-id="35b9c-160">hello hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="35b9c-161">Hive 조정에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="35b9c-161">Further information on Hive tuning</span></span>

<span data-ttu-id="35b9c-162">Hive 쿼리를 조정하는 데 도움이 되는 몇 가지 블로그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35b9c-162">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="35b9c-163">HDInsight에서 Hadoop에 대한 Hive 쿼리 최적화</span><span class="sxs-lookup"><span data-stu-id="35b9c-163">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="35b9c-164">Hive 쿼리 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="35b9c-164">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="35b9c-165">HDInsight에서 Hive 최적화에 대한 논의</span><span class="sxs-lookup"><span data-stu-id="35b9c-165">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
