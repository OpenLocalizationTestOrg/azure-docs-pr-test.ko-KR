---
title: "Azure HDInsight에서 Hadoop으로 데이터 레이크 저장소 aaaUse | Microsoft Docs"
description: "Tooquery 및 데이터를 Azure 데이터 레이크 저장소 toostore 발생 하는 방법에 대해 알아봅니다 분석 합니다."
keywords: "Blob Storage, hdfs, 구조화된 데이터, 구조화되지 않은 데이터, Data Lake Store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="874fb-104">Azure HDInsight 클러스터에 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="874fb-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="874fb-105">HDInsight 클러스터의 tooanalyze 데이터를 저장할 수 있습니다 hello 데이터 중 하나에서 [Azure 저장소](../storage/common/storage-introduction.md), [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md), 또는 둘 다 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="874fb-106">저장소 옵션을 모두 사용자 데이터의 손실 없이 계산에 사용 되는 toosafely 삭제 HDInsight 클러스터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="874fb-107">이 문서에서는 Data Lake Store가 HDInsight 클러스터에서 작동하는 방식에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="874fb-108">toolearn HDInsight 클러스터와 함께 작동 하는 Azure 저장소 참조 [사용 하 여 Azure 저장소와 Azure HDInsight 클러스터](hdinsight-hadoop-use-blob-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="874fb-109">HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="874fb-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="874fb-110">Data Lake Store는 항상 보안 채널을 통해 액세스되기 때문에 `adls` 파일 시스템 구성표 이름이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="874fb-111">항상 `adl`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="874fb-112">HDInsight 클러스터에 대한 가용성</span><span class="sxs-lookup"><span data-stu-id="874fb-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="874fb-113">Hadoop은 hello 기본 파일 시스템의 개념을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="874fb-114">hello 기본 파일 시스템에는 기본 스키마와 기관 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="874fb-115">상대 경로 사용 하는 tooresolve 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="874fb-116">Hello HDInsight 클러스터를 만드는 프로세스 동안 hello 기본 파일 시스템으로 Azure 저장소의 blob 컨테이너를 지정할 수 있습니다 또는 HDInsight 3.5 및 최신 버전을 선택할 수 있습니다 Azure 저장소 또는 Azure 데이터 레이크 저장소와 함께 hello 기본 파일 시스템으로는 몇 가지 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="874fb-117">HDInsight 클러스터는 Data Lake Store를 두 가지 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="874fb-118">Hello 기본 저장소로</span><span class="sxs-lookup"><span data-stu-id="874fb-118">As hello default storage</span></span>
* <span data-ttu-id="874fb-119">추가 저장소로, Azure Storage Blob을 기본 저장소로.</span><span class="sxs-lookup"><span data-stu-id="874fb-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="874fb-120">현재, 일부 hello HDInsight 클러스터 데이터 레이크 저장소를 사용 하 여 기본 저장소 및 저장소 계정으로 형식/버전 지원:</span><span class="sxs-lookup"><span data-stu-id="874fb-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="874fb-121">HDInsight 클러스터 유형</span><span class="sxs-lookup"><span data-stu-id="874fb-121">HDInsight cluster type</span></span> | <span data-ttu-id="874fb-122">기본 저장소로 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="874fb-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="874fb-123">추가 저장소로 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="874fb-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="874fb-124">참고</span><span class="sxs-lookup"><span data-stu-id="874fb-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="874fb-125">HDInsight 버전 3.6</span><span class="sxs-lookup"><span data-stu-id="874fb-125">HDInsight version 3.6</span></span> | <span data-ttu-id="874fb-126">예</span><span class="sxs-lookup"><span data-stu-id="874fb-126">Yes</span></span> | <span data-ttu-id="874fb-127">예</span><span class="sxs-lookup"><span data-stu-id="874fb-127">Yes</span></span> | |
| <span data-ttu-id="874fb-128">HDInsight 버전 3.5</span><span class="sxs-lookup"><span data-stu-id="874fb-128">HDInsight version 3.5</span></span> | <span data-ttu-id="874fb-129">예</span><span class="sxs-lookup"><span data-stu-id="874fb-129">Yes</span></span> | <span data-ttu-id="874fb-130">예</span><span class="sxs-lookup"><span data-stu-id="874fb-130">Yes</span></span> | <span data-ttu-id="874fb-131">HBase의 hello 예외</span><span class="sxs-lookup"><span data-stu-id="874fb-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="874fb-132">HDInsight 버전 3.4</span><span class="sxs-lookup"><span data-stu-id="874fb-132">HDInsight version 3.4</span></span> | <span data-ttu-id="874fb-133">아니요</span><span class="sxs-lookup"><span data-stu-id="874fb-133">No</span></span> | <span data-ttu-id="874fb-134">예</span><span class="sxs-lookup"><span data-stu-id="874fb-134">Yes</span></span> | |
| <span data-ttu-id="874fb-135">HDInsight 버전 3.3</span><span class="sxs-lookup"><span data-stu-id="874fb-135">HDInsight version 3.3</span></span> | <span data-ttu-id="874fb-136">아니요</span><span class="sxs-lookup"><span data-stu-id="874fb-136">No</span></span> | <span data-ttu-id="874fb-137">아니요</span><span class="sxs-lookup"><span data-stu-id="874fb-137">No</span></span> | |
| <span data-ttu-id="874fb-138">HDInsight 버전 3.2</span><span class="sxs-lookup"><span data-stu-id="874fb-138">HDInsight version 3.2</span></span> | <span data-ttu-id="874fb-139">아니요</span><span class="sxs-lookup"><span data-stu-id="874fb-139">No</span></span> | <span data-ttu-id="874fb-140">예</span><span class="sxs-lookup"><span data-stu-id="874fb-140">Yes</span></span> | |
| <span data-ttu-id="874fb-141">HDInsight 프리미엄(계층)</span><span class="sxs-lookup"><span data-stu-id="874fb-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="874fb-142">아니요</span><span class="sxs-lookup"><span data-stu-id="874fb-142">No</span></span> | <span data-ttu-id="874fb-143">아니요</span><span class="sxs-lookup"><span data-stu-id="874fb-143">No</span></span> | |
| <span data-ttu-id="874fb-144">Storm</span><span class="sxs-lookup"><span data-stu-id="874fb-144">Storm</span></span> | | |<span data-ttu-id="874fb-145">데이터 레이크 저장소 toowrite 데이터 스톰 토폴로지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="874fb-146">Storm 토폴로지에서 읽을 수 있는 참조 데이터에 Data Lake Store를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="874fb-147">데이터 레이크 저장소를 사용 하 여 추가 저장소 계정으로 해도 성능 또는 기능 tooread hello에 영향을 또는 hello 클러스터에서 tooAzure 저장소 쓰기 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="874fb-148">Data Lake Store를 기본 저장소로 사용</span><span class="sxs-lookup"><span data-stu-id="874fb-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="874fb-149">HDInsight 기본 저장소로 데이터 레이크 저장소에 배포 되 면 hello 클러스터 관련 파일 hello 수정할 수 있는 위치에에서 데이터 레이크 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="874fb-150">여기서 `<cluster_root_path>` hello 데이터 레이크 저장소에 만들 폴더 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="874fb-151">각 클러스터에 대 한 루트 경로 지정 하 여 사용할 수 있습니다 hello 둘 이상의 클러스터에 대 한 동일한 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="874fb-152">따라서 다음 위치에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="874fb-153">Cluster1은 hello 경로 사용할 수 있습니다.`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="874fb-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="874fb-154">클러스터 2 hello 경로 사용할 수 있습니다.`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="874fb-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="874fb-155">클러스터 사용을 hello 모두 공지 hello 동일 데이터 레이크 저장소 계정 **mydatalakestore**합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="874fb-156">각 클러스터에 액세스 tooits 데이터 레이크 저장소에 루트 파일 시스템을 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="874fb-157">Azure 포털 배포 환경을 hello 특히 묻는 toouse 폴더 이름을 같은 **/clusters/\<clustername >** hello 루트 경로 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="874fb-158">toobe 수 toouse 기본 저장소로 데이터 레이크 저장소 경로 따라 hello 서비스 보안 주체 액세스 toohello를 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="874fb-159">hello 데이터 레이크 저장소 계정 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="874fb-160">예: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="874fb-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="874fb-161">클러스터의 모든 폴더에 대 한 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="874fb-162">예: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="874fb-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="874fb-163">hello 클러스터에 대 한 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="874fb-164">예: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="874fb-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="874fb-165">서비스 주체 및 액세스 부여에 대한 자세한 내용은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="874fb-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="874fb-166">추가 저장소로 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="874fb-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="874fb-167">Hello 클러스터에 대 한 추가 저장소로 데이터 레이크 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="874fb-168">이러한 경우 기본 저장소를 클러스터 하는 hello 데이터 레이크 저장소 계정 또는 Azure 저장소 Blob 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="874fb-169">추가 저장소로 데이터 레이크 저장소에 저장 된 hello 데이터에 대 한 HDInsight 작업을 실행 하는 경우에 hello 정식 경로 toohello 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="874fb-170">예:</span><span class="sxs-lookup"><span data-stu-id="874fb-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="874fb-171">없는 **cluster_root_path** hello URL 이제에 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="874fb-172">데이터 레이크 저장소는 기본 저장소가 경우 아니므로 하기만 하면 toodo hello 경로 toohello 파일 제공 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="874fb-173">toobe 수 toouse 추가 저장소로 데이터 레이크 저장소 하기만 하면 toogrant hello 서비스 보안 주체 액세스 toohello 경로 파일이 저장 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="874fb-174">예:</span><span class="sxs-lookup"><span data-stu-id="874fb-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="874fb-175">서비스 주체 및 액세스 부여에 대한 자세한 내용은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="874fb-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="874fb-176">둘 이상의 Data Lake Store 계정 사용</span><span class="sxs-lookup"><span data-stu-id="874fb-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="874fb-177">데이터 레이크 저장소 계정을 추가 하는 추가으로 및 둘 이상의 데이터 레이크 저장소 추가 계정은 데이터 내용을 한 번 이상 Data Lake 저장소 계정에 대해 hello HDInsight 클러스터 권한을 제공 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="874fb-178">[Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="874fb-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="874fb-179">Data Lake Store 액세스 구성</span><span class="sxs-lookup"><span data-stu-id="874fb-179">Configure Data Lake store access</span></span>

<span data-ttu-id="874fb-180">tooconfigure HDInsight 클러스터에서 데이터 레이크 저장소 액세스는 Azure Active directory (Azure AD) 서비스 사용자는 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="874fb-181">Azure AD 관리자만 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="874fb-182">인증서로 hello 서비스 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="874fb-183">자세한 내용은 [Data Lake Store 액세스 구성](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) 및 [자체 서명된 인증서로 서비스 주체 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="874fb-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="874fb-184">HDInsight 클러스터에 대 한 추가 저장소로 toouse Azure 데이터 레이크 저장소 하려는 경우 이렇게 하는 동안이 문서에 설명 된 대로 hello 클러스터를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="874fb-185">추가 저장소 tooan로 Azure 데이터 레이크 저장소 추가 기존 HDInsight 클러스터는 복잡 한 프로세스 및 tooerrors 발생 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="874fb-186">Hello 클러스터에서 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="874fb-186">Access files from hello cluster</span></span>

<span data-ttu-id="874fb-187">여러 가지 방법으로 HDInsight 클러스터에서 데이터 레이크 저장소의 hello 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="874fb-188">**Hello 정규화 된 이름을 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="874fb-189">이 방법에서는 hello 전체 경로 toohello 파일을 제공 하 tooaccess 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="874fb-190">**Hello 축약된 경로 형식을 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="874fb-191">이 방법을 사용 하면 hello 경로 바꿉니다 toohello 클러스터 루트를 adl: / / /입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="874fb-192">따라서 위의 hello 예제에서 바꿀 수 있습니다 `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` 와 `adl:///`합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="874fb-193">**Hello 상대 경로 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-193">**Using hello relative path**.</span></span> <span data-ttu-id="874fb-194">이 방법을 사용 하면만 파일을 제공 hello 상대 경로 toohello tooaccess 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="874fb-195">예를 들어 hello toohello 파일 전체 경로 경우 나요?</span><span class="sxs-lookup"><span data-stu-id="874fb-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="874fb-196">에 액세스할 수 있습니다이 상대 경로 대신 사용 하 여 동일한 sample.log 파일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="874fb-197">HDInsight 클러스터를 만들려면 액세스할 tooData Lake 저장소</span><span class="sxs-lookup"><span data-stu-id="874fb-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="874fb-198">HDInsight 클러스터를 toocreate tooData Lake 저장소를 액세스 하는 방법에 자세한 지침에 대 한 링크를 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="874fb-199">포털 사용</span><span class="sxs-lookup"><span data-stu-id="874fb-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="874fb-200">PowerShell 사용(Data Lake Store를 기본 저장소로)</span><span class="sxs-lookup"><span data-stu-id="874fb-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="874fb-201">PowerShell 사용(Data Lake Store를 추가 저장소로)</span><span class="sxs-lookup"><span data-stu-id="874fb-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="874fb-202">Azure 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="874fb-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="874fb-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="874fb-203">Next steps</span></span>
<span data-ttu-id="874fb-204">이 문서에서는 방법에 대해 배웠습니다 toouse HDFS 호환 HDInsight와 Azure 데이터 레이크 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="874fb-205">이렇게 하면 구조화 되지 않은 데이터 및 데이터 취득 솔루션 및 구성 저장 hello 내부의 HDInsight toounlock hello 정보를 사용 하 여 보관 toobuild 확장 가능 하 고 장기, 있습니다.</span><span class="sxs-lookup"><span data-stu-id="874fb-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="874fb-206">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="874fb-206">For more information, see:</span></span>

* <span data-ttu-id="874fb-207">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="874fb-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="874fb-208">Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="874fb-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="874fb-209">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="874fb-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="874fb-210">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="874fb-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="874fb-211">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="874fb-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="874fb-212">[HDInsight와 Azure 저장소 공유 액세스 서명 toorestrict 액세스 toodata 사용][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="874fb-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
