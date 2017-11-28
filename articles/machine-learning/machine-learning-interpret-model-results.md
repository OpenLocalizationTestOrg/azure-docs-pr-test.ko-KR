---
title: "기계 학습에서 모델 결과 aaaInterpret | Microsoft Docs"
description: "어떻게 toochoose hello 최적의 매개 변수를 사용 하 여 및 점수 모델 출력을 시각화 하는 알고리즘에 대 한 설정 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a><span data-ttu-id="aedd5-103">Machine Learning에서 모델 결과 해석</span><span class="sxs-lookup"><span data-stu-id="aedd5-103">Interpret model results in Azure Machine Learning</span></span>
<span data-ttu-id="aedd5-104">이 항목에서는 설명 어떻게 toovisualize Azure 기계 학습 스튜디오에서 예측 결과 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-104">This topic explains how toovisualize and interpret prediction results in Azure Machine Learning Studio.</span></span> <span data-ttu-id="aedd5-105">모델을 학습 하 고 ("hello 모델 점수") 그 위에 예측 수행 후 toounderstand 필요 하 고 hello 예측 결과 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-105">After you have trained a model and done predictions on top of it ("scored hello model"), you need toounderstand and interpret hello prediction result.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="aedd5-106">Azure 기계 학습에는 다음과 같이 네 가지 주된 유형의 기계 학습 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-106">There are four major kinds of machine learning models in Azure Machine Learning:</span></span>

* <span data-ttu-id="aedd5-107">분류</span><span class="sxs-lookup"><span data-stu-id="aedd5-107">Classification</span></span>
* <span data-ttu-id="aedd5-108">클러스터링</span><span class="sxs-lookup"><span data-stu-id="aedd5-108">Clustering</span></span>
* <span data-ttu-id="aedd5-109">회귀</span><span class="sxs-lookup"><span data-stu-id="aedd5-109">Regression</span></span>
* <span data-ttu-id="aedd5-110">추천 시스템</span><span class="sxs-lookup"><span data-stu-id="aedd5-110">Recommender systems</span></span>

<span data-ttu-id="aedd5-111">이 모델 위에 예측에 사용 하는 hello 모듈은:</span><span class="sxs-lookup"><span data-stu-id="aedd5-111">hello modules used for prediction on top of these models are:</span></span>

* <span data-ttu-id="aedd5-112">분류 및 회귀를 위한 [모델 점수 매기기][score-model] 모듈</span><span class="sxs-lookup"><span data-stu-id="aedd5-112">[Score Model][score-model] module for classification and regression</span></span>
* <span data-ttu-id="aedd5-113">[TooClusters 할당] [ assign-to-clusters] 클러스터링에 대 한 모듈</span><span class="sxs-lookup"><span data-stu-id="aedd5-113">[Assign tooClusters][assign-to-clusters] module for clustering</span></span>
* <span data-ttu-id="aedd5-114">추천 시스템을 위한 [매치박스 추천 점수 매기기][score-matchbox-recommender]</span><span class="sxs-lookup"><span data-stu-id="aedd5-114">[Score Matchbox Recommender][score-matchbox-recommender] for recommendation systems</span></span>

<span data-ttu-id="aedd5-115">이 문서에서는 이러한 각 모듈에 대 한 toointerpret 예측 결과 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-115">This document explains how toointerpret prediction results for each of these modules.</span></span> <span data-ttu-id="aedd5-116">이러한 모듈의 개요를 참조 하십시오. [어떻게 toochoose 매개 변수 toooptimize Azure 기계 학습에서 알고리즘](machine-learning-algorithm-parameters-optimize.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-116">For an overview of these modules, see [How toochoose parameters toooptimize your algorithms in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).</span></span>

<span data-ttu-id="aedd5-117">이 항목에서는 예측 해석에 대해 다루지만 모델 평가는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-117">This topic addresses prediction interpretation but not model evaluation.</span></span> <span data-ttu-id="aedd5-118">방법에 대 한 자세한 내용은 tooevaluate 모델 참조 [tooevaluate Azure 기계 학습에서 성능을 모델링 하는 방법을](machine-learning-evaluate-model-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-118">For more information about how tooevaluate your model, see [How tooevaluate model performance in Azure Machine Learning](machine-learning-evaluate-model-performance.md).</span></span>

<span data-ttu-id="aedd5-119">새 tooAzure 기계 학습 하 고 시작 하는 간단한 실험 tooget 만들기 도움말을 참조 하십시오. 필요한 경우 [Azure 기계 학습 스튜디오에서 간단한 실험 만들기](machine-learning-create-experiment.md) Azure 기계 학습 스튜디오에서.</span><span class="sxs-lookup"><span data-stu-id="aedd5-119">If you are new tooAzure Machine Learning and need help creating a simple experiment tooget started, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.</span></span>

## <a name="classification"></a><span data-ttu-id="aedd5-120">분류</span><span class="sxs-lookup"><span data-stu-id="aedd5-120">Classification</span></span>
<span data-ttu-id="aedd5-121">분류 문제의 하위 범주는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-121">There are two subcategories of classification problems:</span></span>

* <span data-ttu-id="aedd5-122">2클래스에만 문제가 있음(2클래스 또는 이진 분류)</span><span class="sxs-lookup"><span data-stu-id="aedd5-122">Problems with only two classes (two-class or binary classification)</span></span>
* <span data-ttu-id="aedd5-123">세 개 이상의 클래스에 문제가 있음(다중 클래스 분류)</span><span class="sxs-lookup"><span data-stu-id="aedd5-123">Problems with more than two classes (multi-class classification)</span></span>

<span data-ttu-id="aedd5-124">Azure 기계 학습 분류를 이러한 유형에 각각의 서로 다른 모듈 toodeal 갖지만 예측 결과 해석 하기 위한 hello 메서드는 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-124">Azure Machine Learning has different modules toodeal with each of these types of classification, but hello methods for interpreting their prediction results are similar.</span></span>

### <a name="two-class-classification"></a><span data-ttu-id="aedd5-125">2클래스 분류</span><span class="sxs-lookup"><span data-stu-id="aedd5-125">Two-class classification</span></span>
<span data-ttu-id="aedd5-126">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="aedd5-126">**Example experiment**</span></span>

