---
title: "Azure Machine Learning을 사용한 데이터 분석 | Microsoft Docs"
description: "Azure 기계 학습을 사용하여 Azure SQL 데이터 웨어하우스에 저장된 데이터를 기반으로 예측 기계 학습 모델을 구축합니다."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="212d6-103">Azure 기계 학습을 사용하여 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="212d6-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="212d6-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="212d6-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="212d6-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="212d6-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="212d6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="212d6-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="212d6-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="212d6-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="212d6-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="212d6-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="212d6-109">이 자습서는 Azure 기계 학습을 사용하여 Azure SQL 데이터 웨어하우스에 저장된 데이터를 기반으로 예측 기계 학습 모델을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="212d6-110">특히 고객이 자전거를 구매할 가능성 여부를 예측하여 자전거 매장인 Adventure Works에 대한 대상 마케팅 캠페인을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="212d6-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="212d6-111">Prerequisites</span></span>
<span data-ttu-id="212d6-112">이 자습서를 단계별로 실행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="212d6-113">AdventureWorksDW 샘플 데이터로 미리 로드된 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="212d6-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="212d6-114">프로비전하려면 [SQL Data Warehouse 만들기][Create a SQL Data Warehouse]를 참조하고 샘플 데이터 로드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="212d6-115">데이터 웨어하우스는 있지만 샘플 데이터가 없는 경우 [샘플 데이터를 수동으로 로드][load sample data manually]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="212d6-116">1. 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="212d6-116">1. Get the data</span></span>
<span data-ttu-id="212d6-117">데이터는 AdventureWorksDW 데이터베이스의 dbo.vTargetMail 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="212d6-118">이 데이터를 읽으려면:</span><span class="sxs-lookup"><span data-stu-id="212d6-118">To read this data:</span></span>

1. <span data-ttu-id="212d6-119">[Azure Machine Learning 스튜디오][Azure Machine Learning studio]에 로그인하고 내 실험을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="212d6-120">**+새로 만들기**를 클릭하고 **빈 실험**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="212d6-121">실험: 대상 마케팅에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="212d6-122">모듈 창에서 **판독기** 모듈을 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="212d6-123">속성 창에서 SQL 데이터 웨어하우스 데이터베이스에 대한 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="212d6-124">관련 데이터를 읽을 데이터베이스 **쿼리** 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-124">Specify the database **query** to read the data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="212d6-125">실험 캔버스 아래에서 **실행** 을 클릭하여 실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="212d6-126">![실험 실행][1]</span><span class="sxs-lookup"><span data-stu-id="212d6-126">![Run the experiment][1]</span></span>

<span data-ttu-id="212d6-127">실험이 성공적으로 실행되고 나면 판독기 모듈 아래쪽에서 출력 포트를 클릭하고 **시각화** 를 선택하여 가져온 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="212d6-128">![가져온 데이터 확인][3]</span><span class="sxs-lookup"><span data-stu-id="212d6-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="212d6-129">2. 데이터 정리</span><span class="sxs-lookup"><span data-stu-id="212d6-129">2. Clean the data</span></span>
<span data-ttu-id="212d6-130">데이터를 정리하려면 모델에 관련되지 않은 일부 열을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="212d6-131">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-131">To do this:</span></span>

