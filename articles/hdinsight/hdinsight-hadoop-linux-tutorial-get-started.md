---
title: "Hadoop 및 Azure HDInsight의 Hive aaaGet 시작 | Microsoft Docs"
description: "Toocreate HDInsight 클러스터 및 하이브를 사용 하 여 쿼리 데이터에 알아봅니다."
keywords: "Hadoop 시작, Hadoop Linux, Hadoop 빠른 시작, Hive 시작, Hive 빠른 시작"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a><span data-ttu-id="7156b-104">Hadoop 자습서: HDInsight에서 Hadoop 사용 시작</span><span class="sxs-lookup"><span data-stu-id="7156b-104">Hadoop tutorial: Get started using Hadoop in HDInsight</span></span>

<span data-ttu-id="7156b-105">자세한 방법을 toocreate [Hadoop](http://hadoop.apache.org/) HDInsight, 및 HDInsight의 Hive toorun 작업 하는 방법에 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-105">Learn how toocreate [Hadoop](http://hadoop.apache.org/) clusters in HDInsight, and how toorun Hive jobs in HDInsight.</span></span> <span data-ttu-id="7156b-106">[Apache Hive](https://hive.apache.org/) hello Hadoop 생태계에서 hello 가장 인기 있는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-106">[Apache Hive](https://hive.apache.org/) is hello most popular component in hello Hadoop ecosystem.</span></span> <span data-ttu-id="7156b-107">현재 HDInsight는 [일곱 가지 클러스터 형식](hdinsight-hadoop-introduction.md#overview)으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-107">Currently HDInsight comes with [seven different cluster types](hdinsight-hadoop-introduction.md#overview).</span></span> <span data-ttu-id="7156b-108">각 클러스터 유형은 서로 다른 구성 요소 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-108">Each cluster type supports a different set of components.</span></span> <span data-ttu-id="7156b-109">모든 클러스터 형식은 Hive를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-109">All cluster types support Hive.</span></span> <span data-ttu-id="7156b-110">목록이 HDInsight에서 지원 되는 구성에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="7156b-110">For a list of supported components in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</span></span>  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="7156b-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7156b-111">Prerequisites</span></span>
<span data-ttu-id="7156b-112">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-112">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="7156b-113">**Azure 구독**: toocreate 무료 1 개월 평가판 계정을 너무 찾아보기[azure.microsoft.com/free](https://azure.microsoft.com/free)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-113">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>

## <a name="create-cluster"></a><span data-ttu-id="7156b-114">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="7156b-114">Create cluster</span></span>

<span data-ttu-id="7156b-115">Hadoop 작업의 대부분은 배치 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-115">Most of Hadoop jobs are batch jobs.</span></span> <span data-ttu-id="7156b-116">클러스터, 만들고 몇 가지 작업을 실행, 다음 hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-116">You create a cluster, run some jobs, and then delete hello cluster.</span></span> <span data-ttu-id="7156b-117">이 섹션에서는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-template-deploy.md)을 사용하여 HDInsight에서 Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-117">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="7156b-118">이 자습서를 따라 하는 데 Resource Manager 템플릿 환경이 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-118">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="7156b-119">다른 클러스터 생성 방법 및이 자습서에 사용 되는 hello 속성을 이해, 참조 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-119">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="7156b-120">클러스터 만들기 옵션 hello 페이지 toochoose hello 위에 hello 선택기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-120">Use hello selector on hello top of hello page toochoose your cluster creation options.</span></span>

