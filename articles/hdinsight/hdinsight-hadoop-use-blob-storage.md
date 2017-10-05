---
title: "HDFS 호환 가능 Azure Storage에서 데이터 쿼리 - Azure HDInsight | Microsoft Docs"
description: "Azure Storage 및 Azure Data Lake Store에서 데이터를 쿼리하고 분석을 위해 결과를 저장하는 방법을 알아봅니다."
keywords: "Blob 저장소, HDFS, 구조적 데이터, 비구조적 데이터, Data Lake Store, Hadoop 입력, Hadoop 출력, Hadoop 저장소, HDFS 입력, HDFS 출력, HDFS 저장소, WASB Azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: a44c2b363f7ebb593b9a9c5bd9e0d4fc3b4c31bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="d8963-104">Azure HDInsight 클러스터에서 Azure Storage 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="d8963-105">HDInsight 클러스터에서 데이터를 분석하기 위해 Azure Storage, Azure Data Lake Store 또는 양 쪽 모두에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="d8963-106">두 가지 저장소 옵션을 사용하면 사용자 데이터 손실 없이 계산에 사용된 HDInsight 클러스터를 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="d8963-107">Hadoop은 기본 파일 시스템의 개념을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="d8963-108">기본 파일 시스템은 기본 체계와 권한을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="d8963-109">상대 경로를 확인하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="d8963-110">HDInsight 클러스터를 만드는 과정에서 Azure Storage에서 Blob 컨테이너를 기본 파일 시스템으로 지정하거나 HDInsight 3.5를 통해 몇 가지 예외를 제외하고 Azure Storage 또는 Azure Data Lake Store를 기본 파일 시스템으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> <span data-ttu-id="d8963-111">기본 및 연결된 저장소로 Data Lake Store 사용에 대한 지원 가능성은 [HDInsight 클러스터에 대한 가용성](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-111">For the supportability of using Data Lake Store as both the default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="d8963-112">이 문서에서는 Azure Storage가 HDInsight 클러스터에서 작동하는 방식에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="d8963-113">Data Lake Store가 HDInsight 클러스터에서 작동하는 방식에 대해 알아보려면 [Azure HDInsight 클러스터에서 Azure Data Lake Store 사용](hdinsight-hadoop-use-data-lake-store.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-113">To learn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="d8963-114">HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="d8963-115">Azure Storage는 HDInsight와 매끄럽게 통합되는 강력한 범용 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="d8963-116">HDInsight는 Azure Storage의 Blob 컨테이너를 클러스터의 기본 파일 시스템으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-116">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="d8963-117">HDFS(Hadoop Distributed File System) 인터페이스를 통해 HDInsight의 전체 구성 요소 집합을 Blob로 저장된 구조적 또는 비구조적 데이터에 대해 직접 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-117">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="d8963-118">Azure Storage 계정을 만들 때 사용할 수 있는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="d8963-119">다음 표에서는 HDInsight에 지원되는 옵션에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-119">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="d8963-120">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="d8963-120">Storage account type</span></span> | <span data-ttu-id="d8963-121">저장소 계층</span><span class="sxs-lookup"><span data-stu-id="d8963-121">Storage tier</span></span> | <span data-ttu-id="d8963-122">HDInsight에서 지원됨</span><span class="sxs-lookup"><span data-stu-id="d8963-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="d8963-123">범용 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="d8963-123">General-purpose Storage Account</span></span> | <span data-ttu-id="d8963-124">Standard</span><span class="sxs-lookup"><span data-stu-id="d8963-124">Standard</span></span> | <span data-ttu-id="d8963-125">__예__</span><span class="sxs-lookup"><span data-stu-id="d8963-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="d8963-126">Premium</span><span class="sxs-lookup"><span data-stu-id="d8963-126">Premium</span></span> | <span data-ttu-id="d8963-127">아니요</span><span class="sxs-lookup"><span data-stu-id="d8963-127">No</span></span> |
> | <span data-ttu-id="d8963-128">Blob Storage 계정</span><span class="sxs-lookup"><span data-stu-id="d8963-128">Blob Storage Account</span></span> | <span data-ttu-id="d8963-129">핫</span><span class="sxs-lookup"><span data-stu-id="d8963-129">Hot</span></span> | <span data-ttu-id="d8963-130">아니요</span><span class="sxs-lookup"><span data-stu-id="d8963-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="d8963-131">쿨</span><span class="sxs-lookup"><span data-stu-id="d8963-131">Cool</span></span> | <span data-ttu-id="d8963-132">아니요</span><span class="sxs-lookup"><span data-stu-id="d8963-132">No</span></span> |

<span data-ttu-id="d8963-133">기본 Blob 컨테이너는 비즈니스 데이터를 저장하는 데 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-133">We do not recommend that you use the default blob container for storing business data.</span></span> <span data-ttu-id="d8963-134">저장소 비용을 줄이기 위해 사용한 후에는 매번 기본 Blob 컨테이너를 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-134">Deleting the default blob container after each use to reduce storage cost is a good practice.</span></span> <span data-ttu-id="d8963-135">기본 컨테이너에는 응용 프로그램 및 시스템 로그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-135">Note that the default container contains application and system logs.</span></span> <span data-ttu-id="d8963-136">컨테이너를 삭제하기 전에 이러한 로그를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-136">Make sure to retrieve the logs before deleting the container.</span></span>

<span data-ttu-id="d8963-137">여러 클러스터에 대해 하나의 Blob 컨테이너를 공유하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="d8963-138">HDInsight 저장소 아키텍처</span><span class="sxs-lookup"><span data-stu-id="d8963-138">HDInsight storage architecture</span></span>
<span data-ttu-id="d8963-139">다음 다이어그램은 Azure Storage 사용의 HDInsight 저장소 아키텍처의 추상 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-139">The following diagram provides an abstract view of the HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="d8963-140">![Hadoop 클러스터는 HDFS API를 사용하여 Blob Storage의 구조적 및 비구조적 데이터에 액세스하고 저장합니다.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage 아키텍처")</span><span class="sxs-lookup"><span data-stu-id="d8963-140">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="d8963-141">HDInsight는 컴퓨터 노드에 로컬로 연결된 분산 파일 시스템에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-141">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="d8963-142">정규화된 URI를 사용하여 이 파일 시스템에 액세스할 수 있습니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d8963-142">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="d8963-143">또한 HDInsight를 통해 Azure Storage에 저장된 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-143">In addition, HDInsight allows you to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="d8963-144">구문은 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="d8963-144">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="d8963-145">다음은 HDInsight 클러스터와 Azure Storage 계정을 사용하는 경우 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="d8963-146">**클러스터에 연결된 저장소 계정의 컨테이너:** 계정 이름과 키는 만들기 중 클러스터와 연결되므로 사용자는 이러한 컨테이너의 Blob에 대한 모든 권한을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-146">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="d8963-147">**클러스터에 연결되지 않은 저장소 계정의 공용 컨테이너 또는 공용 Blob:** 컨테이너의 Blob에 대한 읽기 전용 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-147">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d8963-148">공용 컨테이너를 사용하면 해당 컨테이너에서 사용할 수 있는 모든 Blob 목록 및 컨테이너 메타데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-148">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="d8963-149">공용 Blob을 사용하면 정확한 URL을 아는 경우에만 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-149">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="d8963-150">자세한 내용은 <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">컨테이너 및 Blob에 대한 액세스 제한</a>을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d8963-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="d8963-151">**클러스터에 연결되지 않은 저장소 계정의 개인 컨테이너:** WebHCat 작업을 제출할 때 저장소 계정을 정의하지 않는 경우 컨테이너의 Blob에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-151">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="d8963-152">이것은 문서 뒷부분에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-152">This is explained later in this article.</span></span>