<span data-ttu-id="aedd5-127">2 클래스 분류 문제의 경우의 예는 iris 꽃의 hello 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-127">An example of a two-class classification problem is hello classification of iris flowers.</span></span> <span data-ttu-id="aedd5-128">hello 작업은 tooclassify iris 꽃 해당 기능을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-128">hello task is tooclassify iris flowers based on their features.</span></span> <span data-ttu-id="aedd5-129">hello Azure 기계 학습에서 제공 된 Iris 데이터 집합의 하위 집합인 인기 있는 hello [Iris 데이터 집합](http://en.wikipedia.org/wiki/Iris_flower_data_set) 지정 (클래스 0과 1) 화 단 두 개의 전용의 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-129">hello Iris data set provided in Azure Machine Learning is a subset of hello popular [Iris data set](http://en.wikipedia.org/wiki/Iris_flower_data_set) containing instances of only two flower species (classes 0 and 1).</span></span> <span data-ttu-id="aedd5-130">각 꽃에는 네 가지 특징이 있습니다(꽃받침 길이, 꽃받침 너비, 꽃잎 길이 및 꽃잎 너비).</span><span class="sxs-lookup"><span data-stu-id="aedd5-130">There are four features for each flower (sepal length, sepal width, petal length, and petal width).</span></span>

![붓꽃 실험의 스크린샷](./media/machine-learning-interpret-model-results/1.png)

<span data-ttu-id="aedd5-132">그림 1.</span><span class="sxs-lookup"><span data-stu-id="aedd5-132">Figure 1.</span></span> <span data-ttu-id="aedd5-133">붓꽃 2클래스 분류 문제 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-133">Iris two-class classification problem experiment</span></span>

<span data-ttu-id="aedd5-134">실험 되었습니다 수행된 toosolve이이 문제를 그림 1에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-134">An experiment has been performed toosolve this problem, as shown in Figure 1.</span></span> <span data-ttu-id="aedd5-135">2클래스의 향상된 의사 결정 트리 모델이 학습되어 점수가 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-135">A two-class boosted decision tree model has been trained and scored.</span></span> <span data-ttu-id="aedd5-136">Hello에서 hello 예측 결과 시각화할 수 이제 [모델 점수 매기기] [ score-model] hello의 hello 출력 포트를 클릭 하 여 모듈 [모델 점수 매기기] [ score-model]모듈을 클릭 한 다음 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-136">Now you can visualize hello prediction results from hello [Score Model][score-model] module by clicking hello output port of hello [Score Model][score-model] module and then clicking **Visualize**.</span></span>

![모델 점수 매기기 모듈](./media/machine-learning-interpret-model-results/1_1.png)

<span data-ttu-id="aedd5-138">그림 2에 나와 있는 것 처럼 결과 점수 매기기 hello가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-138">This brings up hello scoring results as shown in Figure 2.</span></span>

![붓꽃 2클래스 분류 문제 실험의 결과](./media/machine-learning-interpret-model-results/2.png)

<span data-ttu-id="aedd5-140">그림 2.</span><span class="sxs-lookup"><span data-stu-id="aedd5-140">Figure 2.</span></span> <span data-ttu-id="aedd5-141">2클래스 분류의 모델 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-141">Visualize a score model result in two-class classification</span></span>

<span data-ttu-id="aedd5-142">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="aedd5-142">**Result interpretation**</span></span>

<span data-ttu-id="aedd5-143">Hello 결과 테이블에 열이 6 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-143">There are six columns in hello results table.</span></span> <span data-ttu-id="aedd5-144">hello 왼쪽된 열 4 개는 hello 4 개의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-144">hello left four columns are hello four features.</span></span> <span data-ttu-id="aedd5-145">hello 오른쪽으로 두 열, 점수가 매겨진 레이블 및 점수가 매겨진 확률은 hello 예측 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-145">hello right two columns, Scored Labels and Scored Probabilities, are hello prediction results.</span></span> <span data-ttu-id="aedd5-146">hello 점수가 매겨진 확률 열 표시 hello 속할 확률을 꽃 toohello 양의 클래스 (클래스 1).</span><span class="sxs-lookup"><span data-stu-id="aedd5-146">hello Scored Probabilities column shows hello probability that a flower belongs toohello positive class (Class 1).</span></span> <span data-ttu-id="aedd5-147">예를 들어 hello hello 열 (0.028571) 이면 첫 번째 꽃 hello 0.028571 확률 속한 tooClass 1에서에서 첫 번째 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-147">For example, hello first number in hello column (0.028571) means there is 0.028571 probability that hello first flower belongs tooClass 1.</span></span> <span data-ttu-id="aedd5-148">점수가 매겨진 레이블 열 표시 hello hello 각 꽃에 대 한 클래스를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-148">hello Scored Labels column shows hello predicted class for each flower.</span></span> <span data-ttu-id="aedd5-149">이 설정은 hello 점수가 매겨진 확률 열에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-149">This is based on hello Scored Probabilities column.</span></span> <span data-ttu-id="aedd5-150">Hello 꽃의 확률 점수가 매겨진 0.5 보다 큰 경우 클래스 1로 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-150">If hello scored probability of a flower is larger than 0.5, it is predicted as Class 1.</span></span> <span data-ttu-id="aedd5-151">그렇지 않으면 클래스 0으로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-151">Otherwise, it is predicted as Class 0.</span></span>

<span data-ttu-id="aedd5-152">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="aedd5-152">**Web service publication**</span></span>

<span data-ttu-id="aedd5-153">Hello 예측 결과 이해 하 고 사운드 판단 한 후 hello 실험 게시할 수 있습니다를 웹 서비스로 다양 한 응용 프로그램에 배포 하 고 모든 새 iris 꽃에서 tooobtain 클래스 예측을 호출할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-153">After hello prediction results have been understood and judged sound, hello experiment can be published as a web service so that you can deploy it in various applications and call it tooobtain class predictions on any new iris flower.</span></span> <span data-ttu-id="aedd5-154">toolearn toochange 학습 점수 매기기 실험으로 실험 및 웹 서비스로 게시 하는 방법 참조 [hello Azure 기계 학습 웹 서비스 게시](machine-learning-walkthrough-5-publish-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-154">toolearn how toochange a training experiment into a scoring experiment and publish it as a web service, see [Publish hello Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span> <span data-ttu-id="aedd5-155">이 절차에 따르면 그림 3에 표시된 대로 점수 매기기 실험이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-155">This procedure provides you with a scoring experiment as shown in Figure 3.</span></span>

![점수 매기기 실험의 스크린샷](./media/machine-learning-interpret-model-results/3.png)

<span data-ttu-id="aedd5-157">그림 3.</span><span class="sxs-lookup"><span data-stu-id="aedd5-157">Figure 3.</span></span> <span data-ttu-id="aedd5-158">점수 매기기 hello iris 2 클래스 분류 문제 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-158">Scoring hello iris two-class classification problem experiment</span></span>

<span data-ttu-id="aedd5-159">이제 해야 tooset hello 입력 및 출력 hello 웹 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-159">Now you need tooset hello input and output for hello web service.</span></span> <span data-ttu-id="aedd5-160">hello 입력이 hello 오른쪽 입력된 포트의 [모델 점수 매기기][score-model], Iris 꽃 기능 입력 hello은입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-160">hello input is hello right input port of [Score Model][score-model], which is hello Iris flower features input.</span></span> <span data-ttu-id="aedd5-161">hello hello 출력에 따라 선택 여부 관심이 hello에 predicted 클래스 (점수가 매겨진된 레이블), 확률 또는 둘 다 hello 점수가 매겨진 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-161">hello choice of hello output depends on whether you are interested in hello predicted class (scored label), hello scored probability, or both.</span></span> <span data-ttu-id="aedd5-162">이 예에서는 둘 다에 관심이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-162">In this example, it is assumed that you are interested in both.</span></span> <span data-ttu-id="aedd5-163">tooselect hello 출력 열을 사용 하 여 원하는 [데이터 집합에서 열 선택] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-163">tooselect hello desired output columns, use a [Select Columns in Data set][select-columns] module.</span></span> <span data-ttu-id="aedd5-164">[데이터 집합의 열 선택][select-columns] 모듈을 클릭하고, **열 선택기 시작**을 클릭한 다음 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-164">Click [Select Columns in Data set][select-columns], click **Launch column selector**, and select **Scored Labels** and **Scored Probabilities**.</span></span> <span data-ttu-id="aedd5-165">hello 출력 포트를 설정한 후 [데이터 집합에서 열 선택] [ select-columns] 다시 실행 수 있어야 준비 toopublish hello 점수 매기기 실험을 웹 서비스로 클릭 하 여 **웹 게시 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-165">After setting hello output port of [Select Columns in Data set][select-columns] and running it again, you should be ready toopublish hello scoring experiment as a web service by clicking **PUBLISH WEB SERVICE**.</span></span> <span data-ttu-id="aedd5-166">hello 최종 실험 그림 4와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-166">hello final experiment looks like Figure 4.</span></span>

![hello iris 2 클래스 분류 실험](./media/machine-learning-interpret-model-results/4.png)

<span data-ttu-id="aedd5-168">그림 4.</span><span class="sxs-lookup"><span data-stu-id="aedd5-168">Figure 4.</span></span> <span data-ttu-id="aedd5-169">붓꽃 2클래스 분류 문제의 마지막 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-169">Final scoring experiment of an iris two-class classification problem</span></span>

<span data-ttu-id="aedd5-170">Hello 웹 서비스를 실행 하 고 테스트 인스턴스에의 한 기능 값을 입력 한 후 hello 결과 두 개의 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-170">After you run hello web service and enter some feature values of a test instance, hello result returns two numbers.</span></span> <span data-ttu-id="aedd5-171">hello 첫 번째 숫자는 레이블, 점수가 매겨진 hello 및 hello 확률 점수가 매겨진 hello를 두 번째는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-171">hello first number is hello scored label, and hello second is hello scored probability.</span></span> <span data-ttu-id="aedd5-172">이 꽃은 확률이 0.9655인 클래스 1로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-172">This flower is predicted as Class 1 with 0.9655 probability.</span></span>

![모델 점수 매기기 테스트 해석](./media/machine-learning-interpret-model-results/4_1.png)

![점수 매기기 테스트 결과](./media/machine-learning-interpret-model-results/5.png)

<span data-ttu-id="aedd5-175">그림 5.</span><span class="sxs-lookup"><span data-stu-id="aedd5-175">Figure 5.</span></span> <span data-ttu-id="aedd5-176">붓꽃 2클래스 분류의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="aedd5-176">Web service result of iris two-class classification</span></span>

### <a name="multi-class-classification"></a><span data-ttu-id="aedd5-177">다중 클래스 분류</span><span class="sxs-lookup"><span data-stu-id="aedd5-177">Multi-class classification</span></span>
<span data-ttu-id="aedd5-178">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="aedd5-178">**Example experiment**</span></span>

<span data-ttu-id="aedd5-179">이 실험에서는 다중 클래스 분류의 예로 문자 인식 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-179">In this experiment, you perform a letter-recognition task as an example of multiclass classification.</span></span> <span data-ttu-id="aedd5-180">hello 분류자 시도 toopredict 특정 이미지를 직접 작성 하는 hello에서 추출 된 일부 직접 작성 된 특성 값을 기반으로 하는 문자 (클래스).</span><span class="sxs-lookup"><span data-stu-id="aedd5-180">hello classifier attempts toopredict a certain letter (class) based on some hand-written attribute values extracted from hello hand-written images.</span></span>

![문자 인식 예제](./media/machine-learning-interpret-model-results/5_1.png)

<span data-ttu-id="aedd5-182">Hello 학습 데이터에서 직접 작성 된 문자 이미지에서 추출 된 16 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-182">In hello training data, there are 16 features extracted from hand-written letter images.</span></span> <span data-ttu-id="aedd5-183">문자는 26 hello 26 클래스를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-183">hello 26 letters form our 26 classes.</span></span> <span data-ttu-id="aedd5-184">그림 6 표시는 다중 클래스 분류를 학습 하는 실험 문자 인식에 대 한 모델 되며 hello에서 동일한 예측 기능 집합에 테스트 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="aedd5-184">Figure 6 shows an experiment that will train a multiclass classification model for letter recognition and predict on hello same feature set on a test data set.</span></span>

![문자 인식 다중 클래스 분류 실험](./media/machine-learning-interpret-model-results/6.png)

<span data-ttu-id="aedd5-186">그림 6.</span><span class="sxs-lookup"><span data-stu-id="aedd5-186">Figure 6.</span></span> <span data-ttu-id="aedd5-187">문자 인식 다중 클래스 분류 문제 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-187">Letter recognition multiclass classification problem experiment</span></span>

<span data-ttu-id="aedd5-188">Hello 결과 hello에서 시각화 [모델 점수 매기기] [ score-model] 의 hello 출력 포트를 클릭 하 여 모듈 [모델 점수 매기기] [ score-model] 모듈 한 다음 클릭 하면 **시각화**, 그림 7에 표시 된 것 처럼 콘텐츠가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-188">Visualizing hello results from hello [Score Model][score-model] module by clicking hello output port of [Score Model][score-model] module and then clicking **Visualize**, you should see content as shown in Figure 7.</span></span>

![모델 점수 매기기 결과](./media/machine-learning-interpret-model-results/7.png)

<span data-ttu-id="aedd5-190">그림 7.</span><span class="sxs-lookup"><span data-stu-id="aedd5-190">Figure 7.</span></span> <span data-ttu-id="aedd5-191">다중 클래스 분류에서 모델 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-191">Visualize score model results in a multi-class classification</span></span>

<span data-ttu-id="aedd5-192">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="aedd5-192">**Result interpretation**</span></span>

<span data-ttu-id="aedd5-193">16 개의 열을 왼쪽된 hello hello 테스트 집합의 hello 기능 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-193">hello left 16 columns represent hello feature values of hello test set.</span></span> <span data-ttu-id="aedd5-194">hello 2 클래스의 경우에서 "XX" 클래스에 대 한 점수가 매겨진 확률은 hello 점수가 매겨진 확률 열 동일와 같은 이름의 hello 열입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-194">hello columns with names like Scored Probabilities for Class "XX" are just like hello Scored Probabilities column in hello two-class case.</span></span> <span data-ttu-id="aedd5-195">특정 클래스에 해당 하는 항목이 hello hello 확률 해당를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-195">They show hello probability that hello corresponding entry falls into a certain class.</span></span> <span data-ttu-id="aedd5-196">예를 들어 hello 첫 번째 항목에 대 한 확률이 0.003571는 "A" 0.000451 일 가능성이 있는 "B", 및 등 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-196">For example, for hello first entry, there is 0.003571 probability that it is an “A,” 0.000451 probability that it is a “B,” and so forth.</span></span> <span data-ttu-id="aedd5-197">hello 마지막 열 (점수가 매겨진 레이블) hello 2 클래스 경우에서 점수가 매겨진 레이블 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-197">hello last column (Scored Labels) is hello same as Scored Labels in hello two-class case.</span></span> <span data-ttu-id="aedd5-198">가장 큰 hello hello 해당 항목의 클래스를 예측된 하는 대로 확률 점수가 매겨진 hello 사용 하 여 hello 클래스 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-198">It selects hello class with hello largest scored probability as hello predicted class of hello corresponding entry.</span></span> <span data-ttu-id="aedd5-199">예를 들어 hello 첫 번째 항목에 대 한 hello 레이블 점수는 "F" hello 가장 큰 확률 toobe는 "F" (0.916995)에 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-199">For example, for hello first entry, hello scored label is “F” since it has hello largest probability toobe an “F” (0.916995).</span></span>

<span data-ttu-id="aedd5-200">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="aedd5-200">**Web service publication**</span></span>

<span data-ttu-id="aedd5-201">또한 각 진입 지점과 hello 가능성 레이블 점수가 매겨진 hello에 대 한 레이블 점수가 매겨진 hello를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-201">You can also get hello scored label for each entry and hello probability of hello scored label.</span></span> <span data-ttu-id="aedd5-202">hello 기본 논리는 확률 점수가 매겨진 모든 hello 간에 toofind hello 최대 확률입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-202">hello basic logic is toofind hello largest probability among all hello scored probabilities.</span></span> <span data-ttu-id="aedd5-203">toodo이 toouse hello 해야 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-203">toodo this, you need toouse hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="aedd5-204">그림 8에 R 코드 hello 보여지고 hello 결과 hello 실험은 그림 9에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-204">hello R code is shown in Figure 8, and hello result of hello experiment is shown in Figure 9.</span></span>

![R 코드 예제](./media/machine-learning-interpret-model-results/8.png)

<span data-ttu-id="aedd5-206">그림 8.</span><span class="sxs-lookup"><span data-stu-id="aedd5-206">Figure 8.</span></span> <span data-ttu-id="aedd5-207">점수가 매겨진 레이블와 hello 추출에 대 한 R 코드 hello 레이블의 확률에 연결</span><span class="sxs-lookup"><span data-stu-id="aedd5-207">R code for extracting Scored Labels and hello associated probabilities of hello labels</span></span>

![실험 결과](./media/machine-learning-interpret-model-results/9.png)

<span data-ttu-id="aedd5-209">그림 9.</span><span class="sxs-lookup"><span data-stu-id="aedd5-209">Figure 9.</span></span> <span data-ttu-id="aedd5-210">Hello 문자 인식 다중 클래스 분류 문제의 최종 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-210">Final scoring experiment of hello letter-recognition multiclass classification problem</span></span>

<span data-ttu-id="aedd5-211">게시 고 hello 웹 서비스를 실행 한 입력된 기능 값을 입력 한 후 hello 결과 아래 그림 10을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-211">After you publish and run hello web service and enter some input feature values, hello returned result looks like Figure 10.</span></span> <span data-ttu-id="aedd5-212">이 직접 작성 된 문자의 압축을 푼 16 기능 0.9715 확률이 예측된 toobe "T"입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-212">This hand-written letter, with its extracted 16 features, is predicted toobe a “T” with 0.9715 probability.</span></span>

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/9_1.png)

![테스트 결과](./media/machine-learning-interpret-model-results/10.png)

<span data-ttu-id="aedd5-215">그림 10.</span><span class="sxs-lookup"><span data-stu-id="aedd5-215">Figure 10.</span></span> <span data-ttu-id="aedd5-216">다중 클래스 분류의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="aedd5-216">Web service result of multiclass classification</span></span>

## <a name="regression"></a><span data-ttu-id="aedd5-217">회귀</span><span class="sxs-lookup"><span data-stu-id="aedd5-217">Regression</span></span>
<span data-ttu-id="aedd5-218">회귀 문제는 분류 문제와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-218">Regression problems are different from classification problems.</span></span> <span data-ttu-id="aedd5-219">분류 문제의 경우 toopredict 불연속 클래스, iris 꽃 속한 클래스 등을 시도 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-219">In a classification problem, you're trying toopredict discrete classes, such as which class an iris flower belongs to.</span></span> <span data-ttu-id="aedd5-220">하지만 다음 예에서는 회귀 문제의 hello에 보시 toopredict 자동차의 hello 가격 같은 연속 변수를 시도 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-220">But as you can see in hello following example of a regression problem, you're trying toopredict a continuous variable, such as hello price of a car.</span></span>

<span data-ttu-id="aedd5-221">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="aedd5-221">**Example experiment**</span></span>

<span data-ttu-id="aedd5-222">회귀 예제로 자동차 가격 예측을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-222">Use automobile price prediction as your example for regression.</span></span> <span data-ttu-id="aedd5-223">만들기, 연료 유형, 본문 유형 및 드라이브 휠을 포함 하 여 해당 기능을 기반으로 하는 자동차의 toopredict hello 가격을 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-223">You are trying toopredict hello price of a car based on its features, including make, fuel type, body type, and drive wheel.</span></span> <span data-ttu-id="aedd5-224">그림 11에서 hello 실험 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-224">hello experiment is shown in Figure 11.</span></span>

![자동차 가격 회귀 실험](./media/machine-learning-interpret-model-results/11.png)

<span data-ttu-id="aedd5-226">그림 11.</span><span class="sxs-lookup"><span data-stu-id="aedd5-226">Figure 11.</span></span> <span data-ttu-id="aedd5-227">자동차 가격 회귀 문제 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-227">Automobile price regression problem experiment</span></span>

<span data-ttu-id="aedd5-228">형상화 hello [모델 점수 매기기] [ score-model] 모듈 그림 12 같은 목록이 hello 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-228">Visualizing hello [Score Model][score-model] module, hello result looks like Figure 12.</span></span>

![자동차 가격 예측 문제의 점수 매기기 결과](./media/machine-learning-interpret-model-results/12.png)

<span data-ttu-id="aedd5-230">그림 12.</span><span class="sxs-lookup"><span data-stu-id="aedd5-230">Figure 12.</span></span> <span data-ttu-id="aedd5-231">Hello 자동차 가격 예측 문제에 대 한 점수 매기기 결과</span><span class="sxs-lookup"><span data-stu-id="aedd5-231">Scoring result for hello automobile price prediction problem</span></span>

<span data-ttu-id="aedd5-232">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="aedd5-232">**Result interpretation**</span></span>

<span data-ttu-id="aedd5-233">점수가 매겨진된 레이블은 hello 결과 열이 점수 매기기 결과에서입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-233">Scored Labels is hello result column in this scoring result.</span></span> <span data-ttu-id="aedd5-234">hello 번호는 각 자동차에 대 한 hello 예측된 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-234">hello numbers are hello predicted price for each car.</span></span>

<span data-ttu-id="aedd5-235">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="aedd5-235">**Web service publication**</span></span>

<span data-ttu-id="aedd5-236">Hello 회귀 실험을 웹 서비스로 게시 하 고 호출할 hello에서 자동차 가격 예측을 위해 hello 2 클래스 분류와 동일 하 게 대/소문자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-236">You can publish hello regression experiment into a web service and call it for automobile price prediction in hello same way as in hello two-class classification use case.</span></span>

![자동차 가격 회귀 문제의 점수 매기기 실험](./media/machine-learning-interpret-model-results/13.png)

<span data-ttu-id="aedd5-238">그림 13.</span><span class="sxs-lookup"><span data-stu-id="aedd5-238">Figure 13.</span></span> <span data-ttu-id="aedd5-239">자동차 가격 회귀 문제의 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-239">Scoring experiment of an automobile price regression problem</span></span>

<span data-ttu-id="aedd5-240">Hello 웹 서비스를 실행 hello 반환 결과 그림 14 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-240">Running hello web service, hello returned result looks like Figure 14.</span></span> <span data-ttu-id="aedd5-241">이 차량에 대 한 예측된 가격 hello $15,085.52입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-241">hello predicted price for this car is $15,085.52.</span></span>

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/13_1.png)

