---
title: "4단계: 예측 분석 모델 학습 및 평가 | Microsoft Docs"
description: "예측 솔루션 개발 연습 4단계: Azure 기계 학습 스튜디오에서 다중 모델을 학습하고, 점수를 매기고, 평가합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="b1d35-103">연습 4단계: 예측 분석 모델 학습 및 평가</span><span class="sxs-lookup"><span data-stu-id="b1d35-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="b1d35-104">이 토픽에는 연습의 4번째 단계인 [Azure Machine Learning에서 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="b1d35-105">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b1d35-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="b1d35-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="b1d35-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="b1d35-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="b1d35-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="b1d35-108">**모델 학습 및 평가**</span><span class="sxs-lookup"><span data-stu-id="b1d35-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="b1d35-109">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="b1d35-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="b1d35-110">웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="b1d35-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="b1d35-111">Azure Machine Learning Studio를 사용하여 기계 학습 모델을 만들 때의 이점 중 단일 실험에서 한 번에 두 개 이상의 모델 유형을 시도하고 결과를 비교할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="b1d35-112">이 유형의 실험을 사용하면 문제에 대한 최상의 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="b1d35-113">이 연습으로 개발하고 있는 실험에서는 두 가지 모델을 만들고 모델의 점수 매기기 결과를 비교하여 최종 실험에서 사용할 알고리즘을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="b1d35-114">다양한 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-114">There are various models we could choose from.</span></span> <span data-ttu-id="b1d35-115">사용할 수 있는 모델을 보려면 모듈 팔레트에서 **Machine Learning** 노드를 확장하고 **모델 초기화** 및 그 아래 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="b1d35-116">이 실험에서는 [2클래스 SVM(Support Vector Machine)][two-class-support-vector-machine] 및 [2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree] 모듈을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="b1d35-117">해결하려는 특정 문제에 가장 적합한 기계 학습 알고리즘을 결정하는 데 대한 도움말을 보려면 [Microsoft Azure 기계 학습을 위한 알고리즘 선택 방법](machine-learning-algorithm-choice.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1d35-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="b1d35-118">모델 학습</span><span class="sxs-lookup"><span data-stu-id="b1d35-118">Train the models</span></span>

<span data-ttu-id="b1d35-119">이 실험에서는 [2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree] 모듈 및 [2클래스 지원 벡터 컴퓨터][two-class-support-vector-machine] 모듈을 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="b1d35-120">2클래스 향상된 의사 결정 트리</span><span class="sxs-lookup"><span data-stu-id="b1d35-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="b1d35-121">먼저 향상된 의사 결정 트리 모델을 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="b1d35-122">모듈 팔레트에서 [2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree] 모듈을 찾고 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="b1d35-123">[모델 학습][train-model] 모듈을 찾고 캔버스로 끌고 나서 [2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree] 모듈의 출력을 [모델 학습][train-model] 모듈의 왼쪽 입력 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="b1d35-124">[2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree] 모듈은 일반 모델을 초기화하고 [모델 학습][train-model]에서는 학습 데이터를 사용하여 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="b1d35-125">왼쪽 [R 스크립트 실행][execute-r-script] 모듈의 왼쪽 출력을 [모델 학습][train-model] 모듈의 오른쪽 입력 부분에 연결합니다(이 연습의 [3단계](machine-learning-walkthrough-3-create-new-experiment.md)에서 학습을 위해 데이터 분할 모듈 왼쪽의 데이터를 사용하기로 결정함).</span><span class="sxs-lookup"><span data-stu-id="b1d35-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b1d35-126">이 실험에서는 [R 스크립트 실행][execute-r-script] 모듈에 대한 입력 중 두 개와 출력 중 하나가 필요하지 않으므로 연결되지 않은 상태로 유지해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="b1d35-127">실험의 이 부분은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-127">This portion of the experiment now looks something like this:</span></span>  

![모델 학습][1]

<span data-ttu-id="b1d35-129">이제 모델을 통해 신용 위험 값을 예측할 것임을 [모델 학습][train-model] 모듈에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="b1d35-130">[모델 학습][train-model] 모듈을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="b1d35-131">**속성** 창에서 **열 선택기 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="b1d35-132">**단일 열 선택** 대화 상자에서 **사용 가능한 열** 아래의 검색 필드에 "신용 위험"을 입력하고 오른쪽 화살표 단추(**>**)를 클릭하여 "신용 위험"을 **선택한 열**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![모델 학습 모듈에 대한 신용 위험 열 선택][0]

3. <span data-ttu-id="b1d35-134">**확인** 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="b1d35-135">2클래스 Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="b1d35-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="b1d35-136">다음으로 SVM 모델을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="b1d35-137">먼저 SVM에 대한 간단한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="b1d35-138">향상된 의사 결정 트리는 모든 기능 유형에서 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="b1d35-139">그러나 SVM 모듈은 선형 분류자를 생성하므로 여기서 생성하는 모델에는 모든 숫자 기능의 크기가 같을 때 최적의 테스트 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="b1d35-140">모든 숫자 기능을 같은 크기로 변환하려면 "Tanh" 변환을 사용합니다([데이터 정규화][normalize-data] 모듈과 함께).</span><span class="sxs-lookup"><span data-stu-id="b1d35-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="b1d35-141">그러면 숫자가 [0,1] 범위로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="b1d35-142">SVM 모듈은 문자열 기능을 범주 기능으로 변환되고 나서 이진 0/1 기능으로 변환되므로 문자열 기능을 수동으로 변환할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="b1d35-143">또한 신용 위험 열(열 21)을 변환하지 않으려고 합니다. 이 열은 숫자 값이지만 모델을 학습하여 예측할 값이므로 단독으로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="b1d35-144">SVM 모델을 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="b1d35-145">모듈 팔레트에서 [2클래스 Support Vector Machine][two-class-support-vector-machine] 모듈을 찾고 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="b1d35-146">[모델 학습][train-model] 모듈을 마우스 오른쪽 단추로 클릭하고 **복사**를 선택하고 나서 캔버스를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="b1d35-147">[모델 학습][train-model] 모듈의 복사본에는 원래 모듈과 같은 열이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="b1d35-148">[2클래스 Support Vector Machine][two-class-support-vector-machine] 모듈의 출력을 두 번째 [모델 학습][train-model] 모듈의 왼쪽 입력 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="b1d35-149">[데이터 정규화][normalize-data] 모듈을 찾고 캔버스로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="b1d35-150">이 모듈의 입력에 왼쪽 [R 스크립트 실행][execute-r-script] 모듈의 왼쪽 출력을 연결합니다. 모듈의 출력 포트는 두 개 이상의 다른 모듈에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="b1d35-151">[데이터 정규화][normalize-data] 모듈의 왼쪽 출력 포트를 두 번째 [모델 학습][train-model] 모듈의 오른쪽 입력 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="b1d35-152">실험의 이 부분은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-152">This portion of our experiment should now look something like this:</span></span>  

![두 번째 모델 학습][2]  

<span data-ttu-id="b1d35-154">이제 [데이터 정규화][normalize-data] 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="b1d35-155">[데이터 정규화][normalize-data] 모듈을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="b1d35-156">**속성** 창에서 **변환 메서드** 매개 변수에 대해 **Tanh**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="b1d35-157">**열 선택기 시작**을 클릭하고 **시작 문자**에 대해 "열 없음"을 선택한 후, 첫 번째 드롭다운에서 **포함**을, 두 번째 드롭다운에서 **열 형식**을, 세 번째 드롭다운에서 **숫자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="b1d35-158">이렇게 하면 모든 숫자 열(및 숫자만)이 변환되도록 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="b1d35-159">이 행 오른쪽에 있는 더하기 기호(+)를 클릭하면 새 드롭다운 행이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="b1d35-160">첫 번째 드롭다운에서 **제외**를 선택하고, 두 번째 드롭다운에서 **열 이름**을 선택하고, 텍스트 필드에 "신용 위험"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="b1d35-161">이렇게 하면 신용 위험 열이 무시됩니다. 이 열은 숫자이므로 제외하지 않을 경우 변환되기 때문에 이 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="b1d35-162">**확인** 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-162">Click the **OK** check mark.</span></span>  

    ![데이터 정규화 모듈의 열 선택][5]

<span data-ttu-id="b1d35-164">이제 [데이터 정규화][normalize-data] 모듈은 신용 위험 열을 제외한 모든 숫자 열에서 Tanh 변환을 수행하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="b1d35-165">모델 점수 매기기 및 평가</span><span class="sxs-lookup"><span data-stu-id="b1d35-165">Score and evaluate the models</span></span>

<span data-ttu-id="b1d35-166">[데이터 분할][split] 모듈을 통해 구분된 테스트 데이터를 사용하여 학습된 모듈의 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="b1d35-167">그리고 나서 두 모델의 결과를 비교하여 더 나은 결과를 생성한 모듈을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="b1d35-168">모델 점수 매기기 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="b1d35-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="b1d35-169">[모델 점수 매기기][score-model] 모듈을 찾아 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="b1d35-170">[2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree] 모듈에 연결되어 있는 [모델 학습l][train-model] 모듈을 [모델 점수 매기기][score-model] 모듈의 왼쪽 입력 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="b1d35-171">[모델 점수 매기기][score-model] 모듈의 오른쪽 입력 포트에 오른쪽 [R 스크립트 실행][execute-r-script] 모듈(테스트 데이터)을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![모델 점수 매기기 모듈이 연결됨][6]
   
   <span data-ttu-id="b1d35-173">[모델 점수 매기기][score-model] 모듈에서 테스트 데이터의 신용 정보를 사용하고, 모듈을 통해 실행하고, 모델이 생성하는 예측을 테스트 데이터의 실제 신용 위험 열과 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="b1d35-174">[모델 점수 매기기][score-model] 모듈을 복사하고 붙여넣어 두 번째 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="b1d35-175">SVM 모델의 출력(즉, [2클래스 Support Vector Machine][two-class-support-vector-machine] 모듈에 연결된 [모델 학습][train-model] 모듈의 출력 포트)을 두 번째 [모델 점수 매기기][score-model] 모듈의 입력 부분에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="b1d35-176">SVM 모델에서는 학습 데이터에 대해 수행한 것과 같은 변환을 테스트 데이터에 대해 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="b1d35-177">따라서 [데이터 정규화][normalize-data] 모듈을 복사하고 붙여넣고 두 번째 복사본을 만들고 오른쪽 [R 스크립트 실행][execute-r-script] 모듈에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="b1d35-178">두 번째 [모델 점수 매기기][score-model] 모듈의 오른쪽 입력 포트에 두 번째 [데이터 정규화][normalize-data] 모듈의 왼쪽 출력을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![두 모델 점수 매기기 모듈이 연결됨][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="b1d35-180">모델 평가 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="b1d35-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="b1d35-181">점수 매기기 결과 두 개를 평가하고 비교하기 위해 [모델 평가][evaluate-model] 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="b1d35-182">[모델 평가][evaluate-model] 모듈을 찾아 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="b1d35-183">[모델 평가][evaluate-model] 모듈의 왼쪽 입력 포트에 향상된 의사 결정 트리 모델과 연결된 [모델 점수 매기기][score-model] 모듈의 출력 포트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="b1d35-184">다른 [모델 점수 매기기][score-model] 모듈을 오른쪽 입력 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![모델 평가 모듈이 연결됨][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="b1d35-186">실험 실행 및 결과 확인</span><span class="sxs-lookup"><span data-stu-id="b1d35-186">Run the experiment and check the results</span></span>

<span data-ttu-id="b1d35-187">실험을 실행하려면 캔버스 아래에서 **실행** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="b1d35-188">몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-188">It may take a few minutes.</span></span> <span data-ttu-id="b1d35-189">각 모듈에 실행 중임을 나타내는 회전 표시기가 표시되고 나서 모듈이 완료되면 녹색 확인 표시가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="b1d35-190">모든 모듈에 확인 표시가 있으면 실험 실행이 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="b1d35-191">이제 실험이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-191">The experiment should now look something like this:</span></span>  

![두 모델 모두 평가][3]

<span data-ttu-id="b1d35-193">결과를 확인하려면 [모델 평가][evaluate-model] 모듈의 출력 포트를 클릭하고 **시각화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="b1d35-194">[모델 평가][evaluate-model] 모듈에서는 점수를 매긴 모델 두 개의 결과를 비교할 수 있는 곡선 및 메트릭 쌍을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="b1d35-195">결과를 ROC(Receiver Operator Characteristic) 곡선, 정밀도/리콜 곡선 또는 리프트 곡선으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="b1d35-196">표시된 추가 데이터에는 혼동 행렬, AUC(Area Under the Curve)에 대한 누적 값 및 기타 메트릭이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="b1d35-197">슬라이더를 왼쪽이나 오른쪽으로 이동하여 임계값을 변경하고 메트릭 집합에 어떤 영향을 미치는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="b1d35-198">그래프 오른쪽에 있는 **점수를 매긴 데이터 집합** 또는 **비교할 점수를 매긴 데이터 집합**을 클릭하여 관련 곡선을 강조 표시하고 아래에 관련 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="b1d35-199">곡선 범례에서 "점수를 매긴 데이터 집합"은 [모델 평가][evaluate-model] 모듈의 왼쪽 입력 포트(이 경우 향상된 의사 결정 트리 모델)에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="b1d35-200">"비교할 점수를 매긴 데이터 집합"은 오른쪽 입력 포트(이 경우 SVM 모델)에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="b1d35-201">이러한 레이블 중 하나를 클릭하면 다음 그래픽에 표시된 것처럼 해당 모델의 곡선이 강조 표시되고 해당 메트릭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![모델에 대한 ROC 곡선][4]

<span data-ttu-id="b1d35-203">이러한 값을 검토하면 찾고 있는 결과에 가장 근접한 모델을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="b1d35-204">돌아가서 다른 모델에서 매개 변수 값을 변경하여 실험을 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="b1d35-205">이러한 결과를 해석하고 모델 성능을 조정하는 과학 및 미술은 이 연습의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="b1d35-206">추가 도움말을 보려면 다음 문서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="b1d35-207">Azure Machine Learning에서 모델 성능을 평가하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1d35-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="b1d35-208">Azure Machine Learning에서 알고리즘을 최적화하는 매개 변수 선택</span><span class="sxs-lookup"><span data-stu-id="b1d35-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="b1d35-209">Azure Machine Learning에서 모델 결과 해석</span><span class="sxs-lookup"><span data-stu-id="b1d35-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="b1d35-210">실험을 실행할 때마다 해당 반복에 대한 레코드가 실행 기록에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="b1d35-211">이러한 반복을 확인하고 캔버스 아래에서 **실행 기록 보기**를 클릭하여 원하는 반복으로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="b1d35-212">**속성** 창에서 **이전 실행**을 클릭하여 열었던 반복의 바로 이전 반복으로 돌아갈 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="b1d35-213">캔버스 아래에서 **다른 이름으로 저장**을 클릭하여 실험을 반복하도록 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="b1d35-214">실험의 **요약** 및 **설명** 속성을 사용하면 실험 반복에서 시도한 항목을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d35-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="b1d35-215">자세한 내용은 [Azure 기계 학습 스튜디오에서 실험 반복 관리](machine-learning-manage-experiment-iterations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1d35-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="b1d35-216">**다음: [웹 서비스 배포](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="b1d35-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
