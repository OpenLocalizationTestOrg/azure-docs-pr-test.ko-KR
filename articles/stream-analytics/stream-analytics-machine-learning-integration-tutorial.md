---
title: "스트림 분석 및 기계 학습 통합 aaaAzure | Microsoft Docs"
description: "어떻게 toouse 사용자 정의 함수 및 스트림 분석 작업에 대 한 기계 학습"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="e07c1-103">Azure Stream Analytics 및 Azure Machine Learning을 사용한 감정 분석 수행</span><span class="sxs-lookup"><span data-stu-id="e07c1-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="e07c1-104">이 문서에서는 tooquickly Azure 기계 학습을 통합 하는 간단한 Azure 스트림 분석 작업을 설정 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="e07c1-105">Hello Cortana Intelligence 갤러리 tooanalyze 스트리밍 텍스트 데이터에서에서 기계 학습 감성 분석 모델을 사용 하 고이 정보를 실시간으로 hello 감성 점수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="e07c1-106">Hello Cortana Intelligence Suite를 사용 하 여 hello 복잡 한 감성 분석 모델을 작성 하는 방법에 대 한 걱정 없이이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="e07c1-107">이 문서 tooscenarios 이러한에서 배운 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="e07c1-108">스트리밍 Twitter 데이터에 대한 실시간 감정 분석</span><span class="sxs-lookup"><span data-stu-id="e07c1-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="e07c1-109">지원 담당자와 고객 채팅 레코드 분석</span><span class="sxs-lookup"><span data-stu-id="e07c1-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="e07c1-110">포럼, 블로그 및 동영상에 대한 의견 평가</span><span class="sxs-lookup"><span data-stu-id="e07c1-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="e07c1-111">기타 실시간 예측 점수 매기기 시나리오</span><span class="sxs-lookup"><span data-stu-id="e07c1-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="e07c1-112">실제 시나리오에서는 Twitter 데이터 스트림에서 직접 hello 데이터 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="e07c1-113">toosimplify hello 자습서 작성 했습니다 것 수 있도록 hello 스트리밍 분석 작업을 트 윗 Azure Blob 저장소에서 CSV 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="e07c1-114">사용자 고유의 CSV 파일을 만들 수 있습니다 또는 hello 다음 이미지에에서 표시 된 대로 샘플 CSV 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![CSV 파일에서 샘플 트윗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="e07c1-116">hello blob 저장소에서 hello 샘플 텍스트 데이터에 대해 사용자 정의 함수 (UDF)으로 hello 감성 분석 모델을 적용 하는 만드는 hello 스트리밍 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="e07c1-117">hello 출력 (hello 감성 분석 결과 hello)은 toohello를 기록 하는 다른 CSV 파일에서 동일한 blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="e07c1-118">hello 다음 그림에서는이 구성을</span><span class="sxs-lookup"><span data-stu-id="e07c1-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="e07c1-119">언급한 대로 좀 더 현실적인 시나리오에서는 Blob Storage를 Azure Event Hubs 입력의 스트리밍 Twitter 데이터로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="e07c1-120">또한 작성할 수 있습니다는 [Microsoft Power BI](https://powerbi.microsoft.com/) hello 집계 감성의 실시간으로 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Stream Analytics Machine Learning 통합 개요](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="e07c1-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e07c1-122">Prerequisites</span></span>
<span data-ttu-id="e07c1-123">시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="e07c1-124">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e07c1-124">An active Azure subscription.</span></span>
* <span data-ttu-id="e07c1-125">데이터가 포함된 CSV 파일.</span><span class="sxs-lookup"><span data-stu-id="e07c1-125">A CSV file with some data in it.</span></span> <span data-ttu-id="e07c1-126">앞에서 살펴본 hello 파일을 다운로드할 수 있습니다 [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), 하거나 사용자 고유의 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="e07c1-127">이 문서에 대 한 GitHub에서 hello 파일을 사용 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="e07c1-128">상위 수준에서이 문서에서는 표시 되는 toocomplete hello 작업 하면 수행 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="e07c1-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="e07c1-129">Azure 저장소 계정 및 blob 저장소 컨테이너를 만들고 CSV 형식의 입력된 파일이 toohello 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="e07c1-130">Hello Cortana Intelligence 갤러리 tooyour Azure 기계 학습 작업 영역에서 감성 분석 모델을 추가 하 고 hello 기계 학습 작업 영역에서 웹 서비스로이 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="e07c1-131">Hello 텍스트 입력에 대 한 순서 toodetermine 감성에서 함수로이 웹 서비스를 호출 하는 스트림 분석 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="e07c1-132">Hello 스트림 분석 작업을 시작 하 고 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="e07c1-133">저장소 컨테이너를 만들고 hello CSV 입력된 파일을 업로드</span><span class="sxs-lookup"><span data-stu-id="e07c1-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="e07c1-134">이 단계에 대 한 hello GitHub에서 사용할 수 있는 등의 모든 CSV 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="e07c1-135">Hello Azure 포털에서에서 클릭 **새로** &gt; **저장소** &gt; **저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![새 저장소 계정 만들기](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="e07c1-137">이름을 제공 (`samldemo` hello 예제에서).</span><span class="sxs-lookup"><span data-stu-id="e07c1-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="e07c1-138">hello 이름은 소문자 및 숫자를 사용할 수 및 Azure 전체에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="e07c1-139">기존 리소스 그룹을 지정하고 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="e07c1-140">위치에 대 한 모든 hello 리소스 사용이 자습서에서 만든 동일한을 hello 권장 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![저장소 계정 세부 정보 입력](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="e07c1-142">Hello Azure 포털에서에서 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="e07c1-143">저장소 계정 블레이드에서 hello 클릭 **컨테이너** 클릭 하 고  **+ &nbsp;컨테이너** toocreate blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![Blob 컨테이너 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="e07c1-145">Hello 컨테이너에 대 한 이름을 제공 (`azuresamldemoblob` hello 예제에서) 되어 있는지 확인 하 고 **액세스 형식** 너무 설정**Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="e07c1-146">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-146">When you're done, click **OK**.</span></span>

    ![Blob 컨테이너 정보 지정](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="e07c1-148">Hello에 **컨테이너** 블레이드, 선택 hello 새 컨테이너는 해당 컨테이너에 대 한 hello 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="e07c1-149">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-149">Click **Upload**.</span></span>

    ![컨테이너의 '업로드' 단추](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="e07c1-151">Hello에 **업로드 blob** 블레이드에서이 자습서에 대 한 toouse 되도록 hello CSV 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="e07c1-152">에 대 한 **Blob 유형**선택, **블록 blob** 및 집합 hello 블록 too4 MB 하기이 자습서에 충분 한 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![Blob 파일 업로드](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="e07c1-154">Hello 클릭 **업로드** hello hello 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="e07c1-155">Hello Cortana 인텔리전스 갤러리에서에서 hello 감성 분석 모델을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="e07c1-156">이제 hello 샘플 데이터는 blob에 Cortana 인텔리전스 갤러리에서 hello 감성 분석 모델을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="e07c1-157">Toohello 이동 [예측 감성 분석 모델](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) hello Cortana 인텔리전스 갤러리의에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="e07c1-158">**Studio에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, Machine Learning 스튜디오 열기](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="e07c1-160">Toogo toohello 작업 영역에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="e07c1-161">위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-161">Select a location.</span></span>

4. <span data-ttu-id="e07c1-162">클릭 **실행** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="e07c1-163">약 1 분이 걸립니다 hello 프로세스가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-163">hello process runs, which takes about a minute.</span></span>

   ![Machine Learning Studio에서 실험 실행](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="e07c1-165">Hello 프로세스가 성공적으로 실행 된 후에 선택 **웹 서비스 배포** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![Machine Learning Studio에서 실험을 웹 서비스로 배포](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="e07c1-167">감성 분석 모델은 준비 toouse hello toovalidate 클릭 hello **테스트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="e07c1-168">"I love Microsoft"와 같은 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-168">Provide text input such as "I love Microsoft".</span></span> 

   ![Machine Learning Studio에서 실험 테스트](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="e07c1-170">Hello 테스트가 작동 하는 경우 다음 예제 결과 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![Machine Learning Studio의 결과 테스트](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="e07c1-172">Hello에 **앱** 열 hello 클릭 **이전 통합 문서 또는 Excel 2010** 링크 toodownload Excel 통합 문서.</span><span class="sxs-lookup"><span data-stu-id="e07c1-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="e07c1-173">hello API 키 및 이후 tooset hello 스트림 분석 작업을 사용 해야 하는 hello URL hello 통합 문서에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, 간략 상태](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="e07c1-175">Hello 기계 학습 모델을 사용 하는 스트림 분석 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="e07c1-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="e07c1-176">이제 hello 샘플 트 윗을 blob 저장소에 hello CSV 파일에서 읽을 수 있는 스트림 분석 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="e07c1-177">Hello 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="e07c1-177">Create hello job</span></span>

1. <span data-ttu-id="e07c1-178">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="e07c1-179">**새로 만들기** > **사물 인터넷** > **Stream Analytics 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Azure 포털 경로 tooa 새 스트림 분석 작업을 가져오기 위한](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="e07c1-181">이름 hello 작업 `azure-sa-ml-demo`, 구독을 지정, 기존 리소스 그룹을 지정 하거나 새 대시보드를 만든를 hello 작업에 대 한 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![새 Stream Analytics 작업의 설정 지정](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="e07c1-183">Hello 작업 입력 구성</span><span class="sxs-lookup"><span data-stu-id="e07c1-183">Configure hello job input</span></span>
<span data-ttu-id="e07c1-184">hello 작업 이전 tooblob 저장소를 업로드 하는 hello CSV 파일에서 입력을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="e07c1-185">Hello 작업이 만들어진 후에, 아래에서 **작업 토폴로지** hello 작업 블레이드에서 hello 클릭 **입력** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Stream Analytics 작업 블레이드의 '입력' 상자](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="e07c1-187">Hello에 **입력** 블레이드에서 클릭 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![' Add' 입력된 toohello 스트림 분석 작업을 추가 하기 위한 단추](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="e07c1-189">Hello 채울 **새 입력** 블레이드의 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="e07c1-190">**입력된 별칭**: hello 이름 사용 `datainput`합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="e07c1-191">**원본 형식**: **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="e07c1-192">**원본**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="e07c1-193">**가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="e07c1-194">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="e07c1-194">**Storage account**.</span></span> <span data-ttu-id="e07c1-195">이전에 만든 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="e07c1-196">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="e07c1-196">**Container**.</span></span> <span data-ttu-id="e07c1-197">이전에 만든 선택 hello 컨테이너 (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="e07c1-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="e07c1-198">**이벤트 직렬화 형식**</span><span class="sxs-lookup"><span data-stu-id="e07c1-198">**Event serialization format**.</span></span> <span data-ttu-id="e07c1-199">**CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-199">Select **CSV**.</span></span>

    ![새 작업 입력의 설정](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="e07c1-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="e07c1-202">Hello 작업 출력을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-202">Configure hello job output</span></span>
<span data-ttu-id="e07c1-203">hello 작업 보냅니다 결과 toohello 동일한 blob 저장소 입력 가져옵니다입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="e07c1-204">아래 **작업 토폴로지** hello 작업 블레이드에서 hello 클릭 **출력** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Streaming Analytics 작업에 대한 새 출력 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="e07c1-206">Hello에 **출력** 블레이드에서 클릭 **+ 추가**, 다음 hello 별칭으로 출력을 추가 하 고 `datamloutput`합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="e07c1-207">**싱크**에서 **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="e07c1-208">Hello hello 나머지를 입력 한 다음 설정을 사용 하 여 hello 입력에 대 한 hello blob 저장소에 사용 되는 동일한 값을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="e07c1-209">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="e07c1-209">**Storage account**.</span></span> <span data-ttu-id="e07c1-210">이전에 만든 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="e07c1-211">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="e07c1-211">**Container**.</span></span> <span data-ttu-id="e07c1-212">이전에 만든 선택 hello 컨테이너 (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="e07c1-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="e07c1-213">**이벤트 직렬화 형식**</span><span class="sxs-lookup"><span data-stu-id="e07c1-213">**Event serialization format**.</span></span> <span data-ttu-id="e07c1-214">**CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-214">Select **CSV**.</span></span>

   ![새 작업 출력의 설정](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="e07c1-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="e07c1-217">Hello 기계 학습 함수 추가</span><span class="sxs-lookup"><span data-stu-id="e07c1-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="e07c1-218">이전 기계 학습 모델 tooa 웹 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="e07c1-219">이 시나리오에서 hello 스트림 분석 작업이 실행 될 때 보냅니다 각 샘플 윗 감성 분석에 대 한 hello 입력된 toohello 웹 서비스에서.</span><span class="sxs-lookup"><span data-stu-id="e07c1-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="e07c1-220">hello 기계 학습 웹 서비스는 감성 반환 (`positive`, `neutral`, 또는 `negative`) 및 양의 되 고 hello 윗의 확률입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="e07c1-221">Hello 자습서의이 섹션에서는 hello 스트림 분석 작업의 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="e07c1-222">hello 함수 윗 toohello 웹 서비스 호출 된 toosend 일를 돌아갈 hello 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="e07c1-223">Hello 웹 서비스 URL 및 API 키가 이전 hello Excel 통합 문서에서에서 다운로드 한 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="e07c1-224">Toohello 작업 개요 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="e07c1-225">**설정** 아래에서 **함수**를 선택하고 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![함수 toohello 스트림 분석 작업 추가](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="e07c1-227">입력 `sentiment` hello로 별칭를 작동 하 고 이러한 값을 사용 하 여 hello 블레이드 hello 나머지 채울:</span><span class="sxs-lookup"><span data-stu-id="e07c1-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="e07c1-228">**함수 유형**: **Azure ML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="e07c1-229">**가져오기 옵션**: **다른 구독에서 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="e07c1-230">이렇게 하면 기회 tooenter hello URL과 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="e07c1-231">**URL**: hello 웹 서비스 URL에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="e07c1-232">**키**: hello API 키에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-232">**Key**: Paste in hello API key.</span></span>
  
    ![기계 학습 함수 toohello 스트림 분석 작업을 추가 하는 것에 대 한 설정](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="e07c1-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="e07c1-235">쿼리 tootransform hello 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="e07c1-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="e07c1-236">Stream Analytics는 선언적 이며 SQL 기반 쿼리 tooexamine hello 입력을 사용 하 고 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="e07c1-237">이 섹션에서는 입력 으로부터 각 윗을 읽고 다음 hello 기계 학습 함수 tooperform 감성 분석을 호출 하는 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="e07c1-238">hello 쿼리는 다음 hello 결과 toohello (blob storage)를 정의 하는 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="e07c1-239">Toohello 작업 개요 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="e07c1-240">아래 **작업 토폴로지**, hello 클릭 **쿼리** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Streaming Analytics 작업에 쿼리 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="e07c1-242">다음 쿼리에서 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="e07c1-243">이전에 만든 hello 함수를 호출 하는 hello 쿼리 (`sentiment`) hello 입력의 각 트 윗에 순서 tooperform 감성 분석에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="e07c1-244">클릭 **저장** toosave hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="e07c1-245">Hello 스트림 분석 작업을 시작 하 고 hello 출력 확인</span><span class="sxs-lookup"><span data-stu-id="e07c1-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="e07c1-246">이제 hello 스트림 분석 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="e07c1-247">Hello 작업 시작</span><span class="sxs-lookup"><span data-stu-id="e07c1-247">Start hello job</span></span>
1. <span data-ttu-id="e07c1-248">Toohello 작업 개요 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="e07c1-249">클릭 **시작** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-249">Click **Start** at hello top of hello blade.</span></span>

    ![Streaming Analytics 작업에 쿼리 만들기](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="e07c1-251">Hello에 **시작 작업**선택, **사용자 지정**를 선택한 후 1 일 이전 toowhen hello CSV 파일 tooblob 저장소를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="e07c1-252">완료되면 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="e07c1-253">Hello 출력 확인</span><span class="sxs-lookup"><span data-stu-id="e07c1-253">Check hello output</span></span>
1. <span data-ttu-id="e07c1-254">Let hello 작업 hello에서 작업을 볼 때까지 몇 분 동안 실행 **모니터링** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="e07c1-255">일반적으로 blob 저장소의 tooexamine hello 콘텐츠를 사용 하는 도구를 사용 하도록 설정한 경우 해당 도구 tooexamine hello를 사용 하 여 `azuresamldemoblob` 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="e07c1-256">또는 않습니다 hello hello Azure 포털의에서 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="e07c1-257">Hello 포털에서 찾을 hello `samldemo` 저장소 계정을 찾을 hello hello 계정 내에서 한 `azuresamldemoblob` 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="e07c1-258">Hello 컨테이너에 두 파일이 표시: hello hello 샘플 트 윗을 포함 하는 파일 및 hello 스트림 분석 작업에 의해 생성 된 CSV 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="e07c1-259">Hello 생성 된 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Blob Storage에서 CSV 작업 출력 다운로드](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="e07c1-261">열기 hello CSV 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-261">Open hello generated CSV file.</span></span> <span data-ttu-id="e07c1-262">다음 예제는 hello 같은 결과가 표시:</span><span class="sxs-lookup"><span data-stu-id="e07c1-262">You see something like hello following example:</span></span>  
   
   ![Stream Analytics Machine Learning, CSV 보기](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="e07c1-264">메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="e07c1-264">View metrics</span></span>
<span data-ttu-id="e07c1-265">또한 Azure Machine Learning 함수 관련 메트릭도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="e07c1-266">다음 함수 관련 메트릭 hello hello에 표시 되는 **모니터링** hello 작업 블레이드에서 상자:</span><span class="sxs-lookup"><span data-stu-id="e07c1-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="e07c1-267">**요청 함수** hello 수가 전송 된 요청 tooa 기계 학습 웹 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="e07c1-268">**이벤트 함수** hello hello 요청에 있는 이벤트 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="e07c1-269">기본적으로 각 요청 tooa 기계 학습 웹 서비스 too1, 000 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e07c1-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="e07c1-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e07c1-270">Next steps</span></span>

* [<span data-ttu-id="e07c1-271">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="e07c1-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e07c1-272">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="e07c1-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e07c1-273">REST API 및 Machine Learning 통합</span><span class="sxs-lookup"><span data-stu-id="e07c1-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="e07c1-274">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="e07c1-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



