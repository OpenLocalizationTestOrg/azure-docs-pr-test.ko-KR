---
title: "Azure Machine Learning 웹 서비스에서 가져오기/내보내기 데이터 사용 | Microsoft Docs"
description: "데이터 가져오기 및 내보내기 데이터 모듈을 사용하여 웹 서비스에서 데이터를 보내고 받는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 123c8c2b1c5bae268b2a61c185743f2c3920175e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="5b877-103">데이터 가져오기 및 데이터 내보내기 모듈을 사용하는 Azure ML 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5b877-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="5b877-104">예측 실험을 만들 때 일반적으로 웹 서비스 입력 및 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="5b877-105">실험을 배포하면 소비자는 입력 및 출력을 통해 웹 서비스에서 데이터를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span></span> <span data-ttu-id="5b877-106">일부 응용 프로그램에서는 소비자 데이터를 데이터 피드에서 사용할 수 있거나 해당 데이터가 Azure Blob 저장소와 같은 외부 데이터 원본에 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="5b877-107">이러한 경우 웹 서비스 입력 및 출력을 사용하여 데이터를 읽고 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="5b877-108">대신, BES(배치 실행 서비스)를 사용하여 데이터 가져오기 모듈을 통해 데이터 원본에서 데이터를 읽고, 데이터 내보내기 모듈을 통해 다른 데이터 위치에 점수 매기기 결과를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span></span>

<span data-ttu-id="5b877-109">데이터 가져오기 및 내보내기 데이터 모듈은 HTTP를 통한 웹 URL, Hive 쿼리, Azure SQL Database, Azure Table Storage, Azure Blob Storage, 데이터 피드 또는 온-프레미스 SQL Database 등의 다양한 데이터 위치에서 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="5b877-110">이 항목에서는 "샘플 5: 이진 분류에 대한 학습, 테스트, 평가: 성인 데이터 집합" 샘플을 사용하고 데이터 집합이 censusdata라는 Azure SQL 테이블에 이미 로드되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-the-training-experiment"></a><span data-ttu-id="5b877-111">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="5b877-111">Create the training experiment</span></span>
<span data-ttu-id="5b877-112">"샘플 5: 이진 분류에 대한 학습, 테스트, 평가: 성인 데이터 집합" 샘플을 열면 성인 인구 조사 소득 이진 분류 데이터 집합이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="5b877-113">또한 캔버스의 실험은 다음 이미지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-113">And the experiment in the canvas will look similar to the following image:</span></span>

