---
title: "2단계: Machine Learning 실험에 데이터 업로드 | Microsoft Docs"
description: "예측 솔루션 연습 개발의 2단계: Azure 기계 학습 스튜디오로 저장된 공용 데이터를 업로드합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="a0a55-103">연습 2단계: Azure 기계 학습 실험에 기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="a0a55-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="a0a55-104">[Azure 기계 학습에서 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a0a55-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a0a55-105">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="a0a55-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="a0a55-106">**기존 데이터 업로드**</span><span class="sxs-lookup"><span data-stu-id="a0a55-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="a0a55-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="a0a55-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a0a55-108">모델 학습 및 평가</span><span class="sxs-lookup"><span data-stu-id="a0a55-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a0a55-109">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="a0a55-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a0a55-110">웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="a0a55-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a0a55-111">신용 위험에 대한 예측 모델을 개발하려면 모델을 학습 후 테스트할 수 있는 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="a0a55-112">이 연습에서는 UC Irvine Machine Learning 리포지토리의 "UCI Statlog(독일 신용 데이터) 데이터 집합"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="a0a55-113">이 데이터 집합은 </span><span class="sxs-lookup"><span data-stu-id="a0a55-113">You can find it here:</span></span>  
<span data-ttu-id="a0a55-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="a0a55-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="a0a55-115">여기서는 **german.data**라는 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="a0a55-116">로컬 하드 드라이브로 이 파일을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="a0a55-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="a0a55-117">**german.data** 데이터 집합에는 지난 1000명의 신용대출 신청자에 대한 20개 변수 행이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="a0a55-118">이러한 20개 변수는 각 대출 신청자에 대한 특성을 파악하는 기능의 데이터 집합(*기능 벡터*)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="a0a55-119">각 행의 추가 열은 신청자의 계산된 신용 위험을 나타내며, 700명의 신청자는 신용 위험이 낮은 것으로, 300명의 신청자는 위험이 높은 것으로 파악되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="a0a55-120">UCI 웹 사이트에서는 이 데이터에 대한 기능 벡터의 특성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="a0a55-121">여기에는 재무 정보, 신용 기록, 고용 상태 및 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="a0a55-122">각 지원자에 대해 신용 위험이 낮은지 아니면 높은지 여부를 나타내는 이진 등급이 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="a0a55-123">이 데이터를 사용하여 예측 분석 모델의 학습을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="a0a55-124">학습을 완료하면 모델에서 새로운 개인에 대한 기능 벡터를 허용하여 신용 위험이 낮거나 높은지 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="a0a55-125">흥미로운 변형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-125">Here's an interesting twist.</span></span> <span data-ttu-id="a0a55-126">UCI 웹 사이트에 있는 데이터 집합의 설명은 개인의 신용 위험을 잘못 분류하는 경우 발생하는 비용을 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="a0a55-127">모델이 실제로 신용 위험이 낮은 개인에 대해 신용 위험을 높게 예측하는 경우 모델은 오분류를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="a0a55-128">하지만 역방향 오분류(모델이 실제로 신용 위험이 높은 개인에 대해 신용 위험을 낮게 예측하는 경우)는 금융 기관에 대해 5배의 비용이 더 듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="a0a55-129">따라서 이 후자 오분류 유형의 비용이 다른 방향으로 오분류하는 것보다 5배 높도록 모델을 학습하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="a0a55-130">이 실험에서 모델을 학습할 때 이를 수행할 수 있는 간단한 방법은 신용 위험이 높은 사람을 나타내는 항목을 5배 복제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="a0a55-131">그런 다음 모델이 실제로 위험이 높을 때 신용 위험을 낮게 잘못 분류하는 경우 모델은 각 복제마다 한 번씩 동일한 오분류를 5번 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="a0a55-132">그러면 학습 결과에서 이 오류의 비용이 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="a0a55-133">데이터 집합 형식 변환</span><span class="sxs-lookup"><span data-stu-id="a0a55-133">Convert the dataset format</span></span>
<span data-ttu-id="a0a55-134">원래 데이터 집합은 공백으로 구분된 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="a0a55-135">기계 학습 스튜디오는 CSV(쉼표로 구분된 값) 파일에서 더 원활하게 작동하므로 공백을 쉼표로 바꿔서 데이터 집합을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="a0a55-136">여러 가지 방법으로 이 데이터를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-136">There are many ways to convert this data.</span></span> <span data-ttu-id="a0a55-137">한 가지 방법은 다음 Windows PowerShell 명령을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="a0a55-138">또 다른 방법은 Unix sed 명령을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="a0a55-139">이 두 방법에서는 모두 실험에서 사용할 수 있는 쉼표로 구분된 데이터 버전인 **german.csv** 파일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="a0a55-140">기계 학습 스튜디오에 데이터 집합 업로드</span><span class="sxs-lookup"><span data-stu-id="a0a55-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="a0a55-141">데이터를 CSV 형식으로 변환한 후 기계 학습 스튜디오에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="a0a55-142">Machine Learning Studio 홈 페이지를 엽니다([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="a0a55-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="a0a55-143">창의 왼쪽 상단 모서리에 있는 ![메뉴][1]를 클릭하고 **Azure Machine Learning**을 클릭하고 **Studio**를 선택한 다음 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="a0a55-144">창 아래쪽에서 **+새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="a0a55-145">**데이터 집합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="a0a55-146">**로컬 파일에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-146">Select **FROM LOCAL FILE**.</span></span>

    ![로컬 파일에서 데이터 집합 추가][2]

6. <span data-ttu-id="a0a55-148">**새 데이터 집합 업로드** 대화 상자에서 **찾아보기**를 클릭하여 앞서 만든 **german.csv** 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="a0a55-149">데이터 집합의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-149">Enter a name for the dataset.</span></span> <span data-ttu-id="a0a55-150">이 연습에서는 데이터 집합을 "UCI 독일 신용 카드 데이터"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="a0a55-151">데이터 형식으로 **머리글 없는 일반 CSV 파일(.nh.csv)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="a0a55-152">원하는 경우 설명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="a0a55-153">**확인** 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-153">Click the **OK** check mark.</span></span>  

    ![데이터 집합 업로드][3]

<span data-ttu-id="a0a55-155">그러면 데이터가 실험에 사용할 수 있는 데이터 집합 모듈에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="a0a55-156">스튜디오 창 왼쪽의 **데이터 집합** 탭을 클릭하여 스튜디오에 업로드된 데이터 집합을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0a55-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![데이터 집합 관리][4]

<span data-ttu-id="a0a55-158">다른 데이터 형식을 실험으로 가져오는 방법에 대한 자세한 내용은 [Azure Machine Learning Studio로 학습 데이터 가져오기](machine-learning-data-science-import-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0a55-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="a0a55-159">**다음 단계: [새 실험 만들기](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="a0a55-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