![점수 매기기 모듈 결과](./media/machine-learning-interpret-model-results/14.png)

<span data-ttu-id="aedd5-244">그림 14.</span><span class="sxs-lookup"><span data-stu-id="aedd5-244">Figure 14.</span></span> <span data-ttu-id="aedd5-245">자동차 가격 회귀 문제의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="aedd5-245">Web service result of an automobile price regression problem</span></span>

## <a name="clustering"></a><span data-ttu-id="aedd5-246">클러스터링</span><span class="sxs-lookup"><span data-stu-id="aedd5-246">Clustering</span></span>
<span data-ttu-id="aedd5-247">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="aedd5-247">**Example experiment**</span></span>

<span data-ttu-id="aedd5-248">사용 hello Iris 데이터 집합 다시 toobuild 클러스터링 실험 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-248">Let’s use hello Iris data set again toobuild a clustering experiment.</span></span> <span data-ttu-id="aedd5-249">여기만 기능이 고 클러스터링에 사용할 수 있도록 아웃 hello 클래스 레이블을 hello 데이터 집합의 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-249">Here you can filter out hello class labels in hello data set so that it only has features and can be used for clustering.</span></span> <span data-ttu-id="aedd5-250">이 iris에서 대/소문자를 사용 하 여, 클러스터 toobe 두 hello 꽃을 클러스터링 하는 두 개의 클래스로 hello 학습 프로세스 중 hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-250">In this iris use case, specify hello number of clusters toobe two during hello training process, which means you would cluster hello flowers into two classes.</span></span> <span data-ttu-id="aedd5-251">hello 실험 그림 15에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-251">hello experiment is shown in Figure 15.</span></span>

