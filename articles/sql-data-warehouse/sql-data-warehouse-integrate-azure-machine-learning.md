---
title: "SQL Data Warehouse와 함께 Azure Machine Learning 사용 | Microsoft Docs"
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="bd66f-103">SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용</span><span class="sxs-lookup"><span data-stu-id="bd66f-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="bd66f-104">Azure 기계 학습은 SQL 데이터 웨어하우스의 데이터에 대해 예측 모델을 만드는 데 사용할 수 있는 완전한 관리 예측 분석 서비스로, 사용할 준비가 된 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="bd66f-105">[Azure에서 기계 학습 소개][Introduction to Machine Learning on Azure]를 읽어 예측 분석의 기본 사항 및 기계 학습에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="bd66f-106">그런 다음 [실험 만들기 자습서][Create experiment tutorial]를 사용하여 기계 학습 모델을.만들고, 훈련하고, 점수를 매기고 테스트하는 방법에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="bd66f-107">이 문서에서는 [Azure 기계 학습 스튜디오][Azure Machine Learning Studio]를 사용하여 다음을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="bd66f-108">데이터베이스에서 데이터를 읽어, 예측 모델을 만들고 훈련하고 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="bd66f-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="bd66f-109">데이터베이스에 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="bd66f-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="bd66f-110">SQL 데이터 웨어하우스에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="bd66f-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="bd66f-111">AdventureWorksDW 데이터베이스의 Product 테이블에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bd66f-112">1단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-112">Step 1</span></span>
<span data-ttu-id="bd66f-113">기계 학습 스튜디오 창의 아래쪽에서 +NEW를 클릭하여 새 실험을 시작한 다음 EXPERIMENT, Blank Experiment를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="bd66f-114">캔버스 위에서 기본 실험 이름을 선택하고 의미 있는 이름(예: 자전거 가격 예측)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="bd66f-115">2단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-115">Step 2</span></span>
<span data-ttu-id="bd66f-116">데이터 집합의 팔레트에서 판독기 모듈 및 실험 캔버스의 왼쪽에 있는 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="bd66f-117">실험 캔버스에 모듈을 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="bd66f-118">3단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-118">Step 3</span></span>
<span data-ttu-id="bd66f-119">판독기 모듈을 선택하고 속성 창을 완성합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="bd66f-120">Azure SQL 데이터베이스를 데이터 원본으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="bd66f-121">데이터베이스 서버 이름: 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-121">Database server name: Type the server name.</span></span> <span data-ttu-id="bd66f-122">[Azure Portal][Azure portal]을 사용하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="bd66f-123">데이터베이스 이름: 방금 지정한 서버에서 데이터베이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="bd66f-124">서버 사용자 계정 이름: 데이터베이스에 대한 액세스 권한이 있는 계정의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="bd66f-125">서버 사용자 계정 암호: 지정된 사용자 계정에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="bd66f-126">모든 서버 인증서 수락: 데이터를 읽기 전에 사이트 인증서 검토를 건너뛰려면 이 옵션을 사용합니다(보안 수준 낮음).</span><span class="sxs-lookup"><span data-stu-id="bd66f-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="bd66f-127">데이터베이스 쿼리: 읽을 데이터를 설명하는 SQL 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="bd66f-128">이 경우 다음 쿼리를 사용하여 Product 테이블에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="bd66f-129">4단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-129">Step 4</span></span>
1. <span data-ttu-id="bd66f-130">실험 캔버스에서 RUN을 클릭하여 실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="bd66f-131">실험이 완료되면 판독기 모듈에 녹색 확인 표시가 생겨 성공적으로 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="bd66f-132">오른쪽 위 모서리에서 실행 완료 상태도 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="bd66f-133">가져온 데이터를 확인하려면 자동차 데이터 집합 아래에서 출력 포트를 클릭하고 Visualize를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="bd66f-134">모델 만들기, 훈련 및 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="bd66f-134">Create, train and score a model</span></span>
<span data-ttu-id="bd66f-135">이제 이 데이터 집합을 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="bd66f-136">모델 만들기: 데이터 처리 및 기능 정의</span><span class="sxs-lookup"><span data-stu-id="bd66f-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="bd66f-137">모델 교육: 학습 알고리즘 선택 및 적용</span><span class="sxs-lookup"><span data-stu-id="bd66f-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="bd66f-138">모델 점수 매기기 및 테스트: 새 자전거 가격 예측</span><span class="sxs-lookup"><span data-stu-id="bd66f-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="bd66f-139">기계 학습 모델을.만들고, 훈련하고, 점수를 매기고 테스트하는 방법에 대해 알려면 [실험 만들기 자습서][Create experiment tutorial]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="bd66f-140">Azure SQL 데이터 웨어하우스에 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="bd66f-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bd66f-141">결과 집합을 AdventureWorksDW 데이터베이스의 ProductPriceForecast 테이블에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bd66f-142">1단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-142">Step 1</span></span>
<span data-ttu-id="bd66f-143">데이터 집합의 팔레트에서 기록기 모듈 및 실험 캔버스의 왼쪽에 있는 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="bd66f-144">실험 캔버스에 모듈을 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="bd66f-145">2단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-145">Step 2</span></span>
<span data-ttu-id="bd66f-146">기록기 모듈을 선택하고 속성 창을 완성합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="bd66f-147">Azure SQL 데이터베이스를 데이터 대상으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="bd66f-148">데이터베이스 서버 이름: 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-148">Database server name: Type the server name.</span></span> <span data-ttu-id="bd66f-149">[Azure Portal][Azure portal]을 사용하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="bd66f-150">데이터베이스 이름: 방금 지정한 서버에서 데이터베이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="bd66f-151">서버 사용자 계정 이름: 데이터베이스에 대한 쓰기 권한이 있는 계정의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="bd66f-152">서버 사용자 계정 암호: 지정된 사용자 계정에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="bd66f-153">(안전하지 않은) 모든 서버 인증서 수락: 인증서를 보지 않으려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="bd66f-154">저장될 열의 쉼표로 구분된 목록: 출력하려면 데이터 집합 또는 결과 열 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="bd66f-155">데이터 테이블 이름: 데이터 테이블의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="bd66f-156">데이터 테이블 열의 쉼표로 구분된 목록: 새 테이블에 사용할 열 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="bd66f-157">열 이름은 원본 데이터 집합의 열과 다를 수 있지만, 출력 테이블에 대해 여기에서 정의한 동일한 열 수를 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="bd66f-158">SQL Azure 작업당 작성된 행 수: 하나의 작업으로 SQL 데이터베이스에 기록되는 행의 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="bd66f-159">3단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-159">Step 3</span></span>
1. <span data-ttu-id="bd66f-160">실험 캔버스에서 RUN을 클릭하여 실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="bd66f-161">실험이 완료되면 모든 모듈에 성공적으로 완료되었음을 나타내는 녹색 확인 표시가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd66f-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd66f-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd66f-162">Next steps</span></span>
<span data-ttu-id="bd66f-163">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd66f-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
