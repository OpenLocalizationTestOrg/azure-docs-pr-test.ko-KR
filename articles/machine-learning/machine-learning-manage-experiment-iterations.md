---
title: "Machine Learning 스튜디오에서 반복 실험 관리 | Microsoft Docs"
description: "Azure 기계 학습 스튜디오에서 반복 실험을 관리하는 방법"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0e32a02358d1901bb80f356b0289b02b8e98afdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="59db7-103">Azure 기계 학습 스튜디오에서 반복 실험 관리</span><span class="sxs-lookup"><span data-stu-id="59db7-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="59db7-104">예측 분석 모델을 개발하는 과정은 반복 프로세스이며, 실험의 다양한 함수와 해당 매개 변수를 수정할 때 학습된 효과적인 모델을 마련했다고 만족할 때까지 결과가 수렴됩니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="59db7-105">이 프로세스의 핵심은 다양하게 반복되는 실험 매개 변수와 구성을 추적하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="59db7-106">이전 가정에 도전하고 다시 수행하여 궁극적으로 이전 가정을 확인하거나 세분화하기 위해 언제든 이전에 실행된 실험을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="59db7-107">실험을 실행하면 기계 학습 스튜디오에서 데이터 집합, 모듈, 포트 연결 및 매개 변수를 포함하여 실행의 기록을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="59db7-108">이 기록은 시작 및 종료 시간, 로그 메시지 및 실행 상태와 같은 결과, 런타임 정보도 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="59db7-109">언제든 이러한 실행을 다시 확인하여 실험과 중간 결과를 연대순으로 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="59db7-110">이전에 실행한 실험을 사용하여 간단하거나 복잡한 모델링 솔루션 또는 앙상블 모델링 솔루션을 만드는 과정에서 조회하고 검색하는 새로운 단계를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="59db7-111">이전에 실행한 실험을 볼 때, 해당 버전의 실험은 잠겨 있으며 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="59db7-112">그러나 **다른 이름으로 저장** 을 클릭하고 사본의 새 이름을 제공하여 사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="59db7-113">기계 학습 스튜디오에서 사용자가 편집하여 실행할 수 있는 새로운 사본을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="59db7-114">이 실험의 사본은 다른 모든 실험과 함께 **실험** 목록에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="59db7-115">이전 실행 보기</span><span class="sxs-lookup"><span data-stu-id="59db7-115">Viewing the Prior Run</span></span>
<span data-ttu-id="59db7-116">한 번 이상 실행한 실험이 열려 있는 경우, 속성 창에서 **이전 실행** 을 클릭하여 실험의 이전 실행을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="59db7-117">예를 들어, 실험을 만들고 11:23, 11:42 및 11:55에 실험의 버전을 실행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="59db7-118">마지막으로 실행된 실험(11:55)을 열고 **이전 실행**을 클릭하면 11:42에 실행한 버전이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="59db7-119">실행 기록 보기</span><span class="sxs-lookup"><span data-stu-id="59db7-119">Viewing the Run History</span></span>
<span data-ttu-id="59db7-120">열린 실험에서 **실행 기록 보기** 를 클릭하여 이전에 실행된 모든 실험을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="59db7-121">예를 들어, [선형 회귀][linear-regression] 모듈로 실험을 만들고 실험 결과에서 **학습 속도** 값을 변경하는 효과를 관찰하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="59db7-122">다음과 같이 이 매개 변수에 서로 다른 값을 사용하여 실험을 여러 번 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="59db7-123">학습 속도 값</span><span class="sxs-lookup"><span data-stu-id="59db7-123">Learning Rate value</span></span> | <span data-ttu-id="59db7-124">실행 시작 시간</span><span class="sxs-lookup"><span data-stu-id="59db7-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="59db7-125">0.1</span><span class="sxs-lookup"><span data-stu-id="59db7-125">0.1</span></span> |<span data-ttu-id="59db7-126">2014년 9월 11일 오후 4:18:58</span><span class="sxs-lookup"><span data-stu-id="59db7-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="59db7-127">0.2</span><span class="sxs-lookup"><span data-stu-id="59db7-127">0.2</span></span> |<span data-ttu-id="59db7-128">2014년 9월 11일 오후 4:24:33</span><span class="sxs-lookup"><span data-stu-id="59db7-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="59db7-129">0.4</span><span class="sxs-lookup"><span data-stu-id="59db7-129">0.4</span></span> |<span data-ttu-id="59db7-130">2014년 9월 11일 오후 4:28:36</span><span class="sxs-lookup"><span data-stu-id="59db7-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="59db7-131">0.5</span><span class="sxs-lookup"><span data-stu-id="59db7-131">0.5</span></span> |<span data-ttu-id="59db7-132">2014년 9월 11일 오후 4:33:31</span><span class="sxs-lookup"><span data-stu-id="59db7-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="59db7-133">**실행 기록 보기**를 클릭하면 다음과 같은 실행 목록이 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![예제 실행 기록][runhistory]