![붓꽃 클러스터링 문제 실험](./media/machine-learning-interpret-model-results/15.png)

<span data-ttu-id="aedd5-253">그림 15.</span><span class="sxs-lookup"><span data-stu-id="aedd5-253">Figure 15.</span></span> <span data-ttu-id="aedd5-254">붓꽃 클러스터링 문제 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-254">Iris clustering problem experiment</span></span>

<span data-ttu-id="aedd5-255">클러스터링 분류 점에서 다릅니다 hello 학습 데이터 집합에 단독으로 지상 검증 레이블이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-255">Clustering differs from classification in that hello training data set doesn’t have ground-truth labels by itself.</span></span> <span data-ttu-id="aedd5-256">클러스터링 그룹 hello 고유 클러스터인에 학습 데이터 집합 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="aedd5-256">Clustering groups hello training data set instances into distinct clusters.</span></span> <span data-ttu-id="aedd5-257">Hello 모델 레이블의 hello 학습 프로세스 중 해당 기능 간의 hello 차이점에 배웁니다 항목 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-257">During hello training process, hello model labels hello entries by learning hello differences between their features.</span></span> <span data-ttu-id="aedd5-258">그 후 hello 학습 된 모델을 사용할 있습니다 toofurther 이후 항목을 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-258">After that, hello trained model can be used toofurther classify future entries.</span></span> <span data-ttu-id="aedd5-259">두 가지 방법으로 클러스터링 문제 내에서 필요한 hello 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-259">There are two parts of hello result we are interested in within a clustering problem.</span></span> <span data-ttu-id="aedd5-260">hello 첫 번째 부분에는 hello 학습 데이터 집합, 레이블 지정은 및 hello 두 번째는 분류 hello 학습 된 모델에 새 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-260">hello first part is labeling hello training data set, and hello second is classifying a new data set with hello trained model.</span></span>

