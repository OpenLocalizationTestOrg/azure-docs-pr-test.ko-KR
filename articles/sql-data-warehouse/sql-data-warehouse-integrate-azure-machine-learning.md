---
title: "SQL 데이터 웨어하우스에 Azure 기계 학습 aaaUse | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="bdc11-103">SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용</span><span class="sxs-lookup"><span data-stu-id="bdc11-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="bdc11-104">Azure 기계 학습 SQL 데이터 웨어하우스의 데이터에 대해 toocreate 예측 모델을 사용할 수 있으며 다음 준비를 사용 하는 웹 서비스로 게시 하는 완전히 관리 되는 예측 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="bdc11-105">예측 분석의 hello 기본 사항 학습 하 고 기계 학습을 읽어 [소개 tooMachine Azure에서 학습][Introduction tooMachine Learning on Azure]합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="bdc11-106">방법 toocreate, 학습, 점수 및 hello를 사용 하 여 기계 학습 모델을 테스트 한 다음 알아보십시오 [만들기 실험 자습서][Create experiment tutorial]합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="bdc11-107">이 문서에서는 살펴보겠습니다 어떻게 hello를 사용 하 여 다음 toodo hello [Azure 기계 학습 스튜디오][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="bdc11-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="bdc11-108">데이터베이스 toocreate에서 데이터 읽기, 학습 및 예측 모델 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="bdc11-109">데이터 tooyour 데이터베이스 쓰기</span><span class="sxs-lookup"><span data-stu-id="bdc11-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="bdc11-110">SQL 데이터 웨어하우스에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="bdc11-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="bdc11-111">우리는 hello AdventureWorksDW 데이터베이스의 Product 테이블에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bdc11-112">1단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-112">Step 1</span></span>
<span data-ttu-id="bdc11-113">클릭 하 여 새 실험 시작 + hello hello 기계 학습 스튜디오 창 맨 아래에 새 실험을 선택한 다음 빈 실험을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="bdc11-114">선택 hello 기본 hello hello 캔버스 맨 위에 있는 이름 실험을 toosomething 의미 있는 예를 들어 자전거 가격 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="bdc11-115">2단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-115">Step 2</span></span>
<span data-ttu-id="bdc11-116">데이터 집합의 hello 팔레트에 hello 판독기 모듈 및 모듈 hello 실험 캔버스의 왼쪽 hello 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="bdc11-117">Hello 모듈 toohello 실험 캔버스를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="bdc11-118">3단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-118">Step 3</span></span>
<span data-ttu-id="bdc11-119">Hello 판독기 모듈을 선택 하 고 hello 속성 창 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="bdc11-120">Hello 데이터 원본으로 Azure SQL 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="bdc11-121">데이터베이스 서버 이름: 종류 hello 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="bdc11-122">Hello를 사용할 수 있습니다 [Azure 포털] [ Azure portal] toofind이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="bdc11-123">데이터베이스 이름: 방금 지정한 hello 서버에 있는 데이터베이스의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="bdc11-124">서버 사용자 계정 이름: hello hello 데이터베이스에 대 한 액세스 권한이 있는 계정의 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="bdc11-125">서버 사용자 계정 암호: 제공 hello에 대 한 hello 암호가 사용자 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="bdc11-126">모든 서버 인증서 수락: tooskip 데이터를 읽기 전에 먼저 hello 사이트 인증서를 검토 하려는 경우이 옵션 (보안 수준 낮음)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="bdc11-127">쿼리 만들기: tooread 원하는 hello 데이터를 설명 하는 SQL 문을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="bdc11-128">이 경우 다음 쿼리는 hello를 사용 하 여 Product 테이블에서 데이터를 읽이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="bdc11-129">4단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-129">Step 4</span></span>
1. <span data-ttu-id="bdc11-130">Hello 실험 캔버스에서 실행을 클릭 하 여 hello 실험을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="bdc11-131">Hello 실험 완료 되 면 hello 판독기 모듈 성공적으로 완료 된 녹색 확인 표시가 tooindicate를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="bdc11-132">또한 hello 오른쪽 위 모서리에서 실행 중 상태로 마침 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="bdc11-133">toosee 가져온된 데이터 hello hello 아래쪽 hello 자동차 데이터 집합의 출력 포트 hello 누르고 시각화를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="bdc11-134">모델 만들기, 훈련 및 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="bdc11-134">Create, train and score a model</span></span>
<span data-ttu-id="bdc11-135">이제 이 데이터 집합을 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="bdc11-136">모델 만들기: 데이터 처리 및 기능 정의</span><span class="sxs-lookup"><span data-stu-id="bdc11-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="bdc11-137">Hello 모델 학습: 선택 하 고 학습 알고리즘을 적용</span><span class="sxs-lookup"><span data-stu-id="bdc11-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="bdc11-138">점수 및 테스트 hello 모델: 새 자전거 가격 예측</span><span class="sxs-lookup"><span data-stu-id="bdc11-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="bdc11-139">toolearn 방법 toocreate, 학습, 점수 및 기계 학습 모델 사용 하 여 hello를 테스트 하는 방법에 대 한 자세한 [만들기 실험 자습서][Create experiment tutorial]합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="bdc11-140">데이터 tooAzure SQL 데이터 웨어하우스 쓰기</span><span class="sxs-lookup"><span data-stu-id="bdc11-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="bdc11-141">Hello 결과 집합 tooProductPriceForecast 테이블 hello AdventureWorksDW 데이터베이스에 작성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bdc11-142">1단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-142">Step 1</span></span>
<span data-ttu-id="bdc11-143">데이터 집합의 hello 팔레트에 hello 기록기 모듈 및 모듈 hello 실험 캔버스의 왼쪽 hello 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="bdc11-144">Hello 모듈 toohello 실험 캔버스를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="bdc11-145">2단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-145">Step 2</span></span>
<span data-ttu-id="bdc11-146">Hello 기록기 모듈을 선택 하 고 hello 속성 창 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="bdc11-147">Hello 데이터 대상으로 Azure SQL 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="bdc11-148">데이터베이스 서버 이름: 종류 hello 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="bdc11-149">Hello를 사용할 수 있습니다 [Azure 포털] [ Azure portal] toofind이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="bdc11-150">데이터베이스 이름: 방금 지정한 hello 서버에 있는 데이터베이스의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="bdc11-151">서버 사용자 계정 이름: hello hello 데이터베이스에 대 한 쓰기 권한이 있는 계정의 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="bdc11-152">서버 사용자 계정 암호: 제공 hello에 대 한 hello 암호가 사용자 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="bdc11-153">(안전 하지 않음) 모든 서버 인증서 수락: tooview hello 인증서를 표시 하지 않으려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="bdc11-154">쉼표로 구분 된 목록이 저장 열 toobe: toooutput 원하는 hello 데이터 집합 또는 결과 열 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="bdc11-155">데이터 테이블 이름: hello 데이터 테이블의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="bdc11-156">Datatable 열의 쉼표로 구분 된 목록: hello 새 테이블에 열 이름을 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="bdc11-157">hello 열 이름은 다를 수 있습니다 hello 원본 데이터 집합에 hello 것 이지만 나열 해야 hello 출력 테이블에 대 한 정의 하는 동일한 수의 열을 여기 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="bdc11-158">SQL Azure 작업당 작성 된 행 수: hello tooa SQL 데이터베이스를 한 번에 작성 된 행 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="bdc11-159">3단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-159">Step 3</span></span>
1. <span data-ttu-id="bdc11-160">Hello 실험 캔버스에서 실행을 클릭 하 여 hello 실험을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="bdc11-161">Hello 실험 완료 되 면 모든 모듈은 성공적으로 완료 된 녹색 확인 표시가 tooindicate를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc11-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdc11-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdc11-162">Next steps</span></span>
<span data-ttu-id="bdc11-163">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdc11-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
