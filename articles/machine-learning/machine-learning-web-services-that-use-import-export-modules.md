---
title: "Azure 기계 학습 웹 서비스에서 가져오기/내보내기 데이터 aaaUsing | Microsoft Docs"
description: "Toouse 데이터 가져오기 및 내보내기 데이터 모듈 toosend hello 하 고 웹 서비스에서 데이터를 수신 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="2d9d8-103">데이터 가져오기 및 데이터 내보내기 모듈을 사용하는 Azure ML 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="2d9d8-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="2d9d8-104">예측 실험을 만들 때 일반적으로 웹 서비스 입력 및 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="2d9d8-105">Hello 실험을 배포 하면 소비자가 보내고 hello 입 / 출력을 통해 hello 웹 서비스에서 데이터를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="2d9d8-106">일부 응용 프로그램에서는 소비자 데이터를 데이터 피드에서 사용할 수 있거나 해당 데이터가 Azure Blob 저장소와 같은 외부 데이터 원본에 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="2d9d8-107">이러한 경우 웹 서비스 입력 및 출력을 사용하여 데이터를 읽고 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="2d9d8-108">수, 대신 hello 일괄 처리 실행 서비스 (BES) tooread 데이터 데이터 가져오기 모듈을 사용 하 여 hello 데이터 소스에서 사용 하 고 결과 데이터 내보내기 모듈을 사용 하 여 tooa 다른 데이터 위치 점수 매기기 hello.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="2d9d8-109">hello 데이터 가져오기 및 내보내기 데이터 모듈에서 읽고 쓸 수는 온-프레미스 SQL 데이터베이스 또는 toovarious 데이터는 HTTP, Hive 쿼리, Azure SQL 데이터베이스, Azure 테이블 저장소, Azure Blob 저장소, 데이터 피드를 통해 웹 URL 등의 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="2d9d8-110">이 항목에서는 hello "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합" 샘플링 하 고 hello 데이터 집합 censusdata 라는 Azure SQL 테이블에 이미 로드 된 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="2d9d8-111">Hello 학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="2d9d8-111">Create hello training experiment</span></span>
<span data-ttu-id="2d9d8-112">Hello를 열 때 "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합" 사용 하 여 hello 샘플 성인 인구 조사 소득 이진 분류 데이터 집합을 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="2d9d8-113">및 hello 캔버스의 hello 실험 비슷한 toohello 다음 이미지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Hello 실험의 초기 구성입니다.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="2d9d8-115">tooread hello Azure SQL 테이블에서 데이터를 hello:</span><span class="sxs-lookup"><span data-stu-id="2d9d8-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="2d9d8-116">Hello dataset 모듈을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="2d9d8-117">Hello 구성 요소 검색 상자에 가져오기 '를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="2d9d8-118">Hello 결과 목록에서 추가 된 *데이터 가져오기* 모듈 toohello 실험 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="2d9d8-119">Hello 출력에 연결 *데이터 가져오기* hello의 모듈 hello 입력 *누락 데이터 정리* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="2d9d8-120">속성 창에서 선택 **Azure SQL 데이터베이스** hello에 **데이터 원본** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="2d9d8-121">Hello에 **데이터베이스 서버 이름**, **데이터베이스 이름**, **사용자 이름**, 및 **암호** 필드 hello에 대 한 적절 한 정보 입력 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="2d9d8-122">다음 쿼리에서 hello hello 데이터베이스 쿼리 필드에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="2d9d8-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="2d9d8-123">select [age],</span></span>
   
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
     <span data-ttu-id="2d9d8-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="2d9d8-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="2d9d8-125">Hello 실험 캔버스의 hello 아래쪽 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="2d9d8-126">Hello 예측 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="2d9d8-126">Create hello predictive experiment</span></span>