<span data-ttu-id="aedd5-261">hello hello 결과의 첫 번째 부분 시각화할 수 hello 왼쪽의 출력 포트를 클릭 하 여 [클러스터링 모델 학습] [ train-clustering-model] 클릭 한 다음 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-261">hello first part of hello result can be visualized by clicking hello left output port of [Train Clustering Model][train-clustering-model] and then clicking **Visualize**.</span></span> <span data-ttu-id="aedd5-262">hello 시각화는 그림 16에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-262">hello visualization is shown in Figure 16.</span></span>

![클러스터링 결과](./media/machine-learning-interpret-model-results/16.png)

<span data-ttu-id="aedd5-264">그림 16.</span><span class="sxs-lookup"><span data-stu-id="aedd5-264">Figure 16.</span></span> <span data-ttu-id="aedd5-265">Hello 학습 데이터 집합에 대 한 결과 클러스터링 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-265">Visualize clustering result for hello training data set</span></span>

<span data-ttu-id="aedd5-266">hello 학습 된 클러스터링 모델을 가진 새 항목이 클러스터링 hello 두 번째 파트의 hello 결과 17 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-266">hello result of hello second part, clustering new entries with hello trained clustering model, is shown in Figure 17.</span></span>

![클러스터링 결과 시각화](./media/machine-learning-interpret-model-results/17.png)

