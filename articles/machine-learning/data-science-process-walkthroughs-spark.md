---
title: "Azure에서 PySpark 및 Scala를 사용하여 HDInsight Spark 연습 | Microsoft Docs"
description: "예측 분석을 수행하기 위해 Azure HDInsight Spark에서 PySpark 및 Scala 사용을 보여 주는 Team Data Science Process의 예제입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 27065c3437c4617ed035623b48aa1a1a31a7094f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a><span data-ttu-id="0cdd1-103">Azure에서 PySpark 및 Scala를 사용하여 HDInsight Spark 데이터 과학 연습</span><span class="sxs-lookup"><span data-stu-id="0cdd1-103">HDInsight Spark data science walkthroughs using PySpark and Scala on Azure</span></span>

<span data-ttu-id="0cdd1-104">이러한 연습에서는 Azure Spark 클러스터에서 PySpark 및 Scala를 사용하여 예측 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-104">These walkthroughs use PySpark and Scala on an Azure Spark cluster to do predictive analytics.</span></span> <span data-ttu-id="0cdd1-105">Team Data Science Process에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="0cdd1-106">Team Data Science Process의 개요는 [데이터 과학 프로세스](data-science-process-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="0cdd1-107">HDInsight의 Spark 개요는 [HDInsight의 Spark 소개](../hdinsight/hdinsight-apache-spark-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-107">For an overview of Spark on HDInsight, see [Introduction to Spark on HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).</span></span>

<span data-ttu-id="0cdd1-108">Team Data Science Process를 실행하는 추가 데이터 과학 연습은 사용하는 **플랫폼**에 따라 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a><span data-ttu-id="0cdd1-109">Azure Spark에서 PySpark를 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="0cdd1-109">Predict taxi tips using PySpark on Azure Spark</span></span>

<span data-ttu-id="0cdd1-110">[Azure HDInsight에서 Spark 사용](machine-learning-data-science-spark-overview.md) 연습은 뉴욕 택시의 데이터를 사용하여 팁 지불 여부 및 예상되는 지불 금액의 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-110">The [Use Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) walkthrough uses data from New York taxis to predict whether a tip is paid and the range of amounts expected to be paid.</span></span> <span data-ttu-id="0cdd1-111">[Azure HDInsight Spark 클러스터](https://azure.microsoft.com/services/hdinsight/)를 사용하는 시나리오에서 Team Data Science Process를 사용하여 공개적으로 사용 가능한 NYC Taxi Trip 및 요금 데이터 집합에서 데이터를 저장, 탐색 및 기능 엔지니어링합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-111">It uses the Team Data Science Process in a scenario using an [Azure HDInsight Spark cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, and feature engineer data from the publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="0cdd1-112">이 개요 항목은 연습의 나머지 부분에서 사용되는 HDInsight Spark 클러스터와 Jupyter PySpark 노트북을 사용하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-112">This overview topic sets you up with an HDInsight Spark cluster and the Jupyter  PySpark notebooks used in the rest of the walkthrough.</span></span> <span data-ttu-id="0cdd1-113">이러한 노트북은 데이터 탐색 방법을 보여 준 후 모델을 만들고 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-113">These notebooks show you how to explore your data and then how to create and consume models.</span></span> <span data-ttu-id="0cdd1-114">고급 데이터 탐색 및 모델링 Notebook은 교차 유효성 검사, 하이퍼 매개 변수 비우기 및 모델 평가를 포함하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-114">The advanced data exploration and modeling notebook shows how to include cross-validation, hyper-parameter sweeping, and model evaluation.</span></span>

### <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="0cdd1-115">Spark로 데이터 탐색 및 모델링</span><span class="sxs-lookup"><span data-stu-id="0cdd1-115">Data Exploration and modeling with Spark</span></span> 
<span data-ttu-id="0cdd1-116">[Spark MLlib 도구 키트를 사용하여 데이터에 대한 이진 분류 및 회귀 모델 만들기](machine-learning-data-science-spark-data-exploration-modeling.md) 항목을 수행하여 데이터 집합을 탐색하고 기계 학습 모델 만들기, 점수 매기기 및 평가를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-116">Explore the dataset and create, score, and evaluate the machine learning models by working through the [Create binary classification and regression models for data with the Spark MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span>

### <a name="model-consumption"></a><span data-ttu-id="0cdd1-117">모델 사용</span><span class="sxs-lookup"><span data-stu-id="0cdd1-117">Model consumption</span></span>
<span data-ttu-id="0cdd1-118">이 항목에서 만든 분류 및 회귀 모델의 점수를 매기는 방법을 알아보려면 [Spark로 빌드된 기계 학습 모델 점수 매기기 및 평가](machine-learning-data-science-spark-model-consumption.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-118">To learn how to score the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

### <a name="cross-validation-and-hyperparameter-sweeping"></a><span data-ttu-id="0cdd1-119">교차 유효성 검사 및 하이퍼 매개 변수 비우기</span><span class="sxs-lookup"><span data-stu-id="0cdd1-119">Cross-validation and hyperparameter sweeping</span></span>
<span data-ttu-id="0cdd1-120">교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습하는 방법은 [Spark로 고급 데이터 탐색 및 모델링](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-120">See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a><span data-ttu-id="0cdd1-121">Azure Spark에서 Scala를 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="0cdd1-121">Predict taxi tips using Scala on Azure Spark</span></span>

<span data-ttu-id="0cdd1-122">[Azure에서 Spark와 함께 Scala 사용](machine-learning-data-science-process-scala-walkthrough.md) 연습은 뉴욕 택시의 데이터를 사용하여 팁 지불 여부 및 예상되는 지불 금액의 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-122">The [Use Scala with Spark on Azure](machine-learning-data-science-process-scala-walkthrough.md) walkthrough uses data from New York taxis to predict whether a tip is paid and the range of amounts expected to be paid.</span></span> <span data-ttu-id="0cdd1-123">Azure HDInsight Spark 클러스터에서 Spark MLlib(Machine Learning 라이브러리) 및 SparkML 패키지를 사용하여 감독 Machine Learning 작업에 대해 Scala를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-123">It shows how to use Scala for supervised machine learning tasks with the Spark machine learning library (MLlib) and SparkML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="0cdd1-124">[데이터 과학 프로세스](http://aka.ms/datascienceprocess): 데이터 수집 및 탐색, 시각화, 기능 엔지니어링, 모델링, 모델 사용으로 이루어진 작업을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-124">It walks you through the tasks that constitute the [Data Science Process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="0cdd1-125">작성된 모델은 로지스틱 및 선형 회귀, 임의 포리스트 및 그라데이션 향상된 트리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-125">The models built include logistic and linear regression, random forests, and gradient boosted trees.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0cdd1-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cdd1-126">Next steps</span></span>

<span data-ttu-id="0cdd1-127">Team Data Science Process를 구성하는 주요 구성의 논의는 [Team Data Science Process 개요](data-science-process-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-127">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="0cdd1-128">데이터 과학 프로젝트를 구성하는 데 사용할 수 있는 Team Data Science Process 수명 주기의 논의는 [Team Data Science Process 수명 주기](data-science-process-lifecycle.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-128">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="0cdd1-129">수명 주기는 일반적으로 프로젝트가 실행될 때 시작부터 끝까지 따라야 하는 단계를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0cdd1-129">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

