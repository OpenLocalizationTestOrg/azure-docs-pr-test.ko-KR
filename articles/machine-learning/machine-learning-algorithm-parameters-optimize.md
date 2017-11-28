---
title: "Azure Machine Learning에서 알고리즘 최적화 | Microsoft Docs"
description: "Azure 기계 학습에서 알고리즘에 대한 최적 매개 변수 집합을 선택하는 방법에 대해 설명합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b3be7f31ac31c656744fb809e3972af0ac4ad4f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="choose-parameters-to-optimize-your-algorithms-in-azure-machine-learning"></a><span data-ttu-id="7fc21-103">Azure Machine Learning에서 알고리즘을 최적화하는 매개 변수 선택</span><span class="sxs-lookup"><span data-stu-id="7fc21-103">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>
<span data-ttu-id="7fc21-104">이 토픽에서는 Azure Machine Learning에서 알고리즘에 대한 올바른 하이퍼 매개 변수 집합을 선택하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-104">This topic describes how to choose the right hyperparameter set for an algorithm in Azure Machine Learning.</span></span> <span data-ttu-id="7fc21-105">대부분의 기계 학습 알고리즘은 설정할 매개 변수를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-105">Most machine learning algorithms have parameters to set.</span></span> <span data-ttu-id="7fc21-106">모델을 학습할 때 이러한 매개 변수의 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-106">When you train a model, you need to provide values for those parameters.</span></span> <span data-ttu-id="7fc21-107">학습된 모델의 효율성은 선택한 모델 매개 변수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-107">The efficacy of the trained model depends on the model parameters that you choose.</span></span> <span data-ttu-id="7fc21-108">최적의 매개 변수 집합을 찾는 프로세스를 *모델 선택*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-108">The process of finding the optimal set of parameters is known as *model selection*.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="7fc21-109">모델 선택 영역을 수행하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-109">There are various ways to do model selection.</span></span> <span data-ttu-id="7fc21-110">Machine Learning에서는 교차 유효성 검사가 모델 선택에 가장 널리 사용되는 방법 중 하나이며, Azure Machine Learning의 기본 모델 선택 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-110">In machine learning, cross-validation is one of the most widely used methods for model selection, and it is the default model selection mechanism in Azure Machine Learning.</span></span> <span data-ttu-id="7fc21-111">Azure Machine Learning에서는 R과 Python을 둘 다 지원하므로 언제든지 R 또는 Python을 사용하여 고유한 모델 선택 메커니즘을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-111">Because Azure Machine Learning supports both R and Python, you can always implement their own model selection mechanisms by using either R or Python.</span></span>

<span data-ttu-id="7fc21-112">최상의 매개 변수 집합을 찾는 프로세스는 4단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-112">There are four steps in the process of finding the best parameter set:</span></span>

1. <span data-ttu-id="7fc21-113">**매개 변수 공간 정의**: 먼저 알고리즘에 대해 고려할 정확한 매개 변수 값을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-113">**Define the parameter space**: For the algorithm, first decide the exact parameter values you want to consider.</span></span>
2. <span data-ttu-id="7fc21-114">**교차 유효성 검사 설정 정의**: 데이터 집합에 대해 교차 유효성 검사 접기를 선택하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-114">**Define the cross-validation settings**: Decide how to choose cross-validation folds for the dataset.</span></span>
3. <span data-ttu-id="7fc21-115">**메트릭 정의**: 최상의 매개 변수 집합(예: 정확도, 평균 제곱근 오차, 정밀도, 재현율 또는 f-score)을 결정하는 데 사용할 메트릭을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-115">**Define the metric**: Decide what metric to use for determining the best set of parameters, such as accuracy, root mean squared error, precision, recall, or f-score.</span></span>
4. <span data-ttu-id="7fc21-116">**학습, 평가 및 비교**: 매개 변수 값의 각 고유한 조합에 대해 정의한 오류 메트릭을 기반으로 교차 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-116">**Train, evaluate, and compare**: For each unique combination of the parameter values, cross-validation is carried out by and based on the error metric you define.</span></span> <span data-ttu-id="7fc21-117">평가 및 비교 후에 최고 성능 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-117">After evaluation and comparison, you can choose the best-performing model.</span></span>

<span data-ttu-id="7fc21-118">다음 이미지에서는 Azure Machine Learning에서 이를 수행할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-118">The following image illustrates shows how this can be achieved in Azure Machine Learning.</span></span>