<span data-ttu-id="2d9d8-127">그런 다음 웹 서비스를 배포 하는 hello 예측 실험을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="2d9d8-128">Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **예측 웹 서비스 [권장]**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="2d9d8-129">Hello 제거 *웹 서비스 입력* 및 *웹 서비스 출력 모듈* hello 예측 실험에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="2d9d8-130">Hello 구성 요소 검색 상자에 내보내기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="2d9d8-131">Hello 결과 목록에서 추가 된 *데이터 내보내기* 모듈 toohello 실험 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="2d9d8-132">Hello 출력에 연결 *모델 점수 매기기* hello의 모듈 hello 입력 *데이터 내보내기* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="2d9d8-133">속성 창에서 선택 **Azure SQL 데이터베이스** hello 데이터 대상 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="2d9d8-134">Hello에 **데이터베이스 서버 이름**, **데이터베이스 이름**, **서버 사용자 계정 이름**, 및 **서버 사용자 계정 암호** 필드 입력 hello 데이터베이스에 대 한 적절 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="2d9d8-135">Hello에 **쉼표로 구분한 목록입니다. 저장 하는 열 toobe** 필드 점수가 매겨진 레이블을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="2d9d8-136">Hello에 **데이터 테이블 이름 필드**, dbo를 입력 합니다. ScoredLabels 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="2d9d8-137">Hello 테이블이 존재 하지 않는 경우 실행 되는 hello 실험 또는 hello 웹 서비스를 호출할 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="2d9d8-138">Hello에 **쉼표로 구분 된 데이터 테이블 열 목록** 필드 ScoredLabels를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="2d9d8-139">Hello 최종 웹 서비스를 호출 하는 응용 프로그램을 작성, 할 수 있습니다 toospecify 다른 입력된 쿼리 또는 대상 테이블에서 런타임에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="2d9d8-140">tooconfigure 이러한 입력 및 출력을 사용 하 여 hello 웹 서비스 매개 변수 기능 tooset hello *데이터 가져오기* 모듈 *데이터 소스* 속성과 hello *데이터 내보내기* 모드 데이터 대상 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="2d9d8-141">웹 서비스 매개 변수에 대 한 자세한 내용은 참조 hello [AzureML 웹 서비스 매개 변수 항목](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) hello Cortana 인텔리전스 및 기계 학습 블로그.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="2d9d8-142">tooconfigure hello hello 가져오기 쿼리 및 hello 대상 테이블에 대 한 웹 서비스 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="2d9d8-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="2d9d8-143">Hello에 대 한 hello 속성 창에서 *데이터 가져오기* 모듈을 hello에 hello 아이콘을 클릭 hello의 오른쪽 위에 **데이터베이스 쿼리** 필드 및 선택 **웹 서비스 매개 변수로 설정할**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="2d9d8-144">Hello에 대 한 hello 속성 창에서 *데이터 내보내기* 모듈을 hello에 hello 아이콘을 클릭 hello의 오른쪽 위에 **데이터 테이블 이름** 필드 및 선택 **웹 서비스 매개 변수로 설정할**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="2d9d8-145">Hello hello 맨 아래에 *데이터 내보내기* 모듈 속성 창의 hello **웹 서비스 매개 변수가** 섹션 데이터베이스 쿼리를 클릭 하 고 쿼리 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="2d9d8-146">**데이터 테이블 이름**을 클릭하고 이름을 **테이블**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="2d9d8-147">완료 되 면 다음 이미지와 비슷한 toohello 실험 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-147">When you are done, your experiment should look similar toohello following image:</span></span>

![실험의 최종 모습입니다.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="2d9d8-149">이제 hello 실험을 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="2d9d8-150">Hello 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-150">Deploy hello web service</span></span>
<span data-ttu-id="2d9d8-151">Tooeither 클래식 또는 새 웹 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="2d9d8-152">기존 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="2d9d8-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="2d9d8-153">클래식 웹 서비스로 toodeploy 응용 프로그램 tooconsume를 만들고 해당:</span><span class="sxs-lookup"><span data-stu-id="2d9d8-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="2d9d8-154">Hello 실험 캔버스의 hello 맨 아래에 실행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="2d9d8-155">Hello 실행이 완료 되 면 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="2d9d8-156">Hello 웹 서비스 대시보드에서 API 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="2d9d8-157">복사한 toouse 나중 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="2d9d8-158">Hello에 **기본 끝점** 테이블에서 hello **일괄 처리 실행** 링크 tooopen hello API 도움말 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="2d9d8-159">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="2d9d8-160">Hello API 도움말 페이지를 찾을 hello **샘플 코드** hello hello 페이지 맨 아래에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="2d9d8-161">복사 하 여 Program.cs 파일에 hello C# 예제 코드를 붙여 넣고 모든 toohello blob 저장소 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="2d9d8-162">Hello에 hello 값을 업데이트 *apiKey* 이전에 저장 하는 hello API 키가 있는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="2d9d8-163">Toohello 전달 되는 웹 서비스 매개 변수 hello 요청 선언과 업데이트 hello 값을 찾을 *데이터 가져오기* 및 *데이터 내보내기* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="2d9d8-164">이 경우 hello 원래 쿼리를 사용 하지만 새 테이블 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="2d9d8-165">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-165">Run hello application.</span></span> 

<span data-ttu-id="2d9d8-166">Hello 실행 완료 되 면 새 테이블 hello 평가 결과 포함 하는 toohello 데이터베이스를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="2d9d8-167">새 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="2d9d8-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="2d9d8-168">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="2d9d8-169">자세한 내용은 참조 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="2d9d8-170">새 웹 서비스로 toodeploy 응용 프로그램 tooconsume를 만들고 해당:</span><span class="sxs-lookup"><span data-stu-id="2d9d8-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="2d9d8-171">Hello 실험 캔버스의 hello 아래쪽 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="2d9d8-172">Hello 실행이 완료 되 면 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [New]**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="2d9d8-173">Hello 실험 배포 페이지에서 웹 서비스에 대 한 이름을 입력 하 고 가격 계획을 선택한 다음 클릭 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="2d9d8-174">Hello에 **퀵 스타트** 페이지 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="2d9d8-175">Hello에 **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="2d9d8-176">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="2d9d8-177">복사 하 여 Program.cs 파일에 hello C# 예제 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="2d9d8-178">Hello에 hello 값을 업데이트 *apiKey* hello로 변수 **기본 키** hello에 **기본 소비 정보** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="2d9d8-179">Hello 찾을 *scoreRequest* toohello 전달 되는 웹 서비스 매개 변수 선언 및 업데이트 hello 값 *데이터 가져오기* 및 *데이터 내보내기* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="2d9d8-180">이 경우 hello 원래 쿼리를 사용 하지만 새 테이블 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-180">In this case, you use hello original query, but define a new table name.</span></span>
   
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
10. <span data-ttu-id="2d9d8-181">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d9d8-181">Run hello application.</span></span> 

