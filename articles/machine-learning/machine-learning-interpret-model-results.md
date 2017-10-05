---
title: "Machine Learning에서 모델 결과 해석 | Microsoft Docs"
description: "모델 점수 매기기 출력을 사용하고 시각화하여 알고리즘에 설정된 최적의 매개 변수를 선택하는 방법"
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
ms.openlocfilehash: 939dd7b359b4f5c248ade47b794102f4930994b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a><span data-ttu-id="58efe-103">Machine Learning에서 모델 결과 해석</span><span class="sxs-lookup"><span data-stu-id="58efe-103">Interpret model results in Azure Machine Learning</span></span>
<span data-ttu-id="58efe-104">이 토픽에서는 Azure Machine Learning Studio에서 예측 결과를 시각화하고 해석하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-104">This topic explains how to visualize and interpret prediction results in Azure Machine Learning Studio.</span></span> <span data-ttu-id="58efe-105">모델을 학습시키고 모델에 대한 예측을 수행("모델 점수 매기기")한 후에는 예측 결과를 이해하고 해석해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-105">After you have trained a model and done predictions on top of it ("scored the model"), you need to understand and interpret the prediction result.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="58efe-106">Azure 기계 학습에는 다음과 같이 네 가지 주된 유형의 기계 학습 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-106">There are four major kinds of machine learning models in Azure Machine Learning:</span></span>

* <span data-ttu-id="58efe-107">분류</span><span class="sxs-lookup"><span data-stu-id="58efe-107">Classification</span></span>
* <span data-ttu-id="58efe-108">클러스터링</span><span class="sxs-lookup"><span data-stu-id="58efe-108">Clustering</span></span>
* <span data-ttu-id="58efe-109">회귀</span><span class="sxs-lookup"><span data-stu-id="58efe-109">Regression</span></span>
* <span data-ttu-id="58efe-110">추천 시스템</span><span class="sxs-lookup"><span data-stu-id="58efe-110">Recommender systems</span></span>

<span data-ttu-id="58efe-111">이러한 모델을 기반으로 예측에 사용되는 모듈은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-111">The modules used for prediction on top of these models are:</span></span>

* <span data-ttu-id="58efe-112">분류 및 회귀를 위한 [모델 점수 매기기][score-model] 모듈</span><span class="sxs-lookup"><span data-stu-id="58efe-112">[Score Model][score-model] module for classification and regression</span></span>
* <span data-ttu-id="58efe-113">클러스터링을 위한 [클러스터에 할당][assign-to-clusters] 모듈</span><span class="sxs-lookup"><span data-stu-id="58efe-113">[Assign to Clusters][assign-to-clusters] module for clustering</span></span>
* <span data-ttu-id="58efe-114">추천 시스템을 위한 [매치박스 추천 점수 매기기][score-matchbox-recommender]</span><span class="sxs-lookup"><span data-stu-id="58efe-114">[Score Matchbox Recommender][score-matchbox-recommender] for recommendation systems</span></span>

<span data-ttu-id="58efe-115">이 문서에서는 이러한 각 모듈의 예측 결과를 해석하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-115">This document explains how to interpret prediction results for each of these modules.</span></span> <span data-ttu-id="58efe-116">이러한 모델에 대한 개요는 [Azure Machine Learning에서 알고리즘을 최적화하는 매개 변수를 선택하는 방법](machine-learning-algorithm-parameters-optimize.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58efe-116">For an overview of these modules, see [How to choose parameters to optimize your algorithms in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).</span></span>

<span data-ttu-id="58efe-117">이 항목에서는 예측 해석에 대해 다루지만 모델 평가는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-117">This topic addresses prediction interpretation but not model evaluation.</span></span> <span data-ttu-id="58efe-118">모델 평가 방법에 대한 자세한 내용은 [Azure Machine Learning에서 모델 성능을 평가하는 방법](machine-learning-evaluate-model-performance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58efe-118">For more information about how to evaluate your model, see [How to evaluate model performance in Azure Machine Learning](machine-learning-evaluate-model-performance.md).</span></span>

