---
title: "Azure HDInsight에서 Apache Spark 클러스터 만들기 | Microsoft Docs"
description: "HDInsight에서 Apache Spark 클러스터를 만드는 방법에 대한 HDInsight Spark 빠른 시작입니다."
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
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="92697-104">Azure HDInsight에서 Apache Spark 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="92697-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="92697-105">이 문서에서는 Azure HDInsight에서 Apache Spark 클러스터를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="92697-106">HDInsight의 Spark에 대한 자세한 내용은 [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92697-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="92697-107">![Azure HDInsight에서 Apache Spark 클러스터를 만드는 단계를 설명하는 빠른 시작 다이어그램](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "HDInsight에서 Apache Spark를 사용하여 Spark 빠른 시작. 다음을 보여 주는 단계: 클러스터 만들기, Spark 대화형 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="92697-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92697-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="92697-108">Prerequisites</span></span>

* <span data-ttu-id="92697-109">**Azure 구독** -</span><span class="sxs-lookup"><span data-stu-id="92697-109">**An Azure subscription**.</span></span> <span data-ttu-id="92697-110">이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="92697-111">[지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92697-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="92697-112">HDInsight Spark 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="92697-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="92697-113">이 섹션에서는 [Azure Resource Manager 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/)을 사용하여 HDInsight Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92697-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="92697-114">클러스터를 만드는 다른 방법은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92697-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="92697-115">Azure 포털에서 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="92697-116">다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-116">Enter the following values:</span></span>

    <span data-ttu-id="92697-117">![Azure Resource Manager 템플릿을 사용하여 HDInsight Spark 클러스터 만들기](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Azure Resource Manager 템플릿을 사용하여 HDInsight에서 Spark 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="92697-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="92697-118">**구독**: 이 클러스터에 대해 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="92697-119">**리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="92697-120">리소스 그룹은 프로젝트에 대한 Azure 리소스를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="92697-121">**위치**: 리소스 그룹의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="92697-122">템플릿에서는 기본 클러스터 저장소뿐만 아니라 클러스터를 만드는 데 이 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="92697-123">**ClusterName**: 만들려는 HDInsight 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="92697-124">**Spark 버전**: 클러스터에 설치할 버전을 **2.0**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="92697-125">**클러스터 로그인 이름 및 암호**: 기본 로그인 이름은 admin입니다.</span><span class="sxs-lookup"><span data-stu-id="92697-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="92697-126">**SSH 사용자 이름 및 암호**.</span><span class="sxs-lookup"><span data-stu-id="92697-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="92697-127">이러한 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="92697-127">Write down these values.</span></span>  <span data-ttu-id="92697-128">이 정보는 자습서의 뒷부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="92697-129">**위에 명시된 사용 약관에 동의함**을 선택하고 **대시보드에 고정**을 선택한 다음 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="92697-130">템플릿 배포에 배포 제출 중이라는 제목의 새 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="92697-131">클러스터를 만드는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="92697-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="92697-132">HDInsight 클러스터를 만드는 데 문제가 발생하는 경우 이를 수행하기 위한 적절한 사용 권한이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="92697-133">자세한 내용은 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92697-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="92697-134">이 문서에서는 [클러스터 저장소로 Azure 저장소 Blob](hdinsight-hadoop-use-blob-storage.md)을 사용하는 Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92697-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="92697-135">기본 저장소로 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)를 사용하는 Spark 클러스터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="92697-136">자세한 내용은 [Data Lake 저장소가 있는 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92697-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="92697-137">Spark SQL을 사용하여 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="92697-138">HDInsight Spark 클러스터에 구성된 Jupyter Notebook을 사용하는 경우 Spark SQL을 사용하여 Hive 쿼리를 실행하는 데 사용할 수 있는 `sqlContext`를 미리 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="92697-139">이 섹션에서는 Jupyter Notebook을 시작한 다음 기본 Hive 쿼리를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="92697-140">[Azure 포털](https://portal.azure.com/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="92697-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="92697-141">클러스터를 대시보드에 고정하도록 선택한 경우 대시보드에서 클러스터 타일을 클릭하여 클러스터 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="92697-142">클러스터를 대시보드에 고정하지 않은 경우 왼쪽 창에서 **HDInsight 클러스터**를 클릭한 후 만든 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="92697-143">**빠른 링크**에서 **클러스터 대시보드**를 클릭한 다음 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="92697-144">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="92697-145">![Jupyter 노트북을 열어 대화형 Spark SQL 쿼리 실행](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Jupyter 노트북을 열어 대화형 Spark SQL 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="92697-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="92697-146">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter 노트북에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="92697-147">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="92697-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="92697-148">Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92697-148">Create a notebook.</span></span> <span data-ttu-id="92697-149">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="92697-150">![Jupyter 노트북을 만들어 대화형 Spark SQL 쿼리 실행](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter 노트북을 만들어 대화형 Spark SQL 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="92697-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="92697-151">새 노트북이 만들어지고 Untitled(Untitled.pynb) 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="92697-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="92697-152">맨 위에서 노트북 이름을 클릭하고 원하는 경우 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="92697-153">![Jupter 노트북에 대한 이름을 제공하여 대화형 Spark 쿼리 실행](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Jupter 노트북에 대한 이름을 제공하여 대화형 Spark 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="92697-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="92697-154">빈 셀에 다음 코드를 붙여 넣은 다음 **SHIFT + ENTER**를 눌러 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="92697-155">아래 코드에서 `%%sql`(SQL 매직이라고 함)은 Jupyter Notebook에서 `sqlContext` Hive 쿼리를 실행하는 사전 설정을 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="92697-156">Hive 테이블(**hivesampletable**)에서 상위 10개의 행을 검색하는 쿼리는 모든 HDInsight 클러스터에서 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="92697-157">![HDInsight Spark의 Hive 쿼리](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark의 Hive 쿼리")</span><span class="sxs-lookup"><span data-stu-id="92697-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="92697-158">`%%sql` 매직 및 미리 설정 컨텍스트에 대한 자세한 내용은 [HDInsight 클러스터에 사용할 수 있는 Jupyter 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92697-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="92697-159">Jupyter에서 쿼리를 실행할 때마다, 웹 브라우저 창 제목에 Notebook 제목과 함께 **(사용 중)** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="92697-160">또한 오른쪽 위 모서리에 있는 **PySpark** 텍스트 옆에 단색 원이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="92697-161">작업이 완료되면 속이 빈 원으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="92697-162">쿼리 출력을 표시하려면 화면을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="92697-163">![HDInsight Spark의 Hive 쿼리 출력](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark의 Hive 쿼리 출력")</span><span class="sxs-lookup"><span data-stu-id="92697-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="92697-164">응용 프로그램 실행을 완료한 후 클러스터 리소스를 해제하도록 Notebook을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="92697-165">이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="92697-166">나중에 다음 단계를 완료하려는 경우 이 문서에서 만든 HDInsight 클러스터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="92697-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92697-167">Next step</span></span> 

<span data-ttu-id="92697-168">이 문서에서는 HDInsight Spark 클러스터를 만들고 기본 Spark SQL 쿼리를 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="92697-169">다음 문서를 진행하여 샘플 데이터에서 대화형 쿼리를 실행하는 데 HDInsight Spark 클러스터를 사용하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="92697-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="92697-170">HDInsight Spark 클러스터에서 대화형 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="92697-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