<span data-ttu-id="aedd5-268">그림 17.</span><span class="sxs-lookup"><span data-stu-id="aedd5-268">Figure 17.</span></span> <span data-ttu-id="aedd5-269">새 데이터 집합에 대한 클러스터링 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-269">Visualize clustering result on a new data set</span></span>

<span data-ttu-id="aedd5-270">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="aedd5-270">**Result interpretation**</span></span>

<span data-ttu-id="aedd5-271">모양이 hello 두 부분의 hello 결과 서로 다른 실험 단계에서 형태소 분석, 있지만 동일 hello 및 hello에서 해석 되는 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-271">Although hello results of hello two parts stem from different experiment stages, they look hello same and are interpreted in hello same way.</span></span> <span data-ttu-id="aedd5-272">hello 처음 네 개의 열은 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-272">hello first four columns are features.</span></span> <span data-ttu-id="aedd5-273">할당, hello 마지막 열은 hello 예측 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-273">hello last column, Assignments, is hello prediction result.</span></span> <span data-ttu-id="aedd5-274">예측 된 고객 수가 hello 할당 된 항목 hello toobe hello 즉, 동일한 클러스터의 유사성 (hello 기본 유 클 리 디안 거리 메트릭을 사용 하 여이 실험) 어떤 방식으로든에서 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-274">hello entries assigned hello same number are predicted toobe in hello same cluster, that is, they share similarities in some way (this experiment uses hello default Euclidean distance metric).</span></span> <span data-ttu-id="aedd5-275">클러스터 toobe 2의 hello 번호를 지정 하기 때문에 0 또는 1 할당의 hello 항목으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-275">Because you specified hello number of clusters toobe 2, hello entries in Assignments are labeled either 0 or 1.</span></span>

<span data-ttu-id="aedd5-276">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="aedd5-276">**Web service publication**</span></span>

<span data-ttu-id="aedd5-277">웹 서비스 실험 클러스터링 hello를 게시할 수 있으며 같은 방식으로 hello 2 클래스 분류에서 대/소문자를 사용 하 여 클러스터링 예측 hello에 대 한 호출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-277">You can publish hello clustering experiment into a web service and call it for clustering predictions hello same way as in hello two-class classification use case.</span></span>

![붓꽃 클러스터링 문제 점수 매기기 실험](./media/machine-learning-interpret-model-results/18.png)

<span data-ttu-id="aedd5-279">그림 18.</span><span class="sxs-lookup"><span data-stu-id="aedd5-279">Figure 18.</span></span> <span data-ttu-id="aedd5-280">붓꽃 클러스터링 문제 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-280">Scoring experiment of an iris clustering problem</span></span>

<span data-ttu-id="aedd5-281">Hello 웹 서비스를 실행 한 후 hello 그림 19 같이 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-281">After you run hello web service, hello returned result looks like Figure 19.</span></span> <span data-ttu-id="aedd5-282">이 꽃 클러스터 0의에서 예측된 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-282">This flower is predicted toobe in cluster 0.</span></span>

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/18_1.png)

![점수 매기기 모듈 결과](./media/machine-learning-interpret-model-results/19.png)

<span data-ttu-id="aedd5-285">그림 19.</span><span class="sxs-lookup"><span data-stu-id="aedd5-285">Figure 19.</span></span> <span data-ttu-id="aedd5-286">붓꽃 2클래스 분류의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="aedd5-286">Web service result of iris two-class classification</span></span>

## <a name="recommender-system"></a><span data-ttu-id="aedd5-287">추천 시스템</span><span class="sxs-lookup"><span data-stu-id="aedd5-287">Recommender system</span></span>
<span data-ttu-id="aedd5-288">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="aedd5-288">**Example experiment**</span></span>

<span data-ttu-id="aedd5-289">추천 시스템에 대 한 예를 들어 hello 식당 권장 사항 문제를 사용할 수 있습니다: 해당 등급 기록을 기반으로 하는 고객을 위한 식당을 권장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-289">For recommender systems, you can use hello restaurant recommendation problem as an example: you can recommend restaurants for customers based on their rating history.</span></span> <span data-ttu-id="aedd5-290">hello 입력된 데이터의 세 부분으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-290">hello input data consists of three parts:</span></span>

* <span data-ttu-id="aedd5-291">고객이 평가한 음식점 등급</span><span class="sxs-lookup"><span data-stu-id="aedd5-291">Restaurant ratings from customers</span></span>
* <span data-ttu-id="aedd5-292">고객 특징 데이터</span><span class="sxs-lookup"><span data-stu-id="aedd5-292">Customer feature data</span></span>
* <span data-ttu-id="aedd5-293">음식점 기능 데이터</span><span class="sxs-lookup"><span data-stu-id="aedd5-293">Restaurant feature data</span></span>

<span data-ttu-id="aedd5-294">몇 가지 방법으로 hello로 해 [Matchbox 추천 학습] [ train-matchbox-recommender] Azure 기계 학습의 모듈:</span><span class="sxs-lookup"><span data-stu-id="aedd5-294">There are several things we can do with hello [Train Matchbox Recommender][train-matchbox-recommender] module in Azure Machine Learning:</span></span>

* <span data-ttu-id="aedd5-295">지정된 사용자와 항목의 등급 예측</span><span class="sxs-lookup"><span data-stu-id="aedd5-295">Predict ratings for a given user and item</span></span>
* <span data-ttu-id="aedd5-296">사용자 지정 항목 tooa 권장</span><span class="sxs-lookup"><span data-stu-id="aedd5-296">Recommend items tooa given user</span></span>
* <span data-ttu-id="aedd5-297">사용자 지정 하는 사용자가 관련된 tooa 찾기</span><span class="sxs-lookup"><span data-stu-id="aedd5-297">Find users related tooa given user</span></span>
* <span data-ttu-id="aedd5-298">항목 관련된 tooa 항목 찾기</span><span class="sxs-lookup"><span data-stu-id="aedd5-298">Find items related tooa given item</span></span>

<span data-ttu-id="aedd5-299">수행할 toodo hello에 4 hello 옵션 중에서 선택 하 여 선택할 수 있습니다 **추천 예측 종류** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="aedd5-299">You can choose what you want toodo by selecting from hello four options in hello **Recommender prediction kind** menu.</span></span> <span data-ttu-id="aedd5-300">여기서 네 개 시나리오를 모두 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-300">Here you can walk through all four scenarios.</span></span>

![매치박스 추천](./media/machine-learning-interpret-model-results/19_1.png)

<span data-ttu-id="aedd5-302">추천 시스템의 일반적인 Azure Machine Learning 실험은 그림 20과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-302">A typical Azure Machine Learning experiment for a recommender system looks like Figure 20.</span></span> <span data-ttu-id="aedd5-303">어떻게 toouse 해당 추천 시스템 모듈 참조에 대 한 내용은 [matchbox 추천 학습] [ train-matchbox-recommender] 및 [matchbox 추천 점수 매기기] [ score-matchbox-recommender].</span><span class="sxs-lookup"><span data-stu-id="aedd5-303">For information about how toouse those recommender system modules, see [Train matchbox recommender][train-matchbox-recommender] and [Score matchbox recommender][score-matchbox-recommender].</span></span>

