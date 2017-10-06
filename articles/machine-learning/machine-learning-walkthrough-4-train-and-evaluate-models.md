---
title: "4 단계: 학습 하 고 hello 예측 분석 모델을 평가 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 4 단계: 학습, 점수를 매길 및 Azure 기계 학습 스튜디오에서 여러 모델을 평가 합니다."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="daee1-103">4 단계를 연습: 학습 하 고 hello 예측 분석 모델 평가</span><span class="sxs-lookup"><span data-stu-id="daee1-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="daee1-104">이 항목에서는 hello 연습의 4 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발 합니다.](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="daee1-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="daee1-105">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="daee1-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="daee1-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="daee1-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="daee1-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="daee1-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="daee1-108">**학습 하 고 hello 모델 평가**</span><span class="sxs-lookup"><span data-stu-id="daee1-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="daee1-109">Hello 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="daee1-110">Hello 웹 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="daee1-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="daee1-111">Azure 기계 학습 스튜디오를 사용 하 여 기계 학습 모델을 만들기 위한의 hello 이점 중 하나는 hello 기능 tootry 둘 이상의 유형의 모델 단일 실험에서 한 번에 이며 hello 결과 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="daee1-112">이 유형의 실험을 사용 하면 문제에 대 한 hello 가장 적합 한 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="daee1-113">에서는이 연습에서 개발 하는 hello 실험에서 두 가지 유형의 모델 만든 하 해당 점수 매기기 결과 toodecide 알고리즘 비교 하겠습니다 toouse 우리의 마지막 실험에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="daee1-114">다양한 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-114">There are various models we could choose from.</span></span> <span data-ttu-id="daee1-115">를 사용할 수 있는 toosee hello 모델 확장 hello **기계 학습** hello 모듈 색상표에 노드 펼친 다음 **모델 초기화** 및 그 아래의 hello 노드.</span><span class="sxs-lookup"><span data-stu-id="daee1-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="daee1-116">Hello이이 실험에서는 hello 선택 하겠습니다 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] (SVM) 및 hello [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="daee1-117">기계 학습 알고리즘을 가장 잘 결정할 tooget 도움말 hello toosolve 만들려고 하는 특정 문제에 적합 한, 참조 [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="daee1-118">Hello 모델 학습</span><span class="sxs-lookup"><span data-stu-id="daee1-118">Train hello models</span></span>