1. <span data-ttu-id="212d6-132">**프로젝트 열** 모듈을 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="212d6-133">속성 창에서 **열 선택기 시작** 을 클릭하여 삭제하려는 열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="212d6-134">![프로젝트 열][4]</span><span class="sxs-lookup"><span data-stu-id="212d6-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="212d6-135">다음 두 열을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="212d6-136">![불필요한 열 제거][5]</span><span class="sxs-lookup"><span data-stu-id="212d6-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="212d6-137">3. 모델 작성</span><span class="sxs-lookup"><span data-stu-id="212d6-137">3. Build the model</span></span>
<span data-ttu-id="212d6-138">데이터를 80-20으로 분할합니다. 80%는 기계 학습 모델을 학습하고 20%는 모델을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="212d6-139">이진 분류 문제에 대해 "2클래스" 알고리즘을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="212d6-140">**분할** 모듈을 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="212d6-141">속성 창에서 첫 번째 출력 데이터 집합의 행 분수에 대해 0.8을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="212d6-142">![훈련 및 테스트 집합으로 데이터 분할][6]</span><span class="sxs-lookup"><span data-stu-id="212d6-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="212d6-143">**2클래스 향상된 의사 결정 트리** 모듈을 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="212d6-144">**모델 학습** 모듈을 캔버스로 끌어서 놓고 입력을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="212d6-145">그런 다음 속성 창에서 **열 선택기 시작** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="212d6-146">첫 번째 입력: ML 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="212d6-147">두 번째 입력: 알고리즘을 학습할 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="212d6-148">![모델 학습 모듈 연결][7]</span><span class="sxs-lookup"><span data-stu-id="212d6-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="212d6-149">**BikeBuyer** 열을 예측할 열로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="212d6-150">![예측할 열 선택][8]</span><span class="sxs-lookup"><span data-stu-id="212d6-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="212d6-151">4. 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="212d6-151">4. Score the model</span></span>
<span data-ttu-id="212d6-152">이제 모델이 테스트 데이터를 수행하는 방법을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="212d6-153">더 잘 수행하는 알고리즘을 확인하도록 다른 알고리즘을 선택하여 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="212d6-154">**모델 점수 매기기** 모듈을 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="212d6-155">첫 번째 입력: 학습된 모델 두 번째 입력: 테스트 데이터 ![모델 점수 매기기][9]</span><span class="sxs-lookup"><span data-stu-id="212d6-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="212d6-156">**2클래스 Bayes 지점 컴퓨터** 를 실험 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="212d6-157">2클래스 향상된 의사 결정 트리와 비교하여 이 알고리즘이 수행하는 방법을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="212d6-158">캔버스에서 모델 학습 및 모델 점수 매기기 모듈을 복사하고 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="212d6-159">**모델 평가** 모듈을 캔버스로 끌어서 놓아 두 알고리즘을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="212d6-160">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-160">**Run** the experiment.</span></span>
   <span data-ttu-id="212d6-161">![실험 실행][10]</span><span class="sxs-lookup"><span data-stu-id="212d6-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="212d6-162">모델 평가 모듈의 아래쪽에서 출력 포트를 클릭하고 시각화를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="212d6-163">![평가 결과 시각화][11]</span><span class="sxs-lookup"><span data-stu-id="212d6-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="212d6-164">제공된 메트릭은 ROC 곡선, 정밀도-리콜 다이어그램 및 리프트 곡선입니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="212d6-165">이러한 메트릭을 살펴보면 첫 번째 모델이 두 번째보다 더 잘 실행하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="212d6-166">첫 번째 모델이 예측하는 것을 보려면 모델 점수 매기기의 출력 포트를 클릭하고 시각화를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="212d6-167">![점수 결과 시각화][12]</span><span class="sxs-lookup"><span data-stu-id="212d6-167">![Visualize score results][12]</span></span>

<span data-ttu-id="212d6-168">테스트 데이터 집합에 두 개의 열이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="212d6-169">점수가 매겨진 확률: 고객이 자전거 구매자일 가능성입니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="212d6-170">점수가 매겨진 레이블: 모델에 의해 분류가 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="212d6-171">– 자전거 구매자(1) 혹은 아님(0) 레이블 지정에 대한 확률 임계값은 50%로 설정되고 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="212d6-172">점수가 매겨진 레이블(예측)로 열 BikeBuyer(실제) 비교를 통해 모델이 얼마나 잘 실행했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="212d6-173">다음 단계로 이 모델을 사용하여 새 고객에 대한 예측을 수행하고 이 모델을 웹 서비스로 게시하거나 SQL 데이터 웨어하우스에 결과를 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212d6-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="212d6-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="212d6-174">Next steps</span></span>
<span data-ttu-id="212d6-175">예측 Machine Learning 모델을 구축하는 방법에 대한 자세한 내용은 [Azure의 Machine Learning 소개][Introduction to Machine Learning on Azure]를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="212d6-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
