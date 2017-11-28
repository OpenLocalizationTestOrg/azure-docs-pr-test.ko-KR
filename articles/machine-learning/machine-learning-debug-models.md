---
title: "Azure Machine Learning에서 모델 디버그 | Microsoft Docs"
description: "Azure Machine Learning에서 모델 학습 및 모델 점수 매기기 모듈에 의해 생성된 오류를 디버그하는 방법"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="f2f2d-103">Azure 기계 학습에서 모델 디버그</span><span class="sxs-lookup"><span data-stu-id="f2f2d-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="f2f2d-104">이 문서에서는 모델을 실행할 때 다음 두 가지 오류 중 하나가 발생할 수 있는 잠재적 원인을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="f2f2d-105">[모델 학습] [train-model] 모듈에서 오류 발생</span><span class="sxs-lookup"><span data-stu-id="f2f2d-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="f2f2d-106">[모델 점수 매기기][score-model] 모듈에서 잘못된 결과 생성</span><span class="sxs-lookup"><span data-stu-id="f2f2d-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="f2f2d-107">모델 학습 모듈에서 오류 발생</span><span class="sxs-lookup"><span data-stu-id="f2f2d-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="f2f2d-109">[모델 학습][train-model] 모듈에는 다음 두 가지 입력이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="f2f2d-110">Azure Machine Learning에서 제공하는 모델 컬렉션의 Machine Learning 모델 유형</span><span class="sxs-lookup"><span data-stu-id="f2f2d-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="f2f2d-111">예측할 변수를 지정하는 지정된 레이블 열이 있는 학습 데이터(다른 열은 기능으로 간주됨)</span><span class="sxs-lookup"><span data-stu-id="f2f2d-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="f2f2d-112">다음과 같은 경우 이 모듈에서 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="f2f2d-113">레이블 열이 잘못 지정된 경우.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="f2f2d-114">이는 둘 이상의 열을 레이블로 선택하거나 잘못된 열 인덱스를 선택한 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="f2f2d-115">예를 들어 두 번째 경우는 열이 25개뿐인 입력 데이터 집합에서 열 인덱스 30을 사용한 경우에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="f2f2d-116">데이터 집합에 기능 열이 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="f2f2d-117">예를 들어 입력 데이터 집합에 열이 1개뿐이고 이 열이 레이블 열로 표시된 경우 모델을 빌드할 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="f2f2d-118">이 경우에는 [모델 학습][train-model] 모듈에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="f2f2d-119">입력 데이터 집합(기능 또는 레이블)에 Infinity가 값으로 포함된 경우</span><span class="sxs-lookup"><span data-stu-id="f2f2d-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="f2f2d-120">모델 점수 매기기 모듈에서 잘못된 결과 생성</span><span class="sxs-lookup"><span data-stu-id="f2f2d-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="f2f2d-122">감독 학습에 대한 일반적인 학습/테스트 실험에서 [데이터 분할][split] 모듈은 원래 데이터 집합을 모델을 학습하는 데 사용되는 부분과 학습된 모델이 얼마나 잘 작동하는지 점수를 매기는 데 사용된 부분의 두 부분으로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="f2f2d-123">그런 다음 학습된 모델은 테스트 데이터의 점수를 매기는 데 사용되며, 그 결과가 모델의 정확도를 확인하기 위해 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="f2f2d-124">[모델 점수 매기기][score-model] 모듈에는 다음 두 개의 입력이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="f2f2d-125">[모델 학습][train-model] 모듈의 학습된 모델 출력</span><span class="sxs-lookup"><span data-stu-id="f2f2d-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="f2f2d-126">모델 학습에 사용되는 데이터 집합과는 다른 점수 매기기 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="f2f2d-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="f2f2d-127">실험에 성공한 경우에도 [모델 점수 매기기][score-model] 모듈에서 잘못된 결과가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="f2f2d-128">다음과 같은 여러 시나리오에서 이러한 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="f2f2d-129">지정된 레이블이 범주인 경우 데이터에 대해 회귀 모델이 학습되면 [모델 점수 매기기][score-model] 모듈에서 잘못된 출력이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="f2f2d-130">회귀에는 연속 응답 변수가 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="f2f2d-131">이 경우 분류 모델을 사용하는 것이 보다 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="f2f2d-132">마찬가지로 레이블 열에 부동 소수점 숫자가 있는 데이터 집합에 대해 분류 모델이 학습된 경우 바람직하지 않은 결과가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="f2f2d-133">분류에는 범위가 유한하고 일반적으로 클래스 집합이 작은 값만 허용하는 불연속 응답 변수가 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="f2f2d-134">점수 매기기 데이터 집합에 모델을 학습하는 데 사용되는 일부 기능이 포함되지 않은 경우 [모델 점수 매기기][score-model]에서 오류가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="f2f2d-135">점수 매기기 데이터 집합의 행에 해당 기능 중 하나에 대한 무한대 값 또는 누락된 값이 있는 경우 [모델 점수 매기기][score-model]에서 해당 행에 대한 출력이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="f2f2d-136">[모델 점수 매기기][score-model]에서는 점수 매기기 데이터 집합의 모든 행에 대해 동일한 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="f2f2d-137">예를 들어 선택한 리프 노드당 최소 샘플 수가 사용 가능한 학습 예제 수보다 많은 경우 의사 결정 포리스트를 사용하여 분류할 때 이러한 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f2d-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

