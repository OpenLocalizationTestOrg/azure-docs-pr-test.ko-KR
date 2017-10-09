---
title: "Azure HDInsight의 보안 전송 저장소 계정을 가진 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "안전 하 게 전송 된 toocreate HDInsight 클러스터를 Azure 저장소 계정을 사용 하는 방법을 알아봅니다."
keywords: "hadoop 시작,hadoop linux,hadoop 빠른 시작,보안 전송,azure 저장소 계정"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="d9aae-104">Azure HDInsight에서 보안 전송 저장소 계정으로 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="d9aae-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="d9aae-105">hello [보안 전송 필요](../storage/common/storage-require-secure-transfer.md) 기능은 보안 연결을 통해 모든 요청 tooyour 계정을 적용 하 여 Azure 저장소 계정의 hello 보안을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="d9aae-106">이 기능 및 hello wasbs 체계 HDInsight 클러스터 버전이 3.6 이상 버전 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d9aae-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d9aae-107">Prerequisites</span></span>
<span data-ttu-id="d9aae-108">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="d9aae-109">**Azure 구독**: toocreate 무료 1 개월 평가판 계정을 너무 찾아보기[azure.microsoft.com/free](https://azure.microsoft.com/free)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="d9aae-110">**보안 전송이 활성화된 Azure Storage 계정**.</span><span class="sxs-lookup"><span data-stu-id="d9aae-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="d9aae-111">Hello 지침은 [저장소 계정을 만드는](../storage/common/storage-create-storage-account.md#create-a-storage-account) 및 [보안 전송 필요](../storage/common/storage-require-secure-transfer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="d9aae-112">**Hello 저장소 계정에서 Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="d9aae-113">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="d9aae-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="d9aae-114">이 섹션에서는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-template-deploy.md)을 사용하여 HDInsight에서 Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="d9aae-115">hello 서식 파일에 있는 [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="d9aae-116">이 자습서를 따라 하는 데 Resource Manager 템플릿 환경이 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="d9aae-117">다른 클러스터 생성 방법 및이 자습서에 사용 되는 hello 속성을 이해, 참조 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="d9aae-118">Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="d9aae-119">사양을 따르는 hello로 hello 지침 toocreate hello 클러스터를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="d9aae-120">HDInsight 버전 3.6을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="d9aae-121">hello 기본 버전은 3.5입니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-121">hello default version is 3.5.</span></span> <span data-ttu-id="d9aae-122">3.6 이상 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="d9aae-123">보안 전송이 활성화된 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="d9aae-124">Hello 저장소 계정에 대 한 짧은 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="d9aae-125">Hello 저장소 계정과 blob 컨테이너 hello 모두 미리 생성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="d9aae-126">Hello 지침은 [클러스터 만들기](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="d9aae-127">스크립트 동작 tooprovide 사용자 고유의 구성 파일을 사용 하는 경우 hello 설정을 다음에 wasbs를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="d9aae-128">fs.defaultFS(코어 사이트)</span><span class="sxs-lookup"><span data-stu-id="d9aae-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="d9aae-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="d9aae-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="d9aae-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="d9aae-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="d9aae-131">추가 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="d9aae-131">Add additional storage accounts</span></span>

<span data-ttu-id="d9aae-132">몇 가지 옵션 tooadd 사용 하도록 설정 하는 추가 보안 전송 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="d9aae-133">Hello 마지막 섹션에서 hello Azure 리소스 관리자 템플릿을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="d9aae-134">Hello를 사용 하 여 클러스터 만들기 [Azure 포털](https://portal.azure.com) 연결 된 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="d9aae-135">사용 하 여 스크립트 작업 tooadd 추가 보안 전송 저장소 계정을 tooan 기존 HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="d9aae-136">자세한 내용은 참조 [추가 저장소 계정을 tooHDInsight 추가](hdinsight-hadoop-add-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9aae-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9aae-137">Next steps</span></span>
<span data-ttu-id="d9aae-138">이 자습서에서는 toocreate는 HDInsight 클러스터를 사용 하도록 설정한 보안 전송 toohello 저장소 계정에 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="d9aae-139">HDInsight 사용 하 여 데이터 분석에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d9aae-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="d9aae-140">Visual Studio에서 tooperform 하이브 쿼리 하는 방법을 포함 하 여 HDInsight Hive 사용에 대 한 더 toolearn 참조 [HDInsight를 사용 하 여 하이브][hdinsight-use-hive]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="d9aae-141">Pig에 대 한 toolearn, 언어를 사용 하는 tootransform 데이터, 참조 [HDInsight와 Pig][hdinsight-use-pig]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="d9aae-142">toolearn MapReduce, Hadoop에서 데이터를 처리 하는 방식으로 toowrite 프로그램에 대 한 참조 [HDInsight 사용 하 여 MapReduce][hdinsight-use-mapreduce]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="d9aae-143">Visual Studio tooanalyze 데이터 HDInsight에 대 한 hello HDInsight 도구를 사용 하는 방법에 대 한 toolearn 참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="d9aae-144">HDInsight에서 데이터를 저장 하는 방법에 대 한 자세한 toolearn tooget 데이터 HDInsight hello 다음 문서를 참조 하는 방법 또는:</span><span class="sxs-lookup"><span data-stu-id="d9aae-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="d9aae-145">HDInsight에서 Azure Storage를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 Azure Storage 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9aae-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="d9aae-146">방법에 대 한 내용은 tooupload 데이터 tooHDInsight 참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="d9aae-147">toolearn 만들거나는 HDInsight 클러스터 관리에 대 한 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="d9aae-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="d9aae-148">Linux 기반 HDInsight 클러스터를 관리 하는 방법에 대 한 toolearn 참조 [Ambari를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="d9aae-149">HDInsight 클러스터를 만들 때 선택할 수는 hello 옵션에 대해 자세히 toolearn 참조 [사용자 지정 옵션을 사용 하 여 Linux에서 HDInsight를 만드는](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="d9aae-150">Linux, Hadoop와 잘 알고 있는 해도 hello HDInsight에서 Hadoop에 대 한 tooknow 고유 정보를 사용할 경우 참조 [Linux에서 HDInsight 작업](hdinsight-hadoop-linux-information.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="d9aae-151">이 문서에서 제공하는 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9aae-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="d9aae-152">Ambari 등 WebHCat hello 클러스터에서 호스팅되는 서비스에 대 한 Url</span><span class="sxs-lookup"><span data-stu-id="d9aae-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="d9aae-153">Hadoop 파일 및 hello 로컬 파일 시스템에 예제의 hello 위치</span><span class="sxs-lookup"><span data-stu-id="d9aae-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="d9aae-154">hello 기본 데이터 저장소로의 Azure 저장소 (WASB) HDFS 대신 hello 사용</span><span class="sxs-lookup"><span data-stu-id="d9aae-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