<span data-ttu-id="58efe-119">Azure Machine Learning을 처음 사용하며 시작하기 위해 간단한 실험을 만드는 방법에 대한 도움이 필요한 경우 Azure Machine Learning Studio의 [Azure Machine Learning Studio에서 간단한 실험 만들기](machine-learning-create-experiment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58efe-119">If you are new to Azure Machine Learning and need help creating a simple experiment to get started, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.</span></span>

## <a name="classification"></a><span data-ttu-id="58efe-120">분류</span><span class="sxs-lookup"><span data-stu-id="58efe-120">Classification</span></span>
<span data-ttu-id="58efe-121">분류 문제의 하위 범주는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-121">There are two subcategories of classification problems:</span></span>

* <span data-ttu-id="58efe-122">2클래스에만 문제가 있음(2클래스 또는 이진 분류)</span><span class="sxs-lookup"><span data-stu-id="58efe-122">Problems with only two classes (two-class or binary classification)</span></span>
* <span data-ttu-id="58efe-123">세 개 이상의 클래스에 문제가 있음(다중 클래스 분류)</span><span class="sxs-lookup"><span data-stu-id="58efe-123">Problems with more than two classes (multi-class classification)</span></span>

<span data-ttu-id="58efe-124">Azure Machine Learning에는 이러한 각 분류 유형을 다루는 여러 모듈이 있지만 예측 결과를 해석하는 방법은 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-124">Azure Machine Learning has different modules to deal with each of these types of classification, but the methods for interpreting their prediction results are similar.</span></span>

### <a name="two-class-classification"></a><span data-ttu-id="58efe-125">2클래스 분류</span><span class="sxs-lookup"><span data-stu-id="58efe-125">Two-class classification</span></span>
<span data-ttu-id="58efe-126">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="58efe-126">**Example experiment**</span></span>

<span data-ttu-id="58efe-127">2클래스 분류 문제의 예로 붓꽃 분류를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-127">An example of a two-class classification problem is the classification of iris flowers.</span></span> <span data-ttu-id="58efe-128">이 작업은 특징에 따라 붓꽃을 분류하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-128">The task is to classify iris flowers based on their features.</span></span> <span data-ttu-id="58efe-129">Azure Machine Learning에서 제공하는 붓꽃 데이터 집합은 널리 사용되는 [붓꽃 데이터 집합](http://en.wikipedia.org/wiki/Iris_flower_data_set)의 하위 집합입니다. 이 집합에는 꽃의 종류가 두 가지(클래스 0과 1)뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-129">The Iris data set provided in Azure Machine Learning is a subset of the popular [Iris data set](http://en.wikipedia.org/wiki/Iris_flower_data_set) containing instances of only two flower species (classes 0 and 1).</span></span> <span data-ttu-id="58efe-130">각 꽃에는 네 가지 특징이 있습니다(꽃받침 길이, 꽃받침 너비, 꽃잎 길이 및 꽃잎 너비).</span><span class="sxs-lookup"><span data-stu-id="58efe-130">There are four features for each flower (sepal length, sepal width, petal length, and petal width).</span></span>

![붓꽃 실험의 스크린샷](./media/machine-learning-interpret-model-results/1.png)

<span data-ttu-id="58efe-132">그림 1.</span><span class="sxs-lookup"><span data-stu-id="58efe-132">Figure 1.</span></span> <span data-ttu-id="58efe-133">붓꽃 2클래스 분류 문제 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-133">Iris two-class classification problem experiment</span></span>

<span data-ttu-id="58efe-134">그림 1에 표시된 대로 이 문제를 해결하기 위해 실험을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-134">An experiment has been performed to solve this problem, as shown in Figure 1.</span></span> <span data-ttu-id="58efe-135">2클래스의 향상된 의사 결정 트리 모델이 학습되어 점수가 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-135">A two-class boosted decision tree model has been trained and scored.</span></span> <span data-ttu-id="58efe-136">이제 [모델 점수 매기기][score-model] 모듈의 출력 포트를 클릭하고 **시각화**를 클릭하여 [모델 점수 매기기][score-model] 모듈에서 예측 결과를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-136">Now you can visualize the prediction results from the [Score Model][score-model] module by clicking the output port of the [Score Model][score-model] module and then clicking **Visualize**.</span></span>

![모델 점수 매기기 모듈](./media/machine-learning-interpret-model-results/1_1.png)

<span data-ttu-id="58efe-138">그러면 그림 2에 표시된 대로 점수 매기기 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-138">This brings up the scoring results as shown in Figure 2.</span></span>

![붓꽃 2클래스 분류 문제 실험의 결과](./media/machine-learning-interpret-model-results/2.png)

<span data-ttu-id="58efe-140">그림 2.</span><span class="sxs-lookup"><span data-stu-id="58efe-140">Figure 2.</span></span> <span data-ttu-id="58efe-141">2클래스 분류의 모델 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-141">Visualize a score model result in two-class classification</span></span>

<span data-ttu-id="58efe-142">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="58efe-142">**Result interpretation**</span></span>

<span data-ttu-id="58efe-143">결과 테이블에 6 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-143">There are six columns in the results table.</span></span> <span data-ttu-id="58efe-144">왼쪽에 있는 네 개의 열이 네 개의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-144">The left four columns are the four features.</span></span> <span data-ttu-id="58efe-145">오른쪽 두 개의 열인 점수가 매겨진 레이블 및 점수가 매겨진 확률이 예측 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-145">The right two columns, Scored Labels and Scored Probabilities, are the prediction results.</span></span> <span data-ttu-id="58efe-146">점수가 매겨진 확률 열에는 꽃이 양의 클래스(클래스 1)에 속할 확률이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-146">The Scored Probabilities column shows the probability that a flower belongs to the positive class (Class 1).</span></span> <span data-ttu-id="58efe-147">예를 들어 열의 첫 번째 숫자(0.028571)는 첫 번째 꽃이 클래스 1에 속할 확률이 0.028571임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-147">For example, the first number in the column (0.028571) means there is 0.028571 probability that the first flower belongs to Class 1.</span></span> <span data-ttu-id="58efe-148">점수가 매겨진 레이블 열에는 각 꽃의 예측 클래스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-148">The Scored Labels column shows the predicted class for each flower.</span></span> <span data-ttu-id="58efe-149">이 값은 점수가 매겨진 확률 열을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-149">This is based on the Scored Probabilities column.</span></span> <span data-ttu-id="58efe-150">꽃의 점수가 매겨진 확률이 0.5보다 크면 클래스 1로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-150">If the scored probability of a flower is larger than 0.5, it is predicted as Class 1.</span></span> <span data-ttu-id="58efe-151">그렇지 않으면 클래스 0으로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-151">Otherwise, it is predicted as Class 0.</span></span>

<span data-ttu-id="58efe-152">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="58efe-152">**Web service publication**</span></span>

<span data-ttu-id="58efe-153">예측 결과를 철저히 파악하고 판단한 후에는 실험을 웹 서비스로 게시할 수 있습니다. 그러면 다양한 응용 프로그램에 실험을 배포하고 호출하여 모든 새 붓꽃에 대한 클래스 예측을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-153">After the prediction results have been understood and judged sound, the experiment can be published as a web service so that you can deploy it in various applications and call it to obtain class predictions on any new iris flower.</span></span> <span data-ttu-id="58efe-154">학습 실험을 점수 매기기 실험으로 변경하여 웹 서비스로 게시하는 방법은 [Azure Machine Learning 웹 서비스 게시](machine-learning-walkthrough-5-publish-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58efe-154">To learn how to change a training experiment into a scoring experiment and publish it as a web service, see [Publish the Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span> <span data-ttu-id="58efe-155">이 절차에 따르면 그림 3에 표시된 대로 점수 매기기 실험이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-155">This procedure provides you with a scoring experiment as shown in Figure 3.</span></span>

![점수 매기기 실험의 스크린샷](./media/machine-learning-interpret-model-results/3.png)

<span data-ttu-id="58efe-157">그림 3.</span><span class="sxs-lookup"><span data-stu-id="58efe-157">Figure 3.</span></span> <span data-ttu-id="58efe-158">붓꽃 2클래스 분류 문제 실험 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="58efe-158">Scoring the iris two-class classification problem experiment</span></span>

<span data-ttu-id="58efe-159">이제 웹 서비스의 입력 및 출력을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-159">Now you need to set the input and output for the web service.</span></span> <span data-ttu-id="58efe-160">입력은 붓꽃 기능 입력인 [모델 점수 매기기][score-model]의 오른쪽 입력 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-160">The input is the right input port of [Score Model][score-model], which is the Iris flower features input.</span></span> <span data-ttu-id="58efe-161">출력은 관심 있는 사항이 예측 클래스(점수가 매겨진 레이블)인지 점수가 매겨진 확률인지 아니면 둘 다인지에 따라 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-161">The choice of the output depends on whether you are interested in the predicted class (scored label), the scored probability, or both.</span></span> <span data-ttu-id="58efe-162">이 예에서는 둘 다에 관심이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-162">In this example, it is assumed that you are interested in both.</span></span> <span data-ttu-id="58efe-163">원하는 출력 열을 선택하려면 [데이터 집합의 열 선택][select-columns] 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-163">To select the desired output columns, use a [Select Columns in Data set][select-columns] module.</span></span> <span data-ttu-id="58efe-164">[데이터 집합의 열 선택][select-columns] 모듈을 클릭하고, **열 선택기 시작**을 클릭한 다음 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-164">Click [Select Columns in Data set][select-columns], click **Launch column selector**, and select **Scored Labels** and **Scored Probabilities**.</span></span> <span data-ttu-id="58efe-165">[데이터 집합의 열 선택][select-columns] 모듈의 출력 포트를 설정하고 다시 실행하면 **웹 서비스 게시** 단추를 클릭하여 점수 매기기 실험을 웹 서비스로 게시할 준비가 완료될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-165">After setting the output port of [Select Columns in Data set][select-columns] and running it again, you should be ready to publish the scoring experiment as a web service by clicking **PUBLISH WEB SERVICE**.</span></span> <span data-ttu-id="58efe-166">마지막 실험은 그림 4와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-166">The final experiment looks like Figure 4.</span></span>

![붓꽃 2클래스 분류 실험](./media/machine-learning-interpret-model-results/4.png)

<span data-ttu-id="58efe-168">그림 4.</span><span class="sxs-lookup"><span data-stu-id="58efe-168">Figure 4.</span></span> <span data-ttu-id="58efe-169">붓꽃 2클래스 분류 문제의 마지막 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-169">Final scoring experiment of an iris two-class classification problem</span></span>

<span data-ttu-id="58efe-170">웹 서비스를 실행하고 테스트 인스턴스의 특징 값을 입력하면 결과에 두 숫자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-170">After you run the web service and enter some feature values of a test instance, the result returns two numbers.</span></span> <span data-ttu-id="58efe-171">첫 번째 숫자는 점수가 매겨진 레이블이고 두 번째는 점수가 매겨진 확률입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-171">The first number is the scored label, and the second is the scored probability.</span></span> <span data-ttu-id="58efe-172">이 꽃은 확률이 0.9655인 클래스 1로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-172">This flower is predicted as Class 1 with 0.9655 probability.</span></span>

![모델 점수 매기기 테스트 해석](./media/machine-learning-interpret-model-results/4_1.png)

![점수 매기기 테스트 결과](./media/machine-learning-interpret-model-results/5.png)

<span data-ttu-id="58efe-175">그림 5.</span><span class="sxs-lookup"><span data-stu-id="58efe-175">Figure 5.</span></span> <span data-ttu-id="58efe-176">붓꽃 2클래스 분류의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="58efe-176">Web service result of iris two-class classification</span></span>

### <a name="multi-class-classification"></a><span data-ttu-id="58efe-177">다중 클래스 분류</span><span class="sxs-lookup"><span data-stu-id="58efe-177">Multi-class classification</span></span>
<span data-ttu-id="58efe-178">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="58efe-178">**Example experiment**</span></span>

<span data-ttu-id="58efe-179">이 실험에서는 다중 클래스 분류의 예로 문자 인식 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-179">In this experiment, you perform a letter-recognition task as an example of multiclass classification.</span></span> <span data-ttu-id="58efe-180">분류자는 필기 이미지에서 추출된 필기 특성 값을 기반으로 특정 문자(클래스)를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-180">The classifier attempts to predict a certain letter (class) based on some hand-written attribute values extracted from the hand-written images.</span></span>

![문자 인식 예제](./media/machine-learning-interpret-model-results/5_1.png)

<span data-ttu-id="58efe-182">학습 데이터에 필기 문자 이미지에서 추출된 16개의 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-182">In the training data, there are 16 features extracted from hand-written letter images.</span></span> <span data-ttu-id="58efe-183">26개 문자가 26개 클래스를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-183">The 26 letters form our 26 classes.</span></span> <span data-ttu-id="58efe-184">그림 6은 문자를 인식하도록 다중 클래스 분류 모델을 교육하고 테스트 데이터 집합에 설정된 동일한 특징에 대한 예측을 수행하는 실험을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-184">Figure 6 shows an experiment that will train a multiclass classification model for letter recognition and predict on the same feature set on a test data set.</span></span>

![문자 인식 다중 클래스 분류 실험](./media/machine-learning-interpret-model-results/6.png)

<span data-ttu-id="58efe-186">그림 6.</span><span class="sxs-lookup"><span data-stu-id="58efe-186">Figure 6.</span></span> <span data-ttu-id="58efe-187">문자 인식 다중 클래스 분류 문제 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-187">Letter recognition multiclass classification problem experiment</span></span>

<span data-ttu-id="58efe-188">[모델 점수 매기기][score-model] 모듈의 출력 포트를 클릭한 다음 **시각화**를 클릭하여 [모델 점수 매기기][score-model]의 결과를 시각화하면 그림 7과 같은 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-188">Visualizing the results from the [Score Model][score-model] module by clicking the output port of [Score Model][score-model] module and then clicking **Visualize**, you should see content as shown in Figure 7.</span></span>

![모델 점수 매기기 결과](./media/machine-learning-interpret-model-results/7.png)

<span data-ttu-id="58efe-190">그림 7.</span><span class="sxs-lookup"><span data-stu-id="58efe-190">Figure 7.</span></span> <span data-ttu-id="58efe-191">다중 클래스 분류에서 모델 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-191">Visualize score model results in a multi-class classification</span></span>

<span data-ttu-id="58efe-192">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="58efe-192">**Result interpretation**</span></span>

<span data-ttu-id="58efe-193">왼쪽에 있는 16개의 열이 테스트 집합의 기능 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-193">The left 16 columns represent the feature values of the test set.</span></span> <span data-ttu-id="58efe-194">클래스 “XX”의 점수가 매겨진 확률이라고 이름이 지정된 열은 2클래스 사례의 점수가 매겨진 확률 열과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-194">The columns with names like Scored Probabilities for Class "XX" are just like the Scored Probabilities column in the two-class case.</span></span> <span data-ttu-id="58efe-195">해당 항목이 특정 클래스에 속할 확률을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-195">They show the probability that the corresponding entry falls into a certain class.</span></span> <span data-ttu-id="58efe-196">예를 들어 첫 번째 항목은 “A”인 0.003571 확률과 “B”인 0.000451 확률 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-196">For example, for the first entry, there is 0.003571 probability that it is an “A,” 0.000451 probability that it is a “B,” and so forth.</span></span> <span data-ttu-id="58efe-197">마지막 열(점수가 매겨진 레이블)은 2클래스에서의 점수가 매겨진 레이블과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-197">The last column (Scored Labels) is the same as Scored Labels in the two-class case.</span></span> <span data-ttu-id="58efe-198">점수가 매겨진 확률이 가장 높은 클래스를 해당 항목의 예측 클래스로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-198">It selects the class with the largest scored probability as the predicted class of the corresponding entry.</span></span> <span data-ttu-id="58efe-199">예를 들어, 첫 번째 항목에서 가장 큰 확률은 “F”(0.916995)이므로 점수가 매겨진 레이블은 “F”입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-199">For example, for the first entry, the scored label is “F” since it has the largest probability to be an “F” (0.916995).</span></span>

<span data-ttu-id="58efe-200">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="58efe-200">**Web service publication**</span></span>

<span data-ttu-id="58efe-201">또한 각 항목의 점수가 매겨진 레이블 및 점수가 매겨진 레이블의 확률을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-201">You can also get the scored label for each entry and the probability of the scored label.</span></span> <span data-ttu-id="58efe-202">기본 논리는 점수가 매겨진 확률 중에서 가장 큰 확률을 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-202">The basic logic is to find the largest probability among all the scored probabilities.</span></span> <span data-ttu-id="58efe-203">이렇게 하려면 [R 스크립트 실행][execute-r-script] 모듈을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-203">To do this, you need to use the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="58efe-204">R 코드는 그림 8에 표시되어 있고 실험 결과는 그림 9와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-204">The R code is shown in Figure 8, and the result of the experiment is shown in Figure 9.</span></span>

![R 코드 예제](./media/machine-learning-interpret-model-results/8.png)

<span data-ttu-id="58efe-206">그림 8.</span><span class="sxs-lookup"><span data-stu-id="58efe-206">Figure 8.</span></span> <span data-ttu-id="58efe-207">점수가 매겨진 레이블 및 레이블의 연관된 확률을 추출하는 R 코드</span><span class="sxs-lookup"><span data-stu-id="58efe-207">R code for extracting Scored Labels and the associated probabilities of the labels</span></span>

![실험 결과](./media/machine-learning-interpret-model-results/9.png)

<span data-ttu-id="58efe-209">그림 9.</span><span class="sxs-lookup"><span data-stu-id="58efe-209">Figure 9.</span></span> <span data-ttu-id="58efe-210">문자 인식 다중 클래스 분류 문제의 마지막 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-210">Final scoring experiment of the letter-recognition multiclass classification problem</span></span>

<span data-ttu-id="58efe-211">웹 서비스를 게시하고 실행한 다음 입력 특징 값을 입력하고 나면 그림 10과 같은 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-211">After you publish and run the web service and enter some input feature values, the returned result looks like Figure 10.</span></span> <span data-ttu-id="58efe-212">16개의 기능이 추출된 이 필기 문자는 확률이 0.9715인 “T”로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-212">This hand-written letter, with its extracted 16 features, is predicted to be a “T” with 0.9715 probability.</span></span>

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/9_1.png)

![테스트 결과](./media/machine-learning-interpret-model-results/10.png)

<span data-ttu-id="58efe-215">그림 10.</span><span class="sxs-lookup"><span data-stu-id="58efe-215">Figure 10.</span></span> <span data-ttu-id="58efe-216">다중 클래스 분류의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="58efe-216">Web service result of multiclass classification</span></span>

## <a name="regression"></a><span data-ttu-id="58efe-217">회귀</span><span class="sxs-lookup"><span data-stu-id="58efe-217">Regression</span></span>
<span data-ttu-id="58efe-218">회귀 문제는 분류 문제와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-218">Regression problems are different from classification problems.</span></span> <span data-ttu-id="58efe-219">분류 문제에서는 붓꽃이 속한 클래스와 같이 개별 클래스를 예측하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-219">In a classification problem, you're trying to predict discrete classes, such as which class an iris flower belongs to.</span></span> <span data-ttu-id="58efe-220">하지만 회귀 문제에서는 다음 예에서 볼 수 있듯이, 자동차 가격과 같은 연속 변수에 대해 예측하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-220">But as you can see in the following example of a regression problem, you're trying to predict a continuous variable, such as the price of a car.</span></span>

<span data-ttu-id="58efe-221">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="58efe-221">**Example experiment**</span></span>

<span data-ttu-id="58efe-222">회귀 예제로 자동차 가격 예측을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-222">Use automobile price prediction as your example for regression.</span></span> <span data-ttu-id="58efe-223">제조사, 연료 유형, 차체 유형, 구동륜 등의 특징에 따라 자동차의 가격을 예측하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-223">You are trying to predict the price of a car based on its features, including make, fuel type, body type, and drive wheel.</span></span> <span data-ttu-id="58efe-224">이 실험은 그림 11에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-224">The experiment is shown in Figure 11.</span></span>

![자동차 가격 회귀 실험](./media/machine-learning-interpret-model-results/11.png)

<span data-ttu-id="58efe-226">그림 11.</span><span class="sxs-lookup"><span data-stu-id="58efe-226">Figure 11.</span></span> <span data-ttu-id="58efe-227">자동차 가격 회귀 문제 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-227">Automobile price regression problem experiment</span></span>

<span data-ttu-id="58efe-228">[모델 점수 매기기][score-model] 모듈을 시각화하면 결과는 그림 12와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-228">Visualizing the [Score Model][score-model] module, the result looks like Figure 12.</span></span>

![자동차 가격 예측 문제의 점수 매기기 결과](./media/machine-learning-interpret-model-results/12.png)

<span data-ttu-id="58efe-230">그림 12.</span><span class="sxs-lookup"><span data-stu-id="58efe-230">Figure 12.</span></span> <span data-ttu-id="58efe-231">자동차 가격 예측 문제의 점수 매기기 결과</span><span class="sxs-lookup"><span data-stu-id="58efe-231">Scoring result for the automobile price prediction problem</span></span>

<span data-ttu-id="58efe-232">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="58efe-232">**Result interpretation**</span></span>

<span data-ttu-id="58efe-233">이 점수 매기기 결과에서 점수가 매겨진 레이블이 결과 열입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-233">Scored Labels is the result column in this scoring result.</span></span> <span data-ttu-id="58efe-234">숫자는 각 자동차의 예상 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-234">The numbers are the predicted price for each car.</span></span>

<span data-ttu-id="58efe-235">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="58efe-235">**Web service publication**</span></span>

<span data-ttu-id="58efe-236">웹 서비스에 회귀 실험을 게시한 다음 2클래스 분류 사용 사례에서와 동일한 방법으로 자동차 가격 예측을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-236">You can publish the regression experiment into a web service and call it for automobile price prediction in the same way as in the two-class classification use case.</span></span>

![자동차 가격 회귀 문제의 점수 매기기 실험](./media/machine-learning-interpret-model-results/13.png)

<span data-ttu-id="58efe-238">그림 13.</span><span class="sxs-lookup"><span data-stu-id="58efe-238">Figure 13.</span></span> <span data-ttu-id="58efe-239">자동차 가격 회귀 문제의 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-239">Scoring experiment of an automobile price regression problem</span></span>

<span data-ttu-id="58efe-240">웹 서비스를 실행하면 반환된 결과는 그림 14와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-240">Running the web service, the returned result looks like Figure 14.</span></span> <span data-ttu-id="58efe-241">이 자동차의 예상 가격은 $15,085.52입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-241">The predicted price for this car is $15,085.52.</span></span>

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/13_1.png)

![점수 매기기 모듈 결과](./media/machine-learning-interpret-model-results/14.png)

<span data-ttu-id="58efe-244">그림 14.</span><span class="sxs-lookup"><span data-stu-id="58efe-244">Figure 14.</span></span> <span data-ttu-id="58efe-245">자동차 가격 회귀 문제의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="58efe-245">Web service result of an automobile price regression problem</span></span>

## <a name="clustering"></a><span data-ttu-id="58efe-246">클러스터링</span><span class="sxs-lookup"><span data-stu-id="58efe-246">Clustering</span></span>
<span data-ttu-id="58efe-247">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="58efe-247">**Example experiment**</span></span>

<span data-ttu-id="58efe-248">다시 붓꽃 데이터 집합을 사용하여 클러스터링 실험을 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-248">Let’s use the Iris data set again to build a clustering experiment.</span></span> <span data-ttu-id="58efe-249">여기에서는 특징만 보유하고 클러스터링에 사용할 수 있도록 데이터 집합의 클래스 레이블을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-249">Here you can filter out the class labels in the data set so that it only has features and can be used for clustering.</span></span> <span data-ttu-id="58efe-250">이 붓꽃 사용 사례에서는 학습 프로세스 중에 클러스터의 수를 2로 지정합니다. 즉, 꽃을 2클래스로 클러스터링합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-250">In this iris use case, specify the number of clusters to be two during the training process, which means you would cluster the flowers into two classes.</span></span> <span data-ttu-id="58efe-251">실험은 그림 15에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-251">The experiment is shown in Figure 15.</span></span>

![붓꽃 클러스터링 문제 실험](./media/machine-learning-interpret-model-results/15.png)

<span data-ttu-id="58efe-253">그림 15.</span><span class="sxs-lookup"><span data-stu-id="58efe-253">Figure 15.</span></span> <span data-ttu-id="58efe-254">붓꽃 클러스터링 문제 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-254">Iris clustering problem experiment</span></span>

<span data-ttu-id="58efe-255">클러스터링은 학습 데이터 집합에 자체 실측 자료가 없다는 점에서 분류와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-255">Clustering differs from classification in that the training data set doesn’t have ground-truth labels by itself.</span></span> <span data-ttu-id="58efe-256">클러스터링은 학습 데이터 집합 인스턴스를 개별 클러스터로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-256">Clustering groups the training data set instances into distinct clusters.</span></span> <span data-ttu-id="58efe-257">학습 프로세스 중에 모델에서 해당 특징 사이의 차이점을 학습하여 항목의 레이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-257">During the training process, the model labels the entries by learning the differences between their features.</span></span> <span data-ttu-id="58efe-258">그런 다음 학습된 모델을 사용하여 나중에 항목을 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-258">After that, the trained model can be used to further classify future entries.</span></span> <span data-ttu-id="58efe-259">클러스터링 문제에서 결과의 두 부분에 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-259">There are two parts of the result we are interested in within a clustering problem.</span></span> <span data-ttu-id="58efe-260">첫 번째 부분은 학습 데이터 집합의 레이블을 지정하는 것이고, 두 번째는 학습된 모델을 사용하여 새 데이터 집합을 분류하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-260">The first part is labeling the training data set, and the second is classifying a new data set with the trained model.</span></span>

<span data-ttu-id="58efe-261">결과의 첫 번째 부분은 [클러스터링 모델 학습][train-clustering-model] 모듈의 왼쪽 출력 포트를 클릭하고 **시각화**를 클릭하여 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-261">The first part of the result can be visualized by clicking the left output port of [Train Clustering Model][train-clustering-model] and then clicking **Visualize**.</span></span> <span data-ttu-id="58efe-262">시각화는 그림 16에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-262">The visualization is shown in Figure 16.</span></span>

![클러스터링 결과](./media/machine-learning-interpret-model-results/16.png)

<span data-ttu-id="58efe-264">그림 16.</span><span class="sxs-lookup"><span data-stu-id="58efe-264">Figure 16.</span></span> <span data-ttu-id="58efe-265">학습 데이터 집합의 클러스터링 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-265">Visualize clustering result for the training data set</span></span>

<span data-ttu-id="58efe-266">결과의  번째 부분, 즉 학습된 클러스터링 모델로 새 항목 클러스터링은 그림 17에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-266">The result of the second part, clustering new entries with the trained clustering model, is shown in Figure 17.</span></span>

![클러스터링 결과 시각화](./media/machine-learning-interpret-model-results/17.png)

<span data-ttu-id="58efe-268">그림 17.</span><span class="sxs-lookup"><span data-stu-id="58efe-268">Figure 17.</span></span> <span data-ttu-id="58efe-269">새 데이터 집합에 대한 클러스터링 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-269">Visualize clustering result on a new data set</span></span>

<span data-ttu-id="58efe-270">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="58efe-270">**Result interpretation**</span></span>

<span data-ttu-id="58efe-271">두 부분의 결과가 서로 다른 실험 단계에서 기인하지만 결과가 똑같으며 동일한 방식으로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-271">Although the results of the two parts stem from different experiment stages, they look the same and are interpreted in the same way.</span></span> <span data-ttu-id="58efe-272">처음 네 개의 열이 특징입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-272">The first four columns are features.</span></span> <span data-ttu-id="58efe-273">마지막 열인 할당이 예측 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-273">The last column, Assignments, is the prediction result.</span></span> <span data-ttu-id="58efe-274">같은 숫자가 할당된 항목은 같은 클러스터에 있을 것으로 예상됩니다. 즉, 일정한 방식으로 유사성을 공유합니다(이 실험에서는 기본 유클리드 거리 메트릭을 사용함).</span><span class="sxs-lookup"><span data-stu-id="58efe-274">The entries assigned the same number are predicted to be in the same cluster, that is, they share similarities in some way (this experiment uses the default Euclidean distance metric).</span></span> <span data-ttu-id="58efe-275">클러스터 수를 2로 지정했기 때문에 할당의 항목에 0 또는 1 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-275">Because you specified the number of clusters to be 2, the entries in Assignments are labeled either 0 or 1.</span></span>

<span data-ttu-id="58efe-276">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="58efe-276">**Web service publication**</span></span>

<span data-ttu-id="58efe-277">웹 서비스에 클러스터링 실험을 게시한 다음 2클래스 분류 사용 사례에서와 동일한 방법으로 클러스터링 예측을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-277">You can publish the clustering experiment into a web service and call it for clustering predictions the same way as in the two-class classification use case.</span></span>

![붓꽃 클러스터링 문제 점수 매기기 실험](./media/machine-learning-interpret-model-results/18.png)

<span data-ttu-id="58efe-279">그림 18.</span><span class="sxs-lookup"><span data-stu-id="58efe-279">Figure 18.</span></span> <span data-ttu-id="58efe-280">붓꽃 클러스터링 문제 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-280">Scoring experiment of an iris clustering problem</span></span>

<span data-ttu-id="58efe-281">웹 서비스를 실행하면 그림 19와 비슷한 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-281">After you run the web service, the returned result looks like Figure 19.</span></span> <span data-ttu-id="58efe-282">이 꽃은 클러스터 0에 있는 것으로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-282">This flower is predicted to be in cluster 0.</span></span>

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/18_1.png)