<span data-ttu-id="59db7-135">임의의 실행을 클릭하여 실험을 실행한 시간의 스냅샷을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="59db7-136">실험 실행에 관한 전체 레코드를 제공하기 위해 구성, 매개 변수 값, 주석 및 결과가 모두 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="59db7-137">반복 실험을 문서화하려면 실행할 때마다 제목을 수정하고, 속성 창에서 실험의 **요약** 을 업데이트하며, 변경 사항을 기록하기 위해 개별 모듈에 대한 주석을 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="59db7-138">제목, 요약 및 모듈 주석은 실험이 실행될 때마다 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="59db7-139">기계 학습 스튜디오의 **실험** 탭에 있는 실험 목록은 항상 실험의 최신 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="59db7-140">**이전 실행** 또는 **실행 기록 보기**를 사용하여 이전에 실행된 실험을 열면, **실행 기록 보기**를 클릭하고 **상태**가 **편집 가능**인 반복을 선택하여 초안 버전으로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="59db7-141">이전 실행 반복</span><span class="sxs-lookup"><span data-stu-id="59db7-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="59db7-142">**이전 실행** 또는 **실행 기록 보기**를 클릭하고 이전 실행을 열면 읽기 전용 모드로 완료된 실험을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="59db7-143">이전 실행을 위해 실험을 구성한 방식으로 실험 반복을 시작하려면 실행을 열고 **다른 이름으로 저장**을 클릭하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="59db7-144">그러면 실행 기록이 비어 있으며 이전 실행의 모든 구성 요소와 매개 변수 값을 사용하는 새로운 제목의 새 실험이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="59db7-145">이 새 실험은 기계 학습 스튜디오 홈 페이지의 **실험** 탭에 나열되므로, 사용자가 수정하고 실행하여 이 반복 실험의 새로운 실행 기록을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="59db7-146">예를 들어, 이전 섹션에 표시된 실험 실행 기록이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="59db7-147">**학습 속도** 매개 변수를 0.4로 설정하면 어떻게 되는지 관찰하고 **학습 epoch 수** 매개 변수에 다른 값을 사용해 보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="59db7-148">**실행 기록 보기** 를 클릭하고 오후 4:28:36에 실행한 반복 실험을 엽니다(매개 변수 값을 0.4로 설정함).</span><span class="sxs-lookup"><span data-stu-id="59db7-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="59db7-149">**다른 이름으로 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="59db7-150">새 제목을 입력하고 **확인** 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="59db7-151">실험의 새 복사본이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="59db7-152">**학습 epoch 수** 매개 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="59db7-153">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-153">Click **RUN**.</span></span>

<span data-ttu-id="59db7-154">이제 계속하여 이 버전의 실험을 수정하고 실행하여 작업을 기록할 새 실행 기록을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59db7-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
