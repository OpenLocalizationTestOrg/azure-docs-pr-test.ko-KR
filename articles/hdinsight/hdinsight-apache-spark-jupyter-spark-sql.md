---
title: "Azure HDInsight의 Apache Spark aaaCreate 클러스터가 | Microsoft Docs"
description: "HDInsight의 Apache Spark toocreate 클러스터 되는 방법에 HDInsight Spark 빠른 시작 합니다."
keywords: "spark 빠른 시작, 대화형 spark, 대화형 쿼리, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="967a0-104">Azure HDInsight에서 Apache Spark 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="967a0-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="967a0-105">이 문서에서는 Azure HDInsight의 Apache Spark toocreate 클러스터링 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="967a0-106">HDInsight의 Spark에 대한 자세한 내용은 [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="967a0-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="967a0-107">![Azure HDInsight의 Apache Spark 클러스터 단계 toocreate를 설명 하는 빠른 시작 다이어그램](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Apache Spark를 사용 하 여 HDInsight의 Spark 빠른 시작 합니다. 다음을 보여 주는 단계: 클러스터 만들기, Spark 대화형 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="967a0-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="967a0-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="967a0-108">Prerequisites</span></span>

* <span data-ttu-id="967a0-109">**Azure 구독** -</span><span class="sxs-lookup"><span data-stu-id="967a0-109">**An Azure subscription**.</span></span> <span data-ttu-id="967a0-110">이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="967a0-111">[지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="967a0-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="967a0-112">HDInsight Spark 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="967a0-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="967a0-113">이 섹션에서는 [Azure Resource Manager 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/)을 사용하여 HDInsight Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="967a0-114">클러스터를 만드는 다른 방법은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="967a0-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="967a0-115">Hello 이미지 tooopen hello 템플릿을 hello Azure 포털에서에서 다음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="967a0-116">Hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-116">Enter hello following values:</span></span>

    <span data-ttu-id="967a0-117">![Azure Resource Manager 템플릿을 사용하여 HDInsight Spark 클러스터 만들기](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Azure Resource Manager 템플릿을 사용하여 HDInsight에서 Spark 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="967a0-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="967a0-118">**구독**: 이 클러스터에 대해 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="967a0-119">**리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="967a0-120">리소스 그룹은 사용 되는 toomanage 프로젝트에 대 한 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="967a0-121">**위치**: hello 리소스 그룹에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="967a0-122">hello 템플릿은 기본 클러스터 저장소의 hello hello 클러스터를도 만드는 데이 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="967a0-123">**ClusterName**: toocreate 원하는 hello HDInsight 클러스터에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="967a0-124">**Spark 버전**: 선택 **2.0** hello 클러스터에서 tooinstall hello 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="967a0-125">**로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="967a0-126">**SSH 사용자 이름 및 암호**.</span><span class="sxs-lookup"><span data-stu-id="967a0-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="967a0-127">이러한 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-127">Write down these values.</span></span>  <span data-ttu-id="967a0-128">Hello 자습서의 뒷부분에 나오는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="967a0-129">선택 **toohello 약관 위에서 설명한 동의**선택, **Pin toodashboard**, 클릭 하 고 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="967a0-130">템플릿 배포에 배포 제출 중이라는 제목의 새 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="967a0-131">Toocreate hello 클러스터 약 20 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="967a0-132">HDInsight 클러스터를 만들어 문제를 실행 하면 하지 않았는지 hello 적절 한 사용 권한이 toodo 하므로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="967a0-133">자세한 내용은 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="967a0-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="967a0-134">이 문서를 사용 하는 Spark 클러스터 만듭니다 [hello Azure 저장소 Blob을 저장소 클러스터](hdinsight-hadoop-use-blob-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="967a0-135">사용 하는 Spark 클러스터를 만들 수도 있습니다 [Azure 데이터 레이크 저장소](hdinsight-hadoop-use-data-lake-store.md) hello 기본 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="967a0-136">자세한 내용은 [Data Lake 저장소가 있는 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="967a0-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="967a0-137">Spark SQL을 사용하여 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="967a0-138">사전 설정을 가져올 HDInsight Spark 클러스터에 대해 구성 된 Jupyter 노트북을 사용 하면 `sqlContext` Spark SQL을 사용 하 여 toorun 하이브 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="967a0-139">이 섹션에서는 설명 어떻게 toostart Jupyter 노트북 후 기본 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="967a0-140">열기 hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="967a0-141">Toopin hello 클러스터 toohello 대시보드를 선택한 경우 hello 대시보드 toolaunch hello 클러스터 블레이드에서 hello 클러스터 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="967a0-142">Hello 왼쪽된 창에서 hello 클러스터 toohello 대시보드에 고정 하지 않은 경우 클릭 **HDInsight 클러스터**, hello 클러스터를 만든 다음 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="967a0-143">**빠른 링크**에서 **클러스터 대시보드**를 클릭한 다음 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="967a0-144">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="967a0-145">![Jupyter 노트북 toorun 대화형 Spark SQL 쿼리 열기](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "열기 Jupyter 노트북 toorun 대화형 Spark SQL 쿼리")</span><span class="sxs-lookup"><span data-stu-id="967a0-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="967a0-146">브라우저에서 URL을 다음 열어 hello 통해 클러스터에 대 한 hello Jupyter 노트북에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="967a0-147">대체 **CLUSTERNAME** 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="967a0-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="967a0-148">Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-148">Create a notebook.</span></span> <span data-ttu-id="967a0-149">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="967a0-150">![Jupyter 노트북 toorun 대화형 Spark SQL 쿼리를 만들](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter 노트북 toorun 대화형 Spark SQL 쿼리를 만들려면")</span><span class="sxs-lookup"><span data-stu-id="967a0-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="967a0-151">새 전자 필기장 만들어지고 Untitled(Untitled.pynb) hello 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="967a0-152">Hello 위쪽에, hello 노트북 이름을 클릭 하 고 원하는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="967a0-153">![Hello Jupter 노트북 toorun 대화형 Spark에서 쿼리 이름을 제공](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "hello Jupter 노트북 toorun 대화형 Spark에서 쿼리 이름을 제공 합니다.")</span><span class="sxs-lookup"><span data-stu-id="967a0-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="967a0-154">붙여넣기 hello 다음 빈 셀을 코드로 바꾸고 다음 키를 누릅니다 **SHIFT + ENTER** toorun hello 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="967a0-155">아래의 hello 코드에서 `%%sql` Jupyter 노트북 toouse hello 미리 설정 (sql 매직 호출된 hello) 지시 `sqlContext` toorun hello 하이브 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="967a0-156">Hive 테이블에서 hello 상위 10 개의 행을 검색 하는 hello 쿼리 (**hivesampletable**) 모든 HDInsight 클러스터에서 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="967a0-157">![HDInsight Spark의 Hive 쿼리](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark의 Hive 쿼리")</span><span class="sxs-lookup"><span data-stu-id="967a0-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="967a0-158">Hello에 대 한 자세한 내용은 `%%sql` 매직 및 hello 컨텍스트 사전 설정을 참조 하십시오. [Jupyter 커널은 HDInsight 클러스터에 사용할 수 있는](hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="967a0-159">웹 브라우저 창 제목 표시 Jupyter에서 쿼리를 실행할 때마다는 **(Busy)** hello 노트북 제목 함께 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="967a0-160">이 찬 원 모양 다음 toohello 표시 **PySpark** hello 오른쪽 위 모퉁이의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="967a0-161">Hello 작업이 완료 되 면 tooa 흰색 원을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="967a0-162">hello 화면 tooshow hello 쿼리 결과 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="967a0-163">![HDInsight Spark의 Hive 쿼리 출력](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark의 Hive 쿼리 출력")</span><span class="sxs-lookup"><span data-stu-id="967a0-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="967a0-164">Hello 응용 프로그램 실행을 완료 한 후 hello 노트북 toorelease hello 클러스터 리소스를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="967a0-165">toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="967a0-166">나중에 toocomplete hello 다음 단계를 계획 하는 경우이 문서에서 만든 hello HDInsight 클러스터를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="967a0-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="967a0-167">Next step</span></span> 

<span data-ttu-id="967a0-168">이 문서 toocreate HDInsight Spark 클러스터 방법을 배웠습니다 및 실행 기본 Spark SQL에서 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="967a0-169">예제 데이터에서 어떻게 toouse HDInsight Spark 클러스터 toohello 다음 문서 toolearn toorun 대화형 쿼리를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="967a0-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="967a0-170">HDInsight Spark 클러스터에서 대화형 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="967a0-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



