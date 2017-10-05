---
title: "고급 Spark로 데이터 탐색 및 모델링 | Microsoft Docs"
description: "HDInsight Spark를 사용하여 데이터 탐색 및 학습 이진 분류를 수행하며 교차 유효성 검사 및 하이퍼 매개 변수 최적화를 사용하는 회귀 모델링을 수행합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: e6bf6bd3c905f077841ef166540337a251b91ad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="4d1e2-103">고급 Spark로 데이터 탐색 및 모델링</span><span class="sxs-lookup"><span data-stu-id="4d1e2-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="4d1e2-104">이 연습에서는 HDInsight Spark를 사용하여 데이터 탐색 및 학습 이진 분류를 수행하며 NYC Taxi Trip 및 요금 2013 데이터 집합 샘플에서 교차 유효성 검사 및 하이퍼 매개 변수 최적화를 사용하는 회귀 모델링을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="4d1e2-105">처리를 위한 HDInsight Spark 클러스터와 데이터 및 모델을 저장하는 Azure Blob을 사용하여 [데이터 과학 프로세스](http://aka.ms/datascienceprocess)의 단계를 종단 간 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="4d1e2-106">프로세스는 Azure 저장소 Blob에서 가져온 데이터를 탐색하고 시각화한 다음 데이터를 준비하여 예측 모델을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="4d1e2-107">Python은 솔루션을 코딩하고 관련 차트를 표시하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="4d1e2-108">이러한 모델은 Spark MLlib 도구 키트를 사용하여 이진 분류 및 회귀 모델링 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="4d1e2-109">**이진 분류** 작업은 여정에 대해 팁이 지불되었는지 여부를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="4d1e2-110">**회귀** 작업은 다른 팁 기능을 기반으로 하는 팁의 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="4d1e2-111">또한 모델링 단계에는 각 모델 유형을 학습, 평가 및 저장하는 방법을 보여주는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="4d1e2-112">이 항목에는 [Spark로 데이터 탐색 및 모델링](machine-learning-data-science-spark-data-exploration-modeling.md) 항목과 동일한 기본적인 내용이 일부 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="4d1e2-113">하지만 좀 더 "고급" 내용으로, 하이퍼 매개 변수 비우기와 교차 유효성 검사를 함께 사용하여 정확한 분류 및 회귀 모델을 최적으로 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="4d1e2-114">**CV(교차 유효성 검사)**는 알려진 데이터 집합에서 학습된 모델이 학습되지 않은 데이터 집합의 기능 예측을 얼마나 잘 일반화하는지 평가하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="4d1e2-115">여기에 사용된 일반적인 구현은 데이터 집합을 K 접기로 나눈 다음 접기 중 하나를 제외한 모든 접기에서 라운드 로빈 방식으로 모델을 학습하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="4d1e2-116">이 접기에서 모델을 테스트하는 데 사용되지 않은 독립 데이터 집합에 대해 모델을 테스트할 때 모델이 정확히 예측하는 기능이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="4d1e2-117">**하이퍼 매개 변수 최적화** 는 학습 알고리즘에 대한 하이퍼 매개 변수 집합을 선택하는 문제이며, 일반적으로 독립된 데이터 집합에서의 알고리즘 성능 측정값을 최적화하는 것을 목표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="4d1e2-118">**하이퍼 매개 변수** 는 모델 학습 절차 외부에서 지정해야 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="4d1e2-119">이러한 값에 대한 가정은 모델의 유연성 및 정확도에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="4d1e2-120">의사 결정 트리에는 원하는 깊이와 트리의 리프 수와 같은 하이퍼 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="4d1e2-121">SVM(Support Vector Machine)은 오분류 페널티 조건을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="4d1e2-122">여기에 사용된 하이퍼 매개 변수 최적화를 수행하는 일반적인 방법은 그리드 검색 또는 **매개 변수 비우기**입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="4d1e2-123">이 작업은 학습 알고리즘에 대해 지정된 하이퍼 매개 변수 공간 하위 집합 값을 통한 철저한 검색 수행으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="4d1e2-124">교차 유효성 검사는 그리드 검색 알고리즘에 의해 생성되는 최적의 결과를 분류하는 성능 메트릭을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="4d1e2-125">하이퍼 매개 변수 비우기와 함께 사용된 CV를 통해 데이터 학습 모델의 과잉 맞춤과 같은 문제를 제한하여 모델이 학습 데이터가 추출되는 일반 데이터 집합에 적용할 용량을 유지하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="4d1e2-126">사용하는 모델은 로지스틱 및 선형 회귀, 임의 포리스트, 그라데이션 향상된 트리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="4d1e2-127">[SGD로 선형 회귀](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 는 SGD(Stochastic Gradient Descent) 메서드를 사용하는 선형 회귀 모델이며 최적화 및 기능에 대해 크기를 조정하여 결재된 팁 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="4d1e2-128">[LBFGS로 로지스틱 회귀 분석](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) 또는 "로짓" 회귀는 종속 변수가 데이터 분류를 수행하는 범주인 경우 사용할 수 있는 회귀 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="4d1e2-129">LBFGS는 제한된 양의 컴퓨터 메모리를 사용하여 BFGS(Broyden–Fletcher–Goldfarb–Shanno) 알고리즘을 비슷하게 만들고 기계 학습에서 널리 사용되는 준 뉴턴 최적화 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="4d1e2-130">[임의 포리스트](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="4d1e2-131">즉, 과잉 맞춤의 위험을 줄이기 위해 많은 결정 트리를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="4d1e2-132">임의 포리스트는 회귀 및 분류에 사용되며 범주 기능을 처리하고 다중 클래스 분류 설정으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="4d1e2-133">기능 크기 조정을 필요로 하지 않으며 비선형 및 기능 상호 작용을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="4d1e2-134">임의 포리스트는 분류 및 회귀를 위해 매우 성공적인 기계 학습 모델 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="4d1e2-135">[GBT](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (그라데이션 승격 트리)는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="4d1e2-136">GBT는 기능 손실을 최소화하기 위해 결정 트리를 반복적으로 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="4d1e2-137">GBT는 회귀 및 분류에 사용되며 범주 기능을 처리하고 기능 크기 조정을 필요로 하지 않으며 비선형 및 기능 상호 작용을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="4d1e2-138">또한 다중 클래스 분류 설정에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="4d1e2-139">이진 분류 문제에 대한 CV 및 하이퍼 매개 변수 비우기를 사용하는 모델링 예제가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="4d1e2-140">더 간단한 예제(매개 변수 비우기 없음)가 회귀 작업에 대한 주요 토픽으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="4d1e2-141">하지만 부록에서는 선형 회귀에 대해 탄력적 net을 사용한 유효성 검사와 임의 포리스트 회귀에 대해 사용한 매개 변수 비우기가 있는 CV도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="4d1e2-142">**탄력적 net**은 L1 및 L2 메트릭을 선형으로 결합하는 선형 회귀 모델을 [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) 및 [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) 메서드의 페널티로 맞추기 위한 정칙 회귀 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="4d1e2-143">Spark MLlib 도구 키트가 큰 데이터 집합에서 작동하도록 디자인되었지만 여기서는 편의상 비교적 작은 샘플을 사용합니다(30Mb보다 작은 170,000개 행 즉, 원래 NYC 데이터 집합의 약 0.1%를 사용함).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="4d1e2-144">여기에 제공된 연습은 2개의 작업자 노드를 가진 HDInsight 클러스터에서 효율적으로 실행됩니다(약 10분 동안).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="4d1e2-145">동일한 코드를 약간만 수정하면 데이터를 메모리에 캐시하고 클러스터 크기를 변경하도록 적절하게 수정하여 더 큰 데이터 집합을 처리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="4d1e2-146">설정: Spark 클러스터 및 Notebook</span><span class="sxs-lookup"><span data-stu-id="4d1e2-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="4d1e2-147">설치 단계와 코드는 HDInsight Spark 1.6을 사용하는 이 연습에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="4d1e2-148">하지만 Jupyter Notebook은 HDInsight Spark 1.6과 Spark 2.0 클러스터 둘 다에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="4d1e2-149">노트북과 이에 연결된 링크의 설명은 이들을 포함하는 GitHub 리포지토리의 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="4d1e2-150">그뿐 아니라 여기에 있는 코드와 연결된 Notebook에 있는 코드는 일반적이므로 아무 Spark 클러스터에서나 작동할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="4d1e2-151">HDInsight Spark를 사용하지 않는 경우 클러스터 설치 및 관리 단계가 여기에 나오는 내용과 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="4d1e2-152">편의를 위해, Jupyter Notebook 서버의 pyspark 커널에서 실행되는 Spark 1.6 및 2.0용 Jupyter Notebook에 연결된 링크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="4d1e2-153">Spark 1.6 Notebook</span><span class="sxs-lookup"><span data-stu-id="4d1e2-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="4d1e2-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Notebook #1의 항목 및 하이퍼 매개 변수 조정 및 교차 유효성 검사를 사용하는 모델 개발을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="4d1e2-155">Spark 2.0 Notebook</span><span class="sxs-lookup"><span data-stu-id="4d1e2-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="4d1e2-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): 이 파일은 Spark 2.0 클러스터에서 데이터 탐색, 모델링, 점수 매기기를 수행하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="4d1e2-157">설정: 저장소 위치, 라이브러리 및 사전 설정 Spark 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="4d1e2-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="4d1e2-158">Spark는 Azure 저장소 Blob(WASB라고도 함)를 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="4d1e2-159">따라서 Spark 및 WASB에 다시 저장된 결과를 사용하여 해당 저장소에 저장된 기존 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="4d1e2-160">모델 또는 파일을 WASB에 저장하려면 경로를 올바르게 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="4d1e2-161">"wasb///"로 시작하는 경로를 사용하여 Spark 클러스터에 연결된 기본 컨테이너를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="4d1e2-162">다른 위치를 “wasb://”에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="4d1e2-163">WASB의 저장소 위치에 대한 디렉터리 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="4d1e2-164">다음 코드 샘플은 읽을 데이터의 위치 및 모델 출력을 저장할 모델 저장소 디렉터리에 대한 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="4d1e2-165">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-165">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="4d1e2-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="4d1e2-167">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-167">Import libraries</span></span>
<span data-ttu-id="4d1e2-168">다음 코드를 사용하여 필요한 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-168">Import necessary libraries with the following code:</span></span>

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="4d1e2-169">미리 설정된 Spark 컨텍스트 및 PySpark 매직</span><span class="sxs-lookup"><span data-stu-id="4d1e2-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="4d1e2-170">Jupyter Notebook과 함께 제공되는 PySpark 커널에는 사전 설정 컨텍스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="4d1e2-171">따라서 개발 중인 응용 프로그램으로 작업을 시작하기 전에 Spark 또는 Hive 컨텍스트를 명시적으로 설정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="4d1e2-172">이러한 컨텍스트는 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-172">These contexts are available for you by default.</span></span> <span data-ttu-id="4d1e2-173">이러한 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-173">These contexts are:</span></span>

* <span data-ttu-id="4d1e2-174">sc - Spark용</span><span class="sxs-lookup"><span data-stu-id="4d1e2-174">sc - for Spark</span></span> 
* <span data-ttu-id="4d1e2-175">sqlContext - Hive용</span><span class="sxs-lookup"><span data-stu-id="4d1e2-175">sqlContext - for Hive</span></span>

<span data-ttu-id="4d1e2-176">PySpark 커널은 특수 명령인 일부 미리 정의된 "매직"을 제공하며 이러한 매직은 %%를 사용하여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="4d1e2-177">이러한 코드 샘플에 사용되는 다음과 같은 두 가지 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="4d1e2-178">**%%local** 다음 줄의 코드는 로컬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="4d1e2-179">코드는 유효한 Python 코드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="4d1e2-180">**%%sql -o <variable name>** sqlContext에 대해 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="4d1e2-181">-o 매개 변수가 전달된 경우 쿼리 결과가 %%local Python 컨텍스트에서 Pandas 데이터 프레임으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="4d1e2-182">Jupyter Notebook의 커널 및 제공되는 미리 정의된 "매직"에 대한 자세한 내용은 [HDInsight의 HDInsight Spark Linux 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="4d1e2-183">공용 blob에서 데이터 수집:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="4d1e2-184">데이터 과학 프로세스의 첫 번째 단계는 원본에서 분석할 데이터를 수집하여 데이터 탐색 및 모델링 환경에 상주시키는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="4d1e2-185">이 환경은 이 연습에서 Spark입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="4d1e2-186">이 섹션은 일련의 작업을 완료하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="4d1e2-187">모델링할 데이터 샘플 수집</span><span class="sxs-lookup"><span data-stu-id="4d1e2-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="4d1e2-188">입력 데이터 집합 읽기(.tsv 파일로 저장됨)</span><span class="sxs-lookup"><span data-stu-id="4d1e2-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="4d1e2-189">데이터 포맷 및 정리</span><span class="sxs-lookup"><span data-stu-id="4d1e2-189">format and clean the data</span></span>
* <span data-ttu-id="4d1e2-190">메모리에 개체 만들기 및 캐시(RDD 또는 데이터 프레임)</span><span class="sxs-lookup"><span data-stu-id="4d1e2-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="4d1e2-191">SQL 컨텍스트에 임시 테이블로 등록</span><span class="sxs-lookup"><span data-stu-id="4d1e2-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="4d1e2-192">데이터 수집에 대한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-192">Here is the code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-193">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-193">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-194">위의 셀을 실행하는 데 걸린 시간: 276.62초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="4d1e2-195">데이터 탐색 및 시각화</span><span class="sxs-lookup"><span data-stu-id="4d1e2-195">Data exploration & visualization</span></span>
<span data-ttu-id="4d1e2-196">데이터를 Spark로 가져오면 데이터 과학 프로세스의 다음 단계에서 탐색 및 시각화를 통해 데이터를 더 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="4d1e2-197">이 섹션에서는 SQL 쿼리를 사용하여 Taxi 데이터를 검사하고 시각적 조사에 대한 대상 변수 및 잠재 기능을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="4d1e2-198">특히, Taxi Trip에서 승객 수의 빈도, 팁 금액의 빈도 및 지불 금액 및 형식에 따른 팁의 변화를 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="4d1e2-199">Taxi Trip의 샘플에서 승객 수 빈도의 히스토그램을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="4d1e2-200">이 코드와 후속 코드 조각은 샘플을 쿼리하는 데 SQL 매직을 사용하고 데이터를 그리는 데 로컬 매직을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="4d1e2-201">**SQL 매직(`%%sql`)** HDInsight PySpark 커널은 sqlContext에 대해 간편한 인라인 HiveQL 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="4d1e2-202">(-o VARIABLE_NAME) 인수는 Jupyter 서버에서 Pandas 데이터 프레임으로 SQL 쿼리의 출력을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="4d1e2-203">즉, 로컬 모드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="4d1e2-204">**`%%local` 매직** 은 HDInsight 클러스터의 헤드 노드인 Jupyter 서버에서 코드를 로컬로 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="4d1e2-205">일반적으로 `%%sql -o` 매직을 사용하여 쿼리를 실행한 후에 `%%local`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="4d1e2-206">-o 매개 변수는 SQL 쿼리 출력을 로컬로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="4d1e2-207">그런 다음 `%%local` 매직은 로컬로 유지된 SQL 쿼리 출력에 대해 다음 코드 조각 집합이 로컬로 실행되도록 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="4d1e2-208">코드를 실행한 후 출력이 자동으로 시각화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="4d1e2-209">이 쿼리는 승객 수에 따라 여정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="4d1e2-210">이 코드는 쿼리 출력에서 로컬 데이터 프레임을 만들고 데이터를 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="4d1e2-211">`%%local` 매직은 로컬 데이터 프레임 `sqlResults`를 만드는데, 이것은 matplotlib로 그리는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d1e2-212">이 PySpark 매직은 이 연습에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="4d1e2-213">데이터 양이 많은 경우 로컬 메모리에 맞게 데이터 프레임을 만들도록 샘플링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="4d1e2-214">다음은 승객 수에 따라 여정을 그리는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="4d1e2-215">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-215">**OUTPUT**</span></span>

![승객 수에 따른 여정 빈도](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="4d1e2-217">Notebook의 **형식** 메뉴 버튼을 사용하여 다양한 시각화 형식(테이블, 원형, 꺾은선형, 영역 또는 막대) 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="4d1e2-218">막대 그리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="4d1e2-219">승객 수 및 요금 금액에 따라 팁 금액이 어떻게 달라지는지와 팁 금액에 대한 히스토그램을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="4d1e2-220">SQL 쿼리를 사용하여 데이터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-220">Use a SQL query to sample data..</span></span>

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


<span data-ttu-id="4d1e2-221">이 코드 셀에서는 SQL 쿼리를 사용하여 3가지로 데이터 그리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="4d1e2-222">**출력:**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-222">**OUTPUT:**</span></span> 

![팁 금액 분포](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![승객 수에 따른 여정 수](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![금액에 따른 팁 금액](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="4d1e2-226">모델링에 대한 기능 엔지니어링, 변환 및 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="4d1e2-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="4d1e2-227">이 섹션에서는 기계 학습 모델링에 사용할 데이터를 준비하는 데 사용되는 프로시저에 대한 코드를 설명하고 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="4d1e2-228">다음 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="4d1e2-229">시간을 트래픽 시간 bin으로 분할하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="4d1e2-230">범주 기능 인덱스 및 원 핫 인코딩(one-hot encoding)</span><span class="sxs-lookup"><span data-stu-id="4d1e2-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="4d1e2-231">기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="4d1e2-232">데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분할합니다</span><span class="sxs-lookup"><span data-stu-id="4d1e2-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="4d1e2-233">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="4d1e2-233">Feature scaling</span></span>
* <span data-ttu-id="4d1e2-234">메모리에서 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="4d1e2-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="4d1e2-235">트래픽 시간을 bin으로 분할하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="4d1e2-236">이 코드는 트래픽 시간을 bin으로 분할하여 새로운 기능을 만드는 방법 및 메모리에 결과 데이터 프레임을 캐시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="4d1e2-237">RDD(복원력 있는 분산된 데이터 집합) 및 데이터 프레임을 반복해서 사용하는 경우 캐시하면 실행 시간이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="4d1e2-238">따라서 RDD 및 데이터 프레임을 연습의 여러 단계에서 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="4d1e2-239">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-239">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-240">126050</span><span class="sxs-lookup"><span data-stu-id="4d1e2-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="4d1e2-241">범주 기능 인덱스 및 원 핫 인코딩(one-hot encoding)</span><span class="sxs-lookup"><span data-stu-id="4d1e2-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="4d1e2-242">이 섹션에는 모델링 기능에 입력에 대한 범주 기능을 인덱싱하거나 인코딩하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="4d1e2-243">MLlib의 모델링 및 예측 함수는 사용하기 전에 범주 입력 데이터로 기능을 인덱싱 또는 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="4d1e2-244">모델에 따라 다양한 방식에서 인덱싱하거나 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="4d1e2-245">예를 들어 로지스틱 및 선형 회귀 모델은 원 핫 인코딩(one-hot encoding)이 필요하며 이런 경우, 예를 들어 3개의 범주가 있는 기능이 관찰 범주에 따라 각각 0 또는 1을 포함하는 3개의 기능 열로 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="4d1e2-246">MLlib는 원 핫 인코딩 작업을 수행하는 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="4d1e2-247">이 인코더는 레이블 인덱스의 열을 단 하나의 값을 가진 이진 벡터의 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="4d1e2-248">이 인코딩을 사용하여 로지스틱 회귀 분석 등과 같은 숫자 값을 가진 기능을 예상하는 알고리즘을 범주 기능에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="4d1e2-249">다음은 범주 기능을 인덱스 및 인코딩하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-250">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-250">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-251">위의 셀을 실행하는 데 걸린 시간: 3.14초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="4d1e2-252">기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="4d1e2-253">이 섹션에는 범주별 텍스트 데이터를 레이블이 지정된 지점 데이터 형식으로 인덱싱하는 방법과 인코딩하는 방법을 보여 주는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="4d1e2-254">이러한 데이터를 MLlib 로지스틱 회귀 및 기타 분류 모델을 학습 및 테스트하는 데 사용할 수 있도록 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="4d1e2-255">레이블이 지정된 지점 개체는 대부분 MLlib의 기계 학습 알고리즘에서 입력 데이터로 필요한 방식으로 형식이 지정된 RDD(Resilient Distributed Datasets)입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="4d1e2-256">[레이블이 지정된 지점](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 은 레이블/응답과 연결된 로컬 벡터, 밀도 또는 스파스입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="4d1e2-257">다음은 이진 분류를 위해 텍스트 기능을 인덱싱 및 인코딩하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-257">Here is the code to index and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="4d1e2-258">다음은 선형 회귀 분석을 위해 범주 텍스트 기능을 인코딩 및 인덱싱하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="4d1e2-259">데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분할합니다</span><span class="sxs-lookup"><span data-stu-id="4d1e2-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="4d1e2-260">이 코드는 데이터의 무작위 샘플링을 만듭니다(25%가 여기에서 사용됨).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="4d1e2-261">데이터 집합의 크기로 인해 이 예제에 필요하지 않지만 여기서는 데이터를 샘플링하는 방법도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="4d1e2-262">그러면 필요할 때 자체 문제에 사용하는 방법을 알 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="4d1e2-263">샘플이 큰 경우 모델을 학습하는 동안 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="4d1e2-264">다음 샘플을 교육 부분(여기서 75%)와 테스트 부분(여기서 25%)로 분할하여 분류 및 회귀 모델링에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4d1e2-265">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-265">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-266">위의 셀을 실행하는 데 걸린 시간: 0.31초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="4d1e2-267">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="4d1e2-267">Feature scaling</span></span>
<span data-ttu-id="4d1e2-268">데이터 정규화라고도 하는 기능 크기 조정은 폭 넓게 분배된 값을 가진 기능이 목적 함수에서 과도한 가중치를 부여하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="4d1e2-269">기능 크기 조정에 대한 코드는 단위 분산에 대한 기능의 크기를 조정하는 [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="4d1e2-270">이러한 기능은 SGD(Stochastic Gradient Descent)와 함께 선형 회귀에 사용하기 위해 MLlib에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="4d1e2-271">SGD는 정칙 회귀 또는 SVM(support vector machine)과 같은 광범위한 다른 기계 학습 모델을 학습하기 위한 인기 있는 알고리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="4d1e2-272">LinearRegressionWithSGD 알고리즘이 기능 크기 조정에 민감하다는 점을 발견했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="4d1e2-273">여기에 정칙 선형 SGD 알고리즘에 사용할 변수의 크기를 조정하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4d1e2-274">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-274">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-275">위의 셀을 실행하는 데 걸린 시간: 11.67초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="4d1e2-276">메모리에서 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="4d1e2-276">Cache objects in memory</span></span>
<span data-ttu-id="4d1e2-277">분류, 회귀 및 확장된 기능에 사용되는 입력 데이터 프레임 개체를 캐시하여 ML(기계 학습) 알고리즘의 학습 및 테스트에 소요된 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4d1e2-278">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-278">**OUTPUT**</span></span> 

<span data-ttu-id="4d1e2-279">위의 셀을 실행하는 데 걸린 시간: 0.13초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="4d1e2-280">팁이 지불되었는지 여부를 이진 분류 모델로 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="4d1e2-281">이 섹션에서는 Taxi Trip에 팁을 지불했는지 여부를 예측하는 이진 분류 작업에 대한 세 개의 모델을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="4d1e2-282">제공된 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-282">The models presented are:</span></span>

* <span data-ttu-id="4d1e2-283">로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="4d1e2-283">Logistic regression</span></span> 
* <span data-ttu-id="4d1e2-284">임의 포리스트</span><span class="sxs-lookup"><span data-stu-id="4d1e2-284">Random forest</span></span>
* <span data-ttu-id="4d1e2-285">그라데이션 향상 트리</span><span class="sxs-lookup"><span data-stu-id="4d1e2-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="4d1e2-286">코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="4d1e2-287">**모델 교육** 데이터</span><span class="sxs-lookup"><span data-stu-id="4d1e2-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="4d1e2-288">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="4d1e2-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="4d1e2-289">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="4d1e2-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="4d1e2-290">매개 변수 비우기를 사용하여 CV(교차 유효성 검사)를 수행하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="4d1e2-291">MLlib의 모든 알고리즘과 알고리즘 내의 모든 매개 변수 집합에 적용할 수 있는 **제네릭** 사용자 지정 코드 사용</span><span class="sxs-lookup"><span data-stu-id="4d1e2-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="4d1e2-292">**pySpark CrossValidator 파이프라인 함수** 사용</span><span class="sxs-lookup"><span data-stu-id="4d1e2-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="4d1e2-293">CrossValidator에서 Spark 1.5.0을 사용할 때는 다음과 같은 몇 가지 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="4d1e2-294">파이프라인 모델은 향후 사용을 위해 저장되거나 유지될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="4d1e2-295">모델의 모든 매개 변수에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="4d1e2-296">모든 MLlib 알고리즘에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="4d1e2-297">이진 분류에 대한 로지스틱 회귀 분석 알고리즘과 함께 사용되는 일반적인 교차 유효성 검사 및 하이퍼 매개 변수 비우기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="4d1e2-298">이 섹션의 코드에서는 NYC Taxi Trip 및 요금 데이터 집합에서 팁이 여정에 지불되었는지를 예측하는 [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) 로 로지스틱 회귀 분석 모델을 학습하고 평가하며 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="4d1e2-299">MLlib 내의 모든 학습 알고리즘에 적용할 수 있는 사용자 지정 코드로 구현된 CV(교차 유효성 검사) 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="4d1e2-300">이 사용자 지정 CV 코드를 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="4d1e2-301">**CV 및 하이퍼 매개 변수 비우기를 사용하여 로지스틱 회귀 모델 학습**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-302">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-302">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="4d1e2-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="4d1e2-304">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="4d1e2-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="4d1e2-305">위의 셀을 실행하는 데 걸린 시간: 14.43초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="4d1e2-306">**표준 메트릭을 사용한 이진 분류 모델 평가**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="4d1e2-307">이 섹션의 코드는 ROC 곡선 그림을 포함하는 테스트 데이터 집합에 대해 로지스틱 회귀 분석 모델을 평가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-308">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-308">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-309">Area under PR = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="4d1e2-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="4d1e2-310">Area under ROC = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="4d1e2-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="4d1e2-311">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="4d1e2-311">Summary Stats</span></span>

<span data-ttu-id="4d1e2-312">Precision = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="4d1e2-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="4d1e2-313">Recall = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="4d1e2-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="4d1e2-314">F1 Score = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="4d1e2-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="4d1e2-315">위의 셀을 실행하는 데 걸린 시간: 2.67초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="4d1e2-316">**ROC 곡선을 그립니다.**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="4d1e2-317">*predictionAndLabelsDF*는 이전 셀에서 테이블 *tmp_results*로 등록되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="4d1e2-318">*tmp_results*를 사용하면 쿼리를 수행하고 결과를 sqlResults 데이터 프레임으로 출력하여 그래프에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="4d1e2-319">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="4d1e2-320">ROC 곡선을 그리고 예측을 수행하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


<span data-ttu-id="4d1e2-321">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-321">**OUTPUT**</span></span>

![일반적인 접근 방식에 대한 로지스틱 회귀 분석 ROC 곡선](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="4d1e2-323">**나중에 사용할 Blob의 모델 유지**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="4d1e2-324">이 섹션의 코드는 소비에 대한 로지스틱 회귀 분석 모델을 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="4d1e2-325">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-325">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-326">위의 셀을 실행하는 데 걸린 시간: 34.57초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="4d1e2-327">로지스틱 회귀(탄력적 회귀) 모델과 함께 MLlib의 CrossValidator 파이프라인 함수 사용</span><span class="sxs-lookup"><span data-stu-id="4d1e2-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="4d1e2-328">이 섹션의 코드에서는 NYC Taxi Trip 및 요금 데이터 집합에서 팁이 여정에 지불되었는지를 예측하는 [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) 로 로지스틱 회귀 분석 모델을 학습하고 평가하며 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="4d1e2-329">매개 변수 비우기와 함께 CV에 대한 MLlib CrossValidator 파이프라인 함수로 구현되는 CV(교차 유효성 검사) 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="4d1e2-330">이 MLlib CV 코드를 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-330">The execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="4d1e2-331">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-331">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-332">위의 셀을 실행하는 데 걸린 시간: 107.98초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="4d1e2-333">**ROC 곡선을 그립니다.**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="4d1e2-334">*predictionAndLabelsDF*는 이전 셀에서 테이블 *tmp_results*로 등록되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="4d1e2-335">*tmp_results*를 사용하면 쿼리를 수행하고 결과를 sqlResults 데이터 프레임으로 출력하여 그래프에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="4d1e2-336">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="4d1e2-337">다음은 ROC 곡선을 그리는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


<span data-ttu-id="4d1e2-338">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-338">**OUTPUT**</span></span>

![MLlib의 CrossValidator를 사용하는 로지스틱 회귀 분석 ROC 곡선](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="4d1e2-340">임의 포리스트 분류</span><span class="sxs-lookup"><span data-stu-id="4d1e2-340">Random forest classification</span></span>
<span data-ttu-id="4d1e2-341">이 섹션의 코드에서는 NYC Taxi Trip 및 요금 데이터 집합에서 팁이 여정에 지불되었는지 여부를 예측하는 임의 포리스트 회귀를 학습, 평가, 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-342">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-342">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-343">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="4d1e2-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="4d1e2-344">위의 셀을 실행하는 데 걸린 시간: 26.72초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="4d1e2-345">그라데이션 향상 트리 분류</span><span class="sxs-lookup"><span data-stu-id="4d1e2-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="4d1e2-346">이 섹션의 코드에서는 NYC Taxi Trip 및 요금 데이터 집합에서 팁이 여정에 지불되었는지 여부를 예측하는 그라데이션 향상 트리 모델을 학습, 평가, 저장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4d1e2-347">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-347">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-348">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="4d1e2-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="4d1e2-349">위의 셀을 실행하는 데 걸린 시간: 28.13초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="4d1e2-350">회귀 모델로 CV를 사용하지 않고 팁 금액 예측</span><span class="sxs-lookup"><span data-stu-id="4d1e2-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="4d1e2-351">이 섹션에서는 다른 팁 기능에 따라 지불한 팁의 금액을 예측하는 회귀 작업에 대한 세 가지 모델을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="4d1e2-352">제공된 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-352">The models presented are:</span></span>

* <span data-ttu-id="4d1e2-353">정칙 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="4d1e2-353">Regularized linear regression</span></span>
* <span data-ttu-id="4d1e2-354">임의 포리스트</span><span class="sxs-lookup"><span data-stu-id="4d1e2-354">Random forest</span></span>
* <span data-ttu-id="4d1e2-355">그라데이션 향상 트리</span><span class="sxs-lookup"><span data-stu-id="4d1e2-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="4d1e2-356">이러한 모델은 소개에서 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-356">These models were described in the introduction.</span></span> <span data-ttu-id="4d1e2-357">코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="4d1e2-358">**모델 교육** 데이터</span><span class="sxs-lookup"><span data-stu-id="4d1e2-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="4d1e2-359">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="4d1e2-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="4d1e2-360">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="4d1e2-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="4d1e2-361">AZURE 참고: 교차 유효성 검사는 로지스틱 회귀 모델에 대한 세부 정보에 표시되므로 이 섹션의 3가지 회귀 모델에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="4d1e2-362">선형 회귀에 대한 탄력적 net과 함께 CV를 사용하는 방법을 보여 주는 예제를 이 토픽의 부록에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="4d1e2-363">AZURE NOTE: 경험에 따르면 LinearRegressionWithSGD 모델의 수렴과 관련된 문제가 발생할 수 있으며 매개 변수는 유효한 모델을 얻기 위해 신중하게 변경/최적화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="4d1e2-364">변수의 크기를 조정하면 수렴에 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="4d1e2-365">이 토픽의 부록에 나와 있는 바와 같이 LinearRegressionWithSGD 대신 탄력적 net 회귀를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="4d1e2-366">SGD가 있는 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="4d1e2-366">Linear regression with SGD</span></span>
<span data-ttu-id="4d1e2-367">이 섹션의 코드는 크기 조정된 기능을 사용하여 최적화를 위해 SGD(Stochastic Gradient Descent)를 사용하는 선형 회귀를 학습하는 방법 및 WASB(Azure Blob 저장소)에서 모델의 점수를 매기고 평가하며 저장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="4d1e2-368">경험에 따르면 LinearRegressionWithSGD 모델의 수렴과 관련된 문제가 발생할 수 있으며 매개 변수는 유효한 모델을 얻기 위해 신중하게 변경/최적화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="4d1e2-369">변수의 크기를 조정하면 수렴에 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4d1e2-370">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-370">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="4d1e2-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="4d1e2-372">Intercept: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="4d1e2-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="4d1e2-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="4d1e2-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="4d1e2-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="4d1e2-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="4d1e2-375">위의 셀을 실행하는 데 걸린 시간: 38.62초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="4d1e2-376">임의 포리스트 회귀</span><span class="sxs-lookup"><span data-stu-id="4d1e2-376">Random Forest regression</span></span>
<span data-ttu-id="4d1e2-377">이 섹션의 코드에서는 NYC Taxi Trip 데이터에서 팁 금액을 예측하는 임의 포리스트 모델을 학습, 평가, 저장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="4d1e2-378">사용자 지정 코드로 매개 변수 비우기를 사용하는 교차 유효성 검사는 부록에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4d1e2-379">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-379">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="4d1e2-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="4d1e2-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="4d1e2-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="4d1e2-382">위의 셀을 실행하는 데 걸린 시간: 25.98초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="4d1e2-383">그라데이션 향상 트리 회귀</span><span class="sxs-lookup"><span data-stu-id="4d1e2-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="4d1e2-384">이 섹션의 코드에서는 NYC Taxi Trip 데이터에서 팁 금액을 예측하는 그라데이션 향상 트리 모델을 학습, 평가, 저장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="4d1e2-385">* * 학습 하 고 평가 * *</span><span class="sxs-lookup"><span data-stu-id="4d1e2-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-386">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-386">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="4d1e2-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="4d1e2-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="4d1e2-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="4d1e2-389">위의 셀을 실행하는 데 걸린 시간: 20.9초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="4d1e2-390">**그림**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-390">**Plot**</span></span>

<span data-ttu-id="4d1e2-391">*tmp_results*는 이전 셀에서 Hive 테이블로 등록되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="4d1e2-392">테이블의 결과는 그래프로 나타내기 위해 *sqlResults* 데이터 프레임에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="4d1e2-393">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="4d1e2-394">다음은 Jupyter 서버를 사용하여 데이터를 그리는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="4d1e2-396">부록: 매개 변수 비우기를 사용하는 교차 유효성 검사로 추가 회귀 작업</span><span class="sxs-lookup"><span data-stu-id="4d1e2-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="4d1e2-397">이 부록에는 선형 회귀에 대한 탄력적 net을 사용하여 CV를 수행하는 방법 및 임의 포리스트 회귀에 대한 사용자 지정 코드로 매개 변수 비우기를 사용하여 CV를 수행하는 방법을 보여 주는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="4d1e2-398">선형 회귀에 대한 탄력적 net을 사용하여 교차 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4d1e2-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="4d1e2-399">이 섹션의 코드는 선형 회귀에 대한 탄력적 net을 사용하여 교차 유효성 검사를 실행하는 방법 및 테스트 데이터에 대한 모델을 평가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-400">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-400">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-401">위의 셀을 실행하는 데 걸린 시간: 161.21초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="4d1e2-402">**Evaluate with R-SQR metric**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="4d1e2-403">*tmp_results*는 이전 셀에서 Hive 테이블로 등록되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="4d1e2-404">테이블의 결과는 그래프로 나타내기 위해 *sqlResults* 데이터 프레임에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="4d1e2-405">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="4d1e2-406">R-sqr을 계산하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="4d1e2-407">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-407">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="4d1e2-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="4d1e2-409">임의 포리스트 회귀에 대한 사용자 지정 코드로 교차 유효성 검사를 사용한 매개 변수 비우기</span><span class="sxs-lookup"><span data-stu-id="4d1e2-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="4d1e2-410">이 섹션의 코드는 임의 포리스트 회귀에 대한 사용자 지정 코드로 교차 유효성 검사를 사용하여 매개 변수 비우기를 수행하는 방법과 테스트 데이터에 대한 모델을 평가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4d1e2-411">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-411">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="4d1e2-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="4d1e2-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="4d1e2-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="4d1e2-414">위의 셀을 실행하는 데 걸린 시간: 69.17초</span><span class="sxs-lookup"><span data-stu-id="4d1e2-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="4d1e2-415">메모리에서 개체 정리 및 모델 위치 인쇄</span><span class="sxs-lookup"><span data-stu-id="4d1e2-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="4d1e2-416">`unpersist()` 를 사용하여 메모리에 캐시된 개체를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-416">Use `unpersist()` to delete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


<span data-ttu-id="4d1e2-417">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-417">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="4d1e2-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="4d1e2-419">* * 인쇄물 모델 파일을 경로를 소비 노트북에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-419">**Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="4d1e2-420">* *를 사용 하 고 독립적인 데이터 집합 점수를 매깁니다.에서 복사 및 붙여넣기 이러한 파일 이름은 "소비 전자 필기장" 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-420">** To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="4d1e2-421">**출력**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-421">**OUTPUT**</span></span>

<span data-ttu-id="4d1e2-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="4d1e2-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="4d1e2-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="4d1e2-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="4d1e2-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="4d1e2-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="4d1e2-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="4d1e2-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="4d1e2-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="4d1e2-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="4d1e2-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="4d1e2-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="4d1e2-428">다음 작업</span><span class="sxs-lookup"><span data-stu-id="4d1e2-428">What's next?</span></span>
<span data-ttu-id="4d1e2-429">Spark MlLib로 회귀 및 분류 모델을 만든 경우 이러한 모델의점수를  매기고 평가하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="4d1e2-430">**모델 사용:** 이 토픽에서 만든 분류 및 회귀 모델의 점수를 매기고 평가하는 방법을 알아보려면 [Spark에서 만든 기계 학습 모델 점수 매기기 및 평가](machine-learning-data-science-spark-model-consumption.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