![점수 매기기 모듈 결과](./media/machine-learning-interpret-model-results/19.png)

<span data-ttu-id="58efe-285">그림 19.</span><span class="sxs-lookup"><span data-stu-id="58efe-285">Figure 19.</span></span> <span data-ttu-id="58efe-286">붓꽃 2클래스 분류의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="58efe-286">Web service result of iris two-class classification</span></span>

## <a name="recommender-system"></a><span data-ttu-id="58efe-287">추천 시스템</span><span class="sxs-lookup"><span data-stu-id="58efe-287">Recommender system</span></span>
<span data-ttu-id="58efe-288">**예제 실험**</span><span class="sxs-lookup"><span data-stu-id="58efe-288">**Example experiment**</span></span>

<span data-ttu-id="58efe-289">추천 시스템의 경우 음식점 추천 문제를 예로 사용할 수 있습니다. 고객의 등급 지정 내역을 기반으로 고객에게 음식점을 추천할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-289">For recommender systems, you can use the restaurant recommendation problem as an example: you can recommend restaurants for customers based on their rating history.</span></span> <span data-ttu-id="58efe-290">입력 데이터는 다음 세 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-290">The input data consists of three parts:</span></span>

* <span data-ttu-id="58efe-291">고객이 평가한 음식점 등급</span><span class="sxs-lookup"><span data-stu-id="58efe-291">Restaurant ratings from customers</span></span>
* <span data-ttu-id="58efe-292">고객 특징 데이터</span><span class="sxs-lookup"><span data-stu-id="58efe-292">Customer feature data</span></span>
* <span data-ttu-id="58efe-293">음식점 기능 데이터</span><span class="sxs-lookup"><span data-stu-id="58efe-293">Restaurant feature data</span></span>