<span data-ttu-id="7156b-121">이 자습서에 사용 된 hello 리소스 관리자 템플릿을에 위치한 [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-121">hello Resource Manager template used in this tutorial is located in [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> 

1. <span data-ttu-id="7156b-122">Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-122">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="7156b-123">입력 하거나 다음 값에는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-123">Enter or select hello following values:</span></span>
   
    <span data-ttu-id="7156b-124">![HDInsight Linux get 포털에서 리소스 관리자 템플릿을 시작](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Azure 포털 및 리소스 그룹 관리자 템플릿을 사용 하 여 HDInsigut 배포 Hadoop 클러스터 hello")합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-124">![HDInsight Linux get started Resource Manager template on portal](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Deploy Hadoop cluster in HDInsigut using hello Azure portal and a resource group manager template").</span></span>
   
    * <span data-ttu-id="7156b-125">**구독**: Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-125">**Subscription**: Select your Azure subscription.</span></span>
    * <span data-ttu-id="7156b-126">**리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-126">**Resource group**: Create a resource group or select an existing resource group.</span></span>  <span data-ttu-id="7156b-127">리소스 그룹은 Azure 구성 요소의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-127">A resource group is a container of Azure components.</span></span>  <span data-ttu-id="7156b-128">이 경우 hello 리소스 그룹에는 hello HDInsight 클러스터와 hello 종속 Azure 저장소 계정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-128">In this case, hello resource group contains hello HDInsight cluster and hello dependent Azure Storage account.</span></span> 
    * <span data-ttu-id="7156b-129">**위치**: 저장할 toocreate 클러스터 Azure 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-129">**Location**: Select an Azure location where you want toocreate your cluster.</span></span>  <span data-ttu-id="7156b-130">성능 향상을 위해 위치 가까이 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-130">Choose a location closer tooyou for better performance.</span></span> 
    * <span data-ttu-id="7156b-131">**클러스터 유형**: 이 자습서에서는 **hadoop**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-131">**Cluster Type**: Select **hadoop** for this tutorial.</span></span>
    * <span data-ttu-id="7156b-132">**클러스터 이름**: hello Hadoop 클러스터에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-132">**Cluster Name**: Enter a name for hello Hadoop cluster.</span></span>
    * <span data-ttu-id="7156b-133">**로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 **admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-133">**Cluster login name and password**: hello default login name is **admin**.</span></span>
    * <span data-ttu-id="7156b-134">**SSH 사용자 이름 및 암호**: hello 기본 사용자 이름은 **sshuser**합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-134">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="7156b-135">이름은 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-135">You can rename it.</span></span> 
     
    <span data-ttu-id="7156b-136">일부 속성 hello 템플릿에 하드 코드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-136">Some properties have been hardcoded in hello template.</span></span>  <span data-ttu-id="7156b-137">Hello 서식 파일에서 이러한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-137">You can configure these values from hello template.</span></span>

    * <span data-ttu-id="7156b-138">**위치**: hello hello 클러스터의 위치 및 hello 종속 저장소 계정을 공유 hello 같은 hello 리소스 그룹 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-138">**Location**: hello location of hello cluster and hello dependent storage account share hello same location as hello resource group.</span></span>
    * <span data-ttu-id="7156b-139">**클러스터 버전**: 3.5</span><span class="sxs-lookup"><span data-stu-id="7156b-139">**Cluster version**: 3.5</span></span>
    * <span data-ttu-id="7156b-140">**OS 유형**: Linux</span><span class="sxs-lookup"><span data-stu-id="7156b-140">**OS Type**: Linux</span></span>
    * <span data-ttu-id="7156b-141">**작업자 노드 수**: 2</span><span class="sxs-lookup"><span data-stu-id="7156b-141">**Number of worker nodes**: 2</span></span>

     <span data-ttu-id="7156b-142">각 클러스터에는 [Azure Storage 계정](hdinsight-hadoop-use-blob-storage.md) 또는 [Azure Data Lake 계정](hdinsight-hadoop-use-data-lake-store.md) 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-142">Each cluster has an [Azure Storage account](hdinsight-hadoop-use-blob-storage.md) or an [Azure Data Lake account](hdinsight-hadoop-use-data-lake-store.md) dependency.</span></span> <span data-ttu-id="7156b-143">Hello 기본 저장소 계정으로 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-143">It is referred as hello default storage account.</span></span> <span data-ttu-id="7156b-144">HDInsight 클러스터와 해당 기본 저장소 계정 함께 위치 해야 hello에 동일한 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-144">HDInsight cluster and its default storage account must be co-located in hello same Azure region.</span></span> <span data-ttu-id="7156b-145">클러스터를 삭제 하는 hello 저장소 계정을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-145">Deleting clusters does not delete hello storage account.</span></span> 
     
     <span data-ttu-id="7156b-146">이러한 속성에 대한 자세한 설명은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7156b-146">For more explanation of these properties, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="7156b-147">선택 **toohello 약관 위에서 설명한 동의** 및 **Pin toodashboard**, 클릭 하 고 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-147">Select **I agree toohello terms and conditions stated above** and **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="7156b-148">라는 새 타일이 표시 **배포 템플릿 배포** hello 포털 대시보드에서.</span><span class="sxs-lookup"><span data-stu-id="7156b-148">You shall see a new tile titled **Deploying Template deployment** on hello portal dashboard.</span></span> <span data-ttu-id="7156b-149">클러스터에 대 한 약 20 분 toocreate 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-149">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="7156b-150">Hello 클러스터를 만든 후 hello 타일의 hello 캡션은는 지정한 변경 된 toohello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-150">Once hello cluster is created, hello caption of hello tile is changed toohello resource group name you specified.</span></span> <span data-ttu-id="7156b-151">고 hello 포털에는 새 블레이드가 hello 리소스 그룹을 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-151">And hello portal automatically opens hello resource group in a new blade.</span></span> <span data-ttu-id="7156b-152">Hello 클러스터와 나열 된 hello 기본 저장소를 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-152">You can see both hello cluster and hello default storage listed.</span></span>
   
    <span data-ttu-id="7156b-153">![HDInsight Linux 시작 - 리소스 그룹](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight 클러스터 리소스 그룹")</span><span class="sxs-lookup"><span data-stu-id="7156b-153">![HDInsight Linux get started resource group](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight cluster resource group").</span></span>

4. <span data-ttu-id="7156b-154">에 새 블레이드가 hello 클러스터 이름 tooopen hello 클러스터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-154">Click hello cluster name tooopen hello cluster in a new blade.</span></span>

   <span data-ttu-id="7156b-155">![HDInsight Linux 시작 - 클러스터 설정](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "HDInsight 클러스터 속성")</span><span class="sxs-lookup"><span data-stu-id="7156b-155">![HDInsight Linux get started cluster settings](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "HDInsight cluster properties")</span></span>


## <a name="run-hive-queries"></a><span data-ttu-id="7156b-156">Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7156b-156">Run Hive queries</span></span>
<span data-ttu-id="7156b-157">[Apache Hive](hdinsight-use-hive.md) HDInsight에서 사용 되는 hello 가장 인기 있는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-157">[Apache Hive](hdinsight-use-hive.md) is hello most popular component used in HDInsight.</span></span> <span data-ttu-id="7156b-158">여러 가지 방법으로 하이브 작업 toorun HDInsight의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-158">There are many ways toorun Hive jobs in HDInsight.</span></span> <span data-ttu-id="7156b-159">이 자습서에서는 hello hello 포털에서 Ambari 하이브 보기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-159">In this tutorial, you use hello Ambari Hive view from hello portal.</span></span> <span data-ttu-id="7156b-160">Hive 작업을 제출하는 다른 방법은 [HDInsight에서 Hive 사용](hdinsight-use-hive.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7156b-160">For other methods for submitting Hive jobs, see [Use Hive in HDInsight](hdinsight-use-hive.md).</span></span>

1. <span data-ttu-id="7156b-161">Hello 이전 스크린 샷에서 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-161">From hello previous screenshot, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span>  <span data-ttu-id="7156b-162">너무 찾아볼 수도 있습니다 **https://&lt;ClusterName >. azurehdinsight.net**여기서 &lt;ClusterName >는 hello 이전 섹션 tooopen Ambari에서에서 만든 hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-162">You can also browse too **https://&lt;ClusterName>.azurehdinsight.net**, where &lt;ClusterName> is hello cluster you created in hello previous section tooopen Ambari.</span></span>
2. <span data-ttu-id="7156b-163">Hello Hadoop 사용자 이름 및 hello 이전 섹션에서 지정한 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-163">Enter hello Hadoop username and password that you specified in hello previous section.</span></span> <span data-ttu-id="7156b-164">hello 기본 사용자 이름은 **admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-164">hello default username is **admin**.</span></span>
3. <span data-ttu-id="7156b-165">열기 **하이브 보기** hello 스크린 샷 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="7156b-165">Open **Hive View** as shown in hello following screenshot:</span></span>
   
    <span data-ttu-id="7156b-166">![Ambari 보기 선택](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive 뷰어 메뉴")</span><span class="sxs-lookup"><span data-stu-id="7156b-166">![Selecting Ambari views](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive Viwer menu").</span></span>
4. <span data-ttu-id="7156b-167">Hello에 **쿼리 편집기** hello 페이지, 붙여넣기 hello hello 워크시트로 HiveQL 문 뒤의 섹션:</span><span class="sxs-lookup"><span data-stu-id="7156b-167">In hello **Query Editor** section of hello page, paste hello following HiveQL statements into hello worksheet:</span></span>
   
        SHOW TABLES;
   
   > [!NOTE]
   > <span data-ttu-id="7156b-168">Hive에서 세미콜론이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-168">Semi-colon is required by Hive.</span></span>       
   > 
   > 
5. <span data-ttu-id="7156b-169">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-169">Click **Execute**.</span></span> <span data-ttu-id="7156b-170">A **쿼리 프로세스 결과** 섹션 아래 hello 쿼리 편집기에 표시 하 고 hello 작업에 대 한 정보를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-170">A **Query Process Results** section should appear beneath hello Query Editor and display information about hello job.</span></span> 
   
    <span data-ttu-id="7156b-171">Hello 쿼리 완료 되 면 hello **쿼리 프로세스 결과** hello 연산의 hello 결과 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-171">Once hello query has finished, hello **Query Process Results** section displays hello results of hello operation.</span></span> <span data-ttu-id="7156b-172">**hivesampletable**이라는 테이블이 한 개 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-172">You shall see one table called **hivesampletable**.</span></span> <span data-ttu-id="7156b-173">이 예제 하이브 테이블 모든 hello HDInsight 클러스터와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-173">This sample Hive table comes with all hello HDInsight clusters.</span></span>
   
    <span data-ttu-id="7156b-174">![HDInsight Hive 보기](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive 보기 - 쿼리 편집기")</span><span class="sxs-lookup"><span data-stu-id="7156b-174">![HDInsight Hive views](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive View Query Editor").</span></span>
6. <span data-ttu-id="7156b-175">4 단계와 5 단계 toorun hello 다음 쿼리를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-175">Repeat step 4 and step 5 toorun hello following query:</span></span>
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > <span data-ttu-id="7156b-176">참고 hello **결과 저장** hello의 왼쪽 위 hello에 드롭다운에서 **쿼리 프로세스 결과** 섹션;이 tooeither 다운로드 hello 결과 사용 하거나 CSV 파일로 tooHDInsight 저장소를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-176">Note hello **Save results** dropdown in hello upper left of hello **Query Process Results** section; you can use this tooeither download hello results, or save them tooHDInsight storage as a CSV file.</span></span>
   > 
   > 
7. <span data-ttu-id="7156b-177">클릭 **기록** tooget hello 작업의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-177">Click **History** tooget a list of hello jobs.</span></span>

<span data-ttu-id="7156b-178">하이브 작업을 완료 한 후 다음을 할 수 있습니다 [hello 결과 tooAzure SQL 데이터베이스 또는 SQL Server 데이터베이스 내보내기](hdinsight-use-sqoop-mac-linux.md), 수도 있습니다 [Excel을 사용 하 여 hello 결과 시각화](hdinsight-connect-excel-power-query.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-178">After you have completed a Hive job, you can [export hello results tooAzure SQL database or SQL Server database](hdinsight-use-sqoop-mac-linux.md), you can also [visualize hello results using Excel](hdinsight-connect-excel-power-query.md).</span></span> <span data-ttu-id="7156b-179">HDInsight의 Hive 사용에 대 한 자세한 내용은 참조 [사용 하 여 Hive 및 HDInsight tooanalyze 샘플 Apache log4j 파일에서에서 Hadoop으로 HiveQL](hdinsight-use-hive.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-179">For more information about using Hive in HDInsight, see [Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file](hdinsight-use-hive.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="7156b-180">Hello 자습서 정리</span><span class="sxs-lookup"><span data-stu-id="7156b-180">Clean up hello tutorial</span></span>
<span data-ttu-id="7156b-181">Hello 자습서를 완료 한 후 toodelete hello 클러스터를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-181">After you complete hello tutorial, you may want toodelete hello cluster.</span></span> <span data-ttu-id="7156b-182">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-182">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="7156b-183">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-183">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="7156b-184">Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-184">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> 

> [!NOTE]
> <span data-ttu-id="7156b-185">사용 하 여 [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), 주문형 HDInsight 클러스터를 만들어 구성 하는 TimeToLive 설정이 너무 hello 클러스터 자동으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-185">Using [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), you can create HDInsight clusters on demand, and configure a TimeToLive setting too delete hello clusters automatically.</span></span> 
> 
> 

<span data-ttu-id="7156b-186">**toodelete hello 클러스터 및/또는 hello 기본 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="7156b-186">**toodelete hello cluster and/or hello default storage account**</span></span>

1. <span data-ttu-id="7156b-187">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-187">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7156b-188">Hello 포털 대시보드에서 hello 클러스터를 만들 때 사용한 hello 리소스 그룹 이름으로 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-188">From hello portal dashboard, click hello tile with hello resource group name you used when you created hello cluster.</span></span>
3. <span data-ttu-id="7156b-189">클릭 **삭제** 리소스 블레이드 toodelete hello 리소스 그룹을 hello 클러스터 및 hello 기본 저장소 계정; 포함 하는 hello 또는 hello에 hello 클러스터 이름을 클릭 **리소스** 타일을 클릭 **삭제** hello 클러스터 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-189">Click **Delete** on hello resource blade toodelete hello resource group, which contains hello cluster and hello default storage account; or click hello cluster name on hello **Resources** tile and then click **Delete** on hello cluster blade.</span></span> <span data-ttu-id="7156b-190">Hello 저장소 계정을 삭제 하는 참고 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-190">Note deleting hello resource group deletes hello storage account.</span></span> <span data-ttu-id="7156b-191">Tookeep hello 저장소 계정 toodelete hello 클러스터만을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-191">If you want tookeep hello storage account, choose toodelete hello cluster only.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="7156b-192">문제 해결</span><span class="sxs-lookup"><span data-stu-id="7156b-192">Troubleshoot</span></span>

<span data-ttu-id="7156b-193">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7156b-193">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7156b-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7156b-194">Next steps</span></span>
<span data-ttu-id="7156b-195">이 자습서에서는 배웠습니다 toocreate Linux 기반 HDInsight 클러스터 리소스 관리자 템플릿을 사용 하는 방식과 tooperform 기본 하이브 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-195">In this tutorial, you have learned how toocreate a Linux-based HDInsight cluster using a Resource Manager template, and how tooperform basic Hive queries.</span></span>

<span data-ttu-id="7156b-196">HDInsight 사용 하 여 데이터 분석에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7156b-196">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="7156b-197">Visual Studio에서 tooperform 하이브 쿼리 하는 방법을 포함 하 여 HDInsight Hive 사용에 대 한 더 toolearn 참조 [HDInsight를 사용 하 여 하이브][hdinsight-use-hive]합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-197">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="7156b-198">Pig에 대 한 toolearn, 언어를 사용 하는 tootransform 데이터, 참조 [HDInsight와 Pig][hdinsight-use-pig]합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-198">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="7156b-199">toolearn MapReduce, Hadoop에서 데이터를 처리 하는 방식으로 toowrite 프로그램에 대 한 참조 [HDInsight 사용 하 여 MapReduce][hdinsight-use-mapreduce]합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-199">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="7156b-200">Visual Studio tooanalyze 데이터 HDInsight에 대 한 hello HDInsight 도구를 사용 하는 방법에 대 한 toolearn 참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-200">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="7156b-201">HDInsight 데이터를 저장 하는 방법 또는 tooget 데이터 HDInsight hello 다음을 참조 하는 방법에 대해 더 알아봅니다 tooknow 필요와 준비 toostart 사용자 고유의 데이터로 작업 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7156b-201">If you're ready toostart working with your own data and need tooknow more about how HDInsight stores data or how tooget data into HDInsight, see hello following:</span></span>

* <span data-ttu-id="7156b-202">HDInsight에서 Azure Storage를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 Azure Storage 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7156b-202">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="7156b-203">방법에 대 한 내용은 tooupload 데이터 tooHDInsight 참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-203">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="7156b-204">만들거나 HDInsight 클러스터를 관리 하는 방법에 대 한 자세한 toolearn를 원하는 경우 hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-204">If you'd like toolearn more about creating or managing an HDInsight cluster, see hello following:</span></span>

* <span data-ttu-id="7156b-205">Linux 기반 HDInsight 클러스터를 관리 하는 방법에 대 한 toolearn 참조 [Ambari를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-205">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="7156b-206">HDInsight 클러스터를 만들 때 선택할 수는 hello 옵션에 대해 자세히 toolearn 참조 [사용자 지정 옵션을 사용 하 여 Linux에서 HDInsight를 만드는](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-206">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="7156b-207">Linux, Hadoop와 잘 알고 있는 해도 hello HDInsight에서 Hadoop에 대 한 tooknow 고유 정보를 사용할 경우 참조 [Linux에서 HDInsight 작업](hdinsight-hadoop-linux-information.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-207">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="7156b-208">이 문서에서 제공하는 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7156b-208">This article provides information such as:</span></span>
  
  * <span data-ttu-id="7156b-209">Ambari 등 WebHCat hello 클러스터에서 호스팅되는 서비스에 대 한 Url</span><span class="sxs-lookup"><span data-stu-id="7156b-209">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="7156b-210">Hadoop 파일 및 hello 로컬 파일 시스템에 예제의 hello 위치</span><span class="sxs-lookup"><span data-stu-id="7156b-210">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="7156b-211">hello 기본 데이터 저장소로의 Azure 저장소 (WASB) HDFS 대신 hello 사용</span><span class="sxs-lookup"><span data-stu-id="7156b-211">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


