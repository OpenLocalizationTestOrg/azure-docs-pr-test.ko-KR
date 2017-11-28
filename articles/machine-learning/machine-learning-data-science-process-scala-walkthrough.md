---
title: "aaaData 과학 Scala 및 Spark를 사용 하 여 Azure에서 | Microsoft Docs"
description: "어떻게 toouse Scala 감독 된 기계 학습 작업에 대 한 hello Spark 확장 가능한 MLlib 및 Spark ML 패키지 Azure HDInsight Spark 클러스터에 있습니다."
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
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="d75e1-103">Azure에서 Scala 및 Spark를 사용하는 데이터 과학</span><span class="sxs-lookup"><span data-stu-id="d75e1-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="d75e1-104">이 문서에서는 Azure HDInsight Spark 클러스터에서 toouse Scala Spark 확장 가능한 MLlib hello 및 Spark ML 감독 된 기계 학습 작업에 대 한 패키지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="d75e1-105">Hello를 구성 하는 hello 작업 안내 합니다 [데이터 과학 프로세스](http://aka.ms/datascienceprocess): 데이터를 수집 하 고 탐색, 시각화, 기능 엔지니어링, 모델링 및 모델 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="d75e1-106">tootwo 공통 기계 학습 작업을 감독 하는 또한, 물류 및 선형 회귀, 임의 포리스트 및 그라데이션 승격 된 트리 (GBTs) hello 모델 hello 문서에 포함:</span><span class="sxs-lookup"><span data-stu-id="d75e1-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="d75e1-107">회귀 문제: hello 팁 금액 ($) 택시 여행에 대 한 예측</span><span class="sxs-lookup"><span data-stu-id="d75e1-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="d75e1-108">이진 분류: 택시 여정에 대한 팁 또는 노팁(1/0) 예측</span><span class="sxs-lookup"><span data-stu-id="d75e1-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="d75e1-109">프로세스를 모델링 하는 hello 학습 및 테스트 데이터 집합 및 관련 정확도 메트릭을 평가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="d75e1-110">이 문서에서는 학습할 수 있는 방법을 toostore 이러한 모델에 Azure Blob 저장소와 방법을 tooscore 하 고 예측의 성능을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="d75e1-111">Hello 더 고급 toooptimize 교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용 하 여 모델링 하는 방법의 항목에이 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="d75e1-112">사용 되는 hello 데이터는 hello 2013 NYC 택시 여행 및 요금 데이터 집합의 GitHub에서 사용할 수 있는 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="d75e1-113">[Scala](http://www.scala-lang.org/), 개체 지향 및 기능 언어 개념을 통합 하는 hello Java 가상 컴퓨터 기반 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="d75e1-114">것은 적합된 toodistributed hello 클라우드에서 처리 되 고 Azure Spark 클러스터에서 실행 하는 확장 가능한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="d75e1-115">[Spark](http://spark.apache.org/) 빅 데이터 분석 응용 프로그램의 tooboost hello 성능 처리에 메모리를 지 원하는 오픈 소스 병렬 처리 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="d75e1-116">hello Spark 처리 엔진에 대 한 속도, 사용 및 복잡 한 분석의 용이성 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="d75e1-117">Spark는 메모리 내 분산형 계산 기능을 지원하여 기계 학습 및 그래프 계산의 반복 알고리즘에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="d75e1-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) 패키지 균일 하 게 하는 프레임을 만들고 파이프라인을 학습 하는 실제 컴퓨터를 튜닝 하는 데이터를 기반으로 빌드된 고급 수준의 Api 집합이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="d75e1-119">[MLlib](http://spark.apache.org/mllib/) 모델링 기능을 도입 하는 스파크의 확장 가능한 기계 학습 라이브러리는 toothis 분산된 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="d75e1-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) 은 오픈 소스 Spark의 hello Azure 호스팅 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="d75e1-121">Hello Spark 클러스터에서 Jupyter Scala 전자 필기장에 대 한 지원도 포함 됩니다 하 고 실행된 Spark SQL 대화형 쿼리 tootransform 필터링 하 고 수 Azure Blob 저장소에 저장 된 데이터를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="d75e1-122">hello Scala 코드 조각을이 문서의 hello 솔루션을 제공 하 고 hello 관련 점도 toovisualize hello 데이터를 보여 주는 Jupyter 노트북 hello Spark 클러스터에 설치에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="d75e1-123">이 항목의 hello 모델링 단계를 각 모델의 입력, tootrain를 평가, 저장 및 사용 방법을 보여 줍니다 해당 코드 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="d75e1-124">Azure HDInsight 3.4 Spark 1.6 hello 설정 단계 및이 문서의 코드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="d75e1-125">그러나이 문서 및 hello 코드 hello [Scala Jupyter 노트북](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) 어떤 Spark 클러스터에서 작동 해야 하 고 일반적으로 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="d75e1-126">hello 클러스터 설치 및 관리 단계 HDInsight Spark를 사용 하지 않는 경우이 문서에 표시 되는 기능에서 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="d75e1-127">Toouse Scala 보다는 Python toocomplete 종단 간 데이터 과학 프로세스에 대 한 작업 하는 방법을 보여 주는 항목을 참조 하십시오. [Azure HDInsight의 Spark를 사용 하 여 데이터 과학](machine-learning-data-science-spark-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d75e1-128">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d75e1-128">Prerequisites</span></span>
* <span data-ttu-id="d75e1-129">Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-129">You must have an Azure subscription.</span></span> <span data-ttu-id="d75e1-130">아직 없으면 [Azure 무료 평가판을 다운로드하세요](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d75e1-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d75e1-131">다음 절차를 수행 하는 Azure HDInsight 3.4 Spark 1.6 클러스터 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="d75e1-132">hello 지침을 참조 하는 클러스터 toocreate [시작: Azure HDInsight의 Apache Spark 만들기](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="d75e1-133">Hello에 hello 클러스터 유형 및 버전 설정 **클러스터 유형 선택** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="d75e1-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![HDInsight 클러스터 형식 구성](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="d75e1-135">Hello NYC 택시 여행 데이터 tooexecute hello Spark 클러스터에서 Jupyter 노트북에서 코드가 하는 방식에 대 한 지침에 대 한 설명에서 hello 관련 섹션을 참조 하세요. [개요의 데이터 과학 Azure HDInsight의 Spark를 사용 하 여](machine-learning-data-science-spark-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="d75e1-136">Hello Spark 클러스터에서 Jupyter 노트북에서 Scala 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="d75e1-137">Hello Azure 포털에서에서 Jupyter 노트북을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="d75e1-138">동영상이 대시보드에서 hello Spark 클러스터를 찾아 클릭 하면 클러스터에 대 한 tooenter hello 관리 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="d75e1-139">그런 다음 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북** tooopen hello 노트북 hello Spark 클러스터와 연결 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![클러스터 대시보드 및 Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="d75e1-141">https://&lt;clustername&gt;.azurehdinsight.net/jupyter에서 Jupyter Notebook에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="d75e1-142">대체 *clustername* 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="d75e1-143">관리자 계정 tooaccess hello Jupyter 노트북 hello 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Hello 클러스터 이름을 사용 하 여 tooJupyter 전자 필기장 이동](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="d75e1-145">선택 **Scala** toosee PySpark API를 사용 하 여 hello 미리 전자 필기장의 몇 가지 예에 있는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="d75e1-146">Spark 항목의이 도구 모음에서 사용할 수 없으면 hello 코드 샘플이 포함 되어 있는 Scala.ipynb 전자 필기장을 사용 하 여 탐색 모델링 및 점수 매기기 hello [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="d75e1-147">Spark 클러스터에서 GitHub toohello Jupyter 노트북 서버에서 직접 hello 노트북을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="d75e1-148">Jupyter 홈 페이지에서 클릭 hello **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="d75e1-149">Hello 파일 탐색기에서 hello Scala 전자 필기장의 hello GitHub (원시 콘텐츠) URL을 붙여 넣고 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="d75e1-150">hello Scala 노트북 hello url에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="d75e1-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="d75e1-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="d75e1-152">설정: 사전 설정 Spark 및 Hive 컨텍스트, Spark 매직 및 Spark 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d75e1-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="d75e1-153">사전 설정 Spark 및 Hive 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="d75e1-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="d75e1-154">hello Spark 커널 Jupyter 노트북에 제공 되는 미리 설정 된 컨텍스트 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="d75e1-155">Hello 응용 프로그램을 개발 하는 작업을 시작 하기 전에 tooexplicitly 집합 hello Spark 또는 Hive 컨텍스트 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="d75e1-156">hello 미리 설정 된 컨텍스트는:</span><span class="sxs-lookup"><span data-stu-id="d75e1-156">hello preset contexts are:</span></span>

* <span data-ttu-id="d75e1-157">`sc` </span><span class="sxs-lookup"><span data-stu-id="d75e1-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="d75e1-158">`sqlContext` </span><span class="sxs-lookup"><span data-stu-id="d75e1-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="d75e1-159">Spark 매직</span><span class="sxs-lookup"><span data-stu-id="d75e1-159">Spark magics</span></span>
<span data-ttu-id="d75e1-160">hello Spark 커널 제공 일부 미리 정의 된 "마법"으로 호출할 수 있는 특수 명령을 `%%`합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="d75e1-161">두 명령은 두 hello 다음 코드 샘플에에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="d75e1-162">`%%local`다음 줄의 hello 코드는 로컬로 실행 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="d75e1-163">hello 코드가 유효한 Scala 코드 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="d75e1-164">`%%sql -o <variable name>` `sqlContext`에 대해 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="d75e1-165">경우 hello `-o` 매개 변수를 전달, hello 쿼리의 hello 결과 hello에서 유지 되 `%%local` Spark 데이터 프레임으로 Scala 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="d75e1-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="d75e1-166">호출 하면 Jupyter 노트북 및의 미리 정의 된 hello 커널에 대 한 자세한 내용은 "magics"는에 대 한 `%%` (예를 들어 `%%local`), 참조 [HDInsight Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 클러스터에 HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="d75e1-167">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="d75e1-167">Import libraries</span></span>
<span data-ttu-id="d75e1-168">Spark hello, MLlib, 및 다른 라이브러리 코드 다음 hello를 사용 하 여 필요 합니다를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="d75e1-169">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="d75e1-169">Data ingestion</span></span>
<span data-ttu-id="d75e1-170">hello hello 데이터 과학 프로세스의에서 첫 번째 단계는 원하는 tooanalyze tooingest hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="d75e1-171">데이터 탐색 및 모델링 환경에 상주 하 시스템 또는 외부 원본에서 hello 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="d75e1-172">이 문서에서는 hello 데이터 수집 hello 택시 여행 및 요금 파일 (.tsv 파일으로 저장 됨)의 조인 된 0.1% 샘플을입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="d75e1-173">hello 데이터 탐색 및 모델링 환경은 Spark입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="d75e1-174">이 섹션에는 일련의 작업을 수행 하는 hello 코드 toocomplete hello가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="d75e1-175">데이터 및 모델 저장소에 대한 디렉터리 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="d75e1-176">Hello (.tsv 파일으로 저장 됨)는 입력된 데이터 집합에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="d75e1-177">Hello 데이터 및 정리 hello 데이터에 대 한 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="d75e1-178">정리된 데이터 프레임을 만들고 메모리에 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="d75e1-179">SQLContext의 임시 테이블로 hello 데이터를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="d75e1-180">Hello 테이블을 쿼리 하 한을 데이터 프레임으로 hello 결과 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="d75e1-181">Azure Blob 저장소의 저장소 위치에 대한 디렉터리 경로 설정</span><span class="sxs-lookup"><span data-stu-id="d75e1-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="d75e1-182">Spark 읽고 tooAzure Blob 저장소를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="d75e1-183">Spark tooprocess 기존 기존 데이터를 사용 및 다음 Blob 저장소에 hello 결과 다시 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="d75e1-184">tooproperly 필요한 toosave 모델 또는 Blob 저장소의 파일 hello 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="d75e1-185">Hello 기본 컨테이너 참조로 시작 하는 경로 사용 하 여 toohello Spark 클러스터를 연결 `wasb:///`합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="d75e1-186">`wasb://`를 사용하여 다른 위치를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="d75e1-187">hello 다음 코드 샘플 hello의 위치를 지정 hello 입력된 데이터 toobe 읽기 및 hello 경로 tooBlob 저장소 연결 된 toohello Spark 클러스터를 hello 모델을 저장할 위치.</span><span class="sxs-lookup"><span data-stu-id="d75e1-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="d75e1-188">데이터 가져오기는 RDD 만들고 toohello 스키마에 따라 데이터 프레임을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
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

    # CAST VARIABLES ACCORDING toohello SCHEMA
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

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d75e1-189">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-189">**Output:**</span></span>

<span data-ttu-id="d75e1-190">시간 toorun hello 셀: 8 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="d75e1-191">Hello 테이블을 쿼리하고 결과 데이터 프레임에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="d75e1-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="d75e1-192">다음을 요금, 승객, 및; tip 데이터에 대 한 쿼리 hello 테이블 손상 및 외부 데이터; 필터링 여러 행을 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="d75e1-193">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-193">**Output:**</span></span>

| <span data-ttu-id="d75e1-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="d75e1-194">fare_amount</span></span> | <span data-ttu-id="d75e1-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="d75e1-195">passenger_count</span></span> | <span data-ttu-id="d75e1-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="d75e1-196">tip_amount</span></span> | <span data-ttu-id="d75e1-197">tipped</span><span class="sxs-lookup"><span data-stu-id="d75e1-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="d75e1-198">13.5</span><span class="sxs-lookup"><span data-stu-id="d75e1-198">13.5</span></span> |<span data-ttu-id="d75e1-199">1.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-199">1.0</span></span> |<span data-ttu-id="d75e1-200">2.9</span><span class="sxs-lookup"><span data-stu-id="d75e1-200">2.9</span></span> |<span data-ttu-id="d75e1-201">1.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-201">1.0</span></span> |
|        <span data-ttu-id="d75e1-202">16.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-202">16.0</span></span> |<span data-ttu-id="d75e1-203">2.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-203">2.0</span></span> |<span data-ttu-id="d75e1-204">3.4</span><span class="sxs-lookup"><span data-stu-id="d75e1-204">3.4</span></span> |<span data-ttu-id="d75e1-205">1.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-205">1.0</span></span> |
|        <span data-ttu-id="d75e1-206">10.5</span><span class="sxs-lookup"><span data-stu-id="d75e1-206">10.5</span></span> |<span data-ttu-id="d75e1-207">2.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-207">2.0</span></span> |<span data-ttu-id="d75e1-208">1.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-208">1.0</span></span> |<span data-ttu-id="d75e1-209">1.0</span><span class="sxs-lookup"><span data-stu-id="d75e1-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="d75e1-210">데이터 탐색 및 시각화</span><span class="sxs-lookup"><span data-stu-id="d75e1-210">Data exploration and visualization</span></span>
<span data-ttu-id="d75e1-211">Hello 데이터 Spark 가져올 후 hello hello 데이터 과학 프로세스의에서 다음 단계는 toogain hello 데이터 탐색 및 시각화를 통해 더 깊이 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="d75e1-212">이 섹션에서는 SQL 쿼리를 사용 하 여 hello 택시 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="d75e1-213">그런 다음 데이터 프레임 tooplot에 hello 결과 가져오기 hello Jupyter의 hello 자동 시각화 기능을 사용 하 여 대상 변수 및 시각적 검사 하기 위해 잠재 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="d75e1-214">로컬 및 SQL 매직 tooplot 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d75e1-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="d75e1-215">기본적으로 Jupyter 노트북에서 실행 하는 모든 코드 조각의 hello 출력은 hello 작업자 노드에 유지 되는 hello 세션의 hello 컨텍스트 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="d75e1-216">Toosave 여행 toohello 작업자 노드 모든 계산을 위한 고 모든 프로그램 계산 hello Jupyter 서버 노드 (즉, hello 헤드 노드)에서 로컬로 사용할 수 없으면 필요한 데이터를 hello, hello를 사용할 수 있습니다 `%%local` toorun hello 코드 매직 Jupyter 서버 hello에 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="d75e1-217">**SQL 매직**(`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="d75e1-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="d75e1-218">HDInsight Spark 커널 hello SQLContext에 대 한 쉬운 인라인 HiveQL 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="d75e1-219">hello (`-o VARIABLE_NAME`) 인수 hello Jupyter 서버의 팬더 데이터 프레임으로 hello 출력 hello SQL 쿼리를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="d75e1-220">이 hello 로컬 모드에서 제공 된다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="d75e1-221">`%%local` **매직**.</span><span class="sxs-lookup"><span data-stu-id="d75e1-221">`%%local` **magic**.</span></span> <span data-ttu-id="d75e1-222">hello `%%local` 매직 hello 코드에서 로컬로 실행 hello Jupyter 서버 hello hello HDInsight 클러스터의 헤드 노드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="d75e1-223">일반적으로 사용 `%%local` hello와 함께에서 매직 `%%sql` hello로 매직 `-o` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="d75e1-224">hello `-o` 매개 변수는 hello SQL 쿼리를 로컬로 hello 출력을 유지 했다가 `%%local` 매직 hello 다음 코드 조각 toorun 로컬로 유지 되는 hello SQL 쿼리의 hello 출력에 대해 로컬로 집합이 트리거할지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="d75e1-225">SQL을 사용 하 여 hello 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-225">Query hello data by using SQL</span></span>
<span data-ttu-id="d75e1-226">이 쿼리는 hello 택시 trips 요금 금액, 승객 횟수와 팁 크기를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="d75e1-227">코드 다음 hello, hello `%%local` 매직 sqlResults 로컬 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="d75e1-228">Matplotlib를 사용 하 여 sqlResults tooplot를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="d75e1-229">로컬 매직은 이 문서에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="d75e1-230">데이터 집합이 큰 경우 toocreate 데이터 프레임의 로컬 메모리에 맞출 수 있는 샘플 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d75e1-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="d75e1-231">Hello 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="d75e1-231">Plot hello data</span></span>
<span data-ttu-id="d75e1-232">로컬 컨텍스트에서 팬더 데이터 프레임으로 hello 데이터 프레임은 후 Python 코드를 사용 하 여 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="d75e1-233">hello Spark 커널 hello 코드를 실행 한 후 SQL (HiveQL) 쿼리의 hello 출력을 자동으로 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="d75e1-234">여러 형식의 시각화 요소 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="d75e1-235">테이블</span><span class="sxs-lookup"><span data-stu-id="d75e1-235">Table</span></span>
* <span data-ttu-id="d75e1-236">원형</span><span class="sxs-lookup"><span data-stu-id="d75e1-236">Pie</span></span>
* <span data-ttu-id="d75e1-237">꺾은선형</span><span class="sxs-lookup"><span data-stu-id="d75e1-237">Line</span></span>
* <span data-ttu-id="d75e1-238">영역</span><span class="sxs-lookup"><span data-stu-id="d75e1-238">Area</span></span>
* <span data-ttu-id="d75e1-239">가로 막대형</span><span class="sxs-lookup"><span data-stu-id="d75e1-239">Bar</span></span>

<span data-ttu-id="d75e1-240">Hello 코드 tooplot hello 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-240">Here's hello code tooplot hello data:</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="d75e1-241">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-241">**Output:**</span></span>

![팁 금액 히스토그램](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![승객 수에 따른 여정 수](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![금액으로 녀건 금액](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="d75e1-245">기능을 만들고 변환한 후 모델링 함수에 입력하기 위한 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="d75e1-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="d75e1-246">한 Spark ML 및 MLlib 트리 기반 모델링 기능을 해야 tooprepare 대상과 기능 다양 한 범주화, 인덱싱, 인코딩 하나 핫 및 벡터화 같은 기술 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="d75e1-247">이 섹션의 hello 프로시저 toofollow 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="d75e1-248">시간을 트래픽 시간 버킷으로 **범주화** 하여 새로운 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="d75e1-249">적용 **인덱싱 및 인코딩 하나 핫** toocategorical 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="d75e1-250">**샘플 및 분할 데이터 집합을 hello** 학습 및 테스트 분수를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="d75e1-251">**학습 변수 및 기능을 지정**하고, 인덱싱되었거나 원 핫 인코딩된 학습 및 테스팅 입력 레이블이 지정된 지점 RDD(탄력성 분산 데이터 집합) 또는 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="d75e1-252">자동으로 **를 분류 하 고 기능 및 대상 벡터화** toouse 기계 학습 모델에 대 한 입력으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="d75e1-253">시간을 트래픽 시간 버킷으로 범주화하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="d75e1-254">이 코드 toocreate 트래픽 시간에 시간을 범주화 하 여 새로운 기능 팅 하는 방법 및 toocache 메모리에 결과 데이터 프레임을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="d75e1-255">RDDs 및 데이터 프레임 반복적으로 사용 되 면 tooimproved 실행 시간 연결 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="d75e1-256">그에 따라 시 다음 절차를 수행 하는 hello에 여러 단계에서 RDDs 및 데이터 프레임을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="d75e1-257">범주 기능 인덱싱 및 원 핫 인코딩</span><span class="sxs-lookup"><span data-stu-id="d75e1-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="d75e1-258">hello 모델링 하 고 범주 입력된 데이터 toobe 기능과 인덱싱된 또는 이전 toouse 인코딩된 MLlib의 기능 필요를 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="d75e1-259">이 섹션에서는 tooindex 하거나 함수를 모델링 하는 hello에 대 한 입력에 대 한 범주 기능 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="d75e1-260">Tooindex 또는 hello 모델에 따라 다양 한 방법으로 모델을 인코딩할 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="d75e1-261">예를 들어 로지스틱 및 선형 회귀 모델에는 원 핫 인코딩이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="d75e1-262">예를 들어 세 개의 범주가 있는 기능을 세 개의 기능 열로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="d75e1-263">각 열에는 0 또는 1 관찰의 hello 범주에 따라 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="d75e1-264">MLlib 제공 hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 하나 핫 인코딩에 대 한 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="d75e1-265">이 인코더의 레이블 인덱스 tooa 벡터 열을 이진으로 최대 단일 한 값 열을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="d75e1-266">이 인코딩을 사용 하 여 로지스틱 회귀와 같은 숫자 중요 기능을 예상 하는 알고리즘에 적용 된 toocategorical 기능 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="d75e1-267">여기에 4 개의 변수 tooshow 예제는 문자 문자열을 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="d75e1-268">평일과 같이 숫자 값으로 표현되는 기타 변수는 범주 변수로 인덱싱할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="d75e1-269">인덱싱에는 `StringIndexer()` 함수를 사용하고 원 핫 인코딩에는 MLlib의 `OneHotEncoder()` 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="d75e1-270">다음은 코드 tooindex hello와 범주 기능 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-270">Here is hello code tooindex and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
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

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d75e1-271">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-271">**Output:**</span></span>

<span data-ttu-id="d75e1-272">시간 toorun hello 셀: 4 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="d75e1-273">샘플 및 분할 데이터 집합 학습 및 테스트 소수에 hello</span><span class="sxs-lookup"><span data-stu-id="d75e1-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="d75e1-274">이 코드는 hello (이 예제에서 25%) 데이터의 무작위 샘플링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="d75e1-275">샘플링 hello 데이터 집합의 toohello 크기 때문에이 예제에 필요 하지는 않지만 hello 문서에서는 어떻게 알 수 있도록을 샘플링할 수 있습니다 어떻게 toouse 필요할 때 고유한 문제에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="d75e1-276">샘플이 큰 경우 모델을 학습하는 동안 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="d75e1-277">다음으로, 교육 부품 (이 예제의 75%) 및 테스트를 hello 샘플을 분할 분류 및 회귀 모델링에 (이 예제에서 25%) toouse 부 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="d75e1-278">학습 중 사용 되는 tooselect 교차 유효성 검사 접기 수 있는 ("rand" 열)에 (0과 1) 사이의 난수 tooeach 행을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

    # RECORD hello START TIME
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

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d75e1-279">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-279">**Output:**</span></span>

<span data-ttu-id="d75e1-280">시간 toorun hello 셀: 2 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="d75e1-281">학습 변수 및 기능 지정, 인덱싱되었거나 원 핫 인코딩된 학습 및 테스팅 입력 레이블이 지정된 지점 RDD 또는 데이터 프레임 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="d75e1-282">이 섹션에는 tooindex 범주 텍스트 데이터는 레이블이 지정 된 소수점 데이터 형식 및 tootrain 및 테스트 MLlib 로지스틱 회귀 및 다른 분류 모델에는 사용할 수 있도록 인코딩 방식을 보여 주는 코드가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="d75e1-283">레이블이 지정된 지점 개체는 대부분 MLlib의 기계 학습 알고리즘에서 입력 데이터로 필요한 방식으로 형식이 지정된 RDD입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="d75e1-284">[레이블이 지정된 지점](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 은 레이블/응답과 연결된 로컬 벡터, 밀도 또는 스파스입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="d75e1-285">이 코드에서는 hello 대상 (종속) 변수 및 hello 기능 toouse tootrain 모델을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="d75e1-286">그런 후 인덱싱되었거나 원 핫 인코딩된 학습 및 테스팅 입력 레이블이 지정된 지점 RDD 또는 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d75e1-287">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-287">**Output:**</span></span>

<span data-ttu-id="d75e1-288">시간 toorun hello 셀: 4 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="d75e1-289">자동으로 분류 하 고 기계 학습 모델에 대 한 입력으로 기능 및 대상 toouse 벡터화</span><span class="sxs-lookup"><span data-stu-id="d75e1-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="d75e1-290">Spark ML toocategorize hello 대상과 기능 toouse 트리 기반 모델링 기능에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="d75e1-291">hello 코드는 두 가지 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="d75e1-292">임계값 값 0.5 사용 하 여 0 또는 0과 1 사이의 tooeach 데이터 요소 1의 값을 할당 하 여 분류에 대 한 이진 대상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="d75e1-293">기능을 자동으로 범주화합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-293">Automatically categorizes features.</span></span> <span data-ttu-id="d75e1-294">모든 기능에 대 한 고유 숫자 값의 hello 수가 32 보다 작은 경우, 해당 기능 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="d75e1-295">다음은이 두 가지 작업에 대 한 hello 코드가입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-295">Here's hello code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

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

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="d75e1-296">이진 분류 모델: 팁이 지불되었는지 예측</span><span class="sxs-lookup"><span data-stu-id="d75e1-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="d75e1-297">이 섹션에서는 세 가지 유형의 이진 분류 모델 toopredict 팁을 지불 해야 할지 여부를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="d75e1-298">A **로지스틱 회귀 모델** Spark ML hello를 사용 하 여 `LogisticRegression()` 함수</span><span class="sxs-lookup"><span data-stu-id="d75e1-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="d75e1-299">A **임의 포리스트 분류 모델** Spark ML hello를 사용 하 여 `RandomForestClassifier()` 함수</span><span class="sxs-lookup"><span data-stu-id="d75e1-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="d75e1-300">A **부스트 그라데이션 트리 분류 모델** MLlib hello를 사용 하 여 `GradientBoostedTrees()` 함수</span><span class="sxs-lookup"><span data-stu-id="d75e1-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="d75e1-301">로지스틱 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-301">Create a logistic regression model</span></span>
<span data-ttu-id="d75e1-302">다음으로, Spark ML hello를 사용 하 여 로지스틱 회귀 모델을 만들 `LogisticRegression()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="d75e1-303">일련의 단계에는 코드를 작성 하는 hello 모델을 만들면:</span><span class="sxs-lookup"><span data-stu-id="d75e1-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="d75e1-304">**Hello 모델 학습** 하나의 매개 변수 집합을 사용 하 여 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="d75e1-305">**Hello 모델 평가** 메트릭 사용 하 여 테스트 데이터 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="d75e1-306">**Hello 모델 저장** 나중에 사용에 대 한 Blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="d75e1-307">**Hello 모델 점수 매기기** 테스트 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="d75e1-308">**Hello 결과 출력** 특징 (ROC) 곡선을 운영 하는 수신기가 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="d75e1-309">이 절차에 대 한 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-309">Here's hello code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="d75e1-310">로드 하 고 점수를 매길 hello 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-310">Load, score, and save hello results.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="d75e1-311">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-311">**Output:**</span></span>

<span data-ttu-id="d75e1-312">ROC on test data = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="d75e1-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="d75e1-313">로컬 팬더 데이터 프레임 tooplot hello ROC 곡선에 Python을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


<span data-ttu-id="d75e1-314">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-314">**Output:**</span></span>

![팁 여부 ROC 곡선](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="d75e1-316">임의 포리스트 분류 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-316">Create a random forest classification model</span></span>
<span data-ttu-id="d75e1-317">다음으로, Spark ML hello를 사용 하 여 임의 포리스트 분류 모델 만들기 `RandomForestClassifier()` 함수를 한 다음 테스트 데이터에서 hello 모델을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="d75e1-318">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-318">**Output:**</span></span>

<span data-ttu-id="d75e1-319">ROC on test data = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="d75e1-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="d75e1-320">GBT 분류 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-320">Create a GBT classification model</span></span>
<span data-ttu-id="d75e1-321">다음으로 MLlib의를 사용 하 여 GBT 분류 모델을 만들 `GradientBoostedTrees()` 함수를 한 다음 테스트 데이터에서 hello 모델을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="d75e1-322">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-322">**Output:**</span></span>

<span data-ttu-id="d75e1-323">Area under ROC curve: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="d75e1-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="d75e1-324">회귀 모델: 팁 금액 예측</span><span class="sxs-lookup"><span data-stu-id="d75e1-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="d75e1-325">이 섹션에서는 두 가지 유형의 회귀 모델 toopredict hello 팁 amount 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="d75e1-326">A **정규화 된 선형 회귀 모델** Spark ML hello를 사용 하 여 `LinearRegression()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="d75e1-327">Hello 모델을 저장 하 고 테스트 데이터에서 hello 모델 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="d75e1-328">A **그라데이션 승격 트리 회귀 모델** Spark ML hello를 사용 하 여 `GBTRegressor()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="d75e1-329">정칙 선형 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-329">Create a regularized linear regression model</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d75e1-330">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-330">**Output:**</span></span>

<span data-ttu-id="d75e1-331">시간 toorun hello 셀: 13 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-331">Time toorun hello cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="d75e1-332">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-332">**Output:**</span></span>

<span data-ttu-id="d75e1-333">R-sqr on test data = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="d75e1-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="d75e1-334">다음으로 쿼리 hello 테스트 결과 데이터 프레임 및 사용 하 여 AutoVizWidget 및 matplotlib toovisualize로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="d75e1-335">hello 코드 hello 쿼리 결과에서 로컬 데이터 프레임을 만들고 hello 데이터 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="d75e1-336">hello `%%local` 매직에서는 로컬 데이터 프레임을 `sqlResults`이며 matplotlib를 tooplot를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="d75e1-337">이 Spark 매직은 이 문서에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="d75e1-338">Hello 양의 데이터가 클 경우 toocreate 로컬 메모리에 들어갈 수 있는 데이터 프레임을 샘플 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="d75e1-339">Python matplotlib를 사용하여 도표를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-339">Create plots by using Python matplotlib.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="d75e1-340">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-340">**Output:**</span></span>

![팁 금액: 실제 및 예측](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="d75e1-342">GBT 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d75e1-342">Create a GBT regression model</span></span>
<span data-ttu-id="d75e1-343">Spark ML hello를 사용 하 여 GBT 회귀 모델을 만들 `GBTRegressor()` 함수를 한 다음 테스트 데이터에서 hello 모델을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="d75e1-344">[GBT](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (그라데이션 향상 트리)는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="d75e1-345">GBTs 학습 의사 결정 트리 반복적으로 toominimize 손실 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="d75e1-346">회귀 및 분류에 대해 GBT를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="d75e1-347">GBT는 범주 기능을 처리하고 기능 규모 결정을 요구하지 않으며 비선형 기능 상호 작용을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="d75e1-348">또한 다중 클래스 분류 설정에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="d75e1-349">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-349">**Output:**</span></span>

<span data-ttu-id="d75e1-350">Test R-sqr is: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="d75e1-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="d75e1-351">최적화를 위한 고급 모델링 유틸리티</span><span class="sxs-lookup"><span data-stu-id="d75e1-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="d75e1-352">이 섹션에서는 개발자가 모델 최적화를 위해 자주 사용하는 기계 학습 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="d75e1-353">특히, 매개 변수 스윕 작업 및 교차 유효성 검사를 사용하여 세 가지 다른 방식으로 기계 학습 모델을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="d75e1-354">Hello 데이터를 학습 및 유효성 검사 집합으로 분할 하 고, 학습 집합에서 하이퍼 매개 변수 비우기를 사용 하 여 hello 모델을 최적화 하며, 유효성 검사 집합 (선형 회귀)에 대해 평가</span><span class="sxs-lookup"><span data-stu-id="d75e1-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="d75e1-355">교차 유효성 검사 및 hyper-매개 변수 비우기 Spark ML CrossValidator 함수 (이진 분류)를 사용 하 여 사용 하 여 hello 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d75e1-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="d75e1-356">교차 유효성 검사 및 매개 변수 비우기를 수행에 대 한 사용자 지정 코드 toouse (선형 회귀) 하는 함수 및 매개 변수 집합을 학습 하는 모든 컴퓨터를 사용 하 여 hello 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d75e1-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="d75e1-357">**교차 유효성 검사** 은 얼마나 잘 알려진된 데이터 집합에서 학습 된 모델을 toopredict hello 기능 데이터 집합에 있는 것 학습 되지 않았습니다를 일반화 합니다를 평가 하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="d75e1-358">hello 일반 개념이이 기술은 알려진된 데이터의 데이터 집합에는 모델을 학습 하 고 그런 hello 해당 예측의 정확도 테스트 한 독립적인 데이터 집합에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="d75e1-359">데이터 집합 프로젝트로 toodivide 된 일반적인 구현 *k*-, 정리 및 다음 hello 접기 중 하나를 제외한 모든 문에 라운드 로빈 방식에서 hello 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="d75e1-360">**하이퍼 매개 변수 최적화** hello 문제가 하이퍼-매개 변수 집합을 학습 알고리즘에 대 한 독립적인 데이터 집합에 hello 알고리즘의 성능을 최적화의 hello 목표와 일반적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="d75e1-361">하이퍼-매개 변수는 hello 모델 학습 프로시저 밖에 서 지정 해야 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="d75e1-362">하이퍼 매개 변수 값에 대 한 가정을 hello 유연성과 hello 모델의 정확도 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="d75e1-363">의사 결정 트리 hello 필요한 깊이 및 hello 트리의 리프 수 같은 예를 들어, 하이퍼-매개 변수를을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="d75e1-364">SVM(지원 벡터 컴퓨터)은 오분류 페널티 조건을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="d75e1-365">호출 또한 toouse 그리드 검색 방법은 tooperform 하이퍼 매개 최적화에 많이 **매개 변수 비우기를**합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="d75e1-366">표 검색에서는 철저 한 검색이 hello 값 hello 매개 변수 하이퍼 공간 학습 알고리즘에 대 한 지정 된 하위 집합을 통해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="d75e1-367">교차 유효성 검사는 성능 메트릭 toosort hello hello 그리드 검색 알고리즘으로 생성 되는 최적의 결과 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="d75e1-368">하이퍼 매개 변수 비우기 교차 유효성 검사를 사용 하는 경우에 모델 tootraining 데이터에 과잉 맞춤이 다음과 같은 제한 문제를 도울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="d75e1-369">이러한 방식으로 hello 모델은 hello 용량 tooapply toohello 일반 집합이 학습 데이터는 hello에서 추출 된 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="d75e1-370">하이퍼 매개 변수 스윕 작업으로 선형 회귀 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d75e1-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="d75e1-371">다음으로 학습 및 유효성 검사 집합으로 데이터를 분할 사용 하 여 하이퍼-매개 변수 비우기 학습에 toooptimize hello 모델 설정 하 고 유효성 검사 집합 (선형 회귀)을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="d75e1-372">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-372">**Output:**</span></span>

<span data-ttu-id="d75e1-373">Test R-sqr is: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="d75e1-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="d75e1-374">교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용 하 여 hello 이진 분류 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d75e1-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="d75e1-375">이 섹션에서는 교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용 하 여 이진 분류 toooptimize 모델링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="d75e1-376">Spark ML hello를 사용 하 여이 `CrossValidator` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-376">This uses hello Spark ML `CrossValidator` function.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="d75e1-377">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-377">**Output:**</span></span>

<span data-ttu-id="d75e1-378">시간 toorun hello 셀: 33 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="d75e1-379">교차 유효성 검사 및 매개 변수 비우기를 수행에 대 한 사용자 지정 코드를 사용 하 여 hello 선형 회귀 모델 최적화</span><span class="sxs-lookup"><span data-stu-id="d75e1-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="d75e1-380">다음으로, 사용자 지정 코드를 사용 하 여 hello 모델을 최적화 하 고 가장 높은 정확도의 hello 조건을 사용 하 여 hello 최상의 모델 매개 변수를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="d75e1-381">그런 다음 hello 최종 모델, 테스트 데이터에서 hello 모델 평가 만들고 hello 모델 Blob 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="d75e1-382">마지막으로 hello 모델을 로드 하 고 테스트 데이터 점수와 정확도 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
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


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
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

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="d75e1-383">**출력:**</span><span class="sxs-lookup"><span data-stu-id="d75e1-383">**Output:**</span></span>

<span data-ttu-id="d75e1-384">시간 toorun hello 셀: 61 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="d75e1-385">Scala를 사용하여 Spark에서 빌드한 기계 학습 모델을 자동으로 사용</span><span class="sxs-lookup"><span data-stu-id="d75e1-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="d75e1-386">Azure의 hello 데이터 과학 프로세스를 구성 하는 hello 작업을 안내 하는 항목의 개요를 참조 하십시오. [팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="d75e1-387">[데이터 과학 프로세스 연습 팀](data-science-process-walkthroughs.md) hello 특정 시나리오에 대 한 hello 팀 데이터 과학 프로세스의에서 단계를 보여 주는 다른 종단 간 연습에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="d75e1-388">hello 연습도 방법을 toocombine 클라우드 및 온-프레미스 도구 및 워크플로 또는 파이프라인 toocreate에 서비스는 지능형 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="d75e1-389">[Spark 작성 기계 학습 모델 점수를 매깁니다.](machine-learning-data-science-spark-model-consumption.md) toouse Scala 코드 tooautomatically 로드 하 고 기계 학습 모델 Spark에 기본 제공 및 Azure Blob 저장소에 저장 된 새 데이터 집합 점수를 매깁니다. 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="d75e1-390">여기에 제공 하는 hello 지침에 따라 수 있으며 자동화 된 소비에 대 한이 문서의 Scala 코드로 hello Python 코드를 대체 단순히 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75e1-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