<span data-ttu-id="58efe-294">Azure Machine Learning의 [매치박스 추천 학습][train-matchbox-recommender] 모듈을 사용하여 여러 가지를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-294">There are several things we can do with the [Train Matchbox Recommender][train-matchbox-recommender] module in Azure Machine Learning:</span></span>

* <span data-ttu-id="58efe-295">지정된 사용자와 항목의 등급 예측</span><span class="sxs-lookup"><span data-stu-id="58efe-295">Predict ratings for a given user and item</span></span>
* <span data-ttu-id="58efe-296">지정된 사용자를 위한 항목 추천</span><span class="sxs-lookup"><span data-stu-id="58efe-296">Recommend items to a given user</span></span>
* <span data-ttu-id="58efe-297">지정된 사용자와 관련된 사용자 찾기</span><span class="sxs-lookup"><span data-stu-id="58efe-297">Find users related to a given user</span></span>
* <span data-ttu-id="58efe-298">지정된 항목과 관련된 항목 찾기</span><span class="sxs-lookup"><span data-stu-id="58efe-298">Find items related to a given item</span></span>

<span data-ttu-id="58efe-299">**추천 예측 유형** 메뉴에 있는 네 가지 옵션 중에 선택하여 수행할 작업을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-299">You can choose what you want to do by selecting from the four options in the **Recommender prediction kind** menu.</span></span> <span data-ttu-id="58efe-300">여기서 네 개 시나리오를 모두 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-300">Here you can walk through all four scenarios.</span></span>

