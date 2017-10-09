---
title: "aaaOptimize Azure 기계 학습에서 알고리즘 | Microsoft Docs"
description: "Azure 기계 학습에서 알고리즘에 대 한 toochoose hello 최적의 매개 변수 설정 하는 방법에 대해 설명 합니다."
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
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a><span data-ttu-id="62824-103">Azure 기계 학습에서 매개 변수 toooptimize 알고리즘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-103">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>
<span data-ttu-id="62824-104">이 항목에서는 Azure 기계 학습에서 알고리즘에 대 한 toochoose hello 오른쪽 hyperparameter 설정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-104">This topic describes how toochoose hello right hyperparameter set for an algorithm in Azure Machine Learning.</span></span> <span data-ttu-id="62824-105">대부분 기계 학습 알고리즘 매개 변수 tooset이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-105">Most machine learning algorithms have parameters tooset.</span></span> <span data-ttu-id="62824-106">모델을 학습 하는 경우 해당 매개 변수에 대 한 tooprovide 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-106">When you train a model, you need tooprovide values for those parameters.</span></span> <span data-ttu-id="62824-107">hello 학습 된 모델의 hello 효율성 hello 모델 매개 변수를 선택 하면에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="62824-107">hello efficacy of hello trained model depends on hello model parameters that you choose.</span></span> <span data-ttu-id="62824-108">hello hello 최적의 매개 변수 집합을 찾는 작업 이라고 *선택 모델*합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-108">hello process of finding hello optimal set of parameters is known as *model selection*.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="62824-109">다양 한 방법으로 toodo 모델 선택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-109">There are various ways toodo model selection.</span></span> <span data-ttu-id="62824-110">기계 학습에서 교차 유효성 검사는 모델 선택에 대 한 hello 가장 널리 사용 되는 메서드 중 하나 이므로 Azure 기계 학습에서 hello 기본 모델 선택 메커니즘.</span><span class="sxs-lookup"><span data-stu-id="62824-110">In machine learning, cross-validation is one of hello most widely used methods for model selection, and it is hello default model selection mechanism in Azure Machine Learning.</span></span> <span data-ttu-id="62824-111">Azure Machine Learning에서는 R과 Python을 둘 다 지원하므로 언제든지 R 또는 Python을 사용하여 고유한 모델 선택 메커니즘을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-111">Because Azure Machine Learning supports both R and Python, you can always implement their own model selection mechanisms by using either R or Python.</span></span>

<span data-ttu-id="62824-112">Hello hello 최상의 매개 변수 집합을 찾는 과정에서 네 단계는</span><span class="sxs-lookup"><span data-stu-id="62824-112">There are four steps in hello process of finding hello best parameter set:</span></span>

1. <span data-ttu-id="62824-113">**Hello 매개 변수 공간 정의**: hello 알고리즘에 대 한 hello 정확한 매개 변수 값을 원하는 tooconsider 먼저 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-113">**Define hello parameter space**: For hello algorithm, first decide hello exact parameter values you want tooconsider.</span></span>
2. <span data-ttu-id="62824-114">**Hello 교차 유효성 검사 설정을 정의 합니다.**: toochoose 교차 유효성 검사 hello 데이터 집합에 대 한 정리 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-114">**Define hello cross-validation settings**: Decide how toochoose cross-validation folds for hello dataset.</span></span>
3. <span data-ttu-id="62824-115">**Hello 메트릭을 정의**: hello 최상의 집합이 정확도 등의 매개 변수를 확인 하기 위한 어떤 메트릭 toouse 결정, 오류, 정밀도, 회수, 또는 f-점수 제곱 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="62824-115">**Define hello metric**: Decide what metric toouse for determining hello best set of parameters, such as accuracy, root mean squared error, precision, recall, or f-score.</span></span>
4. <span data-ttu-id="62824-116">**학습, 평가 및 비교**: hello 매개 변수 값의 각 고유 조합에 대 한 교차 유효성 검사에 의해 수행 이며 hello 오류 메트릭을 정의한 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-116">**Train, evaluate, and compare**: For each unique combination of hello parameter values, cross-validation is carried out by and based on hello error metric you define.</span></span> <span data-ttu-id="62824-117">평가 후 비교, hello 최고 성능의 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-117">After evaluation and comparison, you can choose hello best-performing model.</span></span>

<span data-ttu-id="62824-118">다음 이미지는 hello Azure 기계 학습에서 수행할 수 있습니다 어떻게 표시를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62824-118">hello following image illustrates shows how this can be achieved in Azure Machine Learning.</span></span>