![실험의 초기 구성입니다.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="5b877-115">Azure SQL 테이블에서 데이터를 읽으려면</span><span class="sxs-lookup"><span data-stu-id="5b877-115">To read the data from the Azure SQL table:</span></span>

1. <span data-ttu-id="5b877-116">데이터 집합 모듈을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-116">Delete the dataset module.</span></span>
2. <span data-ttu-id="5b877-117">구성 요소 검색 상자에 가져오기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-117">In the components search box, type import.</span></span>
3. <span data-ttu-id="5b877-118">결과 목록에서 *데이터 가져오기* 모듈을 실험 캔버스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-118">From the results list, add an *Import Data* module to the experiment canvas.</span></span>
4. <span data-ttu-id="5b877-119">*데이터 가져오기* 모듈의 출력을 *누락 데이터 정리* 모듈의 입력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="5b877-120">속성 패널의 **Azure SQL 데이터베이스** in the **Azure SQL 데이터베이스** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span></span>
6. <span data-ttu-id="5b877-121">**데이터베이스 서버 이름**, **데이터베이스 이름**, **사용자 이름** 및 **암호** 필드에 데이터베이스에 대한 적절한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span></span>
7. <span data-ttu-id="5b877-122">데이터베이스 쿼리 필드에 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-122">In the Database query field, enter the following query.</span></span>
   
     <span data-ttu-id="5b877-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="5b877-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="5b877-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="5b877-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="5b877-125">실험 캔버스 맨 아래에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-125">At the bottom of the experiment canvas, click **Run**.</span></span>

## <a name="create-the-predictive-experiment"></a><span data-ttu-id="5b877-126">예측 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="5b877-126">Create the predictive experiment</span></span>
<span data-ttu-id="5b877-127">다음에는 웹 서비스를 배포할 예측 실험을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-127">Next you set up the predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="5b877-128">실험 캔버스 맨 아래에서 **웹 서비스 설정**을 클릭하고 **예측 웹 서비스[권장]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="5b877-129">예측 실험에서 *웹 서비스 입력* 및 *웹 서비스 출력 모듈*을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span></span> 
3. <span data-ttu-id="5b877-130">구성 요소 검색 상자에 내보내기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-130">In the components search box, type export.</span></span>
4. <span data-ttu-id="5b877-131">결과 목록에서 *데이터 내보내기* 모듈을 실험 캔버스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-131">From the results list, add an *Export Data* module to the experiment canvas.</span></span>
5. <span data-ttu-id="5b877-132">*모델 점수 매기기* 모듈의 출력을 *데이터 내보내기* 모듈의 입력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span></span> 
6. <span data-ttu-id="5b877-133">속성 패널의 데이터 대상 드롭다운에서 **Azure SQL 데이터베이스** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span></span>
7. <span data-ttu-id="5b877-134">**데이터베이스 서버 이름**, **데이터베이스 이름**, **서버 사용자 계정 이름** 및 **서버 사용자 계정 암호** 필드에 데이터베이스에 대한 적절한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span></span>
8. <span data-ttu-id="5b877-135">**쉼표로 구분된 저장할 열 목록** 필드에 점수가 매겨진 레이블을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="5b877-136">**데이터 테이블 이름 필드**에 dbo.ScoredLabels를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-136">In the **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="5b877-137">이 테이블이 없으면 실험을 실행하거나 웹 서비스를 호출할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span></span>
10. <span data-ttu-id="5b877-138">**쉼표로 구분된 데이터베이스 열 목록** 필드에 점수가 매겨진 레이블을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="5b877-139">최종 웹 서비스를 호출하는 응용 프로그램을 작성하는 경우 런타임에 다른 입력 쿼리 또는 대상 테이블을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span></span> <span data-ttu-id="5b877-140">이러한 입력 및 출력을 구성하려면 웹 서비스 매개 변수 기능을 사용하여 *데이터 가져오기* 모듈 *데이터 원본* 속성 및 *데이터 내보내기* 모드 데이터 대상 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span></span>  <span data-ttu-id="5b877-141">웹 서비스 매개 변수에 대한 자세한 내용은 Cortana Intelligence 및 기계 학습 블로그에서 [AzureML 웹 서비스 매개 변수 항목](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b877-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="5b877-142">가져오기 쿼리 및 대상 테이블에 대한 웹 서비스 매개 변수를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="5b877-142">To configure the Web Service Parameters for the import query and the destination table:</span></span>

1. <span data-ttu-id="5b877-143">*데이터 가져오기* 모듈에 대한 속성 창에서 **데이터베이스 쿼리** 필드 오른쪽 위에 있는 아이콘을 클릭하고 **웹 서비스 매개 변수로 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="5b877-144">*데이터 내보내기* 모듈에 대한 속성 창에서 **데이터 테이블 이름** 필드 오른쪽 위에 있는 아이콘을 클릭하고 **웹 서비스 매개 변수로 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="5b877-145">*데이터 내보내기* 모듈 속성 창 아래쪽의 **웹 서비스 매개 변수** 섹션에서 데이터베이스 쿼리를 클릭하고 이름을 쿼리로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="5b877-146">**데이터 테이블 이름**을 클릭하고 이름을 **테이블**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="5b877-147">완료되면 실험은 다음 이미지와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-147">When you are done, your experiment should look similar to the following image:</span></span>

![실험의 최종 모습입니다.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="5b877-149">이제 실험을 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-149">Now you can deploy the experiment as a web service.</span></span>

## <a name="deploy-the-web-service"></a><span data-ttu-id="5b877-150">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5b877-150">Deploy the web service</span></span>
<span data-ttu-id="5b877-151">기존 또는 새 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-151">You can deploy to either a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="5b877-152">기존 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5b877-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="5b877-153">기존 웹 서비스로 배포하고 해당 서비스를 사용하기 위한 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="5b877-153">To deploy as a Classic Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="5b877-154">실험 캔버스 맨 아래에서 실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-154">At the bottom of the experiment canvas, click Run.</span></span>
2. <span data-ttu-id="5b877-155">실행이 완료되면 **웹 서비스 배포**를 클릭하고 **웹 서비스 배포[클래식]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="5b877-156">웹 서비스 대시보드에서 API 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-156">On the web service dashboard, locate your API key.</span></span> <span data-ttu-id="5b877-157">나중에 사용할 수 있게 복사한 다음 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-157">Copy and save it to use later.</span></span>
4. <span data-ttu-id="5b877-158">**기본 끝점** 테이블에서 **Batch 실행** 링크를 클릭하여 API 도움말 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span></span>
5. <span data-ttu-id="5b877-159">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="5b877-160">API 도움말 페이지 맨 아래에서 **샘플 코드** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span></span>
7. <span data-ttu-id="5b877-161">C# 샘플 코드를 복사하고 Program.cs 파일에 붙여 넣은 후 blob 저장소에 대한 모든 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span></span>
8. <span data-ttu-id="5b877-162">*apiKey* 변수의 값을 이전에 저장된 API 키로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-162">Update the value of the *apiKey* variable with the API key saved earlier.</span></span>
9. <span data-ttu-id="5b877-163">요청 선언을 찾고 *데이터 가져오기* 및 *데이터 내보내기* 모듈에 전달되는 웹 서비스 매개 변수 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="5b877-164">이 경우 원래 쿼리를 사용하지만 새 테이블 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-164">In this case, you use the original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="5b877-165">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-165">Run the application.</span></span> 

<span data-ttu-id="5b877-166">실행이 완료되면 새 테이블이 점수 매기기 결과를 포함하는 데이터베이스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-166">On completion of the run, a new table is added to the database containing the scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="5b877-167">새 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5b877-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="5b877-168">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="5b877-169">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b877-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="5b877-170">새 웹 서비스로 배포하고 해당 서비스를 사용하기 위한 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="5b877-170">To deploy as a New Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="5b877-171">실험 캔버스 맨 아래에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-171">At the bottom of the experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="5b877-172">실행이 완료되면 **웹 서비스 배포**를 클릭하고 **웹 서비스 배포[신규]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="5b877-173">실험 배포 페이지에서 웹 서비스의 이름을 입력하고 가격 책정 계획을 선택한 후 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="5b877-174">**빠른 시작** 페이지에서 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-174">On the **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="5b877-175">**샘플 코드** 섹션에서 **Batch**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-175">In the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="5b877-176">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="5b877-177">C# 샘플 코드를 복사하고 Program.cs 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-177">Copy and paste the C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="5b877-178">*apiKey* 변수 값을 **기본 사용량 정보** 섹션에 있는 **기본 키**로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span></span>
9. <span data-ttu-id="5b877-179">*scoreRequest* 선언을 찾고 *데이터 가져오기* 및 *데이터 내보내기* 모듈에 전달되는 웹 서비스 매개 변수 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="5b877-180">이 경우 원래 쿼리를 사용하지만 새 테이블 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-180">In this case, you use the original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="5b877-181">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b877-181">Run the application.</span></span> 

