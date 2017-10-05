---
title: "Distcp를 사용하여 WASB에(서) Data Lake Store 데이터 복사| Microsoft 문서"
description: "Distcp 도구를 사용하여 Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사"
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="ae2e1-103">Distcp를 사용하여 Azure 저장소 Blob과 데이터 레이크 저장소 간에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="ae2e1-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae2e1-104">DistCp 사용</span><span class="sxs-lookup"><span data-stu-id="ae2e1-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="ae2e1-105">AdlCopy 사용</span><span class="sxs-lookup"><span data-stu-id="ae2e1-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="ae2e1-106">Data Lake Store 계정에 액세스할 수 있는 HDInsight 클러스터를 만들었다면 Distcp와 같은 Hadoop 에코시스템 도구를 사용하여 HDInsight 클러스터 저장소(WASB) **간의** 데이터를 Data Lake Store 계정에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="ae2e1-107">이 문서에서는 이 작업을 수행하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae2e1-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ae2e1-108">Prerequisites</span></span>
<span data-ttu-id="ae2e1-109">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="ae2e1-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-110">**An Azure subscription**.</span></span> <span data-ttu-id="ae2e1-111">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ae2e1-112">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="ae2e1-113">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ae2e1-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="ae2e1-114">**Azure HDInsight 클러스터** 입니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="ae2e1-115">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="ae2e1-116">클러스터에 대한 원격 데스크톱을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="ae2e1-117">비디오로 빠르게 배우시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="ae2e1-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="ae2e1-118">[비디오를 보세요](https://mix.office.com/watch/1liuojvdx6sie) .</span><span class="sxs-lookup"><span data-stu-id="ae2e1-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="ae2e1-119">HDInsight Linux 클러스터에서 Distcp 사용</span><span class="sxs-lookup"><span data-stu-id="ae2e1-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="ae2e1-120">HDInsight 클러스터는 서로 다른 원본에서 HDInsight 클러스터로 데이터를 복사하는 데 사용할 수 있는 Distcp 유틸리티와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="ae2e1-121">데이터 레이크 저장소를 추가 저장소로 사용하도록 HDInsight 클러스터를 구성한 경우 Distcp 유틸리티는 기본적으로 데이터 레이크 저장소 계정으로/에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="ae2e1-122">이 섹션에서는 Distcp 유틸리티를 사용하는 방법에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="ae2e1-123">데스크탑에서 SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="ae2e1-124">[Linux 기반 HDInsight 클러스터에 연결](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="ae2e1-125">SSH 프롬프트에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="ae2e1-126">Azure 저장소 Blob(WASB)에 액세스할 수 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="ae2e1-127">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="ae2e1-128">저장소 Blob의 콘텐츠 목록이 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="ae2e1-129">마찬가지로 클러스터에서 데이터 레이크 저장소 계정에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="ae2e1-130">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="ae2e1-131">데이터 레이크 저장소 계정의 파일/폴더 목록이 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="ae2e1-132">Distcp를 사용하여 WASB에서 데이터 레이크 저장소 계정에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="ae2e1-133">이렇게 하면 WASB에 있는 **/example/data/gutenberg/** 폴더의 콘텐츠를 Data Lake Store 계정의 **/myfolder** 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="ae2e1-134">마찬가지로 Distcp를 사용하여 데이터 레이크 저장소 계정에서 WASB에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="ae2e1-135">이렇게 하면 Data Lake Store 계정에 있는 **/myfolder**의 콘텐츠를 WASB의 **/example/data/gutenberg/** 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="ae2e1-136">DistCp 사용에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ae2e1-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="ae2e1-137">DistCp의 가장 낮은 세분성은 단일 파일이므로 최대 동시 복사본 수를 설정하는 것이 Data Lake Store에서 최적화할 가장 중요한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="ae2e1-138">이것은 명령줄에서 매퍼 수(‘m’) 매개 변수를 설정하여 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="ae2e1-139">이 매개 변수는 데이터를 복사하는 데 사용되는 최대 매퍼 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="ae2e1-140">기본값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-140">Default value is 20.</span></span>

<span data-ttu-id="ae2e1-141">**예제**</span><span class="sxs-lookup"><span data-stu-id="ae2e1-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="ae2e1-142">사용할 매퍼 수는 어떻게 확인하나요?</span><span class="sxs-lookup"><span data-stu-id="ae2e1-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="ae2e1-143">다음은 사용할 수 있는 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="ae2e1-144">**1단계: 전체 YARN 메모리 확인** - 첫 번째 단계는 DistCp 작업을 실행하는 클러스터에서 사용할 수 있는 YARN 메모리를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="ae2e1-145">이 정보는 클러스터와 연결된 Ambari 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="ae2e1-146">YARN으로 이동한 후 Configs 탭에서 YARN 메모리를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="ae2e1-147">전체 YARN 메모리를 알려면 노드당 YARN 메모리와 클러스터에 있는 노드 수를 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="ae2e1-148">**2단계: 매퍼 수 계산** - **m** 값은 전체 YARN 메모리를 YARN 컨테이너 크기로 나눈 몫과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="ae2e1-149">YARN 컨테이너 크기 정보도 Ambari 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="ae2e1-150">YARN으로 이동한 후 Configs 탭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="ae2e1-151">이 창에 YARN 컨테이너 크기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="ae2e1-152">매퍼 수(**m**)를 구하는 수식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="ae2e1-153">**예제**</span><span class="sxs-lookup"><span data-stu-id="ae2e1-153">**Example**</span></span>

<span data-ttu-id="ae2e1-154">클러스터에 4개의 D14v2 노드가 있고 10개의 다른 폴더에서 10TB의 데이터를 전송하려고 한다고 가정해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="ae2e1-155">각 폴더에는 다양한 크기의 데이터가 포함되고 각 폴더 내의 파일 크기는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="ae2e1-156">전체 YARN 메모리 - Ambari 포털에서 D14 노드 1개의 YARN 메모리가 96GB임을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="ae2e1-157">따라서 4노드 클러스터의 전체 YARN 메모리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="ae2e1-158">매퍼 수 - Ambari 포털에서 D14 클러스터 노드 1개에 대한 YARN 컨테이너 크기는 3072임을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="ae2e1-159">따라서 매퍼 수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="ae2e1-160">다른 응용 프로그램에서 메모리를 사용하고 있으면 DistCp에 대한 클러스터 YARN 메모리 중에서 일부만 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="ae2e1-161">큰 데이터 집합 복사</span><span class="sxs-lookup"><span data-stu-id="ae2e1-161">Copying large datasets</span></span>

<span data-ttu-id="ae2e1-162">이동해야 하는 데이터 집합의 크기가 매우 큰 경우(예: 1TB 초과) 또는 많은 다른 폴더가 포함된 경우 여러 DistCp 작업을 사용하는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="ae2e1-163">성능이 좋아지지는 않을 수 있지만 작업이 분산되므로 한 작업이 실패해도 전체 작업이 아닌 해당 특정 작업만 다시 시작하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="ae2e1-164">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ae2e1-164">Limitations</span></span>

* <span data-ttu-id="ae2e1-165">DistCp는 성능을 최적화하기 위해 크기가 서로 비슷한 매퍼를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="ae2e1-166">매퍼 수를 늘린다고 항상 성능이 증가하는 것은 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="ae2e1-167">DistCp는 파일당 하나의 매퍼로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="ae2e1-168">따라서 파일 개수보다 매퍼가 더 많지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="ae2e1-169">DistCp는 파일에 하나의 매퍼를 할당하므로 큰 파일을 복사하는 데 사용할 수 있는 동시성 크기가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="ae2e1-170">적은 수의 큰 파일이 있는 경우 이러한 파일을 256MB 파일 청크로 나누면 동시성이 높아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="ae2e1-171">Azure Blob Storage 계정에서 복사하는 경우 Blob Storage 쪽에서 복사 작업이 제한될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="ae2e1-172">이로 인해 복사 작업의 성능이 저하됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="ae2e1-173">Azure Blob Storage의 제한에 대한 자세한 내용은 [Azure 구독 및 서비스 제한](../azure-subscription-service-limits.md)에서 Azure Storage 제한을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ae2e1-174">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ae2e1-174">See also</span></span>
* [<span data-ttu-id="ae2e1-175">Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="ae2e1-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="ae2e1-176">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="ae2e1-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ae2e1-177">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="ae2e1-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ae2e1-178">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="ae2e1-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