![매치박스 추천](./media/machine-learning-interpret-model-results/19_1.png)

<span data-ttu-id="58efe-302">추천 시스템의 일반적인 Azure Machine Learning 실험은 그림 20과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-302">A typical Azure Machine Learning experiment for a recommender system looks like Figure 20.</span></span> <span data-ttu-id="58efe-303">추천 시스템 모듈 사용 방법에 대한 자세한 내용은 [매치박스 추천 학습][train-matchbox-recommender] 및 [매치박스 추천 점수 매기기][score-matchbox-recommender]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58efe-303">For information about how to use those recommender system modules, see [Train matchbox recommender][train-matchbox-recommender] and [Score matchbox recommender][score-matchbox-recommender].</span></span>

![추천 시스템 실험](./media/machine-learning-interpret-model-results/20.png)

<span data-ttu-id="58efe-305">그림 20.</span><span class="sxs-lookup"><span data-stu-id="58efe-305">Figure 20.</span></span> <span data-ttu-id="58efe-306">추천 시스템 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-306">Recommender system experiment</span></span>

<span data-ttu-id="58efe-307">**결과 해석**</span><span class="sxs-lookup"><span data-stu-id="58efe-307">**Result interpretation**</span></span>

<span data-ttu-id="58efe-308">**지정된 사용자와 항목의 등급 예측**</span><span class="sxs-lookup"><span data-stu-id="58efe-308">**Predict ratings for a given user and item**</span></span>