![추천 시스템 실험](./media/machine-learning-interpret-model-results/20.png)

<span data-ttu-id="aedd5-305">그림 20.</span><span class="sxs-lookup"><span data-stu-id="aedd5-305">Figure 20.</span></span> <span data-ttu-id="aedd5-306">추천 시스템 실험</span><span class="sxs-lookup"><span data-stu-id="aedd5-306">Recommender system experiment</span></span>

<span data-ttu-id="aedd5-307">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="aedd5-307">**Result interpretation**</span></span>

<span data-ttu-id="aedd5-308">**지정된 사용자와 항목의 등급 예측**</span><span class="sxs-lookup"><span data-stu-id="aedd5-308">**Predict ratings for a given user and item**</span></span>

<span data-ttu-id="aedd5-309">선택 하 여 **등급 예측** 아래 **추천 예측 종류**, 지정 된 사용자와 항목에 대 한 등급 시스템 toopredict hello hello 추천이 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-309">By selecting **Rating Prediction** under **Recommender prediction kind**, you are asking hello recommender system toopredict hello rating for a given user and item.</span></span> <span data-ttu-id="aedd5-310">시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 21은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-310">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 21.</span></span>

![Hello 추천 시스템-등급 예측의 결과 점수를 매깁니다.](./media/machine-learning-interpret-model-results/21.png)

<span data-ttu-id="aedd5-312">그림 21.</span><span class="sxs-lookup"><span data-stu-id="aedd5-312">Figure 21.</span></span> <span data-ttu-id="aedd5-313">등급 예측 hello 추천 시스템의 hello 점수 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-313">Visualize hello score result of hello recommender system--rating prediction</span></span>

<span data-ttu-id="aedd5-314">hello 처음 두 열은 hello 입력된 데이터에서 제공 하는 hello 사용자-항목 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-314">hello first two columns are hello user-item pairs provided by hello input data.</span></span> <span data-ttu-id="aedd5-315">hello 세 번째 열에 특정 항목에 대 한 사용자의 예측된 등급을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-315">hello third column is hello predicted rating of a user for a certain item.</span></span> <span data-ttu-id="aedd5-316">예를 들어 hello 첫 번째 행 U1048가 고객 2로 toorate 식당 135026 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-316">For example, in hello first row, customer U1048 is predicted toorate restaurant 135026 as 2.</span></span>

<span data-ttu-id="aedd5-317">**사용자 지정 항목 tooa 권장**</span><span class="sxs-lookup"><span data-stu-id="aedd5-317">**Recommend items tooa given user**</span></span>

<span data-ttu-id="aedd5-318">선택 하 여 **항목 추천** 아래 **추천 예측 종류**, 사용자 것을 요청 hello 추천 시스템 toorecommend 항목 tooa 사용자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-318">By selecting **Item Recommendation** under **Recommender prediction kind**, you're asking hello recommender system toorecommend items tooa given user.</span></span> <span data-ttu-id="aedd5-319">이 시나리오에서 마지막 매개 변수 toochoose hello는 *항목 선택 권장*합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-319">hello last parameter toochoose in this scenario is *Recommended item selection*.</span></span> <span data-ttu-id="aedd5-320">옵션 hello **(모델 평가 경우)에 대 한 항목에서 등급을 지정 하는 방법** 주로 hello 학습 프로세스 중 모델 평가 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-320">hello option **From Rated Items (for model evaluation)** is primarily for model evaluation during hello training process.</span></span> <span data-ttu-id="aedd5-321">이 예측 단계에서는 **모든 항목에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-321">For this prediction stage, we choose **From All Items**.</span></span> <span data-ttu-id="aedd5-322">시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 22 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-322">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 22.</span></span>

![추천 시스템 - 항목 추천의 점수 매기기 결과](./media/machine-learning-interpret-model-results/22.png)

<span data-ttu-id="aedd5-324">그림 22.</span><span class="sxs-lookup"><span data-stu-id="aedd5-324">Figure 22.</span></span> <span data-ttu-id="aedd5-325">항목 추천 hello 추천 시스템의 점수가 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-325">Visualize score result of hello recommender system--item recommendation</span></span>

<span data-ttu-id="aedd5-326">hello 입력된 데이터에서 제공한 사용자 Id toorecommend 항목을 제공 하는 hello 6 열 나타냅니다 hello 중 첫 번째를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-326">hello first of hello six columns represents hello given user IDs toorecommend items for, as provided by hello input data.</span></span> <span data-ttu-id="aedd5-327">hello 다른 5 개의 열 항목을 나타낼 hello toohello 사용자 관련성 내림차순에서 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-327">hello other five columns represent hello items recommended toohello user in descending order of relevance.</span></span> <span data-ttu-id="aedd5-328">예를 들어 hello 첫 번째 행에 hello 가장 권장 U1048 고객에 대 한 식당은 차례로 135018, 134975, 135021, 132862 134986 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-328">For example, in hello first row, hello most recommended restaurant for customer U1048 is 134986, followed by 135018, 134975, 135021, and 132862.</span></span>

<span data-ttu-id="aedd5-329">**사용자 지정 하는 사용자가 관련된 tooa 찾기**</span><span class="sxs-lookup"><span data-stu-id="aedd5-329">**Find users related tooa given user**</span></span>

<span data-ttu-id="aedd5-330">선택 하 여 **관련 사용자** 아래 **추천 예측 종류**, 사용자 것을 요청 hello 추천 시스템 toofind 관련된 사용자 지정 tooa 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-330">By selecting **Related Users** under **Recommender prediction kind**, you're asking hello recommender system toofind related users tooa given user.</span></span> <span data-ttu-id="aedd5-331">관련된 사용자는 hello 사용자 기본 설정이 비슷한가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-331">Related users are hello users who have similar preferences.</span></span> <span data-ttu-id="aedd5-332">이 시나리오에서 마지막 매개 변수 toochoose hello는 *관련 사용자 선택*합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-332">hello last parameter toochoose in this scenario is *Related user selection*.</span></span> <span data-ttu-id="aedd5-333">옵션 hello **에서 사용자가 항목 등급을 지정한 (모델 평가 위해)** 주로 hello 학습 프로세스 중 모델 평가 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-333">hello option **From Users That Rated Items (for model evaluation)** is primarily for model evaluation during hello training process.</span></span> <span data-ttu-id="aedd5-334">이 예측 단계에서는 **모든 사용자로부터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-334">Choose **From All Users** for this prediction stage.</span></span> <span data-ttu-id="aedd5-335">시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 23 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-335">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 23.</span></span>

![추천 시스템 - 관련 사용자의 점수 매기기 결과](./media/machine-learning-interpret-model-results/23.png)

