---
title: "Azure에서 Scala 및 Spark를 사용하는 데이터 과학 | Microsoft Docs"
description: "Azure HDInsight Spark 클러스터에서 Spark 확장형 MLlib 및 SparkML 패키지를 사용하여 감독 기계 학습 작업에 대해 Scala를 사용하는 방법을 설명합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: b2419f53bdc3236d7de76b89f2a0a76704e85391
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="d795b-103">Azure에서 Scala 및 Spark를 사용하는 데이터 과학</span><span class="sxs-lookup"><span data-stu-id="d795b-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="d795b-104">이 문서에서는 Azure HDInsight Spark 클러스터에서 Spark 확장형 MLlib 및 SparkML 패키지를 사용하여 감독 기계 학습 작업에 대해 Scala를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="d795b-105">또한 [데이터 과학 프로세스](http://aka.ms/datascienceprocess): 데이터 수집 및 탐색, 시각화, 기능 엔지니어링, 모델링 및 모델 사용으로 이루어진 작업을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="d795b-106">이 문서의 모델에는 두 가지 일반적인 감독 기계 학습 작업 외에 로지스틱 및 선형 회귀, 임의 포리스트 및 GBT(그라데이션 향상 트리)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span></span>

* <span data-ttu-id="d795b-107">회귀 문제: 택시 여정에 대한 팁 금액 예측($)</span><span class="sxs-lookup"><span data-stu-id="d795b-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="d795b-108">이진 분류: 택시 여정에 대한 팁 또는 노팁(1/0) 예측</span><span class="sxs-lookup"><span data-stu-id="d795b-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="d795b-109">모델링 프로세스에는 관련 정확도 메트릭을 통한 테스트 데이터 집합의 학습 및 평가가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="d795b-110">이 문서에서는 이러한 모델을 Azure Blob 저장소에 저장하고 예측 성능의 점수를 매기며 평가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span></span> <span data-ttu-id="d795b-111">그뿐 아니라 교차 유효성 검사 및 하이퍼 매개 변수 스윕 작업을 사용하여 모델을 최적화하는 방법의 고급 항목도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="d795b-112">사용되는 데이터는 GitHub에서 사용할 수 있는 2013 NYC 택시 여정 및 요금 데이터 집합의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="d795b-113">Java 가상 컴퓨터 기반 언어인 [Scala](http://www.scala-lang.org/)는 개체 지향 개념과 함수 언어 개념을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="d795b-114">클라우드의 분산형 처리 및 Azure Spark 클러스터에 실행하기에 적합한 확장형 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="d795b-115">[Spark](http://spark.apache.org/) 는 메모리 내 처리를 지원하여 빅 데이터 분석 응용 프로그램의 성능을 향상하는 오픈 소스 병렬 처리 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span></span> <span data-ttu-id="d795b-116">속도, 간편한 사용 및 정교한 분석을 위해 Spark 처리 엔진이 빌드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="d795b-117">Spark는 메모리 내 분산형 계산 기능을 지원하여 기계 학습 및 그래프 계산의 반복 알고리즘에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="d795b-118">[spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) 패키지는 DataFrames 맨 위에 빌드된 균일한 상위 수준 API 집합을 제공하여 사용자가 실제 기계 학습 파이프라인을 만들고 조정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="d795b-119">[MLlib](http://spark.apache.org/mllib/) 는 Spark의 확장형 기계 학습 라이브러리로, 분산형 환경에서 모델링 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span></span>

<span data-ttu-id="d795b-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) 는 Azure에서 호스트하는 오픈 소스 Spark의 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="d795b-121">또한 Azure Blob 저장소에 저장된 데이터를 변환, 필터링 및 시각화하기 위해 Spark SQL 대화형 쿼리를 실행할 수 있는 Spark 클러스터 상의 Jupyter Scala Notebook에 대한 지원도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="d795b-122">이 문서에서 솔루션을 제공하고 데이터 시각화를 위해 관련 플롯을 보여 주는 Scala 코드 조각은 Spark 클러스터에 설치된 Jupyter Notebook에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span></span> <span data-ttu-id="d795b-123">이러한 항목의 모델링 단계는 각 모델 형식을 학습, 평가, 저장 및 사용하는 방법을 보여 주는 코드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="d795b-124">이 문서의 설정 단계 및 코드는 Azure HDInsight 3.4 Spark 1.6용입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="d795b-125">그러나 이 문서에 나오는 코드와 [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) 에 포함된 코드는 일반적이므로 모든 Spark 클러스터에서 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="d795b-126">HDInsight Spark를 사용하지 않는 경우 클러스터 설치 및 관리 단계가 이 문서에 나오는 내용과 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="d795b-127">Scala가 아닌 Python을 사용하여 종단 간 데이터 과학 프로세스에 대한 작업을 완료하는 방법을 보여 주는 항목에 대해서는 [Azure HDInsight에서 Spark를 사용하는 데이터 과학](machine-learning-data-science-spark-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d795b-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d795b-128">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d795b-128">Prerequisites</span></span>
* <span data-ttu-id="d795b-129">Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-129">You must have an Azure subscription.</span></span> <span data-ttu-id="d795b-130">아직 없으면 [Azure 무료 평가판을 다운로드하세요](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d795b-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d795b-131">다음 절차를 완료하려면 Azure HDInsight 3.4 Spark 1.6 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span></span> <span data-ttu-id="d795b-132">클러스터를 만들려면 [시작: Azure HDInsight에서 Apache Spark 만들기](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d795b-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="d795b-133">**클러스터 형식 선택** 메뉴에서 클러스터 형식 및 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-133">Set the cluster type and version on the **Select Cluster Type** menu.</span></span>

![HDInsight 클러스터 형식 구성](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="d795b-135">NYC 택시 여정 데이터에 대한 설명 및 Spark 클러스터의 Jupyter Notebook에서 코드를 실행하는 방법에 관한 지침은 [Azure HDInsight에서 Spark를 사용하는 데이터 과학 개요](machine-learning-data-science-spark-overview.md)의 관련 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d795b-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-the-spark-cluster"></a><span data-ttu-id="d795b-136">Spark 클러스터의 Jupyter Notebook에서 Scala 코드 실행</span><span class="sxs-lookup"><span data-stu-id="d795b-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span></span>
<span data-ttu-id="d795b-137">Azure 포털에서 Jupyter Notebook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-137">You can launch a Jupyter notebook from the Azure portal.</span></span> <span data-ttu-id="d795b-138">대시보드에서 Spark 클러스터를 찾아 클릭하여 클러스터에 대한 관리 페이지로 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span></span> <span data-ttu-id="d795b-139">다음으로 **클러스터 대시보드**, **Jupyter Notebook**을 차례로 클릭하여 Spark 클러스터와 연결된 Notebook을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span></span>

![클러스터 대시보드 및 Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="d795b-141">https://&lt;clustername&gt;.azurehdinsight.net/jupyter에서 Jupyter Notebook에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="d795b-142">*clustername* 을 사용자의 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-142">Replace *clustername* with the name of your cluster.</span></span> <span data-ttu-id="d795b-143">Jupyter Notebook에 액세스하려면 관리자 계정에 대한 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-143">You need the password for your administrator account to access the Jupyter notebooks.</span></span>

![클러스터 이름을 사용하여 Jupyter Notebook으로 이동](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="d795b-145">**Scala** 를 선택하여 PySpark API를 사용하는 미리 패키지된 Notebook의 몇 가지 예제가 있는 디렉터리를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span></span> <span data-ttu-id="d795b-146">이 Spark 항목 모음에 대한 코드 샘플이 포함된 Scala.ipynb Notebook을 사용하는 탐색 모델링 및 점수 매기기는 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="d795b-147">Notebook을 Github에서 Spark 클러스터의 Jupyter Notebook 서버에 직접 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="d795b-148">Jupyter 홈페이지에서 **Upload** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-148">On your Jupyter home page, click the **Upload** button.</span></span> <span data-ttu-id="d795b-149">파일 탐색기에서 Scala Notebook의 Github(원시 콘텐츠) URL을 붙여넣고 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="d795b-150">Scala Notebook은 다음 URL로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-150">The Scala notebook is available at the following URL:</span></span>

[<span data-ttu-id="d795b-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="d795b-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="d795b-152">설정: 사전 설정 Spark 및 Hive 컨텍스트, Spark 매직 및 Spark 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d795b-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="d795b-153">사전 설정 Spark 및 Hive 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="d795b-153">Preset Spark and Hive contexts</span></span>
    # SET THE START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="d795b-154">Jupyter Notebook이 제공되는 Spark 커널에는 사전 설정 컨텍스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="d795b-155">개발하는 응용 프로그램으로 작업을 시작하기 전에 Spark 또는 Hive 컨텍스트를 명시적으로 설정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span></span> <span data-ttu-id="d795b-156">사전 설정 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-156">The preset contexts are:</span></span>

* <span data-ttu-id="d795b-157">`sc` </span><span class="sxs-lookup"><span data-stu-id="d795b-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="d795b-158">`sqlContext` </span><span class="sxs-lookup"><span data-stu-id="d795b-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="d795b-159">Spark 매직</span><span class="sxs-lookup"><span data-stu-id="d795b-159">Spark magics</span></span>
<span data-ttu-id="d795b-160">Spark 커널은 특수 명령인 일부 미리 정의된 "매직"을 제공하며 이러한 매직은 `%%`기호를 사용하여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="d795b-161">이러한 명령 중 두 가지는 다음 코드 샘플에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-161">Two of these commands are used in the following code samples.</span></span>

* <span data-ttu-id="d795b-162">`%%local` 다음 줄의 코드가 로컬로 실행될 것임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="d795b-163">코드는 유효한 Scala 코드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-163">The code must be valid Scala code.</span></span>
* <span data-ttu-id="d795b-164">`%%sql -o <variable name>` `sqlContext`에 대해 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="d795b-165">`-o` 매개 변수가 전달된 경우 쿼리 결과가 `%%local` Scala 컨텍스트에서 Spark 데이터 프레임으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="d795b-166">Jupyter Notebook의 커널 및 `%%`(예: `%%local`)로 호출할 수 있는 미리 정의된 "매직"에 대한 자세한 내용은 [HDInsight의 HDInsight Spark Linux 클러스터에서 Jupyter Notebook에 대해 사용할 수 있는 커널](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d795b-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="d795b-167">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="d795b-167">Import libraries</span></span>
<span data-ttu-id="d795b-168">다음 코드를 사용하여 Spark, MLlib 및 기타 필요한 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span></span>

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a><span data-ttu-id="d795b-169">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="d795b-169">Data ingestion</span></span>
<span data-ttu-id="d795b-170">데이터 과학 프로세스의 첫 단계는 분석하려는 데이터를 수집하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span></span> <span data-ttu-id="d795b-171">외부 원본 또는 시스템의 데이터를 데이터 탐색 및 모델링 환경으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="d795b-172">이 문서에서 수집하는 데이터는 택시 여정 및 요금 파일(.tsv 파일로 저장됨)의 연결된 0.1% 샘플을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="d795b-173">데이터 탐색 및 모델링 환경은 Spark입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-173">The data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="d795b-174">이 섹션은 다음과 같은 일련의 작업을 완료하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-174">This section contains the code to complete the following series of tasks:</span></span>

1. <span data-ttu-id="d795b-175">데이터 및 모델 저장소에 대한 디렉터리 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="d795b-176">입력 데이터 집합을 읽습니다(.tsv 파일로 저장됨).</span><span class="sxs-lookup"><span data-stu-id="d795b-176">Read in the input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="d795b-177">데이터에 대한 스키마를 정의하고 데이터를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-177">Define a schema for the data and clean the data.</span></span>
4. <span data-ttu-id="d795b-178">정리된 데이터 프레임을 만들고 메모리에 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="d795b-179">데이터를 SQLContext의 임시 테이블로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-179">Register the data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="d795b-180">테이블을 쿼리하고 결과를 데이터 프레임으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-180">Query the table and import the results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="d795b-181">Azure Blob 저장소의 저장소 위치에 대한 디렉터리 경로 설정</span><span class="sxs-lookup"><span data-stu-id="d795b-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="d795b-182">Spark에서는 Azure Blob 저장소에서 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-182">Spark can read and write to Azure Blob storage.</span></span> <span data-ttu-id="d795b-183">Spark를 사용하여 기존 데이터를 처리한 다음 결과를 Blob 저장소에 다시 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span></span>

<span data-ttu-id="d795b-184">Blob 저장소에 모델 또는 파일을 저장하려면 경로를 적절히 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-184">To save models or files in Blob storage, you need to properly specify the path.</span></span> <span data-ttu-id="d795b-185">`wasb:///`로 시작하는 경로를 사용하여 Spark 클러스터에 연결된 기본 컨테이너를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="d795b-186">`wasb://`를 사용하여 다른 위치를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="d795b-187">다음 코드 샘플은 읽을 입력 데이터의 위치 및 모델이 저장될 Spark 클러스터에 연결된 Blob 저장소에 대한 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span></span>

    # SET PATHS TO DATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET THE MODEL STORAGE DIRECTORY PATH
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-to-the-schema"></a><span data-ttu-id="d795b-188">데이터 가져오기, RDD 만들기 및 스키마에 따라 데이터 프레임 정의</span><span class="sxs-lookup"><span data-stu-id="d795b-188">Import data, create an RDD, and define a data frame according to the schema</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE SCHEMA BASED ON THE HEADER OF THE FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING TO THE SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE THE CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER THE DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d795b-189">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-189">**Output:**</span></span>

<span data-ttu-id="d795b-190">셀 실행 시간: 8초</span><span class="sxs-lookup"><span data-stu-id="d795b-190">Time to run the cell: 8 seconds.</span></span>

### <a name="query-the-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="d795b-191">테이블을 쿼리하고 결과를 데이터 프레임으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="d795b-191">Query the table and import results in a data frame</span></span>
<span data-ttu-id="d795b-192">다음으로 요금, 승객 및 팁 데이터에 대한 테이블을 쿼리하고, 손상된 외부 데이터를 필터링하며 여러 행으로 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY THE DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY THE TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="d795b-193">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-193">**Output:**</span></span>

| <span data-ttu-id="d795b-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="d795b-194">fare_amount</span></span> | <span data-ttu-id="d795b-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="d795b-195">passenger_count</span></span> | <span data-ttu-id="d795b-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="d795b-196">tip_amount</span></span> | <span data-ttu-id="d795b-197">tipped</span><span class="sxs-lookup"><span data-stu-id="d795b-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="d795b-198">13.5</span><span class="sxs-lookup"><span data-stu-id="d795b-198">13.5</span></span> |<span data-ttu-id="d795b-199">1.0</span><span class="sxs-lookup"><span data-stu-id="d795b-199">1.0</span></span> |<span data-ttu-id="d795b-200">2.9</span><span class="sxs-lookup"><span data-stu-id="d795b-200">2.9</span></span> |<span data-ttu-id="d795b-201">1.0</span><span class="sxs-lookup"><span data-stu-id="d795b-201">1.0</span></span> |
|        <span data-ttu-id="d795b-202">16.0</span><span class="sxs-lookup"><span data-stu-id="d795b-202">16.0</span></span> |<span data-ttu-id="d795b-203">2.0</span><span class="sxs-lookup"><span data-stu-id="d795b-203">2.0</span></span> |<span data-ttu-id="d795b-204">3.4</span><span class="sxs-lookup"><span data-stu-id="d795b-204">3.4</span></span> |<span data-ttu-id="d795b-205">1.0</span><span class="sxs-lookup"><span data-stu-id="d795b-205">1.0</span></span> |
|        <span data-ttu-id="d795b-206">10.5</span><span class="sxs-lookup"><span data-stu-id="d795b-206">10.5</span></span> |<span data-ttu-id="d795b-207">2.0</span><span class="sxs-lookup"><span data-stu-id="d795b-207">2.0</span></span> |<span data-ttu-id="d795b-208">1.0</span><span class="sxs-lookup"><span data-stu-id="d795b-208">1.0</span></span> |<span data-ttu-id="d795b-209">1.0</span><span class="sxs-lookup"><span data-stu-id="d795b-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="d795b-210">데이터 탐색 및 시각화</span><span class="sxs-lookup"><span data-stu-id="d795b-210">Data exploration and visualization</span></span>
<span data-ttu-id="d795b-211">데이터를 Spark로 가져오면 데이터 과학 프로세스의 다음 단계에서 탐색 및 시각화를 통해 데이터를 더 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="d795b-212">이 섹션에서는 SQL 쿼리를 사용하여 Taxi 데이터를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-212">In this section, you examine the taxi data by using SQL queries.</span></span> <span data-ttu-id="d795b-213">그런 후 결과를 데이터 프레임으로 가져와 Jupyter의 자동 시각화 기능을 사용하여 시각적 조사에 대한 대상 변수 및 잠재 기능을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-to-plot-data"></a><span data-ttu-id="d795b-214">로컬 및 SQL 매직을 사용하여 데이터 그리기</span><span class="sxs-lookup"><span data-stu-id="d795b-214">Use local and SQL magic to plot data</span></span>
<span data-ttu-id="d795b-215">기본적으로 Jupyter Notebook에서 실행하는 코드 조각의 출력은 작업자 노드에서 유지되는 세션 컨텍스트 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span></span> <span data-ttu-id="d795b-216">모든 계산에 대한 작업자 노드에 여정을 저장하는 경우와 계산에 필요한 모든 데이터를 Jupyter 서버 노드(헤드 노드)에서 로컬로 사용할 수 있는 경우, `%%local` 매직을 사용하여 Jupyter 서버에서 코드 조각을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span></span>

* <span data-ttu-id="d795b-217">**SQL 매직**(`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="d795b-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="d795b-218">HDInsight Spark 커널은 SQLContext에 대해 간편한 인라인 HiveQL 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="d795b-219">(`-o VARIABLE_NAME`) 인수는 Jupyter 서버에서 Pandas 데이터 프레임으로 SQL 쿼리의 출력을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span></span> <span data-ttu-id="d795b-220">즉, 로컬 모드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-220">This means it'll be available in the local mode.</span></span>
* <span data-ttu-id="d795b-221">`%%local` **매직**.</span><span class="sxs-lookup"><span data-stu-id="d795b-221">`%%local` **magic**.</span></span> <span data-ttu-id="d795b-222">`%%local` 매직은 HDInsight 클러스터의 헤드 노드인 Jupyter 서버에서 코드를 로컬로 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span></span> <span data-ttu-id="d795b-223">일반적으로 `-o` 매개 변수를 사용하여 `%%local` 매직을 `%%sql` 매직과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span></span> <span data-ttu-id="d795b-224">`-o` 매개 변수는 SQL 쿼리의 출력을 로컬로 유지하고 그 다음 `%%local` 매직은 로컬로 유지되는 SQL 쿼리의 출력에 대해 로컬로 실행할 다음 코드 조각 집합을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span></span>

### <a name="query-the-data-by-using-sql"></a><span data-ttu-id="d795b-225">SQL을 사용하여 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="d795b-225">Query the data by using SQL</span></span>
<span data-ttu-id="d795b-226">이 쿼리는 요금 금액, 승객 수 및 팁 금액에 따라 택시 여정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN THE SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="d795b-227">다음 코드에서 `%%local` 매직은 sqlResults 로컬 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="d795b-228">sqlResults의 matplotlib를 사용하여 그림을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-228">You can use sqlResults to plot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="d795b-229">로컬 매직은 이 문서에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="d795b-230">데이터 집합이 큰 경우 로컬 메모리에 맞게 데이터 프레임을 만들도록 샘플링하세요.</span><span class="sxs-lookup"><span data-stu-id="d795b-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-the-data"></a><span data-ttu-id="d795b-231">데이터 그리기</span><span class="sxs-lookup"><span data-stu-id="d795b-231">Plot the data</span></span>
<span data-ttu-id="d795b-232">데이터 프레임이 Pandas 데이터 프레임처럼 로컬 컨텍스트에 있으면 Python 코드를 사용하여 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES.
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="d795b-233">Spark 커널은 코드를 실행한 후 SQL(HiveQL) 쿼리의 출력을 자동으로 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span></span> <span data-ttu-id="d795b-234">여러 형식의 시각화 요소 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="d795b-235">테이블</span><span class="sxs-lookup"><span data-stu-id="d795b-235">Table</span></span>
* <span data-ttu-id="d795b-236">원형</span><span class="sxs-lookup"><span data-stu-id="d795b-236">Pie</span></span>
* <span data-ttu-id="d795b-237">꺾은선형</span><span class="sxs-lookup"><span data-stu-id="d795b-237">Line</span></span>
* <span data-ttu-id="d795b-238">영역</span><span class="sxs-lookup"><span data-stu-id="d795b-238">Area</span></span>
* <span data-ttu-id="d795b-239">가로 막대형</span><span class="sxs-lookup"><span data-stu-id="d795b-239">Bar</span></span>

<span data-ttu-id="d795b-240">다음은 데이터를 그리는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-240">Here's the code to plot the data:</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


<span data-ttu-id="d795b-241">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-241">**Output:**</span></span>

![팁 금액 히스토그램](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![승객 수에 따른 여정 수](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![금액으로 녀건 금액](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="d795b-245">기능을 만들고 변환한 후 모델링 함수에 입력하기 위한 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="d795b-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="d795b-246">Spark ML 및 MLlib의 트리 기반 모델링 기능의 경우 범주화, 인덱싱, 원 핫 인코딩(one hot encoding), 벡터화 등의 다양한 해당 기법을 사용하여 대상 및 기능을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="d795b-247">이 섹션에서 수행하는 절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-247">Here are the procedures to follow in this section:</span></span>

1. <span data-ttu-id="d795b-248">시간을 트래픽 시간 버킷으로 **범주화** 하여 새로운 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="d795b-249">범주 기능에 **인덱싱 및 원 핫 인코딩(one-hot encoding)** 을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-249">Apply **indexing and one-hot encoding** to categorical features.</span></span>
3. <span data-ttu-id="d795b-250">**데이터 집합을 학습 및 테스트 부분으로 샘플링 및 분할** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-250">**Sample and split the data set** into training and test fractions.</span></span>
4. <span data-ttu-id="d795b-251">**학습 변수 및 기능을 지정**하고, 인덱싱되었거나 원 핫 인코딩된 학습 및 테스팅 입력 레이블이 지정된 지점 RDD(탄력성 분산 데이터 집합) 또는 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="d795b-252">기계 학습 모델에 대한 입력으로 사용할 **기능과 대상을 자동으로 범주화 및 벡터화** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="d795b-253">시간을 트래픽 시간 버킷으로 범주화하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="d795b-254">이 코드는 트래픽 시간 버킷으로 시간을 범주화하여 새로운 기능을 만드는 방법 및 메모리에 결과 데이터 프레임을 캐시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="d795b-255">RDD 및 데이터 프레임을 반복해서 사용하는 경우 캐시하면 실행 시간이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="d795b-256">따라서 RDD 및 데이터 프레임을 다음 절차의 여러 단계에서 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE THE DATA FRAME IN MEMORY AND MATERIALIZE THE DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="d795b-257">범주 기능 인덱싱 및 원 핫 인코딩</span><span class="sxs-lookup"><span data-stu-id="d795b-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="d795b-258">MLlib의 모델링 및 예측 함수는 사용하기 전에 범주 입력 데이터로 기능을 인덱싱 또는 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="d795b-259">이 섹션에는 모델링 기능에 입력에 대한 범주 기능을 인덱싱하거나 인코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span></span>

<span data-ttu-id="d795b-260">모델에 따라 다양한 방식으로 모델을 인덱싱하거나 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-260">You need to index or encode your models in different ways, depending on the model.</span></span> <span data-ttu-id="d795b-261">예를 들어 로지스틱 및 선형 회귀 모델에는 원 핫 인코딩이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="d795b-262">예를 들어 세 개의 범주가 있는 기능을 세 개의 기능 열로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="d795b-263">관찰 범주에 따라, 각 열에는 0 또는 1이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-263">Each column would contain 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="d795b-264">MLlib는 원 핫 인코딩을 위한 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="d795b-265">이 인코더는 레이블 인덱스의 열을 단 하나의 값을 가진 이진 벡터의 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="d795b-266">이 인코딩을 사용하여 로지스틱 회귀 분석 등과 같은 숫자 값을 가진 기능을 예상하는 알고리즘을 범주 기능에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span></span>

<span data-ttu-id="d795b-267">여기서는 문자열 예를 보여 주기 위해 4개의 변수만 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-267">Here you transform only four variables to show examples, which are character strings.</span></span> <span data-ttu-id="d795b-268">평일과 같이 숫자 값으로 표현되는 기타 변수는 범주 변수로 인덱싱할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="d795b-269">인덱싱에는 `StringIndexer()` 함수를 사용하고 원 핫 인코딩에는 MLlib의 `OneHotEncoder()` 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="d795b-270">다음은 범주 기능을 인덱스 및 인코딩하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-270">Here is the code to index and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d795b-271">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-271">**Output:**</span></span>

<span data-ttu-id="d795b-272">셀 실행 시간: 4초</span><span class="sxs-lookup"><span data-stu-id="d795b-272">Time to run the cell: 4 seconds.</span></span>

### <a name="sample-and-split-the-data-set-into-training-and-test-fractions"></a><span data-ttu-id="d795b-273">데이터 집합을 학습 및 테스트 부분으로 샘플링 및 분할</span><span class="sxs-lookup"><span data-stu-id="d795b-273">Sample and split the data set into training and test fractions</span></span>
<span data-ttu-id="d795b-274">이 코드는 데이터의 무작위 샘플링을 만듭니다(이 예제에서는 25%).</span><span class="sxs-lookup"><span data-stu-id="d795b-274">This code creates a random sampling of the data (25%, in this example).</span></span> <span data-ttu-id="d795b-275">데이터 집합의 크기로 인해 이 예제에는 샘플링이 필요하지 않지만, 이 문서에서는 필요한 경우 자신의 문제에 사용하는 방식을 알 수 있도록 샘플링 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span></span> <span data-ttu-id="d795b-276">샘플이 큰 경우 모델을 학습하는 동안 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="d795b-277">다음으로, 샘플을 교육 부분(이 예제에서는 75%)과 테스트 부분(이 예제에서는 25%)으로 분할하여 분류 및 회귀 모델링에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span></span>

<span data-ttu-id="d795b-278">학습 중에 교차 유효성 검사 접기를 선택하는 데 사용할 수 있는 행("rand" 열에서)에 도달하기 위해 난수(0과 1 사이)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT THE SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d795b-279">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-279">**Output:**</span></span>

<span data-ttu-id="d795b-280">셀 실행 시간: 2초</span><span class="sxs-lookup"><span data-stu-id="d795b-280">Time to run the cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="d795b-281">학습 변수 및 기능 지정, 인덱싱되었거나 원 핫 인코딩된 학습 및 테스팅 입력 레이블이 지정된 지점 RDD 또는 데이터 프레임 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="d795b-282">이 섹션은 범주 텍스트 데이터를 레이블이 지정된 지점 데이터 형식으로 인덱싱하고 인코딩하는 방법을 보여주는 코드를 포함하여 MLlib 로지스틱 회귀 및 다른 분류 모델을 학습하고 테스트하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="d795b-283">레이블이 지정된 지점 개체는 대부분 MLlib의 기계 학습 알고리즘에서 입력 데이터로 필요한 방식으로 형식이 지정된 RDD입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="d795b-284">[레이블이 지정된 지점](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 은 레이블/응답과 연결된 로컬 벡터, 밀도 또는 스파스입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="d795b-285">이 코드에서는 모델을 학습하는 데 사용할 대상(종속) 변수 및 기능을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span></span> <span data-ttu-id="d795b-286">그런 후 인덱싱되었거나 원 핫 인코딩된 학습 및 테스팅 입력 레이블이 지정된 지점 RDD 또는 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY THE TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d795b-287">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-287">**Output:**</span></span>

<span data-ttu-id="d795b-288">셀 실행 시간: 4초</span><span class="sxs-lookup"><span data-stu-id="d795b-288">Time to run the cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-to-use-as-inputs-for-machine-learning-models"></a><span data-ttu-id="d795b-289">기계 학습 모델에 대한 입력으로 사용할 기능과 대상을 자동으로 범주화 및 벡터화</span><span class="sxs-lookup"><span data-stu-id="d795b-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span></span>
<span data-ttu-id="d795b-290">Spark ML을 사용하여 트리 기반 모델링 기능에 사용할 대상 및 기능을 범주화합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span></span> <span data-ttu-id="d795b-291">이 코드는 다음 두 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-291">The code completes two tasks:</span></span>

* <span data-ttu-id="d795b-292">0.5의 임계값을 사용하는 0과 1 사이의 각 데이터 요소에 0 또는 1 값을 할당하여 분류의 이진 대상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="d795b-293">기능을 자동으로 범주화합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-293">Automatically categorizes features.</span></span> <span data-ttu-id="d795b-294">기능에 대한 고유 숫자 값이 32보다 작은 경우 해당 기능은 범주화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="d795b-295">이러한 두 작업에 대한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-295">Here's the code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE THE TARGET FOR THE BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR THE REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="d795b-296">이진 분류 모델: 팁이 지불되었는지 예측</span><span class="sxs-lookup"><span data-stu-id="d795b-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="d795b-297">이 섹션에서는 팁이 지불되었는지 아닌지를 예측하기 위해 이진 분류 모델을 세 가지 형식으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="d795b-298">Spark ML `LogisticRegression()` 함수를 사용하는 **로지스틱 회귀 모델**</span><span class="sxs-lookup"><span data-stu-id="d795b-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="d795b-299">Spark ML `RandomForestClassifier()` 함수를 사용하는 **임의 포리스트 분류 모델**</span><span class="sxs-lookup"><span data-stu-id="d795b-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="d795b-300">MLlib `GradientBoostedTrees()` 함수를 사용하는 **그라데이션 향상 트리 분류 모델**</span><span class="sxs-lookup"><span data-stu-id="d795b-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="d795b-301">로지스틱 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-301">Create a logistic regression model</span></span>
<span data-ttu-id="d795b-302">다음으로, Spark ML `LogisticRegression()` 함수를 사용하여 로지스틱 회귀 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="d795b-303">다음과 같은 단계를 통해 모델 빌딩 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-303">You create the model building code in a series of steps:</span></span>

1. <span data-ttu-id="d795b-304">**모델 학습** 데이터</span><span class="sxs-lookup"><span data-stu-id="d795b-304">**Train the model** data with one parameter set.</span></span>
2. <span data-ttu-id="d795b-305">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="d795b-305">**Evaluate the model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="d795b-306">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="d795b-306">**Save the model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="d795b-307">**모델 점수 매기기** </span><span class="sxs-lookup"><span data-stu-id="d795b-307">**Score the model** against test data.</span></span>
5. <span data-ttu-id="d795b-308">**결과 그리기** </span><span class="sxs-lookup"><span data-stu-id="d795b-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="d795b-309">이러한 절차에 대한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-309">Here's the code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON THE TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE THE MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="d795b-310">결과를 로드하고 점수를 매기고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-310">Load, score, and save the results.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD THE SAVED MODEL AND SCORE THE TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON THE TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="d795b-311">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-311">**Output:**</span></span>

<span data-ttu-id="d795b-312">ROC on test data = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="d795b-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="d795b-313">로컬 Pandas 데이터 프레임에서 Python을 사용하여 ROC 곡선을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-313">Use Python on local Pandas data frames to plot the ROC curve.</span></span>

    # QUERY THE RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT THE ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT THE ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="d795b-314">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-314">**Output:**</span></span>

![팁 여부 ROC 곡선](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="d795b-316">임의 포리스트 분류 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-316">Create a random forest classification model</span></span>
<span data-ttu-id="d795b-317">다음으로 Spark ML `RandomForestClassifier()` 함수를 사용하는 임의 포리스트 분류 모델을 만들고 테스트 데이터에 대해 모델을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE THE RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT THE MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE THE MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="d795b-318">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-318">**Output:**</span></span>

<span data-ttu-id="d795b-319">ROC on test data = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="d795b-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="d795b-320">GBT 분류 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-320">Create a GBT classification model</span></span>
<span data-ttu-id="d795b-321">다음으로 MLlib `GradientBoostedTrees()` 함수를 사용하여 GBT 분류 모델을 만들고 테스트 데이터에 대해 모델을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN THE MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE THE MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE THE MODEL ON TEST INSTANCES AND THE COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS TO EVALUATE THE MODEL ON THE TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="d795b-322">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-322">**Output:**</span></span>

<span data-ttu-id="d795b-323">Area under ROC curve: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="d795b-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="d795b-324">회귀 모델: 팁 금액 예측</span><span class="sxs-lookup"><span data-stu-id="d795b-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="d795b-325">이 섹션에서는 팁 금액을 예측하기 위해 두 가지 형식의 회귀 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-325">In this section, you create two types of regression models to predict the tip amount:</span></span>

* <span data-ttu-id="d795b-326">Spark ML `LinearRegression()` 함수를 사용하는 **정칙 선형 회귀 모델**</span><span class="sxs-lookup"><span data-stu-id="d795b-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="d795b-327">모델을 저장하고 테스트 데이터에 대해 모델을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-327">You'll save the model and evaluate the model on test data.</span></span>
* <span data-ttu-id="d795b-328">Spark ML `GBTRegressor()` 함수를 사용하는 **그라데이션 향상 트리 회귀 모델**</span><span class="sxs-lookup"><span data-stu-id="d795b-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="d795b-329">정칙 선형 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-329">Create a regularized linear regression model</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING THE SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT THE MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE THE MODEL OVER THE TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE THE MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT THE COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d795b-330">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-330">**Output:**</span></span>

<span data-ttu-id="d795b-331">셀 실행 시간: 13초</span><span class="sxs-lookup"><span data-stu-id="d795b-331">Time to run the cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="d795b-332">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-332">**Output:**</span></span>

<span data-ttu-id="d795b-333">R-sqr on test data = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="d795b-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="d795b-334">다음으로, 테스트 결과를 데이터 프레임으로 쿼리하고 AutoVizWidget 및 matplotlib를 사용하여 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="d795b-335">이 코드는 쿼리 출력에서 로컬 데이터 프레임을 만들고 데이터를 그립니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-335">The code creates a local data frame from the query output and plots the data.</span></span> <span data-ttu-id="d795b-336">`%%local` 매직은 matplotlib로 그리는 데 사용할 수 있는 로컬 데이터 프레임 `sqlResults`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="d795b-337">이 Spark 매직은 이 문서에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="d795b-338">데이터 양이 많은 경우 로컬 메모리에 맞게 데이터 프레임을 만들도록 샘플링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="d795b-339">Python matplotlib를 사용하여 도표를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-339">Create plots by using Python matplotlib.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT THE RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="d795b-340">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-340">**Output:**</span></span>

![팁 금액: 실제 및 예측](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="d795b-342">GBT 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d795b-342">Create a GBT regression model</span></span>
<span data-ttu-id="d795b-343">Spark ML `GBTRegressor()` 함수를 사용하여 GBT 회귀 모델을 만들고 테스트 데이터에 대해 모델을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span></span>

<span data-ttu-id="d795b-344">[GBT](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (그라데이션 향상 트리)는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="d795b-345">GBT는 기능 손실을 최소화하기 위해 결정 트리를 반복적으로 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-345">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="d795b-346">회귀 및 분류에 대해 GBT를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="d795b-347">GBT는 범주 기능을 처리하고 기능 규모 결정을 요구하지 않으며 비선형 기능 상호 작용을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="d795b-348">또한 다중 클래스 분류 설정에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="d795b-349">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-349">**Output:**</span></span>

<span data-ttu-id="d795b-350">Test R-sqr is: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="d795b-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="d795b-351">최적화를 위한 고급 모델링 유틸리티</span><span class="sxs-lookup"><span data-stu-id="d795b-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="d795b-352">이 섹션에서는 개발자가 모델 최적화를 위해 자주 사용하는 기계 학습 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="d795b-353">특히, 매개 변수 스윕 작업 및 교차 유효성 검사를 사용하여 세 가지 다른 방식으로 기계 학습 모델을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="d795b-354">데이터를 학습 및 유효성 검사 집합으로 분할하고, 학습 집합에서 하이퍼 매개 변수 스윕 작업을 사용하여 모델을 최적화하고, 유효성 검사 집합에서 평가를 수행합니다(선형 회귀).</span><span class="sxs-lookup"><span data-stu-id="d795b-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="d795b-355">Spark ML의 CrossValidator 함수(이진 분류)를 사용하여 교차 유효성 검사 및 하이퍼 매개 변수 스윕 작업을 통해 모델을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="d795b-356">사용자 지정 교차 유효성 검사 및 매개 변수 스윕 작업 코드를 사용하여 모든 기계 학습 함수 및 매개 변수 집합을 통해 모델을 최적화합니다(선형 회귀).</span><span class="sxs-lookup"><span data-stu-id="d795b-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="d795b-357">**교차 유효성 검사** 는 알려진 데이터 집합에서 학습된 모델이 학습되지 않은 데이터 집합의 기능 예측을 얼마나 잘 일반화하는지 평가하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span></span> <span data-ttu-id="d795b-358">이 기술의 일반 개념은 알려진 데이터의 데이터 집합에서 모델을 학습한 다음 독립된 데이터 집합에 대해 예측 정확도를 테스트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="d795b-359">일반적인 구현은 데이터 집합을 *k*접기로 나눈 다음 접기 중 하나를 제외한 모든 접기에서 라운드 로빈 방식으로 모델을 학습하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span></span>

<span data-ttu-id="d795b-360">**하이퍼 매개 변수 최적화** 는 학습 알고리즘에 대한 하이퍼 매개 변수 집합을 선택하는 문제이며, 일반적으로 독립된 데이터 집합에서의 알고리즘 성능 측정값을 최적화하는 것을 목표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="d795b-361">하이퍼 매개 변수는 모델 학습 프로시저 외부에서 지정해야 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span></span> <span data-ttu-id="d795b-362">하이퍼 매개 변수 값에 대한 가정은 모델의 유연성 및 정확도에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span></span> <span data-ttu-id="d795b-363">의사 결정 트리에는 원하는 깊이와 트리의 리프 수와 같은 하이퍼 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="d795b-364">SVM(지원 벡터 컴퓨터)은 오분류 페널티 조건을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="d795b-365">하이퍼 매개 변수 최적화를 수행하는 일반적인 방법은 **매개 변수 스윕**이라고도 하는 그리드 검색을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="d795b-366">그리드 검색에서는 학습 알고리즘에 대한 하이퍼 매개 변수 공간의 지정된 하위 집합 값으로 철저하게 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="d795b-367">교차 유효성 검사는 그리드 검색 알고리즘에 의해 생성되는 최적의 결과를 분류하는 성능 메트릭을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="d795b-368">교차 유효성 검사 하이퍼 매개 변수 스윕 작업을 사용하는 경우 모델 과잉 맞춤과 같은 문제를 학습 데이터로 제한하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span></span> <span data-ttu-id="d795b-369">이러한 방식으로 모델은 학습 데이터가 추출된 일반적인 데이터 집합에 적용할 수 있는 용량을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="d795b-370">하이퍼 매개 변수 스윕 작업으로 선형 회귀 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d795b-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="d795b-371">다음으로 데이터를 학습 및 유효성 검사 집합으로 분할하고, 학습 집합에서 하이퍼 매개 변수 스윕 작업을 사용하여 모델을 최적화하고, 유효성 검사 집합에서 평가를 수행합니다(선형 회귀).</span><span class="sxs-lookup"><span data-stu-id="d795b-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE THE ESTIMATOR FUNCTION: `THE LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE THE PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET), AND THEN THE SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="d795b-372">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-372">**Output:**</span></span>

<span data-ttu-id="d795b-373">Test R-sqr is: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="d795b-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-the-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="d795b-374">교차 유효성 검사 및 하이퍼 매개 변수 스윕 작업을 사용하여 이진 분류 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d795b-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="d795b-375">이 섹션에서는 교차 유효성 검사 및 하이퍼 매개 변수 스윕 작업을 사용하여 이진 분류 모델을 최적화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="d795b-376">여기서는 Spark ML `CrossValidator` 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-376">This uses the Spark ML `CrossValidator` function.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS TO USE WITH THE TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE THE ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY THE NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE THE TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE THE TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d795b-377">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-377">**Output:**</span></span>

<span data-ttu-id="d795b-378">셀 실행 시간: 33초</span><span class="sxs-lookup"><span data-stu-id="d795b-378">Time to run the cell: 33 seconds.</span></span>

### <a name="optimize-the-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="d795b-379">사용자 지정 교차 유효성 검사 및 매개 변수 스윕 작업 코드를 사용하여 선형 회귀 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d795b-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="d795b-380">다음으로 사용자 지정 코드를 사용하여 모델을 최적화하고 최고 정확도 기준을 사용하여 최적의 모델 매개 변수를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span></span> <span data-ttu-id="d795b-381">그런 다음 최종 모델을 만들고 테스트 데이터로 모델을 평가하고 Blob 저장소에 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span></span> <span data-ttu-id="d795b-382">마지막으로 모델을 로드하고 테스트 데이터의 점수를 매기며 해당 정확도를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-382">Finally, load the model, score test data, and evaluate accuracy.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE PARAMETER GRID AND THE NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY THE NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND THE PARAMETER GRID TO GET AND IDENTIFY THE BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 to (nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 to (numModels-1)) {
            for (nParams <- 0 to (numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET THE BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 to (numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE THE BEST MODEL WITH THE BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE THE BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON THE TRAINING SET WITH THE BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


    # LOAD THE MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST THE MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="d795b-383">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d795b-383">**Output:**</span></span>

<span data-ttu-id="d795b-384">셀 실행 시간: 61초</span><span class="sxs-lookup"><span data-stu-id="d795b-384">Time to run the cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="d795b-385">Scala를 사용하여 Spark에서 빌드한 기계 학습 모델을 자동으로 사용</span><span class="sxs-lookup"><span data-stu-id="d795b-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="d795b-386">Azure에서 데이터 과학 프로세스를 구성하는 작업을 안내하는 항목에 대한 개요는 [팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d795b-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="d795b-387">[팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md) 에서는 특정 시나리오에 대한 팀 데이터 과학 프로세스의 단계를 보여 주는 다른 종단 간 연습에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="d795b-388">또한 이 연습에서는 클라우드 및 온-프레미스 도구와 서비스를 워크플로 또는 파이프라인에 결합하여 지능형 응용 프로그램을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>

<span data-ttu-id="d795b-389">[Spark에서 빌드한 기계 학습 모델 점수 매기기](machine-learning-data-science-spark-model-consumption.md) 에서는 Scala 코드를 사용하여 Spark에서 빌드한 기계 학습 모델과 함께 Azure Blob 저장소에 저장된 새 데이터 집합을 자동으로 로드하고 점수를 매기는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="d795b-390">사용자는 제공된 지침을 따르고 자동 사용을 위해 Python 코드를 이 문서의 Scala 코드로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d795b-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span></span>