<span data-ttu-id="58efe-309">**추천 예측 유형** 메뉴에서 **등급 예측**을 선택하여 지정된 사용자와 항목의 등급을 예측해 달라고 추천 시스템에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-309">By selecting **Rating Prediction** under **Recommender prediction kind**, you are asking the recommender system to predict the rating for a given user and item.</span></span> <span data-ttu-id="58efe-310">[매치박스 추천 점수 매기기][score-matchbox-recommender] 출력의 시각화는 그림 21과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-310">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 21.</span></span>

![추천 시스템 - 등급 예측의 점수 매기기 결과](./media/machine-learning-interpret-model-results/21.png)

<span data-ttu-id="58efe-312">그림 21.</span><span class="sxs-lookup"><span data-stu-id="58efe-312">Figure 21.</span></span> <span data-ttu-id="58efe-313">추천 시스템 - 등급 예측의 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-313">Visualize the score result of the recommender system--rating prediction</span></span>

<span data-ttu-id="58efe-314">처음 두 열은 입력된 데이터에서 제공하는 사용자-항목 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-314">The first two columns are the user-item pairs provided by the input data.</span></span> <span data-ttu-id="58efe-315">세 번째 열은 특정 항목에 대한 사용자의 예측 등급입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-315">The third column is the predicted rating of a user for a certain item.</span></span> <span data-ttu-id="58efe-316">예를 들어, 첫 번째 행에서 U1048 고객은 135026 음식점의 등급을 2로 지정할 것으로 예측됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-316">For example, in the first row, customer U1048 is predicted to rate restaurant 135026 as 2.</span></span>