<span data-ttu-id="aedd5-337">그림 23.</span><span class="sxs-lookup"><span data-stu-id="aedd5-337">Figure 23.</span></span> <span data-ttu-id="aedd5-338">관련된 사용자 hello 추천 시스템의 점수 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-338">Visualize score results of hello recommender system--related users</span></span>

<span data-ttu-id="aedd5-339">먼저 hello의 사용자 Id 필요한 toofind 제공 hello 6 열 표시 hello와 관련 된 사용자 입력된 데이터에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-339">hello first of hello six columns shows hello given user IDs needed toofind related users, as provided by input data.</span></span> <span data-ttu-id="aedd5-340">hello 다른 5 개의 열 저장소 hello 관련성 내림차순에서 hello 사용자의 관련된 사용자 예측된 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-340">hello other five columns store hello predicted related users of hello user in descending order of relevance.</span></span> <span data-ttu-id="aedd5-341">예를 들어 hello 첫 번째 행에 U1048 고객에 대 한 hello 관련성이 가장 높은 고객은 차례로 U1066, U1044, U1017, U1072 U1051 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-341">For example, in hello first row, hello most relevant customer for customer U1048 is U1051, followed by U1066, U1044, U1017, and U1072.</span></span>

<span data-ttu-id="aedd5-342">**항목 관련된 tooa 항목 찾기**</span><span class="sxs-lookup"><span data-stu-id="aedd5-342">**Find items related tooa given item**</span></span>

<span data-ttu-id="aedd5-343">선택 하 여 **관련 항목** 아래 **추천 예측 종류**, hello 추천 시스템 toofind 관련된 항목 제공 tooa 항목이 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-343">By selecting **Related Items** under **Recommender prediction kind**, you are asking hello recommender system toofind related items tooa given item.</span></span> <span data-ttu-id="aedd5-344">관련 항목은 동일 하 여 hello hello 항목 가능성이 가장 높은 toobe 빴 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-344">Related items are hello items most likely toobe liked by hello same user.</span></span> <span data-ttu-id="aedd5-345">이 시나리오에서 마지막 매개 변수 toochoose hello는 *항목 선택 관련*합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-345">hello last parameter toochoose in this scenario is *Related item selection*.</span></span> <span data-ttu-id="aedd5-346">옵션 hello **(모델 평가 경우)에 대 한 항목에서 등급을 지정 하는 방법** 주로 hello 학습 프로세스 중 모델 평가 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-346">hello option **From Rated Items (for model evaluation)** is primarily for model evaluation during hello training process.</span></span> <span data-ttu-id="aedd5-347">이 예측 단계에서는 **모든 항목에서** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-347">We choose **From All Items** for this prediction stage.</span></span> <span data-ttu-id="aedd5-348">시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 24 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-348">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 24.</span></span>

![추천 시스템 - 관련 항목의 점수 매기기 결과](./media/machine-learning-interpret-model-results/24.png)

<span data-ttu-id="aedd5-350">그림 24.</span><span class="sxs-lookup"><span data-stu-id="aedd5-350">Figure 24.</span></span> <span data-ttu-id="aedd5-351">관련된 항목 hello 추천 시스템의 점수 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="aedd5-351">Visualize score results of hello recommender system--related items</span></span>

<span data-ttu-id="aedd5-352">필요한 항목 Id를 지정 하는 hello 6 열 나타냅니다 hello 중 첫 번째 hello toofind 관련 항목을 hello 입력된 데이터에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-352">hello first of hello six columns represents hello given item IDs needed toofind related items, as provided by hello input data.</span></span> <span data-ttu-id="aedd5-353">hello 다른 5 개의 열 저장소 hello 관련성 기준으로 내림차순으로 hello 항목의 관련된 항목을 예측된 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-353">hello other five columns store hello predicted related items of hello item in descending order in terms of relevance.</span></span> <span data-ttu-id="aedd5-354">예를 들어 hello 첫 번째 행 135026 항목에 대 한 hello 관련성이 가장 높은 항목 차례로 135035, 132875, 135055, 134992 135074은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-354">For example, in hello first row, hello most relevant item for item 135026 is 135074, followed by 135035, 132875, 135055, and 134992.</span></span>

<span data-ttu-id="aedd5-355">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="aedd5-355">**Web service publication**</span></span>

<span data-ttu-id="aedd5-356">다음이 실험을 웹 서비스 tooget 예측으로 게시 하는 hello 프로세스는 각각 hello 네 가지 시나리오에 대해 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-356">hello process of publishing these experiments as web services tooget predictions is similar for each of hello four scenarios.</span></span> <span data-ttu-id="aedd5-357">여기 예를 들어 hello 두 번째 시나리오 (권장 되는 항목 tooa 사용자 지정)를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-357">Here we take hello second scenario (recommend items tooa given user) as an example.</span></span> <span data-ttu-id="aedd5-358">참고할 수 세 개의 다른 hello와 동일한 절차를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-358">You can follow hello same procedure with hello other three.</span></span>

<span data-ttu-id="aedd5-359">저장 하는 hello 추천 시스템 학습된 된 모델을 학습 하 고 hello 입력된 데이터 tooa 필터링 단일 사용자 ID 열으로 요청을 그림 25에서와 같이 hello 실험을 연결 하 고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-359">Saving hello trained recommender system as a trained model and filtering hello input data tooa single user ID column as requested, you can hook up hello experiment as in Figure 25 and publish it as a web service.</span></span>

![Hello 식당 권장 문제의 실험 점수 매기기](./media/machine-learning-interpret-model-results/25.png)

<span data-ttu-id="aedd5-361">그림 25.</span><span class="sxs-lookup"><span data-stu-id="aedd5-361">Figure 25.</span></span> <span data-ttu-id="aedd5-362">Hello 식당 권장 문제의 실험 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="aedd5-362">Scoring experiment of hello restaurant recommendation problem</span></span>

<span data-ttu-id="aedd5-363">Hello 웹 서비스를 실행 hello 반환 결과 그림 26 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-363">Running hello web service, hello returned result looks like Figure 26.</span></span> <span data-ttu-id="aedd5-364">U1048 사용자에 대 한 hello 5 개 권장된 레스토랑은 134986 "," 135018 "," 134975 "," 135021, "및" 132862 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd5-364">hello five recommended restaurants for user U1048 are 134986, 135018, 134975, 135021, and 132862.</span></span>

![추천 시스템 서비스의 샘플](./media/machine-learning-interpret-model-results/25_1.png)

![샘플 실험 결과](./media/machine-learning-interpret-model-results/26.png)

<span data-ttu-id="aedd5-367">그림 26.</span><span class="sxs-lookup"><span data-stu-id="aedd5-367">Figure 26.</span></span> <span data-ttu-id="aedd5-368">음식점 추천 문제의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="aedd5-368">Web service result of restaurant recommendation problem</span></span>

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