<span data-ttu-id="d8963-153">만들기 프로세스에서 정의된 저장소 계정과 해당 키는 클러스터 노드의 %HADOOP_HOME%/conf/core-site.xml에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-153">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="d8963-154">HDInsight의 기본 동작은 core-site.xml 파일에 정의된 저장소 계정을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-154">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="d8963-155">[Ambari](./hdinsight-hadoop-manage-ambari.md)를 사용하여 이 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="d8963-156">Hive, MapReduce, Hadoop 스트리밍 및 Pig를 비롯한 여러 WebHCat 작업은 저장소 계정 및 메타데이터 설명을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="d8963-157">(현재 메타데이터가 아닌 저장소 계정이 있는 Pig에서 작동합니다.) 자세한 내용은 [대체 저장소 계정 및 Metastore와 HDInsight 클러스터 사용](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="d8963-158">구조적 및 비구조적 데이터에 대한 Blob을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="d8963-159">Blob 컨테이너는 키/값 쌍으로 데이터를 저장하며, 디렉터리 계층 구조는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="d8963-160">그러나 파일이 디렉터리 구조 내에 저장된 것처럼 보이도록 키 이름에 슬래쉬 문자(/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-160">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="d8963-161">예를 들어 Blob의 키 이름을 *input/log1.txt*로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="d8963-162">실제로 *input* 디렉터리는 없지만 키 이름에 슬래쉬 문자가 있으므로 파일 경로처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-162">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

## <span data-ttu-id="d8963-163"><a id="benefits"></a>Azure Storage의 이점</span><span class="sxs-lookup"><span data-stu-id="d8963-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="d8963-164">계산 클러스터 및 저장소 리소스의 공동 배치에 따른 암시적 성능 비용은 계산 클러스터를 Azure 지역 내의 저장소 계정 리소스 근처에 만드는 방식으로 완화됩니다. 여기서 고속 네트워크 환경은 계산 노드가 Azure Storage 내에 있는 데이터에 효율적으로 액세스하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-164">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="d8963-165">HDFS 대신 Azure Storage에 데이터를 저장할 경우 몇 가지 이점이 있습니다:</span><span class="sxs-lookup"><span data-stu-id="d8963-165">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="d8963-166">**데이터 다시 사용 및 공유:** HDFS의 데이터는 계산 클러스터 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-166">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="d8963-167">계산 클러스터에 액세스할 수 있는 응용 프로그램만 HDFS API를 통해 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-167">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="d8963-168">Azure Storage의 데이터는 HDFS API 또는 [Blob Storage REST API][blob-storage-restAPI]를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-168">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="d8963-169">따라서 데이터의 생성과 소비에 더 많은 응용 프로그램(기타 HDInsight 클러스터 포함)과 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="d8963-170">**데이터 보관:** Azure Storage에 데이터를 저장하면 계산에 사용된 HDInsight 클러스터를 사용자 데이터 손실 없이 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-170">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="d8963-171">**데이터 저장 비용:** 데이터를 장기간 저장하는 경우 DFS에 저장하는 것이 Azure Storage에 저장하는 것보다 비용이 많이 드는데, 이는 계산 클러스터의 비용이 Azure Storage의 비용보다 비싸기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-171">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="d8963-172">또한 계산 클러스터를 생성할 때마다 데이터를 다시 로드할 필요가 없기 때문에 데이터 로드 비용도 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-172">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="d8963-173">**탄력적인 확장:** HDFS는 확장된 파일 시스템을 제공하지만, 확장은 클러스터에 대해 만드는 노드의 수에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="d8963-174">규모를 변경하는 것이 Azure Storage에서 자동으로 수행되는 탄력적인 확장 기능에 의존하는 것보다 더 복잡한 프로세스가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-174">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="d8963-175">**지역에서 복제:** Azure Storage를 지역에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="d8963-176">이 경우 지리적 복구와 데이터 중복 기능이 제공되지만, 지역에서 복제된 위치에 대한 장애 조치(Failover)는 성능에 심각한 영향을 미치게 되며 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-176">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="d8963-177">따라서 지역에서 복제 기능은 추가 비용을 감수할 만큼 가치 있는 데이터에 한해서만 현명하게 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-177">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="d8963-178">특정 MapReduce 작업과 패키지는 Azure Storage에 전혀 저장하고 싶지 않을 만한 중간 결과를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="d8963-179">그런 경우에는 로컬 HDFS에 데이터를 저장하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-179">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="d8963-180">실제로 HDInsight는 Hive 작업 및 기타 프로세스에서 생성되는 이러한 중간 결과 중 일부에 DFS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="d8963-181">대부분의 HDFS 명령(예를 들어, <b>ls</b>, <b>copyFromLocal</b> 및 <b>mkdir</b>)은 여전히 예상대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="d8963-182"><b>fschk</b> 및 <b>dfsadmin</b> 등 기본 HDFS 구현(DFS라고 함)에 특정된 명령만이 Azure Storage에서 다르게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-182">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="d8963-183">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d8963-183">Create Blob containers</span></span>
<span data-ttu-id="d8963-184">Blob을 사용하려면 먼저 [Azure Storage 계정][azure-storage-create]을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-184">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="d8963-185">이 작업의 일부로 저장소 계정이 만들어지는 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-185">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="d8963-186">클러스터와 저장소 계정은 동일한 지역에서 호스팅되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-186">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="d8963-187">Hive Metastore SQL Server 데이터베이스 및 Oozie Metastore SQL Server 데이터베이스도 동일한 지역에 위치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-187">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="d8963-188">어디에 있든, 만들어진 각 Blob은 Azure Storage 계정의 일부 컨테이너에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-188">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="d8963-189">이 컨테이너는 HDInsight 외부에 생성된 기존 Blob일 수도 있고 HDInsight 클러스터용으로 생성된 컨테이너일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="d8963-190">기본 Blob 컨테이너는 작업 기록 및 로그와 같은 클러스터 특정 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-190">The default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="d8963-191">여러 HDInsight 클러스터의 기본 Blob 컨테이너를 공유하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="d8963-192">이 경우 작업 기록이 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-192">This might corrupt job history.</span></span> <span data-ttu-id="d8963-193">각 클러스터에 다른 컨테이너를 사용하고 기본 저장소 계정 대신 모든 관련 클러스터 배포에 지정된 연결 저장소 계정에서 공유 데이터를 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-193">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="d8963-194">연결된 저장소 계정에 대한 자세한 내용은 [HDInsight 클러스터 만들기][hdinsight-creation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="d8963-195">그러나 원래 HDInsight 클러스터를 삭제한 후에 기본 저장소 컨테이너를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-195">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="d8963-196">HBase 클러스터의 경우 삭제된 HBase 클러스터에서 사용되는 기본 Blob 컨테이너를 사용하여 새 HBase 클러스터를 만듦으로써 HBase 테이블 스키마 및 데이터를 실제로 보존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-196">For HBase clusters, you can actually retain the HBase table schema and data by creating a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-the-azure-portal"></a><span data-ttu-id="d8963-197">Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-197">Use the Azure portal</span></span>
<span data-ttu-id="d8963-198">포털에서 HDInsight 클러스터를 만드는 경우 저장소 계정 세부 정보를 제공할 수 있는 옵션(아래 그림 참조)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-198">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="d8963-199">추가 저장소 계정을 클러스터와 연결할지 여부를 지정할 수도 있으며, 연결하려는 경우, Data Lake Store 또는 다른 Azure Storage Blob을 추가 저장소로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-199">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![HDInsight Hadoop 만들기 데이터 원본](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="d8963-201">HDInsight 클러스터와 다른 위치에서는 추가 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-201">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="d8963-202">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-202">Use Azure PowerShell</span></span>
<span data-ttu-id="d8963-203">[Azure PowerShell을 설치하고 구성한][powershell-install] 경우 Azure PowerShell 프롬프트에서 다음을 사용하여 저장소 계정 및 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-203">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="d8963-204">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="d8963-205">[Azure CLI를 설치 및 구성한](../cli-install-nodejs.md)경우, 다음 명령을 사용하여 저장소 계정 및 컨테이너를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-205">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="d8963-206">`--type` 매개 변수는 저장소 계정이 복제된 방식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-206">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="d8963-207">자세한 내용은 [Azure Storage 복제](../storage/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="d8963-208">ZRS에서 페이지 Blob, 파일, 테이블 또는 큐를 지원하지 않으므로 ZRS를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="d8963-209">저장소 계정에 생성된 지리적 지역을 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-209">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="d8963-210">HDInsight 클러스터를 만들려는 동일한 지역에 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-210">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="d8963-211">저장소 계정을 만든 후 다음 명령을 사용하여 저장소 계정 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-211">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="d8963-212">컨테이너를 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-212">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="d8963-213">Azure Storage에서 파일 주소 지정</span><span class="sxs-lookup"><span data-stu-id="d8963-213">Address files in Azure storage</span></span>
<span data-ttu-id="d8963-214">HDInsight에서 Azure Storage의 파일에 액세스하기 위한 URI 구성표는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-214">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="d8963-215">URI 체계는 암호화되지 않은 액세스(*wasb:* 접두사가 있음)와 SSL로 암호화된 액세스(*wasbs*가 있음)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-215">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="d8963-216">Azure의 동일한 지역에 있는 데이터에 액세스하는 경우에도 가능하면 *wasbs*를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="d8963-217">&lt;BlobStorageContainerName&gt;은 Azure Storage에서 Blob 컨테이너의 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-217">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="d8963-218">&lt;StorageAccountName&gt;은 Azure Storage 계정 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-218">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="d8963-219">FQDN(정규화된 도메인 이름)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="d8963-220">&lt;BlobStorageContainerName&gt;과 &lt;StorageAccountName&gt;이 둘 다 지정되지 않은 경우 기본 파일 시스템이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="d8963-221">기본 파일 시스템의 파일에 대해서는 상대 경로나 절대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-221">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="d8963-222">예를 들어, HDInsight 클러스터와 함께 제공되는 *hadoop-mapreduce-examples.jar* 파일을 가리킬 때 다음 중 하나를 사용할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="d8963-222">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="d8963-223">HDInsight 버전 2.1 및 1.6 클러스터에서는 파일 이름이<i>hadoop-examples.jar</i>입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-223">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="d8963-224">&lt;경로&gt;는 파일 또는 디렉터리 HDFS 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-224">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="d8963-225">Azure Storage의 컨테이너는 단지 키-값 저장소이므로 실제 계층적 파일 시스템이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="d8963-226">Blob 키 내부의 슬래쉬 문자(/)는 디렉터리 구분기호로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="d8963-227">예를 들어 *hadoop-mapreduce-examples.jar* 의 Blob 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-227">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="d8963-228">HDInsight 외부에서 blob를 작업할 때 대부분의 유틸리티는 WASB 형식을 인식하지 않으며 대신 `example/jars/hadoop-mapreduce-examples.jar`과 같은 기본 경로 형식을 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-228">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="d8963-229">Blob 액세스</span><span class="sxs-lookup"><span data-stu-id="d8963-229">Access blobs</span></span> 


### <span data-ttu-id="d8963-230"><a name="access-blobs-using-azure-powershell"></a> Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="d8963-231">이 섹션의 명령은 PowerShell을 사용하여 blob에 저장된 데이터에 액세스하는 기본 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="d8963-232">HDInsight와의 작업에 대해 사용자 지정되는 더 완전한 기능의 예는 [HDInsight 도구](https://github.com/Blackmist/hdinsight-tools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="d8963-233">다음 명령을 사용하여 Blob 관련 cmdlet을 나열합니다:</span><span class="sxs-lookup"><span data-stu-id="d8963-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![Blob 관련 PowerShell cmdlet의 목록입니다.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="d8963-235">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d8963-235">Upload files</span></span>
<span data-ttu-id="d8963-236">[HDInsight에 데이터 업로드][hdinsight-upload-data]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="d8963-237">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="d8963-237">Download files</span></span>
<span data-ttu-id="d8963-238">다음 스크립트를 실행하면 블록 Blob이 현재 폴더로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="d8963-239">스크립트를 실행하기 전에 디렉터리를 쓰기 권한이 있는 폴더로 변경하십시오.</span><span class="sxs-lookup"><span data-stu-id="d8963-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="d8963-240">리소스 그룹 이름 및 클러스터 이름을 제공할 때 다음 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="d8963-241">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="d8963-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="d8963-242">파일 나열</span><span class="sxs-lookup"><span data-stu-id="d8963-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="d8963-243">정의되지 않은 저장소 계정을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="d8963-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="d8963-244">이 샘플에서는 만들기 프로세스 중에 정의되지 않은 저장소 계정에서 폴더를 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="d8963-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="d8963-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="d8963-246">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-246">Use Azure CLI</span></span>
<span data-ttu-id="d8963-247">다음 명령을 사용하여 Blob 관련 명령을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-247">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="d8963-248">**파일을 업로드하기 위해 Azure CLI를 사용하는 예제**</span><span class="sxs-lookup"><span data-stu-id="d8963-248">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="d8963-249">**파일을 다운로드하기 위해 Azure CLI를 사용하는 예제**</span><span class="sxs-lookup"><span data-stu-id="d8963-249">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="d8963-250">**파일을 삭제하기 위해 Azure CLI를 사용하는 예제**</span><span class="sxs-lookup"><span data-stu-id="d8963-250">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="d8963-251">**파일을 나열하기 위해 Azure CLI를 사용하는 예제**</span><span class="sxs-lookup"><span data-stu-id="d8963-251">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="d8963-252">추가 저장소 계정 사용</span><span class="sxs-lookup"><span data-stu-id="d8963-252">Use additional storage accounts</span></span>

<span data-ttu-id="d8963-253">HDInsight 클러스터를 만드는 동안 클러스터와 연결할 Azure Storage 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-253">While creating an HDInsight cluster, you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="d8963-254">만들기 프로세스 중이나 클러스터를 만든 후에 이 저장소 계정 외에도 동일한 Azure 구독 또는 다른 Azure 구독에서 저장소 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-254">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="d8963-255">저장소 계정 추가에 대한 지침은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="d8963-256">HDInsight 클러스터와 다른 위치에서는 추가 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-256">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8963-257">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8963-257">Next steps</span></span>
<span data-ttu-id="d8963-258">이 문서에서는 HDInsight로 HDFS 호환 Azure Storage를 사용하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-258">In this article, you learned how to use HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="d8963-259">이제 장기적이고 확장성 있는 보관 데이터 취득 솔루션을 구축할 수 있으며, 저장된 구조적 및 비구조적 데이터 내부의 정보를 활용하는 데 HDInsight를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8963-259">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="d8963-260">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8963-260">For more information, see:</span></span>

* <span data-ttu-id="d8963-261">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d8963-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="d8963-262">Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="d8963-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="d8963-263">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d8963-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d8963-264">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d8963-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d8963-265">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d8963-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="d8963-266">[Azure Storage 공유 액세스 서명을 사용하여 HDInsight에서 데이터 액세스 제한][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="d8963-266">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