![최상의 매개 변수 집합 찾기](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-the-parameter-space"></a><span data-ttu-id="7fc21-120">매개 변수 공간 정의</span><span class="sxs-lookup"><span data-stu-id="7fc21-120">Define the parameter space</span></span>
<span data-ttu-id="7fc21-121">모델 초기화 단계에서 매개 변수 집합을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-121">You can define the parameter set at the model initialization step.</span></span> <span data-ttu-id="7fc21-122">모든 Machine Learning 알고리즘의 매개 변수 창에는 두 가지 강사 모드(*단일 매개 변수* 및 *매개 변수 범위*)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-122">The parameter pane of all machine learning algorithms has two trainer modes: *Single Parameter* and *Parameter Range*.</span></span> <span data-ttu-id="7fc21-123">매개 변수 범위 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-123">Choose Parameter Range mode.</span></span> <span data-ttu-id="7fc21-124">매개 변수 범위 모드에서는 각 매개 변수에 대한 여러 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-124">In Parameter Range mode, you can enter multiple values for each parameter.</span></span> <span data-ttu-id="7fc21-125">텍스트 상자에서 쉼표로 구분된 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-125">You can enter comma-separated values in the text box.</span></span>

![2클래스 향상된 의사 결정 트리, 단일 매개 변수](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 <span data-ttu-id="7fc21-127">또는 **범위 작성기 사용**을 사용하여 그리드의 최대 및 최소 요소 수와 생성할 총 요소 수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-127">Alternately, you can define the maximum and minimum points of the grid and the total number of points to be generated with **Use Range Builder**.</span></span> <span data-ttu-id="7fc21-128">기본적으로 매개 변수 값은 선형 눈금으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-128">By default, the parameter values are generated on a linear scale.</span></span> <span data-ttu-id="7fc21-129">그러나 **로그 규모** 상자를 선택한 경우에는 로그 규모에서 값이 생성됩니다(즉, 인접 요소의 비율이 차이가 나지 않고 일정함).</span><span class="sxs-lookup"><span data-stu-id="7fc21-129">But if **Log Scale** is checked, the values are generated in the log scale (that is, the ratio of the adjacent points is constant instead of their difference).</span></span> <span data-ttu-id="7fc21-130">정수 매개 변수의 경우 하이픈을 사용하여 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-130">For integer parameters, you can define a range by using a hyphen.</span></span> <span data-ttu-id="7fc21-131">예를 들어, "1-10"은 1에서 10(모두 포함) 사이의 모든 정수가 매개 변수 집합을 형성함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-131">For example, “1-10” means that all integers between 1 and 10 (both inclusive) form the parameter set.</span></span> <span data-ttu-id="7fc21-132">혼합 모드도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-132">A mixed mode is also supported.</span></span> <span data-ttu-id="7fc21-133">예를 들어, "1-10, 20, 50"으로 설정된 매개 변수는 정수 1-10, 20, 50을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-133">For example, the parameter set “1-10, 20, 50” would include integers 1-10, 20, and 50.</span></span>

![2클래스 향상된 의사 결정 트리, 매개 변수 범위](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a><span data-ttu-id="7fc21-135">교차 유효성 검사 접기 정의</span><span class="sxs-lookup"><span data-stu-id="7fc21-135">Define cross-validation folds</span></span>
<span data-ttu-id="7fc21-136">[파티션 및 샘플][partition-and-sample] 모듈을 사용하여 데이터에 접기 수를 임의로 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-136">The [Partition and Sample][partition-and-sample] module can be used to randomly assign folds to the data.</span></span> <span data-ttu-id="7fc21-137">모듈에 대한 다음 샘플 구성에는 다섯 번 접기를 정의하고 샘플 인스턴스에 접기 수를 임의로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-137">In the following sample configuration for the module, we define five folds and randomly assign a fold number to the sample instances.</span></span>

![파티션 및 샘플](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-the-metric"></a><span data-ttu-id="7fc21-139">메트릭 정의</span><span class="sxs-lookup"><span data-stu-id="7fc21-139">Define the metric</span></span>
<span data-ttu-id="7fc21-140">[모델 조정 하이퍼 매개 변수][tune-model-hyperparameters] 모듈에서는 주어진 알고리즘 및 데이터 집합에 대한 최상의 매개 변수 집합을 경험적으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-140">The [Tune Model Hyperparameters][tune-model-hyperparameters] module provides support for empirically choosing the best set of parameters for a given algorithm and dataset.</span></span> <span data-ttu-id="7fc21-141">이 모듈의 **속성** 창에는 모델 학습에 관련된 기타 정보 외에 최상의 매개 변수 집합을 결정하는 데 사용할 메트릭이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-141">In addition to other information regarding training the model, the **Properties** pane of this module includes the metric for determining the best parameter set.</span></span> <span data-ttu-id="7fc21-142">분류 및 회귀 알고리즘 각각에 대한 두 개의 드롭다운 목록 상자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-142">It has two different drop-down list boxes for classification and regression algorithms, respectively.</span></span> <span data-ttu-id="7fc21-143">고려 중인 알고리즘은 분류 알고리즘인 경우에는 회귀 메트릭이 무시되고 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-143">If the algorithm under consideration is a classification algorithm, the regression metric is ignored and vice versa.</span></span> <span data-ttu-id="7fc21-144">이 특정 예제에서는 메트릭은 **정확도**입니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-144">In this specific example, the metric is **Accuracy**.</span></span>   

![매개 변수 비우기](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a><span data-ttu-id="7fc21-146">학습, 평가 및 비교</span><span class="sxs-lookup"><span data-stu-id="7fc21-146">Train, evaluate, and compare</span></span>
<span data-ttu-id="7fc21-147">동일한 [Tune Model Hyperparameters][tune-model-hyperparameters] 모듈이 매개 변수 집합에 해당하는 모든 모델을 학습하고, 여러 메트릭을 평가한 다음, 선택한 메트릭을 기반으로 최상의 학습된 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-147">The same [Tune Model Hyperparameters][tune-model-hyperparameters] module trains all the models that correspond to the parameter set, evaluates various metrics, and then creates the best-trained model based on the metric you choose.</span></span> <span data-ttu-id="7fc21-148">이 모듈에는 다음 두 개의 필수 입력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-148">This module has two mandatory inputs:</span></span>

* <span data-ttu-id="7fc21-149">미숙한 학습자</span><span class="sxs-lookup"><span data-stu-id="7fc21-149">The untrained learner</span></span>
* <span data-ttu-id="7fc21-150">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="7fc21-150">The dataset</span></span>

<span data-ttu-id="7fc21-151">또한 이 모듈은 선택적 데이터 집합 입력을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-151">The module also has an optional dataset input.</span></span> <span data-ttu-id="7fc21-152">접기 정보가 있는 데이터 집합을 필수 데이터 집합 입력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-152">Connect the dataset with fold information to the mandatory dataset input.</span></span> <span data-ttu-id="7fc21-153">데이터 집합에 접기 정보가 할당되지 않은 경우에는 기본적으로는 10번 접기 교차 유효성 검사가 자동으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-153">If the dataset is not assigned any fold information, then a 10-fold cross-validation is automatically executed by default.</span></span> <span data-ttu-id="7fc21-154">접기 할당이 수행되지 않고 유효성 검사 데이터 집합이 최적의 데이터 집합 포트에서 제공된 경우에는 학습 테스트 모드가 선택되고 첫 번째 데이터 집합이 각 매개 변수 조합에 대한 모델의 학습에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-154">If the fold assignment is not done and a validation dataset is provided at the optional dataset port, then a train-test mode is chosen and the first dataset is used to train the model for each parameter combination.</span></span>

![향상된 의사 결정 트리 분류자](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

<span data-ttu-id="7fc21-156">이 모델은 유효성 검사 데이터 집합에서 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-156">The model is then evaluated on the validation dataset.</span></span> <span data-ttu-id="7fc21-157">모듈의 왼쪽 출력 포트에는 매개 변수 값 함수로 다양한 메트릭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-157">The left output port of the module shows different metrics as functions of parameter values.</span></span> <span data-ttu-id="7fc21-158">오른쪽 출력 포트에는 선택한 메트릭(이 예의 경우 **정확도**)에 따라 최고 성능의 모델에 해당하는 학습된 모델이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-158">The right output port gives the trained model that corresponds to the best-performing model according to the chosen metric (**Accuracy** in this case).</span></span>  

![유효성 검사 데이터 집합](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

<span data-ttu-id="7fc21-160">오른쪽 출력 포트를 시각화하여 선택한 정확한 매개 변수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-160">You can see the exact parameters chosen by visualizing the right output port.</span></span> <span data-ttu-id="7fc21-161">이 모델은 테스트 집합을 채점하거나 학습된 모델로 저장한 후 조작 가능한 웹 서비스를 제공하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc21-161">This model can be used in scoring a test set or in an operationalized web service after saving as a trained model.</span></span>

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