![Hello 최상의 매개 변수 집합 찾기](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a><span data-ttu-id="62824-120">Hello 매개 변수 공간 정의</span><span class="sxs-lookup"><span data-stu-id="62824-120">Define hello parameter space</span></span>
<span data-ttu-id="62824-121">Hello 모델 초기화 단계에서 설정 하는 hello 매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-121">You can define hello parameter set at hello model initialization step.</span></span> <span data-ttu-id="62824-122">hello 모든 기계 학습 알고리즘의 매개 변수 창에 두 가지 트레이너 모드: *단일 매개 변수* 및 *매개 변수 범위*합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-122">hello parameter pane of all machine learning algorithms has two trainer modes: *Single Parameter* and *Parameter Range*.</span></span> <span data-ttu-id="62824-123">매개 변수 범위 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-123">Choose Parameter Range mode.</span></span> <span data-ttu-id="62824-124">매개 변수 범위 모드에서는 각 매개 변수에 대한 여러 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-124">In Parameter Range mode, you can enter multiple values for each parameter.</span></span> <span data-ttu-id="62824-125">Hello 텍스트 상자에 쉼표로 구분 된 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-125">You can enter comma-separated values in hello text box.</span></span>

![2클래스 향상된 의사 결정 트리, 단일 매개 변수](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 <span data-ttu-id="62824-127">Hello 최대 및 최소 포인트 hello 그리드 및 hello 포인트 toobe로 생성 된 총 수를 정의할 수 있습니다 또는 **범위 작성기를 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-127">Alternately, you can define hello maximum and minimum points of hello grid and hello total number of points toobe generated with **Use Range Builder**.</span></span> <span data-ttu-id="62824-128">기본적으로 hello 매개 변수 값은 선형 눈금에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62824-128">By default, hello parameter values are generated on a linear scale.</span></span> <span data-ttu-id="62824-129">그러나 **로그 눈금 간격이** 을 선택 하면 hello 값 hello 로그 눈금에 생성 됩니다 (즉, hello의 hello 포인트가입니다 개의 대신 상수).</span><span class="sxs-lookup"><span data-stu-id="62824-129">But if **Log Scale** is checked, hello values are generated in hello log scale (that is, hello ratio of hello adjacent points is constant instead of their difference).</span></span> <span data-ttu-id="62824-130">정수 매개 변수의 경우 하이픈을 사용하여 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-130">For integer parameters, you can define a range by using a hyphen.</span></span> <span data-ttu-id="62824-131">예를 들어, "1-10"은 1과 10 사이의 모든 정수 hello 매개 변수 집합을 이루는 (둘 다 포함).</span><span class="sxs-lookup"><span data-stu-id="62824-131">For example, “1-10” means that all integers between 1 and 10 (both inclusive) form hello parameter set.</span></span> <span data-ttu-id="62824-132">혼합 모드도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="62824-132">A mixed mode is also supported.</span></span> <span data-ttu-id="62824-133">예를 들어, 매개 변수 집합을 hello "1-10, 20, 50" 정수 1-10, 20, 포함 및 50 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-133">For example, hello parameter set “1-10, 20, 50” would include integers 1-10, 20, and 50.</span></span>

![2클래스 향상된 의사 결정 트리, 매개 변수 범위](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a><span data-ttu-id="62824-135">교차 유효성 검사 접기 정의</span><span class="sxs-lookup"><span data-stu-id="62824-135">Define cross-validation folds</span></span>
<span data-ttu-id="62824-136">hello [분할 및 샘플링] [ partition-and-sample] 모듈에 사용 되는 toorandomly 할당 접기 toohello 데이터 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-136">hello [Partition and Sample][partition-and-sample] module can be used toorandomly assign folds toohello data.</span></span> <span data-ttu-id="62824-137">같은 hello 모듈에 대 한 샘플 구성이 hello,에서는 5 개의 접기를 정의 하 고 접기 번호 toohello 샘플 인스턴스를 임의로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-137">In hello following sample configuration for hello module, we define five folds and randomly assign a fold number toohello sample instances.</span></span>

![파티션 및 샘플](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a><span data-ttu-id="62824-139">Hello 메트릭 정의</span><span class="sxs-lookup"><span data-stu-id="62824-139">Define hello metric</span></span>
<span data-ttu-id="62824-140">hello [모델 하이퍼 튜닝] [ tune-model-hyperparameters] 모듈 실험적으로 hello 최상의 매개 변수 집합을 지정 된 알고리즘 및 데이터 집합에 대 한 선택에 대 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-140">hello [Tune Model Hyperparameters][tune-model-hyperparameters] module provides support for empirically choosing hello best set of parameters for a given algorithm and dataset.</span></span> <span data-ttu-id="62824-141">또한 학습 hello에 대 한 tooother 정보 모델을 hello **속성** 이 모듈의 창 hello 측정 하는 hello 최상의 매개 변수 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-141">In addition tooother information regarding training hello model, hello **Properties** pane of this module includes hello metric for determining hello best parameter set.</span></span> <span data-ttu-id="62824-142">분류 및 회귀 알고리즘 각각에 대한 두 개의 드롭다운 목록 상자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-142">It has two different drop-down list boxes for classification and regression algorithms, respectively.</span></span> <span data-ttu-id="62824-143">회귀 메트릭 hello 분류 알고리즘 고려 대상인 hello 알고리즘을 사용 하는 경우 무시 됩니다 하며 그 반대 과정도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-143">If hello algorithm under consideration is a classification algorithm, hello regression metric is ignored and vice versa.</span></span> <span data-ttu-id="62824-144">이 특정 예제 hello 메트릭을 **정확도**합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-144">In this specific example, hello metric is **Accuracy**.</span></span>   

![매개 변수 비우기](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a><span data-ttu-id="62824-146">학습, 평가 및 비교</span><span class="sxs-lookup"><span data-stu-id="62824-146">Train, evaluate, and compare</span></span>
<span data-ttu-id="62824-147">동일한 hello [모델 하이퍼 튜닝] [ tune-model-hyperparameters] 다양 한 메트릭을 평가 다음 hello hello를 기반으로 가장 학습 된 모델을 만듭니다 toohello 매개 변수 집합을 해당 하는 모든 hello 모델을 학습 하는 모듈 선택한 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="62824-147">hello same [Tune Model Hyperparameters][tune-model-hyperparameters] module trains all hello models that correspond toohello parameter set, evaluates various metrics, and then creates hello best-trained model based on hello metric you choose.</span></span> <span data-ttu-id="62824-148">이 모듈에는 다음 두 개의 필수 입력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-148">This module has two mandatory inputs:</span></span>

* <span data-ttu-id="62824-149">학습 되지 않은 학습자 hello</span><span class="sxs-lookup"><span data-stu-id="62824-149">hello untrained learner</span></span>
* <span data-ttu-id="62824-150">hello 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="62824-150">hello dataset</span></span>

<span data-ttu-id="62824-151">hello 모듈에는 선택적 입력 데이터 집합을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-151">hello module also has an optional dataset input.</span></span> <span data-ttu-id="62824-152">접기 정보 toohello 필수 데이터 집합 입력으로 hello 데이터 집합을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="62824-152">Connect hello dataset with fold information toohello mandatory dataset input.</span></span> <span data-ttu-id="62824-153">Hello 데이터 집합에 모든 접기 정보 할당 되지 않은 경우 기본적으로는 10 배로 교차 유효성 검사 실행 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62824-153">If hello dataset is not assigned any fold information, then a 10-fold cross-validation is automatically executed by default.</span></span> <span data-ttu-id="62824-154">Hello 접기 할당에 작업이 수행 되지 않습니다 및 유효성 검사 데이터 집합 hello 선택적 데이터 집합 포트에서 제공 되며, 다음 학습 테스트 모드 선택 되 고 hello 첫 번째 데이터 집합은 각 매개 변수 조합에 대해 사용 되는 tootrain hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="62824-154">If hello fold assignment is not done and a validation dataset is provided at hello optional dataset port, then a train-test mode is chosen and hello first dataset is used tootrain hello model for each parameter combination.</span></span>

![향상된 의사 결정 트리 분류자](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

<span data-ttu-id="62824-156">hello 모델 hello 유효성 검사 데이터 집합에 대해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62824-156">hello model is then evaluated on hello validation dataset.</span></span> <span data-ttu-id="62824-157">hello 매개 변수 값의 함수로 hello 모듈의 출력 포트 가지 다른 메트릭으로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-157">hello left output port of hello module shows different metrics as functions of parameter values.</span></span> <span data-ttu-id="62824-158">hello toohello 최고 성능의 모델 toohello 메트릭 선택에 따라 해당 하는 hello 학습 된 모델을 제공 하는 출력 포트 오른쪽 (**정확도** 이 경우).</span><span class="sxs-lookup"><span data-stu-id="62824-158">hello right output port gives hello trained model that corresponds toohello best-performing model according toohello chosen metric (**Accuracy** in this case).</span></span>  

![유효성 검사 데이터 집합](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

<span data-ttu-id="62824-160">Hello 오른쪽 출력 포트를 시각화가 선택한 hello 정확한 매개 변수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-160">You can see hello exact parameters chosen by visualizing hello right output port.</span></span> <span data-ttu-id="62824-161">이 모델은 테스트 집합을 채점하거나 학습된 모델로 저장한 후 조작 가능한 웹 서비스를 제공하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62824-161">This model can be used in scoring a test set or in an operationalized web service after saving as a trained model.</span></span>

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
