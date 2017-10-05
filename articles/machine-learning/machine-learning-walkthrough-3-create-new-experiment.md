---
title: "3단계: 새 Machine Learning 실험 만들기 | Microsoft Docs"
description: "예측 솔루션 개발 연습 3단계: Azure 기계 학습 스튜디오에서 새 학습 실험을 만듭니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="ec17e-103">연습 3단계: 새 Azure 기계 학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="ec17e-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="ec17e-104">[Azure 기계 학습에서 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="ec17e-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="ec17e-105">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="ec17e-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="ec17e-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="ec17e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="ec17e-107">**새 실험 만들기**</span><span class="sxs-lookup"><span data-stu-id="ec17e-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="ec17e-108">모델 학습 및 평가</span><span class="sxs-lookup"><span data-stu-id="ec17e-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="ec17e-109">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="ec17e-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="ec17e-110">웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="ec17e-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="ec17e-111">이 연습의 다음 단계는 업로드한 데이터 집합을 사용하는 Machine Learning Studio에서 실험을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="ec17e-112">스튜디오의 창 하단에 있는 **+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="ec17e-113">**실험**을 선택하고 "빈 실험"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![새로운 실험 만들기][0]

2. <span data-ttu-id="ec17e-115">캔버스 위쪽에서 기본 실험 이름을 선택하고 이를 의미 있는 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![실험 이름 바꾸기][5]
   
   > [!TIP]
   > <span data-ttu-id="ec17e-117">**속성** 창에 실험에 대한 **요약** 및 **설명**을 입력하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="ec17e-118">이러한 속성을 사용하면 실험을 문서화할 수 있어 나중에 실험을 참조하는 모든 사용자가 실험의 목표와 방법론을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![실험 속성][6]
   > 
3. <span data-ttu-id="ec17e-120">실험 캔버스의 왼쪽에 있는 모듈 팔레트에서 **저장된 데이터 집합**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="ec17e-121">**내 데이터 집합** 아래에서 만든 데이터 집합을 찾고 캔버스로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="ec17e-122">팔레트 위의 **검색** 상자에 이름을 입력하여 데이터 집합을 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![실험에 데이터 집합 추가][7]

## <a name="prepare-the-data"></a><span data-ttu-id="ec17e-124">데이터 준비</span><span class="sxs-lookup"><span data-stu-id="ec17e-124">Prepare the data</span></span>
<span data-ttu-id="ec17e-125">데이터 집합(아래 작은 원)의 출력 포트를 클릭하고 **시각화**를 선택하여 데이터의 처음 100개 행 및 전체 데이터 집합에 대한 일부 통계 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="ec17e-126">데이터 파일에는 열 제목이 없으므로 스튜디오에서 일반적인 제목(Col1, Col2, *등*)을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="ec17e-127">적합한 제목은 모델 작성 시 필수 사항은 아니지만 제목이 있으면 실험에서 데이터를 더 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="ec17e-128">또한 최종적으로 웹 서비스에서 이 모델을 게시할 때 제목을 사용하여 서비스 사용자에 대한 열을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="ec17e-129">[메타데이터 편집][edit-metadata] 모듈을 사용하여 열 제목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="ec17e-130">[메타데이터 편집][edit-metadata] 모듈을 사용하여 데이터 집합과 연결된 메타데이터를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="ec17e-131">이 경우에는 좀 더 친숙한 열 머리글 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="ec17e-132">[메타데이터 편집][edit-metadata]을 사용하려면 먼저 수정할 열(이 경우 모두)을 지정합니다. 다음으로 해당 열에서 수행할 작업(이 경우 열 머리글 변경)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="ec17e-133">모듈 팔레트에서 **검색** 상자에 "metadata"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="ec17e-134">[메타데이터 편집][edit-metadata]이 모듈 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="ec17e-135">[메타데이터 편집][edit-metadata] 모듈을 클릭하고 캔버스로 끌어서 이전에 추가한 데이터 집합 아래에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="ec17e-136">데이터 집합을 [메타데이터 편집][edit-metadata]에 연결합니다. 데이터 집합의 출력 포트(데이터 집합 맨 아래의 작은 원)를 클릭하여 [메타데이터 편집][edit-metadata]의 입력 포트(모듈 맨 위의 작은 원)로 끌어 놓은 다음 마우스 단추를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="ec17e-137">데이터 집합과 모듈은 캔버스에서 이동해도 연결 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="ec17e-138">이제 실험이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-138">The experiment should now look something like this:</span></span>  
   
   ![메타데이터 편집 추가][1]
   
   <span data-ttu-id="ec17e-140">빨간색 느낌표는 이 모듈에 대한 속성이 아직 설정되지 않았다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="ec17e-141">다음에 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ec17e-142">모듈을 두 번 클릭하고 텍스트를 입력하여 모듈에 주석을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="ec17e-143">그러면 모듈이 실험에서 수행하는 내용을 한눈에 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="ec17e-144">이 경우 [메타데이터 편집][edit-metadata] 모듈을 두 번 클릭하고 주석 "열 제목 추가"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="ec17e-145">캔버스의 다른 곳을 클릭하여 텍스트 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="ec17e-146">주석을 표시하려면 모듈에서 아래쪽 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![주석이 추가된 메타데이터 모듈 편집][8]
   > 
4. <span data-ttu-id="ec17e-148">[메타데이터 편집][edit-metadata]을 선택한 다음 캔버스 오른쪽의 **속성** 창에서 **열 선택기 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="ec17e-149">**열 선택** 대화 상자의 **사용 가능한 열**에서 모든 행을 선택하고 >를 클릭하여 **선택한 열**로 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="ec17e-150">대화 상자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-150">The dialog should look like this:</span></span>

   ![모든 열이 선택된 열 선택기][2]

6. <span data-ttu-id="ec17e-152">**확인** 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="ec17e-153">**속성** 창으로 돌아가서 **새 열 이름** 매개 변수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="ec17e-154">이 필드에 데이터 집합의 21개 열에 대한 이름 목록을 쉼표로 구분하여 열 순서로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="ec17e-155">UCI 웹 사이트의 데이터 집합 설명서에서 열 이름을 얻거나 편의를 위해 다음 목록을 복사하여 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="ec17e-156">속성 창의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-156">The Properties pane looks like this:</span></span>
   
   ![메타데이터 편집에 대한 속성][3]

> [!TIP]
> <span data-ttu-id="ec17e-158">열 제목을 확인하려면 실험을 실행(실험 캔버스 아래의 **실행** 클릭)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="ec17e-159">실행이 완료되면([메타데이터 편집][edit-metadata]에 녹색 확인 표시가 나타남) [메타데이터 편집][edit-metadata] 모듈의 출력 포트를 클릭하고 **시각화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="ec17e-160">같은 방법으로 모듈의 출력을 표시하여 실험을 통해 데이터 진행률을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="ec17e-161">학습 및 테스트 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="ec17e-161">Create training and test datasets</span></span>
<span data-ttu-id="ec17e-162">모델을 학습할 데이터 및 테스트할 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="ec17e-163">따라서 다음 실험 단계에서는 데이터 집합을 하나는 모델 학습을 위한 것으로 하나는 테스트를 위한 것으로 두 개의 별도 데이터 집합으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="ec17e-164">이 작업을 하기 위해 [데이터 분할][split] 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="ec17e-165">[데이터 분할][split] 모듈을 찾고 캔버스로 끌어서 [메타데이터 편집][edit-metadata] 모듈에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="ec17e-166">기본적으로 분할 비율은 0.5이고 **무작위 분할** 매개 변수가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="ec17e-167">이는 데이터의 임의 절반이 [데이터 분할][split] 모듈의 한 포트를 통해 출력되고 나머지 절반은 다른 포트를 통해 출력됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="ec17e-168">이러한 매개 변수와 **임의 초기값** 매개 변수를 조정하여 학습 및 테스트 데이터 간의 분할을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="ec17e-169">이 예제에서는 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ec17e-170">**첫 번째 출력 데이터 집합의 행의 비율** 속성은 *왼쪽* 출력 포트를 통해 출력되는 데이터의 양을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="ec17e-171">예를 들어 비율을 0.7로 설정하면 데이터의 70%가 왼쪽 포트를 통해 출력되고 30%는 오른쪽 포트를 통해 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="ec17e-172">[데이터 분할][split] 모듈을 두 번 클릭하고 주석 "데이터 분할 50% 학습/테스트"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="ec17e-173">[데이터 분할][split] 모듈의 출력을 사용할 수 있지만 왼쪽 출력을 학습 데이터로 사용하고 오른쪽 출력을 테스트 데이터로 사용하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="ec17e-174">[이전 단계](machine-learning-walkthrough-2-upload-data.md)에서 언급한 대로 높은 신용 위험을 낮은 것으로 잘못 분류한 비용은 낮은 신용 위험을 높은 것으로 잘못 분류한 비용보다 5배 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="ec17e-175">이를 고려하기 위해 이 비용 함수를 반영하는 새 데이터 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="ec17e-176">새 데이터 집합에서 위험이 높은 각 예제는 5번 복제되지만 위험이 낮은 각 예제는 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="ec17e-177">R 코드를 사용하여 이 복제를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="ec17e-178">[R 스크립트 실행][execute-r-script] 모듈을 찾아 실험 캔버스로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="ec17e-179">[데이터 분할][split] 모듈의 왼쪽 출력 포트를 [R 스크립트 실행][execute-r-script] 모듈의 첫 번째 입력 포트("Dataset1")에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="ec17e-180">[R 스크립트 실행][execute-r-script] 모듈을 두 번 클릭하고 주석 "비용 조정 설정"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="ec17e-181">**속성** 창에서 **R 스크립트** 매개 변수의 기본 텍스트를 삭제하고 다음 스크립트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R 스크립트 실행 모듈의 R 스크립트][9]

<span data-ttu-id="ec17e-183">학습 및 테스트 데이터에 같은 비용 조정이 포함되도록 [데이터 분할][split] 모듈의 각 출력에 대해 이와 같은 복제 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="ec17e-184">이 작업을 수행하는 가장 쉬운 방법은 방금 만든 [R 스크립트 실행][execute-r-script] 모듈을 복제하고 [데이터 분할][split] 모듈의 다른 출력 포트에 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="ec17e-185">[R 스크립트 실행][execute-r-script] 모듈을 마우스 오른쪽 단추로 클릭하고 **복사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="ec17e-186">실험 캔버스를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="ec17e-187">새 모듈을 해당 위치로 끌어 놓은 다음 [데이터 분할][split] 모듈의 오른쪽 출력 포트를 이 새로운 [R 스크립트 실행][execute-r-script] 모듈의 첫 번째 입력 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="ec17e-188">캔버스 맨 아래에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="ec17e-189">R 스크립트 실행 모듈의 복사본에는 원래 모듈과 같은 스크립트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="ec17e-190">캔버스에서 모듈을 복사하고 붙여넣으면 복사본에서 원본의 모든 속성이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="ec17e-191">이제 실험은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec17e-191">Our experiment now looks something like this:</span></span>

![분할 모듈 및 R 스크립트 추가][4]

<span data-ttu-id="ec17e-193">실험에서의 R 스크립트 사용에 대한 자세한 내용은 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec17e-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="ec17e-194">**다음: [모델 학습 및 평가](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="ec17e-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