<span data-ttu-id="58efe-317">**지정된 사용자에게 항목 추천**</span><span class="sxs-lookup"><span data-stu-id="58efe-317">**Recommend items to a given user**</span></span>

<span data-ttu-id="58efe-318">**추천 예측 유형** 메뉴에서 **항목 추천**을 선택하여 지정된 사용자에게 항목을 추천해 달라고 추천 시스템에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-318">By selecting **Item Recommendation** under **Recommender prediction kind**, you're asking the recommender system to recommend items to a given user.</span></span> <span data-ttu-id="58efe-319">이 시나리오에서 선택할 마지막 매개 변수는 *추천 항목 선택*입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-319">The last parameter to choose in this scenario is *Recommended item selection*.</span></span> <span data-ttu-id="58efe-320">**등급이 지정된 항목에서(모델 평가용)** 옵션은 주로 학습 프로세스 중에 모델 평가용으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-320">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="58efe-321">이 예측 단계에서는 **모든 항목에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-321">For this prediction stage, we choose **From All Items**.</span></span> <span data-ttu-id="58efe-322">[매치박스 추천 점수 매기기][score-matchbox-recommender] 출력의 시각화는 그림 22와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-322">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 22.</span></span>

![추천 시스템 - 항목 추천의 점수 매기기 결과](./media/machine-learning-interpret-model-results/22.png)

<span data-ttu-id="58efe-324">그림 22.</span><span class="sxs-lookup"><span data-stu-id="58efe-324">Figure 22.</span></span> <span data-ttu-id="58efe-325">추천 시스템 - 항목 추천의 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-325">Visualize score result of the recommender system--item recommendation</span></span>

<span data-ttu-id="58efe-326">6개 열 중 첫 번째 열은 입력 데이터에서 제공한 항목을 추천받도록 지정된 사용자 ID를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-326">The first of the six columns represents the given user IDs to recommend items for, as provided by the input data.</span></span> <span data-ttu-id="58efe-327">나머지 5개 열은 사용자에게 추천할 항목을 나타내며 관련성에 따라 내림차순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-327">The other five columns represent the items recommended to the user in descending order of relevance.</span></span> <span data-ttu-id="58efe-328">예를 들어 첫 번째 행에서 U1048 고객에게 가장 많이 추천된 음식점은 134986이고, 다음으로 135018, 134975, 135021 및 132862 순으로 추천되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-328">For example, in the first row, the most recommended restaurant for customer U1048 is 134986, followed by 135018, 134975, 135021, and 132862.</span></span>

<span data-ttu-id="58efe-329">**지정된 사용자와 관련된 사용자 찾기**</span><span class="sxs-lookup"><span data-stu-id="58efe-329">**Find users related to a given user**</span></span>

<span data-ttu-id="58efe-330">**추천 예측 유형**에서 **관련 사용자**를 선택하여 추천 시스템에서 지정된 사용자와 관련된 사용자를 찾도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-330">By selecting **Related Users** under **Recommender prediction kind**, you're asking the recommender system to find related users to a given user.</span></span> <span data-ttu-id="58efe-331">관련된 사용자는 기본 설정이 비슷한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-331">Related users are the users who have similar preferences.</span></span> <span data-ttu-id="58efe-332">이 시나리오에서 선택할 마지막 매개 변수는 *관련 사용자 선택*입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-332">The last parameter to choose in this scenario is *Related user selection*.</span></span> <span data-ttu-id="58efe-333">**등급을 지정한 사용자로부터(모델 평가용)** 옵션은 주로 학습 프로세스 중에 모델 평가용으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-333">The option **From Users That Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="58efe-334">이 예측 단계에서는 **모든 사용자로부터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-334">Choose **From All Users** for this prediction stage.</span></span> <span data-ttu-id="58efe-335">[매치박스 추천 점수 매기기][score-matchbox-recommender] 출력의 시각화는 그림 23과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-335">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 23.</span></span>

![추천 시스템 - 관련 사용자의 점수 매기기 결과](./media/machine-learning-interpret-model-results/23.png)

<span data-ttu-id="58efe-337">그림 23.</span><span class="sxs-lookup"><span data-stu-id="58efe-337">Figure 23.</span></span> <span data-ttu-id="58efe-338">추천 시스템 - 관련 사용자의 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-338">Visualize score results of the recommender system--related users</span></span>

