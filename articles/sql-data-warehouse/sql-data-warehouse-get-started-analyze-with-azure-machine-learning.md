---
title: "Azure 기계 학습을 사용 하 여 aaaAnalyze 데이터 | Microsoft Docs"
description: "Azure 기계 학습 toobuild 예측 기계 학습 Azure SQL 데이터 웨어하우스에 저장 된 데이터를 기반으로 모델을 사용 합니다."
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
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="683a5-103">Azure 기계 학습을 사용하여 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="683a5-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="683a5-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="683a5-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="683a5-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="683a5-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="683a5-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="683a5-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="683a5-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="683a5-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="683a5-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="683a5-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="683a5-109">이 자습서에서는 Azure 기계 학습 toobuild 예측 기계 학습 모델 Azure SQL 데이터 웨어하우스에 저장 된 데이터를 기반으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="683a5-110">특히,이 빌드 대상된 마케팅 캠페인 Adventure Works에서는 hello 자전거 매장에 대 한,으로 예측 하는 경우 고객은 가능성이 toobuy 자전거 여부.</span><span class="sxs-lookup"><span data-stu-id="683a5-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="683a5-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="683a5-111">Prerequisites</span></span>
<span data-ttu-id="683a5-112">이 자습서를 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="683a5-113">AdventureWorksDW 샘플 데이터로 미리 로드된 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="683a5-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="683a5-114">tooprovision이,이 참조 [SQL 데이터 웨어하우스를 만들] [ Create a SQL Data Warehouse] tooload hello 샘플 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="683a5-115">데이터 웨어하우스는 있지만 샘플 데이터가 없는 경우 [샘플 데이터를 수동으로 로드][load sample data manually]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="683a5-116">1. Hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="683a5-116">1. Get hello data</span></span>
<span data-ttu-id="683a5-117">hello 데이터는 hello AdventureWorksDW 데이터베이스에서 hello dbo.vTargetMail 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="683a5-118">tooread이이 데이터:</span><span class="sxs-lookup"><span data-stu-id="683a5-118">tooread this data:</span></span>

1. <span data-ttu-id="683a5-119">[Azure Machine Learning 스튜디오][Azure Machine Learning studio]에 로그인하고 내 실험을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="683a5-120">**+새로 만들기**를 클릭하고 **빈 실험**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="683a5-121">실험: 대상 마케팅에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="683a5-122">끌어서 hello **판독기** hello canvas에 hello 모듈 창에서 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="683a5-123">Hello 속성 창에서 SQL 데이터 웨어하우스 데이터베이스의 hello 세부 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="683a5-124">Hello 데이터베이스 지정 **쿼리** 대상 tooread hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-124">Specify hello database **query** tooread hello data of interest.</span></span>

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

<span data-ttu-id="683a5-125">클릭 하 여 hello 실험을 실행 **실행** hello 실험 캔버스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="683a5-126">![Hello 실험을 실행 합니다.][1]</span><span class="sxs-lookup"><span data-stu-id="683a5-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="683a5-127">Hello 실험 성공적으로 완료 되 면 hello 판독기 모듈 hello 맨 아래에 hello 출력 포트를 클릭 하 고 선택 **시각화** toosee hello 가져온 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="683a5-128">![가져온 데이터 확인][3]</span><span class="sxs-lookup"><span data-stu-id="683a5-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="683a5-129">2. 클린 hello 데이터</span><span class="sxs-lookup"><span data-stu-id="683a5-129">2. Clean hello data</span></span>
<span data-ttu-id="683a5-130">tooclean hello 데이터 hello 모델에 대 한 관계 없는 일부 열을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="683a5-131">toodo이:</span><span class="sxs-lookup"><span data-stu-id="683a5-131">toodo this:</span></span>

