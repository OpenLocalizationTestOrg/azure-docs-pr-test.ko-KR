---
title: "aaaData 탐색 및 모델링 spark | Microsoft Docs"
description: "전시는 데이터 탐색 및 모델링 기능 hello Spark MLlib 도구 키트에서 Azure의 hello 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="c5e7e-103">Spark로 데이터 탐색 및 모델링</span><span class="sxs-lookup"><span data-stu-id="c5e7e-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="c5e7e-104">이 연습에서는 HDInsight Spark toodo 데이터 탐색을 사용 및 택시 여행 및 2013 dataset 있어 이진 분류 및 회귀 샘플 hello NYC 모델링 하는 작업.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="c5e7e-105">Hello hello 단계가 안내 합니다 [데이터 과학 프로세스](http://aka.ms/datascienceprocess), HDInsight Spark를 사용 하 여 끝에 처리를 위해 클러스터 및 Azure blob toostore hello 데이터 및 hello 모델.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="c5e7e-106">hello 프로세스 탐색 하 고, Azure 저장소 Blob에서 가져온 데이터를 시각화 합니다. 하 고, 다음 예측 모델 hello 데이터 toobuild를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="c5e7e-107">이러한 모델은 hello Spark MLlib toolkit toodo 이진 분류 및 회귀 모델링 작업을 사용 하 여 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="c5e7e-108">hello **이진 분류** 작업이 toopredict hello 여행에 대 한 팁을 지불 여부.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="c5e7e-109">hello **회귀** 작업은 toopredict hello 양의 hello 팁 다른 팁 기능을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="c5e7e-110">hello 모델을 사용 하 여 로지스틱 및 선형 회귀, 임의 포리스트 및 그라데이션 승격 된 트리에 포함:</span><span class="sxs-lookup"><span data-stu-id="c5e7e-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="c5e7e-111">[선형 회귀와 SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 추측 기울기 하강 SGD () 메서드를 사용 하는 선형 회귀 모델은 및 최적화 및 기능에 대 한 결제 toopredict hello 팁 금액을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="c5e7e-112">[로지스틱 회귀와 LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) 또는 "logit" 회귀는 hello 종속 변수는 범주 toodo 데이터 분류에 사용할 수 있는 회귀 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="c5e7e-113">LBFGS는 제한 된 양의 컴퓨터 메모리를 사용 하 여 hello Broyden – Fletcher – Goldfarb – (SHANNO) 알고리즘의 근사치를 계산 하 고 기계 학습에서 널리 사용 되는 준 뉴턴 최적화 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="c5e7e-114">[임의 포리스트](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="c5e7e-115">과잉 맞춤의 많은 의사 결정 트리 tooreduce hello 위험을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="c5e7e-116">임의 포리스트는 분류 및 회귀에 사용 범주 기능을 처리할 수 있습니다 및 toohello 다중 클래스 분류 설정을 확장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="c5e7e-117">기능 크기 조정 및가 수 toocapture 비 미치며 및 상호 작용 기능이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="c5e7e-118">임의 포리스트는 분류 및 회귀에 대 한 모델을 학습 하는 hello 성공적으로 컴퓨터 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="c5e7e-119">[GBT](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (그라데이션 승격 트리)는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="c5e7e-120">GBTs 학습 의사 결정 트리 반복적으로 toominimize 손실 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="c5e7e-121">GBTs 회귀 및 분류에 대 한 사용 및 범주 기능을 처리할 수 있는, 기능 크기 조정이 필요 하지 않습니다 이며 미치며 수 toocapture 비 및 상호 작용 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="c5e7e-122">또한 다중 클래스 분류 설정에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="c5e7e-123">hello 모델링 단계 tootrain를 평가 하 고 각 유형의 모델을 저장 하는 방법을 보여 주는 코드도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="c5e7e-124">Python은 사용 되는 toocode hello 솔루션과 tooshow hello 관련 점도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="c5e7e-125">Hello Spark MLlib toolkit은 큰 데이터 집합에서 설계 된 toowork를 상대적으로 작은 샘플 (행 170 K hello 원래 NYC 데이터 집합의 0.1%에 대 한 정보를 사용 하 여 최대 30 Mb) 편의 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="c5e7e-126">hello 연습 여기에 나와 효율적으로 (약 10 분 후에) 작업자 노드 2 개 사용 하는 HDInsight 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="c5e7e-127">hello 약간의 수정 된 동일한 코드 수 tooprocess 사용 되는 데이터 집합이 큰 경우-, 적절 한 수정이 데이터를 메모리에에서 캐시 하 고 hello 클러스터 크기를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c5e7e-128">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5e7e-128">Prerequisites</span></span>
<span data-ttu-id="c5e7e-129">Azure 계정 및는 Spark 1.6 (또는)가 필요한 Spark 2.0 HDInsight 클러스터 toocomplete이이 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="c5e7e-130">Hello 참조 [개요의 데이터 과학 Azure HDInsight의 Spark를 사용 하 여](machine-learning-data-science-spark-overview.md) 방법에 대 한 지침은 toosatisfy 이러한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="c5e7e-131">해당 항목에는 여기에 NYC 2013 택시 데이터 hello 및 tooexecute hello Spark 클러스터에서 Jupyter 노트북에서 코드가 하는 방식에 대 한 지침에 대 한 설명을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="c5e7e-132">Spark 클러스터 및 Notebook</span><span class="sxs-lookup"><span data-stu-id="c5e7e-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="c5e7e-133">설치 단계와 코드는 HDInsight Spark 1.6을 사용하는 이 연습에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="c5e7e-134">하지만 Jupyter Notebook은 HDInsight Spark 1.6과 Spark 2.0 클러스터 둘 다에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="c5e7e-135">Hello에 전자 필기장 및 링크 toothem hello에 대 한 설명을 제공 됩니다 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 이 포함 하는 hello GitHub 리포지토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="c5e7e-136">또한 hello 코드와 연결 된 hello 전자 필기장에서 제네릭 인데 어떤 Spark 클러스터에서 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="c5e7e-137">HDInsight Spark를 사용 하지 않는 경우 hello 클러스터 설치 및 관리 단계는 여기 표시 된에서 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="c5e7e-138">편의 위해 링크는 다음과 같습니다 hello Spark 1.6 (toobe hello pySpark 커널의 hello Jupyter 노트북 서버에서 실행) 및 Spark 2.0 (toobe hello pySpark3 커널의 hello Jupyter 노트북 서버에서 실행)에 대 한 toohello Jupyter 노트북:</span><span class="sxs-lookup"><span data-stu-id="c5e7e-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="c5e7e-139">Spark 1.6 Notebook</span><span class="sxs-lookup"><span data-stu-id="c5e7e-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="c5e7e-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): 방법에 대해 설명 tooperform 데이터 탐색, 모델링 및 다양 한 알고리즘이 점수 매기기입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="c5e7e-141">Spark 2.0 Notebook</span><span class="sxs-lookup"><span data-stu-id="c5e7e-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="c5e7e-142">2.0 Spark 클러스터를 사용 하 여 구현 되는 hello 분류 및 회귀 작업 별도 노트북에 있고 다른 데이터 집합을 사용 하 여 hello 분류 노트북:</span><span class="sxs-lookup"><span data-stu-id="c5e7e-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="c5e7e-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb):이 파일 어떻게 tooperform 데이터 탐색, 모델링 및 Spark 2.0에서 점수 매기기 클러스터 NYC 택시 여행 hello를 사용 하 여에 정보를 제공 합니다. 및 데이터 집합 설명 요금 [여기](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="c5e7e-144">이 전자 필기장 신속 하 게 Spark 2.0를 제공 하는 hello 코드를 탐색 하기 위한 좋은 출발점 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="c5e7e-145">더 자세한 노트북 hello NYC 택시 데이터를 분석에 대 한이 목록에 다음 노트북을 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="c5e7e-146">이러한 전자 필기장을 비교 하는이 목록 다음 되는 hello 메모를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="c5e7e-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb):이 파일은 NYC 택시 여행 및 요금 데이터 집합 설명 tooperform 데이터 wrangling (Spark SQL 및 데이터 프레임 작업) 탐색을 모델링 하 고 사용 하 여 점수 매기기 hello 하는 방법을 보여 줍니다. [ 여기](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="c5e7e-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb):이 파일은 tooperform 데이터 wrangling (Spark SQL 및 데이터 프레임 작업) 탐색을 모델링 하 고 사용 하 여 점수 매기기 잘 알려진 Airline 정시 출발 hello 하는 방법을 보여 줍니다. 2011 및 2012에서 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="c5e7e-149">에서는 통합 hello airline 데이터 집합 hello 공항 날씨 데이터 (예:: windspeed, 온도, 고도 등) 이전 toomodeling, 되므로 이러한 날씨 기능 hello 모델에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="c5e7e-150">hello airline 데이터 집합 추가 toohello Spark 2.0 전자 필기장 toobetter 분류 알고리즘의 hello 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="c5e7e-151">Airline 정시 출발 집합과 날씨 데이터 집합에 대 한 정보에 대 한 링크를 따라 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="c5e7e-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="c5e7e-152">항공사 정시 출발 데이터: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="c5e7e-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="c5e7e-153">공항 날씨 데이터: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="c5e7e-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="c5e7e-154">hello NYC 택시에서 hello Spark 2.0 전자 필기장 및 airline 비행 지연 데이터 집합에는 10 분 또는 (hello의 크기에 따라 HDI 클러스터) 자세한 toorun 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="c5e7e-155">hello 목록 위의 hello에서 첫 번째 노트북 hello 데이터 탐색의 다양 한 부분, 시각화 및 기계 학습 모델 교육 축소 샘플링 NYC 데이터 집합으로는 hello 택시 및 요금 파일 미리 조인 했습니다 적은 시간 toorun 받아들이는 노트북: [ Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) 이 노트북은 훨씬 더 짧은 시간 toofinish (2-3 분) 걸리고 있습니다 수 좋은 시작 지점 신속 하 게 hello 코드 탐색에 대 한 했으므로 Spark 2.0에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="c5e7e-156">hello 설명은 아래에 관련된 toousing Spark 1.6 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="c5e7e-157">Spark 2.0 버전에 대 한 설명 하 고 위에 링크 된 hello 노트북을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="c5e7e-158">설정: 저장소 위치, 라이브러리 및 hello Spark 컨텍스트 사전 설정</span><span class="sxs-lookup"><span data-stu-id="c5e7e-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="c5e7e-159">Spark 수 tooread 및 쓰기 tooAzure Blob 저장소 (WASB)입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="c5e7e-160">따라서 여기에 저장 된 기존 데이터의 Spark를 사용 하 여 처리할 수 하 고 hello에 다시 저장된 WASB 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="c5e7e-161">toosave 모델 또는 WASB의 파일을 제대로 지정 toobe hello 경로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="c5e7e-162">hello 기본 연결 된 컨테이너 toohello Spark 클러스터를 참조할 수 있습니다로 시작 하는 경로 사용 하 여: "wasb: / / /"입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="c5e7e-163">다른 위치를 “wasb://”에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="c5e7e-164">WASB의 저장소 위치에 대한 디렉터리 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="c5e7e-165">hello 다음 코드 샘플 hello의 위치를 지정 hello 데이터 toobe 읽기 및 hello 모델 저장소 디렉터리 toowhich hello 모델 출력에 대 한 hello 경로가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="c5e7e-166">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="c5e7e-166">Import libraries</span></span>
<span data-ttu-id="c5e7e-167">또한 필요한 라이브러리를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="c5e7e-168">Spark 컨텍스트를 설정 하 여 코드 다음 hello로 필요한 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-168">Set spark context and import necessary libraries with hello following code:</span></span>

    # IMPORT LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="c5e7e-169">미리 설정된 Spark 컨텍스트 및 PySpark 매직</span><span class="sxs-lookup"><span data-stu-id="c5e7e-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="c5e7e-170">Jupyter 노트북에 제공 되는 hello PySpark 커널에는 미리 설정 된 컨텍스트가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="c5e7e-171">따라서 불필요 tooset hello Spark 또는 Hive 컨텍스트 명시적으로 개발 하는 hello 응용 프로그램 사용을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="c5e7e-172">이러한 컨텍스트는 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-172">These contexts are available for you by default.</span></span> <span data-ttu-id="c5e7e-173">이러한 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-173">These contexts are:</span></span>

* <span data-ttu-id="c5e7e-174">sc - Spark용</span><span class="sxs-lookup"><span data-stu-id="c5e7e-174">sc - for Spark</span></span> 
* <span data-ttu-id="c5e7e-175">sqlContext - Hive용</span><span class="sxs-lookup"><span data-stu-id="c5e7e-175">sqlContext - for Hive</span></span>

<span data-ttu-id="c5e7e-176">hello PySpark 커널 제공 일부 미리 정의 된 "마법"으로 호출할 수 있는 특수 명령을 % %입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="c5e7e-177">이러한 코드 샘플에 사용되는 다음과 같은 두 가지 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="c5e7e-178">**% % 로컬** hello 코드 줄에는 로컬로 실행 toobe 임을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="c5e7e-179">코드는 유효한 Python 코드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="c5e7e-180">**%%sql o <variable name>**  sqlContext hello에 대 한 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="c5e7e-181">Hello 쿼리의 hello 결과 hello에서 유지 되 hello-o 매개 변수에 전달 되 면 % % 팬더 데이터 프레임으로 로컬 Python 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="c5e7e-182">Hello 커널에서 Jupyter 노트북 및 미리 정의 된 hello에 대 한 자세한 내용은 "magics"는에 대 한 제공, 참조 [HDInsight Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 HDInsight 클러스터로](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="c5e7e-183">공용 blob에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="c5e7e-183">Data ingestion from public blob</span></span>
<span data-ttu-id="c5e7e-184">hello hello 데이터 과학 프로세스의 첫 번째 단계는 원본에서 분석 tooingest hello 데이터 toobe 여기서는 데이터 탐색 및 모델링 환경에 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="c5e7e-185">hello 환경은이 연습에서 Spark입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="c5e7e-186">이 섹션에는 hello 코드 toocomplete 일련의 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="c5e7e-187">hello 데이터 샘플 toobe 모델링 수집</span><span class="sxs-lookup"><span data-stu-id="c5e7e-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="c5e7e-188">hello 입력된 데이터 집합 (.tsv 파일으로 저장 됨)의 읽기</span><span class="sxs-lookup"><span data-stu-id="c5e7e-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="c5e7e-189">형식 및 정리 hello 데이터</span><span class="sxs-lookup"><span data-stu-id="c5e7e-189">format and clean hello data</span></span>
* <span data-ttu-id="c5e7e-190">메모리에 개체 만들기 및 캐시(RDD 또는 데이터 프레임)</span><span class="sxs-lookup"><span data-stu-id="c5e7e-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="c5e7e-191">SQL 컨텍스트에 임시 테이블로 등록</span><span class="sxs-lookup"><span data-stu-id="c5e7e-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="c5e7e-192">데이터 수집에 대 한 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="c5e7e-193">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-193">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-194">셀 위에서 tooexecute에 걸린 시간: 51.72 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="c5e7e-195">데이터 탐색 및 시각화</span><span class="sxs-lookup"><span data-stu-id="c5e7e-195">Data exploration & visualization</span></span>
<span data-ttu-id="c5e7e-196">가져온 후에 hello 데이터에 Spark에, hello hello 데이터 과학 프로세스의 다음 단계는 toogain hello 데이터 탐색 및 시각화를 통해 더 깊이 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="c5e7e-197">이 섹션에서는 visual 검사에 대 한 SQL 쿼리 및 점도 hello 대상 변수 및 잠재 기능을 사용 하 여 hello 택시 데이터를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="c5e7e-198">특히, 우리 택시 trips, 팁 수량의 hello 빈도 및 어떻게 팁에 따라 다른 지불 양 및 형식은 승객 카운트 hello 주파수를 그립니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="c5e7e-199">히스토그램 승객 count 주파수 택시와 hello 샘플에서의 출력</span><span class="sxs-lookup"><span data-stu-id="c5e7e-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="c5e7e-200">이 코드와 이후의 코드 조각을 로컬 매직 tooplot hello 데이터 및 SQL 매직 tooquery hello 샘플을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="c5e7e-201">**SQL 매직 (`%%sql`)** hello HDInsight PySpark 커널 지원 sqlContext hello에 대 한 쉬운 인라인 HiveQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="c5e7e-202">hello (-o VARIABLE_NAME) 인수 hello Jupyter 서버의 팬더 데이터 프레임으로 hello 출력 hello SQL 쿼리를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="c5e7e-203">즉, hello 로컬 모드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="c5e7e-204">hello  **`%%local` 매직** 는 hello HDInsight 클러스터의 헤드 노드에 hello hello Jupyter 서버에서 로컬로 toorun 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="c5e7e-205">일반적으로 사용 `%%local` hello와 함께에서 매직 `%%sql` 매직-o 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="c5e7e-206">hello-o 매개 변수는 hello SQL 쿼리를 로컬로의 hello 출력을 유지 한 다음 % % 로컬 매직 hello 다음 코드 조각 toorun 로컬로 유지 되는 hello SQL 쿼리의 hello 출력에 대해 로컬로 집합이 트리거할지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="c5e7e-207">hello 출력은 hello 코드를 실행 한 후에 자동으로 시각화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="c5e7e-208">이 쿼리는 hello와 승객 수에 따라 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="c5e7e-209">이 코드는 로컬 데이터 프레임 hello 쿼리 결과에서 만들고 hello 데이터 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="c5e7e-210">hello `%%local` 매직 한 로컬 데이터 프레임을 만듭니다 `sqlResults`, matplotlib를 그리기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="c5e7e-211">이 PySpark 매직은 이 연습에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="c5e7e-212">Hello 양의 데이터가 클 경우 toocreate 로컬 메모리에 들어갈 수 있는 데이터 프레임을 샘플 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="c5e7e-213">여기가 hello 코드 tooplot hello trips 승객 개수</span><span class="sxs-lookup"><span data-stu-id="c5e7e-213">Here is hello code tooplot hello trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="c5e7e-214">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-214">**OUTPUT:**</span></span>

![승객 수에 따른 여정 빈도](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="c5e7e-216">Hello를 사용 하 여 다양 한 유형의 시각화 (테이블, 원형, 꺾은선형, 영역 또는 막대) 간에 선택할 수 있습니다 **형식** hello 전자 필기장의 메뉴 버튼.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="c5e7e-217">hello 모음 그림에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="c5e7e-218">승객 수 및 요금 금액에 따라 팁 금액이 어떻게 달라지는지와 팁 금액에 대한 히스토그램을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="c5e7e-219">SQL 쿼리 toosample 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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


<span data-ttu-id="c5e7e-220">이 코드 셀 hello SQL 쿼리 toocreate 세 점도 hello 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="c5e7e-221">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-221">**OUTPUT:**</span></span> 

![팁 금액 분포](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![승객 수에 따른 여정 수](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![금액으로 녀건 금액](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="c5e7e-225">모델링에 대한 기능 엔지니어링, 변환 및 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="c5e7e-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="c5e7e-226">이 섹션에 설명 하 고 ML 모델링에 사용 하기 위해 사용 되는 tooprepare 데이터 hello 프로시저의 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="c5e7e-227">Toodo hello 다음 작업 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="c5e7e-228">시간을 트래픽 시간 버킷으로 범주화하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="c5e7e-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="c5e7e-229">범주 기능 인덱스 및 인코딩</span><span class="sxs-lookup"><span data-stu-id="c5e7e-229">Index and encode categorical features</span></span>
* <span data-ttu-id="c5e7e-230">기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="c5e7e-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="c5e7e-231">Hello 데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분했습니다</span><span class="sxs-lookup"><span data-stu-id="c5e7e-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="c5e7e-232">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c5e7e-232">Feature scaling</span></span>
* <span data-ttu-id="c5e7e-233">메모리에서 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="c5e7e-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="c5e7e-234">시간을 트래픽 시간 버킷으로 범주화하여 새로운 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="c5e7e-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="c5e7e-235">이 코드에 어떻게 toocreate 트래픽 시간에 시간을 범주화 하 여 새로운 기능 버킷 및 toocache 메모리에 결과 데이터 프레임을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="c5e7e-236">복원 력 있는 분산 데이터 집합 (RDDs) 및 데이터 프레임은 사용 되는 반복 해 서, tooimproved 실행 시간 연결 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="c5e7e-237">따라서 캐시 RDDs 및 데이터 프레임 hello 연습에서 여러 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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

<span data-ttu-id="c5e7e-238">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-238">**OUTPUT:**</span></span> 

<span data-ttu-id="c5e7e-239">126050</span><span class="sxs-lookup"><span data-stu-id="c5e7e-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="c5e7e-240">모델링 기능에 입력에 대한 범주 기능 인덱스 및 인코딩</span><span class="sxs-lookup"><span data-stu-id="c5e7e-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="c5e7e-241">이 섹션에서는 어떻게 tooindex 하거나 함수를 모델링 하는 hello에 대 한 입력에 대 한 범주 기능 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="c5e7e-242">hello 모델링 하 고 범주 입력된 데이터 toobe 기능과 인덱싱된 또는 이전 toouse 인코딩된 MLlib의 기능 필요를 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="c5e7e-243">Hello 모델에 따라 tooindex 필요 하거나 다른 방법으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="c5e7e-244">**트리 기반 모델링** 숫자 값으로 인코딩된 범주 toobe 필요 (예를 들어 세 가지 범주의 기능으로 인코딩할 수 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="c5e7e-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="c5e7e-245">MLlib의 [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) 함수에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="c5e7e-246">이 함수는 레이블 주파수로 정렬 됩니다 레이블 인덱스의 레이블 tooa 열의 문자열 열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="c5e7e-247">입력 및 데이터 처리에 대 한 숫자 값을 사용 하 여 인덱싱할 있지만 hello 트리 기반 알고리즘 지정된 tootreat 수 항목으로 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="c5e7e-248">**로지스틱 및 선형 회귀 모델** 하나 핫 인코딩이 필요 where, 예를 들어 세 가지 범주의 기능 구조로 확장할 수 있습니다 각 포함 된 0 또는 1 관찰의 hello 범주에 따라 세 개의 기능 열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="c5e7e-249">MLlib 제공 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo 인코딩 하나 핫 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="c5e7e-250">이 인코더도 최대 단일 한 값을 이진 벡터의 인덱스 tooa 열을 레이블 열을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="c5e7e-251">로지스틱 회귀와 같은 숫자 중요 기능을 예상 하는 알고리즘을 사용 하면이 인코딩 적용 toobe toocategorical 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="c5e7e-252">다음은 코드 tooindex hello와 범주 기능 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

<span data-ttu-id="c5e7e-253">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-253">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-254">셀 위에서 tooexecute에 걸린 시간: 1.28 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="c5e7e-255">기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="c5e7e-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="c5e7e-256">이 섹션에는 레이블이 지정 된 지점 데이터로 tooindex 범주 텍스트 데이터를 입력 하 고 사용 하는 테스트 및 tootrain MLlib 로지스틱 회귀 및 다른 분류 모델 될 수 있도록 인코딩할 하는 방법을 보여 주는 코드가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="c5e7e-257">레이블이 지정된 지점 개체는 대부분 MLlib의 기계 학습 알고리즘에서 입력 데이터로 필요한 방식으로 형식이 지정된 RDD(Resilient Distributed Datasets)입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="c5e7e-258">[레이블이 지정된 지점](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 은 레이블/응답과 연결된 로컬 벡터, 밀도 또는 스파스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="c5e7e-259">이 섹션에서는 보여 주는 코드 방법을 tooindex 범주 텍스트 데이터를는 [지점 레이블이 지정 된](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 데이터 형식를 사용 하는 테스트 및 tootrain MLlib 로지스틱 회귀 및 다른 분류 모델 될 수 있도록 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="c5e7e-260">레이블이 지정된 지점 개체는 레이블(대상/응답 변수) 및 기능 벡터로 구성된 RDD(Resilient Distributed Datasets)입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="c5e7e-261">이 서식은 MLlib의 많은 기계 학습 알고리즘에서 입력으로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="c5e7e-262">다음은 코드 tooindex hello와 이진 분류에 대 한 텍스트 형식 기능을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="c5e7e-263">선형 회귀 분석을 위한 tooencode 및 인덱스 범주 텍스트 기능 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="c5e7e-264">Hello 데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분했습니다</span><span class="sxs-lookup"><span data-stu-id="c5e7e-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="c5e7e-265">이 코드는 hello 데이터 (25% 여기에서 사용 됨)의 무작위 샘플링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="c5e7e-266">Hello 데이터 집합의 toohello 크기 때문에이 예제에 대 한 필요 하지 않더라도 대해서도 설명 방법을 샘플링할 수 있습니다 여기 알 수 있도록 어떻게 toouse 필요할 때 자신의 문제에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="c5e7e-267">샘플이 큰 경우 모델을 학습하는 동안 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="c5e7e-268">다음 hello 샘플 학습 부분 (75% 여기) 및 분류 및 회귀 모델링에 테스트 부분 (25% 여기) toouse로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

<span data-ttu-id="c5e7e-269">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-269">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-270">셀 위에서 tooexecute에 걸린 시간: 0.24 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="c5e7e-271">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c5e7e-271">Feature scaling</span></span>
<span data-ttu-id="c5e7e-272">데이터 정규화 라고도 기능 크기 조정 시나리오는 광범위 하 게 분산된 값이 포함 된 기능은 과도 하 게 지정 된 하지 입니까 hello 목표 함수.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="c5e7e-273">hello 코드 크기를 조정 하는 기능 사용 하 여 hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello 기능 toounit 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="c5e7e-274">정칙 회귀 또는 SVM(support vector machine)과 같은 광범위한 다른 기계 학습 모델을 학습하기 위한 인기 있는 알고리즘인 SGD(Stochastic Gradient Descent)와 함께 선형 회귀에 사용하기 위해 MLlib에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="c5e7e-275">Hello LinearRegressionWithSGD 알고리즘 toobe 중요 한 toofeature 배율 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="c5e7e-276">정규화 된 hello 선형 SGD 알고리즘과 함께 사용 하기 위해 hello 코드 tooscale 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

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

<span data-ttu-id="c5e7e-277">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-277">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-278">셀 위에서 tooexecute에 걸린 시간: 13.17 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="c5e7e-279">메모리에서 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="c5e7e-279">Cache objects in memory</span></span>
<span data-ttu-id="c5e7e-280">hello 시간 분류와 회귀를 사용 하는 hello 입력된 데이터 프레임 개체를 캐시 하 여 학습 및 테스트 기계 학습 알고리즘 중을 줄일 수 있습니다에 대해 수행 되 고 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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

<span data-ttu-id="c5e7e-281">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-281">**OUTPUT:**</span></span> 

<span data-ttu-id="c5e7e-282">셀 위에서 tooexecute에 걸린 시간: 0.15 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="c5e7e-283">팁이 지불되었는지 여부를 이진 분류 모델로 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="c5e7e-284">이 섹션에서는 택시 여행에 대 한 팁을 지불 여부 3 개 사용 하 여 예측의 hello 이진 분류 작업에 대 한 모델링 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="c5e7e-285">제공 된 hello 모델은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-285">hello models presented are:</span></span>

* <span data-ttu-id="c5e7e-286">정칙 로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="c5e7e-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="c5e7e-287">임의 포리스트 모델</span><span class="sxs-lookup"><span data-stu-id="c5e7e-287">Random forest model</span></span>
* <span data-ttu-id="c5e7e-288">그라데이션 향상 트리</span><span class="sxs-lookup"><span data-stu-id="c5e7e-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="c5e7e-289">코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="c5e7e-290">**모델 교육** 데이터</span><span class="sxs-lookup"><span data-stu-id="c5e7e-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="c5e7e-291">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="c5e7e-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="c5e7e-292">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="c5e7e-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="c5e7e-293">로지스틱 회귀를 사용하는 분류</span><span class="sxs-lookup"><span data-stu-id="c5e7e-293">Classification using logistic regression</span></span>
<span data-ttu-id="c5e7e-294">이 섹션의 hello 코드 tootrain를 평가 하 고 사용 하 여 로지스틱 회귀 모델을 저장 하는 방법을 보여 줍니다. [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="c5e7e-295">**CV 및 hyperparameter 비우기 사용 하 여 hello 로지스틱 회귀 모델 학습**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="c5e7e-296">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-296">**OUTPUT:**</span></span> 

<span data-ttu-id="c5e7e-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="c5e7e-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="c5e7e-298">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="c5e7e-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="c5e7e-299">셀 위에서 tooexecute에 걸린 시간: 14.43 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="c5e7e-300">**표준 메트릭 사용 하 여 hello 이진 분류 모델 평가**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-300">**Evaluate hello binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="c5e7e-301">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-301">**OUTPUT:**</span></span> 

<span data-ttu-id="c5e7e-302">Area under PR = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="c5e7e-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="c5e7e-303">Area under ROC = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="c5e7e-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="c5e7e-304">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="c5e7e-304">Summary Stats</span></span>

<span data-ttu-id="c5e7e-305">Precision = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="c5e7e-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="c5e7e-306">Recall = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="c5e7e-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="c5e7e-307">F1 Score = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="c5e7e-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="c5e7e-308">셀 위에서 tooexecute에 걸린 시간: 57.61 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="c5e7e-309">**Hello ROC 곡선을 그립니다.**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="c5e7e-310">hello *predictionAndLabelsDF* 테이블로 등록 *tmp_results*, hello 이전 셀에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="c5e7e-311">*tmp_results* toodo 사용 되는 쿼리 수 있고 hello sqlResults 데이터-프레임으로 그래프에 표시 하는 것에 대 한 결과 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="c5e7e-312">Hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="c5e7e-313">다음은 hello 코드 toomake 예측 및 플롯 hello ROC 곡선입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


<span data-ttu-id="c5e7e-314">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-314">**OUTPUT:**</span></span>

![로지스틱 회귀 ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="c5e7e-316">임의 포리스트 분류</span><span class="sxs-lookup"><span data-stu-id="c5e7e-316">Random forest classification</span></span>
<span data-ttu-id="c5e7e-317">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부를 예측 하는 임의 포리스트 모델을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

<span data-ttu-id="c5e7e-318">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-318">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-319">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="c5e7e-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="c5e7e-320">셀 위에서 tooexecute에 걸린 시간: 31.09 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="c5e7e-321">그라데이션 향상 트리 분류</span><span class="sxs-lookup"><span data-stu-id="c5e7e-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="c5e7e-322">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부를 예측 하는 그라데이션 승격 트리 모델을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


<span data-ttu-id="c5e7e-323">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-323">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-324">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="c5e7e-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="c5e7e-325">셀 위에서 tooexecute에 걸린 시간: 19.76 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="c5e7e-326">회귀 모델로 Taxi Trip에 대한 팁 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="c5e7e-327">이 섹션에서는 다른 팁 기능을 기반으로 택시 여정에 대해 지불한 hello 팁 hello 양을 예측 hello 회귀 작업에 대 한 3 개 사용 하 여 모델링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="c5e7e-328">제공 된 hello 모델은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-328">hello models presented are:</span></span>

* <span data-ttu-id="c5e7e-329">정칙 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="c5e7e-329">Regularized linear regression</span></span>
* <span data-ttu-id="c5e7e-330">임의 포리스트</span><span class="sxs-lookup"><span data-stu-id="c5e7e-330">Random forest</span></span>
* <span data-ttu-id="c5e7e-331">그라데이션 향상 트리</span><span class="sxs-lookup"><span data-stu-id="c5e7e-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="c5e7e-332">이러한 모델은 hello 소개에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-332">These models were described in hello introduction.</span></span> <span data-ttu-id="c5e7e-333">코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="c5e7e-334">**모델 교육** 데이터</span><span class="sxs-lookup"><span data-stu-id="c5e7e-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="c5e7e-335">**모델 평가** </span><span class="sxs-lookup"><span data-stu-id="c5e7e-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="c5e7e-336">**모델 저장** </span><span class="sxs-lookup"><span data-stu-id="c5e7e-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="c5e7e-337">SGD로 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="c5e7e-337">Linear regression with SGD</span></span>
<span data-ttu-id="c5e7e-338">hello이 섹션의 코드를 보여 줍니다 toouse 확장 되는 방식 기능 tootrain 추측 기울기 하강 (SGD) 최적화를 위해 사용 하는 선형 회귀 방법을 tooscore, 평가 및 Azure Blob 저장소 (WASB) hello 모델을 저장 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="c5e7e-339">경험에 따르면 LinearRegressionWithSGD 모델의 hello 수렴 문제가 있을 수 있으며 매개 변수 변경 된/최적화 된 신중 하 게 유효한 모델을 얻기 위한 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="c5e7e-340">변수의 크기를 조정하면 수렴에 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="c5e7e-341">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-341">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="c5e7e-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="c5e7e-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="c5e7e-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="c5e7e-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="c5e7e-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="c5e7e-345">R-sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="c5e7e-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="c5e7e-346">셀 위에서 tooexecute에 걸린 시간: 58.42 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="c5e7e-347">임의 포리스트 회귀</span><span class="sxs-lookup"><span data-stu-id="c5e7e-347">Random Forest regression</span></span>
<span data-ttu-id="c5e7e-348">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 데이터에 대 한 팁 금액을 예측 하는 임의 포리스트 회귀를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

<span data-ttu-id="c5e7e-349">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-349">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="c5e7e-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="c5e7e-351">R-sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="c5e7e-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="c5e7e-352">셀 위에서 tooexecute에 걸린 시간: 49.21 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="c5e7e-353">그라데이션 향상 트리 회귀</span><span class="sxs-lookup"><span data-stu-id="c5e7e-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="c5e7e-354">이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 데이터에 대 한 팁 금액을 예측 하는 그라데이션 승격 트리 모델을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="c5e7e-355">**학습 및 평가**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="c5e7e-356">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-356">**OUTPUT:**</span></span>

<span data-ttu-id="c5e7e-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="c5e7e-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="c5e7e-358">R-sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="c5e7e-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="c5e7e-359">셀 위에서 tooexecute에 걸린 시간: 34.52 초</span><span class="sxs-lookup"><span data-stu-id="c5e7e-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="c5e7e-360">**그림**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-360">**Plot**</span></span>

<span data-ttu-id="c5e7e-361">*tmp_results* hello 이전 셀의 Hive 테이블으로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="c5e7e-362">Hello 테이블의 결과가 hello에 출력 되는 *sqlResults* 그리기에 대 한 데이터 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="c5e7e-363">다음은 hello 코드</span><span class="sxs-lookup"><span data-stu-id="c5e7e-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="c5e7e-364">Hello Jupyter 서버를 사용 하 여 hello 코드 tooplot hello 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="c5e7e-365">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="c5e7e-367">메모리에서 개체 정리</span><span class="sxs-lookup"><span data-stu-id="c5e7e-367">Clean up objects from memory</span></span>
<span data-ttu-id="c5e7e-368">사용 하 여 `unpersist()` toodelete 개체 메모리에 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="c5e7e-369">소비와 점수 매기기에 대 한 hello 모델의 저장소 위치 레코드</span><span class="sxs-lookup"><span data-stu-id="c5e7e-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="c5e7e-370">독립적인 데이터 집합을 사용 하 여 hello에 설명 된 점수와 tooconsume [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md) toocopy 및 이러한 파일 이름을 hello에 여기에 생성 된 포함 된 저장 hello 모델 붙여넣기 필요한 항목 Jupyter 노트북을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="c5e7e-371">Hello 코드 tooprint 발생 해야 하는 hello 경로 toomodel 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="c5e7e-372">**출력**</span><span class="sxs-lookup"><span data-stu-id="c5e7e-372">**OUTPUT**</span></span>

<span data-ttu-id="c5e7e-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="c5e7e-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="c5e7e-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="c5e7e-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="c5e7e-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="c5e7e-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="c5e7e-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="c5e7e-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="c5e7e-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="c5e7e-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="c5e7e-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="c5e7e-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="c5e7e-379">다음 작업</span><span class="sxs-lookup"><span data-stu-id="c5e7e-379">What's next?</span></span>
<span data-ttu-id="c5e7e-380">준비 toolearn 어떻게는 Spark MlLib hello로 분류 및 회귀 모델을 만든 tooscore 하 고 이러한 모델을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="c5e7e-381">고급 데이터 탐색 및 교차 유효성 검사, 하이퍼 매개 변수를 포함 하 여으로 깊은 노트북 다이브 모델링 hello 스윕, 및 평가 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="c5e7e-382">**소비 모델:** toolearn 어떻게 tooscore이이 항목에서 만든 hello 분류 및 회귀 모델을 평가 하 고, 참조 및 [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="c5e7e-383">**교차 유효성 검사 및 하이퍼 매개 변수 비우기**: 교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습하는 방법은 [Spark로 고급 데이터 탐색 및 모델링](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5e7e-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

