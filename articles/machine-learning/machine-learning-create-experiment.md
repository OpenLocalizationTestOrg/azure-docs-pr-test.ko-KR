---
title: "기계 학습 스튜디오에서 간단한 실험 aaaA | Microsoft Docs"
description: "이 기계 학습 자습서에서는 쉬운 데이터 과학 실험을 안내합니다. 회귀 알고리즘을 사용 하는 자동차의 hello 가격을 예측할 합니다 했습니다."
keywords: "실험, 선형 회귀, 기계 학습 알고리즘, 기계 학습 자습서, 예측 모델링 기술, 데이터 과학 실험"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="7bcae-105">기계 학습 자습서: Azure 기계 학습 스튜디오에서 첫 번째 데이터 과학 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="7bcae-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="7bcae-106">**Azure Machine Learning Studio**를 사용한 경험이 없는 경우 이 자습서는 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="7bcae-107">이 자습서에서는 살펴봅니다 방법 toouse Studio hello에 대 한 첫 번째 toocreate 기계 학습 실험을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="7bcae-108">hello 실험 제조업체와 기술 사양 등 다른 변수를 기반으로 하는 자동차의 hello 가격을 예측 하는 분석 모델을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="7bcae-109">이 자습서에서는 사용 하 여 실험에 어떻게 toodrag 놓기 모듈의 기본 사항 hello 이들을 서로 연결 hello 실험을 실행 하 고 hello 결과를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="7bcae-110">하지 않겠습니다 toodiscuss hello 기계 학습의 일반 항목 또는 방법을 사용 하 여 tooselect 환영 100 + 기본 제공 알고리즘 및 데이터 조작 모듈 스튜디오에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="7bcae-111">새 toomachine 학습 인 경우 hello 비디오 시리즈 [초보자를 위한 데이터 과학](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) 좋은 위치 toostart 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="7bcae-112">이 비디오 시리즈 일상적인 언어 및 개념을 사용 하 여 충분히 소개 toomachine 학습입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="7bcae-113">기계 학습에 익숙한 경우, 기계 학습 스튜디오 및 hello 기계 학습 포함 된 알고리즘에 대 한 일반적인 내용은 원하는 좋은 몇 가지 리소스가 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="7bcae-114">기계 학습 스튜디오란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7bcae-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="7bcae-115">- Studio의 차원 높은 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="7bcae-116">[알고리즘 예제를 사용한 기본 사항 학습 컴퓨터](machine-learning-basics-infographic-with-algorithm-examples.md) -이 인포 그래픽은 toolearn hello 다양 한 유형의 기계 학습 스튜디오에 포함 된 기계 학습 알고리즘에 대 한 자세한를 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="7bcae-117">[기계 학습 설명서](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -이 가이드에서는 위의 hello 인포 그래픽 동일 하지만 대화형 형식으로 유사한 정보를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="7bcae-118">[시스템 학습 알고리즘 치트 시트](machine-learning-algorithm-cheat-sheet.md) 및 [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md) -이 다운로드할 수 있는 포스터와 함께 제공 된 문서 심층에서 hello Studio 알고리즘에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="7bcae-119">[기계 학습 스튜디오: 알고리즘 및 모듈 도움말](https://msdn.microsoft.com/library/azure/dn905974.aspx) -이 hello 기계 학습 알고리즘을 포함 하 여 모든 스튜디오 모듈에 대 한 전체 참조</span><span class="sxs-lookup"><span data-stu-id="7bcae-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="7bcae-120">기계 학습 스튜디오는 도움이 되나요?</span><span class="sxs-lookup"><span data-stu-id="7bcae-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="7bcae-121">기계 학습 스튜디오 예측 모델링 기술로 미리 프로그래밍 끌어서 놓기 모듈을 사용 하 여 실험을 쉽게 tooset이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="7bcae-122">대화형 시각적 작업 영역을 사용하여 ***데이터 집합*** 및 분석 ***모듈***을 대화형 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="7bcae-123">함께 tooform를 연결 된 ***실험*** 기계 학습 스튜디오에서 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="7bcae-124">하면 ***모델을 만들***, ***hello 모델을 학습***, 및 ***점수 및 테스트 모델 hello***합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="7bcae-125">Hello 실험을 편집 하면 모델 디자인에 대해 반복할 수 및 원하는 결과 hello 제공 될 때까지 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="7bcae-126">모델이 준비되면 ***웹 서비스***로 게시하여 다른 사람이 새 데이터를 전송하고 예측 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="7bcae-127">Machine Learning Studio 열기</span><span class="sxs-lookup"><span data-stu-id="7bcae-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="7bcae-128">Studio에서 시작 tooget 너무 이동[https://studio.azureml.net](https://studio.azureml.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="7bcae-129">이전에 Machine Learning Studio에 등록했다면 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="7bcae-130">그렇지 않은 경우 **여기서 등록**을 클릭하고 무료와 유료 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="7bcae-131">![TooMachine 학습 스튜디오에 로그인][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="7bcae-132">
***TooMachine 학습 스튜디오에 로그인***</span><span class="sxs-lookup"><span data-stu-id="7bcae-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="7bcae-133">5 단계 toocreate 실험</span><span class="sxs-lookup"><span data-stu-id="7bcae-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="7bcae-134">이 컴퓨터 학습 자습서의 다섯 가지 기본 단계 toobuild 기계 학습 스튜디오 toocreate, 학습의 실험을 수행 하 고 모델 점수를 매깁니다. 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="7bcae-135">**모델 만들기**</span><span class="sxs-lookup"><span data-stu-id="7bcae-135">**Create a model**</span></span>
    - <span data-ttu-id="7bcae-136">[1단계: 데이터 가져오기]</span><span class="sxs-lookup"><span data-stu-id="7bcae-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="7bcae-137">[2 단계: hello 데이터 준비]</span><span class="sxs-lookup"><span data-stu-id="7bcae-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="7bcae-138">[3단계: 기능 정의]</span><span class="sxs-lookup"><span data-stu-id="7bcae-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="7bcae-139">**Hello 모델 학습**</span><span class="sxs-lookup"><span data-stu-id="7bcae-139">**Train hello model**</span></span>
    - <span data-ttu-id="7bcae-140">[4단계: 학습 알고리즘 선택 및 적용]</span><span class="sxs-lookup"><span data-stu-id="7bcae-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="7bcae-141">**모델을 hello 점수 및 테스트**</span><span class="sxs-lookup"><span data-stu-id="7bcae-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="7bcae-142">[5단계: 새 자동차 가격 예측]</span><span class="sxs-lookup"><span data-stu-id="7bcae-142">[Step 5: Predict new automobile prices]</span></span>

[1단계: 데이터 가져오기]: #step-1-get-data
[2 단계: hello 데이터 준비]: #step-2-prepare-the-data
[3단계: 기능 정의]: #step-3-define-features
[4단계: 학습 알고리즘 선택 및 적용]: #step-4-choose-and-apply-a-learning-algorithm
[5단계: 새 자동차 가격 예측]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="7bcae-148">Hello의 작업 복사본을 찾을 수 있습니다 다음 hello에 실험 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="7bcae-149">너무 이동**[여 첫 번째 데이터 과학 자동차 가격 예측 실험](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  클릭 **Studio에서 열기** toodownload hello 실험에 기계 학습의 복사본 스튜디오 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="7bcae-150">1단계: 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="7bcae-150">Step 1: Get data</span></span>

<span data-ttu-id="7bcae-151">hello 먼저 tooperform 기계 학습 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="7bcae-152">Machine Learning Studio에는 사용할 수 있고 다양한 원본에서 데이터를 가져올 수 있는 여러 샘플 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="7bcae-153">이 예제에서는 hello 샘플 데이터 집합 사용 **자동차 가격 데이터 (Raw)**, 작업 영역에 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="7bcae-154">이 데이터 집합에는 제조업체, 모델, 기술 사양 및 가격과 같은 정보를 포함하여 여러 개별 자동차에 대한 항목이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="7bcae-155">Tooget 실험으로 데이터 집합을 hello 하는 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="7bcae-156">클릭 하 여 새 실험 만들기 **+ 새로 만들기** hello 기계 학습 스튜디오 창의 hello 맨 아래에 선택 **실험**를 선택한 후 **빈 실험**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="7bcae-157">hello 실험에는 hello 캔버스의 hello 위쪽에 표시 될 수 있는 기본 이름이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="7bcae-158">이 텍스트를 선택 하 고 이름을 바꾸거나 toosomething 의미 있는 예를 들어 **자동차 가격 예측**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="7bcae-159">hello 이름 toobe 고유 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-159">hello name doesn't need toobe unique.</span></span>

    ![Hello 실험 이름 바꾸기][rename-experiment]

2. <span data-ttu-id="7bcae-161">hello 실험 캔버스의 toohello 왼쪽 데이터 집합 및 모듈의 팔레트입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="7bcae-162">형식 **automobile** 이 색상표 toofind hello 데이터 집합의 레이블이 지정 된 hello 상단 hello 검색 상자에 **자동차 가격 데이터 (Raw)**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="7bcae-163">이 데이터 집합 toohello 실험 캔버스를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="7bcae-164">![Hello 자동차 데이터 집합을 찾아서 hello 실험 캔버스로 끌어][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="7bcae-165">***Hello 자동차 데이터 집합을 찾아서 hello 실험 캔버스로 끌어***</span><span class="sxs-lookup"><span data-stu-id="7bcae-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="7bcae-166">toosee이이 데이터는 모양을 처럼 hello 자동차 데이터 집합의 hello 맨 아래에 hello 출력 포트를 클릭 한 다음 선택 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="7bcae-167">![Hello 출력 포트를 클릭 하 고 "시각화"를 선택 합니다.][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="7bcae-168">
***Hello 출력 포트를 클릭 하 고 "시각화"를 선택 합니다.***</span><span class="sxs-lookup"><span data-stu-id="7bcae-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="7bcae-169">데이터 집합 및 모듈은 입력과 출력 포트 작은 원을 표시-hello 위쪽에, 입력된 포트를 나타내는 출력 hello 맨 아래에는 포트.</span><span class="sxs-lookup"><span data-stu-id="7bcae-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="7bcae-170">실험을 통해 데이터 흐름 toocreate 다른 tooan 입력된 포트의 단일 모듈의 출력 포트로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="7bcae-171">언제 든 지 어떤 hello 데이터가 표시 되는 해당 시점 hello 데이터 흐름에서 데이터 집합 또는 모듈 toosee의 출력 포트 hello 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="7bcae-172">이 샘플 데이터 집합에 자동차의 각 인스턴스에 행으로 나타나고 각 자동차와 연결 된 hello 변수 열으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="7bcae-173">특정 자동차에 대 한 hello 변수를 제공 하겠습니다 tootry toopredict hello 가격 맨 오른쪽 열 (열의 26 "price").</span><span class="sxs-lookup"><span data-stu-id="7bcae-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="7bcae-174">![Hello 데이터 시각화 창에서 hello 자동차 데이터 보기][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="7bcae-175">
***Hello 데이터 시각화 창에서 hello 자동차 데이터 보기***</span><span class="sxs-lookup"><span data-stu-id="7bcae-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="7bcae-176">Hello를 클릭 하 여 시각화 창 닫기 hello "**x**" hello 오른쪽 위 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="7bcae-177">2 단계: hello 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="7bcae-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="7bcae-178">데이터 집합은 일반적으로 전처리를 거쳐야 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="7bcae-179">예를 들어 보았을 것 hello 누락 된 다양 한 행의 hello 열에 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="7bcae-180">이러한 누락 값 정리 hello 모델 hello 데이터를 정확 하 게 분석할 수 있도록 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="7bcae-181">지금은 누락된 값이 있는 행을 모두 제거하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="7bcae-182">또한 hello **정규화 손실** hello 모델에서 해당 열 모두 제외 하도록 열에 누락 값의 상당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="7bcae-183">누락 된 값 입력된 데이터에서 청소 hello는 hello 모듈의 대부분을 사용 하기 위한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="7bcae-184">먼저 hello를 제거 하는 모듈 추가 **정규화 손실** 열 완전히 누락 된 데이터가 모든 행을 제거 하는 다른 모듈을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="7bcae-185">형식 **열 선택** hello 모듈 색상표 toofind hello hello 맨 hello 검색 상자에 [데이터 집합의 열 선택] [ select-columns] 모듈을 끌어와서 toohello 실험 캔버스 .</span><span class="sxs-lookup"><span data-stu-id="7bcae-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="7bcae-186">이 모듈에서는 tooinclude 하거나에서 제외할 데이터 열을 모델 hello tooselect 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="7bcae-187">Hello의 hello 출력 포트를 연결 **자동차 가격 데이터 (Raw)** dataset toohello 입력 포트의 hello [데이터 집합의 열 선택] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="7bcae-188">![Hello "Dataset에서 열 선택" 모듈 toohello 실험 캔버스에 추가 하 고 연결][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="7bcae-189">***Hello "Dataset에서 열 선택" 모듈 toohello 실험 캔버스에 추가 하 고 연결***</span><span class="sxs-lookup"><span data-stu-id="7bcae-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="7bcae-190">Hello 클릭 [데이터 집합의 열 선택] [ select-columns] 모듈과 클릭 **열 선택기 시작** hello에 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="7bcae-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="7bcae-191">Hello 왼쪽에서 클릭 **규칙**</span><span class="sxs-lookup"><span data-stu-id="7bcae-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="7bcae-192">**다음으로 시작**에서 **모든 열**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="7bcae-193">이렇게 하면 [데이터 집합의 열 선택] [ select-columns] (tooexclude에 대 한 하는 열)을 제외한 모든 hello 열을 통해 toopass 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="7bcae-194">Hello 드롭다운 목록에서 선택 **제외** 및 **열 이름을**, 다음 hello 텍스트 상자 안쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="7bcae-195">열 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-195">A list of columns is displayed.</span></span> <span data-ttu-id="7bcae-196">선택 **정규화 손실**, 및 추가 된 toohello 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="7bcae-197">Hello (정상)이 확인 표시 단추 tooclose hello 열 선택 (오른쪽 hello)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="7bcae-198">![Hello 열 선택기 시작 하 고 "정규화 손실" hello 열 제외][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="7bcae-199">***Hello 열 선택기 시작 하 고 "정규화 손실" hello 열 제외***</span><span class="sxs-lookup"><span data-stu-id="7bcae-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="7bcae-200">지금은 hello 속성 창에 대 한 **데이터 집합의 열 선택** 통과 하 게 할 모든 열을 통해 제외 하 고 hello 데이터 집합에서 나타냅니다 **정규화 손실**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="7bcae-201">![해당 "정규화 손실" hello 열은 제외 hello 속성 창 표시][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="7bcae-202">***해당 "정규화 손실" hello 열은 제외 hello 속성 창 표시***</span><span class="sxs-lookup"><span data-stu-id="7bcae-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="7bcae-203">클릭 hello 모듈 및 텍스트를 입력할 주석 tooa 모듈을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="7bcae-204">한 눈에 볼 수 있습니다이 실험에서 hello 모듈을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="7bcae-205">이 경우 hello를 두 번 클릭 [데이터 집합의 열 선택] [ select-columns] 모듈 및 형식 hello 주석 "제외 정규화 손실."</span><span class="sxs-lookup"><span data-stu-id="7bcae-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="7bcae-206">![모듈 tooadd 주석을 두 번 클릭][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="7bcae-207">***모듈 tooadd 주석을 두 번 클릭***</span><span class="sxs-lookup"><span data-stu-id="7bcae-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="7bcae-208">끌어서 hello [누락 데이터 정리] [ clean-missing-data] 모듈 toohello 캔버스를 실험 하 고 toohello 연결 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="7bcae-209">Hello에 **속성** 창 선택 **전체 행 제거** 아래 **Cleaning 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="7bcae-210">이렇게 하면 [누락 데이터 정리] [ clean-missing-data] tooclean hello 데이터 값이 누락 된 행을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="7bcae-211">Hello 모듈을 두 번 클릭 하 고 "누락 된 값 행을 제거 합니다." hello 주석 입력</span><span class="sxs-lookup"><span data-stu-id="7bcae-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="7bcae-212">![Hello 청소 모드 설정 너무 "전체 행 제거" hello "누락 데이터 정리" 모듈에 대 한][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="7bcae-213">***Hello 청소 모드 설정 너무 "전체 행 제거" hello "누락 데이터 정리" 모듈에 대 한***</span><span class="sxs-lookup"><span data-stu-id="7bcae-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="7bcae-214">클릭 하 여 hello 실험을 실행 **실행** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="7bcae-215">Hello 실험 실행이 완료 되었을 때 모든 hello 모듈 성공적으로 완료 되는 녹색 확인 표시가 tooindicate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="7bcae-216">또한 hello 확인 **완료 된 실행** hello 오른쪽 위 모서리에서 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="7bcae-217">![를 실행 한 후 hello 실험은 다음과 같이 표시][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="7bcae-218">
***를 실행 한 후 hello 실험은 다음과 같이 표시***</span><span class="sxs-lookup"><span data-stu-id="7bcae-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="7bcae-219">Hello 실험을 지금 실행 되었습니까 이유 म?</span><span class="sxs-lookup"><span data-stu-id="7bcae-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="7bcae-220">실행 중인 hello 실험 하 여 데이터에 대 한 열 정의 hello hello 통해 hello 데이터 집합에서 전달 [데이터 집합의 열 선택] [ select-columns] 모듈 및 hello를 통해 [누락 데이터를 정리] [ clean-missing-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="7bcae-221">즉, 너무 연결할 모듈[누락 데이터 정리] [ clean-missing-data] 이 정보를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="7bcae-222">Toothis 포인트 hello 실험에 했던 모든 정리 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="7bcae-223">Tooview hello 정리할 데이터 집합 hello 남아 있는 hello의 출력 포트를 클릭 합니다 [누락 데이터 정리] [ clean-missing-data] 모듈과 선택 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="7bcae-224">해당 hello 확인 **정규화 손실** 열 더 이상 포함 되어 있으며, 누락 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="7bcae-225">We're 준비 toospecify 기능에서는 이제 hello 데이터를 정리 했으므로 toouse hello 예측 모델에 맞추려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="7bcae-226">3단계: 기능 정의</span><span class="sxs-lookup"><span data-stu-id="7bcae-226">Step 3: Define features</span></span>

<span data-ttu-id="7bcae-227">기계 학습에서 *기능*은 관심 있는 부분에 대한 측정 가능한 개별 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="7bcae-228">여기서는 데이터 집합의 각 행이 하나의 자동차를 나타내고 각 열은 해당 자동차의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="7bcae-229">Toosolve를 원하는 찾기 좋은 예측 모델을 만들기 위한 기능 집합 실험과 hello 문제에 대 한 지식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="7bcae-230">일부 기능은 예측 hello 대상 다른 항목 보다 더 효과적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="7bcae-231">또한 일부 기능은 다른 기능과 강력한 상관 관계가 있고 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="7bcae-232">예를 들어 도시 mpg 및 고속도로 mpg 밀접 한 관련이 하므로 하나를 유지 하 고 크게 hello 예측 영향을 주지 않고 다른 hello를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="7bcae-233">이 데이터 집합의 hello 기능의 하위 집합을 사용 하는 모델을 제작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="7bcae-234">나중에 다시 시도 하 고 다른 기능 선택, hello 실험을 다시 실행 고 확인할 수 있습니다 더 나은 결과 얻을 경우.</span><span class="sxs-lookup"><span data-stu-id="7bcae-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="7bcae-235">하지만 toostart, 같은 기능 hello 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="7bcae-236">다른 [데이터 집합의 열 선택] [ select-columns] 모듈 toohello 실험 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="7bcae-237">Hello의 출력 포트를 왼쪽 hello 연결 [누락 데이터 정리] [ clean-missing-data] hello의 모듈 toohello 입력 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="7bcae-238">![Hello "Dataset에서 열 선택" 모듈 toohello "누락 데이터 정리" 모듈에 연결][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="7bcae-239">***Hello "Dataset에서 열 선택" 모듈 toohello "누락 데이터 정리" 모듈에 연결***</span><span class="sxs-lookup"><span data-stu-id="7bcae-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="7bcae-240">Hello 모듈을 두 번 클릭 하 고 "선택 기능, 예측에 대 한 합니다."를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="7bcae-241">클릭 **열 선택기 시작** hello에 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="7bcae-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="7bcae-242">**규칙으로**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-242">Click **With rules**.</span></span>

4. <span data-ttu-id="7bcae-243">**다음으로 시작**에서 **열 없음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="7bcae-244">Hello 필터 행에서 선택 **Include** 및 **열 이름을** hello 텍스트 상자에서 열 이름의 목록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="7bcae-245">이 hello를 지정 하는 점을 제외 하 고 모든 열 (기능) 통과 모듈 toonot hello 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="7bcae-246">Hello 확인 표시 (정상) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="7bcae-247">![Hello 열 (기능) tooinclude hello 예측에서 선택][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="7bcae-248">***Hello 열 (기능) tooinclude hello 예측에서 선택***</span><span class="sxs-lookup"><span data-stu-id="7bcae-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="7bcae-249">이 학습 알고리즘에서는 hello 다음 단계에서 toopass toohello 원하는 hello 기능이 포함 된 필터링된 된 데이터 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="7bcae-250">나중에 돌아와서 다른 선택 기능을 사용하여 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="7bcae-251">4단계: 학습 알고리즘 선택 및 적용</span><span class="sxs-lookup"><span data-stu-id="7bcae-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="7bcae-252">이제 hello 데이터 준비 되 면 예측 모델 생성 구성 되어 있다고 학습 및 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="7bcae-253">예제의 데이터 tootrain hello 모델에서는 한 hello 모델 toosee 테스트해 보겠습니다 다음 수 toopredict 가격은 근접도입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="7bcae-254">*분류*와 *회귀*는 감독 기계 학습 알고리즘의 두 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="7bcae-255">분류는 색(빨강, 파랑 또는 녹색)과 같이 정의된 범주 집합에서 답변을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="7bcae-256">회귀는 사용 되는 toopredict 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="7bcae-257">에 사용 하기 위해 숫자인 경우 toopredict 가격 회귀 알고리즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="7bcae-258">이 예제에서는 간단한 *선형 회귀* 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="7bcae-259">다양 한 유형의 기계 학습 알고리즘에 대 한 자세한 toolearn 하 고 때 toouse 초보자를 위한 계열에 대 한 데이터 과학 hello에 hello 첫 번째 비디오를 볼 수 있습니다 이러한 [hello 5 데이터 과학 답변의 질문](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="7bcae-260">Hello 인포 그래픽도 확인할 수 있습니다 [알고리즘 예제를 사용한 기본 사항 학습 컴퓨터](machine-learning-basics-infographic-with-algorithm-examples.md), 체크 아웃 hello 또는 [컴퓨터 학습 알고리즘 치트 시트](machine-learning-algorithm-cheat-sheet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="7bcae-261">Hello 가격을 포함 하는 데이터 집합을 지정 하 여에 hello 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="7bcae-262">hello 모델 hello 데이터를 찾습니다는 자동차의 기능과 해당 가격 간의 상관 관계를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="7bcae-263">그런 다음 hello 모델 테스트해 보겠습니다-म 된 자동차에 대 한 기능 집합을 지정 하 고 hello 모델 toopredicting hello 알려진된 가격을 제공 하는 얼마나 비슷한지를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="7bcae-264">Hello 모델을 학습 하 고 hello 데이터를 별도 학습 및 테스트 데이터 집합으로 분할 하 여 테스트에 대 한 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="7bcae-265">선택 하 고 hello 끌어 [분할 데이터] [ split] 모듈 toohello 캔버스를 실험 하 고 연결 toohello 마지막 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="7bcae-266">Hello 클릭 [분할 데이터] [ split] 모듈 tooselect 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="7bcae-267">Hello **hello의 행 비율 먼저 출력 데이터 집합** (hello에 **속성** hello 캔버스의 오른쪽 창 toohello) too0.75 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="7bcae-268">이러한 방식으로 hello 데이터 tootrain hello 모델의 75%를 사용 하 여 알아보고 하겠습니다 보류 하 게 테스트를 위해 25% (이상 버전에서는 시험해 다른 백분율을 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="7bcae-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="7bcae-269">![Hello "데이터를 분할" 모듈 too0.75의 소수 부분을 분할 집합 hello][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="7bcae-270">***Hello "데이터를 분할" 모듈 too0.75의 소수 부분을 분할 집합 hello***</span><span class="sxs-lookup"><span data-stu-id="7bcae-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="7bcae-271">Hello를 변경 하 여 **임의 초기값** 매개 변수를 학습 및 테스트에 서로 다른 무작위 샘플을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="7bcae-272">이 매개 변수는 hello hello 의사 (pseudo) 난수 생성기의 시드를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="7bcae-273">Hello 실험을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-273">Run hello experiment.</span></span> <span data-ttu-id="7bcae-274">Hello 실험을 실행 하는 경우 hello [데이터 집합의 열 선택] [ select-columns] 및 [분할 데이터] [ split] 모듈 열 정의 toohello 전달 다음 추가 되므로 모듈.</span><span class="sxs-lookup"><span data-stu-id="7bcae-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="7bcae-275">학습 알고리즘, tooselect hello hello 확장 **기계 학습** hello 모듈 색상표 toohello 왼쪽의 범주 hello의 캔버스를 확장 한 다음 **모델 초기화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="7bcae-276">이 사용 되는 tooinitialize 기계 학습 알고리즘을 일 수 있는 모듈의 여러 범주가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="7bcae-277">이 실험에 hello 선택 [선형 회귀] [ linear-regression] hello 아래의 모듈 **회귀** 범주 toohello 실험 캔버스를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="7bcae-278">(또한 모듈 찾을 수 있습니다 hello hello 색상표 검색 상자에 "선형 회귀"를 입력 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7bcae-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="7bcae-279">찾기 및 hello 끌어 [모델 학습] [ train-model] 모듈 toohello 실험 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="7bcae-280">Hello hello 출력에 연결 [선형 회귀] [ linear-regression] 모듈 toohello 왼쪽 입력의 hello [모델 학습] [ train-model] 모듈 hello 연결 hello 데이터 출력 (왼쪽 포트) 학습 [분할 데이터] [ split] 모듈 toohello 오른쪽 입력의 hello [모델 학습] [ train-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="7bcae-281">![Hello "모델 학습" 모듈 tooboth hello "선형 회귀" 및 "데이터를 분할" 모듈에 연결][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="7bcae-282">***Hello "모델 학습" 모듈 tooboth hello "선형 회귀" 및 "데이터를 분할" 모듈에 연결***</span><span class="sxs-lookup"><span data-stu-id="7bcae-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="7bcae-283">Hello 클릭 [모델 학습] [ train-model] 모듈을 클릭 하 여 **열 선택기 시작** hello에 **속성** 창과 선택 hello **가격** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="7bcae-284">이 모델을 하락 toopredict hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="7bcae-285">Hello 선택 **가격** hello에서 이동 하 여 hello 열 선택기의 열 **사용 가능한 열** toohello 목록 **선택한 열** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="7bcae-286">![Hello "모델 학습" 모듈에 대 한 hello price 열을 선택 합니다.][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="7bcae-287">***Hello "모델 학습" 모듈에 대 한 hello price 열을 선택 합니다.***</span><span class="sxs-lookup"><span data-stu-id="7bcae-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="7bcae-288">Hello 실험을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-288">Run hello experiment.</span></span>

<span data-ttu-id="7bcae-289">사용 되는 tooscore 새로운 자동차 데이터 toomake 가격 예측 될 수 있는 학습 된 회귀 모델을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="7bcae-290">![를 실행 한 후 hello 실험은 이제 다음과 같은][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="7bcae-291">
***를 실행 한 후 hello 실험은 이제 다음과 같은***</span><span class="sxs-lookup"><span data-stu-id="7bcae-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="7bcae-292">5단계: 새 자동차 가격 예측</span><span class="sxs-lookup"><span data-stu-id="7bcae-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="7bcae-293">사용할 수 데이터의 75%를 사용 하 여 hello 모델을 학습 한 म 했으므로 tooscore hello hello 데이터 toosee 얼마나 잘의 25% 다른 우리의 모델 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="7bcae-294">찾기 및 hello 끌어 [모델 점수 매기기] [ score-model] 모듈 toohello 실험 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="7bcae-295">Hello hello 출력에 연결 [모델 학습] [ train-model] 왼쪽 입력된 포트의 모듈 toohello [모델 점수 매기기][score-model]합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="7bcae-296">Hello 테스트 데이터의 출력에 연결 (오른쪽 포트) hello [분할 데이터] [ split] 모듈 toohello 오른쪽 입력 포트의 [모델 점수 매기기][score-model]합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="7bcae-297">![Hello "모델 점수 매기기" 모듈 tooboth hello "모델 학습" 및 "데이터를 분할" 모듈에 연결][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="7bcae-298">***Hello "모델 점수 매기기" 모듈 tooboth hello "모델 학습" 및 "데이터를 분할" 모듈에 연결***</span><span class="sxs-lookup"><span data-stu-id="7bcae-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="7bcae-299">Hello 실험을 실행 하 고 hello hello 출력을 볼 [모델 점수 매기기] [ score-model] 모듈 (의 출력 포트 hello 클릭 [모델 점수 매기기] [ score-model] 선택 **시각화**).</span><span class="sxs-lookup"><span data-stu-id="7bcae-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="7bcae-300">hello 출력과 hello 가격에 대 한 예측된 값 및 hello hello 테스트 데이터의 알려진된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="7bcae-301">![Hello "모델 점수 매기기" 모듈의 출력][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="7bcae-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="7bcae-302">***Hello "모델 점수 매기기" 모듈의 출력***</span><span class="sxs-lookup"><span data-stu-id="7bcae-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="7bcae-303">마지막으로 hello 결과의 hello 품질을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="7bcae-304">선택 하 고 hello 끌어 [모델 평가] [ evaluate-model] 모듈 toohello 캔버스를 실험 하 고 hello hello 출력에 연결 [모델 점수 매기기] [ score-model] 왼쪽 입력의 모듈 toohello [모델 평가][evaluate-model]합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="7bcae-305">Hello에는 두 개의 입력된 포트가 [모델 평가] [ evaluate-model] 모듈 toocompare 사용 되는 두 가지 모델 나란히 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="7bcae-306">다른 알고리즘 toohello 실험을 추가 하 고 사용 하 여 수 나중 [모델 평가] [ evaluate-model] toosee 한 더 나은 결과 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="7bcae-307">Hello 실험을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-307">Run hello experiment.</span></span>

<span data-ttu-id="7bcae-308">hello tooview hello 출력 [모델 평가] [ evaluate-model] 모듈 hello 출력 포트를 클릭 한 다음 선택 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="7bcae-309">![Hello 실험에 대 한 평가 결과][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="7bcae-310">
***Hello 실험에 대 한 평가 결과***</span><span class="sxs-lookup"><span data-stu-id="7bcae-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="7bcae-311">이 모델에 대 한 통계를 다음 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="7bcae-312">**절대 평균 오차** (MAE): 평균 절대 오류 hello (한 *오류* hello 차이 hello 예측 값과 실제 값 hello).</span><span class="sxs-lookup"><span data-stu-id="7bcae-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="7bcae-313">**루트 제곱 평균 오차** (RMSE): hello 테스트 데이터 집합에서 예측의 제곱 오류 hello 평균의 제곱근 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="7bcae-314">**상대 절대 오차**: hello 절대 오류 상대 toohello 절대 실제 값과 hello 평균의 차이의 모든 실제 값의 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="7bcae-315">**상대 제곱 오차**: 상대 제곱된 오류 toohello의 hello 평균 hello 실제 값과 실제 값 집합 모든 hello 평균의 차이 제곱 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="7bcae-316">**결정 계수**: 라고도 hello **R 제곱 값**를 얼마나 잘 맞는 hello 데이터는 모델을 나타내는 통계 메트릭을입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="7bcae-317">각 hello 오류에 대 한 통계를 더 작은 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="7bcae-318">값이 작을수록 hello 예측 hello 실제 값과 보다 긴밀 하 게 일치 하는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="7bcae-319">에 대 한 **결정 계수**, hello 곧 제공 될 해당 값이 더 나은 hello 예측 hello tooone (1.0).</span><span class="sxs-lookup"><span data-stu-id="7bcae-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="7bcae-320">최종 실험</span><span class="sxs-lookup"><span data-stu-id="7bcae-320">Final experiment</span></span>

<span data-ttu-id="7bcae-321">hello 최종 실험 코드는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="7bcae-322">![hello 최종 실험][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="7bcae-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="7bcae-323">
***hello 최종 실험***</span><span class="sxs-lookup"><span data-stu-id="7bcae-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bcae-324">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7bcae-324">Next steps</span></span>

<span data-ttu-id="7bcae-325">Hello 첫 번째 컴퓨터 학습 자습서를 완료 하 고 설정 하 여 실험 한 tooimprove hello 모델을 계속 한 다음 예측 웹 서비스로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="7bcae-326">**Tootry tooimprove hello 모델 반복** -예를 들어 hello 기능 프로그램 예측에 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="7bcae-327">Hello의 hello 속성을 수정할 수 있습니다 또는 [선형 회귀] [ linear-regression] 알고리즘 하거나 완전히 다른 알고리즘을 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7bcae-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="7bcae-328">도 여러 기계 학습 알고리즘 tooyour 실험을 한번에 추가 하 고 hello를 사용 하 여 그 중 두 개를 비교할 수 [모델 평가] [ evaluate-model] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="7bcae-329">어떻게 toocompare 단일 실험에서 여러 모델 참조의 예 [회귀 변수 비교](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) hello에 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="7bcae-330">toocopy hello 사용 하 여 실험 반복 **SAVE AS** hello hello 페이지 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="7bcae-331">클릭 하 여 모든 hello 반복 하 여 실험을 볼 수 있습니다 **실행 기록 보기** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="7bcae-332">자세한 내용은 [Azure Machine Learning 스튜디오에서 실험 반복 관리][runhistory]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bcae-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="7bcae-333">**Hello 모델 예측 웹 서비스로 배포** -만족 했으면 모델을 사용 하는 경우 웹 서비스 toobe toopredict 차량 가격을 사용 되는 새 데이터를 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="7bcae-334">자세한 내용은 [Azure Machine Learning 웹 서비스 배포][publish]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bcae-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="7bcae-335">더 많은 toolearn 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="7bcae-335">Want toolearn more?</span></span> <span data-ttu-id="7bcae-336">Hello 프로세스의 생성, 학습, 상태 평가 및 배포 모델의 광범위 하 고 자세한 연습을 참조 하십시오. [Azure 기계 학습을 사용 하 여 예측 솔루션 개발][walkthrough]합니다.</span><span class="sxs-lookup"><span data-stu-id="7bcae-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
