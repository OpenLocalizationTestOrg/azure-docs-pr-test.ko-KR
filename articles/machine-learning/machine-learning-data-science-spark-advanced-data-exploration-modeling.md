---
title: "aaaAdvanced 데이터 탐색 및 모델링 spark | Microsoft Docs"
description: "교차 유효성 검사 및 hyperparameter 최적화를 사용 하 여 이진 분류 및 회귀 모델을 학습 및 HDInsight Spark toodo 데이터 탐색을 사용 합니다."
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
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="4fc6f-103">고급 Spark로 데이터 탐색 및 모델링</span><span class="sxs-lookup"><span data-stu-id="4fc6f-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="4fc6f-104">이 연습에서는 사용 하 여 HDInsight Spark toodo 데이터 탐색 및 학습 이진 분류 및 회귀 모델 교차 유효성 검사를 사용 하 여 hello NYC의 샘플을 hyperparameter 최적화 택시 여행 있어 2013 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="4fc6f-105">Hello hello 단계가 안내 합니다 [데이터 과학 프로세스](http://aka.ms/datascienceprocess), HDInsight Spark를 사용 하 여 끝에 처리를 위해 클러스터 및 Azure blob toostore hello 데이터 및 hello 모델.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="4fc6f-106">hello 프로세스 탐색 하 고, Azure 저장소 Blob에서 가져온 데이터를 시각화 합니다. 하 고, 다음 예측 모델 hello 데이터 toobuild를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="4fc6f-107">Python은 사용 되는 toocode hello 솔루션과 tooshow hello 관련 점도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="4fc6f-108">이러한 모델은 hello Spark MLlib toolkit toodo 이진 분류 및 회귀 모델링 작업을 사용 하 여 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="4fc6f-109">hello **이진 분류** 작업이 toopredict hello 여행에 대 한 팁을 지불 여부.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="4fc6f-110">hello **회귀** 작업은 toopredict hello 양의 hello 팁 다른 팁 기능을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="4fc6f-111">hello 모델링 단계 tootrain를 평가 하 고 각 유형의 모델을 저장 하는 방법을 보여 주는 코드도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="4fc6f-112">hello 항목 몇 가지 설명 hello로 접지 동일 hello [데이터 탐색 및 모델링 spark](machine-learning-data-science-spark-data-exploration-modeling.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="4fc6f-113">하지만 그가 "고급"도와 hyperparameter 스윕 tootrain 최적으로 정확한 분류 및 회귀 모델 교차 유효성 검사를 사용 한다는 점에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="4fc6f-114">**교차 유효성 검사 (CV)** 은 얼마나 잘 알려진된 데이터 집합에서 학습 된 모델을 일반화 기반이 고 학습 되지 않았습니다 데이터 집합의 toopredicting hello 기능을 평가 하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="4fc6f-115">여기에 공통 구현을 toodivide K 접기로 데이터 집합 이며 hello 접기 중 하나를 제외한 모든 문에 라운드 로빈 방식에서 hello 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="4fc6f-116">이 사용 되지 않습니다 접기 tootrain hello 모델 hello 독립적인 데이터 집합에 대해 테스트 하는 경우에 정확 하 게 hello 모델 tooprediction의 hello 기능 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="4fc6f-117">**Hyperparameter 최적화** hello 문제가 hello 독립적인 데이터 집합에 hello 알고리즘의 성능을 최적화 하는 목표를 사용 하 여 일반적으로 학습 알고리즘에 대 한 하이퍼 집합이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="4fc6f-118">**하이퍼** 는 hello 모델 학습 프로시저 외부에서 지정 해야 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="4fc6f-119">이러한 값에 대 한 가정을 hello 유연성과 hello 모델의 정확도 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="4fc6f-120">의사 결정 트리 hello 필요한 깊이 및 hello 트리의 리프 수 같은 예를 들어 하이퍼을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="4fc6f-121">SVM(Support Vector Machine)은 오분류 페널티 조건을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="4fc6f-122">여기에서 사용 하는 일반적인 방법은 tooperform hyperparameter 최적화는 그리드 검색 또는 **매개 변수 비우기를**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="4fc6f-123">학습 알고리즘에 대 한 철저 한 검색 hello 값을 hello hyperparameter 공간의 지정 된 하위 집합을 수행 합니다. 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="4fc6f-124">교차 유효성 검사는 성능 메트릭 toosort hello hello 그리드 검색 알고리즘으로 생성 되는 최적의 결과 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="4fc6f-125">CV hello 모델 유지 되도록 hello 용량 tooapply toohello 일반 데이터 집합이 학습 데이터는 hello에서 추출한 모델 tootraining 데이터에 과잉 맞춤이 다음과 같은 제한 문제 hyperparameter 대대적으로 사용 하면 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="4fc6f-126">hello 모델을 사용 하 여 로지스틱 및 선형 회귀, 임의 포리스트 및 그라데이션 승격 된 트리에 포함:</span><span class="sxs-lookup"><span data-stu-id="4fc6f-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="4fc6f-127">[선형 회귀와 SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 추측 기울기 하강 SGD () 메서드를 사용 하는 선형 회귀 모델은 및 최적화 및 기능에 대 한 결제 toopredict hello 팁 금액을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="4fc6f-128">[로지스틱 회귀와 LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) 또는 "logit" 회귀는 hello 종속 변수는 범주 toodo 데이터 분류에 사용할 수 있는 회귀 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="4fc6f-129">LBFGS는 제한 된 양의 컴퓨터 메모리를 사용 하 여 hello Broyden – Fletcher – Goldfarb – (SHANNO) 알고리즘의 근사치를 계산 하 고 기계 학습에서 널리 사용 되는 준 뉴턴 최적화 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="4fc6f-130">[임의 포리스트](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="4fc6f-131">과잉 맞춤의 많은 의사 결정 트리 tooreduce hello 위험을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="4fc6f-132">임의 포리스트는 분류 및 회귀에 사용 범주 기능을 처리할 수 있습니다 및 toohello 다중 클래스 분류 설정을 확장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="4fc6f-133">기능 크기 조정 및가 수 toocapture 비 미치며 및 상호 작용 기능이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="4fc6f-134">임의 포리스트는 분류 및 회귀에 대 한 모델을 학습 하는 hello 성공적으로 컴퓨터 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="4fc6f-135">[GBT](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (그라데이션 승격 트리)는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="4fc6f-136">GBTs 학습 의사 결정 트리 반복적으로 toominimize 손실 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="4fc6f-137">GBTs 회귀 및 분류에 대 한 사용 및 범주 기능을 처리할 수 있는, 기능 크기 조정이 필요 하지 않습니다 이며 미치며 수 toocapture 비 및 상호 작용 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="4fc6f-138">또한 다중 클래스 분류 설정에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="4fc6f-139">CV 및 Hyperparameter를 사용 하는 예제 모델링 스윕 hello 이진 분류 문제에 대 한 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="4fc6f-140">매개 변수 스윕) (없이 좀 더 간단한 예로 회귀 작업에 대 한 hello 주 항목으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="4fc6f-141">하지만 제공 됩니다 탄력적 net 선형 회귀 및 CV 임의 포리스트 회귀에 대 한 매개 변수 스윕을 사용 하 여 사용 하 여 유효성 검사 hello 부록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="4fc6f-142">hello **탄력적인 net** 결합 하는 정규화 된 회귀 방법을 선형 있는 모델 선형 회귀를 맞추는 방식에 대 한 hello L1 및 L2 메트릭 hello 양의으로 [올가미](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) 및 [홈 음각](https://en.wikipedia.org/wiki/Tikhonov_regularization) 메서드.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="4fc6f-143">Hello Spark MLlib toolkit은 큰 데이터 집합에서 설계 된 toowork를 상대적으로 작은 샘플 (행 170 K hello 원래 NYC 데이터 집합의 0.1%에 대 한 정보를 사용 하 여 최대 30 Mb) 편의 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="4fc6f-144">hello 연습 여기에 나와 효율적으로 (약 10 분 후에) 작업자 노드 2 개 사용 하는 HDInsight 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="4fc6f-145">hello 약간의 수정 된 동일한 코드 수 tooprocess 사용 되는 데이터 집합이 큰 경우-, 적절 한 수정이 데이터를 메모리에에서 캐시 하 고 hello 클러스터 크기를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="4fc6f-146">설정: Spark 클러스터 및 Notebook</span><span class="sxs-lookup"><span data-stu-id="4fc6f-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="4fc6f-147">설치 단계와 코드는 HDInsight Spark 1.6을 사용하는 이 연습에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="4fc6f-148">하지만 Jupyter Notebook은 HDInsight Spark 1.6과 Spark 2.0 클러스터 둘 다에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="4fc6f-149">Hello에 전자 필기장 및 링크 toothem hello에 대 한 설명을 제공 됩니다 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 이 포함 하는 hello GitHub 리포지토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="4fc6f-150">또한 hello 코드와 연결 된 hello 전자 필기장에서 제네릭 인데 어떤 Spark 클러스터에서 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="4fc6f-151">HDInsight Spark를 사용 하지 않는 경우 hello 클러스터 설치 및 관리 단계는 여기 표시 된에서 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="4fc6f-152">편의 위해 Spark 1.6 및 2.0 toobe hello pyspark 커널의 hello Jupyter 노트북 서버에서 실행에 대 한 hello 링크 toohello Jupyter 노트북 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="4fc6f-153">Spark 1.6 Notebook</span><span class="sxs-lookup"><span data-stu-id="4fc6f-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="4fc6f-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Notebook #1의 항목 및 하이퍼 매개 변수 조정 및 교차 유효성 검사를 사용하는 모델 개발을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="4fc6f-155">Spark 2.0 Notebook</span><span class="sxs-lookup"><span data-stu-id="4fc6f-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="4fc6f-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb):이 파일은 어떻게 tooperform 데이터 탐색, 모델링 및 Spark 2.0에서 점수 매기기 클러스터에 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="4fc6f-157">설정: 저장소 위치, 라이브러리 및 hello Spark 컨텍스트 사전 설정</span><span class="sxs-lookup"><span data-stu-id="4fc6f-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="4fc6f-158">Spark 수 tooread 및 쓰기 tooAzure Blob 저장소 (WASB)입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="4fc6f-159">따라서 여기에 저장 된 기존 데이터의 Spark를 사용 하 여 처리할 수 하 고 hello에 다시 저장된 WASB 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="4fc6f-160">toosave 모델 또는 WASB의 파일을 제대로 지정 toobe hello 경로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="4fc6f-161">hello 기본 연결 된 컨테이너 toohello Spark 클러스터를 참조할 수 있습니다로 시작 하는 경로 사용 하 여: "wasb: / / /"입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="4fc6f-162">다른 위치를 “wasb://”에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="4fc6f-163">WASB의 저장소 위치에 대한 디렉터리 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="4fc6f-164">hello 다음 코드 샘플 hello의 위치를 지정 hello 데이터 toobe 읽기 및 hello 모델 저장소 디렉터리 toowhich hello 모델 출력에 대 한 hello 경로가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="4fc6f-165">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-165">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="4fc6f-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="4fc6f-167">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-167">Import libraries</span></span>
<span data-ttu-id="4fc6f-168">필요한 라이브러리를 코드 다음 hello로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-168">Import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="4fc6f-169">미리 설정된 Spark 컨텍스트 및 PySpark 매직</span><span class="sxs-lookup"><span data-stu-id="4fc6f-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="4fc6f-170">Jupyter 노트북에 제공 되는 hello PySpark 커널에는 미리 설정 된 컨텍스트가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="4fc6f-171">따라서 불필요 tooset hello Spark 또는 Hive 컨텍스트 명시적으로 개발 하는 hello 응용 프로그램 사용을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="4fc6f-172">이러한 컨텍스트는 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-172">These contexts are available for you by default.</span></span> <span data-ttu-id="4fc6f-173">이러한 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-173">These contexts are:</span></span>

* <span data-ttu-id="4fc6f-174">sc - Spark용</span><span class="sxs-lookup"><span data-stu-id="4fc6f-174">sc - for Spark</span></span> 
* <span data-ttu-id="4fc6f-175">sqlContext - Hive용</span><span class="sxs-lookup"><span data-stu-id="4fc6f-175">sqlContext - for Hive</span></span>

<span data-ttu-id="4fc6f-176">hello PySpark 커널 제공 일부 미리 정의 된 "마법"으로 호출할 수 있는 특수 명령을 % %입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="4fc6f-177">이러한 코드 샘플에 사용되는 다음과 같은 두 가지 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="4fc6f-178">**% % 로컬** hello 코드 줄에는 로컬로 실행 toobe 임을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="4fc6f-179">코드는 유효한 Python 코드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="4fc6f-180">**%%sql o <variable name>**  sqlContext hello에 대 한 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="4fc6f-181">Hello 쿼리의 hello 결과 hello에서 유지 되 hello-o 매개 변수에 전달 되 면 % % 팬더 데이터 프레임으로 로컬 Python 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="4fc6f-182">Hello 커널에서 Jupyter 노트북 및 미리 정의 된 hello에 대 한 자세한 내용은 "magics"는에 대 한 제공, 참조 [HDInsight Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 HDInsight 클러스터로](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="4fc6f-183">공용 blob에서 데이터 수집:</span><span class="sxs-lookup"><span data-stu-id="4fc6f-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="4fc6f-184">hello hello 데이터 과학 프로세스의 첫 번째 단계는 데이터 탐색 및 모델링 환경에 있는 원본에서 분석 tooingest hello 데이터 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="4fc6f-185">이 환경은 이 연습에서 Spark입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="4fc6f-186">이 섹션에는 hello 코드 toocomplete 일련의 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="4fc6f-187">hello 데이터 샘플 toobe 모델링 수집</span><span class="sxs-lookup"><span data-stu-id="4fc6f-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="4fc6f-188">hello 입력된 데이터 집합 (.tsv 파일으로 저장 됨)의 읽기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="4fc6f-189">형식 및 정리 hello 데이터</span><span class="sxs-lookup"><span data-stu-id="4fc6f-189">format and clean hello data</span></span>
* <span data-ttu-id="4fc6f-190">메모리에 개체 만들기 및 캐시(RDD 또는 데이터 프레임)</span><span class="sxs-lookup"><span data-stu-id="4fc6f-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="4fc6f-191">SQL 컨텍스트에 임시 테이블로 등록</span><span class="sxs-lookup"><span data-stu-id="4fc6f-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="4fc6f-192">데이터 수집에 대 한 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-192">Here is hello code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-193">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-193">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-194">셀 위에서 tooexecute에 걸린 시간: 276.62 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="4fc6f-195">데이터 탐색 및 시각화</span><span class="sxs-lookup"><span data-stu-id="4fc6f-195">Data exploration & visualization</span></span>
<span data-ttu-id="4fc6f-196">가져온 후에 hello 데이터에 Spark에, hello hello 데이터 과학 프로세스의 다음 단계는 toogain hello 데이터 탐색 및 시각화를 통해 더 깊이 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="4fc6f-197">이 섹션에서는 visual 검사에 대 한 SQL 쿼리 및 점도 hello 대상 변수 및 잠재 기능을 사용 하 여 hello 택시 데이터를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="4fc6f-198">특히, 우리 택시 trips, 팁 수량의 hello 빈도 및 어떻게 팁에 따라 다른 지불 양 및 형식은 승객 카운트 hello 주파수를 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="4fc6f-199">히스토그램 승객 count 주파수 택시와 hello 샘플에서의 출력</span><span class="sxs-lookup"><span data-stu-id="4fc6f-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="4fc6f-200">이 코드와 이후의 코드 조각을 로컬 매직 tooplot hello 데이터 및 SQL 매직 tooquery hello 샘플을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="4fc6f-201">**SQL 매직 (`%%sql`)** hello HDInsight PySpark 커널 지원 sqlContext hello에 대 한 쉬운 인라인 HiveQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="4fc6f-202">hello (-o VARIABLE_NAME) 인수 hello Jupyter 서버의 팬더 데이터 프레임으로 hello 출력 hello SQL 쿼리를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="4fc6f-203">즉, hello 로컬 모드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="4fc6f-204">hello  **`%%local` 매직** 는 hello HDInsight 클러스터의 헤드 노드에 hello hello Jupyter 서버에서 로컬로 toorun 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="4fc6f-205">일반적으로 사용 `%%local` hello 후 매직 `%%sql -o` 매직이 사용 되는 toorun 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="4fc6f-206">hello-o 매개 변수 hello SQL 쿼리를 로컬로의 hello 출력을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="4fc6f-207">그런 다음 hello `%%local` 매직 트리거 hello hello SQL 쿼리는 로컬로 유지 hello 출력에 대해 로컬로 코드 조각 toorun 다음 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="4fc6f-208">hello 출력은 hello 코드를 실행 한 후에 자동으로 시각화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="4fc6f-209">이 쿼리는 hello와 승객 수에 따라 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="4fc6f-210">이 코드는 로컬 데이터 프레임 hello 쿼리 결과에서 만들고 hello 데이터 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="4fc6f-211">hello `%%local` 매직 한 로컬 데이터 프레임을 만듭니다 `sqlResults`, matplotlib를 그리기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="4fc6f-212">이 PySpark 매직은 이 연습에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="4fc6f-213">Hello 양의 데이터가 클 경우 toocreate 로컬 메모리에 들어갈 수 있는 데이터 프레임을 샘플 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="4fc6f-214">여기가 hello 코드 tooplot hello trips 승객 개수</span><span class="sxs-lookup"><span data-stu-id="4fc6f-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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

<span data-ttu-id="4fc6f-215">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-215">**OUTPUT**</span></span>

![승객 수에 따른 여정 빈도](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="4fc6f-217">Hello를 사용 하 여 다양 한 유형의 시각화 (테이블, 원형, 꺾은선형, 영역 또는 막대) 간에 선택할 수 있습니다 **형식** hello 전자 필기장의 메뉴 버튼.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="4fc6f-218">hello 모음 그림에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="4fc6f-219">승객 수 및 요금 금액에 따라 팁 금액이 어떻게 달라지는지와 팁 금액에 대한 히스토그램을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="4fc6f-220">SQL 쿼리 toosample 데이터를 사용 하는...</span><span class="sxs-lookup"><span data-stu-id="4fc6f-220">Use a SQL query toosample data..</span></span>

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


<span data-ttu-id="4fc6f-221">이 코드 셀 hello SQL 쿼리 toocreate 세 점도 hello 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="4fc6f-222">**출력:**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-222">**OUTPUT:**</span></span> 

![팁 금액 분포](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![승객 수에 따른 여정 수](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![금액에 따른 팁 금액](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="4fc6f-226">모델링에 대한 기능 엔지니어링, 변환 및 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="4fc6f-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="4fc6f-227">이 섹션에 설명 하 고 ML 모델링에 사용 하기 위해 사용 되는 tooprepare 데이터 hello 프로시저의 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="4fc6f-228">Toodo hello 다음 작업 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="4fc6f-229">시간을 트래픽 시간 bin으로 분할하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="4fc6f-230">범주 기능 인덱스 및 원 핫 인코딩(one-hot encoding)</span><span class="sxs-lookup"><span data-stu-id="4fc6f-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="4fc6f-231">기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="4fc6f-232">Hello 데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분했습니다</span><span class="sxs-lookup"><span data-stu-id="4fc6f-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="4fc6f-233">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="4fc6f-233">Feature scaling</span></span>
* <span data-ttu-id="4fc6f-234">메모리에서 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="4fc6f-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="4fc6f-235">트래픽 시간을 bin으로 분할하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="4fc6f-236">이 코드에 어떻게 toocreate 트래픽을 분할 하 여 새로운 기능 제한 시간이 bin으로 및 toocache 메모리에 결과 데이터 프레임을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="4fc6f-237">캐싱 복원 력 있는 분산 데이터 집합 (RDDs) 및 데이터 프레임 반복적으로 사용 되는 위치 tooimproved 실행 시간 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="4fc6f-238">따라서 RDD 및 데이터 프레임을 연습의 여러 단계에서 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="4fc6f-239">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-239">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-240">126050</span><span class="sxs-lookup"><span data-stu-id="4fc6f-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="4fc6f-241">범주 기능 인덱스 및 원 핫 인코딩(one-hot encoding)</span><span class="sxs-lookup"><span data-stu-id="4fc6f-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="4fc6f-242">이 섹션에서는 어떻게 tooindex 하거나 함수를 모델링 하는 hello에 대 한 입력에 대 한 범주 기능 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="4fc6f-243">모델링 hello 및 MLlib의 함수에는 기능 범주 입력된 데이터에 인덱싱된 것인지 인코딩된 필요 예측 이전 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="4fc6f-244">Hello 모델에 따라 tooindex 필요 하거나 다른 방법으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="4fc6f-245">예를 들어 로지스틱 및 선형 회귀 모델 하나 핫 인코딩이 필요, 여기서 예를 들어 세 가지 범주의 기능 하 여, 포함 된 각 0 또는 1 관찰의 hello 범주에 따라 세 개의 기능 열으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="4fc6f-246">MLlib 제공 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo 인코딩 하나 핫 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="4fc6f-247">이 인코더도 최대 단일 한 값을 이진 벡터의 인덱스 tooa 열을 레이블 열을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="4fc6f-248">로지스틱 회귀와 같은 숫자 중요 기능을 예상 하는 알고리즘을 사용 하면이 인코딩 적용 toobe toocategorical 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="4fc6f-249">다음은 코드 tooindex hello와 범주 기능 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-250">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-250">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-251">셀 위에서 tooexecute에 걸린 시간: 3.14 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="4fc6f-252">기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="4fc6f-253">이 섹션에서는 레이블이 지정 된 지점 데이터로 tooindex 범주 텍스트 데이터 형식 방법 등에 보여 주는 코드 tooencode 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="4fc6f-254">이 준비 사용 toobe tootrain 및 테스트 MLlib 로지스틱 회귀 및 다른 분류 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="4fc6f-255">레이블이 지정된 지점 개체는 대부분 MLlib의 기계 학습 알고리즘에서 입력 데이터로 필요한 방식으로 형식이 지정된 RDD(Resilient Distributed Datasets)입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="4fc6f-256">[레이블이 지정된 지점](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 은 레이블/응답과 연결된 로컬 벡터, 밀도 또는 스파스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="4fc6f-257">다음은 코드 tooindex hello와 이진 분류에 대 한 텍스트 형식 기능을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="4fc6f-258">선형 회귀 분석을 위한 tooencode 및 인덱스 범주 텍스트 기능 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="4fc6f-259">Hello 데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분했습니다</span><span class="sxs-lookup"><span data-stu-id="4fc6f-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="4fc6f-260">이 코드는 hello 데이터 (25% 여기에서 사용 됨)의 무작위 샘플링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="4fc6f-261">Hello 데이터 집합의 toohello 크기 때문에이 예제에 대 한 필요 하지 않더라도 대해서도 설명 방법을 hello 여기에 데이터를 샘플링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="4fc6f-262">한다고 인식 방법을 toouse 필요한 경우 사용자 고유의 문제에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="4fc6f-263">샘플이 큰 경우 모델을 학습하는 동안 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="4fc6f-264">다음 hello 샘플 학습 부분 (75% 여기) 및 분류 및 회귀 모델링에 테스트 부분 (25% 여기) toouse로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4fc6f-265">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-265">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-266">셀 위에서 tooexecute에 걸린 시간: 0.31 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="4fc6f-267">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="4fc6f-267">Feature scaling</span></span>
<span data-ttu-id="4fc6f-268">데이터 정규화 라고도 기능 크기 조정 시나리오는 광범위 하 게 분산된 값이 포함 된 기능은 과도 하 게 지정 된 하지 입니까 hello 목표 함수.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="4fc6f-269">hello 코드 크기를 조정 하는 기능 사용 하 여 hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello 기능 toounit 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="4fc6f-270">이러한 기능은 SGD(Stochastic Gradient Descent)와 함께 선형 회귀에 사용하기 위해 MLlib에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="4fc6f-271">SGD는 정칙 회귀 또는 SVM(support vector machine)과 같은 광범위한 다른 기계 학습 모델을 학습하기 위한 인기 있는 알고리입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="4fc6f-272">Hello LinearRegressionWithSGD 알고리즘 toobe 중요 한 toofeature 배율 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="4fc6f-273">정규화 된 hello 선형 SGD 알고리즘과 함께 사용 하기 위해 hello 코드 tooscale 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4fc6f-274">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-274">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-275">셀 위에서 tooexecute에 걸린 시간: 11.67 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="4fc6f-276">메모리에서 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="4fc6f-276">Cache objects in memory</span></span>
<span data-ttu-id="4fc6f-277">개체 분류와 회귀를 사용 하 고, 기능을 확장할 hello 입력된 데이터 프레임을 캐시 하 여 학습 및 기계 학습 알고리즘의 테스트에 걸린 hello 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4fc6f-278">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-278">**OUTPUT**</span></span> 

<span data-ttu-id="4fc6f-279">셀 위에서 tooexecute에 걸린 시간: 0.13 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="4fc6f-280">팁이 지불되었는지 여부를 이진 분류 모델로 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="4fc6f-281">이 섹션에서는 택시 여행에 대 한 팁을 지불 여부 3 개 사용 하 여 예측의 hello 이진 분류 작업에 대 한 모델링 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="4fc6f-282">제공 된 hello 모델은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-282">hello models presented are:</span></span>

* <span data-ttu-id="4fc6f-283">로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="4fc6f-283">Logistic regression</span></span> 
* <span data-ttu-id="4fc6f-284">임의 포리스트</span><span class="sxs-lookup"><span data-stu-id="4fc6f-284">Random forest</span></span>
* <span data-ttu-id="4fc6f-285">그라데이션 향상 트리</span><span class="sxs-lookup"><span data-stu-id="4fc6f-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="4fc6f-286">코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="4fc6f-287">**모델 교육** 데이터</span><span class="sxs-lookup"><span data-stu-id="4fc6f-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="4fc6f-288">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="4fc6f-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="4fc6f-289">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="4fc6f-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="4fc6f-290">매개 변수를 표시 방법을 toodo 교차 유효성 검사 (CV) 매개 변수 비우기 두 가지 방법으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="4fc6f-291">사용 하 여 **제네릭** 알고리즘에 적용 된 tooany 알고리즘 MLlib 및 tooany 매개 변수에서 될 수 있는 사용자 지정 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="4fc6f-292">Hello를 사용 하 여 **pySpark CrossValidator 파이프라인 함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="4fc6f-293">CrossValidator에서 Spark 1.5.0을 사용할 때는 다음과 같은 몇 가지 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="4fc6f-294">파이프라인 모델은 향후 사용을 위해 저장되거나 유지될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="4fc6f-295">모델의 모든 매개 변수에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="4fc6f-296">모든 MLlib 알고리즘에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="4fc6f-297">교차 유효성 검사 및 이진 분류에 대 한 hello 로지스틱 회귀 알고리즘에 사용 되는 hyperparameter 비우기 제네릭</span><span class="sxs-lookup"><span data-stu-id="4fc6f-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="4fc6f-298">이 섹션의 hello 코드 tootrain를 평가 하 고 사용 하 여 로지스틱 회귀 모델을 저장 하는 방법을 보여 줍니다. [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="4fc6f-299">교차 유효성 검사 (CV) 및 학습 알고리즘에 따라 MLlib hello의 적용 된 tooany 일 수 있는 사용자 지정 코드를 사용 하 여 구현 hyperparameter 비우기를 사용 하 여 hello 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="4fc6f-300">이 사용자 지정 CV 코드 hello 실행 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="4fc6f-301">**CV 및 hyperparameter 비우기 사용 하 여 hello 로지스틱 회귀 모델 학습**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
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


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-302">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-302">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="4fc6f-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="4fc6f-304">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="4fc6f-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="4fc6f-305">셀 위에서 tooexecute에 걸린 시간: 14.43 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="4fc6f-306">**표준 메트릭 사용 하 여 hello 이진 분류 모델 평가**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="4fc6f-307">이 섹션의 hello 코드 방법을 tooevaluate 로지스틱 회귀를 모델링는 테스트 데이터 집합이 hello ROC 곡선의 그림을 포함 하 여에 대해 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-308">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-308">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-309">Area under PR = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="4fc6f-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="4fc6f-310">Area under ROC = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="4fc6f-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="4fc6f-311">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="4fc6f-311">Summary Stats</span></span>

<span data-ttu-id="4fc6f-312">Precision = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="4fc6f-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="4fc6f-313">Recall = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="4fc6f-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="4fc6f-314">F1 Score = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="4fc6f-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="4fc6f-315">셀 위에서 tooexecute에 걸린 시간: 2.67 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="4fc6f-316">**Hello ROC 곡선을 그립니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="4fc6f-317">hello *predictionAndLabelsDF* 테이블로 등록 *tmp_results*, hello 이전 셀에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="4fc6f-318">*tmp_results* toodo 사용 되는 쿼리 수 있고 hello sqlResults 데이터-프레임으로 그래프에 표시 하는 것에 대 한 결과 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="4fc6f-319">Hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="4fc6f-320">다음은 hello 코드 toomake 예측 및 플롯 hello ROC 곡선입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
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


<span data-ttu-id="4fc6f-321">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-321">**OUTPUT**</span></span>

![일반적인 접근 방식에 대한 로지스틱 회귀 분석 ROC 곡선](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="4fc6f-323">**나중에 사용할 Blob의 모델 유지**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="4fc6f-324">이 섹션의 hello 코드 소비에 대 한 toosave hello 로지스틱 회귀 모델 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="4fc6f-325">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-325">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-326">셀 위에서 tooexecute에 걸린 시간: 34.57 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="4fc6f-327">로지스틱 회귀(탄력적 회귀) 모델과 함께 MLlib의 CrossValidator 파이프라인 함수 사용</span><span class="sxs-lookup"><span data-stu-id="4fc6f-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="4fc6f-328">이 섹션의 hello 코드 tootrain를 평가 하 고 사용 하 여 로지스틱 회귀 모델을 저장 하는 방법을 보여 줍니다. [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="4fc6f-329">교차 유효성 검사 (CV)를 사용 하 여 hello 모델을 학습 및 hyperparameter 비우기 구현 hello로 MLlib CrossValidator 파이프라인 함수의 CV에 대 한 매개 변수 비우기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="4fc6f-330">MLlib CV 관리 코드의 hello 실행 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-330">hello execution of this MLlib CV code can take several minutes.</span></span>
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

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="4fc6f-331">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-331">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-332">셀 위에서 tooexecute에 걸린 시간: 107.98 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="4fc6f-333">**Hello ROC 곡선을 그립니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="4fc6f-334">hello *predictionAndLabelsDF* 테이블로 등록 *tmp_results*, hello 이전 셀에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="4fc6f-335">*tmp_results* toodo 사용 되는 쿼리 수 있고 hello sqlResults 데이터-프레임으로 그래프에 표시 하는 것에 대 한 결과 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="4fc6f-336">Hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="4fc6f-337">다음은 hello 코드 tooplot hello ROC 곡선입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
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


<span data-ttu-id="4fc6f-338">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-338">**OUTPUT**</span></span>

![MLlib의 CrossValidator를 사용하는 로지스틱 회귀 분석 ROC 곡선](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="4fc6f-340">임의 포리스트 분류</span><span class="sxs-lookup"><span data-stu-id="4fc6f-340">Random forest classification</span></span>
<span data-ttu-id="4fc6f-341">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부를 예측 하는 임의 포리스트 회귀를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-342">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-342">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-343">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="4fc6f-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="4fc6f-344">셀 위에서 tooexecute에 걸린 시간: 26.72 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="4fc6f-345">그라데이션 향상 트리 분류</span><span class="sxs-lookup"><span data-stu-id="4fc6f-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="4fc6f-346">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부를 예측 하는 그라데이션 승격 트리 모델을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4fc6f-347">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-347">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-348">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="4fc6f-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="4fc6f-349">셀 위에서 tooexecute에 걸린 시간: 28.13 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="4fc6f-350">회귀 모델로 CV를 사용하지 않고 팁 금액 예측</span><span class="sxs-lookup"><span data-stu-id="4fc6f-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="4fc6f-351">이 섹션에서는 3 개 사용 하 여 hello 회귀 작업에 대 한 모델링 하는 방법을 보여 줍니다.: 다른 팁 기능을 기반으로 택시 여행에 대 한 지불 hello 팁 금액을 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="4fc6f-352">제공 된 hello 모델은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-352">hello models presented are:</span></span>

* <span data-ttu-id="4fc6f-353">정칙 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="4fc6f-353">Regularized linear regression</span></span>
* <span data-ttu-id="4fc6f-354">임의 포리스트</span><span class="sxs-lookup"><span data-stu-id="4fc6f-354">Random forest</span></span>
* <span data-ttu-id="4fc6f-355">그라데이션 향상 트리</span><span class="sxs-lookup"><span data-stu-id="4fc6f-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="4fc6f-356">이러한 모델은 hello 소개에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-356">These models were described in hello introduction.</span></span> <span data-ttu-id="4fc6f-357">코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="4fc6f-358">**모델 교육** 데이터</span><span class="sxs-lookup"><span data-stu-id="4fc6f-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="4fc6f-359">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="4fc6f-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="4fc6f-360">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="4fc6f-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="4fc6f-361">AZURE 참고: 교차 유효성 검사 사용 되지 않습니다이 섹션에서는 세 가지 회귀 모델 hello hello 로지스틱 회귀 모델에 대 한 세부 정보에 표시 된이 있으므로.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="4fc6f-362">선형 회귀에 대 한 탄력적인 net CV toouse hello이이 항목의 부록에서 제공 되는 방법을 보여 주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="4fc6f-363">AZURE 참고: 경험에 따르면 포함 될 수 LinearRegressionWithSGD 모델의 일치 문제가 있으며 매개 변수 변경 된/최적화 된 신중 하 게 유효한 모델을 얻기 위한 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="4fc6f-364">변수의 크기를 조정하면 수렴에 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="4fc6f-365">Hello 부록 toothis 항목에 표시 된 탄력적 net 회귀, LinearRegressionWithSGD 대신 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="4fc6f-366">SGD로 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="4fc6f-366">Linear regression with SGD</span></span>
<span data-ttu-id="4fc6f-367">hello이 섹션의 코드를 보여 줍니다 toouse 확장 되는 방식 기능 tootrain 추측 기울기 하강 (SGD) 최적화를 위해 사용 하는 선형 회귀 방법을 tooscore, 평가 및 Azure Blob 저장소 (WASB) hello 모델을 저장 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="4fc6f-368">경험에 따르면 LinearRegressionWithSGD 모델의 hello 수렴 문제가 있을 수 있으며 매개 변수 변경 된/최적화 된 신중 하 게 유효한 모델을 얻기 위한 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="4fc6f-369">변수의 크기를 조정하면 수렴에 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4fc6f-370">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-370">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="4fc6f-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="4fc6f-372">Intercept: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="4fc6f-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="4fc6f-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="4fc6f-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="4fc6f-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="4fc6f-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="4fc6f-375">셀 위에서 tooexecute에 걸린 시간: 38.62 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="4fc6f-376">임의 포리스트 회귀</span><span class="sxs-lookup"><span data-stu-id="4fc6f-376">Random Forest regression</span></span>
<span data-ttu-id="4fc6f-377">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 데이터에 대 한 팁 금액을 예측 하는 임의 포리스트 모델을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="4fc6f-378">매개 변수 사용자 지정 코드를 사용 하 여 비우기와 교차 유효성 검사는 hello 부록에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
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
    # UN-COMMENT IF YOU WANT tooPRING TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4fc6f-379">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-379">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="4fc6f-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="4fc6f-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="4fc6f-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="4fc6f-382">셀 위에서 tooexecute에 걸린 시간: 25.98 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="4fc6f-383">그라데이션 향상 트리 회귀</span><span class="sxs-lookup"><span data-stu-id="4fc6f-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="4fc6f-384">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 데이터에 대 한 팁 금액을 예측 하는 그라데이션 승격 트리 모델을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="4fc6f-385">**학습 및 평가**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-385">**Train and evaluate **</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-386">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-386">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="4fc6f-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="4fc6f-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="4fc6f-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="4fc6f-389">셀 위에서 tooexecute에 걸린 시간: 20.9 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="4fc6f-390">**그림**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-390">**Plot**</span></span>

<span data-ttu-id="4fc6f-391">*tmp_results* hello 이전 셀의 Hive 테이블으로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="4fc6f-392">Hello 테이블의 결과가 hello에 출력 되는 *sqlResults* 그리기에 대 한 데이터 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="4fc6f-393">다음은 hello 코드</span><span class="sxs-lookup"><span data-stu-id="4fc6f-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="4fc6f-394">Hello Jupyter 서버를 사용 하 여 hello 코드 tooplot hello 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="4fc6f-396">부록: 매개 변수 비우기를 사용하는 교차 유효성 검사로 추가 회귀 작업</span><span class="sxs-lookup"><span data-stu-id="4fc6f-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="4fc6f-397">이 부록에서는 코드를 보여 주는 방법을 toodo CV 탄력적 net을 사용 하 여 선형 회귀 및 toodo CV 매개 변수와 함께 스윕 임의 포리스트 회귀에 대 한 사용자 지정 코드를 사용 하 여 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="4fc6f-398">선형 회귀에 대한 탄력적 net을 사용하여 교차 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4fc6f-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="4fc6f-399">이 섹션의 hello 코드 toodo net 확대/축소를 사용 하 여 선형 회귀에 대 한 유효성 검사를 교차 하는 방법 및 tooevaluate 테스트 데이터에 대해 모델을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

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
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-400">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-400">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-401">셀 위에서 tooexecute에 걸린 시간: 161.21 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="4fc6f-402">**Evaluate with R-SQR metric**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="4fc6f-403">*tmp_results* hello 이전 셀의 Hive 테이블으로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="4fc6f-404">Hello 테이블의 결과가 hello에 출력 되는 *sqlResults* 그리기에 대 한 데이터 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="4fc6f-405">다음은 hello 코드</span><span class="sxs-lookup"><span data-stu-id="4fc6f-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="4fc6f-406">Hello 코드 toocalculate R sqr 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="4fc6f-407">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-407">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="4fc6f-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="4fc6f-409">임의 포리스트 회귀에 대한 사용자 지정 코드로 교차 유효성 검사를 사용한 매개 변수 비우기</span><span class="sxs-lookup"><span data-stu-id="4fc6f-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="4fc6f-410">이 섹션의 hello 코드에 toodo 임의 포리스트 회귀에 대 한 사용자 지정 코드를 사용 하 여 매개 변수 비우기를와 유효성 검사를 교차 하는 방법 및 tooevaluate 테스트 데이터에 대해 모델을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

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

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4fc6f-411">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-411">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="4fc6f-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="4fc6f-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="4fc6f-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="4fc6f-414">셀 위에서 tooexecute에 걸린 시간: 69.17 초</span><span class="sxs-lookup"><span data-stu-id="4fc6f-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="4fc6f-415">메모리에서 개체 정리 및 모델 위치 인쇄</span><span class="sxs-lookup"><span data-stu-id="4fc6f-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="4fc6f-416">사용 하 여 `unpersist()` toodelete 개체 메모리에 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


<span data-ttu-id="4fc6f-417">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-417">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="4fc6f-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="4fc6f-419">* * 인쇄물 경로 toomodel toobe hello 소비 전자 필기장에 사용 되는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="4fc6f-420">* * tooconsume 점수와 독립적인 데이터 집합, toocopy 필요 하 고 이러한 파일 이름은 "소비 노트북" hello에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="4fc6f-421">**출력**</span><span class="sxs-lookup"><span data-stu-id="4fc6f-421">**OUTPUT**</span></span>

<span data-ttu-id="4fc6f-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="4fc6f-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="4fc6f-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="4fc6f-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="4fc6f-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="4fc6f-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="4fc6f-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="4fc6f-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="4fc6f-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="4fc6f-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="4fc6f-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="4fc6f-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="4fc6f-428">다음 작업</span><span class="sxs-lookup"><span data-stu-id="4fc6f-428">What's next?</span></span>
<span data-ttu-id="4fc6f-429">준비 toolearn 어떻게는 Spark MlLib hello로 분류 및 회귀 모델을 만든 tooscore 하 고 이러한 모델을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="4fc6f-430">**소비 모델:** toolearn 어떻게 tooscore이이 항목에서 만든 hello 분류 및 회귀 모델을 평가 하 고, 참조 및 [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc6f-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

