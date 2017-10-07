---
title: "Distcp를 사용 하 여 데이터 레이크 저장소로 WASB에서 aaaCopy 데이터 tooand | Microsoft Docs"
description: "Azure 저장소 Blob tooData 레이크 스토어에서 Distcp 도구 toocopy 데이터 tooand 사용"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="9fe8a-103">Azure 저장소 Blob 및 azure 데이터 레이크 저장소 간에 Distcp toocopy 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9fe8a-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fe8a-104">DistCp 사용</span><span class="sxs-lookup"><span data-stu-id="9fe8a-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="9fe8a-105">AdlCopy 사용</span><span class="sxs-lookup"><span data-stu-id="9fe8a-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="9fe8a-106">에 대 한 액세스 tooa 데이터 레이크 저장소 계정이 HDInsight 클러스터를 만든 후 Distcp toocopy 데이터와 같은 Hadoop 에코 시스템 도구를 사용할 수 있습니다 **에서 tooand** 데이터 레이크 저장소 계정에 HDInsight 클러스터 저장소 (WASB).</span><span class="sxs-lookup"><span data-stu-id="9fe8a-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="9fe8a-107">이 문서는 방법에 대해 설명 tooachieve이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fe8a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9fe8a-108">Prerequisites</span></span>
<span data-ttu-id="9fe8a-109">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="9fe8a-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-110">**An Azure subscription**.</span></span> <span data-ttu-id="9fe8a-111">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9fe8a-112">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="9fe8a-113">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9fe8a-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="9fe8a-114">**Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="9fe8a-115">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="9fe8a-116">Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="9fe8a-117">비디오로 빠르게 배우시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="9fe8a-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="9fe8a-118">[이 비디오를 시청](https://mix.office.com/watch/1liuojvdx6sie) 방법에 Azure 저장소 Blob와 DistCp를 사용 하 여 데이터 레이크 저장소 간에 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="9fe8a-119">HDInsight Linux 클러스터에서 Distcp 사용</span><span class="sxs-lookup"><span data-stu-id="9fe8a-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="9fe8a-120">HDInsight 클러스터는 HDInsight 클러스터에 서로 다른 원본에서 사용 되는 toocopy 데이터 될 수 있는 hello Distcp 유틸리티와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="9fe8a-121">추가 저장소로 hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 경우 hello Distcp 유틸리티 수 있습니다. 사용 된 데이터 레이크 저장소 계정에서 기본적으로 toocopy 데이터 tooand.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="9fe8a-122">이 섹션에서는 toouse Distcp 유틸리티 hello 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="9fe8a-123">바탕 화면에서 SSH tooconnect toohello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="9fe8a-124">참조 [연결 tooa Linux 기반 HDInsight 클러스터](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="9fe8a-125">Hello SSH 프롬프트에서 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="9fe8a-126">Azure 저장소 Blob (WASB) hello에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="9fe8a-127">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="9fe8a-128">이 hello 저장소 blob의 콘텐츠 목록을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="9fe8a-129">마찬가지로, hello 클러스터에서 hello 데이터 레이크 저장소 계정에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="9fe8a-130">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="9fe8a-131">이 hello Data Lake 저장소 계정에서에서 파일/폴더의 목록을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="9fe8a-132">WASB tooa Data Lake 저장소 계정에서에서 Distcp toocopy 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="9fe8a-133">이렇게 하면 hello의 hello 내용을 복사 됩니다 **/예제/데이터/gutenberg/** WASB에서 폴더 너무**/myfolder** hello Data Lake 저장소 계정에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="9fe8a-134">마찬가지로, Data Lake 저장소 계정 tooWASB에서 Distcp toocopy 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="9fe8a-135">hello 내용을 복사 됩니다 **/myfolder** hello 데이터 레이크 저장소에서에서 계정을 너무**/예제/데이터/gutenberg/** WASB에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="9fe8a-136">DistCp 사용에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="9fe8a-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="9fe8a-137">세분성은 단일 파일, 동시 복사본의 설정 hello 최대 수는 가장 중요 한 매개 변수 toooptimize hello DistCp의 가장 낮은 때문에 데이터 레이크 저장소에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="9fe8a-138">이 매퍼 hello 수를 설정 하 여 제어 됩니다 (am') hello 명령줄에서 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="9fe8a-139">이 매개 변수는 hello 매퍼 사용된 toocopy 데이터 수 있는 최대 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="9fe8a-140">기본값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-140">Default value is 20.</span></span>

<span data-ttu-id="9fe8a-141">**예제**</span><span class="sxs-lookup"><span data-stu-id="9fe8a-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="9fe8a-142">매퍼 toouse hello 수를 확인 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="9fe8a-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="9fe8a-143">다음은 사용할 수 있는 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="9fe8a-144">**1 단계: 총 YARN 메모리를 확인할** -hello 첫 번째 단계는 toodetermine hello YARN 메모리 사용 가능한 toohello 클러스터 hello DistCp 작업을 실행 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="9fe8a-145">이 정보는 hello 클러스터와 연결 된 hello Ambari 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="9fe8a-146">TooYARN 찾아 hello Configs 탭 toosee hello YARN 메모리를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="9fe8a-147">tooget hello 총 YARN 메모리 hello YARN 노드별로 메모리를 hello 노드 수와 클러스터에 있는 여러 번입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="9fe8a-148">**2 단계: 매퍼 hello 수를 계산** -의 값을 hello **m** YARN 컨테이너 크기 hello로 나눈 총 YARN 메모리의 같은 toohello quotient는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="9fe8a-149">hello YARN 컨테이너 크기 정보 hello Ambari 포털 에서도 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="9fe8a-150">TooYARN 이동한 보기 hello Configs 탭 hello YARN 컨테이너 크기가이 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="9fe8a-151">hello 수 매퍼의 수식 tooarrive hello (**m**)은</span><span class="sxs-lookup"><span data-stu-id="9fe8a-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="9fe8a-152">**예제**</span><span class="sxs-lookup"><span data-stu-id="9fe8a-152">**Example**</span></span>

<span data-ttu-id="9fe8a-153">Hello 클러스터에 4 D14v2s 노드가 있는 고 tootransfer 10TB 고치려는 가정 10 서로 다른 폴더에서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="9fe8a-154">다양 한 양의 데이터를 포함 하는 각 hello 폴더 되며 각 폴더 내의 hello 파일 크기가 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="9fe8a-155">전체 YARN-hello 해당 hello YARN 메모리 확인은 Ambari 포털에서에서 메모리가 96GB D14 노드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="9fe8a-156">따라서 4노드 클러스터의 전체 YARN 메모리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="9fe8a-157">Hello 해당 hello YARN 컨테이너 크기는 3072 D14 클러스터 노드에 대 한 확인은 Ambari 포털에서에서 매퍼-수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="9fe8a-158">따라서 매퍼 수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="9fe8a-159">다른 응용 프로그램 메모리를 사용 하는 경우 다음 선택할 수 있습니다 tooonly 사용 하 여 클러스터의 YARN 메모리의 일부 DistCp에 대 한.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="9fe8a-160">큰 데이터 집합 복사</span><span class="sxs-lookup"><span data-stu-id="9fe8a-160">Copying large datasets</span></span>

<span data-ttu-id="9fe8a-161">매우 크면 hello dataset toobe의 hello 크기 이동한 경우 (예: > 1TB) 또는 여러 폴더를 사용 하도록 설정한 경우 여러 DistCp 작업을 사용 하 여 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="9fe8a-162">가능성이 성능이 향상 되지 않습니다 있지만 모든 작업이 실패 한 경우 하기만 하면 됩니다 toorestart 해당 특정 작업 보다는 전체 작업 hello 있도록 hello 업무 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="9fe8a-163">제한 사항</span><span class="sxs-lookup"><span data-stu-id="9fe8a-163">Limitations</span></span>

* <span data-ttu-id="9fe8a-164">DistCp 크기 toooptimize 성능이 유사한 toocreate 매퍼를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="9fe8a-165">매퍼의 hello 수를 늘리면 성능 항상 늘리지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="9fe8a-166">DistCp 제한 tooonly 파일당 한 매퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="9fe8a-167">따라서 파일 개수보다 매퍼가 더 많지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="9fe8a-168">DistCp만 할당할 수 하나의 매퍼 tooa 파일을이 hello 동시 처리량을 사용 하는 toocopy 큰 파일 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="9fe8a-169">적은 수의 큰 파일을 있는 경우 256MB 파일 청크 toogive로 분할 해야 하면 더 많은 잠재적 동시성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="9fe8a-170">Azure Blob 저장소 계정에서 복사 하는 경우 복사 작업 hello blob 저장소 쪽 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="9fe8a-171">이 복사 작업의 hello 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="9fe8a-172">Azure Blob 저장소의 hello 제한에 대 한 더 toolearn 참조에서 Azure 저장소 제한 [Azure 구독 및 서비스 제한](../azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe8a-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9fe8a-173">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9fe8a-173">See also</span></span>
* [<span data-ttu-id="9fe8a-174">Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="9fe8a-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="9fe8a-175">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="9fe8a-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="9fe8a-176">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="9fe8a-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="9fe8a-177">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="9fe8a-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