1. <span data-ttu-id="683a5-132">끌어서 hello **열 프로젝션** hello 캔버스에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="683a5-133">클릭 **열 선택기 시작** hello 속성 창 toospecify toodrop 원하는 열에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="683a5-134">![프로젝트 열][4]</span><span class="sxs-lookup"><span data-stu-id="683a5-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="683a5-135">다음 두 열을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="683a5-136">![불필요한 열 제거][5]</span><span class="sxs-lookup"><span data-stu-id="683a5-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="683a5-137">3. Hello 모델 작성</span><span class="sxs-lookup"><span data-stu-id="683a5-137">3. Build hello model</span></span>
<span data-ttu-id="683a5-138">Hello 데이터 80-20 분할 합니다: 80 %tootrain 기계 학습 모델 및 20% tootest hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="683a5-139">해 드립니다이 이진 분류 문제에 대 한 hello "2 클래스" 알고리즘을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="683a5-140">끌어서 hello **분할** hello 캔버스에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="683a5-141">Hello 첫 번째 hello 속성 창에서 출력 데이터 집합의 행 비율을 0.8를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="683a5-142">![훈련 및 테스트 집합으로 데이터 분할][6]</span><span class="sxs-lookup"><span data-stu-id="683a5-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="683a5-143">끌어서 hello **2 클래스 승격 된 의사 결정 트리** hello 캔버스에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="683a5-144">끌어서 hello **모델 학습** 모듈 hello로 캔버스 및 hello 입력을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="683a5-145">클릭 **열 선택기 시작** hello 속성 창에서.</span><span class="sxs-lookup"><span data-stu-id="683a5-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="683a5-146">첫 번째 입력: ML 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="683a5-147">두 번째 입력이:에서 tootrain hello 알고리즘은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="683a5-148">![Hello 모델 학습 모듈에 연결][7]</span><span class="sxs-lookup"><span data-stu-id="683a5-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="683a5-149">선택 hello **BikeBuyer** 열 toopredict hello 처럼 열입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="683a5-150">![열 toopredict 선택][8]</span><span class="sxs-lookup"><span data-stu-id="683a5-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="683a5-151">4. Hello 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="683a5-151">4. Score hello model</span></span>
<span data-ttu-id="683a5-152">이제 hello 모델 테스트 데이터에서 수행 하는 방법을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="683a5-153">에서는 더 잘 수행 하는 다른 알고리즘 toosee와 원하는 hello 알고리즘을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="683a5-154">끌기 **모델 점수 매기기** hello 캔버스에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="683a5-155">첫 번째 입력이: 두 번째 입력이 모델을 학습: 테스트 데이터 ![hello 모델 점수 매기기][9]</span><span class="sxs-lookup"><span data-stu-id="683a5-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="683a5-156">끌어서 hello **2 클래스 Bayes 지점 컴퓨터** hello 실험 캔버스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="683a5-157">이 알고리즘 비교 toohello 2 클래스 승격 된 의사 결정 트리에서에서 수행 하는 방법을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="683a5-158">복사 및 붙여넣기 hello 모델 학습 및 점수 모델의에서 모듈 hello 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="683a5-159">끌어서 hello **모델 평가** 모듈 hello 캔버스 toocompare hello 두 알고리즘으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="683a5-160">**실행** 실험 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="683a5-161">![Hello 실험을 실행 합니다.][10]</span><span class="sxs-lookup"><span data-stu-id="683a5-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="683a5-162">Hello 모델 평가 모듈 hello 맨 아래에 hello 출력 포트를 클릭 하 고 시각화를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="683a5-163">![평가 결과 시각화][11]</span><span class="sxs-lookup"><span data-stu-id="683a5-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="683a5-164">제공 된 hello 메트릭을 hello ROC 곡선을 정밀도 회수 다이어그램 이며 곡선 리프트 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="683a5-165">이러한 메트릭을 볼 hello 두 번째 식 보다 더 잘 수행 hello 첫 번째 모델을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="683a5-166">toolook에 hello 예측 하는 첫 번째 모델링 hello 기능, hello 모델 점수 매기기의 출력 포트를 클릭 하 고 시각화를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="683a5-167">![점수 결과 시각화][12]</span><span class="sxs-lookup"><span data-stu-id="683a5-167">![Visualize score results][12]</span></span>

<span data-ttu-id="683a5-168">두 개 이상의 열 tooyour 테스트 데이터 집합을 추가 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="683a5-169">점수가 매겨진된 확률: hello 가능성 고객이 자전거 구매자 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="683a5-170">점수가 매겨진된 레이블: hello 분류 hello 모델 – bike buyer (1)에 의해 수행 여부 (0)입니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="683a5-171">레이블 지정에 대 한 확률 임계값이 too50% 설정 되어 있으며 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="683a5-172">Hello 열 hello 점수가 매겨진 레이블 (예측) BikeBuyer (실제)를 비교 hello 모델 수행한 얼마나 잘 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="683a5-173">다음 단계로이 모델 toomake 예측 신규 고객에 대 한 사용 및이 모델을 웹 서비스로 게시 하거나 결과 백 tooSQL 데이터 웨어하우스 쓰기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="683a5-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="683a5-174">Next steps</span></span>
<span data-ttu-id="683a5-175">toolearn 예측 기계 학습 모델을 작성에 대 한 참조를 너무[소개 tooMachine Azure에서 학습][Introduction tooMachine Learning on Azure]합니다.</span><span class="sxs-lookup"><span data-stu-id="683a5-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

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
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