<span data-ttu-id="58efe-339">6개 열 중 첫 번째 열은 입력 데이터에서 제공한 관련 사용자를 찾는 데 필요한 특정 사용자 ID를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-339">The first of the six columns shows the given user IDs needed to find related users, as provided by input data.</span></span> <span data-ttu-id="58efe-340">나머지 5개 열에는 사용자의 예상되는 관련 사용자가 저장되며, 관련성에 따라 내림차순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-340">The other five columns store the predicted related users of the user in descending order of relevance.</span></span> <span data-ttu-id="58efe-341">예를 들어 첫 번째 행에서 U1048 고객과 가장 관련성이 높은 고객은 U1051이고, 그 뒤를 이어 U1066 U1044 U1017 및 U1072 순입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-341">For example, in the first row, the most relevant customer for customer U1048 is U1051, followed by U1066, U1044, U1017, and U1072.</span></span>

<span data-ttu-id="58efe-342">**지정된 항목과 관련된 항목 찾기**</span><span class="sxs-lookup"><span data-stu-id="58efe-342">**Find items related to a given item**</span></span>

<span data-ttu-id="58efe-343">**추천 예측 유형**에서 **관련 항목**을 선택하여 추천 시스템에서 지정된 항목과 관련된 항목을 찾도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-343">By selecting **Related Items** under **Recommender prediction kind**, you are asking the recommender system to find related items to a given item.</span></span> <span data-ttu-id="58efe-344">관련 항목은 동일한 사용자가 좋아할 가능성이 가장 큰 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-344">Related items are the items most likely to be liked by the same user.</span></span> <span data-ttu-id="58efe-345">이 시나리오에서 선택할 마지막 매개 변수는 *관련 항목 선택*입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-345">The last parameter to choose in this scenario is *Related item selection*.</span></span> <span data-ttu-id="58efe-346">**등급이 지정된 항목에서(모델 평가용)** 옵션은 주로 학습 프로세스 중에 모델 평가용으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-346">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="58efe-347">이 예측 단계에서는 **모든 항목에서** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-347">We choose **From All Items** for this prediction stage.</span></span> <span data-ttu-id="58efe-348">[매치박스 추천 점수 매기기][score-matchbox-recommender] 출력의 시각화는 그림 24와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-348">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 24.</span></span>

![추천 시스템 - 관련 항목의 점수 매기기 결과](./media/machine-learning-interpret-model-results/24.png)

<span data-ttu-id="58efe-350">그림 24.</span><span class="sxs-lookup"><span data-stu-id="58efe-350">Figure 24.</span></span> <span data-ttu-id="58efe-351">추천 시스템 - 관련 항목의 점수 매기기 결과 시각화</span><span class="sxs-lookup"><span data-stu-id="58efe-351">Visualize score results of the recommender system--related items</span></span>

<span data-ttu-id="58efe-352">6개 열 중 첫 번째 열은 입력 데이터에서 제공한 관련 항목을 찾는 데 필요한 특정 항목 ID를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-352">The first of the six columns represents the given item IDs needed to find related items, as provided by the input data.</span></span> <span data-ttu-id="58efe-353">나머지 5개 열에는 항목의 예상되는 관련 항목이 저장되며, 관련성에 따라 내림차순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-353">The other five columns store the predicted related items of the item in descending order in terms of relevance.</span></span> <span data-ttu-id="58efe-354">예를 들어 첫 번째 행에서 135026 항목의 가장 관련성이 높은 항목은 135074이고, 그 다음은 135035, 132875, 135055 및 134992 순입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-354">For example, in the first row, the most relevant item for item 135026 is 135074, followed by 135035, 132875, 135055, and 134992.</span></span>

<span data-ttu-id="58efe-355">**웹 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="58efe-355">**Web service publication**</span></span>

<span data-ttu-id="58efe-356">이러한 실험을 웹 서비스로 게시하여 예측을 얻는 프로세스는 네 개의 각 시나리오와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-356">The process of publishing these experiments as web services to get predictions is similar for each of the four scenarios.</span></span> <span data-ttu-id="58efe-357">두 번째 시나리오에서는 지정된 사용자에게 항목을 추천합니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-357">Here we take the second scenario (recommend items to a given user) as an example.</span></span> <span data-ttu-id="58efe-358">다른 세 가지와 동일한 절차를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-358">You can follow the same procedure with the other three.</span></span>

<span data-ttu-id="58efe-359">학습된 추천 시스템을 학습된 모델로 저장하고 요청된 대로 입력 데이터를 단일 사용자 ID 열로 필터링하면, 그림 25에서와 같이 실험을 연결하여 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-359">Saving the trained recommender system as a trained model and filtering the input data to a single user ID column as requested, you can hook up the experiment as in Figure 25 and publish it as a web service.</span></span>

![음식점 추천 문제의 점수 매기기 실험](./media/machine-learning-interpret-model-results/25.png)

<span data-ttu-id="58efe-361">그림 25.</span><span class="sxs-lookup"><span data-stu-id="58efe-361">Figure 25.</span></span> <span data-ttu-id="58efe-362">음식점 추천 문제의 점수 매기기 실험</span><span class="sxs-lookup"><span data-stu-id="58efe-362">Scoring experiment of the restaurant recommendation problem</span></span>

<span data-ttu-id="58efe-363">웹 서비스를 실행하면 그림 26과 비슷한 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-363">Running the web service, the returned result looks like Figure 26.</span></span> <span data-ttu-id="58efe-364">U1048 사용자에게 추천된 5개의 음식점은 134986, 135018, 134975, 135021 및 132862입니다.</span><span class="sxs-lookup"><span data-stu-id="58efe-364">The five recommended restaurants for user U1048 are 134986, 135018, 134975, 135021, and 132862.</span></span>

![추천 시스템 서비스의 샘플](./media/machine-learning-interpret-model-results/25_1.png)

![샘플 실험 결과](./media/machine-learning-interpret-model-results/26.png)

<span data-ttu-id="58efe-367">그림 26.</span><span class="sxs-lookup"><span data-stu-id="58efe-367">Figure 26.</span></span> <span data-ttu-id="58efe-368">음식점 추천 문제의 웹 서비스 결과</span><span class="sxs-lookup"><span data-stu-id="58efe-368">Web service result of restaurant recommendation problem</span></span>

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