<span data-ttu-id="daee1-119">두 hello 추가 [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈 및 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 이 모듈 시험 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="daee1-120">2클래스 향상된 의사 결정 트리</span><span class="sxs-lookup"><span data-stu-id="daee1-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="daee1-121">첫째, hello 승격 된 의사 결정 트리 모델을 설정 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="daee1-122">Hello [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] hello 모듈 색상표에 모듈 hello 캔버스로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="daee1-123">Hello [모델 학습] [ train-model] hello 캔버스로 끌어 모듈과 다음 hello hello 출력에 연결 [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree]모듈 toohello 왼쪽 입력된 포트의 hello [모델 학습] [ train-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="daee1-124">hello [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈 hello 일반 모델에서 초기화 및 [모델 학습] [ train-model] 학습 데이터를 사용 하 여 tootrain hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="daee1-125">Hello 왼쪽의 hello 왼쪽된 출력 연결 [R 스크립트 실행] [ execute-r-script] 모듈 toohello 오른쪽 입력 포트의 hello [모델 학습] [ train-model] (म 모듈 결정 [3 단계](machine-learning-walkthrough-3-create-new-experiment.md) hello 학습용 hello 분할 데이터 모듈의 왼쪽에서 들어오는이 연습에서는 toouse hello 데이터).</span><span class="sxs-lookup"><span data-stu-id="daee1-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="daee1-126">Hello의 hello 출력 중 하나를 두 hello 입력이 필요 하지 않으므로 [R 스크립트 실행] [ execute-r-script] 하므로 삭제할 수 있습니다. 이러한 연결 되지 않은이 실험에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="daee1-127">이제 hello 실험의이 부분에서는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-127">This portion of hello experiment now looks something like this:</span></span>  

![모델 학습][1]

<span data-ttu-id="daee1-129">이제 tootell hello 필요 [모델 학습] [ train-model] 모듈 hello 모델 toopredict hello 신용 위험 값을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="daee1-130">선택 hello [모델 학습] [ train-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="daee1-131">Hello에 **속성** 창에서 클릭 **열 선택기 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="daee1-132">Hello에 **단일 열 선택** 대화 상자에서 아래 hello 검색 필드에 "신용 위험"을 입력 **사용 가능한 열**, 아래 "신용 위험"을 선택 하 고 hello 오른쪽 화살표 단추를 클릭 ( **>** ) toomove "신용 위험" 너무**선택한 열**합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Hello 모델 학습 모듈에 대 한 hello 신용 위험 열 선택][0]

3. <span data-ttu-id="daee1-134">Hello 클릭 **확인** 확인 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="daee1-135">2클래스 Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="daee1-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="daee1-136">다음으로 hello SVM 모델을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="daee1-137">먼저 SVM에 대한 간단한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="daee1-138">향상된 의사 결정 트리는 모든 기능 유형에서 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="daee1-139">그러나 선형 분류자를 생성 하는 hello SVM 모듈, 이후 hello 모델 생성 하는 hello 최상의 테스트 오류 모든 숫자 기능이 hello 때 같은 눈금.</span><span class="sxs-lookup"><span data-stu-id="daee1-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="daee1-140">모든 숫자 tooconvert 기능 toohello 동일한 크기를 조정, "Tanh" 변환을 사용 하 여 우리 (hello로 [데이터 정규화] [ normalize-data] 모듈).</span><span class="sxs-lookup"><span data-stu-id="daee1-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="daee1-141">이 hello [0, 1] 범위에이 숫자를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="daee1-142">문자열 기능 toocategorical 기능 및 toobinary 0/1 기능으로 변환 하는 hello SVM 모듈, 하지 하므로 필요 toomanually 변환 문자열 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="daee1-143">또한 tootransform hello 신용 위험 열 (열 21) 않도록-이 숫자 이면 하지만 hello 값을 학습 하는 것 때문에 tooleave 모델 toopredict hello 단독 것입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="daee1-144">tooset hello SVM 모델을 따르는 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="daee1-145">Hello [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] hello 모듈 색상표에 모듈 hello 캔버스로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="daee1-146">마우스 오른쪽 단추로 클릭 hello [모델 학습] [ train-model] 모듈을 **복사**, hello 캔버스를 마우스 오른쪽 단추로 클릭 한 다음 및 선택 **붙여넣기**합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="daee1-147">hello의 복사본을 hello [모델 학습] [ train-model] 모듈 hello에 원래 hello로 같은 열 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="daee1-148">Hello hello 출력에 연결 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 모듈 toohello 왼쪽 입력된 포트의 hello 둘째 [모델 학습] [ train-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="daee1-149">Hello [데이터 정규화] [ normalize-data] 모듈 hello 캔버스로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="daee1-150">Hello 왼쪽의 hello 왼쪽된 출력 연결 [R 스크립트 실행] [ execute-r-script] (모듈의 출력 포트 hello 다른 모듈 하나 보다 연결된 toomore 수 있다고 표시)이이 모듈의 모듈 toohello 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="daee1-151">남아 있는 hello의 출력 포트 hello 연결 [데이터 정규화] [ normalize-data] 모듈 toohello 오른쪽 입력 포트의 hello 둘째 [모델 학습] [ train-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="daee1-152">실험의 이 부분은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-152">This portion of our experiment should now look something like this:</span></span>  

![Hello 두 번째 모델 학습][2]  

<span data-ttu-id="daee1-154">이제 hello 구성할 [데이터 정규화] [ normalize-data] 모듈:</span><span class="sxs-lookup"><span data-stu-id="daee1-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="daee1-155">Tooselect hello 클릭 [데이터 정규화] [ normalize-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="daee1-156">Hello에 **속성** 창 선택 **Tanh** hello에 대 한 **변환 방법** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="daee1-157">클릭 **열 선택기 시작**, "열 선택 안 함"에 대 한 **Begin With**선택, **Include** hello 첫 번째 드롭다운에서 선택 **열 형식**에 두 번째 드롭다운에서 hello 및 선택 **숫자** hello 세 번째 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="daee1-158">이 모든 hello 숫자 열 (및만 하는 숫자) 변환 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="daee1-159">클릭 하 여이 행의 오른쪽 더하기 기호 (+) toohello hello-이 드롭다운의 행이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="daee1-160">선택 **제외** hello 첫 번째 드롭다운에서 선택 **열 이름을** 에 두 번째 드롭다운에서 hello 및 hello 텍스트 필드에 "신용 위험"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="daee1-161">이 해당 hello 신용 위험 열을 무시 하도록 지정 (이 숫자 이므로이 열은 때문에 변환 됩니다 것을 제외 하지 않은 경우 toodo 필요).</span><span class="sxs-lookup"><span data-stu-id="daee1-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="daee1-162">Hello 클릭 **확인** 확인 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-162">Click hello **OK** check mark.</span></span>  

    ![Hello 데이터 정규화 모듈에 대 한 열 선택][5]

<span data-ttu-id="daee1-164">hello [데이터 정규화] [ normalize-data] 모듈 집합 tooperform hello 신용 위험 열을 제외한 모든 숫자 열에 Tanh 변환 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="daee1-165">점수와 hello 모델 평가</span><span class="sxs-lookup"><span data-stu-id="daee1-165">Score and evaluate hello models</span></span>

<span data-ttu-id="daee1-166">Hello 테스트 데이터 hello에서 분리를 사용 하 여 [분할 데이터] [ split] 모듈 tooscore 우리의 학습 된 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="daee1-167">더 나은 결과 생성 된 hello 두 모델 toosee의 hello 결과 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="daee1-168">Hello 모델 점수 매기기 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="daee1-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="daee1-169">Hello [모델 점수 매기기] [ score-model] 모듈 hello 캔버스로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="daee1-170">Hello 연결 [모델 학습] [ train-model] toohello 연결 된 모듈 [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈 toohello 왼쪽된 입력 포트의 hello [모델 점수 매기기] [ score-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="daee1-171">Hello 오른쪽 연결 [R 스크립트 실행] [ execute-r-script] 모듈 (테스트 데이터) toohello 오른쪽 입력 포트의 hello [모델 점수 매기기] [ score-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![모델 점수 매기기 모듈이 연결됨][6]
   
   <span data-ttu-id="daee1-173">hello [모델 점수 매기기] [ score-model] 모듈 hello 모델을 통해 실행 데이터를 테스트 하는 hello에서 hello 신용 정보를 지금 사용할 수 있습니다 및 실제 hello로 hello 모델을 생성 하는 비교 hello 예측 신용 위험 hello 테스트 데이터의에서 열입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="daee1-174">복사 및 붙여넣기 hello [모델 점수 매기기] [ score-model] 모듈 toocreate 두 번째 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="daee1-175">Hello SVM 모델의 hello 출력에 연결 (즉, hello 출력의 hello 포트 [모델 학습] [ train-model] toohello 연결 된 모듈 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 모듈) toohello 입력 포트의 hello 둘째 [모델 점수 매기기] [ score-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="daee1-176">Hello SVM 모델에 대 한 toohello 학습 데이터와 같이 동일한 변환 toohello 테스트 데이터를 hello toodo를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="daee1-177">따라서 복사한 hello [데이터 정규화] [ normalize-data] 모듈 toocreate 두 번째 사본 toohello 오른쪽 연결 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="daee1-178">Hello hello 왼쪽된 출력에 두 번째 연결 [데이터 정규화] [ normalize-data] 모듈 toohello 오른쪽 입력 포트의 hello 둘째 [모델 점수 매기기] [ score-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![두 모델 점수 매기기 모듈이 연결됨][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="daee1-180">Hello 모델 평가 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="daee1-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="daee1-181">사용 하 여, tooevaluate 두 점수 매기기 결과 hello과 비교 하는 [모델 평가] [ evaluate-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="daee1-182">Hello [모델 평가] [ evaluate-model] 모듈 hello 캔버스로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="daee1-183">Hello의 hello 출력 포트를 연결 [모델 점수 매기기] [ score-model] hello와 연관 된 모듈에는 의사 결정 트리 모델 toohello 왼쪽 입력 포트의 hello 승격 된 [모델 평가] [ evaluate-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="daee1-184">다른 hello 연결 [모델 점수 매기기] [ score-model] 모듈 toohello 오른쪽 입력 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![모델 평가 모듈이 연결됨][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="daee1-186">Hello 실험을 실행 하 고 hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="daee1-187">toorun 실험 hello를 hello 클릭 **실행** hello 캔버스 아래 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="daee1-188">몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-188">It may take a few minutes.</span></span> <span data-ttu-id="daee1-189">각 모듈에는 회전 표시기는이 서비스를 실행 하 고 hello 모듈 완료 되 면 녹색 확인 표시가 표시 하는 다음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="daee1-190">모든 hello 모듈 확인 표시가 있으면 hello 실험 이미 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="daee1-191">hello 실험 같아야 이제 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-191">hello experiment should now look something like this:</span></span>  

![두 모델 모두 평가][3]

<span data-ttu-id="daee1-193">toocheck hello 결과 클릭 hello의 출력 포트 hello [모델 평가] [ evaluate-model] 모듈과 선택 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="daee1-194">hello [모델 평가] [ evaluate-model] 모듈 곡선과 hello 두 점수가 매겨진된 모델의 toocompare hello 결과 허용 하는 메트릭을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="daee1-195">수신기 연산자 특성 (ROC) 곡선, 전체 자릿수/회수 곡선 또는 리프트 곡선으로 hello 결과 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="daee1-196">혼동 행렬, (AUC) hello 곡선 아래의 영역 hello에 대 한 누적 값 및 기타 메트릭을 표시 하는 추가 데이터에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="daee1-197">왼쪽 또는 오른쪽 이동 hello 슬라이더를 통해 hello 임계값을 변경 하 고 hello 메트릭 집합이 미치는 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="daee1-198">toohello hello 그래프의 오른쪽 클릭 **점수가 매겨진 데이터 집합** 또는 **dataset toocompare 점수가 매겨진** toohighlight hello 관련된 곡선과 toodisplay hello 관련 메트릭 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="daee1-199">Hello 곡선에 대 한 hello 범례에서 왼쪽 입력된 포트의 hello toohello 해당 "점수가 매겨진 데이터 집합" [모델 평가] [ evaluate-model] 모듈-경우에는 hello 승격 된 의사 결정 트리 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="daee1-200">"점수가 매겨진 데이터 집합 toocompare" toohello 오른쪽 입력된 포트-경우에 hello SVM 모델은 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="daee1-201">이러한 레이블 중 하나를 클릭 하면 해당 모델에 대 한 hello 곡선은 강조 표시 하 고 hello 다음 그래픽에에서 표시 된 것과 같이 hello 해당 메트릭이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![모델에 대한 ROC 곡선][4]

<span data-ttu-id="daee1-203">이러한 값을 검사 하 여 모델에 대 한 원하는 결과 hello 가장 가까운 toogiving을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="daee1-204">다시 돌아가서 hello 서로 다른 모델에 매개 변수 값을 변경 하 여 실험을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="daee1-205">hello 과학 및 이러한 결과 해석 하 고 hello 모델 성능을 튜닝의 기술에는이 연습의 외부 hello 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="daee1-206">자세한 도움말을 보려면 다음 문서는 hello을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="daee1-207">Tooevaluate는 Azure 기계 학습에서 성능을 모델링 하는 방법</span><span class="sxs-lookup"><span data-stu-id="daee1-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="daee1-208">Azure 기계 학습에서 매개 변수 toooptimize 알고리즘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="daee1-209">Azure Machine Learning에서 모델 결과 해석</span><span class="sxs-lookup"><span data-stu-id="daee1-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="daee1-210">해당 반복에 대 한 기록을 hello 실험을 실행할 때마다 hello 실행 기록에에서 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="daee1-211">이러한 반복을 볼 수 있으며 그 중 tooany 클릭 하 여 반환 **실행 기록 보기** hello 캔버스 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="daee1-212">클릭할 수도 있습니다 **이전 실행** hello에 **속성** 창 tooreturn toohello 반복 바로 앞에 나오는 hello 열어 놓은 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="daee1-213">클릭 하 여 실험의 모든 반복의 복사본을 만들 수 있습니다 **SAVE AS** hello 캔버스 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="daee1-214">Hello 실험을 사용 하 여 **요약** 및 **설명** 속성 tookeep 레코드가 실험 반복에서 시도 하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="daee1-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="daee1-215">자세한 내용은 [Azure 기계 학습 스튜디오에서 실험 반복 관리](machine-learning-manage-experiment-iterations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="daee1-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="daee1-216">**다음: [hello 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="daee1-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
