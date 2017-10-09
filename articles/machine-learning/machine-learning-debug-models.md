---
title: "aaaDebug Azure 기계 학습에서 모델 | Microsoft Docs"
description: "어떻게 toodebug 발생 한 오류로 인해 모델 학습 및 점수 모델에서 Azure 기계 학습의 모듈입니다."
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
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="bed78-103">Azure 기계 학습에서 모델 디버그</span><span class="sxs-lookup"><span data-stu-id="bed78-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="bed78-104">이 문서에서는 이유 hello 두 개의 오류를 다음 중 하나가 발생할 수 있습니다 모델을 실행 하는 hello 잠재적인 이유를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="bed78-105">hello [모델 학습] [ train-model] 오류를 생성 하는 모듈</span><span class="sxs-lookup"><span data-stu-id="bed78-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="bed78-106">hello [모델 점수 매기기] [ score-model] 모듈에 잘못 된 결과가 생성</span><span class="sxs-lookup"><span data-stu-id="bed78-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="bed78-107">모델 학습 모듈에서 오류 발생</span><span class="sxs-lookup"><span data-stu-id="bed78-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="bed78-109">hello [모델 학습] [ train-model] 모듈에서는 입력이 두 개 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="bed78-110">Azure 기계 학습에서 제공 하는 모델의 hello 컬렉션에서 기계 학습 모델의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="bed78-111">hello 학습 데이터를 지정 하는 지정된 된 레이블 열과 hello 변수 toopredict (hello 다른 열은 않는다고 가정 toobe 기능).</span><span class="sxs-lookup"><span data-stu-id="bed78-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="bed78-112">이 모듈 hello의 경우 다음 오류를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="bed78-113">hello 레이블 열이 잘못 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="bed78-114">이 hello 레이블으로 둘 이상의 열을 선택 또는 잘못 된 열 인덱스를 선택 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="bed78-115">예를 들어 hello 두 번째 경우 30의 열 인덱스에만 25 열이 있는 입력된 데이터 집합에서 사용 되 면 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="bed78-116">hello 데이터 집합 기능 열이 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="bed78-117">예를 들어 hello 입력된 데이터 집합에 hello 레이블 열으로 표시 된 열이 하나만 있는 경우 어떤 toobuild hello 모델 기능이 없습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="bed78-118">이 경우 hello [모델 학습] [ train-model] 모듈에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="bed78-119">hello 입력된 데이터 집합 (기능 또는 레이블) 값으로 무한대를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="bed78-120">모델 점수 매기기 모듈에서 잘못된 결과 생성</span><span class="sxs-lookup"><span data-stu-id="bed78-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="bed78-122">일반적인 학습/테스트 실험에서 지도 학습에 대 한 hello [데이터를 분할] [ split] 모듈 hello 원래 데이터 집합을 두 부분으로 나눕니다: 첫 번째는 사용 되는 tootrain hello 모델 및 한 부분이 사용 됩니다 tooscore 얼마나 잘 hello 학습 된 모델을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="bed78-123">hello 학습 된 모델에 있으면 사용 되는 tooscore hello는 hello 결과 hello 모델의 평가 toodetermine hello 정확도 테스트 데이터.</span><span class="sxs-lookup"><span data-stu-id="bed78-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="bed78-124">hello [모델 점수 매기기] [ score-model] 모듈 두 개의 입력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="bed78-125">Hello에서 학습 된 모델 출력 [모델 학습] [ train-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="bed78-126">Tootrain hello 모델을 사용 하는 hello 데이터 집합의 다른 점수 매기기 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="bed78-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="bed78-127">Hello 실험으로 성공 해도 hello 가능한의 [모델 점수 매기기] [ score-model] 모듈에 잘못 된 결과가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="bed78-128">몇 가지 시나리오는이 toohappen을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="bed78-129">Hello 잘못 된 출력이 생성 되 hello 지정 된 경우 레이블은 범주입니다. 및 hello 데이터에 대 한 회귀 모델을 학습, [모델 점수 매기기] [ score-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="bed78-130">회귀에는 연속 응답 변수가 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="bed78-131">이 경우에 더 적합 한 toouse 분류 모델 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="bed78-132">마찬가지로, 부동 소수점 숫자 hello 레이블 열에 있는 데이터 집합에는 분류 모델을 학습 하는 경우 원하지 않는 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="bed78-133">분류에는 범위가 유한하고 일반적으로 클래스 집합이 작은 값만 허용하는 불연속 응답 변수가 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="bed78-134">데이터 집합 점수 매기기 hello 모든 hello 사용 되는 기능 tootrain hello 모델 없으면 hello [모델 점수 매기기] [ score-model] 에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="bed78-135">데이터 집합 점수 매기기 hello에 행에는 누락 된 값 또는 해당 기능에 대 한 무한 값이 포함 된, hello [모델 점수 매기기] [ score-model] 모든 해당 toothat 행으로 출력을 생성 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="bed78-136">hello [모델 점수 매기기] [ score-model] 동일한 출력 데이터 집합 점수 매기기 hello에서 모든 행에 대해 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="bed78-137">이 발생할 수, 예를 들어 hello 최소 리프 노드당 샘플 수 hello 이상 toobe 사용할 수 있는 학습 예제 수 있다고 표시 하는 경우에 의사 결정 포리스트를 사용 하 여 분류를 시도할 때 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bed78-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

